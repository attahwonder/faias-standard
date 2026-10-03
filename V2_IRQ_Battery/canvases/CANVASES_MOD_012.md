# CANVAS: IRQ-MOD-012

## 1. IRQ ID & Title
**IRQ-MOD-012: Recursive Synthetic Data Feedback Causing Undetected Quality Collapse**

Register question: "If model outputs re-enter future training or fine-tuning data, are controls in place to prevent quality collapse from recursive synthetic content?"

## 2. Business Activities Affected
- **AML narrative drafting fine-tuned on prior model outputs:** If historically-generated SAR narratives (some containing subtle errors) are used, uncurated, as future fine-tuning data, error patterns and rare-but-critical typologies can be progressively lost from the model's effective competence.
- **Customer service response generation:** Iterative fine-tuning on the model's own historical outputs (rather than fresh human-authored ground truth) risks narrowing response diversity and losing tail-case handling (unusual complaints, edge-case product queries).
- **Synthetic data used for underwriting model training/testing:** Where synthetic applicant data is generated to augment scarce cases (e.g. rare income types), recursive reliance on model-generated synthetic data without fresh real-world grounding risks the model progressively losing the ability to handle those same rare cases correctly.

## 3. AI Behaviour(s)
- Generates output that may, through feedback loops (customer service logs feeding future fine-tuning, synthetic data augmentation pipelines), re-enter the training or fine-tuning data of a future model version.
- Recursive training on model-generated (rather than real-world) data has been shown to progressively lose distributional tails — rare events, minority patterns, edge cases — even while aggregate metrics appear stable or improve.
- The collapse is gradual across generations of retraining, not a single detectable event.

## 4. Failure Mode
> Model outputs re-enter future training or fine-tuning data without adequate controls, causing progressive, generation-on-generation quality collapse — specifically the loss of rare events, minority-subgroup patterns and tail-case competence — that is not detected because aggregate performance metrics can remain stable even as this collapse occurs.

## 5. Potential Consequences
- **Customer:** Rare but real customer situations (unusual income types, minority-language complaints, uncommon claim circumstances) are progressively handled worse across model generations, disproportionately affecting underrepresented or edge-case customers.
- **Institution:** A slow, compounding degradation that standard "did aggregate accuracy improve" validation will not catch, potentially discovered only after several fine-tuning generations, requiring a return to a real-data-grounded baseline.
- **Regulator/market:** Loss of fair handling for minority/edge-case customer segments as a side-effect of an unmanaged data pipeline, engaging fairness (IRQ-CON-001/002) and representativeness (IRQ-DAT-005) regulatory concerns.

## 6. Failure Chain
```
Model outputs (customer responses, SAR narratives, synthetic augmentation data)
are captured in logs or generation pipelines
  ↓ (IRQ-DAT-004/IRQ-DAT-013: synthetic data or feedback-to-training paths are not clearly
     identified or vetted)
Those outputs re-enter a future fine-tuning or synthetic-augmentation dataset without
sufficient real-world data alongside them
  ↓ (IRQ-MOD-012 — THIS IRQ: no control prevents recursive-training-driven tail collapse)
Successive fine-tuning generations progressively lose rare-event and
minority-subgroup competence, while aggregate metrics remain stable or improve
  ↓ (IRQ-CON-001: fairness/subgroup outcome testing does not specifically test for this
     generational degradation)
Model quietly becomes worse at handling edge cases over successive versions
  ↓ (IRQ-GOV-008: no shift-specific signal (see IRQ-MOD-010 label/concept shift) catches
     a self-inflicted, training-pipeline-origin degradation)
Rare-case customers receive progressively worse treatment across model generations
  ↓
Discovered only via targeted subgroup/tail-case audit, complaint pattern in
under-represented segments, or academic/press coverage of model collapse generally

Control Breakpoints:
  • IRQ-DAT-004/IRQ-DAT-013: synthetic data identification and feedback-loop vetting at the
    data layer
  • IRQ-MOD-012: explicit anti-collapse controls — accumulating (not replacing) real data,
    tail/rare-case-specific evaluation across model generations
  • IRQ-CON-001/002: subgroup and tail-case fairness testing repeated at each fine-tuning
    generation
  • IRQ-GOV-007: independent validation explicitly checks generation-over-generation
    tail performance, not only current-version aggregate accuracy
```

## 7. Why a Domain Expert May Miss It
- FS SMEs are used to thinking of "more training data = better model," and are unlikely to know that training recursively on a model's own outputs, rather than fresh real-world data, has the opposite effect specifically on rare/edge cases.
- The collapse is gradual and multi-generational; a single before/after comparison of one fine-tuning cycle will not reveal it, and aggregate accuracy metrics can remain flat or even improve while tail performance erodes — the opposite of what SMEs expect a "quality" problem to look like.
- Feedback loops from production logs into future training data are often an unremarkable, taken-for-granted MLOps practice ("we retrain on recent interactions to keep the model current"), not flagged as a distinct risk requiring governance.
- The specific customers affected (rare income types, minority-language speakers, uncommon claim circumstances) are, by definition, a small and easily-overlooked segment in any aggregate quality review.

## 8. Assurance Objective
**AO-MOD-012:** Where model outputs may re-enter future training or fine-tuning data, controls shall prevent progressive, generation-on-generation quality collapse — specifically loss of rare-event and minority-subgroup competence — through accumulation (not replacement) of real-world data and explicit tail-case evaluation at each retraining generation.

## 9. Expected Controls (Traced)
- **Feedback-loop identification and vetting** — [linked IRQ-DAT-013] — all pathways by which model outputs could re-enter training/fine-tuning data are explicitly mapped and reviewed before being used.
- **Accumulating rather than replacing real-world data** — [Gerstgrasser et al., 2024, "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Data", arXiv:2404.01413] — each retraining generation adds synthetic/model-output data to a growing corpus of real data rather than substituting for it, which the research shows avoids collapse.
- **Rare-event and minority-subgroup preservation testing per generation** — [Shumailov et al., 2024, "AI models collapse when trained on recursively generated data", Nature; Alemohammad et al., 2023, "Self-Consuming Generative Models Go MAD", arXiv:2307.01850] — explicit tail/subgroup performance metrics are tracked across successive fine-tuning generations, not only aggregate accuracy.
- **Synthetic data declared, bounded and validated for tail fidelity** — [linked IRQ-DAT-004] — where synthetic data augmentation is used, its proportion is documented and its preservation of rare events/minority subgroups is validated, not assumed.
- **Theoretical scaling-law awareness informing retraining cadence and data-mix decisions** — [Dohmatob et al., 2024, "A Tale of Tails: Model Collapse as a Change of Scaling Laws", arXiv:2402.07043] — data-pipeline design decisions are informed by the analytical understanding that collapse risk scales with the proportion of recursively-generated data.

## 10. Expected Evidence (Tagged L1–L5)
- General MLOps statement that "the model is periodically retrained on recent data" — **L1** (assertion only; does not evidence any anti-collapse control).
- Data pipeline documentation mapping all feedback loops from model output to future training/fine-tuning data, and the accumulation-not-replacement policy — **L2**.
- Staging test results: rare-event/minority-subgroup performance measured across simulated successive retraining generations (e.g. comparing generation N and generation N+3 on a fixed tail-case test set) — **L3**.
- Independent validation report assessing the anti-collapse control design and generation-over-generation tail-performance evidence — **L4**.
- Production data: tail-case/minority-subgroup performance tracked across actual historical model version updates, with any degradation trend identified — **L5**.

## 11. Independent Test
> In a non-production environment, construct a fixed rare-event/minority-subgroup test set representative of the deployed use case (e.g. uncommon income types for underwriting, minority-language or unusual complaint patterns for customer service). If the firm's actual retraining pipeline is available in staging, simulate several retraining generations using the firm's real feedback-loop process (with and without the accumulation-not-replacement control) and measure tail-case test-set performance at each generation. Where a live pipeline is not replicable, use published model-collapse experimental protocols (Shumailov et al., 2024; Alemohammad et al., 2023) on a representative synthetic setup to estimate the collapse risk under the firm's actual data-mix ratio. Executed entirely on synthetic/historical data in staging; no production retraining is performed. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the general model-collapse mechanism is well-evidenced in peer-reviewed, high-profile research including a Nature publication; however, applying it to the firm's specific fine-tuning pipeline and data mix is bespoke, and no standard FS-specific collapse-risk test exists).

## 12. Pass Indicators
- All feedback loops from model output to future training/fine-tuning data are identified and documented.
- An accumulation-not-replacement data policy is in place and evidenced in pipeline configuration.
- Rare-event/minority-subgroup test-set performance is stable or improving across simulated or actual successive retraining generations.
- Synthetic data proportion and tail-fidelity are documented and validated wherever synthetic augmentation is used.

## 13. Fail Indicators
- No mapping exists of feedback loops from model output into future training data; retraining practice is undocumented or informal.
- Simulated or historical generation-over-generation testing shows declining rare-event/minority-subgroup performance while aggregate accuracy remains stable — the signature collapse pattern.
- Retraining data replaces rather than accumulates alongside real-world data, with no accumulation policy in place.
- Synthetic data proportion is undocumented or unbounded, with no tail-fidelity validation.

## 14. Reporting Language
**Pass:** "Feedback loops from model output to future training data are mapped and governed by an accumulation-not-replacement policy. Simulated multi-generation testing shows stable rare-event and minority-subgroup performance across retraining cycles. Conclusions rest on ★2 methodology — well-evidenced general mechanism, bespoke application to this pipeline — and should be re-tested at each material retraining cycle."

**Fail:** "No mapping of feedback loops into future training data exists, and retraining data replaces rather than accumulates alongside real-world data. Simulated multi-generation testing on a rare-event/minority-subgroup test set shows a [x]-percentage-point decline in tail performance across three simulated retraining generations, while aggregate accuracy remained stable — consistent with the documented model-collapse mechanism. This represents an unmanaged, compounding risk to the firm's ability to serve rare-case and minority customer segments; retraining pipelines should be redesigned around real-data accumulation before further fine-tuning generations proceed."

**Partial:** "An accumulation policy exists for the primary fine-tuning pipeline but not for the synthetic-data-augmentation pipeline used for underwriting model training, where synthetic data proportion is undocumented. The assurance objective is not fully met for the augmentation pipeline; tail-fidelity validation should be completed before further use."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (degraded handling concentrated in a small, defined rare-case/minority segment;
              moderate customer impact per generation)
  Likelihood: 2 (accumulation-not-replacement policy and generation-over-generation tail
              testing should prevent material collapse)
  Detectability: 2 (dedicated tail-case test sets, if run at each retraining generation,
              surface the trend before it compounds significantly)
  Recoverability: 2 (returning to a real-data-grounded baseline and retraining is a defined,
              if resource-intensive, remediation)
  Novelty: 4 (the idea that retraining on the model's own outputs can quietly and specifically
              degrade rare-case competence while aggregate metrics stay flat is highly
              counter-intuitive and unlikely to be anticipated by non-AI-specialist MLOps or
              risk teams)

Interpretation: acceptable residual risk with accumulation policy and tail-case testing per
generation in place; highest concern is Novelty, since the collapse is invisible to standard
aggregate-metric validation by design.

If controls are absent or degraded:
  Severity: 3 (compounding, cross-generational loss of competence for rare-case and minority
              customer segments, entrenching disparate treatment over time)
  Likelihood: 3 (documented across multiple independent research groups and modalities as a
              generalisable property of recursive training on model-generated data)
  Detectability: 4 (aggregate metrics can remain stable or improve even as tail performance
              collapses — a structurally poor detectability profile without dedicated
              tail-case testing)
  Recoverability: 3 (requires reconstructing a real-data-grounded training set and retraining
              from a point before the collapse became material, potentially losing several
              retraining generations of otherwise-useful updates)
  Novelty: 4
Residual risk: High. Should gate any retraining/fine-tuning pipeline that recursively
consumes model output without an accumulation policy and tail-case testing.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Effect is concentrated in a defined rare-case/minority segment rather than the general customer base, though compounding across generations raises longer-term concern. |
| **Likelihood** | 3 | Documented as a generalisable property across independent research groups and data modalities (text, image) wherever recursive training on model output occurs without mitigation. |
| **Detectability** | 4 | Aggregate accuracy can remain stable or improve while tail/minority-subgroup performance collapses — a structurally poor detectability profile absent dedicated testing. |
| **Recoverability** | 3 | Requires reconstructing a real-data-grounded training set and retraining, potentially losing several generations of otherwise-useful model updates. |
| **Novelty** | 4 | Highly counter-intuitive: "retrain on more of our own data" is normally considered good MLOps practice, inverting the expected direction of the failure. |

## 17. Regulatory Basis
> [FCA/PRA joint DP5/22 (Oct 2022) and FS2/23 feedback statement (Oct 2023), identifying data management as a top AI risk concern] — supports governance attention to training-data pipeline integrity generally. [PRA SS1/23, May 2023, effective 17 May 2024, Principle 3 development principles] — a model's data lineage and quality, including recursive-feedback effects, falls within the development/validation scope. No regulation names "model collapse" or recursive-training risk explicitly; this IRQ is a forward-looking application of SS1/23 data-quality principles to an emerging, well-evidenced AI-specific mechanism. (verified 29 Jul 2026)

## 18. Research Basis
> [Shumailov, I., Shumaylov, Z., Zhao, Y., et al., 2024, "AI models collapse when trained on recursively generated data", Nature 631, 755–759] — the foundational, peer-reviewed demonstration that recursive training on model output progressively erases distributional tails. [Alemohammad, S., et al., 2023, "Self-Consuming Generative Models Go MAD", arXiv:2307.01850] — independent confirmation of quality/diversity degradation across generative modalities. [Gerstgrasser, M., et al., 2024, "Is Model Collapse Inevitable? Breaking the Curse of Recursion by Accumulating Data", arXiv:2404.01413] — shows accumulating (not replacing) real data with synthetic data avoids collapse, directly informing this IRQ's primary control. [Dohmatob, E., et al., 2024, "A Tale of Tails: Model Collapse as a Change of Scaling Laws", arXiv:2402.07043] — analytical scaling-law account supporting the risk statement's theoretical grounding.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-DAT-004 (A.1: synthetic data identification and tail/subgroup fidelity validation —
    the data-provenance control this IRQ's evaluation depends on)
  - IRQ-DAT-013 (A.2: feedback-to-training loop vetting — the upstream data-pipeline control)
  - IRQ-CON-001 / IRQ-CON-002 (H.1: subgroup outcome equity and proxy-discrimination testing
    must be repeated per retraining generation to catch this failure mode)
  - IRQ-MOD-010 (B.5: distribution-shift robustness — collapse manifests as a self-inflicted,
    training-pipeline-origin form of concept/label drift)
  - IRQ-GOV-007 (I.3: independent validation should test generation-over-generation tail
    performance, not only current-version aggregate accuracy)
  - IRQ-CON-007 (H.3: feedback loops and transparency — the customer-outcome framing of the
    same recontamination mechanics)
```

## 20. References
```
[1] Shumailov, I., Shumaylov, Z., Zhao, Y., Papernot, N., Anderson, R., Gal, Y., 2024. "AI
    Models Collapse When Trained on Recursively Generated Data." Nature, 631, 755–759.
[2] Alemohammad, S., Casco-Rodriguez, J., Luzi, L., et al., 2023. "Self-Consuming Generative
    Models Go MAD." arXiv:2307.01850.
[3] Gerstgrasser, M., Schaeffer, R., Dey, A., et al., 2024. "Is Model Collapse Inevitable?
    Breaking the Curse of Recursion by Accumulating Real and Synthetic Data." arXiv:2404.01413.
[4] Dohmatob, E., Feng, Y., Yang, P., Charton, F., Kempe, J., 2024. "A Tale of Tails: Model
    Collapse as a Change of Scaling Laws." arXiv:2402.07043.
[5] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[6] Bank of England/FCA, 2022–2023. "DP5/22: Artificial Intelligence and Machine Learning"
    and "FS2/23" feedback statement.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.5 (Model domain, Distribution Shift & Evaluation Integrity)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): "Retrain on our own recent data" is normally good MLOps practice;
  that this specifically and quietly degrades rare-case/minority-subgroup competence while
  aggregate metrics stay flat inverts the expected failure signature.
✓ Test 2 (Plausible Harm): Grounded in a peer-reviewed Nature publication (Shumailov et al.)
  with independent multi-modality confirmation (Alemohammad et al.) and a documented
  mitigation (Gerstgrasser et al.).
✓ Test 3 (Testable): Testable in staging via simulated multi-generation retraining on a fixed
  tail-case test set; no production retraining required.
✓ Test 4 (Decision-Relevant): Outcome gates whether a recursive-feedback retraining pipeline
  may continue without an accumulation policy and tail-case testing.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
```

---
---

