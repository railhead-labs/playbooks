# FS-04 · Reconciliation

> Breaks found and explained across ledgers before anyone opens a spreadsheet.

**Industry:** Financial services and insurance · **Typical owner:** Controller or head of finance operations · **Reading time:** 9 min

## Who this is for

Banks, insurers, lenders, payment companies and asset managers that reconcile high volumes across systems never built to agree: bank accounts to the general ledger, core or policy systems to the GL, settlement to processor reports, custodian positions to internal books. The pain sits with reconciliation analysts who export, match and investigate in spreadsheets, and with controllers who sign off on aged breaks nobody can fully explain. This playbook fits if close depends on a few people's spreadsheets, or if the same break causes come back every month.

## How it runs today

1. Analysts export data from each source: bank statement files, GL detail, core or policy system extracts, processor and custodian reports.
2. They clean and load it into spreadsheets or a reconciliation tool. Formats differ: truncated references, different cut-off times, amounts net on one side and gross on the other.
3. Matching runs on rules: exact amount and reference first, then looser rules. Whatever doesn't match becomes a break.
4. An analyst investigates each break: searches source systems, reads remittance details, emails operations, treasury or claims teams, and waits.
5. The analyst writes an explanation and, where needed, prepares an adjusting entry or asks the owning team to fix the source.
6. A reviewer checks the reconciliation, explanations and entries, and signs off.
7. Unresolved breaks carry forward and age. Old ones get escalated, written off with approval, or carried.

Where the hours go: not the matching. Rules handle most clean items. The hours go to breaks: finding the related transaction elsewhere, reading free-text descriptions, deciding whether it is timing or a real error, and writing it up. Reviewers redo investigation when explanations are thin. Recurring causes, like a fee posted net or a processor cut-off, get explained again every month instead of fixed.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Export and prepare data | | | | |
| Run matching and review results | | | | |
| Investigate breaks | | | | |
| Write explanations and prepare entries | | | | |
| Chase owning teams | | | | |
| Review and sign off | | | | |
| **Example (illustrative values):** Investigate breaks | Reconciliation analyst | 240 | 10 | 40 |

Hours per week = volume × minutes ÷ 60. In the example, 240 × 10 ÷ 60 = 40. For monthly reconciliations, divide the period's volume by the number of weeks.

Collect the numbers in one week:

- **Sample the work.** Pick the reconciliations with the most breaks. Time the investigation of a sample of breaks, start to finish.
- **Ask the people doing it.** Sit with two analysts and a reviewer. Ask which breaks take hours and which nobody owns.
- **Pull break history.** From your reconciliation tool or spreadsheets, get break counts by account, age and cause for the last few periods.

Also record how many breaks turn out to be timing differences, and how many sit past your aging thresholds. Those set your quality baseline.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Ingest | No model needed: plain software loads each source on schedule, normalizes formats, dates, signs and references, and checks control totals. | Feed owners fix source problems. | A feed that fails control totals stops the run. Nothing reconciles on partial data. |
| 2. Match | Runs your deterministic rules first (exact, tolerance, one-to-many). For what remains, proposes matches from descriptions, remittance text, counterparties and past approved matches, with evidence. | Analyst accepts or rejects proposed matches. | Rule matches clear as they do today. AI proposals are never final until a person accepts them. |
| 3. Classify breaks | Labels each break by likely cause: timing, missing entry, duplicate, amount difference, fee or FX, misposting, unknown. | Analyst confirms or changes the cause. | "Unknown" and anything above your materiality threshold go to a senior analyst. |
| 4. Explain | Drafts a short explanation for each break with links to evidence: the related transaction, the expected clearing date, the prior-period pattern. | Analyst edits and owns the explanation. | Drafts without evidence links are marked unsupported. |
| 5. Propose fix | Drafts the adjusting entry or the correction request to the owning team. | An accountant reviews entries and posts them under your authority matrix. The owning team fixes source errors. | The AI never posts an entry. Entries above thresholds need the approvals your policy sets. |
| 6. Package | Assembles the reconciliation: balances, match counts, breaks by cause and age, explanations, proposed entries. | Preparer and reviewer sign off separately. The controller or delegate approves write-offs. | Sign-off always stays with people, and preparer and reviewer are different people. |
| 7. Fix root causes | Groups recurring breaks by cause and source each month. | The process owner picks causes to fix and assigns owners. | Reviewed monthly. |

Two kinds of matching sit side by side. Rule-based matches are deterministic and auditable, so keep them. AI-proposed matches and break causes carry a confidence score and an evidence list. Start by reviewing every AI proposal one at a time. Once a proposal type proves accurate in sampled audits, high-confidence proposals of that type with complete evidence can be accepted in batches after a spot check. Low-confidence proposals stay one at a time. Anything material or unexplained goes to a senior analyst.

False matches are worse than missed ones. A missed match is a break someone looks at. A false match hides a real error inside a reconciled balance. Measure the false-match rate on its own and set thresholds to keep it near zero.

## What stays with people

- **Sign-off.** A preparer and a separate reviewer sign every reconciliation.
- **Journal entries.** An accountant approves and posts each one, under your authority matrix.
- **Write-offs.** The controller or delegate approves them.
- **Materiality and escalation.** Deciding what goes to leadership, auditors or regulators.
- **Counterparty disputes.** Conversations with banks, processors and custodians about contested items.
- **Root-cause fixes.** Choosing which upstream process to change, and getting the owning team to change it.
- **Unknown breaks and possible fraud.** Someone who knows the systems investigates. Suspected fraud goes where your policy says, such as internal audit.

## Controls and risks

- **Accuracy targets.** The controller sets targets for false-match rate, cause classification accuracy and the share of explanations with supporting evidence. Someone other than the preparer measures them each period on a random sample.
- **Audit trail.** Keep every source file and control total, every match with its rule or proposal and who accepted it, explanation edits, each entry's preparer, approver and poster, sign-offs, and model and prompt versions. Auditors should be able to trace any reconciled item to its source.
- **Internal control over financial reporting.** If you are a public company, many of these reconciliations are likely key controls under the Sarbanes-Oxley Act. Changing how they run is a control change: document the new control, test it and involve your auditors early. Insurers may have similar expectations under state versions of the NAIC Annual Financial Reporting Model Regulation (often called the Model Audit Rule), and banks above certain sizes have internal control reporting requirements.
- **Segregation of duties.** AI components get read access to source systems and write access only to the reconciliation workspace. They cannot post to the GL. Give each its own scoped service identity and include it in access reviews.
- **Failure modes and fallback.** Watch for false matches, stale or partial feeds, explanations that sound right but cite the wrong evidence, and drift after a source system change. If a feed or the model service fails, that reconciliation runs the current way. Keep the old spreadsheets or tool in use until the new path has run cleanly through several period-ends.
- **Data handling and access.** Transaction detail can include account numbers and customer names. Send models only the fields they need, restrict access by role, use model providers that contractually do not train on your data, and retain records under your records policy.
- **Change control.** Version match rules, prompts, models and thresholds. Before release, rerun prior periods with known answers and compare. The controller approves changes.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Pick one reconciliation with high break volume and a clear owner.
- Trace one full period with the analyst: every export, handoff, wait and workaround, with hours and cost per step.
- Pull break history by cause and age. List each data source, its format and its owner.
- Document the current control: who prepares, who reviews, what evidence is kept.

### Redesign

- Write the match rules down explicitly. Many live only in spreadsheet formulas.
- Agree a break cause list with the analysts.
- Set materiality thresholds and approval roles with the controller.
- Design the package the reviewer sees, and walk your auditors through the planned control.

### Build (two-week sprints)

- **Sprint 1:** ingest, control totals and your deterministic rules. Results must match the current process before you go further.
- **Sprint 2:** AI match proposals and break classification in shadow mode.
- **Sprint 3:** explanations with evidence links, and the review screen.
- **Sprint 4:** the package and sign-off flow. Run in parallel with the old process through full period-ends.
- **Later:** a second reconciliation, then more. The old path stays open until each proves out.

### Run

- A report each period on false-match rate, classification accuracy, aging and unexplained breaks, shared with internal audit.
- Monthly review with the controller: thresholds, recurring causes, root-cause fixes.

### Reference architecture

- **Ingest:** scheduled Workers pulling from bank, processor and custodian APIs. Fly.io for SFTP pulls and long-running jobs. Tailscale for a private link to an on-premises GL or core system. Queues between steps.
- **Storage:** R2 for raw source files, unchanged. D1 for matches, breaks, explanations and sign-offs. At very high transaction volumes, keep detail in your data warehouse and store references.
- **Matching:** deterministic rules in Workers, or on Fly.io for large batch runs.
- **AI proposals and drafting:** Workers AI models (or another provider) through AI Gateway for logging, rate limits and fallback.
- **Orchestration:** Workflows runs each reconciliation as durable steps with retries.
- **Human review queue:** a reconciliation workbench behind Access, with roles for preparers, reviewers and the controller.
- **Write-back:** proposed entries go into the GL's own approval workflow. Nothing posts directly.
- **Observability:** Logpush to your SIEM, Log Explorer for investigations, period reports from D1.

**Integration points:** general ledger or ERP, core banking or policy and claims systems, bank statement feeds, payment processors, custodians, treasury management system, data warehouse, and any reconciliation tool you already run.

## How to know it is working

- **Match rate:** share of items cleared by rules or by accepted AI proposals.
- **False-match rate on sampled audit:** share of sampled matches that were wrong. Keep it near zero.
- **Break aging:** count and value of breaks past your aging thresholds.
- **Explained-on-arrival rate:** share of breaks with an evidence-backed explanation before an analyst opens them.
- **Time to sign-off:** days from period end to reviewer sign-off.
- **Recurring break rate:** share of breaks from causes seen the prior period.

Review weekly during close and monthly with the controller.

## Getting started checklist

- [ ] Name the controller as process owner and one senior analyst as design partner.
- [ ] Pick the first reconciliation.
- [ ] Pull break history for the last few periods.
- [ ] Fill in the baseline worksheet for one week of close.
- [ ] Write down the current match rules.
- [ ] List every data source with its format and owner.
- [ ] Brief your external auditors on the planned control change.
- [ ] Agree materiality thresholds and approval roles.

## Related playbooks

- [MD-01 · Order-to-cash](../md-01/): cash application and payment matching on the receivables side.
- [FS-01 · Claims intake](../fs-01/): the claims process whose payments and recoveries land in these ledgers.
- [AG-02 · Agent identity and access](../ag-02/): one scoped identity for each agent that reads your ledgers.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
