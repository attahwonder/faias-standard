# CANVAS: IRQ-RES-006

## 1. IRQ ID & Title
**IRQ-RES-006: Alerting Design Blind to Slow, Gradual Quality Decay**

Register question: "Would the alerting design surface a slow degradation (gradual quality decay, rising hallucination rate) as opposed to only hard failures?"

## 2. Business Activities Affected
- **Any AI system with a long operational lifespan without retraining or re-grounding:** customer service, credit narrative generation and claims triage systems that run continuously are the most exposed, since slow decay compounds silently over months.
- **Services relying on RAG grounding against a corpus that ages:** gradual staleness produces a slow rise in hallucination rate that a threshold tuned for abrupt failure will not catch.
- **Any workflow where the "acceptable" baseline itself may drift** (e.g. seasonal or population-mix changes disguising a genuine quality decline as normal variance).

## 3. AI Behaviour(s)
- System's quality metrics change gradually over time due to data drift, corpus staleness, population shift or subtle prompt/config interactions, rather than through a single abrupt event.
- Alerting thresholds, if calibrated against short-term variance or absolute hard-failure levels, treat each small incremental change as within "normal" bounds, never triggering because no single measurement crosses the threshold.
- Cumulative effect over weeks or months can represent a materially degraded system that no single alert ever flagged.

## 4. Failure Mode
> The alerting design is calibrated to detect abrupt, hard failures (system down, error rate spike) but is statistically insensitive to slow, gradual quality decay (rising hallucination rate, declining accuracy) that unfolds over an extended period below any single-point threshold — so a materially degraded system can operate for months without triggering any alert.

## 5. Potential Consequences
- **Customer:** Cumulative exposure to a system whose quality has meaningfully declined over an extended period, with no single incident marking the point of harm — making both detection and subsequent remediation/redress assessment materially harder.
- **Institution:** When eventually discovered (via a lagging indicator such as a complaint pattern or a periodic deep-dive review), the firm faces a large backlog of potentially affected decisions/interactions to review, rather than a bounded incident.
- **Regulator:** Evidences a monitoring design gap distinct from, and more subtle than, the outright absence of monitoring addressed in RES-005 — a firm can have "monitoring" and still fail this specific test.

## 6. Failure Chain
```
Threshold-driven alerting exists (RES-005 satisfied at a basic level)
but thresholds are calibrated against absolute levels or short-window
variance, not trend/cumulative-drift statistics
  ↓ (IRQ-DAT-011: input drift baselining does not extend to a
     trend-sensitive detection design for the model's output quality)
Quality metric (e.g. hallucination rate) rises gradually, week over
week, each increment individually within "normal" short-term variance
  ↓ (IRQ-RES-006 — THIS IRQ: alerting design has no mechanism to
     detect the cumulative trend across the extended period)
System continues operating with materially degraded quality for
months; no alert ever fires because no single measurement crosses
the hard-failure threshold
  ↓
Eventual discovery (periodic deep-dive, customer complaint pattern
analysis, or model revalidation cycle) reveals an extended period of
undetected degradation

Control Breakpoints:
  • IRQ-RES-006: alerting design explicitly includes trend/cumulative-
    drift detection (e.g. statistical process control charts, rolling
    baseline comparison), not only absolute-threshold alerting
  • IRQ-DAT-011: drift baselining methodology feeds trend-sensitive
    detection criteria
  • IRQ-RES-005: the underlying active-monitoring capability this
    control depends upon must itself be functioning
```

## 7. Why a Domain Expert May Miss It
- "We have alerting" (satisfying RES-005 at a surface level) is treated as sufficient, without the further question of whether that alerting is statistically capable of detecting gradual, as opposed to abrupt, change — a distinction that requires specific statistical process control knowledge to recognise as a gap.
- Alert fatigue concerns often push teams toward wider thresholds and longer smoothing windows to reduce false positives, which directly reduces sensitivity to genuine slow decay — a well-intentioned tuning decision that creates this specific blind spot.
- Slow decay, by definition, produces no single dramatic incident to prompt investigation; the absence of an obvious trigger event means the gap can persist indefinitely without anyone having a specific reason to look for it.
- Traditional infrastructure monitoring (uptime, error rate) genuinely is well-served by hard-failure alerting, reinforcing an unexamined assumption that the same threshold philosophy suffices for AI quality metrics, which decay differently.

## 8. Assurance Objective
**AO-RES-006:** Alerting design for AI system quality and behavioural metrics shall include explicit trend and cumulative-drift detection capable of surfacing gradual degradation over an extended period, in addition to hard-failure/abrupt-change alerting.

## 9. Expected Controls (Traced)
- **Statistical process control with trend detection (e.g. CUSUM, rolling baseline comparison)** — [Page, E.S., 1954, "Continuous Inspection Schemes", Biometrika 41(1–2):100–115, https://doi.org/10.1093/biomet/41.1-2.100; extended by NIST AI RMF 1.0, January 2023, MEASURE function, to AI system performance monitoring] — detects cumulative small deviations, not only single-point threshold breaches.
- **Periodic model revalidation independent of alerting** — [PRA, SS1/23, May 2023, ongoing monitoring and periodic revalidation principle] — a scheduled, alert-independent review acts as a backstop against slow-decay blind spots.
- **Drift baselining with trend-sensitive criteria** — [linked IRQ-DAT-011, IRQ-MOD-010] — statistical baselines explicitly designed to detect gradual as well as abrupt shift.
- **Rolling cohort comparison rather than point-in-time snapshot** — Emerging Practice — comparing current performance against a rolling historical window (not just the most recent measurement) to surface trend; no single published FS-specific standard identified, drawing on general time-series monitoring practice.
- **Alert threshold review balancing sensitivity and alert fatigue** — Emerging Practice — deliberate, documented trade-off decision rather than an unexamined default toward wide thresholds.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "alerting would catch a quality problem" with no test of gradual-decay sensitivity — **L1**.
- Alerting design specification explicitly documenting trend/cumulative-drift detection logic, distinct from hard-failure thresholds — **L2**.
- Staging test: inject a simulated gradual decay (e.g. small incremental accuracy decline over a simulated multi-week period) and verify whether the alerting design detects it — **L3**.
- Independent audit confirming trend-detection logic is operating in production and has been validated against a known historical or synthetic decay scenario — **L4**.
- Production case study (if available) where trend-detection alerting successfully surfaced a genuine gradual degradation, with time-to-detection recorded — **L5**.

## 11. Independent Test
> In a non-production environment, construct a synthetic time series representing gradual quality decay (e.g. hallucination rate rising 0.5 percentage points per week over 12 weeks, each individual weekly change within normal short-term variance) and run it through the firm's actual alerting logic/configuration. Record whether and when an alert fires, compared against the point at which cumulative degradation became material. Repeat with an abrupt-change scenario as a control comparison. — **★2 Confidence — as at FAIAS v1.2.0 (12 September 2026)** (the statistical limb is peer-reviewed and multi-group, not merely "well established": CUSUM originates in [Page, Biometrika 41(1–2):100–115, 1954]; the two canonical drift detectors come from independent groups and are benchmarked against each other in the peer-reviewed record [Gama et al., Lecture Notes in Computer Science 3171, pp. 286–295, 2004; Bifet & Gavaldà, SIAM SDM 2007:443–448, which provides "rigorous guarantees of its performance, in the form of bounds on the rates of false positives and false negatives"]; and the gradual-versus-abrupt distinction this IRQ turns on is itself a published finding — "detecting the change is harder in slopes than in abrupt changes" [Bifet & Gavaldà 2007, §3, quoted from the authors' preprint of 17 October 2006]. **The test design below is that literature's own evaluation protocol** — synthetic series at a known slope, a no-change or abrupt control, and measured detection delay [Bifet & Gavaldà 2007, §4, same preprint] — so it is adopted, not constructed here. Temporal quality degradation is empirically established across four industries including finance, in 91% of 128 model/dataset pairs, with gradual degradation classified separately from explosive and from increasing-unpredictability patterns [Vela et al., Scientific Reports 12:11654, 2022, Figure 3]. The blend is held at ★2 by two things the peer-reviewed record does not supply: no published methodology addresses detection of *LLM* output-quality decay specifically (searched 12 September 2026; none found), and there is no agreed benchmark for "material cumulative degradation" in an FS service — a gap the same literature states of itself, lacking "systematic knowledge on what exactly should trigger and control model retraining" [Vela et al. 2022]. **A ★3 reading is available on §6's peer-review and multiple-independent-groups limbs; it was considered at this anchor and the rating held at ★2.**)

## 12. Pass Indicators
- Synthetic gradual-decay test triggers an alert materially before the cumulative degradation reaches a harm-relevant level.
- Alerting design documentation explicitly distinguishes trend/cumulative-drift logic from hard-failure thresholds.
- Periodic revalidation (independent of alerting) is scheduled and evidenced as a backstop.
- Threshold-sensitivity trade-off (alert fatigue versus detection speed) is a documented, deliberate decision, not a default.

## 13. Fail Indicators
- Synthetic gradual-decay test produces no alert throughout the full simulated period, despite material cumulative degradation.
- Alerting design contains only hard-failure/absolute-threshold logic, with no trend or cumulative-drift component.
- No periodic revalidation exists independent of the alerting system as a backstop.
- Historical review finds an actual gradual degradation episode that went undetected until discovered by other means (complaint, deep-dive).

## 14. Reporting Language
**Pass:** "Synthetic gradual-decay testing confirms the alerting design detects cumulative degradation materially before it reaches a harm-relevant level, distinct from and in addition to hard-failure alerting. Conclusions rest on ★2 methodology — the underlying statistical method is well-established, but FS-specific calibration is bespoke — and should be interpreted as a point-in-time capability demonstration."

**Fail:** "Synthetic gradual-decay testing produced no alert across the full simulated 12-week degradation period, despite cumulative quality decline reaching a materially harmful level. The current alerting design is limited to hard-failure detection and provides no defence against slow decay — the specific failure mode this IRQ addresses."

**Partial:** "Trend detection has been implemented for accuracy metrics but not extended to hallucination rate or tone/sentiment drift, which remain hard-failure-only. Remediation should extend trend-sensitive detection to the full quality metric set."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (gradual degradation is caught before reaching a materially harmful cumulative level)
  Likelihood: 2 (data drift, corpus staleness and population shift are foreseeable, ongoing pressures on any long-lived system)
  Detectability: 2 (trend-sensitive alerting, if working, provides earlier detection than would otherwise occur)
  Recoverability: 2 (earlier detection bounds the scale of remediation required)
  Novelty: 3 (the distinction between hard-failure and trend-sensitive alerting requires specific statistical process control knowledge)

If controls are absent or degraded:
  Severity: 3 (an extended period of undetected degradation compounds harm across a large, retrospectively-discovered population of affected decisions/interactions)
  Likelihood: 3 (probable given data drift and corpus staleness are near-universal pressures on continuously operating AI systems)
  Detectability: 4 (silent by design — this is precisely the scenario where no single measurement crosses any hard-failure threshold)
  Recoverability: 3 (large accumulated harm population makes remediation and any redress assessment materially more complex than a bounded incident)
  Novelty: 4 (the "we have alerting but it's still blind to this" distinction is genuinely counter-intuitive without deliberate testing)

Residual risk interpretation: This is a high-detectability-risk, high-novelty IRQ that specifically undermines confidence in RES-005 being satisfied at face value — a firm can pass a basic "do you have alerting" test and still fail this one; both should be assessed, not just the former.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Undetected gradual decay compounds harm across a large retrospectively-discovered population |
| **Likelihood** | 3 | Data drift and corpus staleness are near-universal, ongoing pressures on continuously operating systems |
| **Detectability** | 4 | Definitionally silent — the failure mode is specifically designed to evade single-point threshold alerting |
| **Recoverability** | 3 | Large accumulated-harm populations complicate remediation and redress assessment relative to a bounded incident |
| **Novelty** | 4 | Counter-intuitive even for teams who believe they already have adequate monitoring |

## 17. Regulatory Basis
> [PRA, SS1/23, May 2023] establishes ongoing monitoring and periodic revalidation as continuous obligations, which this IRQ interprets as requiring sensitivity to gradual as well as abrupt change. [PRA, SS1/21, March 2021] and [Regulation (EU) 2022/2554, DORA, Art. 10] establish detection obligations generally; neither specifies trend-detection methodology explicitly, so this IRQ's specific technical requirement (trend/cumulative-drift sensitivity) is an interpretive extension rather than a directly cited rule [UNVERIFIED — no more specific PRA/DORA text on gradual-degradation/trend-detection methodology was located after search] (verified 29 Jul 2026).

## 18. Research Basis
> The statistical basis for trend and cumulative-drift detection is peer-reviewed, multi-group and named, not a general practice claim. CUSUM originates in [Page, E.S., 1954, "Continuous Inspection Schemes", Biometrika 41(1–2):100–115, https://doi.org/10.1093/biomet/41.1-2.100], with the change-point inference that completes the "Page-Hinkley" pairing in [Hinkley, D.V., 1971, "Inference about the change-point from cumulative sum tests", Biometrika 58(3):509–523, https://doi.org/10.1093/biomet/58.3.509]. The two canonical drift detectors come from independent groups: DDM in [Gama, J., Medas, P., Castillo, G., Rodrigues, P., 2004, "Learning with Drift Detection", Advances in Artificial Intelligence – SBIA 2004, Lecture Notes in Computer Science 3171, pp. 286–295, https://doi.org/10.1007/978-3-540-28645-5_29] and ADWIN in [Bifet, A., Gavaldà, R., 2007, "Learning from Time-Changing Data with Adaptive Windowing", Proc. 2007 SIAM International Conference on Data Mining, pp. 443–448, https://doi.org/10.1137/1.9781611972771.42], the latter providing "rigorous guarantees of its performance, in the form of bounds on the rates of false positives and false negatives" and benchmarking itself directly against DDM. The field is surveyed in [Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., Bouchachia, A., 2014, "A survey on concept drift adaptation", ACM Computing Surveys 46(4):1–37, https://doi.org/10.1145/2523813] — already carried in this repository's academic source register and cited at IRQ-DAT-011, to which this IRQ's failure chain links.
>
> Two findings in that literature are load-bearing for this IRQ and replace what was previously asserted. First, the gradual-versus-abrupt asymmetry is a published result, not an inference: "As predicted by theory, detecting the change is harder in slopes than in abrupt changes" [Bifet & Gavaldà 2007, §3; read at the authors' preprint of 17 October 2006, the version relied on, the SDM proceedings text not having been reached]. Second, the Independent Test at §11 is that literature's own evaluation protocol rather than a design constructed here — synthetic series at a known slope, a no-change control for false positives, and measured detection delay, reported per slope [Bifet & Gavaldà 2007, §4, same preprint].
>
> Temporal quality degradation is empirically established in peer-reviewed work covering financial-services data: [Vela, D., Sharp, A., Zhang, R., Nguyen, T., Hoang, A., Pianykh, O.S., 2022, "Temporal quality degradation in AI models", Scientific Reports 12:11654, https://doi.org/10.1038/s41598-022-15245-z] reports degradation in 91% of 128 (model, dataset) pairs drawn from healthcare operations, transportation, finance and weather, and classifies the degradation it observed into at least three patterns (Figure 3 A–C): gradual, in which relative model error increases no faster than linearly over time; explosive; and increasing unpredictability. The same paper states the benchmark gap this IRQ's ★ turns on: the field still lacks "systematic knowledge on what exactly should trigger and control model retraining".
>
> [NIST AI RMF 1.0, January 2023, MEASURE function] extends continuous measurement expectations to AI systems generally. **The residual gap is narrower than previously recorded and is stated precisely: no peer-reviewed research addresses detection of slow decay in *LLM output quality* specifically, in financial services or elsewhere** [UNVERIFIED — searched 12 September 2026 across peer-reviewed indexing; none located. Candidate material on LLM drift is preprint or vendor-published only and is not cited here].
>
> **Research basis last reviewed:** 12 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-RES-005 (G.3 Monitoring & Alerting: underlying active-monitoring capability this control depends upon)
  - IRQ-DAT-011 (A.5 Data Drift: drift baselining feeds trend-sensitive detection criteria)
  - IRQ-MOD-010 (B.5 Distribution Shift & Evaluation Integrity: revalidation triggers per shift type, incl. gradual)
```

## 20. References
```
[1] Prudential Regulation Authority, 2023. "SS1/23 — Model risk management principles for banks."
    Published: May 2023
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss

[2] Prudential Regulation Authority, 2021. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2021
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss

[3] NIST, 2023. "Artificial Intelligence Risk Management Framework (AI RMF) Version 1.0."
    Published: January 2023
    URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf

[4] Page, E.S., 1954. "Continuous Inspection Schemes." Biometrika 41(1–2):100–115.
    Published: 1954
    URL: https://doi.org/10.1093/biomet/41.1-2.100

[5] Hinkley, D.V., 1971. "Inference about the change-point from cumulative sum tests." Biometrika 58(3):509–523.
    Published: 1971
    URL: https://doi.org/10.1093/biomet/58.3.509

[6] Gama, J., Medas, P., Castillo, G., Rodrigues, P., 2004. "Learning with Drift Detection." Advances in Artificial Intelligence – SBIA 2004, Lecture Notes in Computer Science 3171, pp. 286–295.
    Published: 2004
    URL: https://doi.org/10.1007/978-3-540-28645-5_29

[7] Bifet, A., Gavaldà, R., 2007. "Learning from Time-Changing Data with Adaptive Windowing." Proceedings of the 2007 SIAM International Conference on Data Mining, pp. 443–448.
    Published: 2007
    URL: https://doi.org/10.1137/1.9781611972771.42

[8] Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., Bouchachia, A., 2014. "A survey on concept drift adaptation." ACM Computing Surveys 46(4):1–37.
    Published: March 2014
    URL: https://doi.org/10.1145/2523813

[9] Vela, D., Sharp, A., Zhang, R., Nguyen, T., Hoang, A., Pianykh, O.S., 2022. "Temporal quality degradation in AI models." Scientific Reports 12:11654.
    Published: 8 July 2022
    URL: https://doi.org/10.1038/s41598-022-15245-z
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.3 (Operational Resilience domain, Monitoring & Alerting)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): "We have alerting" is assumed to cover slow decay, when hard-failure thresholds are specifically insensitive to gradual, cumulative change.
✓ Test 2 (Plausible Harm): Grounded in PRA SS1/23 ongoing monitoring obligations and established statistical process control principles.
✓ Test 3 (Testable): Answerable via synthetic gradual-decay injection testing against actual alerting configuration.
✓ Test 4 (Decision-Relevant): Outcome gates whether RES-005's monitoring claim can be trusted for slow-decay scenarios specifically.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): ★2 justification rewritten at an unchanged rating (no ★ movement) — the statistical limb re-anchored from "a well-established general discipline" to peer-reviewed primaries (Page, Biometrika 41(1–2), 1954; Hinkley, Biometrika 58(3), 1971; Gama et al., SBIA 2004; Bifet & Gavaldà, SIAM SDM 2007; Gama et al., ACM Computing Surveys 46(4), 2014; Vela et al., Scientific Reports 12:11654, 2022); the field 9 CUSUM attribution re-anchored to Page (1954), field 18 rewritten, six references added at §20; the ★3 reading recorded as considered at this anchor with the rating held; the TP-RES-006 playbook sheet carries the same basis.
- v1.3.0 (2026-10): Field 20 — reference [3], AI RMF 1.0, given the URL of NIST AI 100-1 in place of the URL of NIST AI 600-1. ★2 unchanged.
```

---
---

