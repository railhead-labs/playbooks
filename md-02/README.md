# MD-02 · Quoting

> Quotes built from specs, price rules, and past jobs in hours instead of days.

**Industry:** Manufacturing and distribution · **Typical owner:** Estimating or sales operations manager · **Reading time:** 8 min

## Who this is for

Manufacturers that quote made-to-order or engineered work, such as fabricators and machine shops, and distributors that answer large bids. The pain sits with estimators and inside sales. This playbook fits if requests for quote pile up, a few senior estimators are the bottleneck, and similar parts get quoted at different prices.

## How it runs today

1. **Request intake.** A request for quote (RFQ) arrives by email, portal or a sales rep, with drawings, spec sheets, quantities and a due date. Someone logs it in a spreadsheet or the CRM.
2. **Reading the package.** An estimator reads every page and pulls out materials, dimensions, finishes, tolerances, certifications and delivery dates. Missing drawings or unclear revisions go back to the customer, and the request waits.
3. **Finding past jobs.** The estimator searches the ERP, shared drives and old quote files for similar work, or asks whoever has been there longest.
4. **Building the cost.** The estimator works out material, routing, labor, tooling, outside processing and freight. Fresh supplier prices are often needed, so the estimate waits again.
5. **Setting the price.** Sales applies markup, quantity breaks, customer agreements and a margin floor. Discounts below the floor wait for a sales manager.
6. **Writing the quote.** Someone writes the quote with terms, assumptions, exclusions and a lead time, often after checking capacity with operations.
7. **Follow-up and conversion.** Sales follows up. If the job is won, someone retypes the quote into a sales order.

Most hours go to reading packages, searching for past jobs, waiting on prices and approvals, and retyping. The real judgment, whether you can make the part well and what price wins at an acceptable margin, takes a small share.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Request intake | | | | |
| Reading the package | | | | |
| Finding past jobs | | | | |
| Building the cost | | | | |
| Setting the price | | | | |
| Writing the quote | | | | |
| Follow-up and conversion | | | | |
| **Example (illustrative values only):** Reading the package | Estimators | 40 RFQs | 45 | 30 |

Hours per week = volume × minutes each ÷ 60. In the example, 40 × 45 ÷ 60 = 30. Multiply by a loaded hourly cost for the cost of each step.

Collect the numbers in one week:

- **Pull timestamps.** Your CRM, quote log or sent mail shows when each recent RFQ arrived and when the quote went out. The gap is your turnaround time.
- **Sample the work.** Follow a handful of new RFQs, simple and complex, and time each step, including waits.
- **Ask the estimators.** Ask which requests take longest, where they look for past jobs, and which price rules live only in their heads or personal spreadsheets.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Request intake | Reads the email and attachments, logs the RFQ, and checks the package is complete. | Inside sales confirms new customers and sends questions to the customer. | Complete packages from known customers go to the estimating queue. Gaps produce a drafted question for a person to send. |
| Reading the package | Builds a structured spec sheet from text and notes: materials, finishes, dimensions, tolerances, quantities and special processes. Links each value to its page. | The estimator checks the spec sheet against the drawing, starting with flagged values. | Values from clear text prefill. Anything read from a drawing image, any special process, and any critical tolerance is always flagged. |
| Finding past jobs | Finds similar past jobs by material, process, description and customer. Shows what was quoted, what it cost, and whether you won. | The estimator picks the right reference job, or none. | Top matches appear with reasons. A past price is never reused automatically. |
| Building the cost | Drafts routing, labor and material from the reference job and current costs. Flags stale prices and drafts supplier requests. | The estimator adjusts hours, routing and risk. A buyer confirms supplier prices. | Repeat parts with a current costed routing get a full draft. New parts get every changed operation flagged. Stale or missing costs block the quote. |
| Setting the price | Applies your price rules and writes a short note explaining the price. | Sales sets the final price. A sales manager approves prices below the floor, non-standard terms, and quotes above your dollar threshold. | Prices inside the rules go to the estimator for a final look. Everything else routes to the named approver. |
| Writing the quote | Drafts the quote with terms, assumptions, exclusions and a lead time from current capacity and stock. | The estimator or sales rep reviews and sends it. Operations confirms rush or large-job lead times. | Nothing reaches a customer unless a person sends it. Shorter-than-standard lead times need operations sign-off. |
| Follow-up and conversion | Drafts follow-ups. Drafts the sales order from a won quote and asks for a win or loss reason. | Sales follows up and records the reason. | Won quotes become draft orders under the order entry rules in [MD-01](../md-01/). |

Here, confidence depends on the inputs and the reference job as much as on the model. A repeat part with a recent costed job and current prices is the fast path: the estimator reviews a complete draft. New parts, materials and customers take the full estimator path, but still start from a spec sheet and the closest past jobs, not a blank page.

A quote commits you to a price and a date. The route rules decide how much of the draft a person checks, never whether a person sends it.

## What stays with people

- **Manufacturability and risk.** Whether you can make the part well, with what tooling and scrap, is the estimator's call.
- **Price strategy.** Whether to chase a job, sharpen a price or walk away is a sales call.
- **Discounts and non-standard terms.** Prices below the floor and changes to payment terms, warranties or liability go to a named approver.
- **Lead time commitments.** Operations owns capacity.
- **Supplier commitments.** Buyers confirm material and outside processing prices.
- **Customer conversations.** Questions, negotiation and follow-up stay with the people who own the relationship.

## Controls and risks

- **Accuracy targets.** Compare drafted spec sheets and costs with what estimators approved. After jobs ship, compare quoted with actual cost to catch margin leaks.
- **Audit trail.** Keep every quote version with its sources, extracted values, reference jobs, price rules, model and prompt version, and approvals.
- **Failure modes.** Watch for mixed inches and millimeters, the wrong drawing revision, stale material prices, and past jobs that look similar but aren't. Any estimator can quote the old way at any time, and drafting can be switched off per product family.
- **Price rule ownership.** Pricing leadership owns the rules. Store them as versioned configuration, not inside a prompt, and approve every change.
- **Data handling and access.** Customer drawings are confidential and often under nondisclosure agreements. Keep them in storage you control, limit access by team, and confirm your model provider does not train on your data. Some drawings are export-controlled technical data, for example under ITAR or the EAR. Decide with counsel where that data may be stored and processed, and keep it out of the automated path until you have.
- **Model and prompt change control.** Version prompts, models and thresholds. Test each change against past RFQs with known answers, and record who approved it.

## How to build it

### Map (week 1-2)

- Trace recent quotes, won and lost, with estimators and inside sales. Fill in the baseline worksheet.
- Pull your quote archive: past quotes, the jobs that followed, routings and actual costs. Cleaning this data can be the largest single task.
- Write down the price rules people actually use.

### Redesign

- Start with one product family that has many repeat or similar parts.
- Turn the price rules into a table pricing leadership signs.
- Define what estimators must check and what needs a sales manager or operations. Name an owner for each queue and approval.

### Build (two-week sprints)

- **Sprint 1:** intake and spec extraction in shadow mode. Estimators quote the old way and compare spec sheets.
- **Sprint 2:** past job search over the cleaned archive.
- **Sprint 3:** cost and price drafts, with price rules as versioned configuration.
- **Sprint 4:** quote drafts and conversion of won quotes to draft orders.
- A product family moves to the new path only when its drafts meet the accuracy target.

### Run

- Report weekly on turnaround, draft accuracy and estimator changes.
- Review quoted versus actual cost and price rule changes monthly with the process owner.
- Re-run the test set after any model, prompt or rule change.

### Reference architecture

- **Intake:** an RFQ address routed to a Worker (Cloudflare Email Routing) and an upload portal on Vercel. Packages land in R2. Queues buffer the work.
- **Extraction:** Workers AI or another model provider, through AI Gateway for logging and model switching.
- **Past job search:** a vector index (Cloudflare Vectorize) over past quote and job descriptions, with filters such as material and customer in D1.
- **Rules and orchestration:** Workflows move each RFQ through drafts and approvals, including waits for supplier prices.
- **Human review queue:** an estimator workbench behind Cloudflare Access.
- **System-of-record write-back:** a Worker that writes quotes and draft orders to the ERP, over Tailscale for on-premises systems.
- **Observability:** AI Gateway logs plus Logpush or Log Explorer.

**Integration points:** ERP · CRM · drawing store or product data management system · supplier email and portals · scheduling or MRP · configure-price-quote tool, if any.

## How to know it is working

- **Quote turnaround time:** RFQ received to quote sent, median and slowest tenth.
- **Draft acceptance rate:** the share of drafted spec and cost lines estimators keep unchanged. Its inverse is your rework rate.
- **Extraction accuracy on a sampled audit:** the share of spec values a reviewer confirms are correct.
- **Quotes per estimator per week.**
- **Hit rate:** quotes won divided by quotes sent, by product family. Price and market move it too.
- **Margin variance:** quoted margin compared with actual margin on completed jobs.

Review turnaround and accuracy weekly, and all six monthly with the process owner.

## Getting started checklist

- [ ] Name the process owner and two estimators who know the exceptions.
- [ ] Fill in the baseline worksheet and measure recent turnaround.
- [ ] Check how many past jobs have actual costs attached.
- [ ] Write down your price rules and get them signed.
- [ ] List who approves discounts, terms and lead times today.
- [ ] Ask counsel whether any customer drawings are export-controlled.
- [ ] Pick the first product family.

## Related playbooks

- [MD-01 · Order-to-cash](../md-01/): won quotes become orders, and clean quote records settle pricing exceptions.
- [MD-03 · Inventory and demand planning](../md-03/): open quotes are an early demand signal.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
