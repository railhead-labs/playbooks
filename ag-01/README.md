# AG-01 · Agent inventory

> Find every agent, the tools it calls, and whose credentials it uses.

**Industry:** Agentic AI governance · **Typical owner:** CISO or IT director · **Reading time:** 9 min

## Who this is for

Mid-market companies where AI agents already do real work: coding assistants in your repositories, agents connected to internal systems through MCP servers, copilots inside your SaaS apps, and scripts that call a model API with a key pasted into a config file. Security, IT and risk leaders feel it first, usually when an auditor, a customer questionnaire or an incident asks which agents can reach a given system. If nobody can answer within a day, or the answer is last spring's spreadsheet, this playbook fits.

## How it runs today

1. A question arrives from an auditor, a board member, a customer questionnaire or an incident.
2. Security sends a survey to department heads. Replies trickle in over weeks. Many say "none," because people don't think of a script or a copilot as an agent.
3. IT exports third-party app grants from the identity provider and reads the OAuth consents by hand, guessing which are AI tools.
4. Engineering answers questions about API keys from memory. Keys live in environment files, CI secrets, automation platforms and password vaults. Several agents share one key.
5. Finance pulls AI subscriptions from cards and invoices, which turns up tools nobody mentioned.
6. Someone merges it all into a spreadsheet. The same agent appears under three names. Many rows have no owner. The "whose credentials?" column is mostly blank.
7. The spreadsheet answers the question that started it, then goes stale. The next question starts over.

The hours go into chasing and reconciling: reading raw exports, retyping findings, sending reminders. Whose credentials an agent runs on gets settled by asking around, because the evidence sits in a dozen consoles.

## Measure your own baseline

Fill this in for your last inventory effort. Hours per week = volume per week × minutes each ÷ 60. For work done once a quarter, total the cycle's hours and divide by 13.

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Send and chase team surveys | | | | |
| Read identity provider app grants | | | | |
| Find API keys and where they live | | | | |
| Match AI spend to tools and teams | | | | |
| Merge and dedupe the spreadsheet | | | | |
| Confirm owners and whose credentials | | | | |
| **Example:** Chase owners for survey replies | Security analyst | 20 messages | 10 | 3.3 |

To collect the numbers in one week, have the people who ran the last inventory estimate each step, and pull timestamps from the email or ticket thread. Then time how long it takes to confirm the owner and credential for ten rows of the old spreadsheet. That also gives you a first accuracy number.

Record four facts alongside the hours: agents known, agents with a current owner, agents on a person's credentials or a shared key, and how long the last "which agents can reach X?" question took to answer.

## The redesigned process

Start with a definition. An agent is any software that uses an AI model to decide or draft actions and uses a credential to read data or act in a system. Four types cover most of what you'll find: coding assistants, MCP-connected agents, SaaS copilots and homegrown automations. The inventory then runs continuously. AI reads, matches and drafts. People confirm ownership and make every call that could stop someone's work.

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Collect signals | Pulls identity provider grants and service accounts, AI gateway logs, model provider key lists, secrets manager entries, MCP config files in repositories (for example `.mcp.json`), egress and DNS logs, and AI spend into one format. | Platform owner confirms each source is connected and complete. | A source that stops sending data alerts its owner the same day. |
| 2. Find candidate agents | Classifies each signal as agent, ordinary app or human use. Groups signals that belong to one agent. | Security analyst reviews new candidates. | Exact match on a key ID, OAuth client ID or service account: update the record. New, or matched only by name: review queue. |
| 3. Attribute credentials | Identifies the credential type (shared API key, personal OAuth token, service account, user session) and whose it is. | Analyst confirms every personal credential and every admin or write scope. | Personal credentials and admin scopes always go to a person. |
| 4. Map tools and MCP servers | Lists the tools, APIs and MCP servers each agent calls, with scopes granted and scopes used. | Analyst confirms for high-risk agents. | Seen in logs: "observed." Only in a config file: "configured, not observed." |
| 5. Confirm the owner | Suggests an owner from the evidence (who created the key, consented to the grant or owns the repository) and sends a confirmation request. | Named owner confirms purpose, data touched and whether the agent is still needed. | No answer by your deadline (for example, five business days): escalate to the department head. Still unclaimed: the security lead decides whether to suspend. |
| 6. Propose a risk tier | Applies your tier rules: write access, customer data, money movement, outbound messages, admin scopes, personal credentials. | Security lead approves Tier 1 and Tier 2. | Tier 3 (read-only, internal data, own identity) is accepted by rule and sampled monthly. |
| 7. Keep it current | Compares each week's signals with the inventory. Flags new agents, tools and scopes, and agents gone quiet. | Owner confirms changes. Security reviews anything that raises the tier. | A tier increase or new personal credential reaches security within one business day. |

Routing here is by strength of evidence, not a model's self-reported score. A key ID seen in both gateway logs and the provider's key list is a fact. An agent inferred from an app name in a grant export is a guess. Facts update the record. Guesses go to the review queue with the evidence attached. Track how often reviewers overturn the AI's calls, and tighten the rules if that rate rises. AI never suspends an agent, revokes a key or assigns an owner on its own.

## What stays with people

- **Edge cases.** Is a spreadsheet macro that calls a model an agent? Your definition, your call.
- **Ownership.** A named person answers for each agent's purpose and access. AI suggests. Only the person can accept.
- **Suspending an agent.** It can stop a team's work, so the security lead decides and the owner's manager is told.
- **Risk tiers** for anything that writes data, moves money, touches customer data or holds admin scopes.
- **Talking to teams.** People disclose shadow agents when they trust the inventory isn't a punishment. Run it as an amnesty first: register now, fix credentials later.
- **SaaS copilot settings and contracts,** which often decide what a copilot can reach and which logs don't show.

## Controls and risks

- **Accuracy target.** Each week, an analyst checks a random sample of automatically updated records against the source systems. Set targets for owner and credential accuracy. Widen automation only while you meet them.
- **Completeness check.** Monthly, confirm each model provider account, AI subscription and gateway key maps to an inventory record. Unmapped spend means unmapped agents.
- **Audit trail.** Every record change stores the evidence, the rule or model version that proposed it, and the person who confirmed it.
- **No secrets in the inventory.** Store key IDs or fingerprints, never secret values. The inventory maps where your credentials live, so restrict and log who reads it.
- **Sensitive data in logs.** Gateway and egress logs can contain prompts and customer data. Keep only the fields you need (agent, destination, credential ID, scope, timestamp) and set retention to policy.
- **Blind spots and fallback.** An agent on a laptop with a personal key and no path through company networks won't appear in logs, so the questionnaire and endpoint checks stay. If a connector breaks or the classifier drifts, the survey and manual grant review still work.
- **Model and prompt change control.** Prompts, rules and model versions are versioned. Each change is tested on a labeled set of past signals before it goes live.

## How to build it

### Map (week 1-2)
- Trace the last inventory request end to end with the people who did it: every source, handoff and delay, with hours for each step.
- Interview the teams most likely to run agents: engineering, support, sales operations, finance, marketing. Ask what they use, what it can reach and whose login it runs on.
- Announce the amnesty and the definition of "agent."

### Redesign
- Write the agent definition and three risk tiers on one page.
- Define the inventory record: agent ID, name, type, owner, purpose, models, tools and MCP servers, credentials (type, whose, scopes, where stored, expiry), data touched, actions, tier, first and last seen, evidence, status.
- Set the routing rules, owner deadline and escalation path. Decide who staffs the review queue.

### Build (two-week sprints)
- **Sprint 1:** connect the three richest sources, usually identity provider grants, model provider key lists, and gateway or egress logs. Seed the store with your existing spreadsheet.
- **Sprint 2:** add classification, grouping and the review queue. Start measuring the overturn rate.
- **Sprint 3:** add owner confirmations, tier proposals and weekly change alerts. Connect the remaining sources.
- The survey and spreadsheet stay in use until the new inventory finds everything they did, and more.

### Run
- Weekly: security reviews new agents, changes and unclaimed records.
- Monthly: review metrics with the process owner and reconcile spend.
- Quarterly: hand the inventory to the access review in [AG-03](../ag-03/).

### Reference architecture
- **Intake:** scheduled Workers (Cron Triggers) pull grants, key lists and spend through each system's API. Logpush delivers AI Gateway and Access logs to R2. Queues buffer signals.
- **Classification:** Workers AI classifies and groups signals, with its own calls logged through AI Gateway.
- **Rules:** tier and routing rules in plain Worker code, reviewed like any other code.
- **Inventory store:** D1 holds records, evidence links and change history.
- **Human review queue:** a small internal app behind Cloudflare Access, on Workers or Vercel.
- **Owner confirmations:** Workflows, a durable workflow engine, sends requests, waits days for answers, reminds and escalates.
- **Observability:** connector health, queue age, overturn rate and audit results on one page.

**Integration points:** identity provider, code host, CI, secrets manager, model provider consoles, SaaS admin consoles, automation platforms, expense system, endpoint management, ticketing, SIEM.

## How to know it is working

- **Owner coverage:** share of agents with a confirmed, current owner.
- **Credential hygiene:** share of agents on a personal credential or shared key. Once [AG-02](../ag-02/) is in place, this should fall every month.
- **Time to inventory:** time from an agent's first signal to a confirmed record.
- **Unmapped spend:** AI spend that doesn't tie to an inventoried agent.
- **Sampled accuracy:** share of sampled records that match the source systems.
- **Stale records:** agents marked active with no activity in 90 days.

Security reviews these weekly. The process owner reviews them monthly.

## Getting started checklist

- [ ] Name the process owner and the review queue staff.
- [ ] Write a one-page definition of "agent" and three risk tiers.
- [ ] Export third-party app grants and service accounts from your identity provider.
- [ ] Pull the API key list from each model provider console.
- [ ] Search your repositories for model API keys and MCP configuration files.
- [ ] Pull 30 days of egress or DNS logs for model provider and MCP endpoints.
- [ ] Announce the amnesty and send a short questionnaire to team leads.
- [ ] Time how long it takes to answer "which agents can reach our customer data?"

## Related playbooks

- [AG-02 · Agent identity and access](../ag-02/): give each agent you found its own identity, scoped access and a fast off switch.
- [AG-03 · Quarterly agent access review](../ag-03/): turn the inventory into a review your risk committee can sign off in one sitting.
- [SO-03 · Log pipeline and detections](../so-03/): get the gateway, identity and egress logs this inventory depends on into one place.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
