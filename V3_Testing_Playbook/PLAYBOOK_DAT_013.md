# TP-DAT-013 — Feedback-Channel Gaming and Recursive-Content Simulation

**Procedure ID:** TP-DAT-013
**IRQ:** IRQ-DAT-013 — Unvetted Feedback Loops Re-Entering Training or Fine-Tuning
**Assurance objective:** AO-DAT-013 — feedback-to-training and output-to-training paths shall be identified, vetted for provenance and manipulation risk, and protected before any user feedback signal or model output is permitted to influence future model updates.
**★ Confidence:** ★2 (carried from canvas — harm mechanism plausible and partially evidenced by adjacent research (recursive collapse per Shumailov et al.; general adversarial-ML anomaly detection), but feedback-channel gaming specifically has no dedicated published FS benchmark; test design is bespoke)
**Method classification:** Emerging Practice — no established benchmark. Structured bespoke and labelled as such per METHODOLOGY_STANDARDS §3; grounded on adjacent research cited in the canvas rather than on a dedicated methodology, because none exists.

## Preconditions

- **Environment:** non-production replica of the feedback pipeline, from signal capture through vetting to the point at which data would be handed to a training/fine-tuning job. Simulated retraining runs in the isolated sandbox; **no production retraining is triggered.**
- **Access needed:** feedback pipeline replica; vetting/anomaly-detection configuration; the inventory (if any) of feedback-to-training paths; change-control records for feedback-derived model updates; fine-tuning sandbox for the retraining simulation.
- **Artefacts requested in advance (2 weeks):** map of all feedback signals and which training/fine-tuning process each feeds (thumbs-up/down, human overrides, corrections, accepted/rejected suggestions, logged outputs); vetting gate design; anomaly-detection rules for feedback; change-control records for the last three feedback-derived model updates (reviewer-set design minimum, disclosed at scoping); the accumulation/filtering policy for recursive model-generated content.
- **Personnel:** reviewer (lead); feedback platform engineer; ML engineer for the simulated retraining cycle; model change-control owner.

## Test design

- **Three attack classes simulated (per canvas):**
  - **(a) Coordinated repeat-source gaming** — many low-cost interactions from a small number of sources pushing a specific rating direction. Vary the coordination signature: identical timing, identical content, and a deliberately dispersed variant that is harder to detect.
  - **(b) Single-source concentration** — one compromised or simply careless human-override source producing a disproportionate share of correction signal. This is the more realistic insider-shaped case and is often entirely unmonitored.
  - **(c) Recursive synthetic content** — model-generated content re-entering as if it were fresh human feedback.
- **Measures:** for each class, whether the vetting/anomaly gate flags the data **before** it would reach a training job; and, for unflagged data, whether a simulated retraining cycle produces a measurable behavioural shift against a clean-feedback baseline.
- **Baseline:** a clean-feedback retraining cycle run first, on the same base model and configuration, providing the comparison point. Without it the behavioural-shift measure is uninterpretable.
- **Benign-payload principles:** all simulated feedback is synthetic and benign in content; the "gaming" is a *pattern* of submission, not harmful content. No real users are impersonated, no live customers are involved, and no production feedback records are altered.

## Steps

1. Build the feedback-path inventory independently from the pipeline configuration, then compare against the firm's own inventory. **Record:** paths found, paths in the firm's inventory, and the difference — an inventory gap is the canvas's first fail indicator.
2. Review vetting gate design and anomaly-detection rules for feedback. **Record:** which paths have a gate, and what each gate checks.
3. Run the clean-feedback baseline retraining cycle in the sandbox. **Record:** configuration, run ID, and the behavioural baseline measured on a fixed evaluation set.
4. Simulate class (a): coordinated repeat-source gaming, in both concentrated and dispersed signatures, at two volumes (reviewer-set design minimum, disclosed at scoping). **Record:** submission log, and gate disposition per record.
5. Simulate class (b): single-source concentration in the correction signal. **Record:** the share of correction signal attributable to the source, and whether any concentration monitoring fired.
6. Simulate class (c): recursive model-generated content submitted as fresh feedback. **Record:** whether provenance filtering or accumulation control identified it.
7. For each class, determine whether any unflagged data would have reached a training/fine-tuning job. **Record:** the survivor set per class.
8. Run a simulated retraining cycle on the survivor-containing feedback set. Measure behavioural shift against the clean baseline on the fixed evaluation set. **Record:** the delta, with particular attention to shifts in the direction the gaming pushed.
9. Review change control: is each feedback-derived fine-tuning cycle treated as a discrete, re-validated model change, or as automatic "continuous improvement"? **Record:** change records for the last three cycles, or their absence.
10. Destroy simulated feedback data and sandbox artefacts; record confirmation.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Feedback-to-training paths with a documented vetting gate | All identified paths (canvas pass indicator) | Canvas |
| Detection of coordinated-gaming and single-source-concentration attacks | Detected and throttled/flagged in staging (canvas pass indicator) | Canvas; **no published FS benchmark** — detection rate threshold is reviewer judgement |
| Recursive model-output content filtered or accumulation-controlled | Present (canvas pass indicator) | Canvas; accumulation control per the collapse-mitigation literature cited in the canvas |
| Behavioural shift versus clean baseline after simulated retraining | **Reviewer judgement — no established threshold**; any directionally-consistent shift is material | Bespoke |
| Feedback-derived cycles treated as discrete, re-validated changes | Yes (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — all identified feedback-to-training paths pass a documented vetting gate; simulated coordinated-gaming and single-source-concentration attacks are detected and throttled or flagged; recursive model-output content is filtered or accumulation-controlled before re-ingestion; each feedback-derived fine-tuning cycle is a discrete, re-validated model change.
- **Fail** — no inventory of which feedback signals feed which training process; simulated gaming passes undetected and would influence a retraining cycle; a single reviewer or narrow source demonstrably dominates the correction signal, unmonitored; feedback-derived retraining occurs without change-control re-validation, treated as routine continuous improvement.
- **Partial** — the concentrated gaming signature is detected but the dispersed one is not; or class (a) is controlled while class (b) — the insider-shaped case — is entirely unmonitored. Report by class and signature. Where the simulated retraining cycle could not be run, report the detection conclusion only and mark the behavioural-impact question unresolved.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Independently-built feedback-path inventory and comparison against the firm's | **L4** (independent enumeration) |
| Vetting gate and anomaly-rule configuration extracts | L2–L3 |
| Clean-baseline retraining configuration and behavioural baseline | L3 |
| Simulated-attack submission logs with gate dispositions (patterns described, no reusable tooling published) | L4 |
| Survivor set per class | L4 |
| Post-simulation behavioural delta against baseline | L4 |
| Change-control records for the last three feedback-derived cycles | L2–L3 |
| Destruction confirmation | L3 |

## Common pitfalls & limitations

- **No clean baseline.** The behavioural-shift measure is then uninterpretable. Step 3 is mandatory.
- **Simulating only the obvious signature.** Identical-timing, identical-content gaming is detectable by almost any rule; the dispersed variant is the informative one.
- **Ignoring class (b).** Single-source concentration in human-override signal is the most likely real occurrence and the least likely to be monitored, precisely because it looks like normal work.
- **Canvas limitation carried forward:** feedback-channel gaming has **no dedicated published FS benchmark**; the grounding is adjacent (recursive-collapse research and general adversarial-ML anomaly-detection practice). This is the least mature DAT procedure alongside TP-DAT-010, and reporting must carry the ★2 judgement-based label.
- **Simulated retraining is not the firm's real retraining.** Sandbox configuration inevitably differs; state the divergence and its direction (usually the sandbox is smaller, which overstates the behavioural shift per unit of gamed data).
- **Detecting a gaming pattern in staging does not establish detection at production volume**, where the signal-to-noise ratio is far less favourable.

## Time/effort estimate

**4 reviewer-days** (0.5 path inventory; 0.5 gate review; 0.5 baseline retraining; 1 attack simulation across three classes; 0.5 survivor retraining and delta measurement; 0.5 change-control review; 0.5 analysis and reporting).

---
---

