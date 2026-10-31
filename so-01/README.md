# SO-01 · Critical vulnerability response

> From advisory to an edge rule in hours, then the real fix with owners.

**Industry:** Security operations · **Typical owner:** Security lead · **Reading time:** 8 min

## Who this is for
Mid-market companies with a security team of a handful of people and no 24/7 SOC, running more internet-facing systems than the inventory knows about. This fits if every critical advisory starts a scramble in chat, if you can't say "are we affected?" within hours, or if fixes stall because nobody knows who owns the system.

## How it runs today
1. An advisory arrives by vendor email, news story, chat link, scanner finding or customer question. There is no single intake.
2. Someone reads the advisory and decides whether it matters.
3. The exposure check is a question in the engineering channel: "Is anyone running this?" The inventory spreadsheet is months old.
4. The team waits. Some owners reply. Versions are guessed.
5. If someone knows the WAF well, they write an edge rule by hand. Often the edge rule is skipped.
6. Fix tickets go out unranked and sit in backlogs next to routine work.
7. Leadership asks "are we safe?" The security lead builds the answer by hand.
8. Closure is informal. Nobody confirms the fix, and temporary rules stay for years.

The hours go to re-reading advisories, rebuilding the affected-systems list from scratch, chasing owners and writing updates. The edge rule, which could cut risk within hours, waits behind the inventory question.

## Measure your own baseline
Critical advisories come in bursts, so spend one week reaching back. Pull your last three to five from chat and tickets. Record when each was published, first seen, mitigated and verified fixed. Ask the people involved for minutes per step.

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Reading advisories and deciding relevance | | | | |
| Finding affected systems | | | | |
| Chasing owners for versions and status | | | | |
| Writing and testing edge rules | | | | |
| Creating and ranking fix tickets | | | | |
| Status updates and close-out | | | | |
| **Example** (illustrative values): Finding affected systems | Security lead and three app owners | 2 advisories | 180 | 6.0 |

Hours per week is volume times minutes, divided by 60. In the example, 2 × 180 / 60 = 6.0.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Intake | Pulls advisories from your feeds (the [CISA Known Exploited Vulnerabilities catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog), the [National Vulnerability Database](https://nvd.nist.gov/), vendor advisories). Removes duplicates by CVE. Summarizes affected versions, attack vector, exploitation status and fix, with the source linked. | The on-duty analyst reads summaries each morning and whenever a page fires. | In your inventory and reported exploited (KEV listing or vendor statement): page on-call. In your inventory only: same-day queue. No match: weekly digest. |
| 2. Exposure check | Matches affected versions against your inventory, DNS records, Cloudflare hostnames, scanner results and dependency manifests. Marks each system internet-facing or internal and cites the evidence. | The analyst confirms the list with system owners and orders direct checks where versions are unknown. | Direct evidence (scanner banner, manifest): "confirmed." Product name only: "probable." No evidence either way: "unknown," treated as affected if internet-facing. |
| 3. Edge mitigation | Checks whether a Cloudflare managed rule already covers the CVE. Drafts a WAF custom rule matching the exploit pattern in the advisory, with benign and malicious test requests. | A security engineer reviews the rule and deploys it in log mode. After reviewing what it matched, a named approver switches it to block. | Nothing goes to block without the named approver. If legitimate traffic matches, the rule is revised first. |
| 4. Ranked fix list | Ranks affected systems: internet-facing first, then known exploitation, [EPSS](https://www.first.org/epss/) score, business criticality and edge coverage. Drafts one ticket per system with the vendor's fix steps and the owner. | The security lead approves ranking and due dates. Owners accept their tickets. | A system with no owner goes to the lead. The AI never guesses an owner. |
| 5. Fix and verify | Tracks tickets, re-runs version checks and drafts status updates. | Owners patch, upgrade or apply the workaround. The analyst confirms the evidence. | No evidence, no closure. Overdue tickets escalate. |
| 6. Compromise check | Drafts hunt queries for the advisory's indicators over the window before mitigation. Summarizes hits. | The analyst reviews results and decides whether this is an incident. | Any credible hit goes to your incident process with a named incident lead. |
| 7. Close-out | Drafts the record: timeline, systems, decisions, and every temporary rule with a review date. | The lead signs off. The engineer removes or renews each temporary rule on its date. | A temporary rule with no review date blocks closure. |

Confidence here means strength of evidence, not how sure the model sounds. The AI can mark a system "confirmed" only with evidence it can cite, and it never marks a system "not affected" on its own. An internet-facing system of unknown status counts as affected until a person shows otherwise.

On Cloudflare, deploy the custom rule with the Log action first. At the time of writing, that action is available only on Enterprise plans. On other plans, build the same filter in Security Analytics and review which recent requests match. Set the log window in policy ahead of time, and let the approver shorten it when exploitation is active. An edge rule buys time. It is not the fix, and attackers often find ways around a pattern match.

## What stays with people
- **Relevance when evidence is thin.** It takes knowledge of how your systems are really built.
- **Approving every blocking rule.** A bad rule blocks customers. The approver owns that trade-off.
- **Emergency changes to revenue systems.** Patching an order system mid-day is a call for its business owner.
- **Risk acceptance.** When no fix exists, the business owner signs a documented acceptance with an expiry date.
- **Vendor and owner conversations.** Pushing a vendor for a fix date is a relationship.
- **Declaring an incident.** Whether a hunt hit means compromise, and who gets told, stays with the incident lead and counsel.

## Controls and risks
- **Accuracy targets.** After each critical advisory, compare the AI's exposure list with everything owners and scans eventually found. The target for internet-facing systems is zero misses. Log each miss and its cause. The analyst marks each summary right or wrong on affected versions.
- **Audit trail.** Record each exposure decision with its evidence, and each rule change: who drafted it, who deployed it in log mode, who approved block, and when. Cloudflare's account audit logs independently record configuration changes.
- **Failure modes and fallback.** Feed stops updating: alert on freshness gaps. Versions misread: the analyst checks the linked vendor text. Rule blocks legitimate traffic: one-step rollback. System down: the old path (chat, spreadsheet, manual WAF change) stays documented and usable.
- **Untrusted input.** Advisory text is outside content. The AI only drafts, rule expressions are syntax-checked, and the model holds no credential that can change the WAF. See [SO-02](../so-02/) for prompt injection controls.
- **Data handling and access.** Your exposure list maps what is vulnerable. Keep it behind Cloudflare Access and don't send inventory data to a model provider without an agreement that covers it.
- **Model and prompt change control.** Prompts, rule templates and routing rules live in version control. Re-run a test set of past advisories before any change ships.
- **Notification obligations.** If the compromise check finds exploitation, obligations may follow under state breach notification laws, customer contracts, sector regulators or, for public companies, SEC rules on disclosing material cybersecurity incidents. Bring counsel in early. <!-- VERIFY: confirm which breach notification laws, contract terms, sector rules and SEC disclosure requirements apply to the reader's company; no deadlines are stated here on purpose. -->

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it
### Map (week 1-2)
- Reconstruct the timeline of your last three to five critical advisories.
- List every place asset data lives: inventory, cloud accounts, DNS, Cloudflare zones, scanners, code repositories.
- List who can change the WAF today and how changes are approved.
- Define "critical" for you, for example: actively exploited and present on an internet-facing system.

### Redesign
- Write the route rules as policy: who is on duty, who approves block, the log window, due dates by rank, escalation.
- Define the evidence levels and what counts as direct evidence.
- Name emergency rules with the CVE ID, owner and review date in the rule description.
- Decide which model drafts and what data it may see.

### Build (two-week sprints)
- **Sprint 1:** Intake, deduplication and summaries. Analysts keep reading advisories directly and compare.
- **Sprint 2:** Exposure matching with evidence levels, tested against past advisories.
- **Sprint 3:** Rule drafting, syntax checks, log-mode deployment, block approval and rollback.
- **Sprint 4:** Ranked fix list, tickets and verification. Run a tabletop on a past advisory before go-live.

### Run
- After each critical advisory: review misses, time to mitigation and rule false positives.
- Monthly with the security lead: overdue fixes, expired temporary rules, inventory gaps.

### Reference architecture
- **Intake:** Workers on Cron Triggers fetch feeds; Queues buffer.
- **Drafting:** Workers AI, or another model through AI Gateway for request logs and rate limits.
- **Process state:** Workflows run the durable steps and pause for approvals; D1 holds decisions; R2 holds evidence.
- **Edge mitigation:** WAF custom rules and managed rulesets, changed through a scoped API token held by the deployment service, not the model.
- **Human review:** An approval console behind Access, with chat notifications.
- **Observability:** Logpush of firewall events to your SIEM or R2. See [SO-03](../so-03/).

**Integration points:** asset inventory or CMDB, cloud provider accounts, attack surface and vulnerability scanners, code repositories, ticketing, chat, paging.

## How to know it is working
- **Time to exposure answer:** first seen to a confirmed list of affected internet-facing systems.
- **Time to edge mitigation:** first seen to a block-mode rule or confirmed managed rule.
- **Time to fix by rank:** median and worst case for top-ranked systems.
- **Exposure recall on a sampled audit:** affected systems the AI listed, divided by all affected systems eventually found.
- **Emergency rule false positives:** legitimate requests blocked, from log review and support tickets.
- **Temporary rule hygiene:** emergency rules past their review date.

Review after every critical advisory and monthly with the process owner.

## Getting started checklist
- [ ] List your advisory sources and pick one intake channel.
- [ ] Subscribe to the CISA KEV catalog and your top vendors' advisories.
- [ ] Reconcile internet-facing hostnames from DNS and Cloudflare with your inventory.
- [ ] Name an owner for every internet-facing system.
- [ ] Confirm which WAF actions your Cloudflare plan supports, including Log.
- [ ] Confirm the managed ruleset on your plan is deployed.
- [ ] Write the block approval policy: approver, log window, rollback.
- [ ] Agree on fix due dates by rank and an escalation path with engineering leadership.

## Related playbooks
- [SO-02 · Alert triage for a small team](../so-02/): handle the alerts that follow, with an analyst approving each response.
- [SO-03 · Log pipeline and detections](../so-03/): firewall events and hunt queries in one place.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
