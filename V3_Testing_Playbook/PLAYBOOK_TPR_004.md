# TP-TPR-004 — Silent Provider-Side Model Change Detection Review

**IRQ:** IRQ-TPR-004 — Undetected Silent Provider-Side Model Change.
**Assurance objective:** AO-TPR-004 — the firm shall detect material provider-side changes to model weights, safety filters or defaults before they affect customers or controls, through version pinning and behavioural canary testing, and shall have a tested rollback and re-approval path available on detection.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — research and industry practice recognise vendor-side drift, but no standardised, benchmarked FS methodology exists for silent-drift detection; canary design and threshold-setting are bespoke professional judgement.

### Preconditions
- Isolated non-production environment able to call the current model endpoint. Note the boundary: this procedure legitimately calls the provider's live endpoint from a staging environment, using synthetic prompts only. No production customer data is used at any point, and the calls are ordinary API usage, within the provider's published usage terms and under the firm's existing contract — not probing of provider infrastructure.
- **The archived baseline** from the last approved model version: the benchmark prompt set and its recorded output distribution. Where no archived baseline exists, the canary comparison cannot run and that absence is itself the primary finding — the firm has no means of detecting change other than customer complaint.
- The canary testing design specification, where one exists: benchmark set, cadence, alert thresholds.
- Endpoint configuration for production-critical model calls, to test version pinning.
- Provider change communications and public release notes for the review window, to identify whether a real provider-side update occurred.
- Rollback path documentation and any evidence of it having been tested.
- Personnel: lead reviewer; technical reviewer for benchmark execution; firm platform engineer; model risk/approval contact.

### Test design
**Benchmark comparison limb (technical).** A fixed benchmark prompt set is run against the current live endpoint and its output distribution compared against the archived baseline across four dimensions the canvas names:
- **Accuracy** on tasks with known correct answers;
- **Tone** — assessed against a rubric, since it has no natural metric;
- **Refusal rate** — the proportion of prompts declined, which is the dimension most sensitive to silent safety-filter changes and often the earliest signal;
- **Structured-output conformance** — the proportion of responses conforming to the required schema, which is the dimension most likely to break downstream systems silently.

The benchmark set must be **fixed** — the same prompts as the baseline. A regenerated set measures prompt variation, not model change.

**Detection-efficacy limb (the real test).** Where the provider **published a model update during the review window**, establish whether the firm's own canary process independently detected it, on what date relative to the update, and whether re-approval was triggered. This limb answers the assurance objective directly; the benchmark comparison alone only tells you whether change has occurred, not whether the firm would have noticed.

**Version-pinning limb.** Inspect production-critical model call configuration: are calls pinned to a specific version, or made against a "latest"-alias endpoint? Where the provider supports pinning and the firm does not use it, that is a discrete finding.

**Rollback limb.** Establish whether a rollback path is documented, whether a **recovery time objective** is defined, and whether the path has been **tested** rather than merely written. Where a real provider-side change occurred in the window, review what actually happened.

**Cadence and threshold limb.** Review the canary design: is the cadence defined and adhered to, are alert thresholds defined, and what happens when one trips? Thresholds set without a documented basis are recorded as such — there is no published FS methodology for setting them, and inventing one would breach the no-invented-controls discipline.

### Steps
1. Obtain the canary design specification, the archived baseline, and 12 months of canary run logs. Record what exists and what does not.
2. Verify the archived baseline is genuinely from the last approved version — check its date against the model approval record. A baseline captured after an undetected change is worthless.
3. Inspect endpoint configuration for all production-critical model calls; record pinning status per call site and whether the provider supports pinning.
4. Execute the fixed benchmark set against the current endpoint in staging. Record outputs.
5. Compare against the archived baseline across accuracy, tone, refusal rate and structured-output conformance. Record deltas per dimension.
6. Identify from provider release notes and change communications whether a model update occurred in the review window. Record dates.
7. **Detection-efficacy:** where an update occurred, establish from canary logs whether the firm detected it, when, and whether re-approval was triggered. Where no update occurred in the window, record that the limb could not be tested and that the canary process is therefore unproven in practice.
8. Review the rollback path: documented, RTO defined, tested? Obtain evidence of any test.
9. Review cadence adherence from the run logs, and the basis on which alert thresholds were set.
10. Report per model dependency, not in aggregate.

### Observations & measures
- **Benchmark deltas** per dimension (accuracy, tone, refusal rate, structured-output conformance) against the archived baseline. **No established threshold — reviewer judgement**, and the firm's own alert thresholds are recorded and assessed for whether they have any documented basis.
- **Baseline validity** (binary): archived baseline verified as from the last approved version / not verifiable.
- **Version pinning** = production-critical call sites pinned ÷ call sites where the provider supports pinning. Canvas threshold: **pinning used for all production-critical calls where the provider supports it.** Canvas Fail condition: production calls use "latest"-alias endpoints with no pinning used.
- **Detection efficacy** (categorical): a real provider change occurred and was independently detected by the canary process, with rollback/re-approval following / occurred and was not detected / no change occurred in the window so the limb is untested. Canvas pass indicator requires **at least one instance in the review period** demonstrating detection followed by rollback or re-approval — so an untested canary cannot achieve a full Pass on this indicator, and that should be stated rather than waived.
- **Cadence adherence** = canary runs executed ÷ runs due per the defined cadence.
- **Rollback status** (categorical): documented, RTO defined and tested / documented and RTO defined but untested / undocumented or no RTO. Canvas Fail condition: undocumented or untested with no defined RTO.

### Interpretation
- **Pass** — canary testing runs on a defined cadence with documented baseline comparison and deviations triggering a defined alert and investigation; version pinning is used for all production-critical calls where supported; at least one instance in the review period demonstrates the canary process detecting a real provider-side change followed by rollback or re-approval; the rollback path is tested within a defined recovery time objective.
- **Fail** — no canary testing exists and the firm has no mechanism to detect provider-side change other than customer complaint or incident; **or** production calls use "latest"-alias endpoints with no version pinning available or used; **or** a known provider model update occurred in the review period with no corresponding internal detection or re-approval record; **or** the rollback path is undocumented or untested with no defined RTO.
- **Partial** — canary testing operates on cadence with pinning in place, but no provider change occurred in the window so detection efficacy is unproven, or the rollback path is documented with an RTO but has never been tested. State precisely which indicator is unevidenced.

### Evidence outputs
- E1 Assertion that the model has not changed since approval, with no supporting test evidence — **L1** (explicitly labelled).
- E2 Canary design specification: benchmark set, cadence, alert thresholds — **L2**.
- E3 Archived baseline with validity verification against the approval record — **L3**.
- E4 Endpoint configuration inspection: pinning status per production-critical call site — **L3**.
- E5 Benchmark execution results with per-dimension deltas against baseline — **L3**.
- E6 Provider release-note and change-communication review for the window — **L2**.
- E7 Detection-efficacy findings from canary logs with dates — **L3**.
- E8 Cadence adherence analysis from 12 months of run logs — **L3**.
- E9 Rollback path documentation, RTO and any test evidence — **L2/L3**.
- E10 Independent audit confirming canary testing operates as designed across the critical-model population, where held — **L4**.
- E11 Production canary monitoring log over the last 12 months including detected changes and resulting rollback/re-approval actions — **L5**.

### Common pitfalls & limitations
- **A regenerated benchmark set.** It must be the same prompts. Otherwise the comparison measures the reviewer's prompt-writing, not the model.
- **An invalid baseline.** If the baseline was captured after an undetected change, everything downstream is anchored to a drifted reference. Step 2 exists for this.
- **Confusing the reviewer's detection with the firm's.** The reviewer executing a benchmark comparison and finding drift does not evidence that the firm's canary process would have found it. The detection-efficacy limb is the one that speaks to the objective.
- **Tone assessed without a rubric**, which produces an unrepeatable judgement. Agree the rubric before running.
- **Thresholds without basis.** Where the firm's alert thresholds were set arbitrarily, record that; do not substitute a FAIAS threshold, since none exists in any cited source.
- **Provider endpoint calls treated as production testing.** They are staging calls under existing contract with synthetic prompts, and that framing should be documented so the non-production rule is visibly respected.
- **★2 honesty.** Canary design is bespoke. A pass evidences that the firm's own bespoke process detected drift on the occasions tested.

### Time/effort estimate
**3.5 reviewer-days** — 0.5 documentation and baseline validity review; 0.5 endpoint configuration inspection; 0.75 benchmark execution and comparison; 0.5 detection-efficacy investigation; 0.5 cadence and rollback review; 0.25 threshold-basis enquiry; 0.5 write-up. Add 0.5 day per additional model dependency beyond two.

---
---

