# AG-03 · Quarterly agent access review

> A review your risk committee can sign off in one sitting.

**Industry:** Agentic AI governance · **Typical owner:** CISO, with the governance, risk and compliance (GRC) lead · **Reading time:** 9 min

## Who this is for

Companies whose risk committee, audit committee or board now asks about AI agents, and whose security or GRC team already runs access reviews for people. The pain is a review that takes weeks to assemble, attestations nobody reads, and a meeting that ends with "let's revisit next quarter." If agents aren't in your access review at all, or appear as one line called "service accounts," this playbook fits. It works best once you have an inventory ([AG-01](../ag-01/)) and per-agent identities ([AG-02](../ag-02/)), but you can start without them.

## How it runs today

1. Weeks before the committee meets, a GRC analyst exports user and service account lists from the identity provider, cloud consoles and major SaaS apps.
2. Spreadsheets go to managers by email: "Is this access still needed?" Agents mostly aren't on them, because they don't look like people.
3. Managers approve everything to clear the request, or don't answer. The analyst chases.
4. Service accounts and API keys get reviewed as one block, often by the team that created them.
5. Revocations are requested by ticket. Nobody checks that they happened.
6. Exceptions are granted in email threads with no expiry date.
7. The committee gets a deck of counts. Members can't see what changed or which risks need a decision. Questions go unanswered, and sign-off slips.

The hours go into assembling evidence from many consoles, chasing attestations, reconciling lists that disagree, and proving after the fact that revocations happened.

## Measure your own baseline

Use your last review cycle. Hours per week = volume per week × minutes each ÷ 60. Because the work is quarterly, total each step's hours for the cycle and divide by 13 for the weekly column.

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Export and merge access lists | | | | |
| Send and chase attestations | | | | |
| Request and confirm revocations | | | | |
| Track and renew exceptions | | | | |
| Build the committee deck | | | | |
| Answer committee follow-up questions | | | | |
| **Example:** Chase managers for attestations | GRC analyst | 25 reminders | 6 | 2.5 |

To collect the numbers in one week, ask the analyst who ran the last cycle to walk through it step by step. Pull timestamps from the email threads and tickets: when exports started, when the last attestation came in, when each revocation closed. Count the reminders sent.

Also record: how many agents were in the last review, the share of attestations returned on time, how many revocations were confirmed, how many exceptions have no expiry, and whether the committee signed off at the first meeting.

## The redesigned process

The review runs on a fixed four-week calendar each quarter. Week 1: snapshot and flags. Weeks 2-3: owner attestations. Week 4: revocations, exceptions and the evidence pack. The committee meets after week 4.

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Snapshot | Pulls the inventory, identities, grants, last-used dates, spend per agent, tool calls, policy changes, drill results and incidents as of a fixed date. | GRC lead checks counts against each source and signs off the snapshot. | A source that doesn't reconcile blocks the cycle until fixed. |
| 2. Flag | Flags grants unused for 90 days, departed owners, personal or shared credentials, scopes that grew, new agents, expired exceptions and spend jumps. Drafts one packet per owner. | Security reviews flags on Tier 1 agents before packets go out. | Tier 1: security reviews every flag. Tiers 2 and 3: flags go straight to owners. |
| 3. Attest | Pre-fills each packet with a recommendation per grant (keep, reduce, remove) and the evidence behind it. | Owner decides each grant and attests that the purpose still holds. | No attestation by the deadline: escalate to the owner's manager. Still none a week later: the security lead decides whether to suspend. |
| 4. Revoke | Re-checks the source system after each removal and attaches proof that access is gone. | Platform admin runs approved removals. GRC confirms the proof. | A removal without proof stays open and appears in the pack. |
| 5. Exceptions | Drafts the exception register: reason, compensating control, owner, approver and expiry. Flags renewals. | Risk owner approves or denies each one. Nobody approves their own. | Every exception has an expiry date. Renewal needs a fresh decision, never a rollover. |
| 6. Draft the pack | Drafts the summary text from the snapshot and the decisions. | GRC lead edits, checks every figure and owns the pack. | Every number comes from a saved query. A figure the lead can't trace comes out. |
| 7. Sign off | None. | The committee decides the open items. The chair signs or sends specific items back. | Items sent back get an owner and a date before the meeting ends. |

Routing here decides what reaches the committee. Items that are attested, unchanged and low tier appear as counts. Changes, removals and exceptions appear line by line. Anything Tier 1, any exception renewal and any revocation without proof gets its own row with a recommended decision.

That is how a committee finishes in one sitting. Members decide the handful of items that need a decision and see evidence that the rest were handled. The AI drafts and flags. People attest, approve, revoke and sign.

## What stays with people

- **Attestation.** Only the owner can say an agent still needs its access. AI pre-fills the packet. It never attests.
- **Exceptions.** A named risk owner accepts each one, with its expiry date in front of them.
- **Suspensions** of agents whose owners don't respond.
- **Risk appetite.** The committee decides which agent actions need a person to approve every time. Security writes that into policy and [AG-02](../ag-02/) enforces it.
- **Sign-off.** The chair signs, and the record shows who attended and what was sent back.
- **Vendor follow-up** on copilot settings and logging that the snapshot can't see.

## Controls and risks

- **Accuracy target.** Each cycle, check a sample of flagged and unflagged grants against the source systems. Report missed flags in the pack, and set a target for them.
- **Numbers are queries.** Every figure in the pack comes from a saved query over the frozen snapshot. The model drafts words, not numbers.
- **Segregation of duties.** Owners don't approve their own exceptions. Whoever runs a revocation doesn't confirm its proof.
- **Evidence retention.** Keep snapshots, packets, attestations and proofs in write-once storage where you can, for the period your auditors require.
- **Data handling.** The snapshot lists where every credential lives. Limit access to the review team and log every read.
- **Fallback.** If the pipeline fails, run the cycle by hand with the same packet template. The calendar doesn't move.
- **Model and prompt change control.** Prompts and model versions used for flags and drafting are versioned. Test changes against last cycle's snapshot before use.
- **Frameworks.** If you use the NIST AI Risk Management Framework, this review supports its Govern and Manage functions. If you are working toward ISO/IEC 42001, the evidence pack can serve as a record for monitoring and management review. If your auditors already test periodic user access reviews as part of IT general controls, ask whether agent identities belong in that scope.
- This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.

## How to build it

### Map (week 1-2)
- Walk through last quarter's access review with the GRC analyst: every export, email, ticket and meeting, with the hours each took.
- Ask the committee chair what they need in order to sign: decisions, evidence, format and length.
- Ask your internal or external auditors what evidence they will test.
- Pull the agent inventory from AG-01 and grant records from AG-02, or the best lists you have.

### Redesign
- Fix the calendar and the snapshot date for each quarter.
- Write the owner packet: one page per agent, one line per grant, keep, reduce or remove.
- Write the exception policy: who can approve, the longest allowed expiry, and what counts as a compensating control.
- Set the escalation path and the suspension rule for owners who don't respond.
- Agree the evidence pack outline with the chair before you build it:
  1. One-page summary: what changed, decisions needed, open risks.
  2. Inventory changes: agents added, retired and retiered.
  3. Attestation status by owner and tier.
  4. Revocations, each with proof.
  5. Exception register, sorted by expiry date.
  6. Revocation drill results from AG-02.
  7. Metric trends for the last four quarters.
  8. Sign-off page with names, date and items sent back.

### Build (two-week sprints)
- **Sprint 1:** snapshot job and evidence store. Reconcile counts against every source.
- **Sprint 2:** flags, owner packets and the attestation flow with reminders and escalation.
- **Sprint 3:** revocation proof checks, the exception register and the evidence pack draft.
- Run the first quarter alongside your existing review. The old review stays the record until the committee accepts the new pack.

### Run
- Quarterly cycle on the fixed calendar.
- Monthly check of exceptions nearing expiry.
- After each cycle, a short retrospective with the process owner: what slowed down and which flags were wrong.

### Reference architecture
- **Intake:** a scheduled Worker (Cron Triggers) starts a Workflows run that pulls the D1 inventory from AG-01, logs that Logpush delivered to R2, and grants from source system APIs.
- **Flags and drafting:** rules in Worker code compute the flags. Workers AI drafts packet recommendations and summary text, with calls logged through AI Gateway.
- **Human review:** attestation and approval forms behind Cloudflare Access. Workflows sends packets, waits for answers, reminds and escalates.
- **Write-back:** after approval, Workers call the identity provider and Access APIs to remove access, then re-query to capture proof.
- **Evidence store:** R2 holds snapshots, packets, attestations and proofs, with retention rules set to your policy.
- **Observability:** cycle progress by owner, overdue attestations and open revocations on one page for the GRC lead.

**Integration points:** identity provider, HR system, ticketing system, GRC tool, SIEM, model provider admin consoles, code host, cloud providers, SaaS admin consoles.

## How to know it is working

- **On-time attestation:** share of packets attested by the deadline.
- **Verified revocations:** removals with proof divided by removals approved.
- **Overdue exceptions:** exceptions past expiry with no decision. The target is zero.
- **Unused access removed:** grants removed because they went unused.
- **Cycle time:** days from snapshot to committee sign-off.
- **First-meeting sign-off:** whether the committee signed without deferring.

The committee reviews these each quarter. The process owner checks attestation and revocation progress weekly during the cycle.

## Getting started checklist

- [ ] Ask the committee chair what a signable review looks like.
- [ ] Set next quarter's snapshot date and four-week calendar.
- [ ] Confirm every agent in your inventory has a named owner.
- [ ] Draft the one-page owner packet and test it with two owners.
- [ ] Write the exception policy with a maximum expiry.
- [ ] List every open exception and give each an expiry date.
- [ ] Pull last quarter's values for the metrics above.
- [ ] Agree the evidence pack outline with the chair.

## Related playbooks

- [AG-01 · Agent inventory](../ag-01/): the list of agents, owners and credentials this review starts from.
- [AG-02 · Agent identity and access](../ag-02/): per-agent identities, scoped grants and the revocation drills the pack reports.
- [SO-03 · Log pipeline and detections](../so-03/): the log store that supplies last-used dates and activity evidence.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
