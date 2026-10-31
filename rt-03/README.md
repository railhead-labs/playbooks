# RT-03 · Demand forecasting

> Store and channel forecasts that respond to promotions and weather.

**Industry:** Retail · **Typical owner:** Director of demand planning · **Reading time:** 9 min

## Who this is for

Multi-store retailers and omnichannel brands that plan by store, channel and week, and run frequent promotions. Demand planners feel the pain, and so do store teams when promoted items run out or sit on the shelf. This playbook fits if the promotion calendar arrives as a slide deck, planners estimate lift from memory, weather means a phone call to a regional manager, and store managers override orders because they don't trust the forecast.

This playbook covers the retail inputs: promotions, store and channel splits, and weather. For the core forecasting and replenishment loop built on orders and suppliers, see [MD-03 Inventory and demand planning](../md-03/).

## How it runs today

1. A baseline forecast comes from the planning system or a spreadsheet built on point-of-sale and online order history.
2. Merchandising and marketing send the promotion calendar: items, discount depth, ad placement, displays, dates and channels. It arrives late and changes often.
3. Planners estimate lift for each promotion by hand, usually from the last similar event they remember.
4. Weather is handled informally. A heat wave or storm in the forecast leads to calls, emails and manual bumps for a few categories.
5. Totals are split across stores and channels with fixed ratios that ignore where the promotion runs and where the weather hits.
6. Store and channel managers override numbers they don't trust. Nobody tracks the overrides.
7. Replenishment and allocation orders go out. After the event, nobody compares plan with actuals in a structured way.

Where the hours go: retyping the promotion calendar, rebuilding a lift estimate for every event, reconciling overrides and explaining misses. The larger cost is harder to see: empty shelves on promoted items, and leftover stock marked down afterward.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Promotion calendar entry | | | | |
| Promotion lift estimates | | | | |
| Weather adjustments | | | | |
| Store and channel split | | | | |
| Override review | | | | |
| Replenishment order review | | | | |
| Post-event review | | | | |
| **Example** (illustrative values only): Promotion lift estimates | Demand planner | 45 promoted items | 20 | 15 |

Hours per week is volume times minutes, divided by 60.

Collect the hours in one week. Sit with planners through one forecast cycle and time each step. Count promoted items and overrides from the planning system. Ask where they wait.

Also record your current accuracy, because the redesign is judged against it. Use two measures at the level you order at, such as item, store and week:

- **WAPE** (weighted absolute percentage error): the sum of absolute errors divided by the sum of actual sales.
- **Bias:** the sum of forecast minus actual, divided by the sum of actual sales. Positive means you over-forecast.

**Example** (illustrative values only): three stores forecast 100, 50 and 30 units of one item. Actual sales are 80, 60 and 30. Absolute errors are 20, 10 and 0, totaling 30. Actual sales total 170. WAPE is 30 ÷ 170, about 18%. Bias is (180 − 170) ÷ 170, about 6% over.

Compute both separately for promoted and regular weeks. They behave differently, and averaging them hides the promotion problem.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Promotion intake | Reads the calendar from decks, spreadsheets and email. Turns each event into a structured record: items, stores, channels, dates, discount, ad and display support. Flags changes since the last version. | Planner confirms uncertain records and asks merchandising about gaps. | Complete and unambiguous: loaded. Missing stores, dates or depth, or conflicting versions: planner. |
| Baseline forecast | A forecasting model (statistical or machine learning, not a language model) forecasts each item by store and channel from sales history, seasonality, price and stockouts. | Planner owns model settings and reviews exceptions. | Runs on a schedule. Large swings from last cycle: exception queue. |
| Promotion lift | Estimates lift from past events with similar items, depth, ad support, display and channel. Estimates the pull from substitute items and the dip after the event. Lists the past events it used. | Planner approves lift for new event types, new items and anything above the approval threshold. | Enough comparable events and lift within range: applied. Few comparables or lift over threshold: planner. |
| Weather adjustment | Pulls weather forecasts for each store's area. Applies category sensitivities learned from your own history. Writes a note on which stores, which categories and why. | Planner or regional manager reviews large adjustments and severe weather. | Small adjustment in a category with a proven weather link: applied. Large swing, severe weather or no proven link: person. |
| Store and channel split | Splits demand using where the promotion runs, recent channel mix and online orders filled from stores. | Store and channel leads review flagged shifts. | Mix change within range: applied. Large shift: person. |
| Overrides | Records each override with a reason and later compares it with actual sales. | Managers can still override. Planners see each manager's track record. | Overrides above a size limit need planner approval. |
| Orders | Drafts replenishment and allocation orders from the approved forecast. | Planner or buyer approves orders above a value limit, new items and one-time promotional buys. | Routine replenishment within limits: released. Over limit or new item: person. |
| Post-event review | Compares plan with actuals for each event and explains the largest misses in plain language. | Planner and merchandiser agree on lessons and update the event library. | Every event gets a review record. |

Confidence here comes from evidence. A lift estimate backed by many similar past events earns more trust than one based on a single event two years ago. A weather adjustment earns trust only in categories where your own history shows a clear link. The system shows the evidence next to every number and routes to a planner when the evidence is thin or the number is large.

The language model does not produce forecast numbers. It reads the promotion calendar, explains changes, writes post-event notes and sorts exceptions. The numbers come from forecasting models you can test, version and backtest.

## What stays with people

- **Lift on new promotion types and new items,** and anything above the approval threshold. Thin history calls for judgment.
- **Severe weather and local events.** Regional managers know about closures, evacuations and community events before the data does.
- **Large purchase commitments.** One-time promotional buys, long-lead imports and items you can't reorder.
- **The promotion calendar conversation.** Telling merchandising a promotion will sell out early is a negotiation.
- **Model settings,** including which categories use weather at all.
- **Accountability for the forecast** in your sales and operations planning meeting.

## Controls and risks

- **Accuracy targets.** Measure WAPE and bias at the ordering level, separately for promoted and regular weeks. Before go-live, the new forecast must beat your current accuracy on a backtest. In production, it must stay ahead.
- **Forecast value added.** For each step (lift, weather, split, override), measure whether it made the forecast more or less accurate than the step before. Remove steps that don't help.
- **Backtesting.** Every model change is tested on past periods held out from training, including past promotions and weather events, before release.
- **Audit trail.** Store each forecast version with its inputs (promotion record, weather data, model version), every adjustment and override with who made it, and the orders it produced.
- **Failure modes and fallback.** Expect late or wrong calendars, weather data outages, new stores with no history, and stockouts that hide true demand. If an input is missing, the system uses the last approved forecast and flags it. The old process runs in parallel until the new forecast beats it over several cycles, and planners can revert at any time.
- **Data handling and access.** Sales history and promotion plans are commercially sensitive. Access is by role. Confirm your weather data license covers commercial use and storing history. <!-- VERIFY: confirm with your weather data provider and counsel that the license permits this use, including storing and reusing historical data. -->
- **Model and prompt change control.** Forecast models, features, thresholds and extraction prompts are versioned. Changes need a passing backtest and the planning owner's sign-off.

## How to build it

### Map (week 1-2)
- Sit with planners through one forecast cycle, and follow one promotion from calendar to post-event.
- List data sources: point of sale, online orders, inventory, promotion calendar, pricing, store attributes and any weather data.
- Fill in the baseline worksheet and compute baseline WAPE and bias.
- Gather every past promotion calendar you can find. These become the event library.
- Note every override path and who uses it.

### Redesign
- Define the forecast level and horizon each decision needs, such as weekly by store for replenishment and longer horizons for promotional buys.
- Agree on a promotion record format with merchandising.
- Choose candidate weather-sensitive categories, then test each against your history before turning weather on.
- Set thresholds for lift, weather adjustments, overrides and orders. Name the approvers.
- Pick a starting scope: one region or category with frequent promotions and good history.

### Build (two-week sprints)
- **Sprint 1:** promotion intake into structured records. Build the event library from past calendars.
- **Sprint 2:** baseline model and a backtest against your current forecast for the starting scope.
- **Sprint 3:** promotion lift and store and channel split, shown to planners next to their own numbers.
- **Sprint 4:** weather for categories that passed the test, the exception queue and override tracking.
- **Sprint 5:** drafted orders with approval limits for the starting scope.
- The old process runs alongside until the new forecast wins over several cycles.

### Run
- Weekly: accuracy by scope, exception queue age, override outcomes.
- After each major promotion: post-event review.
- Monthly with the planning owner: accuracy trend, forecast value added, thresholds and the next region or category.

### Reference architecture
- **Intake:** Cloudflare Workers receive promotion files and emails. Files in R2.
- **Extraction:** Workers AI turns calendars into promotion records, called through AI Gateway for logging and model fallback.
- **Data:** sales history in your existing data warehouse or as files in R2. D1 for promotion records, approvals, overrides and the event library.
- **Forecast runs:** model training and batch forecasts as long-running jobs on Fly.io or your existing data platform.
- **Orchestration:** a Cron Trigger starts a Workflows run each cycle: pull data, run the forecast, apply adjustments, open exceptions, wait for approvals, draft orders. A scheduled Worker pulls weather forecasts from your chosen provider.
- **Human review queue:** planner console behind Cloudflare Access.
- **System-of-record write-back:** approved forecasts and orders to the planning, replenishment or ERP system. Tailscale for on-premises systems.
- **Observability:** Logpush and Log Explorer for runs, adjustments and approvals.

**Integration points:**
- Point of sale and e-commerce order management
- Promotion planning and pricing systems
- Planning and replenishment system
- ERP
- Store and warehouse inventory
- Weather data provider

## How to know it is working

- **WAPE on promoted weeks:** against your baseline, by region and category.
- **Bias:** steady over- or under-forecasting by region, category or channel.
- **Promoted-item in-stock rate:** share of store-days during an event with the item on hand.
- **Post-event excess:** units left after the event, and markdowns taken on them.
- **Forecast value added by step:** whether lift, weather, split and overrides each improved accuracy.
- **Planner hours on promotions:** from the baseline worksheet, re-measured.

Review weekly with planners, after each major event, and monthly with the planning owner.

## Getting started checklist

- [ ] Name the planning owner and approvers for lift, large orders and severe-weather calls.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Compute baseline WAPE and bias for recent promoted and regular weeks.
- [ ] Collect past promotion calendars in one place.
- [ ] Agree on a promotion record format with merchandising.
- [ ] Pick candidate weather-sensitive categories to test.
- [ ] Start recording overrides with a reason.
- [ ] Choose one region or category to start.

## Related playbooks

- [MD-03 Inventory and demand planning](../md-03/): the core forecast and replenishment loop from orders and suppliers. Start there if you don't yet have a baseline forecast you trust.
- [RT-01 Returns](../rt-01/): returns change net demand and put stock back on shelves.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
