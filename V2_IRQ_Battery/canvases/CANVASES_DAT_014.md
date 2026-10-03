# CANVAS: IRQ-DAT-014

## 1. IRQ ID & Title
**IRQ-DAT-014: Construct Validity of the Modelled Target Variable**

Register question: "Is the quantity the model is trained or configured to predict or optimise a valid proxy for the substantive construct the decision is actually about — and has proxy validity been tested at subgroup level, including for cases where the historical label itself encodes prior unequal treatment rather than the true outcome of interest?"

## 2. Business Activities Affected
- **Credit and underwriting decisioning:** Models are commonly trained to predict a proxy such as historical arrears, write-off or prior-approval outcomes as a stand-in for "creditworthiness" or "risk" — but where the historical proxy itself reflects prior unequal access to credit rather than the applicant's true repayment capacity, the model inherits and re-encodes that history.
- **Claims triage and case-management prioritisation:** Prioritisation models trained on historical claim spend or prior case-handling intensity as a proxy for "genuine need" or "severity" can systematically under-prioritise a segment for whom less was historically spent for reasons unrelated to actual need.
- **Fraud and conduct-risk scoring:** Models trained on prior enforcement or investigation outcomes as a proxy for "actual misconduct" can encode any historical bias in who was investigated or referred, rather than who actually offended.

## 3. AI Behaviour(s)
- Optimises against whatever target variable it is configured to predict, with no inherent capacity to distinguish a faithful measure of the true construct from a historically biased proxy for it.
- Achieves high, well-calibrated predictive accuracy against the chosen label, which is the metric conventional validation reports.
- Produces no signal that the label itself — rather than the model's fit to it — may be the source of a downstream disparity.

## 4. Failure Mode
> A model is trained or configured to predict a proxy quantity (e.g. historical cost, prior approval, prior enforcement) as a stand-in for the true construct a decision is actually about (e.g. need, creditworthiness, actual misconduct). The model predicts the proxy accurately, with no protected attribute anywhere in its inputs, and passes conventional accuracy validation — but the proxy is itself a biased measure of the true construct because it was generated under a historical process (differential spend, differential access, differential enforcement) that encodes prior unequal treatment, so the model systematically misjudges the true construct for the affected group despite measuring its assigned target correctly.

## 5. Potential Consequences
- **Customer:** A segment historically under-served, under-spent-on or under-enforced against for reasons unrelated to genuine need or risk is systematically mis-scored — denied credit, under-prioritised for case handling, or over- or under-flagged for conduct risk — with no protected attribute or model error to point to.
- **Institution:** Fair-outcomes and non-discrimination findings that conventional feature-level bias testing does not detect, because the disparity originates in the target label, not the feature set; retraining or re-specification of the target variable required once found, not merely re-tuning.
- **Regulator:** Consumer Duty fair-value and fair-treatment findings, and EU AI Act Art. 10 bias-examination and Art. 15 accuracy-maintenance findings, where the firm cannot demonstrate the modelled target was assessed for construct validity independent of feature-level fairness testing.

## 6. Failure Chain
```
A proxy quantity is chosen as the model's training/optimisation target
(historical cost, prior approval, prior enforcement) without a documented
assessment of whether it faithfully represents the true construct
  ↓ (IRQ-DAT-014 — THIS IRQ: construct validity of the target itself
     is not tested)
Historical process that generated the proxy label (differential spend,
access or enforcement) encodes prior unequal treatment into the label
  ↓ (IRQ-DAT-003: even perfect inter-annotator agreement on the label
     as recorded does not catch this — the label is measured accurately
     and is still the wrong construct)
Model is trained/validated against the proxy; reported accuracy is high
because the model predicts the proxy correctly, not because the proxy
is a valid stand-in for the true construct
  ↓ (IRQ-CON-002: feature-level proxy-discrimination testing finds
     nothing, because no protected attribute appears anywhere in the
     pipeline — the defect is in the label, not a feature)
Model deployed; systematically misjudges the true construct for the
affected group in production decisions
  ↓
Fair-outcomes/Consumer Duty finding or discrimination claim surfaces via
outcome-pattern audit, not standard model validation or fairness testing

Control Breakpoints:
  • IRQ-DAT-014: construct-to-target mapping review and subgroup label analysis
  • IRQ-DAT-003: label-quality measurement, extended to ask whether the label
    is the right construct, not only whether it was recorded accurately
  • IRQ-CON-002: feature-level proxy testing, which this IRQ's failure mode
    structurally evades
  • IRQ-CON-001: outcome-level subgroup testing, the point at which this
    failure mode is most likely to actually surface
```

## 7. Why a Domain Expert May Miss It
- Model validation practice checks predictive accuracy against the chosen label almost universally, and essentially never checks whether the label is the right thing to predict — the question "accurate at predicting what?" is not part of conventional validation logic.
- "The label is measured correctly" (IRQ-DAT-003's concern) is easily conflated with "the label is the right thing to measure" (this IRQ's concern); a credit or claims SME who has confirmed the former reasonably assumes the latter is settled too.
- Because no protected attribute appears anywhere in the model's inputs, standard proxy-discrimination and feature-level fairness review finds nothing to flag — the disparity is an emergent property of the target variable, not of any single feature.
- The inversion this IRQ requires — treating the historical outcome label itself as a potential source of bias, rather than as ground truth against which the model is judged — is counter-intuitive to validation practice built around trusting the label.

## 8. Assurance Objective
**AO-DAT-014:** The quantity a model is trained or configured to predict or optimise shall be assessed for construct validity against the decision's true objective, with that assessment including subgroup-level testing of the target label itself — independent of, and prior to, feature-level accuracy or protected-attribute analysis.

## 9. Expected Controls (Traced)
- **Documented construct-to-target mapping and justification** — [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(b) and (f), data governance including examination for possible biases relevant to the intended purpose] — the choice of target variable, and why it was preferred to plausible alternatives, is recorded and reasoned, not assumed.
- **Subgroup-level testing of the label itself, independent of model predictions** — [Obermeyer, Powers, Vogeli & Mullainathan, *Science* 366(6464), 447–453 (2019)] — the label's relationship to the true construct is tested by subgroup, using an independent measure of the construct where one exists, not only the model's fit to the label.
- **Consideration of the label-generation process for embedded prior unequal treatment** — [Obermeyer et al. (2019); linked IRQ-DAT-003] — where a historical label was generated under a process (spend, prior approval, prior enforcement) that could itself encode unequal treatment, that possibility is explicitly assessed rather than assumed away.
- **Independent validation that tests the target variable, not only the model** — [PRA SS1/23, May 2023, Principle 3 (development, implementation and use) and Principle 4 (independent model validation)] — a function independent of development inspects the construct-validity assessment as part of model approval.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the model predicts [outcome] accurately" with no discussion of whether that outcome is the right construct — **L1** (flag: accuracy-only assertion).
- Construct-to-target mapping document: the decision's true objective, the modelled target, the justification for the choice and the alternatives considered — **L2**.
- Subgroup-level label analysis comparing the modelled target against an independent measure of the true construct, where one exists, for the specific model under review — **L3**.
- Independent validation report confirming the construct-validity assessment was inspected, not merely referenced, as part of model approval — **L4**.
- Production outcome monitoring tracking whether subgroup-level disparities predicted by a construct-validity concern materialise in deployed decisions — **L5**.

## 11. Independent Test
> In a non-production environment, require the firm to produce the construct-to-target mapping and its documented justification for the model under review, and to run a subgroup-level analysis of the target label — comparing it, where an independent measure of the true construct exists, against that measure rather than against the model's predictions of the label. No re-derivation of the model itself is required; the test is a review of the target variable and its label, not a re-run of model training. **No FAIAS-standard acceptance threshold exists for this test; the published methodology it draws on is domain-specific (developed and validated for one construct in one sector) and must be adapted to the construct and sector under review, not applied off the shelf.** — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (a rigorous, peer-reviewed, replicated methodology exists and is directly transferable in logic — compare model output, or the target label itself, against an independent, unbiased measure of the true construct rather than against the proxy label alone — but it was developed and validated in one domain, and no settled financial-services equivalent, benchmark or acceptance threshold exists).

## 12. Pass Indicators
- A documented construct-to-target mapping exists for the model under review, with the choice of target variable justified against the decision's true objective and against plausible alternatives.
- Subgroup-level label analysis finds no material divergence between the modelled target and an independent measure of the true construct, where one exists.
- Where the target label derives from a historical process (spend, prior approval, prior enforcement) capable of encoding unequal treatment, that possibility has been explicitly assessed and, if found, addressed.
- Independent validation confirms the construct-validity assessment was inspected as part of model approval, not assumed.

## 13. Fail Indicators
- No construct-to-target mapping or justification exists; the target variable was chosen without documented consideration of alternatives or of its relationship to the true construct.
- Subgroup-level label analysis finds a material divergence between the modelled target and an independent measure of the true construct for one or more segments, with no remediation.
- The target label derives from a historical process capable of encoding unequal treatment, and that possibility was not assessed.
- Model approval relied on accuracy-against-label alone, with no evidence the label itself was examined.

## 14. Reporting Language
**Pass:** "A documented construct-to-target mapping exists for [model], justifying the choice of modelled target against the decision's true objective. Subgroup-level label analysis found no material divergence between the modelled target and an independent measure of the true construct. This is a ★2 professional assessment: the underlying methodology is well-established and peer-reviewed but developed in a different domain, and no financial-services-specific acceptance threshold exists."

**Fail:** "No construct-to-target mapping exists for [model]; the target variable was adopted without documented assessment of whether it is a valid proxy for the decision's true objective. Subgroup-level label analysis found [x]% divergence between the modelled target and an independent measure of the true construct, concentrated in [segment]. Because no protected attribute appears in the model's inputs, this disparity would not have been detected by standard feature-level fairness testing. The model's reported accuracy cannot be relied upon as evidence of fair treatment until the target variable is re-assessed and, if found biased, re-specified."

**Partial:** "A construct-to-target mapping exists for the primary decisioning model but has not been extended to [related model/product line], which shares the same target-variable logic and accounts for [x]% of the affected decision volume. Extend subgroup-level label analysis to that scope before the assurance objective is considered met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (systematic mis-scoring of a segment on the decision's true construct;
              Consumer Duty and fair-treatment exposure)
  Likelihood: 2 (requires the construct-to-target mapping and subgroup label analysis
              to be skipped or superficial, plausible but not the default where MRM
              discipline is otherwise mature)
  Detectability: 3 (invisible to standard feature-level fairness testing by construction;
              surfaces via deliberate subgroup label analysis or outcome-pattern audit)
  Recoverability: 2 (correctable via target re-specification and retraining, though this
              is a governance decision, not a tuning exercise)
  Novelty: 4 (the inversion — questioning whether the target itself is the right thing to
              predict, not just whether the model predicts it accurately — sits outside
              conventional model validation intuition entirely)

If controls are absent or degraded:
  Severity: 4 (systematic, scaled mis-scoring of a segment on the substantive decision,
              with no protected attribute or feature to point to; can affect a large
              proportion of a portfolio before discovery)
  Likelihood: 3 (target-variable choice is rarely subjected to construct-validity review
              under current conventional practice, making the gap a foreseeable default
              rather than an edge case)
  Detectability: 4 (silent by construction — accuracy metrics look strong precisely
              because the model is measuring its assigned proxy correctly; discovery
              requires deliberate subgroup label analysis, not routine monitoring)
  Recoverability: 3 (requires re-specifying the target variable, retraining, and
              retrospective review of affected decisions — not a parameter adjustment)
  Novelty: 4
Residual risk: Critical where the target variable feeds a consequential, high-volume
decision (credit, claims, enforcement) and no construct-validity assessment has ever
been performed; the failure is structurally invisible to every other fairness control
in the register.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Systematic mis-scoring of a segment on the decision's true construct, with Consumer Duty and fair-treatment exposure, despite no protected attribute or feature-level defect. |
| **Likelihood** | 2 | Plausible where construct-validity review of the target variable is skipped, which is common given it sits outside conventional validation practice, but not universal. |
| **Detectability** | 4 | Structurally invisible to feature-level fairness and proxy-discrimination testing; requires a dedicated subgroup label analysis to surface at all. |
| **Recoverability** | 2 | Correctable via target re-specification and retraining once identified, though this is a governance decision rather than a tuning exercise. |
| **Novelty** | 4 | Questioning the target label itself, rather than the model's fit to it, inverts the normal logic of model validation and is well outside conventional FS domain-expert practice. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(b) and (f)] requires data governance measures including examination of training, validation and testing datasets for possible biases likely to affect the health, safety or fundamental rights of persons, or lead to discrimination, in light of the intended purpose of the AI system — a requirement this IRQ operationalises specifically at the level of the target variable rather than the feature set. [PRA SS1/23, May 2023, effective 17 May 2024, Principle 3 (development, implementation and use) and Principle 4 (independent model validation)] require the data basis of a model — which includes the target variable it is trained to predict — to be evidenced and independently checked. [FCA, PRIN 2A Consumer Duty, in force 31 July 2023, the cross-cutting obligations (PRIN 2A.2) and the price and value outcome (PRIN 2A.4)] is engaged where a target-variable choice produces systematically worse outcomes for a segment, independent of whether any individual feature or protected attribute is implicated. No regulation names "construct validity of the target variable" explicitly; this IRQ operationalises the above general data-governance and fair-treatment principles for this specific, AI-relevant failure mode. (verified 1 Aug 2026)

## 18. Research Basis
> [Obermeyer, Z., Powers, B., Vogeli, C., Mullainathan, S., 2019. "Dissecting racial bias in an algorithm used to manage the health of populations." *Science* 366(6464), 447–453. DOI: 10.1126/science.aax2342.] — verified finding: a widely deployed healthcare-management algorithm used historical healthcare cost as a proxy for healthcare need; because less was spent on Black patients with the same level of underlying need, the algorithm concluded — with no protected attribute in the model and no data error — that Black patients were healthier than equally sick white patients, reducing the number identified for extra care by more than half at matched risk scores. This is the strongest available public anchor for a proxy-label bias mechanism operating with no protected attribute and no data error, and it is the direct basis for the review methodology in Field 11 above. No financial-services-specific peer-reviewed study of construct-validity testing for modelled target variables was located; this is a genuine research gap for the sector, not filled with an unrelated citation — the methodology is adapted from Obermeyer et al. by logical transfer, not by a sector-matched precedent.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-003 (A.1: label quality — measures whether the recorded label is accurate;
    this IRQ asks the prior question of whether the label is the right construct at all)
  - IRQ-CON-002 (H.1: feature-level proxy discrimination — tests whether a feature proxies
    a protected characteristic; this IRQ tests whether the target label itself proxies the
    wrong construct, which can produce disparity with no protected attribute anywhere in
    the pipeline)
  - IRQ-CON-001 (H.1: subgroup/intersectional outcome testing — the point at which this
    failure mode is most likely to surface in practice, at the outcome level)
  - IRQ-MOD-007 (B.4: specification gaming — covers the model's optimisation diverging from
    a correctly specified metric; this IRQ covers the metric being mis-specified from the
    outset, a distinct and prior failure mode)
```

## 20. References
```
[1] Obermeyer, Z., Powers, B., Vogeli, C., Mullainathan, S., 2019. "Dissecting racial bias
    in an algorithm used to manage the health of populations." Science 366(6464), 447-453.
    DOI: 10.1126/science.aax2342.
[2] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10.
[3] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[4] FCA, 2022. "PS22/9: A New Consumer Duty." PRIN 2A in force 31 July 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Model validation practice checks predictive accuracy against the
  chosen label almost universally, and essentially never checks whether the label is the
  right thing to predict — the target variable itself sits outside conventional review scope.
✓ Test 2 (Plausible Harm): Grounded in a peer-reviewed, replicated study (Obermeyer et al.,
  Science, 2019) demonstrating the exact mechanism — proxy-label bias with no protected
  attribute and no data error — in a directly analogous setting; this is precisely the
  failure mode a fair-outcomes claim must guard against, and no existing IRQ tests the
  target label rather than the feature set.
✓ Test 3 (Testable): Construct-to-target mapping review and subgroup label analysis on a
  held-out sample are executable in non-production, requiring no model re-derivation. ★2.
✓ Test 4 (Decision-Relevant): A target-variable choice that fails this test cannot be
  corrected by better model fitting; it requires re-specifying what is being predicted, which
  is a governance decision, gating model approval rather than a tuning exercise.

Change Log:
- v1.0 (2026-08-01): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

