# TP-RES-005 — Threshold-to-Response Monitoring Chain Test

## 1. Procedure Identity
**Procedure ID:** TP-RES-005
**IRQ:** IRQ-RES-005 — Dashboard-Only Monitoring Without Threshold-Triggered Response
**Assurance objective:** AO-RES-005 — Quality, drift and behavioural anomaly metrics for every production AI system shall be monitored continuously against defined thresholds that automatically trigger a pre-agreed response playbook, not solely displayed for periodic human review.
**Subdomain:** G.3 Monitoring & Alerting
**★ Confidence (carried from canvas, unchanged):** ★3 — statistical process control and alerting design is a well-established general engineering discipline; setting FS/AI-specific threshold values is more bespoke, moderating confidence from ★4.
**Method classification:** Adapted Industry Practice — statistical process control and alerting-design review, applied to AI quality/drift metrics.

## 2. Preconditions
**Environment:** Staging environment carrying the same monitoring and alerting configuration as production, or an isolated replica of the alerting configuration into which synthetic metric values can be injected. Read-only access to production monitoring *history* is permitted and expected; no production alerting rule may be modified.
**Access required:** Read access to the monitoring configuration (metric definitions, threshold values, alert routing) for a sample of production AI systems; ability to inject a synthetic metric breach into a staging alerting instance; read access to historical metric time series and to the alert/incident record.
**Artefacts required:** Monitoring design documentation; threshold register; response playbooks; alert routing configuration; historical metric series for the review period; historical alert and incident records; MI packs evidencing what reaches governance.
**Personnel required:** Monitoring/observability engineer; the on-call or first-response team named in the playbook; reviewer.
**Data handling:** Historical metric series are aggregate and generally non-personal; confirm before extraction that no metric series is decomposable to individual customer records. Synthetic breach values only in the staging instance.

## 3. Test Design
This procedure traces the chain from *metric defined* → *threshold set* → *alert fires* → *playbook exists* → *response occurs* → *governance sees it*. A break at any link fails the objective, and the most common break is between "alert fires" and "playbook exists".

Sampling: a risk-based sample of production AI systems weighted to Tier 2–3 under TIERING_MODEL.md, minimum five systems (reviewer-set design minimum, disclosed at scoping) or all in-scope systems where fewer than five exist.

Two evidence routes are combined because neither alone is sufficient: a **forward test** (inject a synthetic breach in staging, observe end-to-end behaviour) and a **backward test** (find historical breaches in the metric series and trace what actually happened).

## 4. Steps
1. For each sampled system, obtain the metric definitions and threshold register. **Record:** which of quality, drift and behavioural-anomaly metric families are covered; the threshold value per metric; whether each threshold has a documented derivation or is a default.
2. Classify each metric as *threshold-and-alert*, *threshold-only (displayed, no alert)*, or *dashboard-only (no threshold)*. **Record:** counts per system. This classification is the core finding of the procedure.
3. Obtain the response playbook for each threshold-and-alert metric. **Record:** whether a playbook exists; whether it names an owner, an action and a timeframe; date of last review.
4. **Forward test.** In the staging alerting instance, inject a synthetic metric value breaching the threshold. **Record:** whether the alert fires; time from breach to alert; where the alert routes; whether the recipient acknowledges within the playbook's stated timeframe.
5. Repeat step 4 for at least one metric from each of the three metric families per sampled system.
6. **Backward test.** Search the historical metric series for the review period for values that crossed a defined threshold. **Record:** every historical breach found.
7. For each historical breach found, search the alert and incident record for a corresponding alert. **Record:** breaches with a matching alert; breaches with no matching alert (this is the highest-value finding in the procedure — a threshold that was crossed with silence).
8. For each historical breach with a matching alert, trace the response. **Record:** whether the playbook was followed; what action was taken; elapsed time.
9. Trace alert output to governance. **Record:** whether the alert or its aggregate appears in any MI pack reaching an accountable governance body (cross-reference TP-GOV-008, which tests the governance-consumption side of the same chain).
10. Interview the first-response team. **Record:** whether they know the playbook exists; whether they have ever executed it; whether alert volume is such that they routinely dismiss AI alerts.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Proportion of metrics that are dashboard-only | Zero for quality/drift/anomaly metrics on sampled systems; the canvas treats dashboard-only monitoring as a fail indicator | Categorical per canvas |
| Alert fires on injected breach | 100% of injected breaches must produce an alert | Established alerting-design practice; categorical |
| Historical breaches with no corresponding alert | Zero | Categorical per canvas fail indicator |
| Threshold value adequacy | Reviewer judgement — no established threshold. Statistical process control provides the *method* (e.g. control limits at a stated number of standard deviations) but the value appropriate to an AI quality metric in an FS context is firm-specific | Explicitly bespoke; this is the reason for ★3 rather than ★4 |
| Alert acknowledgement time | The firm's own playbook-stated timeframe | Firm-set |

## 6. Interpretation (per CANVASES_RES.md fields 12–14)
**Pass** where: all sampled production AI systems have defined thresholds with automated alerting rather than dashboard-only visibility; staging or historical evidence confirms alerts fire correctly on threshold breach; defined response playbooks exist and have been followed for historical breaches; and alert output reaches governance via a defined escalation path, evidenced by MI.

**Fail** where: monitoring consists solely of a dashboard with no threshold or alerting logic; no response playbook exists even where thresholds are nominally defined; a historical metric breach is found with no corresponding alert or documented response; or alert output does not reach any accountable governance function.

**Partial** where thresholds and alerts exist for quality metrics but not for drift or behavioural-anomaly metrics, or where alerts fire correctly but no playbook defines the response. Name the specific broken link in the chain.

## 7. Evidence Outputs
- Threshold register and metric classification matrix — **L2**
- Response playbooks as obtained — **L2**
- Forward-test injection log showing alert-fire behaviour — **L3**
- Backward-test reconciliation of historical breaches against alert records — **L4** where performed independently by the reviewer
- Historical metric series and incident records as operational data — **L5**

## 8. Common Pitfalls & Limitations
- **Accepting the threshold register at face value.** A threshold documented in a register but absent from the alerting configuration is the single most common finding. Always inspect the live configuration, not the register.
- **The backward test is the valuable half.** Firms can usually make a synthetic alert fire. Whether a real breach three months ago produced silence is the harder and more probative question.
- **Alert fatigue masquerading as coverage.** Step 10 exists because a system generating hundreds of dismissed alerts satisfies the letter of the objective and defeats its purpose.
- **Scope overlap with GOV-008.** This procedure ends at "the signal was generated and routed". Whether governance *consumed* it belongs to TP-GOV-008. Cross-reference; do not double-report.
- **Threshold values cannot be benchmarked externally.** Report threshold adequacy as reviewer judgement, consistent with the ★3 rating.

## 9. Time / Effort Estimate
**3 reviewer-days**: 1 day configuration and threshold review across the sample, 0.5 day forward-test injection, 1 day backward-test reconciliation against historical series, 0.5 day interviews and working papers. Add 0.5 day per system beyond five.

---
---

