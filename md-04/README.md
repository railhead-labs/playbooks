# MD-04 · Supplier onboarding

> Supplier documents collected, checked, and filed without a week of email.

**Industry:** Manufacturing and distribution · **Typical owner:** Procurement or purchasing manager · **Reading time:** 8 min

## Who this is for

Manufacturers and distributors that add suppliers every month. Procurement feels the pain first, then accounts payable and quality. This playbook fits if a new supplier takes weeks to set up, buyers work around the process for urgent orders, vendor files are incomplete, and insurance certificates expire unnoticed.

## How it runs today

1. **Request.** A buyer asks procurement to add a supplier. Nobody checks whether it is already in the ERP under a slightly different name.
2. **Packet out.** Procurement emails a packet: a supplier form, a tax form, banking details, a certificate of insurance, quality certifications, and agreements to sign.
3. **Chasing.** Documents return in pieces over days or weeks. Procurement tracks gaps in a spreadsheet and sends reminders.
4. **Checking.** Someone reads each document. Do names match across forms? Do insurance limits and dates meet requirements? Are certifications current and in scope?
5. **Screening and approvals.** Finance screens the supplier against sanctions lists, accounts payable verifies bank details, and quality approves critical suppliers.
6. **Vendor setup.** Accounts payable keys the vendor record into the ERP, and a second person approves it.
7. **Filing and upkeep.** Documents go to a shared drive. Expiration dates live in a spreadsheet, if they are tracked at all.

The hours go to email: sending packets, chasing pages and answering repeat questions. Then comes retyping the same name, address and tax ID into the ERP. Each step waits on the one before.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Request | | | | |
| Packet out | | | | |
| Chasing | | | | |
| Checking | | | | |
| Screening and approvals | | | | |
| Vendor setup | | | | |
| Filing and upkeep | | | | |
| **Example (illustrative values only):** Chasing | Procurement specialist | 60 reminder emails | 5 | 5 |

Hours per week = volume × minutes each ÷ 60. In the example, 60 × 5 ÷ 60 = 5. Multiply by a loaded hourly cost for the cost of each step.

Collect the numbers in one week:

- **Pull dates.** For recent suppliers, compare the request date with the date the vendor record went active. The gap is your time to onboard.
- **Count the email.** Count a week of onboarding email, and how much was reminders or repeat questions.
- **Sample the files.** Open a few dozen active vendor files. Note missing documents, expired certificates and names that don't match.
- **Ask the people doing it.** Ask where suppliers get stuck and which checks people do from memory.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Request | Checks the vendor master for duplicates and picks the checklist for the supplier type. | Procurement approves the need for a new supplier. | Possible duplicates go to procurement before anything goes out. |
| Document collection | Sends a portal link with the checklist. Reads each upload, shows what is missing, and sends reminders on a schedule you approve. | Procurement answers questions the portal can't. | Suppliers that stall after the set number of reminders go to the buyer to call. |
| Document check | Extracts name, address, tax ID, insurance limits, certification scope and dates. Cross-checks them against each other and your requirements. | Procurement reviews flagged documents. | Clean, consistent documents that meet requirements are marked checked. Mismatches, missing signatures, low limits and unreadable pages go to a person. |
| Screening | Runs your sanctions, denied-party and tax ID checks and collects the results. | A named compliance or finance reviewer decides any potential match. | No match: logged and passed. Potential match: the supplier stays inactive until a person clears it. |
| Bank details | Extracts bank details and flags any difference from the bank letter. | Accounts payable calls the supplier at a number obtained independently, not one from the submission. A second person approves. | Always a person. No bank details go live without a call-back and a second approval. |
| Quality approval | Summarizes certifications and past audit history. Drafts the approved-supplier record. | Quality approves suppliers in critical categories. | Critical categories always need quality approval. |
| Vendor setup | Drafts the ERP vendor record from checked data. | Accounts payable reviews it. A second person approves. | No vendor record goes active without two people. |
| Upkeep | Tracks expiration dates, requests renewals before they lapse, and reads the renewals. | Procurement handles suppliers who don't renew. | Lapses alert the buyer, or block new purchase orders if your policy says so. |

Routing by confidence here asks whether documents agree with each other and with your requirements. A clean, consistent packet that meets policy can be marked checked without a person reading every line. Anything else goes to procurement with the conflicting values side by side.

Sanctions matches, bank details and vendor activation never route by confidence. A named person always decides, because a mistake means paying the wrong party or account.

## What stays with people

- **Whether to add the supplier.** Sourcing strategy belongs to procurement.
- **Potential sanctions or denied-party matches.** A match may be a different party with a similar name. A trained person clears each one and records why.
- **Bank details.** Bank change requests by email are a known fraud pattern. Every new account or change is verified by phone, at an independently obtained number, with a second approver.
- **Quality approval for critical parts.** Quality engineers judge certifications and history.
- **Exceptions to requirements.** Lower insurance limits or non-standard terms go to risk or legal.
- **Vendor activation.** Two people approve every record, so no one person can create a supplier and pay it.

## Controls and risks

- **Accuracy targets.** Audit a weekly sample of checked documents for extraction accuracy. Bank details and tax IDs always get a person's check.
- **Separation of duties.** The requester can't approve the vendor record or bank details. The system's service account drafts records but can't activate them.
- **Audit trail.** Keep each document version, extracted values, cross-check and screening results, call-back notes and every approval, with names and times.
- **Failure modes.** Watch for unreadable scans, trade names that differ from legal names, and certificates for the wrong entity. If the portal or extraction fails, procurement falls back to the email packet, which stays open through Build.
- **Data handling and access.** Encrypt tax IDs and bank details at rest, mask them in review screens, limit access to named reviewers through single sign-on, and keep them out of model prompts where a masked value will do.
- **Tax forms.** U.S. suppliers usually provide IRS Form W-9, which gives you the taxpayer identification number used for information returns such as Form 1099. Foreign suppliers usually provide a Form W-8 instead. If you file information returns, the IRS offers a TIN Matching service to check a name and TIN combination before you file.
- **Sanctions screening.** Many U.S. companies screen suppliers against government lists such as the OFAC Specially Designated Nationals list. Counsel should set which lists you screen against and how often you re-screen.
- **Model and prompt change control.** Version prompts, checklists and models. Test each change against past supplier packets with known answers, and record who approved it.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Trace a few recent suppliers from request to first purchase order with procurement, accounts payable and quality. Fill in the baseline worksheet.
- Collect your packet, forms and requirements by supplier category.
- Gather a test set of past supplier packets with what your team decided.

### Redesign

- Write the checklist for each supplier type and get procurement, finance and quality to sign it.
- Define what can be marked checked and what always needs a named approver. Confirm separation of duties.
- Name an owner for each queue and agree on accuracy targets.

### Build (two-week sprints)

- **Sprint 1:** the supplier portal and checklist, with extraction in shadow mode. Procurement checks documents the old way and compares.
- **Sprint 2:** cross-checks, duplicate detection and the review queue.
- **Sprint 3:** screening and tax ID integrations, the bank call-back task, and quality approval.
- **Sprint 4:** vendor record drafts and expiration tracking.
- Move suppliers to the portal one category at a time, once each meets its targets.

### Run

- Report weekly on time to onboard, flagged documents, audit results and stalled suppliers.
- Review expired documents and requirement changes monthly with the process owner.
- Re-run the test set after any model, prompt or checklist change.

### Reference architecture

- **Intake:** a supplier portal on Vercel. Uploads are stored in R2, and Queues pass each new document on for processing.
- **Extraction:** Workers AI or another model provider, through AI Gateway so every request is logged.
- **Rules and orchestration:** Workflows run each onboarding from request to activation, including durable waits while the supplier responds and steps that wait for approval.
- **Human review queue:** a review app behind Cloudflare Access, with sensitive fields masked by role.
- **System-of-record write-back:** a Worker that drafts vendor records in the ERP through its API, over Tailscale for on-premises systems.
- **State and documents:** D1 for checklist status, expiration dates and audit records; R2 for documents.
- **Observability:** Logpush or Log Explorer for decision logs, with reports built from the audit records.

**Integration points:** ERP vendor master · procurement system · screening service · tax ID verification · quality management system · contract management · email.

## How to know it is working

- **Time to onboard:** request to active vendor record, median and slowest.
- **First-pass completeness:** the share of packets complete on first submission.
- **Accuracy on a sampled audit:** the share of checked documents a reviewer confirms are correct.
- **Touch time per supplier:** staff minutes per new supplier.
- **Expired documents on active suppliers:** a point-in-time count. It should fall and stay low.
- **Bank changes verified by call-back:** should be all of them. Any miss is an incident.

Review these weekly during Build, and monthly with the process owner.

## Getting started checklist

- [ ] Name the process owner and one person each from procurement, accounts payable and quality.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Audit a sample of active vendor files for missing and expired documents.
- [ ] Write the checklist and requirements for each supplier type.
- [ ] Confirm with counsel which sanctions lists you screen against.
- [ ] Write down who can approve suppliers and bank details.
- [ ] Gather a test set of past supplier packets.
- [ ] Pick the first supplier category for the portal.

## Related playbooks

- [FS-03 · Customer onboarding and KYC](../fs-03/): the same pattern of documents checked against policy, with gaps flagged for a reviewer.
- [MD-03 · Inventory and demand planning](../md-03/): clean supplier records make lead times and order confirmations reliable.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
