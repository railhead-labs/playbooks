# MD-03 · Inventory and demand planning

> Forecasts that pull from orders and suppliers without a weekly spreadsheet.

**Industry:** Manufacturing and distribution · **Typical owner:** Supply chain or materials planning manager · **Reading time:** 8 min

## Who this is for

Manufacturers and distributors with thousands of stocked items and a planning team that rebuilds the plan by hand every week. Planners and buyers feel the pain first. This playbook fits if the forecast lives in a spreadsheet exported from the ERP, you run short on some items while others pile up, and supplier delays reach planners late, by email.

## How it runs today

1. **Export.** Each week a planner exports sales history, open orders, inventory and open purchase orders from the ERP into a spreadsheet.
2. **Clean.** The planner removes one-time orders, fixes units of measure and merges superseded part numbers. The same fixes repeat every week.
3. **Forecast.** The planner runs moving averages or the ERP's built-in forecast, then adjusts items by hand for seasonality, known projects and gut feel.
4. **Gather demand signals.** Planners email and call sales reps about large deals. Customer forecasts and release schedules arrive as spreadsheets, PDFs or EDI, and someone types the important ones in.
5. **Gather supplier signals.** Buyers chase order acknowledgments, ship dates and delay notices by email. Lead times in the ERP drift away from what suppliers actually deliver.
6. **Plan replenishment.** The planner sets reorder points and safety stock, reviews suggested buys, and buyers place purchase orders.
7. **Expedite.** Shortages surface late, so buyers expedite. Excess stock gets reviewed only now and then.

The hours go to cleaning the same data every week, chasing sales and suppliers for input, and retyping what they send. Little time is left for the items where a planner's judgment changes the result.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Export | | | | |
| Clean | | | | |
| Forecast | | | | |
| Gather demand signals | | | | |
| Gather supplier signals | | | | |
| Plan replenishment | | | | |
| Expedite | | | | |
| **Example (illustrative values only):** Gather supplier signals | Buyers | 150 supplier emails | 8 | 20 |

Hours per week = volume × minutes each ÷ 60. In the example, 150 × 8 ÷ 60 = 20. Multiply by a loaded hourly cost to get the cost of each step.

Collect the numbers in one week:

- **Shadow one planning cycle.** Sit with a planner and a buyer for a full week. Time each step and note every spreadsheet and macro.
- **Count the inputs.** Count supplier date emails, customer forecasts and sales conversations about demand.
- **Pull system data.** Count purchase orders, expedites, stockouts and past-due supplier orders. Compare item master lead times with actual receipt dates.
- **Ask about overrides.** Ask which items planners always adjust, and why. Those reasons often become rules.

## The redesigned process

The forecast comes from statistical methods you can explain and test against history. Language models read the unstructured inputs: supplier emails, customer forecasts and sales notes.

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Data assembly | Pulls sales, orders, inventory and purchase orders nightly. Applies cleaning rules and flags new anomalies. | The planner approves cleaning rules and reviews anomalies. | Approved rules apply and are logged. New anomalies go to the planner. Stale or missing data stops the run. |
| Baseline forecast | Runs several statistical methods per item, tests each against past demand, and keeps the one with the lowest error. Groups items by volume and demand pattern. | The planner reviews results by item group, not item by item. | Steady items with low tested error flow through. New items, erratic demand and items with high tested error go to the planner. |
| Demand signals | Reads customer forecasts, release schedules, sales notes and open quotes. Proposes forecast adjustments, each linked to its source. | The planner accepts or rejects each adjustment. Sales confirms large deals. | Adjustments appear as proposals. Any adjustment above your size threshold needs planner approval before it changes the plan. |
| Supplier signals | Reads acknowledgments, ship notices and delay emails. Updates expected dates and compares actual lead times with the item master. | The buyer handles supplier conversations and approves changes to standard lead times. | Matching confirmations apply. Slips beyond your tolerance alert the buyer. Lead time master data changes only with buyer approval. |
| Replenishment plan | Calculates reorder points and suggested buys from forecast, lead time, safety stock policy and order minimums. Drafts purchase orders. | The buyer reviews and releases purchase orders. A manager approves any order above your dollar threshold. | Routine drafts go to the buyer's queue for batch review. Nothing is released without a buyer. Large orders route to the named approver. |
| Exceptions and excess | Flags projected stockouts, excess and slow movers. Drafts expedite requests and transfer suggestions, ranked by dollar impact. | The planner decides to expedite, transfer or substitute. The controller approves write-downs. | Every flagged item goes to a person, highest impact first. |

Routing by confidence here rests on track record, not a single model score. The system keeps comparing the forecast with what actually sold. Items whose forecasts have held up run on the plan without a daily touch. Erratic demand, new products, large signals and supplier slips go to a person with the history and the reason attached.

**Example (illustrative values only):** an item sells 20 units a day, the measured lead time is 15 days, and policy sets 100 units of safety stock. The reorder point is 20 × 15 + 100 = 400 units. Use your own numbers. The system does this nightly for every item, using measured lead times.

## What stays with people

- **Overrides for what the data can't see.** A new customer, a lost account, a launch or a price change. Planners adjust the forecast and record why.
- **Service level and safety stock policy.** How much cash to hold against running short is a business decision for operations and finance leadership.
- **Purchase order release.** Buyers release every order. Large orders need a manager.
- **Supplier relationships.** Allocation, expediting, price and terms are negotiated by people.
- **Excess and obsolete write-downs.** These change the balance sheet, so the controller approves them.
- **New product planning.** Items with no history start from a planner's estimate.

## Controls and risks

- **Accuracy targets.** Set targets for forecast error and bias by item group, measured monthly against actual demand. Audit a weekly sample of extracted supplier dates.
- **Forecast value added.** Compare the statistical forecast with the planner-adjusted one after the fact. Keep the overrides that improve accuracy and question the ones that don't.
- **Audit trail.** Store every forecast version, every adjustment with its source and approver, every lead time change, and who released each purchase order.
- **Failure modes.** A failed data feed must stop the run, not produce a plan from stale data. Watch for demand shifts history can't explain, bad units of measure and misread supplier dates. If a run fails or accuracy drops, planners keep the last approved plan. The spreadsheet path stays open through Build.
- **Write-back limits.** The system drafts purchase orders and proposes master data changes. It cannot release orders or change lead times.
- **Data handling and access.** Customer forecasts may be covered by confidentiality terms. Limit access by role through single sign-on.
- **Model and method change control.** Version forecast methods, parameters, prompts and models. Test every change against past demand, and record who approved it.

## How to build it

### Map (week 1-2)

- Shadow one weekly planning cycle and fill in the baseline worksheet.
- Collect every planning spreadsheet and write down the cleaning rules applied by hand.
- Pull as much demand history as you have, ideally more than one seasonal cycle, plus recent purchase orders with receipt dates.

### Redesign

- Decide which item groups the system plans first and which stay with planners.
- Write down the safety stock policy and get operations and finance to sign it.
- Set thresholds for demand adjustments, date slips and purchase order approval, and name an owner for each queue.

### Build (two-week sprints)

- **Sprint 1:** the nightly data pipeline and cleaning rules, checked against the planner's spreadsheet.
- **Sprint 2:** baseline forecasts and tests against history, run in shadow next to the current plan.
- **Sprint 3:** supplier signal extraction from email and acknowledgments, with the buyer review queue.
- **Sprint 4:** replenishment drafts and the exception list.
- Move one item group at a time once its forecast error meets the target. The old path stays open until then.

### Run

- Report weekly on supplier date accuracy, exceptions and expedites.
- Review forecast error, bias and forecast value added monthly with the process owner.
- Re-test after any method, parameter, prompt or model change.

### Reference architecture

- **Intake:** a nightly ERP extract over Tailscale into R2, supplier emails routed to a Worker (Cloudflare Email Routing), and EDI files in R2. Queues buffer the documents.
- **Extraction:** Workers AI or another model provider, through AI Gateway, for emails, customer forecasts and notes.
- **Forecast runs:** statistical forecasting jobs on Fly.io, which suits long batch runs. A scheduled Worker starts each nightly run, and Workflows tracks its steps.
- **Rules and state:** D1 for plan state, thresholds, approvals and audit records. Keep long demand history in R2 files or your existing data warehouse.
- **Human review queue:** a planner and buyer workbench on Vercel, behind Cloudflare Access.
- **System-of-record write-back:** a Worker that writes approved forecasts and purchase order drafts to the ERP or MRP through its API.
- **Observability:** Logpush or Log Explorer for run and decision logs, plus an accuracy report.

**Integration points:** ERP and MRP · warehouse management system · EDI provider · supplier email and portals · CRM and quoting system · data warehouse.

## How to know it is working

- **Forecast error:** the sum of absolute differences between forecast and actual demand, divided by total actual demand, by item group and month.
- **Forecast bias:** whether forecasts run consistently high or low. Persistent bias builds excess or shortages.
- **Line fill rate:** order lines shipped complete from stock, divided by order lines ordered.
- **Inventory turns:** cost of goods sold divided by average inventory.
- **Expedites:** expedited purchase orders per month.
- **Planner touch rate:** the share of items planners adjusted, and hours spent on the weekly cycle.

Review supplier signals and exceptions weekly, and forecast measures monthly with the process owner.

## Getting started checklist

- [ ] Name the process owner, one planner and one buyer who know the exceptions.
- [ ] Shadow one planning cycle and fill in the baseline worksheet.
- [ ] Pull demand history and recent purchase orders with receipt dates.
- [ ] Compare item master lead times with actual receipts for your top suppliers.
- [ ] Write down your safety stock policy, or note that you don't have one.
- [ ] Set dollar thresholds for purchase order approval.
- [ ] Pick the first item group to plan in shadow.

## Related playbooks

- [RT-03 · Demand forecasting](../rt-03/): store and channel forecasts for retailers that respond to promotions and weather.
- [MD-01 · Order-to-cash](../md-01/): clean order data is the main forecast input.
- [MD-04 · Supplier onboarding](../md-04/): accurate supplier records make lead time data trustworthy.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
