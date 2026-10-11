# TP-CON-001 — Subgroup and Intersectional Outcome Disparity Testing

## 1. Procedure Identity
**Procedure ID:** TP-CON-001
**IRQ:** IRQ-CON-001 — Undetected Subgroup and Intersectional Outcome Disparity in AI-Influenced Decisions
**Assurance objective:** AO-CON-001 — The AI system's outcome distributions shall be tested at subgroup and intersectional level against justified fairness metrics, with material disparities documented and formally accepted or remediated before and during deployment. The same applies to the error rates, for each subgroup, of any perception component (identity verification, liveness checking, voice authentication or speech transcription) upstream of a customer outcome.
**★ Confidence (carried from canvas, unchanged):** ★3 — subgroup fairness-metric testing draws on a substantial and increasingly consistent body of published research; no single agreed FS benchmark or regulator-mandated test suite exists, so professional judgement governs metric selection and threshold-setting.
**Method classification:** Adapted Industry Practice — published fairness-metric methods applied to an FS decisioning context with no agreed FS benchmark.

## 2. Preconditions
**Environment:** Non-production analysis environment with an offline copy of the model (or a scoring API pointed at a non-production model instance). No production decisioning system is invoked and no live decision is affected.
**Access required:** Ability to score a held-out dataset through the model at the same configuration as production; read access to the model's documented fairness testing to date; read access to production monitoring definitions for subgroup tracking.
**Artefacts required:** Held-out dataset representative of the deployed population, with protected-characteristic labels available for testing only; the firm's prior fairness testing reports; the model's documented feature set; the definition of the outcome metric (approval, score, price or alert rate) appropriate to the system; the firm's documented fairness metric selection rationale, if any. Where a perception component sits upstream of the customer outcome: a non-production instance of that component, the threshold configured for deployment where the component applies one, and a subgroup-labelled evaluation set in the component's modality (image, video or audio) containing no production customer data; where none is available, step 13 records the component as untestable.
**Personnel required:** Model owner; data scientist able to score the held-out set and, where step 13 applies, to run the perception component's non-production instance on the evaluation set; the firm's DPO or privacy lead (for the special-category-data confirmation); reviewer with competence in fairness metrics and, where step 13 applies, in the error rates of the component in scope.
**Data handling:** Special category data. Labels held in a separate, access-controlled store, joined to model inputs only within the analysis environment, never written back to any production store, and deleted at engagement close. Where representativeness of the held-out set cannot be confirmed, substitute a clearly labelled synthetic proxy and mark every downstream conclusion as proxy-based. An image, video or audio evaluation set used at step 13 is handled on the same terms as the labels.

## 3. Test Design
Outcome distributions are computed disaggregated by each protected characteristic individually and by defined intersectional combinations — at minimum two-way intersections for the highest-volume protected characteristics. At least two fairness metrics are computed (the canvas names demographic parity and equalised odds as examples), and divergence between them is documented rather than resolved silently.

Metric selection is fixed and recorded *before* computation, together with the reason for the choice given the decision context: broadly, demographic-parity-family metrics suit access/eligibility questions, error-rate-family metrics (equalised odds, equal opportunity) suit questions of who bears the cost of model error. Both are computed regardless, because the divergence between them is itself a finding.

Minimum cell sizes must be set before disaggregation. Intersectional cells become small quickly; a disparity computed on a cell of 12 records is noise. Set the minimum, record it, and report cells below it as untestable rather than as passing.

Where an AI component performs identity verification, liveness checking, voice authentication or speech transcription upstream of a customer outcome, the procedure also computes that component's error rates for each subgroup — false match and false non-match rates for identity verification and voice authentication; for liveness checking, the rate at which presentation attacks are missed and the rate at which genuine presentations are wrongly rejected (NISTIR 8280's APCER and BPCER); word error rate for speech transcription. Where the component applies a decision threshold, both error rates are computed at the threshold configured for deployment and reported for each subgroup at that single threshold rather than as an aggregate or as a single error type. For such a component the disparity sits in the error rate, and balanced outcome distributions downstream do not show it. Where no subgroup-labelled evaluation set in the component's modality is available, the component is recorded as untestable and its error rates are not computed at step 13; the Pass, Fail or Partial result is reached without that computation, and the untested component is reported beside that result as a coverage gap (§6).

## 4. Steps
1. Confirm the lawful basis and DPIA for processing protected-characteristic labels. **Record:** confirmation, DPO name and date. Do not proceed without this.
2. Obtain the held-out dataset and assess representativeness against the deployed population (compare marginal distributions of key non-protected features and of volume by product/channel). **Record:** representativeness assessment and, if inadequate, the decision to proceed on a labelled synthetic proxy.
3. Define and record the outcome metric appropriate to the system (approval rate, mean score, mean price, alert rate). **Record:** definition and rationale.
4. Select and record the fairness metrics to be computed, with the reason for each given the decision context, **before** any computation. **Record:** metric list, rationale, and the reviewer's statement that selection preceded results.
5. Set and record the minimum cell size for disaggregated analysis. **Record:** value and reasoning.
6. Score the held-out dataset through the non-production model instance. **Record:** model version, prompt version (where applicable), configuration and scoring date.
7. Compute the outcome metric disaggregated by each protected characteristic individually. **Record:** per-group values, cell sizes, and the disparity measure (ratio and difference) against the reference group.
8. Compute the same for defined two-way intersections across the highest-volume protected characteristics. **Record:** per-cell values, cell sizes, and cells falling below the minimum size (reported as untestable).
9. Compute the second (and any further) fairness metric across the same disaggregations. **Record:** results, and explicitly every group or cell where the two metrics give opposing verdicts.
10. For every disparity exceeding the recorded threshold, search the firm's documentation for an existing business justification or formal risk acceptance. **Record:** whether justification exists, its content, and the body that accepted it.
11. Review the firm's own prior fairness testing. **Record:** whether it was intersectional or single-attribute only; how many metrics were used; whether metric selection rationale was documented.
12. Review production monitoring definitions. **Record:** whether subgroup and intersectional outcome tracking is active in production, or whether fairness testing was a one-off pre-deployment exercise.
13. Where the system includes a perception component (identity verification, liveness checking, voice authentication or speech transcription) upstream of the customer outcome, compute on the non-production instance the component's error rates for each subgroup: false match and false non-match rates for identity verification and voice authentication; for liveness checking, the rate at which presentation attacks are missed and the rate at which genuine presentations are wrongly rejected (NISTIR 8280's APCER and BPCER); word error rate for speech transcription. Where the component applies a decision threshold, obtain the threshold configured for deployment and compute both error rates at that threshold. Assess the evaluation set's representativeness against the deployed population; where it cannot be confirmed, mark every conclusion drawn at this step as proxy-based. **Record:** the evaluation set's source, subgroup composition and representativeness assessment, the configured threshold where one applies, per-subgroup values for each error type, cell sizes, and whether the firm's own testing reported these per subgroup — at that threshold, where one applies — or only in aggregate, as a single error type, or at another threshold. Where no subgroup-labelled evaluation set in the component's modality, or no non-production instance of the component, is available, do not compute: record the component as untestable at this step, to be reported beside the result as a coverage gap (§6), and still record how the firm's own testing reported its error rates.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Disparity ratio per subgroup and intersectional cell | Reviewer judgement — no established threshold. No UK regulator has adopted a numeric fairness threshold for FS AI decisioning. The reviewer must set, record and justify a threshold before computation, and report it as a reviewer-set value | Explicitly bespoke; the reason the canvas rates this ★3 rather than ★4 |
| Number of fairness metrics computed | ≥2, with divergence documented | Per canvas fail indicator ("only one fairness metric was tested with no documentation of why alternatives were not considered") |
| Intersectional coverage | ≥ two-way intersections for the highest-volume protected characteristics | Per canvas independent test specification |
| Minimum cell size | Reviewer judgement — no established threshold. Set and record before disaggregation | Bespoke; standard statistical practice provides the principle, not the value |
| Production subgroup monitoring | Present and active | Categorical per canvas pass indicator |
| Perception-component error rates by subgroup (where such a component sits upstream of a customer outcome) | Reported for each subgroup, per error type and, where the component applies a decision threshold, at the threshold configured for deployment; any disparity threshold is reviewer-set before computation, recorded and justified | Per canvas independent test; the fixed-threshold reporting rule follows NISTIR 8280 as cited at the canvas's field 18, whose Figure 1 also gives the presentation-attack-detection error rates used for liveness checking |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: testing is conducted at subgroup *and* intersectional level; the chosen metrics are documented and justified given known trade-offs; no material unexplained disparity is found, or where disparity exists a documented and formally accepted business justification exists; production monitoring shows subgroup/intersectional tracking is active rather than a one-off exercise; and, where a perception component sits upstream of a customer outcome, the firm's own testing reports its error rates for each subgroup — both error types at the threshold configured for deployment where the component applies one, word error rate for speech transcription — and the reviewer's step-13 computation finds no material unexplained disparity in them, or a documented and formally accepted justification exists where disparity is found. Where step 13 records the component as untestable, the limb on the reviewer's step-13 computation does not apply, and the component is reported beside the result (below).

**Fail** where: testing is conducted only at aggregate or single-attribute level with intersectional combinations untested; material disparity is found for a protected or intersectional subgroup with no documented justification or remediation plan; only one fairness metric was tested with no documentation of why alternatives were not considered; no production monitoring exists to detect emergent or worsening disparity; a fairness metric is selected, changed or substituted after subgroup or intersectional results have been seen (a fail on timing alone, whatever the metric shows); or, for a perception component upstream of a customer outcome, the firm's own testing reports its error rates only in aggregate or, where the component applies a decision threshold, as a single error type or at a threshold other than the one configured for deployment, or does not report them.

**Partial** where single-attribute testing is sound and documented but intersectional analysis is absent, or where testing is thorough pre-deployment but no production monitoring continues it. Both are common; name which limb fails.

**Untested perception component.** Where step 13 records the component as untestable, the Pass, Fail or Partial result is reached without the step-13 computation, and the component is reported beside that result as a coverage gap, in the report and in the opinion, in the wording of the canvas's field 14. The untested component does not by itself make the result a Fail or a Partial, and does not make it Not Testable (ASSURANCE_ARCHITECTURE.md, Layer 3); the Fail limb on how the firm's own testing reports the component's error rates still applies.

## 7. Evidence Outputs
- Metric selection rationale recorded before computation — **L2**
- Representativeness assessment of the held-out set — **L2**
- Disaggregated outcome tables with cell sizes, single-attribute and intersectional — **L3**
- Two-metric divergence analysis — **L3**
- Per-subgroup error rates for any perception component in scope, at the threshold configured for deployment where the component applies one, labelled proxy-based where the evaluation set's representativeness is not confirmed — **L3**
- Reviewer's independent disparity assessment against the pre-recorded threshold — **L4**
- Production subgroup monitoring output showing outcomes over time — **L5**

## 8. Common Pitfalls & Limitations
- **Choosing the metric after seeing results.** Fatal to the procedure's credibility. Step 4 exists to make the ordering evidenced.
- **Intersectional cells too small to interpret.** Reporting a 40% disparity computed on nine records as a finding will destroy the credibility of the entire report. Report as untestable.
- **Treating metric divergence as a data problem.** Demographic parity and equalised odds diverging is the expected mathematical outcome, not an error. Document it; do not pick the flattering one.
- **Held-out data that predates the current model.** Score the current production configuration, not an older one.
- **Confusing disparity with discrimination.** The procedure evidences an outcome distribution. Legal characterisation is not the reviewer's output.
- **Missing labels for some characteristics.** Firms typically hold ethnicity and age but not disability or religion. Record which characteristics could not be tested at all — an untested characteristic is a coverage gap, not a pass.

## 9. Time / Effort Estimate
**6 reviewer-days**: 1 day data-protection clearance and dataset acquisition, 1 day representativeness assessment and metric selection, 1.5 days scoring and computation, 1 day intersectional analysis and divergence work, 0.5 day documentation review, 1 day working papers. Add 1 day where a synthetic proxy dataset must be constructed. The estimate does not include step 13; where a perception component is in scope, the reviewer estimates that step's manual-equivalent effort at scoping, discloses it, and adds it to the six days as the procedure's upper bound for that engagement.

---
---

