# RT-04 · Customer service

> Routine questions answered with order context. Hard cases go to a person.

**Industry:** Retail · **Typical owner:** Director of customer care · **Reading time:** 9 min

## Who this is for

Retailers and brands with a customer care team handling email, chat and messaging, where peak season multiplies contacts faster than you can hire. Agents feel the pain, and so do customers waiting in the queue. This playbook fits if most contacts are "where is my order," return status and policy questions, agents switch between the help desk, order system and carrier sites for every ticket, seasonal staff take weeks to learn policy, and customers repeat themselves at every handoff.

## How it runs today

1. Customers write in by email, chat, social messages and web forms, or call. Contacts land in the help desk, often in separate queues.
2. Tickets wait in order of arrival, not urgency. A customer with a damaged gift waits behind a store hours question.
3. An agent reads the message, finds the customer and order, and opens the order system, carrier tracking and returns system.
4. The agent finds the answer in a policy document or saved reply, edits it and sends it.
5. Some requests need another team: refunds over a limit, replacements, address changes, damaged goods. The ticket waits.
6. Escalations go to a supervisor with a short note. The supervisor reads the whole thread again.
7. A basic FAQ bot, if you have one, can't see orders, so customers ask for a person anyway.

Where the hours go: looking up orders, copying tracking numbers, rewriting the same answers and re-reading threads at each handoff. Hard cases get the same queue position as easy ones.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Triage and routing | | | | |
| Order status questions | | | | |
| Return and refund questions | | | | |
| Product questions | | | | |
| Order changes and cancellations | | | | |
| Complaints and escalations | | | | |
| After-contact notes | | | | |
| **Example** (illustrative values only): Order status questions | Care agent | 900 | 4 | 60 |

Hours per week is volume times minutes, divided by 60.

Collect the numbers in one week. Export that week's tickets with channel, tags, handle time and timestamps. Help desk tags are often wrong, so have agents re-tag a random sample by the real reason. Measure time to first response, time to resolution, reopen rate and transfers per ticket. Ask agents which lookups take longest.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Intake and triage | Reads each message. Identifies the customer and order, the intent and the urgency. Checks for hard-case signals. | Supervisor watches the queues and owns the routing rules. | Routine intent: assistant. Any hard-case signal: person, at the front of the queue. |
| Identity check | Matches the customer to the order using your verification rules before sharing any order details. | Agent handles failed or suspicious verification. | Verified: continue. Not verified: share nothing about the order and offer a person. |
| Routine answers | Answers order status, delivery, return status, policy and product questions from live order data, carrier tracking and approved help content. Records which sources it used. | Team lead reviews a sample of conversations every day. | Answer grounded in order data or approved content: send. No source: don't guess, hand off. |
| Simple actions | Takes actions within set limits, such as issuing an in-policy return label or resending a confirmation. | Agent approves anything outside the limits. | Within limits: done. Refunds over the threshold, address changes after shipping, cancellations after fulfillment starts: person. |
| Agent assist | For tickets with a person, pulls order facts and drafts the reply. | Agent edits, approves and sends. | On handed-off tickets, a person always sends. |
| Handoff | Writes a summary: who the customer is, the order, what they asked, what was already tried, what they want and a suggested next step. Tells the customer a person is taking over and when to expect a reply. | Agent picks up from the summary and does not ask the customer to repeat anything. | A request for a person is honored at once, at any point in the conversation. |
| Wrap-up | Tags the contact, writes the after-contact note and flags gaps in help content. | Team lead reviews content gaps weekly. | Automatic. |

Hard cases always go to a person:

- The customer asks for a person, in any words.
- Complaints, strong frustration or repeat contacts on the same issue.
- Injury, safety hazards or recalls.
- Legal threats, chargebacks, or mentions of a regulator or attorney general.
- Refunds over the threshold and anything with fraud signals. See [RT-01 Returns](../rt-01/).
- Account changes that could signal a takeover: email, password or shipping address changes on an open order.
- A customer who mentions a disability, an accommodation need, a bereavement or another hard situation.
- Anything the assistant can't ground in order data or approved content.

Two checks run on every turn. The first asks whether the assistant is allowed to handle this. That is a rule, not a guess. The second asks whether the answer is grounded. The assistant answers only from order data, tracking and approved help content. If it can't find a source, it says so and hands off. It never invents a delivery date, a policy or a promise.

The way to a person is always open. Every chat shows a "talk to a person" option on every turn. Every automated email tells the customer how to reach a person. Outside staffed hours, the assistant says when a person will reply and opens the ticket with the summary attached. Customers are told they are talking with an automated assistant.

## What stays with people

- **Anyone who asks for a person.** No retention scripts, no loops back to the assistant.
- **Complaints and goodwill.** Apologies, credits and exceptions are relationship decisions.
- **Refunds over the threshold, fraud signals and policy exceptions.** These follow the approvals in [RT-01](../rt-01/).
- **Safety reports and injury claims.** These go to your product safety lead the same day.
- **Account security.** Failed verification and sensitive account changes.
- **Legal, chargeback and regulator contacts.**
- **What the assistant may do.** People set its limits, policies and help content.

## Controls and risks

- **Accuracy targets.** A team lead grades a daily sample of assistant conversations on a rubric: correct answer, correct use of order data, policy followed, tone. Grade agent conversations with the same rubric. Before go-live, agree with the care owner that the assistant must score at or above your agents.
- **Resolution, not deflection.** A contact the assistant closed but the customer reopened, or escalated by another channel, counts as a failure.
- **Handoff quality.** Agents rate each summary as complete, partial or wrong. Track how often customers had to repeat information.
- **Audit trail.** Store each conversation with the data the assistant looked up, actions it took, model and prompt versions and the handoff summary, attached to the ticket.
- **Untrusted input.** Customers can type anything, including attempts to manipulate the assistant. Tools are read-only by default. The assistant sees only the verified customer's orders. The model can request an action, but rules outside the model decide whether it runs.
- **Failure modes and fallback.** Expect wrong answers, outages, stale carrier data and surges. On any failure, contacts route to the existing agent queue with an honest message. The old path stays open.
- **Data handling.** Redact card numbers and other sensitive data before storage and before any model call. Keep transcripts only as long as your retention policy allows. Rules on customer data, including access and deletion requests, vary by state and country.
- **Access.** The assistant runs under its own identity, scoped to the tools it needs. Agents and supervisors sign in through single sign-on.
- **Model and prompt change control.** Help content, policies, prompts and models are versioned. Changes are tested before release against a saved set of past conversations, including hard cases that must hand off.

## How to build it

### Map (week 1-2)
- Sit with agents on each channel during a busy shift. Follow a handful of tickets from first message to close, including escalations.
- List every system an agent opens and every saved reply they use.
- Fill in the baseline worksheet.
- Collect policies and help content. Mark what is out of date.
- Write down how agents verify identity today.

### Redesign
- Choose the first intents: high volume, clear answers, order data available. Order status is the usual start.
- Write the hard-case list and the handoff summary format with your agents.
- Set the action limits and the refund threshold. Name the approvers.
- Decide the verification rules before any order detail is shared.
- Agree on the grading rubric, accuracy targets and daily sample.

### Build (two-week sprints)
- **Sprint 1:** triage and intent tagging on live tickets in shadow mode, compared with agent tags.
- **Sprint 2:** agent assist. Drafted replies with order facts. Agents send everything.
- **Sprint 3:** the assistant answers order status questions in chat for verified customers, with the handoff summary and "talk to a person" from day one. Start with a share of traffic.
- **Sprint 4:** add return status and policy questions, simple actions within limits, and email.
- The existing queues stay staffed. Widen each intent only after it meets the target.

### Run
- Daily: conversation sample grading.
- Weekly: content gaps, handoff ratings, reopen rate.
- Monthly with the care owner: accuracy, resolution, satisfaction by path, limits and new intents.

### Reference architecture
- **Intake:** chat widget on your site (Vercel or your current front end). Chat, email and help desk events handled by Cloudflare Workers. WAF and rate limiting in front of public endpoints. Queues absorb email surges.
- **Models:** Workers AI or another model provider, called through AI Gateway for logging, rate limits and fallback.
- **Knowledge:** approved help content and policies indexed for retrieval, with source documents in R2.
- **Tools:** a small set of scoped tools (order lookup, tracking, return label) behind Cloudflare Access. MCP Server Portals can publish them to the assistant through one governed, logged endpoint.
- **Rules:** hard-case list, action limits and verification rules as versioned code in a Worker, separate from the model.
- **Orchestration:** Workflows for multi-step actions that wait on a person.
- **Human review queue:** your existing help desk. Summaries post as internal notes on the ticket.
- **System-of-record write-back:** tags, notes and actions back to the help desk and order system. D1 for conversation metadata, actions and handoffs.
- **Observability:** Logpush and Log Explorer for conversations and actions, AI Gateway analytics for model calls.

**Integration points:**
- Help desk
- E-commerce platform and order management system
- Carrier tracking
- Returns system
- Payment processor (refund status only)
- CRM or loyalty system
- Knowledge base

## How to know it is working

- **Assistant resolution rate:** contacts the assistant resolved with no person and no reopen within a window you set.
- **Accuracy:** rubric score on the daily sample, assistant against agents.
- **Time to a person:** minutes from a handoff request to a person's first reply, during and outside staffed hours.
- **Repeat rate after handoff:** share of handoffs where the customer had to repeat information.
- **Satisfaction by path:** assistant only, assistant then agent, and agent only.
- **Agent handle time:** on handed-off tickets, against the baseline.

Review daily samples with team leads, weekly with supervisors and monthly with the care owner.

## Getting started checklist

- [ ] Name the care owner and the approvers for refunds, goodwill and safety reports.
- [ ] Fill in the baseline worksheet for one week and re-tag a sample of tickets.
- [ ] Write the hard-case list with your senior agents.
- [ ] Draft the handoff summary format and test it on real escalations.
- [ ] Confirm your identity verification rules.
- [ ] Clean up policies and help content for the first intents.
- [ ] Save a test set of past conversations, including hard cases.
- [ ] Decide where "talk to a person" appears in every channel.

## Related playbooks

- [RT-01 Returns](../rt-01/): refund, repair or resale decisions behind the return questions customers ask.
- [RT-02 Product content](../rt-02/): the approved product facts the assistant answers from.
- [AG-02 Agent identity and access](../ag-02/): one identity per agent, scoped tool access and fast revocation for the assistant.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
