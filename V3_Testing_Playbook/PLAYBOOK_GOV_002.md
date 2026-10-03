# TP-GOV-002 — Inventory Completeness Sweep

## 1. Procedure Identity
**Procedure ID:** TP-GOV-002
**IRQ:** IRQ-GOV-002 — Incomplete AI Inventory Concealing Shadow, Embedded and Agentic AI Use
**Assurance objective:** AO-GOV-002 — The firm shall maintain an AI inventory that is verified complete through active discovery — including shadow AI, embedded vendor AI, informal spreadsheet-plus-API use, and agentic workflows — not solely through self-declaration.
**★ Confidence (carried from canvas, unchanged):** ★2 — research evidence that shadow/embedded AI is a real and growing exposure exists, but the test design (which routes to sample, how large a sample constitutes reasonable assurance of completeness) is bespoke and relies heavily on reviewer professional judgement; no standard methodology or benchmark for inventory-completeness testing was identified.
**Method classification:** Adapted Industry Practice (IT asset management and audit reconciliation) applied through an Emerging Practice discovery design.

## 2. Preconditions
**Environment:** Logs, contracts and interviews. No production system access required beyond retrieving egress log extracts.
**Access required:** Read access to API/network egress logs or proxy/CASB records for the review period; read access to the contract register and vendor product documentation; ability to schedule structured interviews with front-line staff across sampled business units; read access to the declared AI inventory and its discovery-mechanism design.
**Artefacts required:** Declared AI inventory with version and date; egress log extracts; contract register; vendor questionnaires as issued and as answered; the discovery mechanism's design and its cadence; records of any previous discovery findings; expense/procurement records for SaaS subscriptions below the formal procurement threshold.
**Personnel required:** Network/security operations for log extraction; procurement or vendor management; a sample of front-line staff across business units; reviewer.
**Data handling:** Egress logs may contain user identifiers and request metadata. Extract only destination-endpoint and volume fields where possible; where user attribution is necessary, restrict to the review team and report by business unit rather than by individual. Do not extract request payloads.

## 3. Test Design
Three discovery routes are run, none of which depends on self-declaration, and their union is reconciled against the declared inventory. Anything found by an independent route and absent from the inventory is a discovery-mechanism failure — that is the procedure's core logic.

- **Route 1 — technical.** Review egress logs for calls to known GenAI provider endpoints. Build the endpoint list before the search (major model providers, aggregation layers, common agent/automation platforms) and record it, since the list bounds what the route can find.
- **Route 2 — contractual.** Review vendor contracts and current product documentation for embedded AI/ML features. Product documentation matters more than the contract: vendors add AI features mid-term without contract amendment, which is the canonical embedded-AI blind spot.
- **Route 3 — human.** Structured interviews with front-line staff about the tools they actually use day to day, asked without prompting for "AI" specifically (staff frequently do not classify their tools that way).

A fourth informal route worth running where accessible: expense and low-value SaaS subscription records, which surface individually-purchased tools below the procurement threshold.

Sampling: business units weighted to plausible AI exposure — customer service, HR, fraud, marketing, operations. Vendor relationships weighted to those with software delivery. Record the weighting rationale; the canvas is explicit that sample adequacy here is a reviewer judgement with no benchmark.

## 4. Steps
1. Obtain the declared inventory and freeze a version for comparison. **Record:** version, date, entry count, and how entries were sourced (self-declaration / discovery / both).
2. Obtain the discovery mechanism design. **Record:** whether an active discovery mechanism exists at all; its cadence; its last execution; whether it has ever found anything.
3. Build and record the known-GenAI-endpoint list for Route 1. **Record:** the list and its derivation, acknowledging that it bounds the route's coverage.
4. **Route 1.** Search egress logs for the endpoint list across the review period. **Record:** every endpoint contacted, calling business unit, volume and first-seen date.
5. **Route 2.** For the sampled vendor relationships, review contracts *and* current product documentation/release notes for AI/ML features. **Record:** every embedded AI feature found; whether the vendor questionnaire asked about it; whether the answer matched the documentation.
6. **Route 3.** Interview front-line staff in the sampled business units about their daily tools, using open questions ("walk me through the tools you used yesterday") rather than "do you use AI". **Record:** every tool named; which are AI-based.
7. **Route 4 (where accessible).** Review expense and low-value SaaS subscription records. **Record:** AI-related subscriptions found.
8. Reconcile the union of all routes against the frozen inventory. **Record:** every AI use found by an independent route and absent from the inventory, classified as shadow / embedded / agentic-composite / informal.
9. **Agentic-composite check.** Specifically examine whether approved tools have been combined into agentic workflows (chatbot plus plugins added incrementally) where no single change event would have triggered inventory review. **Record:** any found; this is the category the canvas flags as systematically missed.
10. Assess whether the discovery mechanism has ever operated substantively. **Record:** at least one documented instance of it finding and remediating a previously unrecorded AI use, or the absence of any such instance.
11. Review vendor questionnaire content. **Record:** whether questionnaires specifically probe embedded AI/ML capability or only generic security posture.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| AI uses found by independent routes and absent from inventory | Zero across the sampled population | Categorical per canvas pass indicator |
| Discovery mechanism has found something | ≥1 documented instance | Categorical per canvas pass indicator ("demonstrates it is live, not theoretical") |
| Vendor questionnaires probe embedded AI specifically | Present | Categorical per canvas fail indicator |
| Discovery cadence | Recurring, not one-off | Categorical per canvas pass indicator |
| Sample adequacy for a completeness claim | Reviewer judgement — no established threshold. No standard defines what sample size supports reasonable assurance of inventory completeness; the reviewer must state the sample basis and the limits of the assurance it supports | Explicitly bespoke; the primary reason for the ★2 rating |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: independent discovery routes find zero AI uses absent from the inventory across the sampled population; vendor questionnaires specifically probe embedded AI and responses are corroborated against product documentation; at least one documented instance exists of the discovery mechanism finding and remediating an unrecorded use; front-line interviews corroborate that described tools are all inventoried; and discovery operates on a defined recurring cadence.

**Fail** where: independent routes surface shadow, embedded or agentic AI absent from the inventory; the inventory relies solely on self-declaration with no independent verification (L1 evidence only); vendor questionnaires ask generic security questions without probing embedded AI; no evidence exists that the discovery mechanism has ever found anything; or agentic workflows assembled incrementally from approved tools are uncaptured because no single change event triggered review.

**Partial** where the inventory is complete for directly-procured GenAI but embedded vendor AI or agentic composites are missing — overwhelmingly the most common outcome.

## 7. Evidence Outputs
- Frozen inventory version and discovery mechanism design — **L2**
- Endpoint list and its derivation — **L2**
- Route 1 egress findings; Route 2 contract/documentation findings; Route 3 interview findings — **L3**
- Reconciliation matrix of union-of-routes against inventory, with classification of every gap — **L4**
- Records of the discovery mechanism's own historical findings — **L5**

## 8. Common Pitfalls & Limitations
- **A stale endpoint list.** Route 1 can only find what the list contains. New providers and aggregation layers appear constantly; state the list's derivation date as a limitation.
- **Egress logs that do not cover the estate.** Personal devices, unmanaged networks and vendor-hosted processing are invisible to Route 1. Record the coverage gap explicitly.
- **Asking staff "do you use AI".** They will say no while describing an AI tool. Open questions only.
- **Reading contracts and not release notes.** Embedded AI is usually added post-contract. Route 2 must examine current product documentation.
- **Overstating what the sweep proves.** Finding nothing in a sample does not establish inventory completeness across the estate. The canvas rates this ★2 precisely because no sampling frame supports a completeness claim; report the assurance as bounded by the sample.
- **Sequence dependency.** Run this procedure first in the GOV domain: every other GOV procedure samples from the inventory this one tests.

## 9. Time / Effort Estimate
**5 reviewer-days**: 0.5 day inventory freeze and mechanism review, 1 day endpoint list construction and log analysis, 1.5 days contract and product documentation review, 1 day front-line interviews across sampled units, 1 day reconciliation and working papers. Add 0.5 day per additional business unit beyond five.

---
---

