# TP-GOV-007 — Validation Independence and Evidence Provenance Review

## 1. Procedure Identity
**Procedure ID:** TP-GOV-007
**IRQ:** IRQ-GOV-007 — Validation Not Independent of Development, or Reliant on Vendor/Public Benchmark Claims
**Assurance objective:** AO-GOV-007 — Validation of AI systems prior to deployment shall be performed by a function structurally and substantively independent of development and procurement, with genuine authority to reject, and shall be based on firm-relevant evaluation evidence rather than vendor or public benchmark claims alone.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established independent-validation-adequacy methodology directly anchored in SS1/23 Principle 4 and reinforced by the PRA's October 2025 MRM AI/ML roundtable findings; no AI-specific benchmark defines the precise evidence threshold for "firm-relevant" GenAI validation, so professional judgement determines adequacy.
**Method classification:** Adapted Industry Practice — independent-validation-adequacy review under SS1/23, extended to AI-specific firm-relevance and contamination-screening dimensions.

## 2. Preconditions
**Environment:** Governance records and interviews. No production system access required.
**Access required:** Validation records for sampled systems; organisational charts and reporting lines for the validation function; validation function terms of reference including reject authority; the evaluation evidence underpinning each validation conclusion; deployment decision dates.
**Artefacts required:** Validation reports with dates; organisational structure documentation; validation terms of reference; the underlying evaluation evidence (firm-relevant test results, vendor safety cards, public benchmark scores); contamination screening records; records of any validation rejection or restriction; validation function resourcing and competence records.
**Personnel required:** Validation function staff (minimum two interviews); the development/procurement lead for at least one sampled system (reviewer-set design minimum, disclosed at scoping); reviewer.
**Data handling:** Validation reports may contain commercially sensitive vendor material. Handle under engagement confidentiality; vendor-confidential content should not be reproduced in wider circulation.

## 3. Test Design
Four assessment dimensions per sampled system:

- **Structural independence** — organisational and reporting-line separation of validation from development and procurement.
- **Evidence provenance** — is the evaluation evidence firm-relevant (the firm's own data, use cases, customer population) or substantially vendor-reported / public-benchmark-derived?
- **Contamination screening** — where public benchmark evidence was used, was it screened for contamination risk?
- **Substantive authority** — is there a documented track record of exercising reject or restrict authority, not solely pass outcomes?

Dimension four is the discriminating one. A structurally separate validation function that has never rejected anything across a large population of validations is, on the canvas's own language, indistinguishable from a rubber stamp.

A fifth check that costs almost nothing and frequently yields: compare validation report dates against deployment decision dates. Validation dated after the decision is confirmation, not validation.

Sample: risk-based, weighted to Tier 2–3, minimum six systems, and should include at least one system where the model is third-party-supplied (reviewer-set design minimum, disclosed at scoping), since that is where vendor-claim reliance concentrates.

## 4. Steps
1. Draw and record the sample, including at least one third-party-supplied model. **Record:** basis, size, weighting.
2. Obtain the organisational structure and validation terms of reference. **Record:** reporting lines from validation to the executive; whether validation reports through, or alongside, the function that owns development; documented reject authority.
3. For each sampled system, obtain the validation report and the evidence it relies on. **Record:** the evidence inventory per system.
4. Classify each evidence item as firm-relevant (firm's own data/use case/population), vendor-reported, or public-benchmark-derived. **Record:** classification and the proportion of the validation conclusion resting on each class.
5. For any public benchmark evidence, check for contamination screening. **Record:** whether screening was performed, its method, and its result. Where the benchmark is one with known contamination risk in the literature and no screening occurred, record that specifically.
6. Compare validation report dates against deployment decision dates. **Record:** any validation dated at or after the decision.
7. Search the validation function's records for instances of reject or restrict authority being exercised in the review period. **Record:** count, and the specific instances with dates and outcomes.
8. Interview validation staff (minimum two). Ask about: resourcing adequacy; AI-specific competence and training; experience of commercial pressure and whether they have successfully resisted it; whether they believe they could reject a system the business urgently wants. **Record:** verbatim responses.
9. Interview the development/procurement lead for at least one sampled system. **Record:** their account of the validation interaction — whether validation challenged anything substantive.
10. Assess firm-relevance adequacy per system. **Record:** the reviewer's judgement, with reasoning, on whether the firm-relevant evidence was sufficient to support the validation conclusion, explicitly labelled as professional judgement per the ★3 caveat.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Structural separation from development/procurement | 100% of sample, with documented reject authority | Categorical per canvas pass indicator |
| Validation conclusions supported by firm-relevant evidence | 100% of sample; vendor/public benchmark evidence used only as supplementary and explicitly contamination-screened | Categorical per canvas pass indicator |
| Instances of reject/restrict authority exercised | ≥1 in the review period | Categorical per canvas pass indicator ("no instance across the sample suggests a rubber-stamp function") |
| Validation dated prior to deployment decision | 100% of sample | Categorical per canvas pass indicator |
| Contamination screening where public benchmarks relied upon | Performed | Categorical per canvas fail indicator |
| Sufficiency of firm-relevant evidence | Reviewer judgement — no established threshold. No AI-specific benchmark defines the evidence threshold for firm-relevant GenAI validation | Explicitly bespoke; the ★3 caveat |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: the validation function is organisationally separate for 100% of the sample with documented reject authority; conclusions are supported by firm-relevant evidence with vendor/public benchmark evidence contamination-screened and supplementary only; at least one documented instance of reject/restrict authority exists; validation staff describe adequate resourcing and AI competence and can cite successful challenge to commercial pressure; and validation reports predate deployment decisions.

**Fail** where: validation is performed by the developing or procuring team, or by a nominally separate team with no documented reject authority; conclusions rest substantially on vendor safety-card claims or public benchmark scores with no firm-relevant testing; no instance of reject/restrict authority exists across the sample; validation reports postdate the effective deployment decision; or public benchmark evidence shows no contamination screening despite known risk.

**Partial** where structural independence is sound and reject authority documented, but evidence provenance for third-party models rests heavily on vendor claims — the characteristic pattern for bought-in foundation models.

## 7. Evidence Outputs
- Organisational structure and validation terms of reference — **L2**
- Validation reports as obtained — **L2**
- Evidence provenance classification per system — **L3**
- Date reconciliation (validation vs deployment decision) — **L3**
- Reviewer's independent independence and firm-relevance assessment — **L4**
- Records of real reject/restrict decisions taken by validation — **L5**

## 8. Common Pitfalls & Limitations
- **Confusing organisational separation with substantive independence.** A separate box on a chart that has never said no is the finding this procedure is designed to surface.
- **Accepting a vendor safety card as evaluation evidence.** It is a vendor claim. Classify it as such at step 4.
- **Missing contamination screening because no benchmark was named.** Where a validation cites "strong benchmark performance" without naming the benchmark, that is itself a provenance failure.
- **Sampling only internally-built models.** Third-party inclusion is where vendor-claim reliance lives.
- **Interviewing validation staff in the presence of their management.** Question 8's commercial-pressure limb requires a private setting.

## 9. Time / Effort Estimate
**4 reviewer-days**: 0.5 day sampling and structure review, 1.5 days validation record and evidence provenance analysis, 1 day interviews, 1 day assessment and working papers.

---
---

