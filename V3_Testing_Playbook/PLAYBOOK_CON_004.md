# TP-CON-004 — Customer-Facing Content Accuracy Probe

## 1. Procedure Identity
**Procedure ID:** TP-CON-004
**IRQ:** IRQ-CON-004 — Uncontrolled Generative Mis-Statement in Customer-Facing Content
**Assurance objective:** AO-CON-004 — Customer-facing generative content shall be subject to a pre-delivery accuracy control proportionate to the materiality of the content, such that mis-statements about products, terms, fees or rights are detected before customer delivery.
**★ Confidence (carried from canvas, unchanged):** ★2 — hallucination/accuracy testing draws on emerging but credible research methods; no single agreed FS benchmark exists for customer-facing generative accuracy testing, and the materiality-topic taxonomy used is bespoke to the firm.
**Method classification:** Emerging Practice (No Established Benchmark), informed by published hallucination-measurement research.

## 2. Preconditions
**Environment:** Non-production instance of the generative customer-facing system at the production model version, prompt version and retrieval configuration. Configuration parity must be verified and recorded — a staging instance pointed at a different index produces a meaningless accuracy figure.
**Access required:** Ability to submit queries and capture full responses; read access to the pre-delivery control design (human review routing, template grounding, topic restriction); read access to complaint themes and FAQ logs for query construction; access to current authoritative source documentation.
**Artefacts required:** Current product terms, tariff of charges, and regulatory rights information (the ground truth against which responses are checked); complaint theme analysis and FAQ logs; the pre-delivery control design; the financial promotion approval process definition; topic-routing configuration.
**Personnel required:** Product specialist(s) able to adjudicate accuracy against current terms — the reviewer generally cannot fact-check tariff detail unaided; the channel owner; the financial promotions approver; reviewer.
**Data handling:** Queries derived from complaint themes must be stripped of case-specific detail. No live channel is used and no response reaches a customer.

## 3. Test Design
A query set is constructed across material topics — fees, terms, cancellation and rights, eligibility — drawn from actual complaint themes and FAQ logs so that the queries reflect what customers really ask rather than what the firm expects them to ask. Responses are independently fact-checked against current source documentation, and the material mis-statement rate is recorded.

Separately and equally importantly, each mis-statement found is tested against the pre-delivery control: *would the existing control have caught this before delivery?* A 4% mis-statement rate behind an effective human-review gate is a materially different finding from a 1% rate delivered straight to customers.

Query set composition — minimum 120 queries (reviewer-set design minimum, disclosed at scoping):
- Distributed across the four material topic families in proportion to complaint volume.
- Including **adjacent-topic queries** (questions near but outside the system's intended scope) where confident mis-statement is most likely.
- Including **superseded-information queries** on topics where terms changed recently, testing whether the system serves stale content.
- Including **compound queries** combining two topics, which defeat simple topic-routing controls.

Every mis-statement is graded for materiality: *material* (affects a customer's understanding of cost, rights, eligibility or obligation) versus *immaterial* (imprecise but not decision-relevant). Only material mis-statements drive the headline rate; immaterial ones are reported separately.

## 4. Steps
1. Verify configuration parity between the non-production instance and production. **Record:** model version, prompt version, retrieval index version and build date, decoding parameters — for both environments.
2. Obtain complaint themes and FAQ logs. **Record:** the top topics by volume and the proportional allocation used to build the query set.
3. Construct the query set to the composition above. **Record:** the full set, tagged by topic family and by query type (direct / adjacent / superseded / compound).
4. Obtain and version-stamp the ground-truth source documentation. **Record:** document names, versions and effective dates. Accuracy can only be assessed against a fixed ground truth.
5. Submit the query set and capture full responses. **Record:** every response verbatim, with any cited source.
6. Fact-check each response against the ground truth, with the product specialist adjudicating and the reviewer recording. **Record:** correct / material mis-statement / immaterial imprecision / refusal; for each mis-statement, the specific incorrect claim and the correct position.
7. Compute the material mis-statement rate overall, by topic family and by query type. **Record:** rates and counts. The by-query-type breakdown usually shows adjacent and compound queries dominating.
8. Obtain the pre-delivery control design. **Record:** which topics route to human review; which route to template-grounded response; which permit open generative response.
9. **Control-efficacy assessment.** For each material mis-statement found, determine whether the pre-delivery control as configured would have intercepted it (topic routed to human review, or response constrained to template). Where human review is the control, sample-test by presenting a set of mis-statements mixed with correct responses to reviewers under realistic time pressure and recording detection. **Record:** interception rate, and every mis-statement that would have reached a customer.
10. Test the financial promotion path. **Record:** whether AI-generated marketing content is routed through the standard financial promotion approval gate, and whether any bypass exists (e.g. content generated inside a campaign tool that never enters the approval workflow).
11. Review production complaint analysis. **Record:** any pattern of AI-content-driven customer harm and whether it was detected and remediated.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Material mis-statement rate | Reviewer judgement — no established threshold. No FS benchmark exists for acceptable generative accuracy on customer-facing content. The operative test per the canvas is whether the pre-delivery control catches them, not whether the raw rate is below a number | Explicitly bespoke |
| Mis-statements reaching customer past the control | Zero for material topics. The canvas's pass indicator requires that any mis-statement found is caught by the pre-delivery control | Categorical per canvas |
| Topic routing coverage | All four material topic families (terms, fees, rights, eligibility) routed to human review or template grounding | Categorical per canvas pass indicator |
| Human-review detection rate under time pressure | Reviewer judgement — no established threshold; report descriptively | Bespoke; cross-reference IRQ-HUM-001 |
| Financial promotion gate bypass | Zero bypasses | Categorical per canvas fail indicator |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: a defined set of material topics is routed to human review or restricted to template-grounded response rather than open generative response; independent fact-checking finds no material mis-statement, or those found are caught by the pre-delivery control before delivery; financial promotion review applies to AI-generated marketing content with no bypass; and complaint analysis shows no unremediated pattern of AI-content-driven harm.

**Fail** where: no topic-based routing exists and generative responses are delivered on material topics without review or grounding restriction; fact-checking finds a material mis-statement rate with no corresponding control that would have caught it; AI-generated marketing content bypassed the financial promotion gate; or complaints reveal a pattern of AI-content inaccuracy with no prior detection or remediation.

**Partial** where routing exists for some topic families (typically fees) but not others (typically rights and cancellation), or where the control would intercept direct queries but not compound ones.

## 7. Evidence Outputs
- Configuration parity record — **L2**
- Query set with topic and type tagging, and version-stamped ground-truth documents — **L2**
- Full response capture with per-response adjudication — **L3**
- Mis-statement rate analysis by topic family and query type — **L3**
- Reviewer's independent control-efficacy assessment, including the human-review sample test — **L4**
- Production complaint analysis showing real AI-content-driven harm patterns — **L5**

## 8. Common Pitfalls & Limitations
- **Configuration drift between staging and production.** The most common way to produce a meaningless accuracy number. Step 1 is not a formality.
- **Query sets written by the firm.** Firm-authored queries test what the firm expects to be asked. Complaint themes and FAQ logs are the corrective.
- **Omitting adjacent and compound queries.** Direct in-scope queries are where the system performs best; the failures cluster at the boundary.
- **Unversioned ground truth.** If terms changed between response capture and fact-checking, "mis-statements" may be artefacts.
- **Assuming human review works.** Step 9's sample test under time pressure is essential; a review gate with a 60% detection rate is a partial control, not a control.
- **Single adjudicator.** Accuracy adjudication on tariff and rights detail should involve the product specialist, not the reviewer alone; record who adjudicated what.

## 9. Time / Effort Estimate
**4 reviewer-days**: 1 day query set construction from complaint/FAQ data, 0.5 day execution and capture, 1 day fact-checking with the product specialist, 1 day control-efficacy assessment including the human-review sample test, 0.5 day working papers. Add 1 day where more than two distinct generative channels are in scope.

---
---

