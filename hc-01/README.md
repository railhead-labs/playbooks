# HC-01 · Prior authorization

> Payer requests drafted from clinical notes. A person approves each one.

**Industry:** Healthcare and life sciences · **Typical owner:** Director of patient access or prior authorization manager · **Reading time:** 8 min

## Who this is for

Health systems, large physician groups, specialty practices and infusion centers that file a steady volume of prior authorization requests. The pain sits with coordinators and nurses who read charts, fill payer forms and wait on hold. This playbook fits if procedures get rescheduled because an authorization was not ready, if coordinators keep personal spreadsheets of payer rules, or if "no authorization" denials appear in your reports every month.

## How it runs today

1. A provider signs an order in the EHR: imaging, surgery, an infusion, a specialty drug.
2. A coordinator checks whether the payer requires authorization, using a payer website, a binder, a spreadsheet or memory.
3. The coordinator reads the chart for what the payer asks: diagnosis, treatments already tried, results, dates, findings.
4. If something is missing, the coordinator messages the ordering provider's office and waits. Many requests stall here.
5. The coordinator retypes the facts into a payer portal or fax form and attaches notes. Every payer has its own form and login.
6. The request waits. The coordinator checks status by portal or phone. A request for more information restarts steps 3 to 5.
7. Approvals are recorded in the EHR or scheduling system by hand. Denials go to the ordering provider, who decides on a peer-to-peer review or an appeal.
8. The authorization number, units and dates are copied into billing so the claim matches.

Where the hours go: reading and retyping. A coordinator reads long notes to find three or four facts, then types them into a portal. Next comes chasing: missing notes, status checks, and rework when a payer asks for documents already in the chart. Little time goes to the real judgment of whether the clinical picture meets the criteria.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Check whether authorization is required | | | | |
| Read the chart and gather facts | | | | |
| Request missing documentation | | | | |
| Enter and submit the request | | | | |
| Status checks and follow-up | | | | |
| Respond to requests for more information | | | | |
| Record the decision in each system | | | | |
| **Example:** Read the chart and gather facts | PA coordinator | 120 | 20 | 40 |

The example row is illustrative. Hours per week is volume times minutes, divided by 60.

To collect the numbers in one week:

- Pull request counts by payer and service line from your EHR work queue or tracking sheet.
- Sample a few dozen requests across your top payers. Coordinators note start and stop times per step on a simple form.
- Pull timestamps: order signed, request submitted, decision received, date of service. The gaps are waiting time.
- Count last quarter's reschedules and denials caused by missing or mismatched authorizations.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Detect need | Checks each order against a payer rule table (payer, plan, service, site of care) | Coordinator owns and updates the table | Clear match: proceed. No match or conflict: coordinator decides |
| 2. Gather facts | Pulls the facts the payer form needs, each linked to its source note | Coordinator checks highlighted fields | Fields without a source or below threshold are highlighted |
| 3. Check criteria | Lists each item on the payer's published criteria as met, not met or unclear | Nurse reviewer reads gaps and decides next step | All met with sources: coordinator lane. Any gap: nurse lane |
| 4. Request missing items | Drafts a specific request to the ordering provider | Coordinator edits and sends it | Always sent by a person |
| 5. Draft submission | Fills the form or electronic request, with a summary built only from chart facts | Coordinator or nurse reads the full draft and approves | No submission without a named approver, at any confidence |
| 6. Submit and track | After approval, submits through the approved channel and tracks due dates | Coordinator handles calls and portals the system does not reach | Payer questions and overdue cases return to the case owner |
| 7. Record outcome | Extracts authorization number, units and dates | Coordinator confirms before write-back | Approval differs from order: flag coordinator and scheduler |
| 8. Denial | Summarizes the reason next to relevant record facts | Ordering provider decides on peer-to-peer or appeal | Always a clinician's decision |

Confidence decides which queue a case lands in and how much the reviewer must read. It never decides whether a person approves. A case where every fact has a source and every criterion is met goes to a coordinator. A case with a gap goes to a nurse, gap listed first. A case the system cannot handle (a poor scan, an unknown payer or service) goes to the manual queue, the path you run today.

Start conservative. Route every case to the nurse lane at first. Move a payer and service pair to the coordinator lane only after sampled accuracy holds for several weeks.

## What stays with people

- **Whether documentation supports the request.** A licensed nurse or the ordering provider decides. The system lists what it found; it does not judge medical necessity.
- **Approving every submission.** One named person per request, recorded.
- **Peer-to-peer reviews and appeals.** Clinical arguments belong to clinicians. [HC-02](../hc-02/) covers appeal drafting.
- **Patient conversations.** A delay or denial should come from a person who can answer questions and reschedule.
- **Payer relationships** and policy disputes.
- **The payer rule table.** Coordinators know which payer changed policy last month.

## Controls and risks

- **Accuracy targets.** Agree targets with your clinical lead before launch for field accuracy and draft acceptance (approved without material edits). Measure both on a random weekly sample reviewed by someone other than the approver, reported by payer and service.
- **No invented facts.** Drafts state only facts found in the record, each linked to its source. A grounding check rejects unsourced statements. The system never adds a diagnosis, changes a code or suggests documentation the provider did not write.
- **Audit trail.** Log each draft, edit, approver, timestamp, source document, model and prompt version, and what went to the payer.
- **Fallback.** If the system is down, quality drops or a payer changes its form, cases route to the manual queue.
- **Minimum necessary access.** The system reads only the chart sections a request needs, with its own scoped, read-only service identity. Reviewers see what their EHR role allows. <!-- VERIFY: how the HIPAA minimum necessary standard applies to this workflow, including disclosures to payers for prior authorization. -->
- **Business associate agreements.** Every vendor that stores, processes or transmits PHI here needs a signed BAA first: model providers, cloud services, fax, clearinghouse and portal vendors. Confirm which products each BAA covers; coverage often differs by product and plan. <!-- VERIFY: BAA requirement for vendors that create, receive, maintain or transmit PHI on your behalf, and the product scope of each vendor's BAA. -->
- **No PHI to services that aren't covered.** Route all model calls through one gateway with an allow list of covered endpoints. Turn off response caching for PHI traffic, and turn off prompt logging or keep it in covered storage. Log case IDs, not PHI. Test with de-identified or synthetic charts. <!-- VERIFY: the de-identification method used for test data meets HIPAA de-identification standards. -->
- **Payer channels and rules.** Use the electronic channels each payer offers. Don't automate portal logins unless the payer's terms allow it. Federal and state rules on prior authorization exchange and payer response times have been changing; track which apply to your payers and states. <!-- VERIFY: current federal and state prior authorization requirements (electronic exchange, payer decision timeframes, state "gold card" or similar laws) that apply to your payers and states. -->
- **Change control.** Models, prompts, the rule table and checklists are versioned. Each change is tested on past cases with known outcomes and signed off by the process owner.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Walk through about 20 recent requests with coordinators and a nurse, order to decision. Note every system, handoff and wait.
- Fill the baseline worksheet. Pick one payer and service line to start, such as imaging for your largest commercial payer.
- Turn that payer's published criteria into a checklist your nurse reviewer signs off.
- Inventory where PHI goes and which vendors have BAAs. Bring in your privacy officer now.

### Redesign

- Write the lane rules: what goes to the nurse lane, what goes to manual.
- Choose each payer's channel: electronic transaction, payer API, portal entry by a person, or fax.

### Build (two-week sprints)

- **Sprint 1:** scoped, read-only EHR connection, rule table, need detection in shadow mode. Nobody acts on output yet.
- **Sprint 2:** fact extraction with source links and the review queue. Coordinators mark errors against their own work.
- **Sprint 3:** criteria checklist, grounding check, drafts approved and sent through the existing channel.
- **Sprint 4:** status tracking and confirmed write-back. Add a second payer only after the first holds its targets.
- The old path stays open. Any coordinator can send a case to manual with one click.

### Run

- Weekly sampled audit for the first months, then at a cadence the process owner sets.
- Monthly review with the process owner: accuracy, lane mix, cycle time, overrides, payer changes.
- Read every case with a material edit. They show where the design is weak.

### Reference architecture

Every component that touches PHI runs under a BAA covering that specific product.

- **Intake:** EHR order events through your interface engine over a Tailscale link; faxes from a BAA-covered fax service to a Worker; documents in R2.
- **Orchestration:** Workflows run each case as durable steps that can pause while waiting on a provider or payer. Queues between steps.
- **Extraction and drafting:** model calls through AI Gateway, only to BAA-covered endpoints (Workers AI or an external provider).
- **Rules and state:** rule table, checklists and case state in D1.
- **Human review queue:** review app behind Cloudflare Access, signed in through your identity provider.
- **Write-back:** authorization details to the EHR and billing system after a coordinator confirms.
- **Observability:** append-only audit table; Logpush to your SIEM or R2; Log Explorer for investigations.

**Integration points:** EHR, interface engine (HL7 v2 or FHIR), billing system, scheduling, payer portals and electronic prior authorization channels, clearinghouse, fax service, identity provider.

## How to know it is working

- **Time to submission:** hours from order signed to request submitted (median and slowest tenth).
- **First-pass approval rate:** share approved without a request for more information.
- **Draft acceptance rate:** share of sampled drafts approved without material edits.
- **Field accuracy:** share of sampled fields that match the chart.
- **Authorization-related denials:** claims denied for missing or mismatched authorization.
- **Manual lane share:** cases falling back to manual, by payer. A rise usually means a form or policy changed.

Review weekly with the authorization supervisor at first, then monthly with the process owner.

## Getting started checklist

- [ ] Pick one payer and one service line.
- [ ] Fill the baseline worksheet for one week.
- [ ] Turn that payer's criteria into a nurse-approved checklist.
- [ ] Confirm BAA status and product scope for every vendor that would touch PHI.
- [ ] Build a de-identified test set of past cases with known outcomes.
- [ ] Name the submission approver role and the weekly audit owner.
- [ ] Agree accuracy targets with your clinical lead before any draft is used.

## Related playbooks

- [HC-03 · Intake and referrals](../hc-03/): most authorization work starts with a faxed referral.
- [HC-02 · Revenue cycle and denials](../hc-02/): authorization denials sorted by cause, with appeals drafted from the record.
- [AG-02 · Agent identity and access](../ag-02/): one identity per agent and scoped access to the EHR.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
