# AG-02 · Agent identity and access

> One identity per agent, scoped access, and fast revocation.

**Industry:** Agentic AI governance · **Typical owner:** Head of IT or security engineering lead · **Reading time:** 9 min

## Who this is for

Companies that ran an inventory ([AG-01](../ag-01/)) and found agents on shared API keys, personal OAuth tokens and broad service accounts. IT feels it in access requests built for people. Security feels it when logs can't tell one agent from another. If stopping one agent today means rotating a shared key and waiting to see what else breaks, this playbook fits.

## How it runs today

1. A team wants an agent. A developer creates a model API key in a shared or personal account and pastes it into an environment file or automation platform.
2. The agent needs tools. The developer connects them with their own OAuth login or personal access token. The agent can now do everything that person can do.
3. MCP servers get installed from public lists onto laptops or a shared server. Nobody outside the team knows they exist.
4. If an access request is filed, it uses a form built for people. IT can't tell what scope is needed, so it grants a broad service account rather than block the work.
5. Credentials don't expire. One key ends up in three agents and a CI pipeline.
6. The developer changes roles or leaves. The agent breaks, or keeps running on a token nobody owns.
7. Something goes wrong. Logs show one service account or one person's name. To stop one agent, security rotates the shared key and breaks the others.

The hours go into back-and-forth on scopes, emergency rotations, offboarding cleanup and investigations that start with "which agent was this?"

## Measure your own baseline

Hours per week = volume per week × minutes each ÷ 60. Use a recent quarter and divide by 13 for anything that doesn't happen weekly.

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Handle agent access requests and scope questions | | | | |
| Rotate shared keys and fix what breaks | | | | |
| Clean up agent credentials at offboarding | | | | |
| Investigate which agent did something | | | | |
| Revoke an agent during an incident | | | | |
| **Example:** Investigate which agent made a change | Security engineer | 2 | 90 | 3.0 |

To collect the numbers in one week, time last quarter's tickets that mention bots, integrations, service accounts or API keys from open to close, and ask security about recent investigations involving an automated account. Then run a revocation drill: pick one low-risk agent, say "stop this agent everywhere," and time it until every credential is confirmed dead. The drill time, and the count of credentials the inventory missed, are your most important baselines.

## The redesigned process

Five rules shape the design. One identity per agent, never a person's account. Scopes granted per tool, for the stated purpose only. Short-lived credentials where a system supports them, expiring and rotated keys where it doesn't. Every model call through one gateway. Every tool published through one place, behind an access policy.

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Request | Drafts a least-privilege scope from the stated purpose and your tool catalog. Flags asks broader than the purpose needs. | Owner reviews the draft. A named approver signs off. | Read-only bundle from the pre-approved catalog: owner's manager approves. Write, admin, customer data or outbound messages: security approves. |
| 2. Issue identity | None. Code creates the identity once approval is recorded. | Platform admin confirms the identity, owner and expiry are recorded. | Never runs without a recorded approval. |
| 3. Route model calls | Optional scanning of prompts and responses for sensitive data. | Owner sets the agent's spend limit. Security sets the scanning policy. | Over the spend limit: blocked. Sensitive data match: flagged or blocked per policy. |
| 4. Publish tools | Summarizes each new MCP server's tools and flags those that write, delete or send. | Tool owner approves adding the server and picks which tools to expose. | Any tool that writes, deletes or sends: security review first. |
| 5. Rotate credentials | Watches expiry dates and drafts rotation tasks. | Owner confirms each rotation worked. | A credential with no expiry needs an exception, reviewed in [AG-03](../ag-03/). |
| 6. Watch behavior | Reads gateway, portal and access logs daily. Flags new tools, denied calls, spend jumps and unusual hours. Drafts a short summary. | Security analyst decides what needs action. | Tier 1 agents, denials and new write tools: same-day review. The rest: daily summary. |
| 7. Revoke | Pulls every credential tied to the agent ID from the inventory and drafts the checklist. | Security on-call or the owner approves, runs the kill switch and confirms each credential is dead. | Always a person. Target time set in policy and tested by drill. |
| 8. Retire | Spots owner departures in the HR or identity feed. Flags agents idle for 90 days. | Manager reassigns or retires the agent. | No new owner by the deadline: suspend, then retire. |

Routing here is by risk, not model confidence. The AI's scope proposal is a draft that points the approver at whatever looks too broad. Anything that grants or widens access waits for a named person. Changes that narrow access, like removing unused scopes, can be batched and approved in one pass.

## What stays with people

- **Every access grant.** The approver is named in the record.
- **Which actions need a person every time.** Sending email to customers, merging to production, changing payments, deleting data. Write this per agent and enforce it in the tool.
- **Exceptions** when a system can't issue a per-agent identity, each with an expiry date.
- **The kill switch.** In an incident, security decides and the owner is told.
- **Trust decisions:** which MCP servers and tools the company accepts, and what SaaS copilot settings and vendor contracts allow.

## Controls and risks

- **Accuracy targets.** Track how often approvers narrow or reject the AI's scope drafts. Sample the daily log flags weekly for misses and false alarms.
- **Audit trail.** Every model and tool call carries the agent ID. Gateway, Access and portal logs go to storage you control. Requests, approvals, rotations, revocations and drill results link to the inventory record.
- **Failure modes.** If the gateway path or portal fails, agents stop. That is the safer default. Keep a break-glass procedure owned by a named person. During migration, old credentials stay valid only until the agent runs clean on the new path.
- **Prompt injection and excessive agency.** An agent that reads email, tickets or web pages can be steered by text inside them. Least privilege limits what a misled agent can do. Human approval on consequential actions limits the damage. The OWASP Top 10 for LLM Applications lists excessive agency as a risk.
- **Coverage gaps.** SaaS copilots that run on a vendor's models don't pass through your gateway. Govern them through vendor admin settings, your identity provider and the inventory. Where a coding assistant accepts a custom model endpoint, route it through the gateway.
- **Data handling.** Gateway logs can hold prompts with customer data. Restrict access, set retention and use sensitive data scanning where it fits.
- **Change control.** Keep Access policies, portal settings and gateway settings as code where your tooling supports it. A second person reviews every change.
- **Plan limits.** Some features, such as exporting portal logs with Logpush, depend on your Cloudflare plan. Check first.

## How to build it

### Map (week 1-2)
- Pick the three to five highest-risk agents from your inventory.
- With each agent's builder, trace every credential: where it is stored and who else uses it.
- Run the revocation drill on one agent and time it.
- List every system the agents touch and whether it can issue a per-agent identity and short-lived tokens.

### Redesign
- Naming standard: every identity carries the agent ID (for example, `agt-0142-support-triage`).
- Tier-to-control matrix: approver, credential lifetime, actions needing a person and log review for each tier.
- Tool catalog: approved MCP servers and pre-approved scope bundles.
- A kill switch runbook per agent, generated from the inventory.

### Build (two-week sprints)
- **Sprint 1:** model path for one agent: AI Gateway, a Worker in front, an Access service token, agent ID metadata, spend and rate limits.
- **Sprint 2:** that agent's tools behind an MCP Server Portal and Access applications, unneeded tools hidden, downstream access on its own service accounts.
- **Sprint 3:** request and approval flow, expiry alerts, daily log summary and kill switch runbook. Start on the next agents.
- Old credentials stay valid until the agent runs clean on the new path for an agreed period. Then revoke them and confirm nothing else depended on them.

### Run
- Security reviews the daily log summary.
- Monthly review with the process owner: new agents, grants, exceptions, drill results.
- Every grant, rotation and revocation feeds the quarterly review in [AG-03](../ag-03/).

### Reference architecture
- **Identity:** your identity provider for people. One Cloudflare Access service token (a client ID and secret) per agent, and per-agent service accounts or OAuth clients downstream. Service tokens have a set duration, rotate with a grace period for the old secret, and can alert you before they expire. To revoke, delete the token and revoke existing sessions on the applications it used.
- **Model gateway:** Cloudflare AI Gateway with stored provider keys (so agents never hold them), authentication, spend and rate limits, logging and optional sensitive data scanning. An AI Gateway authentication token works across every gateway in the account, so it is not a per-agent identity. Agents call a small Worker behind Access instead. The Worker stamps the agent ID into the request's custom metadata and calls the gateway through its binding. The ID is set by your code, not claimed by the agent, and you can filter logs and set spend limits by it.
- **Tool publishing:** MCP Server Portals publish approved remote MCP servers behind one endpoint. Access policies decide which servers each identity sees, and admins can hide tools or allow only listed ones. A portal doesn't block direct calls to a server's own URL, so each server also gets its own Access application. Move local-only servers to hosted ones first.
- **Private systems:** Tailscale for links to on-premises systems an agent needs.
- **Requests and approvals:** a short form behind Access. Workflows routes each request to the right approver and waits for the decision.
- **Registry:** the D1 inventory from AG-01, extended with grants and expiry dates.
- **Observability:** Logpush sends gateway, Access and portal logs to R2 or your SIEM.

**Integration points:** identity provider, HR system, code host and CI, cloud providers, the SaaS apps agents use, secrets manager, ticketing, SIEM.

## How to know it is working

- **Own identity:** share of agents with their own identity and no personal or shared credentials.
- **Gateway coverage:** model spend through the gateway divided by total spend on provider invoices.
- **Portal coverage:** share of agent tool calls that go through the portal.
- **Time to revoke:** drill result, from decision to every credential confirmed dead.
- **Unused scope:** grants not used in 90 days.
- **Request cycle time:** from request to approved, working access.

Security reviews these weekly, the process owner monthly.

## Getting started checklist

- [ ] Run a revocation drill on a low-risk agent and record the time.
- [ ] Pick one high-risk agent and list every credential it uses.
- [ ] Create an AI Gateway, store your provider keys in it and turn on authentication.
- [ ] Put a Worker in front that tags each call with the agent ID.
- [ ] Issue that agent its own Access service token with an expiry alert.
- [ ] Put one internal MCP server behind Access and publish it through an MCP Server Portal.
- [ ] Write the tier-to-control matrix on one page.
- [ ] Stop issuing personal tokens to agents and write the exception path.

## Related playbooks

- [AG-01 · Agent inventory](../ag-01/): find the agents and credentials this playbook moves onto their own identities.
- [AG-03 · Quarterly agent access review](../ag-03/): review every grant, exception and drill result each quarter.
- [SO-02 · Alert triage for a small team](../so-02/): route flags from agent logs to an analyst who approves the response.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
