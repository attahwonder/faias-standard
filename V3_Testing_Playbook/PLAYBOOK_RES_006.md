# TP-RES-006 — Gradual-Decay Detection Test

## 1. Procedure Identity
**Procedure ID:** TP-RES-006
**IRQ:** IRQ-RES-006 — Alerting Design Blind to Slow, Gradual Quality Decay
**Assurance objective:** AO-RES-006 — Alerting design for AI system quality and behavioural metrics shall include explicit trend and cumulative-drift detection capable of surfacing gradual degradation over an extended period, in addition to hard-failure/abrupt-change alerting.
**Subdomain:** G.3 Monitoring & Alerting
**★ Confidence (carried from canvas, unchanged):** ★2 — the statistical limb is peer-reviewed and multi-group, not merely well established: CUSUM originates in [Page, Biometrika 41(1–2):100–115, 1954], and the two canonical drift detectors come from independent groups benchmarked against each other in the peer-reviewed record [Gama et al., Lecture Notes in Computer Science 3171, pp. 286–295, 2004; Bifet & Gavaldà, SIAM SDM 2007:443–448]. The blend is held at ★2 by two things that record does not supply: no published methodology addresses detection of LLM output-quality decay specifically, and there is no agreed benchmark for "material cumulative degradation" in an FS service. A ★3 reading is available on §6's peer-review and multiple-independent-groups limbs; it was considered at this anchor and the rating held at ★2.
**Method classification:** Adapted Industry Practice (SPC trend detection) applied to a bespoke AI quality-metric context.

## 2. Preconditions
**Environment:** A staging or offline replica of the firm's *actual* alerting logic and configuration — not a reviewer-built reimplementation. The whole value of the procedure is that it runs synthetic data through the real rules.
**Access required:** Ability to replay a synthetic time series through the production alerting configuration in an isolated instance; read access to alerting design documentation; read access to historical quality-metric series and to any periodic revalidation schedule.
**Artefacts required:** Alerting configuration export; alerting design documentation distinguishing (or failing to distinguish) trend logic from absolute thresholds; historical quality-metric series for the review period; periodic revalidation schedule and its outputs; any documented alert-fatigue/sensitivity trade-off decision.
**Personnel required:** Observability engineer able to replay series through the configuration; the metric owner; reviewer with basic statistical competence in trend detection.
**Data handling:** Synthetic series only for injection. Historical series used for the retrospective component are aggregate; confirm non-decomposability to individual records before extraction.

## 3. Test Design
Construct a synthetic gradual-decay series in which no single period-on-period change exceeds normal short-term variance, but cumulative degradation over the full window is unambiguously material. The canvas's worked example is hallucination rate rising 0.5 percentage points per week over 12 weeks; adapt the metric and gradient to the system under test, and document the adaptation.

Run three series through the real alerting configuration:

- **S1 — Gradual decay:** the primary test. Does anything fire, and when?
- **S2 — Abrupt change (control):** a step change of the same total magnitude, to confirm the configuration alerts at all and to contrast detection latency.
- **S3 — Flat with noise (negative control):** stable performance with realistic variance, to establish the false-positive behaviour of any trend rule that does fire on S1.

S3 is essential. A configuration that alerts on S1 *and* on S3 has not detected decay; it has an oversensitive rule that will be tuned out within a month.

## 4. Steps
1. Obtain the alerting configuration and design documentation. **Record:** whether trend or cumulative-drift logic exists as a distinct construct from absolute thresholds; the parameters of any trend rule (window length, sensitivity).
2. Establish the metric's historical variance. From the historical series, compute period-on-period variation under stable conditions. **Record:** the variance figure used to calibrate S1's per-period step so that it stays within normal noise.
3. Define the "materiality point" — the cumulative degradation level at which the reviewer, in consultation with the metric owner, judges harm becomes relevant. **Record:** the value and the reasoning. This is explicitly a judgement, not a benchmark, and must be labelled as such.
4. Construct S1, S2 and S3. **Record:** full series definitions and generation parameters, so the test is reproducible.
5. Replay **S1** through the real alerting configuration. **Record:** whether any alert fires; at which period; the cumulative degradation at the point of firing; and the gap between the alert point and the materiality point defined in step 3.
6. Replay **S2**. **Record:** whether an alert fires and at which period. If S2 fires and S1 does not, the configuration is abrupt-change-only — the exact failure mode this IRQ addresses.
7. Replay **S3**. **Record:** whether any alert fires. Any alert on S3 is a false positive and must be reported alongside the S1 result, since it bears directly on whether an S1-firing rule would survive in practice.
8. Repeat S1 at two additional gradients (e.g. half and double the primary gradient) — a reviewer-set design minimum, disclosed at scoping. **Record:** the shallowest gradient at which detection still occurs — this is the configuration's effective detection floor and is the most useful single number the procedure produces.
9. Review the periodic revalidation schedule. **Record:** whether an independent periodic revalidation exists as a backstop to alerting; its cadence; its last execution and findings.
10. Review the historical series for any real episode of gradual degradation. **Record:** whether it was detected by alerting, by revalidation, or by an external route (complaint, deep-dive).
11. Review any documented decision on the alert-fatigue/detection-speed trade-off. **Record:** whether the current sensitivity is a deliberate documented choice or an unexamined default.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| S1 detection point vs materiality point | Alert must fire materially before the materiality point. The materiality point itself is reviewer judgement — no established threshold for "material cumulative degradation" in AI quality metrics | Explicitly bespoke; the reason for ★2 |
| S2 detection (control) | Must fire; failure indicates the configuration does not alert at all | Established SPC practice |
| S3 false positives (negative control) | Zero | Established SPC practice |
| Effective detection floor (shallowest detected gradient) | Reviewer judgement — no established threshold. Report as a descriptive capability measure | Bespoke |
| Existence of distinct trend/cumulative-drift logic | Must be present and documented as distinct from absolute thresholds | Categorical per canvas pass indicator |

## 6. Interpretation (per CANVASES_RES.md fields 12–14)
**Pass** where: the synthetic gradual-decay test triggers an alert materially before cumulative degradation reaches a harm-relevant level; alerting design documentation explicitly distinguishes trend/cumulative-drift logic from hard-failure thresholds; periodic revalidation is scheduled and evidenced as an independent backstop; and the sensitivity trade-off is a documented deliberate decision rather than a default.

**Fail** where: S1 produces no alert throughout the full simulated period despite material cumulative degradation; alerting contains only hard-failure/absolute-threshold logic; no periodic revalidation exists independent of alerting; or historical review finds an actual gradual degradation episode that went undetected until discovered by other means.

**Partial** where trend logic exists and fires, but only at a gradient far steeper than plausible real-world decay (step 8 detection floor is high), or where it fires on S1 but also on S3.

## 7. Evidence Outputs
- Alerting configuration export and design documentation — **L2**
- Synthetic series definitions (S1/S2/S3 plus gradient variants), enabling reproduction — **L3**
- Replay results log with detection points — **L3**
- Reviewer's detection-floor analysis and materiality-point rationale — **L4** where the reviewer is independent
- Historical series and any real gradual-degradation episode record — **L5**

## 8. Common Pitfalls & Limitations
- **Reimplementing the alerting logic.** If the reviewer writes their own trend detector and tests that, the procedure proves nothing about the firm. Replay through the real configuration.
- **Omitting the negative control.** Without S3, an alert on S1 cannot be distinguished from a rule that alerts on everything.
- **Treating the materiality point as objective.** It is a judgement made with the metric owner and must be labelled as such in every report; the absence of a benchmark here is precisely why the canvas rates this ★2.
- **Synthetic gradients that are too steep.** A 5-point-per-week decay will be caught by an absolute threshold and tells you nothing about trend detection. Calibrate to step 2's measured variance.
- **Confusing revalidation with alerting.** Periodic revalidation is a backstop, not a substitute; a firm relying solely on annual revalidation to catch decay can at best be Partial.

## 9. Time / Effort Estimate
**3 reviewer-days**: 0.5 day configuration review, 0.5 day historical variance analysis and series construction, 1 day replay execution across S1/S2/S3 and gradient variants, 1 day analysis and working papers.

---
---

