# TP-CON-002 — Proxy Feature and Feature-Combination Probing

## 1. Procedure Identity
**Procedure ID:** TP-CON-002
**IRQ:** IRQ-CON-002 — Undetected Proxy Discrimination via Facially Neutral Features
**Assurance objective:** AO-CON-002 — The system's full feature set shall be analysed for proxy correlation with protected characteristics, individually and in combination, with material proxy risk documented and formally accepted or remediated.
**★ Confidence (carried from canvas, unchanged):** ★2 — proxy discrimination as a general phenomenon is well documented in research; a standardised, benchmarked FS methodology for composite/interaction proxy testing does not exist, so test design and threshold-setting rely heavily on professional judgement.
**Method classification:** Emerging Practice (No Established Benchmark) for composite/interaction proxy probing; the single-feature correlation component is Adapted Industry Practice.

## 2. Preconditions
**Environment:** Non-production analysis environment. The model is scored offline or via a non-production endpoint; no live decisioning is invoked.
**Access required:** The complete model input feature list — including derived and engineered features, not only the business-named inputs; ability to run feature-importance or ablation analysis against the non-production model; read access to any prior proxy analysis.
**Artefacts required:** Full feature dictionary with derivation logic; non-production dataset with protected-characteristic labels held for testing only; prior proxy analysis reports (with dates); feature-engineering pipeline documentation; outcome-level monitoring definitions.
**Personnel required:** Model owner; feature-engineering owner (frequently a different person, and the one who knows what the derived features actually encode); DPO/privacy lead; reviewer.
**Data handling:** As TP-CON-001. Additionally: proxy analysis frequently reveals that an existing production feature is highly predictive of a protected characteristic. That finding is itself sensitive; handle it under engagement confidentiality and route it to the model owner and DPO before it appears in any wider draft.

## 3. Test Design
Three layers, in order of increasing yield and decreasing standardisation:

- **Layer 1 — single-feature correlation.** For every model input feature, compute association with each protected characteristic (correlation for continuous, Cramér's V or equivalent for categorical). Standard, cheap, and rarely where the problem is.
- **Layer 2 — combination probing.** For a defined set of plausible feature combinations (the canvas's example is postcode + device type), compute association with each protected characteristic. The combination set must be defined by reasoning about the business context, not exhaustively — an exhaustive combinatorial search over a large feature set is both infeasible and guaranteed to produce spurious findings at scale.
- **Layer 3 — materiality.** For any feature or combination flagged in layers 1–2, establish whether it materially drives model output, via feature-importance or ablation analysis. A feature that correlates strongly with a protected characteristic but contributes nothing to the output is a lower-priority finding than one that correlates moderately and drives the decision.

The multiple-comparisons problem is real and must be managed explicitly: with 200 features and 6 protected characteristics, 1,200 tests will produce apparent findings by chance. Record the correction applied (or the decision not to correct, with reasoning) before computing.

## 4. Steps
1. Confirm the data-protection basis as in TP-CON-001 step 1. **Record:** confirmation.
2. Obtain the complete feature dictionary, including derived features. **Record:** total feature count; number of derived features; whether derivation logic is documented for each.
3. Define and record the correlation threshold that will flag a feature for further review, and the multiple-comparisons approach. **Record:** both values and their reasoning, before computation.
4. Define the combination set for Layer 2 by structured reasoning about the business and data context (geography-adjacent features, device/channel features, life-stage-adjacent features, income-source features). **Record:** the combination list and the reasoning that produced it.
5. **Layer 1.** Compute association between each feature and each protected characteristic. **Record:** the full association matrix; every cell exceeding the threshold.
6. **Layer 2.** Compute association between each defined combination and each protected characteristic. **Record:** results; every combination exceeding the threshold, and how much stronger the combination is than its strongest constituent (the interaction lift is the finding of interest).
7. **Layer 3.** For each flagged feature and combination, run feature-importance or ablation analysis against the model. **Record:** the feature's contribution to output; the change in outcome distribution when the feature is ablated.
8. For each flagged, materially-driving feature or combination, search for documented business justification, mitigation (removal, transformation) or formal risk acceptance. **Record:** what exists and which body accepted it.
9. Review prior proxy analysis. **Record:** date of last analysis; whether it covered combinations or single features only; whether re-testing has occurred since model build.
10. Review outcome-level monitoring. **Record:** whether outcome-level disparity monitoring exists as a backstop capable of catching proxy-driven disparity even where the specific mechanism was never identified. This is the most important compensating control in the domain.
11. Interview the feature-engineering owner on any derived feature flagged. **Record:** what the feature was intended to encode and whether the proxy relationship was known.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Feature-to-characteristic association | Reviewer judgement — no established threshold. Set and record before computation | Explicitly bespoke; no FS benchmark for proxy correlation thresholds |
| Combination interaction lift | Reviewer judgement — no established threshold. Report the lift over the strongest constituent feature descriptively | Bespoke |
| Materiality (feature contribution to output) | Reviewer judgement — no established threshold | Bespoke |
| Multiple-comparisons handling | Must be recorded before computation, whether a correction is applied or not | Standard statistical practice; the principle is established, the choice is the reviewer's |
| Re-testing cadence since model build | Reviewer judgement. The canvas treats a one-off analysis at build with years of subsequent operation as a fail indicator | Per canvas |
| Outcome-level monitoring backstop | Present | Categorical per canvas pass indicator |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: the full feature set including combinations has been tested for correlation with protected characteristics; any material proxy found has documented justification, mitigation or formally accepted residual risk; proxy testing has been repeated since model build; and outcome-level monitoring exists as a backstop.

**Fail** where: the only fairness assurance offered is "protected characteristics are not used as inputs" with no proxy analysis performed; a feature or combination is found to be a strong material proxy with no prior analysis, justification or mitigation on record; analysis was a one-off at build with no periodic re-testing despite years of operation; or no outcome-level monitoring exists as a backstop.

**Partial** where single-feature analysis exists and is sound but combination probing has never been performed — by some margin the most common outcome, because Layer 2 is the part with no established methodology.

## 7. Evidence Outputs
- Feature dictionary and combination-set definition with reasoning — **L2**
- Pre-recorded threshold and multiple-comparisons decision — **L2**
- Layer 1 and Layer 2 association matrices — **L3**
- Layer 3 feature-importance/ablation results — **L3**
- Reviewer's independent proxy assessment and materiality ranking — **L4**
- Outcome-level production monitoring showing disparity over time — **L5**

## 8. Common Pitfalls & Limitations
- **Exhaustive combination search.** Infeasible and statistically hopeless. Reason about which combinations plausibly encode a protected characteristic and record the reasoning; a defensible narrow set beats an indefensible broad one.
- **Ignoring multiple comparisons.** With hundreds of features, uncorrected testing generates findings that will not replicate, and a single non-replicating finding will be used to discredit the whole report.
- **Correlation without materiality.** Reporting a strongly correlated feature that contributes nothing to output as a headline finding wastes the firm's remediation capacity. Layer 3 exists to rank.
- **Derived features invisible in the business feature list.** The engineered feature "average transaction value in postcode-sector over 90 days" may not appear in the model card. Insist on the pipeline-level dictionary.
- **Treating "we don't use protected characteristics" as an answer.** The canvas names this exact assertion as a fail indicator; it is the belief this procedure exists to test.
- **★2 is the honest rating.** Combination proxy probing is bespoke. Report conclusions as professional assessment.

## 9. Time / Effort Estimate
**5 reviewer-days**: 0.5 day data-protection clearance, 1 day feature dictionary review and combination-set design, 1.5 days Layer 1 and Layer 2 computation, 1 day Layer 3 materiality analysis, 1 day working papers. Add 1 day where the feature set exceeds ~300 features.

---
---

