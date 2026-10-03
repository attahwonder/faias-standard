# CANVAS: IRQ-DAT-003

## 1. IRQ ID & Title
**IRQ-DAT-003: Insufficient Ground-Truth Label Quality for Fine-Tuning and Validation**

Register question: "Are ground-truth labels used for fine-tuning or validation of demonstrably sufficient quality, with inter-annotator agreement and error rates measured and bounded?"

## 2. Business Activities Affected
- **Credit and underwriting model fine-tuning:** Labels driving fine-tuning (e.g. "good outcome"/"bad outcome" annotations, affordability judgements) directly shape what the model learns to optimise for.
- **Content moderation and complaint triage:** Human-labelled examples for classifying complaint severity or vulnerability indicators; label noise here propagates into systematically wrong triage.
- **Model validation datasets:** Held-out evaluation sets used to approve a model rely on labels being at least as reliable as the model being judged against them.

## 3. AI Behaviour(s)
- Fine-tunes on human- or vendor-annotated examples, treating labels as ground truth regardless of underlying annotator disagreement.
- Is validated against held-out labelled sets whose own error rate is rarely disclosed alongside the model's reported accuracy.
- Can encode systematic labeller bias (e.g. consistent mis-scoring of a customer segment) as if it were the correct target function.

## 4. Failure Mode
> The firm fine-tunes or validates a model against labels whose inter-annotator agreement and error rate are unmeasured or undisclosed, so reported model accuracy may reflect agreement with noisy or systematically biased labels rather than true task performance.

## 5. Potential Consequences
- **Customer:** Model trained to replicate a labelling error pattern (e.g. consistent under-scoring of a demographic segment's affordability) produces systematically wrong decisions.
- **Institution:** Approval decisions rest on an accuracy figure that overstates true performance; MRM validation is not evidence-based if label quality is unmeasured.
- **Regulator:** EU AI Act Art. 10 data-quality obligations and PRA SS1/23 validation principles are not satisfiable without label-quality evidence.

## 6. Failure Chain
```
Labels produced by internal staff, crowdworkers, or vendor annotators
without inter-annotator agreement (IAA) measurement
  ↓ (IRQ-DAT-003 — THIS IRQ: label quality unquantified)
Model fine-tuned/validated against these labels; reported accuracy
reflects agreement with noisy or biased ground truth
  ↓ (IRQ-MOD-011: evaluation evidence contaminated by unreliable labels)
Model approved on an inflated or misleading performance claim
  ↓ (IRQ-GOV-007: independent validation does not test label reliability)
Systematic decision errors replicate the underlying labelling bias
  ↓
Customer harm at scale; discovered only via outcome-level audit or complaint pattern

Control Breakpoints:
  • IRQ-DAT-003: IAA measurement and error-rate bounding at label production
  • IRQ-MOD-011: evaluation integrity checks that labels themselves are reliable
  • IRQ-GOV-007: independent validation tests the ground truth, not just the model
```

## 7. Why a Domain Expert May Miss It
- Credit risk SMEs are trained to validate model output against known outcomes, not to question whether the "known outcome" labels themselves were reliably produced.
- Vendor-annotated datasets are treated as a black-box input; contracts rarely require disclosure of IAA statistics (links IRQ-TPR-002).
- "High accuracy against test set" is read as an unambiguous quality signal; the possibility that the test set itself is noisy or biased is a non-obvious inversion of the usual validation logic.
- Crowdsourced or outsourced labelling pipelines can embed systematic bias (e.g. cultural interpretation differences) invisible without demographic stratification of IAA.

## 8. Assurance Objective
**AO-DAT-003:** Ground-truth labels used for model fine-tuning or validation shall have measured inter-annotator agreement and bounded error rates, disclosed alongside any model performance claim that depends on them.

## 9. Expected Controls (Traced)
- **Inter-annotator agreement measurement** — [established annotation-quality practice; ISO/IEC TS 4213:2022, assessment of ML classification performance] — Cohen's/Fleiss' kappa or equivalent computed and reported for every labelled dataset used in fine-tuning/validation.
- **Label error-rate sampling and adjudication** — [ISO/IEC TS 4213:2022] — a sample of labels independently re-annotated and discrepancies adjudicated; error rate bounded and documented.
- **Label-quality disclosure in model documentation** — [NIST AI RMF 1.0, MEASURE function; PRA SS1/23 development principle] — reported accuracy figures accompanied by the label quality they rest on.
- **Stratified IAA by customer segment** — [Emerging Practice — no single published FS standard; grounded in general fairness-in-labelling literature] — checks that label reliability does not vary systematically by protected or vulnerable segment.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "labels were reviewed for quality" with no metric — **L1**.
- Labelling guideline and IAA measurement methodology document — **L2**.
- IAA statistics computed for the specific dataset used in the current model's fine-tuning/validation — **L3**.
- Independent re-annotation audit sample with adjudicated error rate, performed by a party independent of the original labelling — **L4**.
- Production-tracked labelling QA metrics over time for an ongoing annotation pipeline (vendor scorecards, rolling IAA) — **L5**.

## 11. Independent Test
> In a non-production setting, draw a stratified random sample of labelled examples from the training/validation set (including by customer segment where feasible). Have two or more independent, blinded annotators re-label the sample using the documented guidelines; compute inter-annotator agreement (e.g. Cohen's kappa) between the independent annotators and against the original labels. Compare model-reported accuracy against label-quality-adjusted accuracy. Methodology follows standard annotation-quality practice (no single FS-specific published benchmark). — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (research-grounded general method exists; test design — sample size, adjudication protocol, segment stratification — is bespoke to the firm and requires professional judgement; no cross-institution consensus benchmark for FS label-quality thresholds).

## 12. Pass Indicators
- IAA statistics exist and meet a documented, justified threshold (e.g. kappa ≥ 0.6) for every labelled set feeding fine-tuning or validation.
- Label error-rate sampling shows no material discrepancy against independent re-annotation.
- Stratified IAA shows no segment with materially lower label reliability.
- Model documentation discloses label quality alongside accuracy claims.

## 13. Fail Indicators
- No IAA statistic exists for the labels underpinning a current model approval.
- Independent re-annotation reveals a materially different label distribution from the original.
- A specific customer segment shows systematically lower label agreement, unflagged in validation.
- Vendor labelling contracts contain no quality-disclosure obligation and no data is available to test it.

## 14. Reporting Language
**Pass:** "Inter-annotator agreement for the labelled dataset underpinning [model]'s fine-tuning and validation was independently measured at [kappa value], meeting the firm's documented threshold; a stratified re-annotation sample found no segment-level reliability gap. Model performance claims are supported by label-quality evidence, not assumed reliability (★2 professional assessment)."

**Fail:** "No inter-annotator agreement statistic exists for the labels used to validate [model]. Independent re-annotation of a sample found [x]% disagreement with the original labels, concentrated in [segment]. The model's reported accuracy cannot be relied upon as a measure of true task performance until label quality is established and, where segment-level bias is found, remediated."

**Partial:** "Label-quality measurement exists for the primary training set but not for the smaller supplementary set covering [segment/product line], which accounts for [x]% of fine-tuning examples. Extend IAA measurement before treating validation as complete."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (single-segment or moderate accuracy overstatement; correctable via re-labelling)
  Likelihood: 2 (plausible where annotation QA is informal, which is common)
  Detectability: 3 (surfaces via periodic audit or outcome-pattern review, not real time)
  Recoverability: 2 (re-labelling and retraining feasible within weeks)
  Novelty: 3 (the inversion — questioning the ground truth rather than the model — is counter-intuitive to SMEs)

If controls are absent or degraded:
  Severity: 3 (systematic segment-level decision errors at scale; regulatory notice risk)
  Likelihood: 3 (label-quality measurement is frequently skipped under delivery pressure)
  Detectability: 4 (invisible without deliberate re-annotation audit; not visible in standard accuracy metrics)
  Recoverability: 2 (correctable but requires re-labelling and retraining cycle)
  Novelty: 3
Residual risk: moderate-to-high without measurement discipline; compounds into fairness findings (link IRQ-CON-001).
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Systematic decision errors replicating labeller bias can affect a customer segment at scale. |
| **Likelihood** | 2 | Plausible where annotation QA is informal; not universal given growing MRM scrutiny. |
| **Detectability** | 3 | Requires deliberate re-annotation audit; invisible in standard accuracy dashboards. |
| **Recoverability** | 2 | Correctable via re-labelling and retraining within a defined cycle. |
| **Novelty** | 3 | Counter-intuitive to SMEs trained to trust ground truth as fixed; an AI-validation-specific blind spot. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(3)] requires training, validation and testing datasets to be relevant, sufficiently representative and, to the best extent possible, free of errors. [PRA SS1/23, May 2023, Principle 3 (development, implementation and use) and Principle 4 (independent model validation)] require evidence that data underpinning a model (including labels) is fit for purpose. (verified 29 Jul 2026)

## 18. Research Basis
> [ISO/IEC TS 4213:2022, "Assessment of machine learning classification performance"] — statistical methods for classifier assessment, extendable to label-quality measurement. No FS-specific peer-reviewed study of inter-annotator agreement practice in credit/insurance labelling was located in the source registers; this reflects a genuine research gap for the FS domain — flagged [UNVERIFIED — no FS-specific peer-reviewed study located; ISO/IEC TS 4213:2022 confirmed as a general (non-FS) statistical-assessment reference] (verified 29 Jul 2026) rather than filled with an unrelated citation.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-MOD-011 (B.5: evaluation integrity — contaminated ground truth undermines approval evidence)
  - IRQ-GOV-007 (I.3: independent validation must test label reliability, not just model output)
  - IRQ-CON-001 (H.1: segment-level labelling bias surfaces as outcome discrimination)
  - IRQ-TPR-002 (F.1: vendor annotation contracts should secure quality-disclosure rights)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10(3).
[2] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
[3] ISO/IEC, 2022. "ISO/IEC TS 4213:2022 — Assessment of machine learning classification performance."
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Credit SMEs validate the model against ground truth, not the
  ground truth itself — a genuine inversion of normal validation logic.
✓ Test 2 (Plausible Harm): Grounded in annotation-quality standards (ISO/IEC TS 4213:2022);
  mechanism of harm (label bias replication) is well established in ML practice.
✓ Test 3 (Testable): Independent re-annotation sampling is executable in non-production. ★2.
✓ Test 4 (Decision-Relevant): Gates whether reported model accuracy can be relied upon for approval.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

