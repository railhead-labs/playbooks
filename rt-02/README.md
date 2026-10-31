# RT-02 · Product content

> Listings and descriptions written and checked across every channel.

**Industry:** Retail · **Typical owner:** Director of e-commerce content · **Reading time:** 9 min

## Who this is for

Retailers and brands with thousands of SKUs sold through their own site, marketplaces and retail partners, each with its own format. The content team and merchandisers feel the pain, and so does legal when a claim slips through. This playbook fits if new items wait weeks to go live, the same product reads differently on every channel, supplier spec sheets get retyped by hand, and nobody can say where a "non-toxic" or "eco-friendly" claim came from.

## How it runs today

1. A buyer sets up a new item. Suppliers send spec sheets, images, certificates and marketing copy as PDFs, spreadsheets and email.
2. A coordinator retypes attributes into the product information management (PIM) system or a spreadsheet. Missing fields go back to the supplier by email.
3. A copywriter writes the title, bullets and description, often starting from the supplier's copy.
4. Each channel needs its own version: your site, each marketplace's title and attribute rules, partner feeds and sometimes translations.
5. An editor checks brand voice. Claims that sound risky go to legal, sometimes, through email threads.
6. Content is published or syndicated. Feed rejections come back and get fixed one at a time.
7. When a supplier changes a material, formula or certificate, the old copy stays live until someone notices.

Where the hours go: retyping spec sheets, rewriting the same facts for each channel, chasing suppliers for missing attributes and fixing feed rejections. Claims review is the step most often skipped under deadline pressure, and it carries the most risk.

## Measure your own baseline

| Step | Who does it | Volume per week | Minutes each | Hours per week |
|---|---|---|---|---|
| Attribute entry from supplier documents | | | | |
| Chasing missing attributes | | | | |
| First-draft copy | | | | |
| Channel versions | | | | |
| Brand voice edit | | | | |
| Claims review | | | | |
| Feed rejection fixes | | | | |
| Updates after supplier changes | | | | |
| **Example** (illustrative values only): Channel versions | Content coordinator | 80 SKUs | 15 | 20 |

Hours per week is volume times minutes, divided by 60.

Collect the numbers in one week. Count SKUs created or changed from PIM history. Sit with coordinators and writers and time a sample of items at each step. Pull feed rejection reports from each marketplace or syndication tool. Count the claims sent to legal and how long each waited. Note any live listings the team found with errors that week, and what the error was.

## The redesigned process

| Step | What AI does | What a person does | Confidence/route rule |
|---|---|---|---|
| Attribute extraction | Reads spec sheets, labels and certificates. Fills PIM attributes and cites the source page for each value. Lists missing or conflicting fields and drafts the supplier request. | Coordinator confirms flagged fields and sends supplier requests. | Value found in a source with high confidence: filled. Conflicting sources or no source: person. |
| Drafting | Writes title, bullets and description in your brand voice, using only sourced attributes. | Writer edits drafts for new categories and key products. | Routine category: on to checks. New category: writer. |
| Brand voice check | Scores each draft against your style guide: banned words, tone, length, reading level, required elements. Explains each failure and redrafts. | Editor reviews failures and samples passing drafts. | Pass: continue. Fails after one redraft: editor. |
| Claims check | Finds every claim in the copy and image text. Matches each against your approved claims register. Labels unmatched claims by type: safety, health, environmental, origin, certification, performance, comparison. | A named claims approver in legal, compliance or product safety approves every regulated or safety claim before it is published. | Exact match within the claim's approved scope: allowed. Any regulated or safety claim not already approved: blocked until a person approves. |
| Channel versions | Adapts the approved master copy to each channel's length, attribute and format rules. Validates against the feed spec before sending. | Channel manager handles rejections the system can't explain. | Passes channel rules: queued. Fails: person. Channel versions may drop a claim to fit length but never reword it. |
| Publish | Sends approved content to the PIM and channels. Records which version went where. | Content lead approves the first batch for each new category or channel. | Only content that passed every check publishes. |
| Change watch | Reads new supplier documents and flags listings whose facts or claims changed. | Coordinator and claims approver re-review affected listings. | Changed claim or safety fact: listing held for review. |

Two kinds of confidence matter here. Extraction confidence asks whether the system read the right value from the right document. You tune it with your audit sample. Claim status is different. It is a yes-or-no rule, not a score. A regulated or safety claim either has an approval on file for this product, or it waits for a person. The model never decides that a claim is "probably fine."

The approved claims register makes this work. Each entry holds the exact wording, the products or categories it covers, the substantiation (test report, certificate, supplier declaration), who approved it, and when it needs a re-check. The AI may reuse an approved claim within its scope. It may not invent a claim, broaden one (from "recyclable packaging" to "recyclable"), or carry a claim from one product to a similar one without its own register entry.

## What stays with people

- **Approval of every regulated or safety claim before publishing.** This covers product safety, health and wellness, environmental claims ("eco", "biodegradable", "recyclable", "carbon neutral"), "natural" and "organic", country of origin, certifications and test results. A person checks the substantiation because these claims carry legal exposure. <!-- VERIFY: in the US, environmental marketing claims are addressed by the FTC's Green Guides; health claims may fall under FTC and FDA rules depending on product type; "Made in USA" claims are subject to FTC standards; California Proposition 65 warnings may apply to some products. Confirm which rules apply to your categories and markets. -->
- **Required warnings and age grading.** Warning text, such as choking hazard warnings on toys, comes from an approved source and is never written or paraphrased by the AI. <!-- VERIFY: confirm required warning and labeling rules for children's products and other regulated categories you sell, including online listing requirements. -->
- **Brand voice.** The style guide itself, copy for key products and the tone of new categories.
- **Supplier relationships.** Pushing back on missing or weak substantiation.
- **Go-live decisions** for a new category or channel.
- **Fixes to listings** flagged by customers, marketplaces or regulators.

## Controls and risks

- **Accuracy targets.** A coordinator checks a weekly sample of attributes against the source documents. Set targets by attribute type with the content owner. Safety-relevant attributes (materials, age grade, power ratings, allergens, dimensions that affect fit or safety) start at full human review and need a stricter bar before sampling.
- **Claims.** The target for unapproved regulated claims going live is zero. Measure it by auditing a sample of live listings monthly. Every miss gets a root-cause review.
- **Grounding.** Every factual statement in a draft must trace to a sourced attribute. Drafts with unsourced facts are rejected automatically.
- **Exact legal text.** A check confirms that required warnings and legal text appear word for word on every channel version.
- **Audit trail.** For each listing version, store the source documents, extracted values, model and prompt versions, check results, claim approvals, and which channels received it and when.
- **Failure modes and fallback.** Watch for invented features, claims carried over from a similar product, expired certificates, and translations that change a claim's meaning. On any check failure, the listing holds and routes to the current manual workflow. Nothing publishes on a failed check.
- **Translations.** Translated copy goes back through the claims check. A fluent reviewer approves regulated claims in each language.
- **Access.** Only named claims approvers can add or change register entries. Writers can't approve their own claims.
- **Model and prompt change control.** The style guide, register, prompts and models are versioned. Changes are tested against a saved set of past listings, including known problem claims that must be caught, before release.
- This playbook is general information, not legal or compliance advice. Confirm requirements with your counsel and compliance team.

## How to build it

### Map (week 1-2)
- Follow a handful of recent items from supplier email to live listing on each channel.
- Collect the style guide, each channel's listing requirements and every claim currently in use. Find where each claim's substantiation lives, if anywhere.
- Fill in the baseline worksheet and pull feed rejection reports.
- Ask legal and compliance which claim types concern them most and who should approve them.

### Redesign
- Build the first version of the claims register from claims already approved. Mark anything without substantiation as unapproved.
- Turn the style guide into checkable rules: banned words, required elements, length, reading level, plus examples of good copy.
- List the claim types that always need a person.
- Name the claims approvers and a backup for each.
- Pick a starting category with high volume and low claim risk, for example basic housewares with no safety or environmental claims.

### Build (two-week sprints)
- **Sprint 1:** attribute extraction into a staging area, compared with what coordinators enter by hand.
- **Sprint 2:** drafting and the brand voice check in a review console. Writers edit. Nothing publishes.
- **Sprint 3:** claims detection and the register check, tested against saved past listings with known problem claims.
- **Sprint 4:** channel versions and feed validation. Publish the starting category through the new path.
- The old path stays open for every other category. Add categories one at a time.

### Run
- Weekly: attribute and voice samples, claims queue age, feed rejections.
- Monthly with the content owner and claims approver: live-listing claims audit, register re-checks due, supplier gaps, style guide changes.

### Reference architecture
- **Intake:** supplier portal on Vercel, or email and file intake through Cloudflare Workers. Documents and images in R2.
- **Extraction:** Workers AI models read documents and images, called through AI Gateway for logging, rate limits and model fallback.
- **Rules:** style rules, channel specs and the claims register stored in D1 and checked by Workers. Rules live in code and data, not in prompt text.
- **Orchestration:** Workflows moves each SKU through extract, draft, check, approve and publish, and waits for approvals. Queues absorb seasonal bulk loads.
- **Human review queue:** content and claims review console behind Cloudflare Access.
- **System-of-record write-back:** PIM API, then channel syndication or marketplace APIs.
- **Observability:** Logpush and Log Explorer for every check result and publish event.

**Integration points:**
- PIM and ERP item master
- E-commerce platform
- Digital asset management
- Marketplace and retail partner feeds, or a syndication tool
- Supplier portal
- Translation service

## How to know it is working

- **Time to live:** days from item setup to live on all channels.
- **First-pass acceptance:** share of drafts published without edits, by category.
- **Attribute accuracy:** share of sampled attributes that match the source document.
- **Claims caught before publishing versus found live.** The goal for regulated claims found live is zero.
- **Feed rejection rate:** rejections per hundred listings sent, by channel.
- **Content-driven returns and contacts:** returns coded "not as described" and customer questions about missing details.

Review weekly with the content team and monthly with the content owner and claims approver.

## Getting started checklist

- [ ] Name the content owner and the claims approvers for safety, health and environmental claims.
- [ ] Collect every claim in use, with its substantiation, into one list.
- [ ] Write down the claim types that always need a person.
- [ ] Fill in the baseline worksheet for one week.
- [ ] Gather the style guide and each channel's listing requirements.
- [ ] Save a test set of past listings, including some with known problem claims.
- [ ] Decide where required warnings and legal text live as approved source text.
- [ ] Pick a low-risk starting category.

## Related playbooks

- [MD-04 Supplier onboarding](../md-04/): spec sheets and certificates collected and checked before content work starts.
- [RT-04 Customer service](../rt-04/): product questions answered from the same approved content.
- [RT-01 Returns](../rt-01/): "not as described" returns show which listings need work.

---
*Free to use under [CC BY 4.0](../LICENSE). Written by Railhead Labs engineers. Want help mapping this process? Email hello@railheadlabs.com or book a [Process Redesign Assessment](https://railheadlabs.com/services#process-redesign-assessment).*
