# TP-CON-007 — Feedback-Loop Multi-Cycle Simulation

## 1. Procedure Identity
**Procedure ID:** TP-CON-007
**IRQ:** IRQ-CON-007 — Unmanaged Performative Feedback Loops Entrenching Unfair Outcomes
**Assurance objective:** AO-CON-007 — The firm shall map feedback-loop pathways by which the AI system's own decisions shape subsequently observed data, and shall incorporate counterfactual or exploration data into retraining/recalibration to prevent entrenchment or amplification of unfair patterns.
**★ Confidence (carried from canvas, unchanged):** ★2 — reject inference is an established technique in credit-risk modelling specifically (★3 for that component); extending the same logic to a general performative feedback-loop test across multiple retraining cycles, and to non-credit contexts, is research-grounded but bespoke, with no agreed FS benchmark — the blended rating reflects the weaker, more novel component.
**Method classification:** Adapted Industry Practice (reject inference, in credit contexts) extended by Emerging Practice (multi-cycle feedback-loop simulation).

## 2. Preconditions
**Environment:** Non-production analysis environment capable of executing the firm's retraining pipeline against historical or synthetic data, repeatedly, in a controlled configuration. This is the most computationally demanding CON procedure.
**Access required:** The retraining pipeline in a form the reviewer can execute or have executed under observation; historical multi-cycle data (or the ability to generate a synthetic multi-cycle series); read access to model documentation on feedback pathways; read access to retraining governance sign-off records.
**Artefacts required:** Retraining pipeline definition; historical training datasets for successive cycles with the selection mechanism intact (i.e. it must be recoverable which records were model-selected); model documentation's feedback-loop mapping, if any; retraining governance sign-off papers; longitudinal subgroup disparity monitoring, if any.
**Personnel required:** Model owner; MLOps/pipeline engineer to execute retraining runs; reviewer with competence in selection bias and reject inference.
**Data handling:** Historical training data at scale; use a non-production copy with identifiers removed. Protected-characteristic labels handled per the domain data-protection note. Where historical multi-cycle data is unavailable, a synthetic series is generated and every conclusion is labelled synthetic-based.

## 3. Test Design
The retraining process is simulated twice over successive cycles:

- **Arm 1 — as-is.** Retrain using only outcomes observed for the model-selected/accepted population, exactly as the current pipeline does.
- **Arm 2 — counterfactual-aware.** Retrain incorporating a defined counterfactual or reject-inference technique so that the rejected population contributes information.

Subgroup disparity metrics (computed per the TP-CON-001 methodology, with the same pre-recorded metric choices) are tracked across simulated cycles under each arm. The finding of interest is the *trajectory*: does disparity under Arm 1 widen relative to Arm 2 across cycles? A pipeline whose disparity is stable in a single cycle may still be entrenching over five.

Minimum three simulated cycles; five is materially better and is the target where data permits. With fewer than three, no trajectory can be observed and the procedure degrades to a single-cycle disparity measurement already covered by TP-CON-001.

The counterfactual technique used in Arm 2 must be defined and justified before execution — reject inference in credit contexts has established variants, of which the canvas names augmentation for declined applicants; in non-credit contexts the reviewer is constructing an analogue and must say so.

## 4. Steps
1. Obtain the model documentation and search for an explicit feedback-loop mapping. **Record:** whether pathways are named (which decisions shape which subsequently observed data), or whether observed outcomes are treated as unqualified ground truth.
2. Obtain historical multi-cycle data and confirm the selection mechanism is recoverable. **Record:** number of cycles available; whether rejected-population records are retained at all (if not, Arm 2 cannot use real data and must use synthetic augmentation — record this).
3. Define and record the counterfactual/reject-inference technique for Arm 2, with justification. **Record:** technique, variant, parameters, and — where the context is non-credit — an explicit statement that the technique is an analogue extension.
4. Fix the subgroup disparity metrics to be tracked, using the same pre-recorded selections as TP-CON-001. **Record:** metrics and the cross-reference.
5. Execute **Arm 1**: retrain across the available cycles using the as-is pipeline. **Record:** per-cycle model, and per-cycle subgroup disparity metrics.
6. Execute **Arm 2**: retrain across the same cycles with the counterfactual technique applied. **Record:** per-cycle model and disparity metrics.
7. Compare the disparity trajectories. **Record:** per-cycle values for both arms; the divergence at the final cycle; and whether Arm 1's trajectory is widening, stable or narrowing.
8. Assess whether the observed Arm 1 trajectory is attributable to feedback entrenchment or to underlying population change. **Record:** the reasoning; where a synthetic control (a stable synthetic population) is available, run it as a third arm to isolate the mechanism.
9. Review whether a counterfactual/reject-inference technique is in active use in the real pipeline. **Record:** in use / considered and rejected with documented rationale / never considered. The middle case is acceptable; the last is a fail indicator.
10. Review longitudinal production monitoring. **Record:** whether subgroup disparity is tracked across retraining cycles in production, and its observed trajectory.
11. Review retraining governance sign-off papers. **Record:** whether feedback-loop risk appears as a named consideration distinct from general model performance.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Disparity trajectory under Arm 1 | Reviewer judgement — no established threshold. The canvas's operative test is direction: stable or narrowing passes, widening fails | Per canvas pass/fail indicators; no numeric benchmark exists |
| Arm 1 vs Arm 2 divergence at final cycle | Reviewer judgement — no established threshold. Report descriptively as the quantified cost of the current design | Explicitly bespoke |
| Number of simulated cycles | ≥3; ≥5 preferred | Reviewer judgement — a design minimum, not an external standard |
| Counterfactual technique in active use | In use, or documented rationale for non-use | Categorical per canvas fail indicator ("no technique used, with no documented rationale") |
| Feedback-loop mapping in documentation | Present and naming specific pathways | Categorical per canvas pass indicator |
| Retraining sign-off addresses feedback-loop risk | Present as a named consideration | Categorical per canvas fail indicator |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: feedback-loop pathways are explicitly mapped in model documentation naming which decisions shape subsequently observed data; a counterfactual/reject-inference or equivalent technique is in active use for retraining rather than merely considered and rejected without rationale; multi-cycle simulation or longitudinal monitoring shows subgroup disparity stable or narrowing across cycles; and retraining governance sign-off addresses feedback-loop risk as a named consideration.

**Fail** where: no feedback-loop mapping exists and retraining treats observed outcomes as unqualified ground truth; no counterfactual technique is used with no documented rationale for its absence; longitudinal monitoring or simulation shows disparity widening across successive cycles, indicating active entrenchment; or retraining sign-off does not address feedback-loop risk distinctly from general model performance.

**Partial** where the mapping exists and governance addresses the risk, but no counterfactual technique is in use and simulation shows a modest widening trajectory not yet material.

## 7. Evidence Outputs
- Feedback-loop mapping from model documentation as obtained — **L2**
- Counterfactual technique definition and justification, recorded pre-execution — **L2**
- Per-cycle disparity metrics for Arm 1 and Arm 2 — **L3**
- Trajectory comparison analysis including any synthetic control arm — **L3**
- Reviewer's independent entrenchment assessment — **L4**
- Longitudinal production subgroup disparity monitoring across real retraining cycles — **L5**

## 8. Common Pitfalls & Limitations
- **Too few cycles.** Below three cycles there is no trajectory. Report the limitation rather than an inferred trend.
- **Rejected-population records not retained.** Very common, and it makes real-data reject inference impossible. Record the constraint; a synthetic-augmentation Arm 2 is weaker evidence and must be labelled so.
- **Attributing trajectory to feedback without a control.** Population change can produce a widening trajectory with no feedback mechanism at all. Step 8's synthetic control arm is the corrective where data permits.
- **Applying credit-context reject inference to a non-credit system without saying so.** The ★2 rating exists largely because of this extension. Name it.
- **Computational cost underestimated.** Multi-cycle retraining across two arms is expensive; scope the compute before committing to the procedure.
- **Confusing this with TP-CON-001.** CON-001 measures disparity now; CON-007 measures whether the pipeline design makes it worse over time. Both are needed.

## 9. Time / Effort Estimate
**6 reviewer-days**: 1 day documentation and data-availability assessment, 1 day technique definition and design, 2 days simulation execution across both arms (excluding compute wall-time, which may run overnight), 1.5 days trajectory analysis and control work, 0.5 day working papers. Add 1 day where a synthetic multi-cycle series must be generated.

---
---

