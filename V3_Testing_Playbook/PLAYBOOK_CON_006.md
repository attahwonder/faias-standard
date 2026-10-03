# TP-CON-006 — Price Decomposition and Elasticity Isolation

## 1. Procedure Identity
**Procedure ID:** TP-CON-006
**IRQ:** IRQ-CON-006 — Unfair Differential Pricing Untethered from Cost or Risk
**Assurance objective:** AO-CON-006 — AI-influenced pricing shall be tested to isolate and constrain price differentiation driven by inferred price sensitivity or inertia from differentiation driven by genuine cost or risk, consistent with Consumer Duty fair-value expectations.
**★ Confidence (carried from canvas, unchanged):** ★2 — the FCA's general insurance pricing intervention establishes the regulatory principle and a precedent methodology at product level; decomposition testing at the individualised AI-model level is bespoke, with no agreed FS benchmark for isolating elasticity from risk within a single model.
**Method classification:** Emerging Practice (No Established Benchmark), informed by the FCA general insurance pricing intervention as a regulatory precedent at product level.

## 2. Preconditions
**Environment:** Non-production analysis environment with the pricing model available for inspection and ablation. No live pricing system is invoked and no quote reaches a customer.
**Access required:** Model internals sufficient to inspect or compute feature contributions; ability to recompute prices with specified features ablated; read access to the feature dictionary with each feature's business rationale; read access to the board risk appetite as it bears on pricing fairness.
**Artefacts required:** Pricing model and its feature dictionary with stated rationale per feature; a representative non-production dataset; the board risk appetite statement (fair-value/pricing limbs); the firm's fair value assessment for the product; production price-differential monitoring definitions.
**Personnel required:** Pricing model owner; pricing policy/fair-value owner; reviewer with competence in model interpretation.
**Data handling:** Pricing data is commercially sensitive; handle under engagement confidentiality. Where customer-level records are used, they must be from a non-production copy with identifiers removed.

## 3. Test Design
The final price is decomposed into a risk/cost-justified component and a behavioural/elasticity-driven component. Two complementary routes, run together because each has a distinct weakness:

- **Route A — feature classification and contribution.** Classify every pricing feature as risk/cost, elasticity/inertia, or ambiguous, with the pricing owner adjudicating and the classification recorded before computation. Compute each class's contribution to the final price. Weakness: features are frequently ambiguous, and the classification drives the answer.
- **Route B — ablation.** Recompute prices with elasticity/inertia features removed and compare to the full model. Weakness: correlated features mean the model reallocates predictive weight, so ablation understates the elasticity component where a risk feature is also a partial elasticity proxy.

Both routes are then applied comparatively across segments: loyal/inert customers versus new/price-sensitive customers *at equivalent risk and cost*. The equivalence is established by matching, as in TP-CON-005, and the matching quality must be reported.

The signal of interest is not "does price vary" — it always does and should. It is whether, holding risk and cost equivalent, the inert customer pays more.

## 4. Steps
1. Obtain the board risk appetite statement and the fair value assessment. **Record:** whether AI-driven pricing fairness is addressed specifically, or whether the appetite is silent on it.
2. Obtain the feature dictionary with stated rationale. **Record:** total feature count.
3. Classify every feature as risk/cost, elasticity/inertia, or ambiguous, with the pricing owner adjudicating. **Record:** the classification, the adjudicator, and the reasoning for every ambiguous case. Do this before any computation.
4. **Route A.** Compute feature contributions to the final price for the representative dataset and aggregate by class. **Record:** mean and distribution of each class's contribution; the elasticity class's share of total price variation.
5. **Route B.** Recompute prices with all elasticity/inertia-classified features ablated. **Record:** price difference per record between full and ablated models; the mean and distribution of the difference.
6. Compare Route A and Route B results. **Record:** where they diverge and the likely reason (feature correlation, reallocation). Divergence is expected; concealing it is not.
7. Construct matched segments — loyal/inert versus new/price-sensitive at equivalent risk and cost. **Record:** matching variables, method and balance diagnostics.
8. Compute the elasticity-driven price component separately for each matched segment. **Record:** the segment-level values and the differential between them. This differential is the procedure's headline number.
9. Assess the differential against the board-approved fair-value tolerance. **Record:** whether a tolerance exists; if so, the comparison; if not, that absence.
10. Review production price-differential monitoring. **Record:** whether the pattern is tracked over time and whether any persistent unremediated differential exists.
11. Interview the pricing owner. **Record:** whether elasticity features were deliberately included, what business purpose they were understood to serve, and whether fair-value implications were considered at model approval.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Elasticity-driven component of price | The firm's board-approved fair-value tolerance, where one exists. Where none exists, that absence is a fail indicator per the canvas | Per canvas; the tolerance is firm-set. No external numeric threshold exists at individualised-model level |
| Differential between matched loyal/inert and price-sensitive segments | As above; reviewer judgement where no tolerance exists — no established threshold | Explicitly bespoke; the FCA general insurance pricing intervention establishes the principle at product level, not a model-level numeric threshold |
| Route A / Route B divergence | Reviewer judgement — no established threshold. Report descriptively; large divergence indicates heavy feature correlation and weakens both estimates | Bespoke |
| Feature classification | All features classified, with ambiguous cases individually reasoned and adjudicator named | Reviewer judgement; procedural requirement |
| Board appetite addresses AI pricing fairness | Present | Categorical per canvas fail indicator |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: decomposition testing demonstrates the elasticity/inertia-driven component is immaterial or explicitly bounded within a board-approved fair-value tolerance; no material unexplained differential exists between loyal/inert and price-sensitive customers at equivalent risk/cost; board risk appetite explicitly addresses AI-driven pricing fairness; and production monitoring confirms the pattern remains within tolerance over time.

**Fail** where: no decomposition testing exists and pricing is assumed risk-based without verification; testing finds a material elasticity-driven differential between matched-risk loyal and price-sensitive customers with no board-approved tolerance or remediation; board appetite does not address AI-driven pricing fairness specifically; or production monitoring shows a persistent unremediated differential.

**Partial** where decomposition shows a bounded elasticity component but no board tolerance exists against which to judge it, or where the appetite addresses pricing fairness generally but not the AI-specific individualisation mechanism.

## 7. Evidence Outputs
- Board appetite and fair value assessment extracts — **L2**
- Feature classification with adjudicator and reasoning, recorded pre-computation — **L2**
- Route A contribution analysis and Route B ablation results — **L3**
- Matched-segment construction with balance diagnostics — **L3**
- Reviewer's independent decomposition assessment and divergence analysis — **L4**
- Production price-differential monitoring over time — **L5**

## 8. Common Pitfalls & Limitations
- **Classifying features after seeing contributions.** Same failure mode as post-hoc metric selection in TP-CON-001, and just as fatal.
- **Relying on ablation alone.** Correlated features cause weight reallocation; ablation systematically understates the elasticity component. Route A is the check.
- **Ambiguous features resolved silently.** Tenure is both a risk signal and an inertia signal. Record the reasoning for every ambiguous case; the classification of tenure frequently determines the answer.
- **Unmatched segment comparison.** Comparing all loyal customers to all new customers conflates risk mix with elasticity. The matching is not optional.
- **Product-level precedent applied as a model-level threshold.** The FCA general insurance pricing intervention establishes the regulatory principle; it does not supply a numeric threshold for an individualised model. Do not present one as though it did.
- **★2 caveat.** Isolating elasticity from risk within a single model has no agreed method. Report as professional assessment.

## 9. Time / Effort Estimate
**5 reviewer-days**: 1 day appetite/fair-value review and feature classification with the pricing owner, 1.5 days Route A and Route B computation, 1 day matched-segment construction, 1 day comparative analysis and divergence assessment, 0.5 day working papers.

---
---

