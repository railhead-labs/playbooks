# RT-01 · Returns

> Refund, repair, or resale decided from photos and order history.

**Industry:** Retail · **Typical owner:** Director of returns and reverse logistics · **Reading time:** 9 min

## Who this is for

Retailers and brands that sell online, in stores or both, with enough return volume to need a dedicated team. The pain shows up in customer care, at the returns dock and in finance. This playbook fits if photos arrive with requests but nobody looks closely, refunds wait days for a decision, items pile up at the dock, and your team can name repeat abusers but has no consistent way to catch them.

## How it runs today

1. A customer starts a return through a portal, email, chat or store counter. The reason is free text or a vague choice like "didn't like it."
2. A care agent looks up the order, checks the window and policy, and decides whether to issue a label. Photos sit as attachments.
3. Damage, defect and "not as described" claims go to a supervisor's queue. They wait.
4. The item ships back or is dropped at a store. It sits at the dock until someone opens it.
5. A grader inspects it, picks a disposition (restock, open-box resale, repair, return to vendor, liquidate, dispose) and types notes into the warehouse system.
6. Someone keys the refund into the order system or payment processor. Refunds over a limit wait for a manager.
7. Frequent returners, empty boxes and swapped items are caught by memory, if at all, and passed to loss prevention by email.
8. Vendor claims for defective goods are filed later in batches, after the evidence is hard to find.

Where the hours go: agents read the same order history twice, once for the label and again for the refund. Graders retype what the customer already said. Supervisors chase photos and notes across systems. Fraud review happens after the money has left. Vendor claims get skipped because gathering evidence takes too long.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Return request review and label | | | | |
| Damage and defect claim review | | | | |
| Dock receipt and grading | | | | |
| Refund or exchange entry | | | | |
| Refund approvals over the limit | | | | |
| Fraud and abuse review | | | | |
| Vendor claims | | | | |
| **Example** (illustrative values only): Refund approvals over the limit | Returns supervisor | 120 | 6 | 12 |

Hours per week is volume times minutes, divided by 60.

Collect the numbers in one week. Pull volumes from your systems: return authorizations, dock receipts, refunds, approvals. Sit with the person at each step and time a sample of real items. Ask agents and graders where they wait and what they look up. Pull timestamps for request to label, receipt to grade, and grade to refund. The gaps are the waits. Also record how many returns came with photos and how each one ended.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Intake | Reads the request, photos and order. Maps the reason to your reason codes. Checks the window and policy. | Nothing on routine requests. | In policy, under the refund threshold, clear reason: label issued automatically. Anything else: care agent. |
| Photo review | Compares customer photos with catalog images and the order. Describes damage, missing parts or a wrong item. Drafts an outcome: refund, exchange, repair or returnless refund. | Care agent reviews every draft below the confidence threshold. | High confidence, photos match the order, under the threshold: proceed. Otherwise: agent. |
| Fraud and abuse signals | Checks each return against your signals: return frequency, linked accounts and addresses, serial number or weight mismatches, high-theft items. Writes a plain reason for each flag. | Loss prevention or a named returns lead reviews every flagged return and decides. | Any fraud signal: person. The AI never denies a return or labels a customer on its own. |
| Refund approval | Prepares the refund with the evidence attached. | A named approver, for example the returns supervisor, approves every refund over the threshold. | Over the threshold: always a person. Under it with no flags: automatic. |
| Safety reports | Detects mentions of injury, fire, smoke, burns, shocks or choking. | Product safety lead reviews the same day. | Any safety mention: person, flagged urgent. |
| Dock grading | Reads the label, pulls up the claim and photos, and suggests a grade and disposition from bench photos. | Grader confirms or changes the grade and disposition. | Grader confirms every item at first. Move a category to sampled checks only after it meets the accuracy target. |
| Repair and resale | Drafts repair tickets and open-box listing notes from the grade. | Repair tech and resale lead own their queues. | Repairs above your cost limit: person. |
| Vendor claims | Groups defect evidence by vendor and SKU and drafts the claim. | Buyer or vendor manager submits or drops each claim. | Every vendor claim: person submits. |

Every recommendation carries a confidence score and the facts behind it. The system acts alone only when four things are true: the request is in policy, the value is under your refund threshold, the photos agree with the order, and no fraud or safety signal fired. A miss on any one sends the case to a person with the evidence gathered, so the reviewer starts with the decision instead of the lookup.

Set thresholds from your own audit sample, not a vendor default. Start conservative: a low auto-approve limit and a person grading every item. Raise limits one category at a time as the audit shows the AI agrees with your reviewers.

## What stays with people

- **Every refund over the threshold.** A named approver signs off with the evidence in front of them.
- **Every fraud or abuse decision.** A signal is not proof. A person decides whether to deny, limit or investigate. A wrong accusation loses a customer and can create legal exposure.
- **Every denial.** Customers hear "no" from a person, not from the system.
- **Safety reports.** Injury and hazard reports go to your product safety lead. They may carry reporting duties to product safety regulators. <!-- VERIFY: confirm with counsel whether and when retailers must report product hazards to regulators (for example the U.S. Consumer Product Safety Commission) in your markets and categories. -->
- **Policy exceptions for loyal or high-value customers.** These are relationship calls.
- **Grades that decide money.** Final grade in categories that haven't met the accuracy target, and on items that support a vendor claim.
- **Vendor claims.** The buyer owns the vendor relationship.
- **The return policy itself.** The system follows the policy. People change it.

## Controls and risks

- **Accuracy targets.** Before go-live, agree targets with the returns owner for reason codes, recommended outcomes and grades. Measure weekly on a random sample a person re-reviews without seeing the AI's answer. Set the bar at or above what your team achieves on the same sample today.
- **Fraud signal quality.** Review false flags monthly. Check that flags don't cluster by neighborhood or other stand-ins for protected traits. <!-- VERIFY: confirm with counsel which customer data and attributes may be used in return fraud scoring and customer restrictions in each market you sell in. -->
- **Audit trail.** Each return keeps the request, photos, model and prompt versions, scores, recommendation, approver and time, stored with the order record.
- **Failure modes and fallback.** Expect model outages, blurry photos and new products with no catalog images. When the AI service errors or confidence drops, cases route to the existing manual queue. The old path stays open.
- **Customer messages.** Automated decisions use the same approved templates as today. Return policy disclosure and refund timing rules vary by state and country, so keep templates aligned with your posted policy. <!-- VERIFY: confirm consumer protection requirements for return policy disclosure and refund timing in your markets. -->
- **Data handling.** Photos can show faces, homes and shipping labels. Store them in a private bucket with retention set by your policy. Card numbers never enter prompts or logs. Refunds go through your payment processor by original transaction reference. <!-- VERIFY: confirm with your PCI DSS assessor that issuing refunds by transaction reference keeps the returns system out of cardholder data scope. -->
- **Access.** The reviewer console sits behind single sign-on with role-based views. Only named approvers can release refunds over the threshold.
- **Model and prompt change control.** Versions are pinned. Every change runs against a saved test set of past returns with known outcomes, and the process owner signs off before release.

## How to build it

### Map (week 1-2)
- Walk the path with a care agent, a dock grader, a supervisor and someone from loss prevention. Follow a handful of real returns from request to refund.
- List every system a return touches.
- Fill in the baseline worksheet for one week.
- Collect the current policy, reason codes, refund limits and the fraud signals people already use informally.
- Pull a sample of past returns with photos and final outcomes. This becomes your test set.

### Redesign
- Define each disposition and its owner.
- Write the route rules: auto-approve conditions, the refund threshold, fraud signals and safety triggers.
- Name the approvers for refunds over the threshold, fraud, safety and vendor claims, plus a backup for each.
- Start with a high-volume, low-value category with a clear policy.

### Build (two-week sprints)
- **Sprint 1:** intake, reason mapping and policy check in shadow mode next to agents. No customer-facing actions.
- **Sprint 2:** photo review and recommended outcomes in the reviewer console. Agents still decide everything.
- **Sprint 3:** fraud signals with loss prevention review. Automatic labels for in-policy, low-value returns.
- **Sprint 4:** grading assist, automatic refunds under the threshold where the target was met, and vendor claim drafts.
- The manual queue stays open throughout. Turn on each automated step only after its shadow results meet the target.

### Run
- Weekly sampled audit of automated decisions.
- Monthly review with the returns owner: accuracy, flags upheld, approvals over the threshold, dispositions, policy changes.
- Thresholds and signals change only through change control.

### Reference architecture
- **Intake:** returns portal on Vercel or your current platform. Cloudflare Workers receive portal, email and help desk events. WAF in front of public endpoints.
- **Storage:** R2 for photos. D1 for case records, decisions and audit entries.
- **Orchestration:** Workflows runs each return as durable steps, including waiting for an approver. Queues absorb post-holiday spikes.
- **Extraction:** Workers AI for reason mapping and photo description, called through AI Gateway for logging, rate limits and model fallback.
- **Rules:** policy, threshold and fraud rules as versioned code in a Worker, separate from the model. Rules decide the route. The model supplies facts.
- **Human review queue:** a reviewer console behind Cloudflare Access.
- **System-of-record write-back:** labels, refunds and dispositions through order management, carrier and payment processor APIs. Tailscale for on-premises warehouse systems.
- **Observability:** Logpush to your log store or SIEM, Log Explorer for queries, AI Gateway analytics.

**Integration points:**
- E-commerce platform and order management system
- Returns portal and help desk
- Warehouse management system and bench cameras or scanners
- Payment processor
- Carrier label and tracking service
- Loss prevention case system
- ERP or vendor management system for claims

## How to know it is working

- **Straight-through rate:** share of returns completed with no person touching them, by category.
- **Decision accuracy:** on the weekly audit sample, share of automated decisions the reviewer would have made the same way.
- **Refund cycle time:** hours from request or dock receipt to refund. Track the median and the slowest tenth.
- **Fraud flag precision:** share of flags a reviewer upheld, plus abuse found later on returns never flagged.
- **Grade agreement:** share of suggested grades the grader kept.
- **Vendor claim recovery:** claims filed and amounts recovered against your baseline.

Review weekly with the returns team and monthly with the process owner.

## Getting started checklist

- [ ] Name the process owner and the approvers for refunds over the threshold, fraud and safety.
- [ ] Write down your current refund threshold and who can approve above it.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Pull past returns with photos and final outcomes into a test set.
- [ ] List the fraud signals your team already watches for.
- [ ] Pick one category to start.
- [ ] Agree on accuracy targets and the weekly audit sample.
- [ ] Confirm photo retention and access rules with privacy and security.

## Related playbooks

- [RT-04 Customer service](../rt-04/): return status and policy questions answered with order context, with the same handoff to a person.
- [RT-02 Product content](../rt-02/): "not as described" returns point to listings that need fixing.
- [MD-01 Order-to-cash](../md-01/): refunds and credits that have to reconcile with invoices and payments.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
