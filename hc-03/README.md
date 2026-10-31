# HC-03 · Intake and referrals

> Faxed and emailed referrals turned into structured, routed work.

**Industry:** Healthcare and life sciences · **Typical owner:** Patient access or intake manager · **Reading time:** 8 min

## Who this is for

Specialty groups, health system specialty clinics, imaging centers, home health, hospice, post-acute and equipment suppliers that receive referrals by fax and email from many outside offices. The pain sits with intake coordinators, schedulers and the nurses who triage. This playbook fits if your fax inbox has a backlog, if referring offices call to ask whether you got their referral, or if nobody can say how many referrals never became appointments.

## How it runs today

1. Referrals arrive by fax, e-fax inbox, email, phone, EHR referral messages and portals. Faxes often bundle several patients or mix referrals with unrelated records.
2. A coordinator opens each one and works out who the patient is, who sent it, what service is requested and how urgent it is.
3. The coordinator searches the EHR for the patient, creates or updates the registration, and retypes demographics and insurance.
4. The coordinator checks completeness: orders, notes, results, insurance card, signatures. Missing items mean a fax back to the referring office, and a wait.
5. Someone verifies eligibility and works out whether the service needs prior authorization.
6. A nurse or provider reviews the referral for clinical urgency and fit.
7. A scheduler calls the patient, books the visit and lets the referring office know.

Where the hours go: reading faxes and retyping what they say. Then chasing: missing records, phone tag with patients, status calls from referring offices. Referrals also get lost. A fax filed to the wrong queue or parked waiting for one missing page can sit for days, and nothing tells anyone it is aging.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Sort incoming faxes and email | | | | |
| Identify and match or register the patient | | | | |
| Retype referral details | | | | |
| Check completeness and request missing items | | | | |
| Verify eligibility | | | | |
| Clinical triage | | | | |
| Schedule and notify the referring office | | | | |
| **Example:** Retype referral details | Intake coordinator | 300 | 6 | 30 |

The example row is illustrative. Hours per week is volume times minutes, divided by 60.

To collect the numbers in one week:

- Pull page and document counts from your fax server or e-fax service logs, by day.
- Time a sample of a few dozen referrals through each step, using a simple form at each desk.
- Measure aging from timestamps: received, registered, complete, scheduled. Count referrals with no appointment after a set number of days.
- Ask coordinators which referring offices send incomplete referrals most often, and which document types confuse the queue.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Capture and sort | Pulls every channel into one queue; classifies each document (referral, records, results, misdirected); splits multi-patient faxes | Coordinator sorts anything unclassified | Below threshold or unknown type: coordinator. Every page is accounted for daily |
| 2. Extract | Pulls patient, insurance, referring provider, diagnosis, service and urgency notes, each highlighted on the page | Coordinator checks highlighted fields | Passes format checks (ID formats, provider found in the NPI registry): shown as ready. Otherwise highlighted |
| 3. Match patient | Proposes a match to an existing record with the identifiers that agree and disagree | Coordinator confirms every match or registers a new patient | Never links or merges records without a person |
| 4. Check completeness | Compares contents with a checklist for the requested service; drafts a request to the referring office for missing items | Coordinator approves and sends the request | Always sent by a person, to a verified fax number or secure address |
| 5. Coverage | Triggers an eligibility check and flags services that may need authorization | Coordinator resolves coverage problems | Authorization needed: hand off to [HC-01](../hc-01/) |
| 6. Clinical triage | Flags urgency language and abnormal results it finds, quoted from the page | Nurse or provider decides urgency and whether to accept | Any urgency flag goes to clinical review at once. The system can raise priority, never lower it |
| 7. Schedule and close the loop | Proposes slots that fit provider rules; drafts the acknowledgment to the referring office | Scheduler books with the patient and sends the acknowledgment | Always a person contacts the patient |

The routing rule is lopsided on purpose. Confidence decides how much a coordinator needs to check on a field. Urgency works differently: any sign of urgency, at any confidence, sends the referral straight to a nurse. The system can move a referral up; only a clinician can move one down.

Patient matching is the other hard line. A wrong match puts one patient's records in another patient's chart. The system shows which identifiers agree and which don't, and a coordinator makes every match.

## What stays with people

- **Clinical triage and acceptance.** A nurse or provider decides urgency and whether the referral fits your service.
- **Patient identity.** Coordinators confirm every match. Merges follow your health information management process.
- **Declining a referral,** and how to tell the referring office and the patient.
- **Patient calls.** Scheduling and explaining next steps is a conversation, not a form.
- **Sensitive records and privacy questions.** Misdirected faxes and specially protected records go to trained staff and your privacy officer.
- **Relationships with referring offices.** Coordinators know which offices need a call instead of a fax.

## Controls and risks

- **Accuracy targets.** Agree targets for field accuracy and classification accuracy before launch. Check a random weekly sample against the source pages.
- **Urgent-miss check.** Each week a nurse reviews a sample of referrals the system did not flag as urgent. Any miss is investigated and the flag rules updated.
- **Nothing gets dropped.** A daily count reconciles pages received with pages filed. Any gap is investigated the same day.
- **Audit trail.** Log each classification, extraction, match decision, outbound request, approver, timestamp, and model and prompt version.
- **Fallback.** The raw fax and email queues stay visible. If the system is down, coordinators work them as they do today.
- **Minimum necessary access.** The system reads only incoming documents and the registration fields it needs to match, using its own scoped service identity. Reviewers see what their role allows.
- **Specially protected records.** Some records carry extra legal protection, such as substance use disorder treatment records under federal rules (often called Part 2) and categories that state laws protect. Route them to a restricted queue with tighter access, as your privacy officer directs.
- **Misdirected faxes.** A fax meant for another provider is routed to your privacy officer, who decides how to handle it under your policy.
- **Business associate agreements.** Every vendor that stores, processes or transmits PHI here needs a signed BAA first: fax and e-fax services, model providers, cloud services and eligibility vendors. Confirm which products each BAA covers.
- **No PHI to services that aren't covered.** Route model calls through one gateway with an allow list of covered endpoints. Turn off response caching for PHI traffic, and turn off prompt logging or keep it in covered storage. Log document IDs, not PHI. Test with de-identified or synthetic faxes.
- **Change control.** Models, prompts, classification rules and service checklists are versioned. Each change is tested on a labeled set of past documents and signed off by the process owner. Clinical leads approve checklist and urgency-rule changes.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Sit with intake for a day. Follow about 30 referrals from fax to appointment. Note every system, retype and wait.
- Fill the baseline worksheet and the aging numbers.
- List your referral types by service. For the top few, write a completeness checklist with your clinical lead.
- Write down the urgency language your nurses watch for.
- Inventory channels, vendors and BAAs. Bring in your privacy officer now.

### Redesign

- Pick one service line with high volume and clear checklists to start.
- Write the lane rules, the urgency escalation path and the patient-matching rules with your health information management team.
- Decide the secure channels for outbound requests: verified fax numbers, Direct secure messaging or a portal.

### Build (two-week sprints)

- **Sprint 1:** all channels into one queue, classification and page reconciliation in shadow mode.
- **Sprint 2:** extraction and match proposals in a review screen. Coordinators confirm and mark errors.
- **Sprint 3:** completeness checks, drafted outbound requests and urgency flags routed to nurses.
- **Sprint 4:** eligibility trigger, authorization handoff, scheduling proposals and referral status.
- The old inboxes stay open throughout. Any coordinator can work a referral by hand.

### Run

- Weekly sampled audit and urgent-miss check for the first months, then at a cadence the process owner sets.
- Monthly review with the process owner: accuracy, aging, unscheduled referrals, urgent flags, referring offices with repeat gaps.
- Share completeness feedback with your top referring offices. Fewer gaps upstream means less chasing.

### Reference architecture

Every component that touches PHI runs under a BAA covering that specific product.

- **Intake:** a BAA-covered fax service delivers documents to a Worker; a secure mailbox for email; EHR referral messages through your interface engine over a Tailscale link. Documents in R2.
- **Classification and extraction:** model calls through AI Gateway, only to BAA-covered endpoints.
- **Rules and state:** checklists, urgency rules and referral state in D1.
- **Orchestration:** Workflows hold each referral as durable steps, including waits for missing items with reminders. Queues between steps.
- **Human review queue:** review app behind Cloudflare Access, signed in through your identity provider.
- **Write-back:** confirmed registrations and referral records to the EHR; appointments in the scheduling system.
- **Observability:** append-only audit table; daily page reconciliation report; Logpush to your SIEM or R2; Log Explorer.

**Integration points:** EHR (registration, referrals, documents), interface engine, fax or e-fax service, secure email or Direct messaging, eligibility through your clearinghouse, scheduling, referral management or CRM, NPI registry.

## How to know it is working

- **Time to registered:** hours from receipt to a registered, complete referral.
- **Time to scheduled:** days from receipt to a booked appointment.
- **Complete at first touch:** share of referrals that need no request for missing items.
- **Unscheduled referral rate:** share with no appointment after a set number of days.
- **Field accuracy:** share of sampled fields that match the source page.
- **Urgent-miss rate:** urgent referrals the system did not flag, found in the weekly nurse sample.

Review weekly with the intake supervisor at first, then monthly with the process owner.

## Getting started checklist

- [ ] Pull one week of fax and email volume by day.
- [ ] Fill the baseline worksheet and measure referral aging.
- [ ] Pick one service line to start.
- [ ] Write its completeness checklist and urgency language with your clinical lead.
- [ ] Agree patient-matching rules with health information management.
- [ ] Confirm BAA status and product scope for your fax service and every other vendor that would touch PHI.
- [ ] Ask your privacy officer how to handle misdirected faxes and protected record types.
- [ ] Name the weekly audit owner and the nurse for the urgent-miss check.

## Related playbooks

- [HC-01 · Prior authorization](../hc-01/): referrals that need authorization hand off here.
- [HC-02 · Revenue cycle and denials](../hc-02/): registration errors at intake show up later as denials.
- [FS-01 · Claims intake](../fs-01/): the same read, extract and route-by-confidence pattern for insurance claims.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
