# TP-MOD-012 — Recursive-Feedback Collapse Simulation

**Procedure ID:** TP-MOD-012
**IRQ:** IRQ-MOD-012 — Recursive Synthetic Data Feedback Causing Undetected Quality Collapse
**Assurance objective:** AO-MOD-012 — where model outputs may re-enter future training or fine-tuning data, controls shall prevent progressive generation-on-generation quality collapse — specifically loss of rare-event and minority-subgroup competence — through accumulation (not replacement) of real-world data and explicit tail-case evaluation at each retraining generation.
**★ Confidence:** ★2 (carried from canvas — the general model-collapse mechanism is well evidenced in peer-reviewed, high-profile research including a Nature publication (Shumailov et al., 2024; Alemohammad et al., 2023); applying it to the firm's specific fine-tuning pipeline and data mix is bespoke, and no standard FS-specific collapse-risk test exists)
**Method classification:** Adapted Industry Practice / Emerging — published model-collapse experimental protocols applied either to the firm's own pipeline (preferred) or to a representative synthetic setup calibrated to the firm's data mix (fallback).

## Preconditions

- **Environment:** isolated fine-tuning sandbox. **No production retraining is performed** under any circumstances. Synthetic/historical data only.
- **Access needed:** the firm's retraining pipeline in staging, if replicable; the actual data-mix ratio (real versus model-generated content); the accumulation/replacement policy and its pipeline implementation; rare-event/minority-subgroup case data.
- **Artefacts requested in advance (3 weeks):** the map of feedback loops from model output into future training data; retraining pipeline configuration; the documented data-mix ratio and synthetic proportion; the accumulation-not-replacement policy and evidence of its implementation in configuration; tail-fidelity validation records; historical generation-over-generation performance data if any retraining cycles have occurred.
- **Personnel:** reviewer (lead); ML engineer for the sandbox retraining cycles; domain SME to define the rare-event/minority-subgroup test set.

## Test design

- **Fixed tail test set:** rare events and minority subgroups representative of the deployed use case — the canvas gives the shape: uncommon income types for underwriting, minority-language or unusual complaint patterns for customer service. n≥100 (reviewer-set design minimum, disclosed at scoping), held **fixed** across all generations. This set never changes; it is the instrument.
- **Aggregate control measure:** a standard aggregate accuracy measure tracked alongside. The signature collapse pattern is **stable aggregate accuracy with declining tail performance** — without the aggregate measure the signature cannot be demonstrated.
- **Two paths, in order of preference:**
  - **Path A (preferred):** simulate several retraining generations using the firm's **actual** feedback-loop process in staging, run twice — once **with** the accumulation-not-replacement control and once **without**. The paired comparison isolates the control's contribution and is the strongest available evidence.
  - **Path B (fallback, where the live pipeline is not replicable):** apply published collapse experimental protocols to a representative synthetic setup calibrated to the firm's **actual data-mix ratio**, to estimate collapse risk. Clearly weaker; label it as an estimate, not a measurement.
- **Generations:** at least three, preferably five (reviewer-set design minimum, disclosed at scoping). Collapse is progressive and a single generation shows little.
- **Benign-payload principles:** not applicable; all content is synthetic or historical.

## Steps

1. Build the feedback-loop map independently from pipeline configuration, then compare against the firm's own map. **Record:** loops found, loops documented, the difference — an undocumented loop is the canvas's first fail indicator. (Reuse and cross-check against the TP-DAT-013 inventory.)
2. Verify the accumulation-not-replacement policy **in pipeline configuration**, not policy documents. **Record:** the configuration reference, or confirm the policy is unimplemented.
3. Record the actual data-mix ratio and synthetic proportion. **Record:** the figures and their source; *undocumented or unbounded* is a fail indicator in its own right.
4. Construct the fixed tail test set with the SME and the aggregate control measure. **Record:** both, with the SME's confirmation that the tail cases genuinely represent rare production events.
5. Measure generation-0 baseline performance on both the tail set and the aggregate measure. **Record:** the baseline.
6. **Path A:** run n retraining generations with the accumulation control active; measure tail and aggregate performance at each generation. **Record:** the per-generation series.
7. **Path A:** repeat with the accumulation control disabled. **Record:** the second series.
8. **Path B (if A is infeasible):** run the published collapse protocol on the representative synthetic setup at the firm's data-mix ratio. **Record:** the series, with an explicit label that this is an estimate for the firm's pipeline, not a measurement of it.
9. Plot tail performance and aggregate performance against generation for each arm. **Record:** the curves — divergence between them is the collapse signature.
10. Review historical generation-over-generation data where actual retraining cycles have occurred. **Record:** the observed trend and whether tail performance was ever measured at the time.
11. Review synthetic-augmentation tail-fidelity validation records. **Record:** presence or absence (links TP-DAT-004, which measures fidelity directly).
12. Destroy sandbox artefacts; record confirmation.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Feedback loops identified and documented | All identified and documented (canvas pass indicator) | Canvas |
| Accumulation-not-replacement policy evidenced in pipeline configuration | Present in configuration, not policy alone (canvas pass indicator) | Canvas; Gerstgrasser-type accumulation mitigation cited in canvas |
| Tail-set performance across generations | Stable or improving (canvas pass indicator) | Canvas; **no standard FS collapse-risk threshold exists** |
| Aggregate accuracy across generations | Tracked as the control — stable aggregate with declining tail is the collapse signature (canvas fail indicator) | Canvas |
| Synthetic proportion documented and tail-fidelity validated | Documented and validated (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — all feedback loops from model output to future training data are identified and documented; an accumulation-not-replacement policy is in place and evidenced in pipeline configuration; rare-event/minority-subgroup test-set performance is stable or improving across simulated or actual successive generations; synthetic proportion and tail fidelity are documented and validated.
- **Fail** — no mapping of feedback loops exists and retraining practice is undocumented or informal; simulated or historical generation-over-generation testing shows declining rare-event/minority-subgroup performance while aggregate accuracy remains stable (the signature collapse pattern); retraining data replaces rather than accumulates alongside real-world data with no accumulation policy; synthetic proportion is undocumented or unbounded with no tail-fidelity validation.
- **Partial** — the accumulation policy exists and is implemented, but tail performance is never measured at each retraining generation, so collapse would not be detected if it began; or Path B only was feasible, giving an estimate rather than a measurement. Where Path B was used, the conclusion must be stated as an estimate of collapse risk under the firm's data mix, not as a finding about the firm's pipeline.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Independently-built feedback-loop map and comparison | **L4** |
| Accumulation-policy configuration extract | L3 |
| Data-mix ratio record with source | L2–L3 |
| Fixed tail test set with SME validation | L3 |
| Per-generation tail and aggregate performance series, both arms | **L4** |
| Collapse curves | L4 |
| Path B protocol record and explicit estimate labelling, where used | L3 |
| Historical generation-over-generation data | L5 |
| Tail-fidelity validation records | L2–L3 |
| Sandbox destruction confirmation | L3 |

## Common pitfalls & limitations

- **Tracking aggregate accuracy only.** The collapse signature is invisible in aggregate metrics — that is precisely why the IRQ exists.
- **Too few generations.** Collapse is progressive; one or two generations show nothing.
- **A tail set that drifts.** If the test set changes between generations, the series is meaningless. Fix it at generation 0.
- **Presenting Path B as a measurement.** It is an estimate under a representative setup; the canvas explicitly frames it as such.
- **Canvas limitation carried forward:** the collapse mechanism is well evidenced in peer-reviewed research, but applying it to the firm's specific pipeline and data mix is bespoke and no standard FS collapse-risk test exists. ★2 — professional assessment.
- **Sandbox scale.** Sandbox retraining typically uses less data than production, which tends to **overstate** collapse per generation. State the direction of the bias.

## Time/effort estimate

**5 reviewer-days** (0.5 feedback-loop mapping; 0.5 configuration and data-mix review; 1 tail set construction with SME; 2 multi-generation simulation supervision across both arms; 0.5 curve analysis; 0.5 reporting). Excludes ML-engineer compute and execution time, which can be substantial.

---
---

