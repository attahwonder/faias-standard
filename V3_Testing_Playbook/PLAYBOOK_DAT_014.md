# TP-DAT-014 — Construct-to-Target Mapping Review and Subgroup Label Analysis

**Procedure ID:** TP-DAT-014
**IRQ:** IRQ-DAT-014 — Construct Validity of the Modelled Target Variable
**Assurance objective:** AO-DAT-014 — the quantity a model is trained or configured to predict or optimise shall be assessed for construct validity against the decision's true objective, with that assessment including subgroup-level testing of the target label itself — independent of, and prior to, feature-level accuracy or protected-attribute analysis.
**★ Confidence:** ★2 (carried from canvas — see canvas §11 for the full derivation. Summary: a rigorous, peer-reviewed, replicated methodology exists and is directly transferable in logic — compare model output, or the target label itself, against an independent, unbiased measure of the true construct rather than against the proxy label alone — but it was developed and validated in one domain, and no settled financial-services equivalent, benchmark or acceptance threshold exists.)
**Method classification:** Adapted Industry Practice — the proxy-label bias methodology of Obermeyer et al. (2019), as cited in the canvas, adapted by logical transfer to the construct and sector under review rather than by a sector-matched precedent. The canvas records that **no financial-services-specific peer-reviewed study of construct-validity testing for modelled target variables was located**, and is explicit that the published methodology is domain-specific — developed and validated for one construct in one sector — and must be adapted, not applied off the shelf. The adaptation made is recorded as part of the evidence.

## Preconditions

- **Environment:** non-production. The procedure reviews the target variable and its label; **no re-derivation or retraining of the model is required**, and none is performed. Analysis runs on a held-out or historical non-live sample approved for test use.
- **Access needed:** the model's target-variable specification and any construct-to-target mapping the firm holds; the labelled dataset underpinning the current approval, at a granularity permitting subgroup analysis; an independent measure of the true construct where one exists in the firm's own data or in a lawfully available external source; the model documentation carrying the accuracy claim; the independent validation report supporting model approval.
- **Artefacts requested in advance (2 weeks):** the construct-to-target mapping and its justification, including alternatives considered; a description of the process that generated the historical label (spend, prior approval, prior enforcement) and its date range; any existing subgroup-level analysis of the label as distinct from the model's predictions; the independent validation report; production outcome-monitoring definitions for subgroup tracking; segment metadata sufficient to stratify, where lawfully available for this purpose.
- **Personnel:** reviewer (lead); the model development or data-science function, to produce the mapping and its justification and to compute the label analysis; the independent validation function, for the approval-inspection limb; a domain practitioner able to speak to what the decision's true objective actually is and to identify any independent measure of it; **privacy sign-off for any segment stratification**, following TP-DAT-003's precedent for the same requirement.
- **Dependency:** where TP-DAT-003 (label quality) is also in scope, run it first or alongside. The two questions are adjacent and distinct — TP-DAT-003 asks whether the label was *recorded accurately*, this procedure asks whether it is *the right construct at all* — and the canvas is explicit that perfect inter-annotator agreement does not catch this failure mode.

## Test design

- **Limb 1 — construct-to-target mapping review.** Establish whether a documented mapping exists for the model under review: the decision's true objective, the modelled target, the justification for choosing it, and the plausible alternatives considered. Absence is itself a canvas fail indicator, distinct from a mapping that exists and is weak.
- **Limb 2 — label-generation process review.** Where the target label derives from a historical process capable of encoding prior unequal treatment — differential spend, differential access or prior approval, differential enforcement or investigation — establish whether that possibility was explicitly assessed, and if found, addressed. The canvas's fail condition is that the possibility "was not assessed", not that it was assessed and dismissed.
- **Limb 3 — subgroup-level label analysis.** The firm runs a subgroup-level analysis of the target label, comparing it — **where an independent measure of the true construct exists** — against that measure, rather than against the model's predictions of the label. The reviewer reviews the design, the independent measure chosen, and the result. **Where no independent measure exists, limb 3 cannot run as specified:** record the absence, narrow the conclusion to limbs 1, 2 and 4, and state the limitation. Do not substitute the model's predictions as the comparator.
- **Limb 4 — approval-inspection check.** Establish whether independent validation inspected the construct-validity assessment as part of model approval, or merely referenced it, or relied on accuracy-against-label alone.
- **Adaptation record.** The published methodology is domain-specific. The reviewer documents the adaptation made to the construct and sector under review, fixed **before** limb 3 is computed, per the canvas's instruction that the methodology must not be applied off the shelf. That record is what makes the transfer defensible.
- **What this procedure deliberately does not do.** It does not run feature-level proxy-discrimination testing (IRQ-CON-002) or outcome-level subgroup testing (IRQ-CON-001). The canvas's whole point is that this failure mode structurally evades the first and surfaces, if at all, only at the second. Reporting must not let a clean feature-level result stand in for this one.
- **Benign-payload principles:** not applicable — no adversarial content. The governing safety rule is data handling: anonymised, synthetic or approved non-live extracts only, with segment metadata handled under the privacy sign-off obtained at preconditions.

## Steps

1. Request the construct-to-target mapping and its justification for the model under review. **Record:** the mapping as provided, whether it is dated, the alternatives it records as considered, or the fact that no mapping exists.
2. Establish the decision's true objective independently, from the product or process documentation and from the domain practitioner, **before** reading the firm's justification. **Record:** the objective as independently derived, and any divergence from the firm's stated objective.
3. Identify the process that generated the historical target label and its date range. **Record:** the process, and whether it is of a type capable of encoding prior unequal treatment (spend, prior approval, prior enforcement).
4. Establish whether the firm assessed that possibility. **Record:** the assessment, or its documented absence.
5. Identify with the domain practitioner whether an independent measure of the true construct exists in the firm's data or in a lawfully available source. **Record:** the measure and its provenance, or the fact that none exists — the latter bounds every conclusion that follows.
6. Document the adaptation of the published methodology to this construct and sector. **Record:** the adaptation note, fixed and timestamped before computation.
7. Review the design of the subgroup-level label analysis before results are seen: strata, cell sizes, the comparator used, and whether the comparison is against the independent measure or merely against model predictions. **Record:** the design and any defect in it.
8. Obtain and review the subgroup-level analysis results. **Record:** per-subgroup divergence between the modelled target and the independent construct measure, with the direction of divergence, cell sizes and the segments affected. Where limb 3 was infeasible, record the limitation and confine the label question to step 4's process assessment.
9. Where a material divergence is found, establish whether it has been remediated, and how. **Record:** the remediation, or its absence.
10. Inspect the independent validation record for evidence that the construct-validity assessment was examined rather than referenced. **Record:** the evidence, or that approval relied on accuracy-against-label alone.
11. Review production outcome monitoring. **Record:** whether subgroup-level disparities predicted by a construct-validity concern would surface in deployed decisions, or whether discovery would depend on an external outcome-pattern audit.
12. Establish whether the same target-variable logic is used by any related model or product line outside the scope of the assessment. **Record:** the scope of related use and the proportion of affected decision volume it represents — this is the canvas's own partial-result shape.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Documented construct-to-target mapping exists, with the target justified against the decision's true objective and against plausible alternatives | Exists and is justified (canvas pass indicator); absence is a canvas fail indicator | Canvas |
| Subgroup-level divergence between the modelled target and an independent measure of the true construct | **No material divergence** (canvas pass indicator). Materiality is **reviewer judgement — no established threshold**; the canvas states plainly that no FS acceptance threshold exists and that the published methodology is domain-specific | Canvas; Obermeyer et al. (2019) as cited in the canvas |
| Label-generation process assessed for embedded prior unequal treatment, where the label derives from spend, prior approval or prior enforcement | Explicitly assessed and, if found, addressed (canvas pass indicator) | Canvas |
| Independent validation inspected the construct-validity assessment at approval | Inspected, not merely referenced or assumed (canvas pass indicator) | Canvas; PRA SS1/23 Principles 3 and 4 as cited in the canvas |
| Availability of an independent measure of the true construct | Where none exists, report the label question as unresolved rather than passed | Canvas — the test is conditional on such a measure existing |

## Interpretation

- **Pass** — a documented construct-to-target mapping exists for the model under review, justified against the decision's true objective and against plausible alternatives; subgroup-level label analysis finds no material divergence between the modelled target and an independent measure of the true construct, where one exists; where the label derives from a historical process capable of encoding unequal treatment, that possibility was explicitly assessed and, if found, addressed; independent validation confirms the assessment was inspected at approval.
- **Fail** — no mapping or justification exists and the target was chosen without documented consideration of alternatives or of its relationship to the true construct; **or** subgroup-level analysis finds material divergence for one or more segments with no remediation; **or** the label derives from a process capable of encoding unequal treatment and that possibility was never assessed; **or** approval rested on accuracy-against-label alone with no evidence the label itself was examined.
- **Partial** — the canvas's own shape: a mapping exists for the primary decisioning model but has not been extended to a related model or product line sharing the same target-variable logic. Report the proportion of affected decision volume that is uncovered, and extend the subgroup-level label analysis to that scope before the assurance objective is considered met. Also partial where no independent measure of the true construct exists — in that case the mapping and process limbs may pass while the label-analysis limb is unresolved, and the report must say which.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Statement that the model predicts its outcome accurately, with no discussion of whether that outcome is the right construct | **L1** (flag: accuracy-only assertion) |
| Construct-to-target mapping document: true objective, modelled target, justification, alternatives considered | L2 |
| Label-generation process description and the firm's assessment of embedded prior unequal treatment | L2 |
| Reviewer's independently derived statement of the decision's true objective, recorded before the firm's justification was read | L3 |
| Methodology adaptation note, fixed and timestamped before computation | L3 |
| Subgroup-level label analysis against an independent measure of the true construct, for the specific model under review | **L3** |
| Independent validation report confirming the construct-validity assessment was inspected, not merely referenced, at approval | **L4** |
| Production outcome monitoring tracking whether subgroup-level disparities predicted by a construct-validity concern materialise in deployed decisions | L5 |

## Common pitfalls & limitations

- **Accepting "the label is measured correctly" as an answer to this question.** It answers TP-DAT-003's question. A label can be recorded with perfect agreement and still be the wrong construct; the canvas makes this the central distinction.
- **Using the model's own predictions as the comparator.** That measures fit, not construct validity, and reproduces the failure mode under test. The comparator must be an independent measure of the true construct, and where there is none the question is unresolved.
- **Reading the firm's justification first.** It anchors the reviewer to the firm's framing of the decision's objective. Step 2 exists to prevent that and must precede any review of the artefact requested at step 1.
- **Treating a clean feature-level fairness result as coverage.** By construction this failure mode produces disparity with no protected attribute anywhere in the pipeline, so proxy-discrimination testing finds nothing. A clean IRQ-CON-002 result is not evidence here and must not be reported as though it were.
- **Applying the published methodology off the shelf.** It was developed and validated for one construct in one sector; step 6's adaptation record is what makes the transfer defensible.
- **Manufacturing a comparator where none exists.** Where no independent measure of the true construct is available, limb 3 does not run; report the narrower conclusion and the limitation.
- **Under-powered strata.** Subgroup divergence computed on a handful of cases is noise. Either power the strata or report the subgroup question as unresolved, following the existing DAT convention.
- **Canvas limitation carried forward:** no FAIAS-standard acceptance threshold exists for this test, and the published methodology it draws on was developed and validated for one construct in one sector. It must be adapted to the construct and sector under review, not applied off the shelf. ★2 — professional assessment per METHODOLOGY_STANDARDS §3c.
- **A failed result is not a tuning finding.** The canvas is explicit: a target-variable choice that fails this test cannot be corrected by better model fitting; it requires re-specifying what is being predicted, which is a governance decision. Report it as gating model approval, not as a calibration item.

## Time/effort estimate

**4 reviewer-days** (0.5 independent derivation of the decision's true objective and domain-practitioner session; 0.5 mapping and justification review; 0.5 label-generation process review; 0.5 independent-measure identification and adaptation record; 1.5 subgroup label-analysis design review and results analysis; 0.5 approval-inspection, monitoring and related-scope limbs and reporting). Excludes the firm's own effort in running the subgroup analysis, costed separately.

