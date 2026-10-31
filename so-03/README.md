# SO-03 · Log pipeline and detections

> Edge and identity logs in one place, with detections tested before they page anyone.

**Industry:** Security operations · **Typical owner:** Security engineering lead · **Reading time:** 8 min

## Who this is for
Mid-market companies with a security team of a handful of people and no 24/7 SOC, whose logs sit in many consoles with different retention. This fits if investigations start with exporting CSV files, if a source can stop sending unnoticed, if detections have no tests or owner, or if new rules page people before anyone knows how noisy they are.

## How it runs today
1. Logs stay in each product's console at default retention. Some sources aren't collected at all.
2. During an investigation, analysts export files from each console and join them by hand on user, address and time.
3. Some sources reach the SIEM. When a vendor changes its format, parsing breaks silently until a search comes back empty.
4. Detections are written in the SIEM's interface by whoever has time, with no version history, tests or owner.
5. New detections go straight to paging. Noisy ones get muted instead of fixed.
6. Nobody can say which attacks you would catch.
7. Retention follows defaults or cost, not an agreed policy.

The hours go to exporting and joining logs, fixing parsers after the fact and handling pages from untested rules. The deeper gap is trust: nobody is sure the data is complete or the rules work.

## Measure your own baseline
Spend one week collecting numbers. Mark last week's pages actionable or not. Ask how much of the last three investigations went to collecting logs. List every log source with owner, destination and retention. Pull last quarter's tickets about broken parsing or missing data, and check people's minute estimates against them.

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Collecting logs for investigations | | | | |
| Fixing parsers and pipelines | | | | |
| Writing and changing detections | | | | |
| Handling false-positive pages | | | | |
| Investigating missing data | | | | |
| **Example** (illustrative values): Handling false-positive pages | On-call analyst | 25 pages | 12 | 5.0 |

Hours per week is volume times minutes, divided by 60. In the example, 25 × 12 / 60 = 5.0.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Source inventory | Drafts an inventory from existing configurations: source, owner, fields, volume, retention. | A security engineer confirms it and sets priority and retention. | A source with no owner goes to the lead. |
| 2. Collection | Drafts field mappings from sample events to a common schema (such as OCSF), with test samples. | The engineer configures collection as code (Logpush for Cloudflare datasets, exports or collectors for the rest) and approves each mapping. | A mapping goes live only after its tests pass. Unmapped fields are kept raw. |
| 3. Pipeline health | Rules watch volume, freshness and parse errors per source. The AI drafts a diagnosis when a source drifts. | The engineer fixes it with the source owner. | Thresholds are deterministic. A critical source going silent is treated as a detection. |
| 4. Search | Turns an analyst's question into a query and shows it before it runs. | The analyst reviews the query, runs it and interprets the results. | Results come from the log store, never from the model. |
| 5. Detection authoring | Drafts a rule from a threat description or past incident, with matching and non-matching test events, severity, runbook outline and MITRE ATT&CK mapping. | A detection engineer edits and owns the rule. A second person reviews the pull request. | No rule merges without passing tests and a reviewer's approval. |
| 6. Testing | A harness runs each rule against its test events: fire on matches, stay quiet otherwise. It replays the rule over recent real logs, and the AI summarizes the result. | The reviewer reads the summary before approving. | A rule that would exceed its agreed volume goes back to the author. |
| 7. Shadow mode | The rule runs in production, writing to a review queue without paging. The AI proposes a label per hit. | The owner labels hits. The lead approves promotion to paging. | Promotion needs the precision target met and a named approver. |
| 8. Tuning and retirement | Flags rules that are noisy, long silent, or tied to a changed source. | The owner tunes, fixes or retires the rule. | Same review and tests as any change. |

Here, routing decides what reaches a person's phone. Each rule file carries a tier: page, queue or record. Page is for tested, promoted, high-severity rules. Queue goes to business-hours triage (see [SO-02](../so-02/)). Record keeps hits for hunting. The model never promotes or demotes a rule. Changing who gets paged is a code review with a named approver.

Detections fail quietly, so test end to end too. Send a synthetic event on a schedule, such as a sign-in from a dedicated test account, and confirm the rule fires in time. A canary that stops firing tells you something broke.

## What stays with people
- **What pages anyone, and when.** The after-hours budget weighs the team's health against risk.
- **Retention and what not to collect.** Longer retention helps investigations and adds privacy exposure. Decide with counsel.
- **Detection priorities.** Which attacks matter most depends on your systems and adversaries.
- **Rule ownership and promotion.** Each rule has a named owner. A person approves every move to paging.
- **Interpreting results.** A query returns rows. A person decides what they mean.
- **Suppressions.** Each exclusion gets an owner and an expiry date.

## Controls and risks
- **Accuracy targets.** Set a shadow-mode precision target per severity: the share of hits worth an analyst's time. Require passing tests for every production rule. Track canary success and parse error rate per source.
- **Audit trail.** Rules, mappings, Logpush jobs and retention settings live in version control, with promotion approvals recorded. Cloudflare's account audit logs independently record configuration changes.
- **Log integrity.** Logs are evidence. Separate write and read credentials, restrict delete permission on the archive, and use retention locks if your storage supports them. No one person can delete logs alone.
- **Failure modes and fallback.** Source goes silent: the health monitor raises it. Push job fails: alert on job errors and destination volume drops. Vendor changes format: mapping tests catch it, and raw events are kept. SIEM down: the R2 archive is intact. Old consoles stay available until the new path proves out.
- **Data handling and access.** Logs contain personal data: IP and email addresses, user agents, sometimes URLs with tokens. Choose fields per Logpush job and drop what you don't need. Put search behind Cloudflare Access with role-based access.
- **Retention requirements.** Laws, regulations, contracts and frameworks can set minimum retention for security logs, and privacy laws can limit how long you keep personal data. If you handle payment card data, PCI DSS has log review and retention requirements.
- **Model and prompt change control.** The AI drafts only. It has no write access to production rules or pipeline configuration, and its drafts get the same review as human work. Prompts are versioned.
- **Untrusted log content.** Summarizing hits means reading attacker-controlled text. Apply the prompt injection controls in [SO-02](../so-02/).

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it
### Map (week 1-2)
- Collect the baseline numbers above.
- Review your last three investigations and note which logs were missing or slow.
- Test one standard question: who signed in, from where, and what did they touch?

### Redesign
- Pick first sources: Cloudflare HTTP requests and firewall events, Cloudflare Access, your identity provider, cloud audit logs, endpoint detection.
- Choose destinations. A common split is R2 as the archive and a SIEM for detection and recent search.
- Write the tier policy and promotion criteria.
- Pick a rule format. Sigma is an open format not tied to one SIEM.
- Set retention per source with counsel.

### Build (two-week sprints)
- **Sprint 1:** Logpush jobs to R2 and your SIEM, as code. Identity provider export. Log Explorer for the Cloudflare datasets you search most, if your account includes it. Old consoles stay in use.
- **Sprint 2:** Health monitor, mappings with tests, first canary events.
- **Sprint 3:** Detection repository, test harness in CI, your ten most important rules migrated with tests, and the shadow tier.
- **Sprint 4:** AI drafting for rules, tests and queries. Shadow summaries and the promotion workflow.

### Run
- Weekly shadow review by rule owners.
- Monthly review with the security engineering lead: pages, precision, source health, coverage gaps.
- Quarterly review of retention and coverage.

### Reference architecture
- **Collection:** Logpush for Cloudflare datasets, to destinations including R2, Amazon S3, HTTP endpoints and several SIEM platforms. Available datasets depend on your Cloudflare products. Workers receive webhooks and, on Cron Triggers, poll APIs; Fly.io runs long backfills; Queues buffer.
- **Storage:** R2 as the archive, organized by source and date. A SIEM for detection and recent search.
- **Search:** Log Explorer stores selected Cloudflare datasets inside Cloudflare and lets you filter or query them with SQL. It covers Cloudflare logs only. The dashboard now shows it under Observability, Logs; check how it is licensed for your account. Use the SIEM, or a query engine that reads object storage, for the rest.
- **Detections:** A repository, a CI test harness and deployment to the SIEM by API.
- **AI drafting:** Workers AI, or another model through AI Gateway.
- **Health and review:** D1 for inventory and rule metadata; review queues behind Access.

**Integration points:** SIEM, identity provider, endpoint detection, cloud audit logs, SaaS admin logs, ticketing, paging, CI.

## How to know it is working
- **Source health:** critical sources within expected volume and freshness, checked daily.
- **Page precision:** actionable pages divided by all pages, per rule.
- **After-hours pages per week,** with the share that needed action.
- **Test coverage:** production rules with passing tests, divided by all production rules.
- **Canary success:** synthetic events detected end to end in the expected time.
- **Time to answer the standard question,** sampled monthly.

Review weekly with rule owners and monthly with the process owner.

## Getting started checklist
- [ ] List every log source with owner, destination and retention.
- [ ] Mark last month's pages actionable or not.
- [ ] Confirm which Cloudflare datasets and Logpush destinations your account supports.
- [ ] Create an R2 archive bucket with restricted delete permission.
- [ ] Push Cloudflare HTTP request, firewall and Access logs to it.
- [ ] Set up the identity provider log export.
- [ ] Create a detection repository with one rule and its tests.
- [ ] Add a shadow tier so new rules don't page on day one.
- [ ] Set up one canary event and the rule that catches it.

## Related playbooks
- [SO-02 · Alert triage for a small team](../so-02/): where queued detections land.
- [SO-01 · Critical vulnerability response](../so-01/): hunting for compromise after an advisory.
- [AG-01 · Agent inventory](../ag-01/): agent tool calls belong here too.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
