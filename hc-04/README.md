# HC-04 · Quality reporting

> Measures pulled from the record on a schedule, not rebuilt each quarter.

**Industry:** Healthcare and life sciences · **Typical owner:** Director of quality or quality reporting manager · **Reading time:** 8 min

## Who this is for

Health systems, physician groups and post-acute providers that report quality measures to several programs at once: government quality programs, health plan measures such as HEDIS, value-based contracts, registries and accreditation bodies. <!-- VERIFY: which quality reporting programs apply to your organization and their current requirements. --> The pain sits with quality analysts, chart abstractors and informatics staff. This playbook fits if every reporting period is a scramble, if your numbers never match the payer's, or if care gap lists reach clinics too late in the year to act on.

## How it runs today

1. A new reporting period starts, or updated measure specifications arrive. Analysts update their queries and spreadsheets, often rebuilding them.
2. Data comes from EHR reports, claims files, lab feeds and registries. Each source is pulled separately and joined by hand.
3. Analysts compute denominators. Much numerator evidence (screenings done elsewhere, outside results, scanned reports) sits outside structured fields, so abstractors read charts.
4. Exclusions and exceptions are reviewed one patient at a time.
5. Internal numbers are compared with payer gap lists and reports. Differences are investigated patient by patient.
6. Reports are built and submitted to each program in its own format and portal.
7. Gap lists go to clinics, often late in the period.
8. When an audit comes, staff reassemble the evidence from scratch.

Where the hours go: rebuilding the same logic every cycle, abstracting charts, and reconciling numbers that disagree. The cost that matters most is time. Because the numbers arrive late, care teams get gap lists when there is little time left to close the gaps.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Update measure logic for new specifications | | | | |
| Pull and join data | | | | |
| Chart abstraction | | | | |
| Review exclusions and exceptions | | | | |
| Reconcile with payer reports | | | | |
| Build and submit reports | | | | |
| Produce and send gap lists | | | | |
| Retrieve audit evidence | | | | |
| **Example:** Chart abstraction | Quality abstractor | 150 | 12 | 30 |

The example row is illustrative. Hours per week is volume times minutes, divided by 60.

Many of these steps run quarterly or yearly, so collect the numbers differently:

- List every measure, program, owner and submission date in one calendar.
- Ask each analyst and abstractor how many hours each step took in the last reporting period. Divide by the weeks in the period to get a weekly average.
- Pull counts of charts abstracted and gap lists sent from your tracking sheets.
- Time a sample of a few dozen chart abstractions this week to check the estimates.
- Count the patients where your status and a payer's status disagreed last period.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Measure logic | When specifications change, drafts a change list: what changed and which logic it affects | Analyst or informaticist edits and approves the logic; test cases must pass | No logic change goes live without approval and passing tests |
| 2. Scheduled data pull | Not needed for structured data; pipelines pull EHR, claims and lab data on a schedule. AI flags anomalies such as a missing feed or a sudden drop | Data owner fixes feed problems | Anomaly found: the run holds and the owner is alerted |
| 3. Find evidence in documents | Searches notes and scanned documents for candidate evidence (an outside screening report, a documented exclusion reason) and links the passage | Abstractor confirms each item before it counts | AI-found evidence never counts until a person confirms it |
| 4. Compute results | Rules compute status per patient. AI writes a plain explanation of why each open patient is open | Analyst reviews outliers and large swings | Rate moves beyond a set tolerance since the last run: analyst review before release |
| 5. Care gaps | Drafts a pre-visit summary of open gaps for the care team | Clinicians decide what care to offer; outreach staff contact patients | Care decisions always rest with the care team |
| 6. Reconcile with payers | Compares payer gap lists with internal status and drafts a list of differences with evidence | Analyst reviews; quality director approves any supplemental data sent | Every outbound submission has a named approver |
| 7. Report and submit | Produces each report in the program's format | Quality director signs off; an authorized person submits and attests | Always submitted by a person |
| 8. Audit pack | Keeps the patient-level evidence trail for each measure | Quality lead answers auditors | Always a person's response |

Confidence matters most at step 3. A candidate with a clear match (right test, date inside the measurement period, clear result) goes to a quick confirmation screen with the passage shown. A weak or ambiguous candidate (unclear test type, date near the period edge, conflicting notes) goes to a full abstraction review. Nothing counts toward a numerator or an exclusion on the system's judgment alone.

Track how often abstractors confirm the system's candidates, by measure. Use that to order the work and decide how much a reviewer reads, not to skip review.

## What stays with people

- **Interpreting specifications.** Analysts and informaticists decide how a specification maps to your data and approve every logic change.
- **Confirming chart evidence.** An abstractor confirms each piece of evidence before it counts.
- **Exclusions that need clinical judgment.** These go to clinical staff, not the system.
- **Care decisions.** Gap summaries inform clinicians. They do not tell them what to do.
- **Sign-off, submission and attestation.** The quality director and authorized submitters own every report.
- **Auditors and payers.** Explaining your numbers is a conversation.
- **Choosing where to improve.** Leadership decides which measures get focus and resources.

## Controls and risks

- **Accuracy targets.** Test measure logic against a set of patient test cases with known answers. For document evidence, agree targets for precision (share of candidates confirmed) and recall. To measure recall, abstractors review a random sample of charts where the system found nothing.
- **Reporting integrity.** The system never edits documentation or creates evidence. Gaps close only when care is delivered and documented. Report results as computed. Some programs require an attestation that submitted data is accurate. <!-- VERIFY: attestation and data accuracy requirements for each program you submit to. -->
- **Specification versions.** Record the specification version for each measure and program. Specifications are updated periodically, often yearly, and a run must use the version for its period. <!-- VERIFY: specification update cycles and version rules for each program. -->
- **Audit trail and reproducibility.** Store the logic version, data snapshot, evidence confirmations and approver for every report. You should be able to rerun a past report and get the same numbers.
- **Fallback.** Keep the current method documented and runnable. Run old and new side by side for one full reporting period before retiring the old one.
- **Minimum necessary access.** The system reads only the data elements and documents the measures need, with its own scoped, read-only service identity. Share aggregate rates widely; restrict patient-level lists by role. <!-- VERIFY: how the HIPAA minimum necessary standard applies to quality reporting and health care operations in this workflow, and the basis for disclosing patient-level data to payers and registries. -->
- **Business associate agreements.** Every vendor that stores, processes or transmits PHI here needs a signed BAA first: model providers, cloud and data platforms, and reporting vendors. Confirm which products each BAA covers. <!-- VERIFY: BAA requirement for vendors that create, receive, maintain or transmit PHI on your behalf, and the product scope of each vendor's BAA. -->
- **No PHI to services that aren't covered.** Route model calls through one gateway with an allow list of covered endpoints. Turn off response caching for PHI traffic, and turn off prompt logging or keep it in covered storage. Log record IDs, not PHI. Test with de-identified or synthetic data. <!-- VERIFY: the de-identification method used for test data meets HIPAA de-identification standards. -->
- **Change control.** Measure logic, prompts, models and evidence rules are versioned. Each change runs against the test cases and is signed off by the process owner.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Build the measure calendar: every measure, program, owner, data source and submission date.
- Trace one measure end to end with the analyst and abstractor who own it. Note every query, spreadsheet and handoff.
- Fill the baseline worksheet.
- Map each data source: where it lives, how often it refreshes, who owns it.
- Inventory where PHI goes and which vendors have BAAs. Bring in your privacy officer now.

### Redesign

- Pick a few measures with heavy abstraction and clear specifications to start.
- Write the evidence rules for each: what counts, what dates qualify, what goes to full review.
- Build test cases for each measure with your analysts, including edge cases they have argued over.
- Plan the parallel run for one full reporting period.

### Build (two-week sprints)

- **Sprint 1:** scheduled data pulls and versioned logic for the first measures, with test cases.
- **Sprint 2:** evidence search and the confirmation screen. Abstractors confirm and mark misses.
- **Sprint 3:** patient-level results with explanations; gap lists to care teams on a schedule.
- **Sprint 4:** payer reconciliation, report output and the audit pack.
- The old method keeps running until the parallel run matches.

### Run

- Weekly sampled audit of evidence and results for the first months, then at a cadence the process owner sets.
- Monthly review with the process owner: accuracy, recall sample, data feed health, payer differences and gap list timing.
- Before each new specification year, run the logic change process and test cases early.

### Reference architecture

Every component that touches PHI runs under a BAA covering that specific product.

- **Intake:** scheduled extracts from the EHR (bulk FHIR export where supported, or a reporting database), claims files and lab feeds, over Tailscale links to on-premises systems. Files land in R2.
- **Pipelines:** Workflows, started on a schedule, run each refresh as durable steps. Large joins run as long jobs on Fly.io or in your data warehouse.
- **Evidence search:** model calls through AI Gateway, only to BAA-covered endpoints.
- **Rules and state:** measure definitions, run history and review state in D1; large patient-level tables in your warehouse.
- **Human review queue:** confirmation app behind Cloudflare Access, signed in through your identity provider.
- **Outputs:** gap lists to EHR worklists or care management; reports prepared for submission by people.
- **Observability:** append-only audit table; feed health alerts; Logpush to your SIEM or R2; Log Explorer.

**Integration points:** EHR, data warehouse, payer claims and gap list files, lab and health information exchange feeds, registries, payer portals for supplemental data, care management platform, program submission portals.

## How to know it is working

- **Time to report:** days from period close to a report ready for sign-off.
- **Abstraction hours per period:** total hours abstractors spend, compared with your baseline.
- **Evidence precision:** share of system candidates abstractors confirm, by measure.
- **Evidence recall:** share of qualifying evidence the system found, from the random no-evidence sample.
- **Payer differences resolved:** patients where your status and the payer's differ, and the share resolved before submission.
- **Gap list freshness:** days from a gap opening to the care team seeing it.

Review weekly with the quality reporting manager at first, then monthly with the process owner.

## Getting started checklist

- [ ] Build the measure calendar with owners and submission dates.
- [ ] Fill the baseline worksheet from last period's hours.
- [ ] Pick the first few measures.
- [ ] Write evidence rules and test cases for each with your analysts.
- [ ] Map data sources and refresh schedules.
- [ ] Confirm BAA status and product scope for every vendor that would touch PHI.
- [ ] Plan a parallel run for one full reporting period.
- [ ] Name the logic approver and the weekly audit owner.

## Related playbooks

- [HC-02 · Revenue cycle and denials](../hc-02/): the same claims and chart data, read for a different purpose.
- [HC-03 · Intake and referrals](../hc-03/): outside records captured at intake become quality evidence later.
- [AG-02 · Agent identity and access](../ag-02/): one identity per agent and scoped access to patient data.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
