# MD-01 · Order-to-cash

> Orders, invoices, and payments matched as they arrive. People handle only the gaps.

**Industry:** Manufacturing and distribution · **Typical owner:** Controller · **Reading time:** 8 min

## Who this is for

Distributors and manufacturers with $100M to $3B in revenue, thousands of customers, and orders arriving by email, PDF, EDI and phone. Customer service, credit, billing and cash application all feel the pain. This playbook fits if month-end runs late, cash sits unapplied for days, and experienced people spend mornings retyping orders and matching remittances.

## How it runs today

1. **Order entry.** Orders arrive in a shared inbox as emails, PDFs and spreadsheets, alongside EDI and phone. A rep reads each one, looks up customer and part numbers, and keys the lines into the ERP. Unclear lines go back to the customer, and the order waits.
2. **Credit check.** The ERP holds orders over limit or past terms. A credit analyst pulls aging, payment history and call notes, then releases or holds.
3. **Pricing exceptions.** The price on the purchase order doesn't match the ERP. A rep checks contracts, quotes and past orders, then emails sales or pricing and waits for an answer.
4. **Invoice and delivery match.** Billing waits for proof of delivery, compares quantities shipped to quantities ordered, and fixes short ships, substitutions and freight before the invoice goes out.
5. **Cash application.** Payments arrive by check, ACH and wire, with remittance details sent separately in emails, PDFs, portals and bank files. A specialist matches each payment to open invoices, including short pays and deductions.
6. **Collections follow-up.** A collector works the aging report, writes reminders with invoice copies attached, and calls late customers.

Very little of this time goes to decisions. Most goes to reading, retyping and chasing people for answers. The waits between steps are often longer than the work.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Order entry | | | | |
| Credit check | | | | |
| Pricing exceptions | | | | |
| Invoice and delivery match | | | | |
| Cash application | | | | |
| Collections follow-up | | | | |
| **Example (illustrative values only):** Order entry | Customer service reps | 500 orders | 6 | 50 |

Hours per week = volume × minutes each ÷ 60. In the example, 500 × 6 ÷ 60 = 50. Multiply by a loaded hourly cost for the cost of each step.

Collect the numbers in one week:

- **Pull system counts.** Count orders, holds, invoices, payments applied and collection contacts from the ERP and bank reports. Timestamps show how long items wait.
- **Sample the work.** Time a few dozen items per step, including lookups and emails.
- **Ask the people doing it.** Ask where they lose time. Write down every workaround and side spreadsheet.
- **Count second touches.** Items needing a call or a corrected invoice become your review queues.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Order entry | Reads orders from email, PDF and spreadsheets. Matches customer, ship-to and parts to ERP master data. Drafts the order with a score on each line. | Reviews only the lines the system is unsure of. | Lines that match master data and score above the threshold post. Unmatched parts, new ship-to addresses and low-confidence fields go to review beside the source document. |
| Credit check | Clears routine orders against limit, terms and payment history. For holds, summarizes aging, payments, disputes and notes. | The credit team decides every hold. The credit manager approves releases over the set limit. | Orders within limit and terms, with no past-due balance beyond your rule, release automatically. Everything else goes to the credit queue. |
| Pricing exceptions | Compares the order price to contracts, open quotes and past orders, and explains the gap. | Pricing or sales approves each exception in one click. | Gaps explained by a valid contract or open quote are corrected and logged. All others go to a person. Key accounts always route to the named account owner. |
| Invoice and delivery match | Matches invoices to proof of delivery as it arrives. Flags short ships, substitutions and freight differences. | Billing resolves real gaps and approves credit memos. | Exact matches release the invoice. Any difference goes to billing. Credit memos above your threshold need a named approver. |
| Cash application | Reads remittances from email, portals and bank files. Proposes the invoice match for each payment, including short pays. | Cash application works unmatched payments and deductions. | Payments that match exactly, with a clear remittance, post. Partial matches, unidentified payments and deductions go to a person. |
| Collections follow-up | Drafts reminders with the right invoices and proof of delivery attached. Summarizes account history before each call. | Collectors send reminders and make the calls. | Drafts wait for a collector to send. Accounts more than sixty days late, in dispute, or flagged by sales get a call from a person. |

Routing works the same way at every step. The system scores each field and proposed match, then checks it against rules you already trust: master data, contracts, credit limits and open invoices. When the score is high and the rules agree, the item moves on and is logged. Otherwise it goes to a person with the source document, the proposed answer and the reason it was flagged.

Set thresholds by running the system on last month's orders and payments and comparing its answers with your team's. Start conservative. Widen what posts automatically only after the sampled audit shows a step is accurate.

## What stays with people

- **Credit holds over a set limit.** A credit call weighs the relationship and your risk appetite. The credit manager approves releases over the limit.
- **Pricing exceptions for key accounts.** Pricing is part of the relationship, so the account owner approves every one.
- **Unmatched payments.** Each may be a deduction, a dispute, a duplicate or an error. Someone who knows the customer works it out.
- **Collections calls to customers more than sixty days late.** These calls protect the relationship and surface disputes nobody logged.
- **Credit memos, write-offs and dispute settlements.** These change revenue and receivables, so a named approver signs off.
- **Master data.** New customers, credit limits, prices and ship-to addresses stay with their owners.

The team still makes every credit call. They just stop typing.

## Controls and risks

- **Accuracy targets.** Set a target per step, such as field accuracy on order lines. Each week a reviewer re-checks a random sample of auto-posted items, plus every corrected item.
- **Audit trail.** For every line, release, match and draft, log the source document, extracted values, score, rule that fired, model and prompt version, and who approved or changed it.
- **Failure modes.** Watch for similar part numbers, misread units of measure and new purchase order layouts. When accuracy drops or an input fails, route the whole step to review. The old path stays open during Build, and any step can switch back without a code change.
- **Write-back limits.** The ERP service account is narrowly scoped. It cannot change credit limits, prices or customer master data.
- **Data handling and access.** Keep data in accounts you control. Limit review tools to the teams that need them, through single sign-on. Mask bank account numbers. Keep card numbers out of this path; card data carries its own security requirements under PCI DSS.
- **Model and prompt change control.** Version prompts, thresholds and models like code. Test each change against past orders and payments, and record who approved it.

## How to build it

### Map (week 1-2)

- Sit with each team and trace real orders from arrival to cash applied. Fill in the baseline worksheet.
- Pull a test set: a few hundred recent orders across channels, a month of remittances, and their ERP records.
- List the exceptions people handle from memory. The design has to keep them.

### Redesign

- Pick the first step by your baseline numbers, not by habit.
- Write the routing rules and name an owner for every queue and approval.
- Agree on accuracy targets and the audit method before anything is built.

### Build (two-week sprints)

- **Sprint 1:** intake and extraction for one channel, such as emailed PDFs, in shadow mode. People still key orders, and you compare results daily.
- **Sprint 2:** the review queue and ERP write-back for high-confidence lines, behind a switch per customer or channel.
- **Later sprints:** credit summaries, pricing comparison, delivery match, cash application and collection drafts, one at a time.
- Keep the old path open until each step meets its target on live work.

### Run

- Publish a weekly accuracy and quality report per step.
- Hold a monthly review with the process owner to adjust thresholds and rules.
- Re-run the test set after any model, prompt or threshold change.

### Reference architecture

- **Intake:** an inbound address routed to a Worker (Cloudflare Email Routing), plus EDI and bank files in R2. Queues buffer the work.
- **Extraction:** Workers AI or another model provider, through AI Gateway for logging and model switching.
- **Rules and orchestration:** Workflows carry each order and payment through extraction, checks, routing and the wait for approval.
- **Human review queue:** a review app behind Cloudflare Access, with the source document beside the proposed values.
- **System-of-record write-back:** a Worker that posts to the ERP API, reaching on-premises systems over Tailscale.
- **State and documents:** D1 for routing state and audit records, R2 for documents.
- **Observability:** Logpush or Log Explorer, with reports built from the audit records.

**Integration points:** ERP · EDI provider · bank and lockbox files · warehouse and carrier proof-of-delivery feeds · remittance portals · CRM · shared inboxes.

## How to know it is working

- **Straight-through rate:** the share of order lines, invoices and payments that post untouched, by step and channel.
- **Exception rate and age:** items in each review queue and how long they wait.
- **Accuracy on a sampled audit:** the share of auto-posted items a reviewer confirms are correct.
- **Cycle time:** order received to entered, shipment to invoice, payment received to applied.
- **Unapplied cash:** dollars received but not applied, and how long they have waited.
- **Days sales outstanding:** receivables divided by credit sales for the period, times days in the period.

Review accuracy weekly during Build, and all six monthly with the process owner.

## Getting started checklist

- [ ] Name the process owner and one person from each team.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Pull recent orders and a month of remittances with their ERP records.
- [ ] List every exception people handle from memory.
- [ ] Write down your credit release rules and who can release what.
- [ ] Set accuracy targets and the audit method.
- [ ] Confirm how you can write to your ERP: API, import file or integration tool.

## Related playbooks

- [MD-02 · Quoting](../md-02/): won quotes become orders and settle many pricing exceptions.
- [MD-03 · Inventory and demand planning](../md-03/): clean order data is the starting point for a better forecast.
- [FS-04 · Reconciliation](../fs-04/): breaks found and explained across ledgers, the same pattern as cash application.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
