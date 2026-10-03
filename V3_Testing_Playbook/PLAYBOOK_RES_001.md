# TP-RES-001 — Fallback Mode Exercise Against Impact Tolerance

## 1. Procedure Identity
**Procedure ID:** TP-RES-001
**IRQ:** IRQ-RES-001 — Absent or Untested Fallback Mode for AI-Dependent Important Business Services
**Assurance objective:** AO-RES-001 — For every important business service with an embedded AI component, the firm shall define, resource and periodically test a fallback mode capable of delivering the service within its stated impact tolerance when the AI component is unavailable or untrusted.
**Subdomain:** G.1 Fallback & Degradation
**★ Confidence (carried from canvas, unchanged):** ★3 — scenario testing against impact tolerance is established, regulator-mandated practice; the AI-specific trigger condition and "untrusted" determination are less standardised, moderating confidence from ★4.
**Method classification:** Adapted Industry Practice — FCA SYSC 15A.5.3R / PRA SS1/21 severe-but-plausible scenario testing, adapted to an AI-component trigger.

## 2. Preconditions
**Environment:** Non-production staging replica of the IBS-supporting process. Where the firm has run its own controlled live exercise of the fallback, outside customer-affecting hours with the sponsoring executive's written authorisation, the reviewer may observe it or take its records as evidence, identified as such (METHODOLOGY_STANDARDS.md §3). The reviewer never disables a production AI component.
**Access required:** Read access to the IBS register, impact tolerance statements and current IBS mapping; read access to the fallback process design documentation; the ability to disable or stub the AI component within the staging replica; access to the last three op-res scenario testing reports (reviewer-set design minimum, disclosed at scoping).
**Artefacts required:** IBS register entry for the in-scope service; stated impact tolerance (metric and value); fallback process design document; prior fallback rehearsal records (if any); current AI inventory entry for the component (from TP-GOV-002 output where available); staffing roster for the fallback function.
**Personnel required:** Op-res lead (to confirm the tolerance being tested is the current board-approved one); business process owner for the IBS; the named individual holding authority to declare the AI component "untrusted"; a sample of at least three front-line staff who would execute the fallback (reviewer-set design minimum, disclosed at scoping); a reviewer to observe and time.
**Data handling:** Synthetic or anonymised case volumes only. Where realistic volume cannot be achieved with synthetic cases, use replayed historical case *shapes* with all customer identifiers removed, and record the substitution in the working paper.

## 3. Test Design
The procedure tests two distinct trigger types, because the canvas identifies the second as the near-universal weak point:

- **Trigger A — Unavailability:** the AI component is technically down. This is the trigger most firms have contemplated.
- **Trigger B — Untrusted:** the AI component is technically available and returning fluent output, but a quality incident, detected drift or security concern means its output can no longer be relied upon. This requires a named human to make a judgement call and invoke the fallback.

For each trigger, the reviewer measures three quantities: time-to-detect-and-trigger, fallback throughput at representative volume, and resulting service delivery against the stated impact tolerance. Trigger B additionally tests whether a decision authority and decision process exist at all.

Sampling: one exercise per in-scope IBS with a material AI dependency. Where more than four such IBSs exist (reviewer-set design minimum, disclosed at scoping), sample risk-based, weighted to those with the tightest impact tolerance and the highest AI dependency depth.

## 4. Steps
1. Obtain the IBS register entry and record the exact impact tolerance metric and value (e.g. "claims first-response within 24 hours; tolerance = no more than 5% breach over a rolling 5-day disruption"). **Record:** metric, value, approval date, approving body.
2. Obtain the fallback process design document. **Record:** stated trigger conditions; whether Trigger B ("untrusted") is defined at all; named decision authority; designed throughput assumption; staffing assumption.
3. Reconcile the designed staffing assumption against the current roster for that function. **Record:** designed FTE vs actual current FTE, and any headcount change since the AI component was introduced.
4. Confirm with the op-res lead that the tolerance in step 1 is current and board-approved. **Record:** confirmation and any pending revision.
5. **Trigger A exercise.** In the staging replica, disable or stub the AI component without prior notice to the fallback staff participating. Start the clock. **Record:** wall-clock time from component disablement to (a) detection by any monitoring or human, (b) formal fallback invocation.
6. Feed the fallback process a case volume representative of peak load for the service (state the percentile used — e.g. 95th percentile daily volume observed over the last 12 months). Run for a minimum of two hours or one full processing cycle, whichever is longer (reviewer-set design minimum, disclosed at scoping). **Record:** cases completed per hour; error/rework rate; queue depth at end of run.
7. Project the observed throughput against the impact tolerance metric over the tolerance's own time window. **Record:** projected breach/no-breach and the margin.
8. **Trigger B exercise.** Restore the AI component but inject degraded output (e.g. a stubbed response set containing plausible but materially wrong values, using synthetic cases only). Do not inform participants. **Record:** whether anyone detects the degradation; how long it takes; whether the named authority is contacted; whether the fallback is invoked; and if not, why not.
9. Interview the named "untrusted" decision authority. **Record:** whether they knew they held the authority; whether they have ever exercised it; what evidence they would require before invoking; whether they believe they would face challenge for invoking wrongly.
10. Interview the three front-line participants on competency. **Record:** date of last AI-free execution of this process; self-reported confidence; observed error rate in step 6 versus any historical pre-AI baseline.
11. Compare all findings against the last three op-res scenario testing reports. **Record:** whether any AI-trigger scenario has previously been exercised, and the result.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Fallback throughput vs impact tolerance | The firm's own stated impact tolerance value for the IBS | Defined by [FCA SYSC 15A.2.5R / PRA SS1/21] — the firm sets the value; the regime mandates that it be met |
| Time-to-detect (Trigger A) | Must be short enough that detection + switchover + fallback processing still fits inside the tolerance window | Derived from the firm's own tolerance; no external threshold |
| Time-to-detect (Trigger B) | Reviewer judgement — no established threshold. Record the observed value and assess against the tolerance window | No published benchmark for AI quality-degradation detection latency |
| Staffing sufficiency | Designed FTE ≤ actual current FTE for the fallback function | Reviewer judgement against the firm's own design assumption |
| Competency currency | Reviewer judgement — no established threshold. Flag where last AI-free execution exceeds 12 months (aligns with TIERING_MODEL re-assessment cadence, not an external standard) | Bespoke |

## 6. Interpretation (per CANVASES_RES.md fields 12–14)
**Pass** where: fallback is defined with explicit triggers covering *both* unavailability and untrusted states; the rehearsed exercise demonstrates throughput sufficient to meet the impact tolerance; participating staff demonstrate current competency; and the trigger decision authority is named and has practised invoking the fallback.

**Fail** where: the fallback exists only as a policy statement with no rehearsal evidence; rehearsed throughput falls materially short of the tolerance; no "untrusted" trigger is defined (only technical outage is covered); or staff cannot execute the process to standard when tested.

**Partial** (the most common outcome, per the canvas): Trigger A is rehearsed and adequate, Trigger B is undefined or unexercised. Report as: fallback rehearsed for outright AI unavailability but not for the untrusted-output trigger, which has no defined decision authority or rehearsed process; remediation should extend scenario testing to quality-degradation triggers.

## 7. Evidence Outputs
- Fallback process design document as obtained — **L2**
- Reviewer-observed exercise log with timings and throughput counts (Trigger A) — **L3**
- Reviewer-observed exercise log for Trigger B including detection outcome — **L3**
- Staffing reconciliation working paper — **L2**
- Independent confirmation that the exercise met impact tolerance at realistic volume, signed by the reviewer — **L4**
- Records of any actual historical AI unavailability/quality incident and the fallback's real performance — **L5** (where such an incident exists; do not manufacture one)

## 8. Common Pitfalls & Limitations
- **Announced exercises.** If fallback staff know the exercise is coming, detection and switchover times are unrepresentative. Steps 5 and 8 must be unannounced to participants (though authorised by management).
- **Short-run extrapolation.** Two hours of fallback throughput does not capture fatigue, shift handover or backlog compounding. State the extrapolation explicitly and treat multi-day tolerance windows as tested only by inference.
- **Staging representativeness.** A staging replica rarely reproduces the full downstream dependency chain. Record which downstream systems were stubbed; conclusions about end-to-end tolerance compliance are weakened proportionately.
- **Confusing "a manual process exists" with "a fallback capability exists".** The manual process may exist and be unable to absorb current volumes because headcount fell when the AI was introduced. Step 3 exists precisely to catch this.
- **Trigger B is a governance test wearing a resilience costume.** If no one holds the authority, the finding belongs in both RES-001 and HUM-005 reporting; cross-reference rather than duplicate.

## 9. Time / Effort Estimate
**4 reviewer-days** per IBS exercised: 1 day artefact review and reconciliation, 1.5 days exercise execution and observation (both triggers), 0.5 day interviews, 1 day analysis and working-paper production. Add 1 day per additional IBS in a multi-IBS sample.

---
---

