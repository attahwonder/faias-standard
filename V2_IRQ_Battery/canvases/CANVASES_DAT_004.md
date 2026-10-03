# CANVAS: IRQ-DAT-004

## 1. IRQ ID & Title
**IRQ-DAT-004: Undeclared or Unvalidated Synthetic Data Concealing Rare Events and Subgroups**

Register question: "Is synthetic data identifiable as such within corpora, with generation method and proportion documented — and does validation demonstrate it preserves rare events, minority subgroups and real-world complexity rather than concealing them?"

## 2. Business Activities Affected
- **Fraud and AML model training:** Synthetic data is routinely used to augment rare fraud/typology examples; if generation smooths away the tail behaviour that defines those events, the model trains on a sanitised fiction.
- **Underrepresented-segment model development:** Synthetic augmentation used to "balance" thin-file or minority-segment data can inadvertently homogenise those segments rather than genuinely representing their diversity.
- **Testing and validation datasets:** Synthetic test data standing in for real customer data must preserve edge cases, or validation results overstate real-world robustness.

## 3. AI Behaviour(s)
- Trains on a blend of real and synthetic examples without any inherent signal distinguishing which is which.
- Learns whatever distribution the synthetic generator produces — including its systematic simplifications, mode collapse toward "typical" cases, and loss of tail diversity.
- Presents validation performance that reflects the (possibly sanitised) synthetic distribution rather than true operating conditions.

## 4. Failure Mode
> Synthetic data is incorporated into training or validation corpora without being labelled as synthetic, without documented generation method and proportion, and without validation that it preserves rare events, minority-subgroup characteristics and real-world complexity — so the model is trained and evaluated against a smoothed fiction that under-represents exactly the tail cases assurance most depends on.

## 5. Potential Consequences
- **Customer:** A rare-but-real fraud typology, or a minority-subgroup pattern, is under-represented in training, degrading model performance precisely for the cases where errors matter most.
- **Institution:** False confidence from validation metrics computed on synthetic data that conceals tail complexity; undetected until a real-world rare event is mishandled.
- **Regulator:** EU AI Act Art. 10 representativeness requirements are not met if synthetic augmentation is undisclosed and unvalidated for fidelity.

## 6. Failure Chain
```
Synthetic data generated to augment thin or imbalanced real data
(rare fraud cases, minority segments) without fidelity validation
  ↓ (IRQ-DAT-004 — THIS IRQ: generation smooths tails/subgroups; not flagged as synthetic)
Blended corpus used for training and/or validation without provenance tags
  ↓ (IRQ-MOD-011: evaluation integrity — validation metrics reflect sanitised distribution)
Model appears to perform well on tail cases in testing but has not seen
their true complexity
  ↓ (IRQ-DAT-005: representativeness gap compounds with under-representation elsewhere)
Real rare event or minority-segment case occurs in production;
model mishandles it
  ↓
Missed fraud/AML typology, or discriminatory outcome for minority segment
→ financial loss or Consumer Duty/fairness finding

Control Breakpoints:
  • IRQ-DAT-004: synthetic data labelling, generation-method documentation, fidelity validation
  • IRQ-MOD-011: evaluation integrity checks distinguish real vs synthetic validation performance
  • IRQ-DAT-005: representativeness assessment against the deployed population
```

## 7. Why a Domain Expert May Miss It
- Fraud/AML SMEs know synthetic augmentation is used for rare-event balancing but rarely ask whether the generator itself preserves tail structure — the intuition is "more examples = better," not "are these examples faithful?"
- Synthetic data is often invisible in the final blended corpus; without an explicit provenance tag, nobody downstream can distinguish it from real data during review.
- Validation performance looking strong on synthetic tail cases is read as reassurance, when it may actually mean the tail cases were made easier by the generation process (a form of the evaluation-integrity trap in IRQ-MOD-011).
- Generative-model mode collapse and diversity loss are ML-research findings, not intuitions available to a credit or fraud SME.

## 8. Assurance Objective
**AO-DAT-004:** Synthetic data used in training, fine-tuning or validation corpora shall be identifiable as such, with generation method and proportion documented, and shall be validated to demonstrate preservation of rare events, minority-subgroup characteristics and real-world complexity before use.

## 9. Expected Controls (Traced)
- **Synthetic-data provenance tagging** — [EU AI Act, Regulation (EU) 2024/1689, Art. 10 data governance] — every record's real/synthetic origin and generation method recorded in the data registry.
- **Fidelity validation against real-distribution tail statistics** — [Shumailov et al., 2024, Nature, "AI models collapse when trained on recursively generated data"; Alemohammad et al., 2023, "Self-Consuming Generative Models Go MAD"] — synthetic augmentation validated to confirm it does not erode distributional tails relative to the real reference population.
- **Segment-stratified representativeness testing** — [linked IRQ-DAT-005; ISO/IEC TR 24027:2021 bias measurement] — synthetic augmentation of minority segments tested for preserved within-segment diversity, not homogenised replacement.
- **Accumulation over replacement in synthetic augmentation strategy** — [Gerstgrasser et al., 2024, "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Data"] — synthetic data supplements rather than replaces real data in training mixes, per the documented mitigation for collapse-type degradation.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "synthetic data is used to balance rare classes" with no fidelity evidence — **L1**.
- Data generation methodology document (generator type, proportion, target classes) — **L2**.
- Statistical fidelity comparison: tail-distribution and subgroup-diversity metrics, synthetic vs real reference population — **L3**.
- Independent audit of synthetic-data fidelity validation methodology and results — **L4**.
- Production outcome monitoring showing model performance on genuinely rare real-world events post-deployment, compared against the synthetic-trained expectation — **L5**.

## 11. Independent Test
> In a non-production environment, compare the statistical properties (distributional tails, subgroup diversity, rare-event feature combinations) of the synthetic augmentation set against a held-out real reference sample covering the same classes. Measure whether synthetic examples cluster toward "typical" cases (mode collapse) or preserve the variance and rare-event structure of the real distribution. Where feasible, evaluate model performance on real (not synthetic) rare-event holdout cases separately from synthetic-holdout performance. Methodology informed by Shumailov et al. (2024) and Alemohammad et al. (2023) collapse-detection approaches, adapted to a discriminative FS use case rather than the generative-model setting those papers study directly. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (research base is strong but developed for recursive generative-model collapse, not FS tabular/text fine-tuning augmentation specifically; test design requires significant adaptation and professional judgement).

## 12. Pass Indicators
- All synthetic records are tagged and traceable to a documented generation method and proportion.
- Fidelity comparison shows no material tail-distribution or subgroup-diversity loss versus the real reference sample.
- Model performance on real rare-event holdout data is not materially worse than on synthetic rare-event holdout data.
- Synthetic augmentation strategy accumulates alongside, rather than replaces, real data.

## 13. Fail Indicators
- Synthetic and real data are blended with no provenance tag; the proportion is unknown or undocumented.
- Fidelity testing shows synthetic tail cases are systematically "easier" or more homogeneous than real tail cases (mode collapse).
- Validation metrics are reported without disclosing what proportion of the test set was synthetic.
- A minority segment's synthetic augmentation reduces rather than preserves within-segment diversity.

## 14. Reporting Language
**Pass:** "Synthetic data used in [model]'s training corpus is provenance-tagged, generation method documented, and fidelity-tested against a real reference population; no material tail-distribution or subgroup-diversity loss was found. Real-world rare-event holdout performance is consistent with synthetic-holdout performance (★2 professional assessment given the adapted methodology)."

**Fail:** "Synthetic augmentation data is untagged and blended indistinguishably with real training data. Fidelity testing shows synthetic rare-event examples are systematically less complex than real equivalents, indicating the model has been trained and validated against a sanitised approximation of the events it is intended to detect. This represents a material risk of undetected performance degradation on real rare events and requires remediation before reliance."

**Partial:** "Synthetic-data provenance tagging exists for the primary training set but fidelity validation has not been extended to the minority-segment augmentation subset, which constitutes [x]% of that segment's training examples. The assurance objective is not met for that subset until fidelity testing is completed."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (missed fraud/AML typology or degraded minority-segment performance; regulatory and financial exposure)
  Likelihood: 2 (requires fidelity validation to be skipped, plausible under delivery pressure but not default)
  Detectability: 3 (surfaces via post-deployment outcome monitoring on genuinely rare real events, inherently slow)
  Recoverability: 2 (remediable via re-augmentation and retraining)
  Novelty: 4 (mode collapse and tail erosion in synthetic augmentation is deep ML-research territory; invisible to FS domain SMEs)

If controls are absent or degraded:
  Severity: 4 (systematic blind spot on the exact rare events the model exists to catch; large-scale fraud/AML miss or discriminatory minority-segment outcome)
  Likelihood: 3 (synthetic augmentation without fidelity testing is a common shortcut under data-scarcity pressure)
  Detectability: 4 (silent — validation metrics look strong precisely because the tail was sanitised)
  Recoverability: 3 (requires full re-augmentation, retraining, and retrospective review of affected decisions)
  Novelty: 4
Residual risk: Critical when synthetic augmentation targets exactly the highest-materiality rare cases (fraud, AML, minority fairness).
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Degraded detection of rare fraud/AML typologies or minority-segment fairness harm; material financial and regulatory exposure. |
| **Likelihood** | 2 | Plausible where fidelity validation is skipped under data-scarcity pressure, not the universal default. |
| **Detectability** | 4 | Validation metrics look reassuring precisely because the failure sanitises the tail — a structurally silent failure mode. |
| **Recoverability** | 2 | Remediable via re-augmentation and retraining once identified. |
| **Novelty** | 4 | Mode collapse / tail erosion in synthetic data is specialist ML-research knowledge, well outside FS domain expertise. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(f) and Art. 10(3)] requires training data to be relevant, representative and examined for possible biases including as they might affect the intended purpose; synthetic augmentation falls within this data-governance obligation. No UK/FS-specific regulation names synthetic-data fidelity explicitly; this IRQ addresses prudential risk under PRA SS1/23 (Principle 3) general data-quality expectations. (verified 29 Jul 2026)

## 18. Research Basis
> [Shumailov, I., et al., 2024, "AI models collapse when trained on recursively generated data", Nature 631, https://doi.org/10.1038/s41586-024-07566-y] — recursive training on generated data erases distributional tails, the foundational mechanism this IRQ guards against. [Alemohammad et al., 2023, "Self-Consuming Generative Models Go MAD", arXiv:2307.01850] — independent confirmation of quality/diversity degradation across modalities. [Gerstgrasser et al., 2024, "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Data", arXiv:2404.01413] — accumulation (not replacement) mitigates collapse, the basis for the accumulation control above. [Dohmatob et al., 2024, "A Tale of Tails: Model Collapse as a Change of Scaling Laws", arXiv:2402.07043] — theoretical grounding. Note: this literature is developed primarily for recursive generative-model training (text/image), not FS tabular fine-tuning augmentation directly — the analogy is credible but adapted, hence ★2 test confidence, not ★3+.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-MOD-012 (B.5: model collapse from output-to-training feedback — the recursive-generation variant)
  - IRQ-MOD-011 (B.5: evaluation integrity — synthetic-inflated validation metrics)
  - IRQ-DAT-005 (A.1: representativeness against the deployed population — compounding risk)
  - IRQ-CON-001 (H.1: subgroup outcome equity — where synthetic homogenisation surfaces as fairness harm)
```

## 20. References
```
[1] Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., Gal, Y., 2024.
    "AI models collapse when trained on recursively generated data." Nature 631, 755–759.
    https://doi.org/10.1038/s41586-024-07566-y
[2] Alemohammad, S., et al., 2023. "Self-Consuming Generative Models Go MAD." arXiv:2307.01850.
[3] Gerstgrasser, M., et al., 2024. "Is Model Collapse Inevitable? Breaking the Curse of
    Recursion by Accumulating Data." arXiv:2404.01413.
[4] Dohmatob, E., et al., 2024. "A Tale of Tails: Model Collapse as a Change of Scaling Laws."
    arXiv:2402.07043.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Fraud/AML SMEs trust "more synthetic examples = better balance";
  mode collapse and tail erosion are invisible without fidelity testing.
✓ Test 2 (Plausible Harm): Grounded in Shumailov et al. (2024) and related model-collapse
  literature, adapted to FS training-augmentation context.
✓ Test 3 (Testable): Statistical fidelity comparison is executable in non-production. ★2.
✓ Test 4 (Decision-Relevant): Gates whether synthetic-augmented training data may be relied
  upon for fraud/AML/minority-segment model development.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

