# TP-MOD-010 — Six-Type Distribution-Shift Robustness Testing

**Procedure ID:** TP-MOD-010
**IRQ:** IRQ-MOD-010 — Unassessed Robustness Across Population, Covariate, Concept, Label, Temporal and Policy Shift
**Assurance objective:** AO-MOD-010 — model robustness shall be separately assessed against population, covariate, concept, label, temporal and policy shift, with defined revalidation triggers specific to each shift type, so that degradation from any one shift mechanism is detectable and actionable.
**★ Confidence:** ★3 (carried from canvas — credible, peer-reviewed shift-detection methods with reasonable consensus for statistical shift types (Koh et al., 2021 WILDS; Rabanser et al., 2019); concept/label/policy shift testing is more bespoke and professional-judgement-led, pulling the overall rating toward the middle of the ★3 band rather than ★4)
**Method classification:** Established for statistical shift types; **Emerging/bespoke for concept, label and policy shift** — labelled distinctly in reporting, since the confidence is not uniform across the six.

## Preconditions

- **Environment:** staging pipeline plus the firm's detection/monitoring mechanism configured as in production. Synthetic/historical data.
- **Access needed:** staging pipeline; monitoring and revalidation trigger configuration; historical data spanning at least two materially different periods; the rule/policy set the model depends on.
- **Artefacts requested in advance (3 weeks — historical data assembly drives lead time):** the shift-monitoring design by shift type; revalidation trigger definitions; production history of revalidation events; policy/regulatory change log for the review period and any linkage to model revalidation; governance escalation thresholds.
- **Personnel:** reviewer (lead); data scientist to construct the shift scenarios; domain SME to define a realistic concept and policy shift; monitoring owner.

## Test design

Six scenarios (per canvas), each applied to a representative dataset, with the model held constant:

| Shift | Construction | Confidence character |
|---|---|---|
| **(a) Population** | Resample to change subgroup proportions | Established statistical method |
| **(b) Covariate** | Alter the input-feature distribution, holding the true relationship constant | Established statistical method |
| **(c) Concept** | Alter the true input–output relationship (re-label a subset consistent with a changed real-world relationship), holding inputs constant | **Bespoke** — requires SME definition of a realistic relationship change |
| **(d) Label** | Alter the base rate of outcomes | Established |
| **(e) Temporal** | Use data from a materially different time period | Established, but period selection is judgement |
| **(f) Policy** | Simulate a rule change removing or altering a previously-used feature or threshold | **Bespoke** — requires the SME to select a realistic rule change |

- **Magnitude tiers:** each shift at subtle, moderate and obvious magnitudes (reviewer-set design minimum, disclosed at scoping), as in TP-DAT-011. Detection only at the obvious tier is a partial result.
- **Dual measurement per scenario:** (1) does model performance actually degrade, and (2) does the firm's detection mechanism flag it and fire a revalidation trigger. These are separate questions and a system can fail either independently — a shift that degrades performance undetected, and a shift detected that triggers nothing, are both fails, of different kinds.
- **Control:** an unshifted run through the same monitoring, giving the false-positive baseline.
- **Benign-payload principles:** not applicable; all shifts are constructed from synthetic or historical data.

## Steps

1. Confirm the staging monitoring configuration matches production per shift type. **Record:** configuration diff, and any shift type for which no mechanism exists at all (frequently concept, label and policy — record before testing, since it predicts the result).
2. With the SME, define the concept shift and policy shift realistically. **Record:** the definitions and the SME's rationale — these two constructions carry the procedure's judgement load and must be defensible.
3. Establish the unshifted baseline: model performance and monitoring output. **Record:** the baseline and false-positive rate.
4. Construct and run scenario (a) population shift at three magnitudes. **Record:** performance delta, monitoring signal, revalidation trigger firing.
5. Repeat for (b) covariate, (d) label and (e) temporal. **Record:** as above per scenario and tier.
6. Run (c) concept shift. **Record:** as above, noting specifically whether input-side monitoring can detect it at all — by construction it cannot, if inputs are unchanged, which is the diagnostic point.
7. Run (f) policy shift. **Record:** as above, plus whether the firm's policy-change process (rather than statistical monitoring) would have triggered revalidation.
8. Build the results matrix: shift type × magnitude × (performance degraded? / detected? / trigger fired?). **Record:** the matrix — the headline output.
9. Review production history: has any shift type ever triggered a documented revalidation? **Record:** events, with dates and shift types.
10. Review the policy/regulatory change log for the period and check each material change for a corresponding revalidation record. **Record:** changes with and without revalidation.
11. Review governance escalation: is it calibrated to shift-specific signals, or only to generic accuracy metrics? **Record:** the escalation design.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Detection mechanism exists and functions for all six shift types | All six, each with a defined revalidation trigger (canvas pass indicator) | Canvas |
| Performance degradation per shift type and magnitude | Report; **reviewer judgement — no established threshold** for materiality | Canvas |
| Detection latency and false-negative rate per type | Report per type and tier; **no established threshold** | Rabanser et al. / Koh et al. methods as cited |
| False-positive rate (unshifted control) | Report as context | Bespoke |
| At least one shift detected and acted upon in production history | Evidenced (canvas pass indicator — the control works in practice, not only in theory) | Canvas |
| Policy/regulatory changes linked to mandatory revalidation | Demonstrable linkage (canvas pass indicator) | Canvas |
| Escalation calibrated to shift-specific signals | Not solely generic accuracy metrics (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — detection mechanisms exist and function for all six shift types in the staging test, each with a defined revalidation trigger; at least one shift type has been detected and acted upon in actual production history; policy-shift mapping demonstrably links regulatory or internal rule changes to a mandatory revalidation step; governance escalation is calibrated to shift-specific signals.
- **Fail** — monitoring exists only for input-side statistical shift (population/covariate) with no mechanism for concept, label or policy shift; no shift type has ever triggered a documented revalidation in production history despite known economic-cycle or typology change over the review period; policy or regulatory changes affecting model-relevant rules occur with no corresponding revalidation trigger or record; "drift monitoring" is described only in general terms with no shift-type-specific design evidence.
- **Partial** — the near-universal shape: statistical shifts well covered, concept and policy shift uncovered. Report by shift type; do not aggregate. Note explicitly that concept shift is undetectable by input-side monitoring by construction, so its absence from the monitoring design is a structural gap rather than a tuning issue.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Monitoring configuration diff by shift type | L3 |
| SME definitions of the concept and policy shifts with rationale | L3 |
| Unshifted baseline and false-positive record | L3 |
| Per-scenario construction records and data manifests | L3 |
| Performance and monitoring results per scenario and tier | **L4** |
| Results matrix (type × magnitude × degraded/detected/triggered) | L4 |
| Production revalidation history | L5 |
| Policy/regulatory change log with revalidation linkage | L2–L3 |
| Governance escalation design | L2 |

## Common pitfalls & limitations

- **Testing only statistical shifts.** They are the easy four; the canvas's finding is usually in concept and policy shift.
- **Confusing performance degradation with detection.** Measure both (step 8) — they are different controls.
- **An unrealistic concept shift.** If the SME cannot describe a plausible real-world relationship change, the scenario proves nothing. Do not invent one.
- **Canvas limitation carried forward:** confidence is **not uniform across the six**. Statistical shift detection rests on published, consensus methods; concept, label and policy shift testing is bespoke and judgement-led, which is exactly why the canvas places the combined rating in the middle of ★3 rather than at ★4. Report the six results with that distinction visible.
- **Temporal shift confounds everything.** A different period differs in population, covariates, concepts and policy simultaneously; treat the temporal result as an aggregate indicator, not an isolated mechanism.
- **Historical data availability** frequently constrains the temporal scenario; record the periods used and their comparability.

## Time/effort estimate

**6 reviewer-days** (0.5 configuration confirmation; 1 SME-led concept and policy shift definition; 1 scenario construction; 1.5 execution across six types and three tiers; 1 matrix analysis; 0.5 production history and policy-log review; 0.5 reporting).

---
---

