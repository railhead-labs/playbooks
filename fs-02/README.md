# FS-02 · Underwriting submissions

> Broker submissions sorted and summarized so underwriters start with the decision.

**Industry:** Financial services and insurance · **Typical owner:** Head of underwriting operations · **Reading time:** 9 min

## Who this is for

Commercial insurance carriers, MGAs and program administrators that receive broker submissions by email and portal. The pain sits with underwriting assistants who log and key every submission, and with underwriters who spend mornings reading attachments to learn whether a risk is even in appetite. This playbook fits if submissions sit unopened for days, if good risks expire in the queue behind ones you would decline, or if underwriters complain about re-keying application data.

## How it runs today

1. A broker emails or uploads a submission: ACORD and supplemental applications, loss runs, schedules, financials and a cover note.
2. An underwriting assistant saves the files and runs clearance: is this insured already on file, and has another broker submitted it?
3. The assistant keys the account into the submission or policy system: insured, address, class of business, exposures, coverages, limits, effective date, broker.
4. An underwriter or senior assistant reads the cover note to judge appetite and decide whether to work it.
5. Missing items (current loss runs, a signed application, a supplemental) go back to the broker. The submission waits.
6. The underwriter reads the full file, summarizes loss history, enters rating data, and refers anything above their authority.
7. The underwriter quotes, declines or asks for more.

Where the hours go: retyping application data. Reading loss runs in many layouts to answer simple questions: how many claims, how large, what is still open. Clearance searches against messy names. Chasing documents. Underwriters spend expert hours reading instead of judging risk and talking to brokers. And in a first-in, first-out queue, a clean risk with a near effective date can sit behind a stack of declines.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Log and clear submission | | | | |
| Key account and exposure data | | | | |
| Appetite triage | | | | |
| Request missing items | | | | |
| Read and summarize loss runs | | | | |
| Underwriter full review | | | | |
| **Example (illustrative values):** Read and summarize loss runs | Underwriter | 60 | 25 | 25 |

Hours per week = volume × minutes ÷ 60. In the example, 60 × 25 ÷ 60 = 25. Use a loaded hourly cost per role, because underwriter hours cost more than assistant hours.

Collect the numbers in one week:

- **Sample the work.** Pull a few dozen recent submissions across lines and sizes. Time each step on a handful.
- **Ask the people doing it.** Sit with two assistants and two underwriters. Ask what they re-key, chase, and open first.
- **Pull system timestamps.** Compare received, cleared, first underwriter touch, and quote or decline sent.

Also count declines the appetite guide would have caught early, and submissions that expire unworked.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| 1. Receive | Captures inbox and portal submissions into one queue. Stores originals. Identifies each document type. | Owns inbox and portal rules. | Unreadable or locked files go to the assistant queue. |
| 2. Clear | Normalizes insured name and address. Searches accounts and open submissions. Lists possible matches with reasons. | Assistant confirms matches. Underwriting manager resolves broker conflicts under your broker-of-record rules. | Exact identifier matches attach automatically. Any possible broker conflict goes to a person. |
| 3. Extract | Pulls account and exposure data from applications, schedules and spreadsheets into fields, with the source page for each. | Assistant corrects flagged fields. | Per-field thresholds. Rating fields (exposures, values, class) never pass below threshold. |
| 4. Screen | Sends named parties to your sanctions screening tool. Checks the submission against your written appetite guide. | Compliance clears possible sanctions matches. Underwriter reviews anything marked outside appetite. | A possible sanctions match stops the submission. "Outside appetite" is a flag, never an automatic decline. |
| 5. Find gaps | Compares the file with the required-document list for the line and size. Drafts the broker request. | Assistant approves and sends. | Standard template requests may send automatically if you choose. Drafted text waits. |
| 6. Summarize | Writes a one-page summary: operations, exposures, requested terms, a loss history table (counts, paid, open, largest) and open questions. Links every number to its source. | Underwriter reads the summary and checks decision-critical numbers against the source. | Low-confidence loss run reads are marked so the underwriter knows what to check. |
| 7. Prioritize | Orders the queue by rules your underwriting manager sets: effective date, completeness, appetite fit. | Manager owns and changes the rules. | The order is a suggestion. Underwriters can pull any submission. |
| 8. Decide | Drafts a quote cover note or decline note on request, from the underwriter's stated reasons. | Underwriter quotes, declines or asks for more, sets price and terms, refers above authority, and sends every response. | The AI never prices, quotes, binds or declines. |

Routing by confidence protects two things: the data going into rating and the underwriter's attention. Field confidence decides whether an assistant checks a value. Rule checks decide where the submission goes: compliance, the broker, or an underwriter's queue. A submission reaches the underwriter only when it is cleared, its key fields are checked and its gaps are listed. The underwriter starts at the decision, not the inbox.

Loss runs need extra care. Layouts vary by carrier, and a misread paid amount or a missed open claim changes the picture. Run loss run summaries in shadow mode first, compared with underwriters' own notes, before anyone relies on them. Keep the source page one click from every number.

## What stays with people

- **Risk selection.** Whether to write a risk is the underwriter's decision within their authority. Referrals follow your authority matrix.
- **Pricing and terms.** Rates, credits and debits, deductibles, exclusions and subjectivities.
- **Declines.** An underwriter decides and sends each decline, with the reason recorded.
- **Broker relationships.** Negotiation, feedback and the call that saves a renewal.
- **Clearance conflicts and sanctions matches.** The underwriting manager and compliance, respectively.
- **The appetite guide.** Underwriting leadership owns the written guide the system checks against. The AI does not infer appetite from past decisions, which could carry old patterns forward without anyone choosing them.

## Controls and risks

- **Accuracy targets.** Set per-field targets with the head of underwriting operations, stricter for rating fields. Measure loss run summaries separately: claim counts, totals and open claims. Audit a random sample weekly against source documents.
- **Audit trail.** Record each submission, extracted fields with sources, every correction, who cleared it, model and prompt versions, and who decided.
- **Unfair discrimination and filed rules.** State laws prohibit unfairly discriminatory underwriting, and admitted carriers often must file rating and underwriting rules with regulators. The AI should check only against criteria in your approved guidelines, and summaries should leave out characteristics you may not use.
- **AI governance.** Many states have adopted the NAIC model bulletin on insurers' use of AI systems, which covers AI used in underwriting as well as claims. Keep a written record of each model's purpose, testing and approval.
- **Sanctions.** US insurers must not provide coverage that violates OFAC sanctions. Screen named parties before quoting and binding.
- **Consumer reports.** If you use consumer reports in underwriting, more common in personal and small commercial lines, Fair Credit Reporting Act adverse action requirements may apply.
- **Failure modes and fallback.** Watch for wrong clearance matches, misread exposures flowing into rating, loss summaries that miss an open large claim, and priority rules that bury one broker's business. If any step fails, the submission lands in the assistant queue and the old process takes over.
- **Data handling and access.** Submissions carry insureds' financials and sometimes personal data on drivers or employees. Restrict access by role and team, keep retention rules, and use model providers that contractually do not train on your data.
- **Change control.** Version prompts, models, thresholds and appetite rules. Test changes against past submissions with known answers. The head of underwriting operations approves releases; the chief underwriting officer approves appetite guide changes.

*This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.*

## How to build it

### Map (week 1-2)

- Trace 30 to 50 recent submissions from receipt to quote or decline, across your main lines.
- List every handoff, wait and workaround with assistants and underwriters, with hours and cost per step.
- Collect the appetite guide, authority matrix and required-document lists. Note where practice differs.
- Gather loss run samples from the carriers you see most.

### Redesign

- Agree the field list per line and the review thresholds.
- Turn the appetite guide into explicit checks with underwriting leadership. Anything ambiguous stays a flag for the underwriter.
- Write prioritization rules with the underwriting manager.
- Design the one-page summary with two or three underwriters.

### Build (two-week sprints)

- **Sprint 1:** inbox intake, document typing and extraction for one line, in shadow mode.
- **Sprint 2:** clearance suggestions and the assistant review screen.
- **Sprint 3:** loss run summaries in shadow mode, compared with underwriter notes.
- **Sprint 4:** the summary page, gap requests, the prioritized queue, and write-back for one line behind a switch you can turn off.
- **Later:** more lines and the broker portal. The old inbox stays open until the new path proves out.

### Run

- Weekly accuracy report: fields, clearance matches and loss run summaries.
- Monthly review with the head of underwriting operations: thresholds, priority rules, broker feedback, late declines.
- Update the appetite checks whenever the guide changes.

### Reference architecture

- **Intake:** Email Routing with an Email Worker for the submission inbox. A broker upload portal on Vercel posting to Workers endpoints behind WAF. Queues to buffer volume.
- **Storage:** R2 for original files. D1 for submission records, extracted fields, clearance decisions and the audit log.
- **Extraction and summaries:** Workers AI models (or another provider) through AI Gateway for logging, rate limits and fallback. Fly.io for long-running jobs such as very large schedules.
- **Rules and orchestration:** Workflows runs receive, clear, extract, screen, summarize and route as durable steps. Appetite checks live in code underwriters can review.
- **Human review queue:** an underwriting workbench behind Access, with roles for assistants, underwriters, managers and compliance.
- **Write-back:** Workers calling the submission, policy and rating system APIs. Tailscale for systems on premises.
- **Observability:** Logpush to your SIEM, Log Explorer for investigations, accuracy reports from D1.

**Integration points:** submission and clearance system, policy administration, rating engine, document management, broker portal, sanctions screening tool, CRM, and third-party property or business data you already license.

## How to know it is working

- **Time to decision-ready:** receipt to a cleared, summarized submission in an underwriter's queue.
- **Quote turnaround:** receipt to quote or decline sent, by line.
- **Field accuracy on sampled audit:** share of fields correct against source, with rating fields reported separately.
- **Loss summary accuracy:** share of sampled summaries with correct counts, totals and open claims.
- **Late-decline rate:** share of declines made after a full review that the appetite checks could have caught.
- **Exception rate:** share of submissions needing assistant correction, by reason.

Review weekly with the underwriting operations lead and monthly with the head of underwriting operations.

## Getting started checklist

- [ ] Name the process owner and one underwriter and one assistant as design partners.
- [ ] Pull a sample of recent submissions with timestamps.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Get the current appetite guide and authority matrix, and mark what is out of date.
- [ ] List required documents per line and size.
- [ ] Collect loss run samples from your most common carriers.
- [ ] Confirm sanctions screening steps with compliance.
- [ ] Pick one line for the first shadow sprint.

## Related playbooks

- [FS-01 · Claims intake](../fs-01/): the same document reading and confidence routing, applied to claims.
- [FS-03 · Customer onboarding and KYC](../fs-03/): identity checks and sanctions screening with a reviewer on every gap.
- [MD-02 · Quoting](../md-02/): quotes built from specs, price rules and past jobs, a similar read-and-summarize pattern.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
