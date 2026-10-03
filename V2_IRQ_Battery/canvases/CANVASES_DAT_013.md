# CANVAS: IRQ-DAT-013

## 1. IRQ ID & Title
**IRQ-DAT-013: Unvetted Feedback Loops Re-Entering Training or Fine-Tuning**

Register question: "Can user feedback signals or model outputs re-enter training or fine-tuning loops without vetting, allowing organic degradation or deliberate gaming of the feedback channel to steer future model behaviour?"

## 2. Business Activities Affected
- **Customer service assistant continuous improvement:** Thumbs-up/down feedback, chat ratings or complaint-resolution outcomes often feed retraining or prompt-tuning loops; a customer or coordinated group can game these signals.
- **Fraud/complaint triage model refresh:** Human reviewer overrides and corrections are natural fine-tuning fodder — if unvetted, a compromised or careless reviewer's pattern becomes future ground truth.
- **RAG relevance tuning:** Click-through or "was this helpful" signals used to retrain retrieval ranking are directly exposed to manipulation by anyone who can interact with the system repeatedly.

## 3. AI Behaviour(s)
- Incorporates user feedback, model-output-derived signals, or human override/correction records as training or fine-tuning input for future model versions.
- Treats feedback volume and direction as a proxy for quality without inherent ability to distinguish genuine signal from gaming, coordinated manipulation, or organic model-generated content re-entering the loop.
- Adapts behaviour over successive fine-tuning cycles based on this feedback, compounding any unvetted bias or manipulation across iterations.

## 4. Failure Mode
> User feedback signals or the model's own outputs re-enter a training or fine-tuning loop without vetting, so the feedback channel becomes a vector for organic quality degradation (a variant of recursive model collapse) or deliberate gaming that steers future model behaviour toward attacker- or gamer-chosen outcomes.

## 5. Potential Consequences
- **Customer:** Systematically manipulated future model behaviour (e.g. gamed to approve certain claim patterns, or to suppress a fraud-typology flag) affecting subsequent customers.
- **Institution:** Slow, hard-to-attribute quality degradation across model refresh cycles; loss of institutional trust in the "continuously improving" narrative once discovered.
- **Regulator:** Governance failure to control a foreseeable data-integrity risk under EU AI Act Art. 10 and general MRM change-control principles; potential Consumer Duty implications if gamed behaviour harms customers.

## 6. Failure Chain
```
Feedback signals (ratings, overrides, corrections, click-through)
or model outputs are captured for future training/fine-tuning use
  ↓ (IRQ-DAT-013 — THIS IRQ: no vetting gate before the loop closes)
Feedback re-enters training/fine-tuning without provenance, quality
or manipulation screening
  ↓ (IRQ-MOD-012: recursive use of model-generated content risks
     quality/diversity collapse, Shumailov et al. mechanism)
Model retrained/fine-tuned on the unvetted, potentially gamed or
degraded feedback signal
  ↓ (IRQ-CON-007: the model's own decisions reshape the data it later
     learns from — a performative feedback loop)
Systematic behaviour shift toward the gamed or degraded target,
compounding across successive refresh cycles
  ↓
Manipulated or degraded model behaviour in production
→ customer harm, entrenched unfair pattern, governance/oversight finding

Control Breakpoints:
  • IRQ-DAT-013: vetting gate on feedback-to-training paths (provenance, anomaly, manipulation screening)
  • IRQ-MOD-012: filtering/blocking of recursive model-output content before it re-enters training
  • IRQ-CON-007: performative feedback-loop mapping and interruption
```

## 7. Why a Domain Expert May Miss It
- "Continuous learning from feedback" is marketed and understood as an unambiguous quality improvement mechanism; the possibility that the feedback channel itself is an attack surface is counter-intuitive.
- Product teams optimising engagement metrics (thumbs-up rate, resolution rate) may not realise those very metrics can be gamed by repeat or coordinated interaction, especially where no rate-limiting or anomaly detection exists on feedback submission.
- The recursive-collapse mechanism (Shumailov et al.) is a distinct research finding from adversarial gaming; SMEs aware of one often are not aware of the other, and a data-governance review focused on "training data" may not think to trace the feedback pipeline as training data at all.
- Human reviewer overrides feel authoritative ("a person corrected this") and are rarely treated with the same scepticism as automated or external data sources, even though a compromised or fatigued reviewer's pattern can systematically bias the loop.

## 8. Assurance Objective
**AO-DAT-013:** Feedback-to-training and output-to-training paths shall be identified, vetted for provenance and manipulation risk, and protected before any user feedback signal or model output is permitted to influence future model updates.

## 9. Expected Controls (Traced)
- **Feedback pipeline mapping and vetting gate** — [Emerging Practice — no single published FS standard for feedback-channel vetting; grounded in general data-governance principle that any input to training is training data] — every feedback-to-training path is inventoried and passes a provenance/anomaly check before use.
- **Rate-limiting and anomaly detection on feedback submission** — [Emerging Practice, drawing on general adversarial-ML anomaly-detection practice, NIST AI 100-2 E2025] — coordinated or repeat-source feedback manipulation is detectable and throttled.
- **Recursive-content filtering before re-ingestion** — [Shumailov et al., 2024, Nature; Gerstgrasser et al., 2024, "Is Model Collapse Inevitable?"] — model-generated outputs re-entering the loop are filtered or accumulated-not-replaced per the documented collapse-mitigation pattern.
- **Human-override pattern monitoring** — [linked IRQ-HUM-002 approval-theatre monitoring] — reviewer correction patterns are monitored for anomalous concentration (single reviewer driving disproportionate future-training signal).
- **Change control and re-validation on every feedback-derived fine-tuning cycle** — [PRA SS1/23 ongoing monitoring and periodic validation] — each retraining cycle using feedback data is validated as a discrete model change, not an automatic "improvement."

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the model learns from user feedback" with no vetting detail — **L1**.
- Feedback pipeline architecture document identifying every feedback-to-training path — **L2**.
- Code/config inspection confirming a vetting/anomaly-detection gate actually executes before feedback data reaches a training/fine-tuning job — **L3**.
- Staging test results: simulated coordinated-gaming feedback injected; detection/throttling rate measured — **L3**.
- Independent audit of the feedback-vetting control and of a specific feedback-derived fine-tuning cycle — **L4**.
- Production monitoring: feedback volume/pattern anomaly alerts over a defined period, with investigation outcomes logged — **L5**.

## 11. Independent Test
> In a non-production replica of the feedback pipeline, simulate three classes of feedback-channel attack: (a) coordinated repeat-source gaming (many low-cost interactions pushing a specific rating direction), (b) a single compromised/careless human-override source producing a disproportionate share of correction signal, and (c) synthetic model-generated content re-entering as if it were fresh feedback. Measure whether vetting/anomaly detection flags each class before the data would reach a training/fine-tuning job, and whether a simulated retraining cycle on unflagged gamed data produces a measurable behavioural shift versus a clean-feedback baseline. No production data or live customers involved. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (harm mechanism is plausible and partially evidenced by adjacent research — recursive collapse per Shumailov et al., and general adversarial-ML anomaly-detection practice — but feedback-channel gaming specifically has no dedicated published FS benchmark; test design is bespoke).

## 12. Pass Indicators
- All identified feedback-to-training paths pass a documented vetting gate before use.
- Simulated coordinated-gaming and single-source-concentration attacks are detected and throttled/flagged in staging testing.
- Recursive model-output content is filtered or accumulation-controlled before re-ingestion, per the collapse-mitigation control.
- Each feedback-derived fine-tuning cycle is treated as a discrete, re-validated model change (not an automatic silent update).

## 13. Fail Indicators
- No inventory exists of which feedback signals feed which training/fine-tuning process.
- Simulated gaming attacks in staging testing pass through undetected and would influence a retraining cycle.
- A single reviewer or narrow source can be shown to dominate the correction signal feeding fine-tuning, unmonitored.
- Feedback-derived retraining occurs without change-control re-validation, treated as routine "continuous improvement."

## 14. Reporting Language
**Pass:** "All identified feedback-to-training paths pass a documented vetting gate; staging simulation of coordinated gaming and single-source concentration attacks was detected and throttled in [x]% of cases. Feedback-derived fine-tuning cycles are treated as discrete, re-validated model changes. This is ★2 professional-judgement testing given the absence of a published FS benchmark for feedback-channel gaming; re-test as gaming techniques evolve."

**Fail:** "No vetting gate exists on the feedback pipeline feeding [model]'s fine-tuning cycles. Staging simulation demonstrated that coordinated gaming and single-reviewer-concentration attacks pass through undetected and would measurably shift model behaviour in a retraining cycle. This is an unmanaged data-integrity risk with a foreseeable path to attacker- or gamer-steered model behaviour and requires remediation before further feedback-derived retraining."

**Partial:** "Vetting exists for the primary customer-rating feedback channel but not for human-reviewer override signals, which account for [x]% of the fine-tuning correction data. Extend vetting coverage before the assurance objective is considered met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (steered future model behaviour affecting subsequent customers at scale)
  Likelihood: 2 (requires an adversary or careless internal source to exploit an unvetted
                 channel; plausible but not the default with basic monitoring)
  Detectability: 3 (gradual behavioural shift across refresh cycles; requires deliberate
                    cross-cycle comparison to detect)
  Recoverability: 2 (remediable by reverting to a clean-feedback baseline and retraining)
  Novelty: 4 (feedback-channel gaming and recursive collapse are both AI-specific mechanisms
              invisible to product/ops SMEs who see "continuous improvement" as inherently safe)

If controls are absent or degraded:
  Severity: 3 (compounding degradation or attacker-steered behaviour across successive
              fine-tuning cycles, entrenching unfair or manipulated patterns)
  Likelihood: 3 (feedback loops are commonly implemented as an unquestioned improvement
                 mechanism, with no vetting gate a foreseeable default)
  Detectability: 4 (silent, gradual, cross-cycle — no single event to detect)
  Recoverability: 3 (requires identifying a clean baseline to revert to, which may itself
                     be uncertain after several unvetted cycles)
  Novelty: 4
Residual risk: material and likely to be underestimated precisely because "feedback improves
the model" is the default institutional narrative.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Steered or degraded future model behaviour affects subsequent customers systematically. |
| **Likelihood** | 2 | Requires an adversary or careless source to exploit an unvetted channel; plausible given feedback loops are rarely vetted by default. |
| **Detectability** | 4 | Gradual, cross-cycle degradation with no single detectable event; requires deliberate longitudinal comparison. |
| **Recoverability** | 3 | Reverting requires identifying an uncontaminated baseline, which becomes harder the longer unvetted cycles have run. |
| **Novelty** | 4 | Feedback-channel gaming and recursive collapse are AI-specific mechanisms invisible to SMEs who treat "continuous improvement" as self-evidently safe. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)] data-governance obligations extend to any data used for training, including feedback-derived data, requiring examination for possible biases and appropriate mitigation. [PRA SS1/23, Principle 4 (independent model validation, including ongoing monitoring and review of model changes), with Principle 5 (model risk mitigants) engaged where use restrictions follow] require each model update — including feedback-derived fine-tuning — to be treated as a change subject to governance, not an automatic improvement. No regulation names feedback-channel vetting explicitly; this IRQ addresses prudential risk under general MRM change-control expectations. (verified 29 Jul 2026)

## 18. Research Basis
> [Shumailov, I., et al., 2024, "AI models collapse when trained on recursively generated data", Nature 631, https://doi.org/10.1038/s41586-024-07566-y] — establishes the recursive-degradation mechanism underlying the "organic degradation" half of this IRQ. [Gerstgrasser, M., et al., 2024, "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Data", arXiv:2404.01413] — mitigation basis (accumulation over replacement). [Dohmatob, E., et al., 2024, "A Tale of Tails: Model Collapse as a Change of Scaling Laws", arXiv:2402.07043] — theoretical grounding. No FS-specific published research on deliberate feedback-channel gaming (the "deliberate gaming" half) was located in the source registers; this is a genuine evidence gap, flagged [UNVERIFIED — no FS-specific published research located; Shumailov et al. 2024 (Nature 631, DOI confirmed) and arXiv:2404.01413/2402.07043 confirmed for the "organic degradation" half only] (verified 29 Jul 2026) rather than papered over with an unrelated citation — the deliberate-gaming mechanism is inferred by analogy to general adversarial-ML anomaly-evasion literature (NIST AI 100-2 E2025) rather than directly evidenced for FS feedback loops.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-MOD-012 (B.5: model collapse from output-to-training feedback — the recursive-generation mechanism)
  - IRQ-CON-007 (H.3: performative feedback loops entrenching unfair outcomes — the fairness-facing consequence)
  - IRQ-DAT-006 (A.2: ingestion/curation integrity screening — the general poisoning-control pattern this IRQ specialises)
  - IRQ-HUM-002 (D.1: approval-theatre/override monitoring — relevant to the human-reviewer-correction feedback path)
```

## 20. References
```
[1] Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., Gal, Y., 2024.
    "AI models collapse when trained on recursively generated data." Nature 631, 755–759.
    https://doi.org/10.1038/s41586-024-07566-y
[2] Gerstgrasser, M., et al., 2024. "Is Model Collapse Inevitable? Breaking the Curse of
    Recursion by Accumulating Data." arXiv:2404.01413.
[3] Dohmatob, E., et al., 2024. "A Tale of Tails: Model Collapse as a Change of Scaling Laws."
    arXiv:2402.07043.
[4] NIST, 2025. "NIST AI 100-2 E2025: Adversarial Machine Learning: A Taxonomy and
    Terminology of Attacks and Mitigations." March 2025.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10.
[6] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.2 (Data domain, Data Poisoning)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): "Continuous learning from feedback" is understood as inherently
  safe improvement; the feedback channel as an attack/degradation surface is counter-intuitive.
✓ Test 2 (Plausible Harm): Recursive-collapse half is well evidenced (Shumailov et al. 2024);
  deliberate-gaming half is evidenced by analogy and flagged as a research gap [UNVERIFIED — see Research Basis note above] (verified 29 Jul 2026).
✓ Test 3 (Testable): Simulated gaming/concentration/recursive-content attacks are executable
  in a non-production pipeline replica. ★2.
✓ Test 4 (Decision-Relevant): Gates whether feedback-derived fine-tuning cycles may proceed
  without a vetting gate.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

