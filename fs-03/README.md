# FS-03 · Customer onboarding and KYC

> Identity documents checked against policy, with gaps flagged for a reviewer.

**Industry:** Financial services and insurance · **Typical owner:** Onboarding operations manager, with the BSA/AML officer · **Reading time:** 9 min

## Who this is for

Banks, credit unions and other financial institutions that open accounts for individuals and businesses. The pain sits with onboarding analysts who check every file line by line against the KYC procedure, and with the BSA/AML team who receive files that are incomplete or inconsistent. This playbook fits if business accounts take days to open because of document back-and-forth, if quality control finds the same gaps every month, or if analysts keep personal checklists.

## How it runs today

1. A customer applies online, in a branch or through a relationship manager, with identification. Business customers add formation documents, tax identification, owners and signers.
2. An onboarding analyst checks the application against the KYC procedure: required fields, acceptable documents, matching names and addresses, expiration dates, signatures.
3. Identity verification runs through a vendor or credit bureau. Results come back as scores and codes the analyst interprets.
4. Names are screened against sanctions lists and, where your program requires, politically exposed persons and negative news. Possible matches go to the BSA/AML team.
5. The analyst assigns a customer risk rating and sends higher-risk customers to enhanced due diligence.
6. Gaps go back to the customer or relationship manager by email or phone. The file waits.
7. The analyst or a supervisor approves, and the account opens in the core system. Quality control samples files later.

Where the hours go: comparing documents to each other and to the procedure, by eye. Re-keying data into the core system and screening tool. Clearing alerts that are plainly not the customer. Chasing documents, often for several rounds on a business account because the first request missed something. And QC findings that arrive weeks after the account is open.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Check application completeness | | | | |
| Compare documents to application | | | | |
| Review identity verification results | | | | |
| Clear screening alerts | | | | |
| Risk rate and route to enhanced due diligence | | | | |
| Request missing items | | | | |
| QC rework | | | | |
| **Example (illustrative values):** Clear screening alerts | BSA/AML analyst | 150 | 6 | 15 |

Hours per week = volume × minutes ÷ 60. In the example, 150 × 6 ÷ 60 = 15. Multiply by a loaded hourly cost per role.

Collect the numbers in one week:

- **Sample the work.** Pull recent individual and business files separately; they are different processes. Time each step on a handful.
- **Ask the people doing it.** Sit with two analysts and a BSA/AML analyst. Ask which checks take longest.
- **Pull system timestamps.** Compare application received, file complete, decision and account opened.

Also record request rounds per business account and recent QC findings by type. That is your quality baseline.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Receive | Collects the application and documents from portal, branch or relationship manager into one file. Checks images are legible. | Staff meet the customer where your procedure requires. | Illegible uploads prompt a retry before the file enters the queue. |
| 2. Read documents | Identifies each document and extracts names, dates of birth, addresses, ID numbers, expiration dates, entity details, owners and signers, with the source for each field. | Analyst corrects flagged fields. | Per-field thresholds. Identifying information your procedure requires never passes below threshold. |
| 3. Check against policy | Runs your KYC procedure as an explicit checklist: items present, names and addresses consistent, IDs unexpired, ownership complete. Lists each gap with the rule it relates to. | Analyst reviews the gap list and decides what is a real gap. | Every rule passes or shows as a gap. No silent passes. |
| 4. Verify and screen | Sends data to your verification vendor and screening tool. Summarizes results. For each alert, lays out evidence for and against a match. | BSA/AML analyst dispositions every screening alert. Analyst reviews verification failures. | The AI never clears an alert. It orders alerts and pre-fills the evidence. |
| 5. Risk rate | Pre-fills inputs to your customer risk rating model (products, geography, business type, expected activity) from the application. | Analyst confirms inputs and rating. The BSA/AML officer or delegate approves high-risk ratings and enhanced due diligence outcomes. | The rating model is yours and documented. The AI fills inputs; it does not choose a rating. |
| 6. Request gaps | Drafts one complete, plain-language request listing every missing item. | Analyst or relationship manager approves and sends. | One request per round, covering everything known. |
| 7. Decide and open | Assembles the decision file: checklist, data, verification and screening results, risk rating. Prepares the core system entry. | A named analyst approves or declines every account. Higher-risk files get a second approver. The account opens only after approval. | The AI never opens or declines an account. |

Files move in three lanes. **Clean files** pass every check, match on verification, have no alerts and rate low risk. They go to a fast approval queue, where an analyst confirms the checklist and approves quickly because the reading is done. **Gap files** go to an analyst with the gaps and a drafted request. **Alert and higher-risk files** go to the BSA/AML team. The lanes change who reviews and how much they read. They never remove the review.

Start in shadow mode. Compare the system's gap lists with analysts' findings and past QC results, and set thresholds from that. The system compares documents; it does not certify that a document is genuine. Authenticity, liveness and database checks stay with a verification vendor whose method you have vetted.

## What stays with people

- **Every approval and decline.** A named analyst decides each account. The AI assembles the file.
- **Screening alerts.** BSA/AML analysts disposition every alert and record why.
- **Higher-risk relationships.** Risk ratings, enhanced due diligence and decisions to decline or exit stay with the BSA/AML officer or delegate.
- **Suspicious activity.** Concerns go to the BSA/AML team through your referral process. The AI does not judge suspicion and drafts nothing to the customer about it.
- **Customer conversations.** A person explains declines and sensitive requests.
- **The procedure.** The BSA/AML officer owns it and approves exceptions. The checklist follows it.

## Controls and risks

- **Accuracy targets.** Set per-field targets with the onboarding operations manager. For gaps, measure recall: gaps the system found versus gaps found in sampled QC review. A missed gap matters more than an extra flag.
- **Audit trail.** Record documents received, extracted data with sources, every check and result, model and prompt versions, every human change, alert dispositions with reasons, and the approver. Examiners should be able to rebuild any decision from the file.
- **Regulatory basis.** For US banks, the Bank Secrecy Act and its implementing rules require a customer identification program (CIP): collecting identifying information, verifying identity, keeping records and giving customers notice. For these rules, "bank" generally includes credit unions and savings associations. <!-- VERIFY: that the CIP rule covers your institution type, plus CIP minimum data elements, verification timing, recordkeeping periods and notice requirements. --> FinCEN's customer due diligence requirements add identification and verification of beneficial owners of legal entity customers, a customer risk profile and ongoing monitoring. <!-- VERIFY: current beneficial ownership thresholds, exclusions and any recent FinCEN changes, including those related to the Corporate Transparency Act. --> Sanctions compliance under OFAC is a separate obligation. <!-- VERIFY: OFAC screening scope and timing for your institution. --> Broker-dealers, money services businesses and fintechs working through a partner bank have related but different obligations. <!-- VERIFY: which rules apply to your charter or business type. -->
- **SAR confidentiality.** Suspicious activity reports are confidential. Keep SAR-related information out of onboarding drafts, prompts and logs that onboarding staff can see. <!-- VERIFY: SAR confidentiality requirements and how they apply to your systems, logs and vendors. -->
- **Model risk.** Bring the AI components into your model risk and third-party risk programs, with validation before go-live and on change. <!-- VERIFY: applicable bank regulatory guidance on model risk management and third-party risk. --> Include the system in the scope of your BSA program's independent testing.
- **Biometrics.** If your verification vendor uses selfies or face matching, some states regulate biometric data. <!-- VERIFY: state biometric privacy laws that apply to your customers and vendor. -->
- **Failure modes and fallback.** The worst failures are a missed gap, names marked consistent when they are not, and a misread ID number. If the vendor, screening tool or model service is down, files wait; they never default to approval. The manual path stays open.
- **Data handling and access.** Identity documents are high-value targets. Encrypt them, keep them off public URLs, restrict access by role, and mask ID and account numbers in model-call logs. Retain records as your BSA program requires. The Gramm-Leach-Bliley Act's privacy and safeguards requirements likely apply. <!-- VERIFY: GLBA and state privacy requirements for your institution. -->
- **Change control.** The BSA/AML officer approves any change to checklist rules. Version prompts, models and thresholds, and test changes against past files, including files with known QC findings.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Trace 20 to 30 individual and 20 to 30 business files from application to account open.
- List every handoff, wait and workaround with analysts, with hours and cost per step.
- Collect the KYC procedure, recent QC findings and alert volumes. Note where personal checklists differ from the procedure.

### Redesign

- Turn the procedure into explicit checklist rules with the BSA/AML officer. Ambiguous rules stay with the analyst.
- Agree the field list, thresholds and the three lanes.
- Name approvers for each lane, including second approvers for higher-risk files.
- Write the customer request templates in plain language.

### Build (two-week sprints)

- **Sprint 1:** intake and extraction for one consumer product, in shadow mode.
- **Sprint 2:** the checklist engine and gap lists, compared with analyst findings and QC history.
- **Sprint 3:** verification and screening summaries, with alert evidence.
- **Sprint 4:** the decision file, fast approval queue and core write-back for that product, behind a switch you can turn off.
- **Later:** business accounts with ownership structures. The old path stays open until the new one proves out.

### Run

- Weekly accuracy and gap recall report.
- Monthly review with the onboarding operations manager and BSA/AML officer: thresholds, QC findings, procedure changes.

### Reference architecture

- **Intake:** onboarding portal on Vercel posting to Workers endpoints behind WAF. Workers endpoints for branch scans and relationship manager uploads. Queues to buffer volume.
- **Storage:** R2 for documents, private and encrypted. D1 for file state, checks, dispositions and approvals.
- **Extraction and summaries:** Workers AI models (or another provider) through AI Gateway. Mask ID numbers before each call and limit payload logging.
- **Rules and orchestration:** checklist rules as plain code in Workers, deterministic and reviewable. Workflows runs each file through its steps durably.
- **Human review queue:** an analyst workbench behind Access, with roles for analysts, BSA/AML and QC.
- **Write-back:** Workers calling the core banking system. Tailscale for a private link to an on-premises core.
- **Observability:** Logpush to your SIEM, Log Explorer for investigations, accuracy reports from D1.

**Integration points:** core banking, digital account opening platform, identity verification vendor, sanctions and PEP screening tool, customer risk rating model, CRM, document imaging and BSA/AML case management.

## How to know it is working

- **Time to decision:** complete application to approve or decline, by product.
- **First-request completeness:** share of files needing only one document request round.
- **Gap recall on sampled audit:** share of gaps found in QC review that the system had already flagged.
- **Field accuracy:** share of fields correct against source in a weekly sample.
- **Alert handling time:** time from screening alert to disposition.
- **Post-opening QC finding rate:** QC findings per sampled file after go-live, compared with your baseline.

Review weekly with the onboarding lead and monthly with the process owner and BSA/AML officer.

## Getting started checklist

- [ ] Name the process owner and confirm the BSA/AML officer's role in the design.
- [ ] Pull samples of recent individual and business files.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Collect the KYC procedure and the last few QC reports.
- [ ] Ask compliance to confirm which rules apply to your institution.
- [ ] Agree the three lanes and who approves in each.
- [ ] Pick one consumer product for the first shadow sprint.

## Related playbooks

- [MD-04 · Supplier onboarding](../md-04/): the same collect, check and file pattern, applied to supplier documents.
- [FS-02 · Underwriting submissions](../fs-02/): sanctions screening and document reading ahead of an underwriter's decision.
- [AG-02 · Agent identity and access](../ag-02/): scoped access for the agents that handle customer identity data.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
