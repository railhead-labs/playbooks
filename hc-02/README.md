# HC-02 · Revenue cycle and denials

> Denials sorted by cause, with appeals drafted from the record.

**Industry:** Healthcare and life sciences · **Typical owner:** Director of revenue cycle or denials manager · **Reading time:** 8 min

## Who this is for

Health systems, physician groups, ambulatory surgery centers, labs and post-acute providers that work thousands of claims a month across commercial and government-sponsored plans. The pain sits with follow-up specialists, and with the coders and clinical reviewers pulled into appeals. This playbook fits if denial queues grow faster than your team clears them, if appeal deadlines slip, or if the same denial reasons return every month because nobody upstream hears about them.

## How it runs today

1. Payers send remittance advice: electronic 835 files, plus paper explanations of benefits and denial letters. The posting team posts payments, adjustments and denials to the billing system.
2. Denials land in work queues by payer or reason code. They are worked oldest first, or by whoever picks them up.
3. A specialist opens each denial, reads the reason and remark codes, then opens the claim, the chart, the authorization record and the payer policy to find out what actually went wrong.
4. The specialist decides: correct and resubmit, appeal, bill another payer or the patient, or write off. Questions go to coding, registration or a clinical reviewer, and wait.
5. For an appeal, the specialist gathers records, writes a letter from an old template, assembles attachments and submits by portal, fax or mail.
6. Follow-up means status calls, second-level appeals and deadlines tracked in a spreadsheet.
7. Root causes are counted, if at all, in a monthly report. Fixes in registration, authorization, documentation or charge capture come slowly.

Where the hours go: reading. Codes alone rarely explain a denial, so a specialist reads the letter, the claim and the chart. Then writing: appeal letters are slow, and templates drift from what payers respond to. Then chasing status and deadlines. The hidden cost is repeat work: the same denials return because the upstream cause never gets fixed.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Post denials from paper letters and EOBs | | | | |
| Research the denial cause | | | | |
| Decide the next action | | | | |
| Correct and resubmit claims | | | | |
| Write and assemble appeals | | | | |
| Status follow-up | | | | |
| Root-cause reporting | | | | |
| **Example:** Write and assemble appeals | Appeals specialist | 60 | 45 | 45 |

The example row is illustrative. Hours per week is volume times minutes, divided by 60.

To collect the numbers in one week:

- Pull last quarter's denials from your billing system by payer, reason code and dollar amount.
- Time a sample of a few dozen denials across your main causes, from first touch to resolution or appeal sent.
- Pull timestamps: denial received, first touch, appeal sent, final outcome. The gaps are waiting time.
- Count appeals that missed their deadline, and compute your own overturn rate by payer and cause.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Intake | Reads 835 data and paper letters; captures codes, amounts, reason text and dates | Posting team checks low-confidence paper items | Structured 835 data posts by existing rules. Unclear paper fields go to posting review |
| 2. Classify cause | Assigns a cause from your taxonomy (eligibility, authorization, medical necessity, coding, timely filing, duplicate, coordination of benefits, missing records) and shows the evidence | Denial analyst owns the taxonomy and confirms flagged tags | Codes and letter agree: tag accepted. Disagreement or a new pattern: analyst |
| 3. Prioritize | Ranks by dollars, days left to appeal and your own overturn history for that payer and cause | Supervisor sets and adjusts the ranking rules | Near a deadline: top of queue regardless of score |
| 4. Recommend action | Recommends corrected claim, appeal, other payer, patient balance or write-off, with reasons | Specialist decides. A supervisor approves write-offs above your policy limit | Always a person's decision |
| 5. Correct and resubmit | Drafts corrections for registration and eligibility errors, using facts in the record | Specialist approves. A credentialed coder approves any code change | No code change without a coder |
| 6. Draft appeal | Drafts the letter from the denial, the payer's policy, contract terms and cited chart pages; assembles the packet | Appeals specialist edits and approves. Medical necessity appeals are reviewed and signed by a nurse or physician advisor | Every appeal has a named approver |
| 7. Submit and track | After approval, submits through the approved channel and tracks deadlines | Specialist handles payer calls and escalations | No response by the follow-up date: back to the owner |
| 8. Feed back | Groups causes weekly by upstream owner, with example claims | Revenue cycle director assigns fixes to owners | Always a person's call |

Confidence decides two things: whether a cause tag is accepted without a second look, and which queue a denial lands in. It never decides whether a claim is corrected or an appeal goes out. Reason codes and letter text often disagree. When they do, the denial goes to an analyst, who sees both side by side.

Start with every cause tag reviewed. Accept tags without review only for causes where sampled accuracy has held for several weeks. Ranking should be explainable: each denial shows why it sits where it does. Where you lack history for a payer and cause, rank by dollars and deadline only.

## What stays with people

- **Whether to correct, appeal or write off.** The system recommends. Specialists decide, and they know which payers respond to what.
- **Clinical arguments.** Medical necessity appeals are reviewed and signed by licensed clinical staff.
- **Coding.** Code changes are made only by credentialed coders, based on documentation, never to make a claim pay.
- **Write-offs and patient balances.** Write-offs above your limit need a supervisor. Patient balance decisions follow your financial assistance and billing policies.
- **Payer escalations and contract disputes,** which depend on relationships and contract knowledge.
- **Upstream fixes.** Registration, authorization, documentation and charge capture leaders own them.

## Controls and risks

- **Accuracy targets.** Agree targets for cause-tag accuracy and appeal draft acceptance before launch. A senior analyst checks a random weekly sample. Track overturn rate as an outcome, knowing it lags by months.
- **Claim integrity.** The system never adds or changes codes and never creates documentation. Drafts cite only the record, the payer policy and the contract. Inaccurate claims to government programs can create liability under federal law, including the False Claims Act. Involve your compliance team in the design. <!-- VERIFY: False Claims Act and related federal billing rules as they apply to automated correction and appeal workflows. -->
- **Deadlines from the source.** Appeal and corrected-claim windows come from payer contracts and program rules. A person enters and owns them; the model never infers them. <!-- VERIFY: appeal and corrected-claim filing windows for each payer contract and government program in your mix. -->
- **Audit trail.** Log each cause tag, recommendation, draft, edit, approver, timestamp, source document, and model and prompt version, plus what went to the payer.
- **Fallback.** Existing work queues stay open. If the system is down or quality drops, denials route to the queues your team uses today.
- **Minimum necessary access.** The system reads only the claim data and chart sections a denial needs, with its own scoped, read-only service identity. <!-- VERIFY: how the HIPAA minimum necessary standard applies to payment activities in this workflow. -->
- **Business associate agreements.** Every vendor that stores, processes or transmits PHI here needs a signed BAA first: model providers, cloud services, clearinghouse and scanning vendors. Confirm which products each BAA covers. <!-- VERIFY: BAA requirement for vendors that create, receive, maintain or transmit PHI on your behalf, and the product scope of each vendor's BAA. -->
- **No PHI to services that aren't covered.** Route model calls through one gateway with an allow list of covered endpoints. Turn off response caching for PHI traffic, and turn off prompt logging or keep it in covered storage. Log claim IDs, not PHI. Test with de-identified data. <!-- VERIFY: the de-identification method used for test data meets HIPAA de-identification standards. -->
- **Change control.** The taxonomy, prompts, models, ranking rules and appeal templates are versioned. Each change is tested on labeled past denials and signed off by the process owner. Coding and compliance review new appeal templates.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Walk through about 30 recent denials with specialists, coders and a clinical reviewer. Note every lookup and wait.
- Fill the baseline worksheet. Rank causes by dollars and by count.
- Write the cause taxonomy with your analysts. Keep it short enough that two people tag the same denial the same way.
- Pull appeal windows for your top payers from the contracts.
- Inventory where PHI goes and which vendors have BAAs. Bring in compliance and your privacy officer now.

### Redesign

- Pick the two or three causes with the most dollars. Favor causes where the fix is usually a fact already in the record, such as eligibility or authorization details.
- Write the lane rules and the write-off approval limit.
- Draft appeal templates per payer and cause with your clinical, coding and compliance reviewers.

### Build (two-week sprints)

- **Sprint 1:** ingest 835 data and letters, classify in shadow mode. Analysts compare tags with their own.
- **Sprint 2:** ranked work queue with recommendations. Specialists still decide everything.
- **Sprint 3:** appeal drafting for one cause and one payer, with cited chart pages and named approval.
- **Sprint 4:** deadline tracking and the weekly root-cause report.
- The old queues stay open throughout. Any specialist can pull a denial back to manual.

### Run

- Weekly sampled audit of tags and drafts for the first months, then at a cadence the process owner sets.
- Monthly review with the process owner: accuracy, overturns, deadlines met, and status of each upstream fix.
- Close the loop. A cause assigned to an upstream owner stays on the agenda until its count drops.

### Reference architecture

Every component that touches PHI runs under a BAA covering that specific product.

- **Intake:** 835 files from your clearinghouse to a Worker; scanned letters and EOBs to R2. Private Tailscale links to on-premises billing systems.
- **Extraction and classification:** model calls through AI Gateway, only to BAA-covered endpoints.
- **Rules and state:** taxonomy, ranking rules, deadlines and case state in D1.
- **Orchestration:** Workflows track each appeal as durable steps with follow-up dates. Queues between steps. Large historical reprocessing jobs on Fly.io.
- **Human review queue:** work queue app behind Cloudflare Access, signed in through your identity provider.
- **Write-back:** notes, status and approved corrected claims to the billing system and clearinghouse.
- **Observability:** append-only audit table; Logpush to your SIEM or R2; Log Explorer; a root-cause dashboard.

**Integration points:** billing or practice management system, clearinghouse, EHR (notes and documents), authorization records, payer portals, contract management, document scanning, data warehouse.

## How to know it is working

- **Initial denial rate by cause:** denied claims divided by claims submitted, by cause and payer.
- **Days to first touch:** from denial received to first action.
- **Appeals filed on time:** share of appeals submitted before the deadline.
- **Overturn rate:** share of appealed dollars paid, by cause and payer.
- **Cause-tag accuracy:** share of sampled tags a senior analyst agrees with.
- **Repeat-cause rate:** denials for a cause that recur after its upstream fix date.

Review weekly with the denials supervisor at first, then monthly with the process owner.

## Getting started checklist

- [ ] Pull last quarter's denials by payer, cause and dollars.
- [ ] Fill the baseline worksheet for one week.
- [ ] Write a cause taxonomy and test it: two analysts tag the same 50 denials.
- [ ] Pull appeal windows for your top payers from the contracts.
- [ ] Pick the first cause and payer to automate.
- [ ] Confirm BAA status and product scope for every vendor that would touch PHI.
- [ ] Have compliance and coding review the first appeal templates.
- [ ] Name the write-off approval limit and the weekly audit owner.

## Related playbooks

- [HC-01 · Prior authorization](../hc-01/): fewer authorization denials start with better requests.
- [HC-03 · Intake and referrals](../hc-03/): registration and eligibility errors often start at intake.
- [FS-04 · Reconciliation](../fs-04/): matching remittances to payments and deposits.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
