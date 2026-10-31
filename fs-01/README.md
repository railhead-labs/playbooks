# FS-01 · Claims intake

> Claim documents read, facts pulled out, and each claim routed by confidence.

**Industry:** Financial services and insurance · **Typical owner:** Claims operations manager · **Reading time:** 9 min

## Who this is for

Property and casualty carriers, MGAs and third-party administrators that take first notice of loss (FNOL) through several channels. The pain sits with intake teams and adjusters, who spend each claim's first days reading, keying and chasing. This playbook fits if new claims sit in a shared inbox before anyone sets them up, if adjusters re-read what intake already read, or if your backlog jumps after every storm.

## How it runs today

1. A loss arrives by email, web form, phone, agent, broker or TPA feed, with photos, police reports, estimates, bills or demand letters.
2. An intake specialist opens each item and works out which policy and which claim it belongs to, new or existing.
3. The specialist looks up the policy and keys the FNOL into the claims system field by field.
4. Missing information means an email or call to the insured, agent or broker. The claim waits.
5. A supervisor or assignment rules route the claim to an adjuster. Some get flagged for the special investigation unit (SIU), subrogation or large loss, from a checklist and experience.
6. An acknowledgment goes out, often from a template filled in by hand.
7. The adjuster re-reads the documents, works through coverage questions, sets reserves and makes first contact.

Where the hours go: reading and retyping. The specialist reads and types the facts; the adjuster reads them again. Chasing documents adds days of waiting. Matching follow-up mail to open claims is a quiet time sink, because correspondence rarely carries a clean claim number. In a surge, the inbox becomes the queue.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Sort incoming mail and match it to claims | | | | |
| Look up the policy and key the FNOL | | | | |
| Request missing information | | | | |
| Assign and flag (SIU, subrogation, large loss) | | | | |
| Send acknowledgment | | | | |
| Adjuster re-read on first touch | | | | |
| **Example (illustrative values):** Key the FNOL | Intake specialist | 300 | 15 | 75 |

Hours per week = volume × minutes ÷ 60. In the example, 300 × 15 ÷ 60 = 75. Multiply by a loaded hourly cost to get dollars.

Collect the numbers in one week:

- **Sample the work.** Pull a few dozen recent claims across channels. Time each step on a handful.
- **Ask the people doing it.** Sit with two specialists and an adjuster. Ask what they re-check, chase and dread.
- **Pull system timestamps.** Compare email received, claim created, assigned and first contact. The gaps are waiting time.

Also record today's error rate (wrong policy, wrong date of loss, wrong team). You need it to judge the new process fairly.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Receive | Captures every channel into one queue. Stores originals. Splits multi-document packets. | Owns the channel list. | Unreadable files go to the intake queue. |
| 2. Classify and match | Labels each document (FNOL, estimate, police report, medical bill, correspondence). Matches it to an open claim or marks it new. | Confirms uncertain matches. | Attach to an open claim only on an exact identifier and high confidence. |
| 3. Extract facts | Pulls insured, policy number, date and location of loss, cause, parties, injuries and a short summary, with the source line for each field. | Corrects flagged fields in a side-by-side view. | Per-field thresholds. Policy number and date of loss never pass below threshold. |
| 4. Validate | Checks the policy number against the policy system, checks the date of loss against policy periods, and looks for duplicates and prior claims. | Resolves mismatches. Handles anything that looks like a coverage question. | Any mismatch goes to a person. The system flags; it does not conclude. |
| 5. Find gaps | Lists missing documents for the claim type. Drafts the request. | Approves and sends drafted requests. | Fixed, approved templates may send automatically. Drafted text waits for a person. |
| 6. Flag and route | Suggests severity and flags (injury, litigation, possible large loss, subrogation, SIU indicators your SIU defined). Applies your assignment rules. | Supervisor reviews flagged claims. SIU decides whether a referral becomes an investigation. | Clean, low-severity claims go to the assigned adjuster. Flagged claims go to a supervisor first. |
| 7. Set up and acknowledge | Creates the claim in the claims system with facts and source links. Fills the approved acknowledgment template. | The adjuster owns the claim: coverage, reserves, contact, payment, denial. | The AI never sets reserves, confirms coverage or denies a claim. |

Routing works at two levels: a confidence score on each field, and rule checks against your systems on each claim. A claim goes straight through only when every required field clears its threshold, the policy matches, and no duplicate or flag turns up. Anything else stops at the failed step, with the reason shown. The reviewer fixes one field, not the whole claim.

Set thresholds from measured accuracy, not the model's own scores. Start with nothing straight-through. Run in shadow mode, compare output with what specialists keyed, and open the lane one claim type at a time as the numbers hold. Straight-through means a claim is set up and assigned without an intake touch. It never means a claim is decided.

## What stays with people

- **Coverage decisions.** Covered, excluded or reservation of rights is an adjuster's call. The system can surface the relevant endorsement. It does not interpret it.
- **Reserves and payments.** Adjusters set reserves and approve payments within their authority. Larger amounts follow your authority levels.
- **Denials.** A named adjuster or manager decides, signs and sends every denial.
- **Fraud referrals.** SIU decides whether to investigate. No claim is slowed, denied or treated differently on an AI flag alone.
- **Hard conversations.** Injuries, fatalities and total losses get a person on the phone.
- **The exceptions list.** Experienced specialists know which agents send partial packets. Keep them in design reviews.

## Controls and risks

- **Accuracy targets.** Set a target per field with the claims operations manager before go-live, stricter for policy number, date of loss and insured. Measure weekly on a random sample checked against source documents, plus every review correction.
- **Audit trail.** Record what arrived and when, what the AI extracted (with model and prompt version), every field a person changed, and who approved each outgoing message. Regulators review claim files in market conduct examinations, so the file must show what happened and when. <!-- VERIFY: claim file documentation and market conduct exam expectations in each state where you write business. -->
- **Timeliness rules.** Most states set requirements for acknowledging and responding to claims, many based on the NAIC model law on unfair claims settlement practices. Time limits vary by state and line, so build them into queue alerts by state. <!-- VERIFY: acknowledgment and response timeframes by state and line, and which states follow the NAIC model. -->
- **AI governance.** Many states have adopted the NAIC model bulletin on insurers' use of AI systems, which expects a written program, governance and testing. Some states have their own rules on algorithms and external data. Record what each model does, how it was tested and who approved it. <!-- VERIFY: which states have adopted the NAIC AI model bulletin or have separate AI or algorithm rules, and what they require. -->
- **Fraud handling.** Many states require an anti-fraud plan or SIU and reporting of suspected fraud. AI indicators feed that process; they don't replace it. <!-- VERIFY: state anti-fraud plan, SIU and fraud reporting requirements. -->
- **Failure modes and fallback.** Watch for misread policy numbers, mail on the wrong claim, and summaries that drop a key fact. If a model call or lookup fails, the item falls back to the existing intake queue. Keep the old path staffed until the new one proves out.
- **Data handling and access.** Claim files hold personal, financial and often medical information. Encrypt originals, restrict access by role, and use model providers that contractually do not train on your data. The Gramm-Leach-Bliley Act and state insurance data security laws may apply. <!-- VERIFY: applicable privacy and data security requirements, including state adoption of the NAIC Insurance Data Security Model Law and rules on medical information in claim files. -->
- **Change control.** Version every prompt, model and threshold. Test changes against past claims with known answers. The claims operations manager approves routing and threshold changes.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Trace 30 to 50 recent claims from arrival to first adjuster contact, across channels and your largest lines.
- List every handoff, wait and workaround with the people who do the work, with hours and cost per step.
- Inventory document types and required fields per claim type.
- With compliance, write down the timeliness and claim file rules in your states.

### Redesign

- Agree the field list, required documents per claim type, and review thresholds.
- Write routing rules with the claims operations manager and SIU.
- Name who confirms matches, who sends drafted requests and who owns the claim at each stage.
- Design the adjuster's first view: summary, facts with source links, gaps and flags.

### Build (two-week sprints)

- **Sprint 1:** the main FNOL mailbox through classification and extraction, in shadow mode. Nothing writes to the claims system.
- **Sprint 2:** the review screen and a report comparing AI output with what specialists keyed.
- **Sprint 3:** policy lookup, duplicate checks, gap lists and drafted requests.
- **Sprint 4:** write-back for one low-severity claim type, behind a switch you can turn off.
- **Later:** more channels and claim types, one at a time. The old path stays open.

### Run

- Weekly accuracy report by field and claim type.
- Monthly review with the claims operations manager: thresholds, routing, complaints, regulator questions. A named owner keeps prompts, thresholds and the test set.

### Reference architecture

- **Intake:** Email Routing with an Email Worker for the FNOL mailbox. A web FNOL form on Vercel posting to Workers endpoints behind WAF. Workers endpoints for TPA and broker feeds. Queues to absorb surges.
- **Storage:** R2 for original documents. D1 for intake records, extracted fields, review decisions and the audit log.
- **Extraction and drafting:** Workers AI models (or another provider) through AI Gateway, which logs calls and handles rate limits and fallback.
- **Rules and orchestration:** Workflows runs each item through classify, extract, validate, route and write-back as durable steps with retries.
- **Human review queue:** a review app behind Access, with roles for intake, supervisors and SIU.
- **Write-back:** Workers calling the claims system API. Tailscale when the claims or policy system runs on premises.
- **Observability:** Logpush to your SIEM, Log Explorer for investigations, accuracy reports from D1.

**Integration points:** policy administration, claims management, document management, email and telephony, agent and TPA feeds, SIU case management, and data services you already license.

## How to know it is working

- **Straight-through rate:** share of new claims set up and assigned with no intake touch, by claim type.
- **Field accuracy on sampled audit:** share of fields correct when a person checks a random sample against the source. It sets thresholds.
- **Exception rate:** share of claims stopped for review, grouped by reason.
- **Time to setup:** first notice to claim created and assigned, median and slowest tenth.
- **Adjuster rework rate:** share of claims where the adjuster corrects intake facts or reassigns.
- **Wrong-claim match rate:** documents attached to the wrong claim. Target zero; treat each as an incident.

Review weekly with the intake lead and monthly with the claims operations manager.

## Getting started checklist

- [ ] Name the process owner and an experienced intake specialist as design partner.
- [ ] List every intake channel and its share of volume.
- [ ] Pull a sample of recent claims with timestamps from receipt to first contact.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Write down the fields and documents each claim type needs.
- [ ] Ask compliance for the timeliness and claim file rules in your states.
- [ ] Agree which flags go to a supervisor and which go to SIU.
- [ ] Pick one channel and one low-severity claim type for the first shadow sprint.

## Related playbooks

- [FS-02 · Underwriting submissions](../fs-02/): the same reading and routing, applied to broker submissions.
- [HC-03 · Intake and referrals](../hc-03/): faxed and emailed packets turned into structured, routed work.
- [FS-04 · Reconciliation](../fs-04/): claim payments and recoveries matched back to the ledgers.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
