# CANVAS: IRQ-RES-005

## 1. IRQ ID & Title
**IRQ-RES-005: Dashboard-Only Monitoring Without Threshold-Triggered Response**

Register question: "Are quality, drift, and behavioural anomaly metrics monitored continuously with thresholds that trigger defined responses, not just dashboards?"

## 2. Business Activities Affected
- **Every production AI system in the estate:** ongoing quality, drift and anomaly monitoring is the mechanism by which any other control in this register (fallback triggers, rollback triggers, escalation triggers) actually gets invoked in practice — without it, every downstream control is dependent on someone noticing a dashboard.
- **Model risk ongoing monitoring obligations:** independent validation and periodic review depend on monitoring data actually existing and being actionable.
- **Any AI system feeding governance escalation (GOV-008):** monitoring is the upstream source; if it does not trigger defined responses, governance has nothing to act on regardless of its own maturity.

## 3. AI Behaviour(s)
- System's quality, drift and behavioural metrics (accuracy, hallucination rate, refusal rate, latency, distributional statistics) are computed and displayed, typically on an operational dashboard reviewed by a human at some cadence.
- Metrics may cross a concerning level without any automated mechanism that distinguishes "worth investigating" from "acceptable normal variance," relying instead on a human noticing during a periodic dashboard review.
- Response to a concerning metric, where it occurs, is ad hoc rather than following a pre-agreed playbook.

## 4. Failure Mode
> Quality, drift and behavioural anomaly metrics are visible on a dashboard but have no defined thresholds that automatically trigger an alert and a pre-agreed response playbook, so detection of a degrading AI system depends on a human periodically choosing to look at, correctly interpret, and act on a dashboard — rather than on an active monitoring control.

## 5. Potential Consequences
- **Institution:** A material quality or drift event goes unnoticed for an extended period because no one happened to review the relevant dashboard metric at the right time; downstream controls (fallback, rollback, escalation) that depend on monitoring as their trigger never fire.
- **Customer:** Continued exposure to a degrading AI system for longer than necessary, because detection relied on passive observation rather than active alerting.
- **Regulator:** Monitoring that exists only as a dashboard, without evidenced threshold-triggered response, does not meet the "continuous monitoring with defined triggers" expectation embedded in operational resilience and model risk management guidance.

## 6. Failure Chain
```
Quality/drift/behavioural metrics are computed and displayed on a
dashboard; no automated threshold or alerting logic is attached
  ↓ (IRQ-RES-005 — THIS IRQ: monitoring is passive, not active)
Metric crosses a concerning level (e.g. hallucination rate rising,
accuracy dropping) but no alert fires; detection depends entirely on
a human reviewing the dashboard at the right moment
  ↓ (IRQ-GOV-008: even if governance wanted to act on monitoring
     signals, no signal reaches it because none was generated)
Degradation continues unaddressed for an extended period, since the
downstream fallback/rollback/escalation controls that depend on
monitoring as their trigger have nothing to respond to
  ↓
Eventually detected via customer complaint, incident, or a rare
manual deep-dive — far later than a threshold-triggered alert would
have achieved

Control Breakpoints:
  • IRQ-RES-005: threshold-driven monitoring with pre-agreed response
    playbooks, not dashboard-only visibility
  • IRQ-GOV-008: governance escalation triggers depend on RES-005
    actually generating a signal to escalate
  • IRQ-RES-006: slow-decay detection specifically requires threshold
    design sensitive to gradual, not just abrupt, change
```

## 7. Why a Domain Expert May Miss It
- "We have a monitoring dashboard" is treated as equivalent to "we have monitoring," when the two are materially different — a dashboard is a display mechanism, monitoring (in the operational resilience sense) requires an active, threshold-triggered response capability.
- Traditional infrastructure monitoring (CPU, memory, uptime) has mature threshold-alerting tooling built in by default; AI-specific quality/drift metrics are newer and often bolted on without the same threshold-alerting discipline being applied by teams unfamiliar with the difference.
- Dashboard reviews are often assigned as a periodic task (e.g. weekly) to a team member, creating a false sense that "someone is watching," when in practice competing priorities mean dashboards are reviewed inconsistently or superficially.
- Setting meaningful thresholds for AI-specific metrics (what hallucination rate is "concerning" versus "normal variance") requires domain judgement that is harder to calibrate than infrastructure thresholds, so teams may defer defining them indefinitely rather than accept an imperfect threshold.

## 8. Assurance Objective
**AO-RES-005:** Quality, drift and behavioural anomaly metrics for every production AI system shall be monitored continuously against defined thresholds that automatically trigger a pre-agreed response playbook, not solely displayed for periodic human review.

## 9. Expected Controls (Traced)
- **Threshold-driven continuous monitoring** — [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021), para 4.16, operational resilience maintained as a dynamic activity for important business services] — extended to AI-specific quality/drift/anomaly metrics with defined thresholds, not dashboard-only visibility.
- **Pre-agreed response playbooks per threshold breach** — [Regulation (EU) 2022/2554, DORA, Art. 10(2), detection mechanisms that define alert thresholds and criteria to trigger and initiate ICT-related incident response processes] — detection mechanisms should trigger defined response actions.
- **Model risk ongoing performance monitoring** — [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023), ongoing monitoring principle] — monitoring is a continuous obligation, not a one-time validation event.
- **Statistical process control / anomaly detection methodology** — [established general statistical monitoring practice; NIST AI RMF 1.0, January 2023, MEASURE function] — quantitative basis for setting meaningful thresholds distinguishing normal variance from concerning drift.
- **Escalation trigger to governance** — [linked IRQ-GOV-008] — monitoring output must reach accountable governance bodies through a defined trigger, not rely on ad hoc awareness.

## 10. Expected Evidence (Tagged L1–L5)
- Screenshot of a monitoring dashboard with no accompanying threshold or alert configuration — **L1**.
- Monitoring design specification defining metrics, thresholds and the response playbook for each threshold breach — **L2**.
- Staging test: inject a metric breach (e.g. simulate a hallucination rate spike) and verify the alert fires and the playbook is followed — **L3**.
- Independent audit confirming threshold-triggered alerting is operating in production, sampled across the AI system population — **L4**.
- Production alert log over the last 12 months showing threshold breaches, alerts fired, and playbook actions taken — **L5**.

## 11. Independent Test
> For a sample of production AI systems, verify (a) defined thresholds exist for quality/drift/anomaly metrics, (b) a staging or historical test demonstrates the alert actually fires on threshold breach, (c) a defined response playbook exists and was followed for any historical breach. Where feasible, inject a synthetic metric breach in staging and observe end-to-end alert-to-response behaviour. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (statistical process control and alerting design is a well-established general engineering discipline; setting FS/AI-specific threshold values is more bespoke, moderating confidence from ★4).

## 12. Pass Indicators
- All sampled production AI systems have defined thresholds with automated alerting, not dashboard-only visibility.
- Staging or historical evidence confirms alerts fire correctly on threshold breach.
- Defined response playbooks exist and have been followed for historical breaches.
- Alert output reaches governance via a defined escalation path (GOV-008), evidenced by MI.

## 13. Fail Indicators
- Monitoring consists solely of a dashboard with no threshold or alerting logic attached.
- No response playbook exists for a threshold breach, even where thresholds are nominally defined.
- A historical metric breach is found in the data with no corresponding alert or documented response.
- Alert output, where it exists, does not reach any accountable governance function.

## 14. Reporting Language
**Pass:** "Sampled production AI systems have defined thresholds with automated alerting and evidenced response playbooks, tested via staged breach injection and confirmed operating in production over the review period. Conclusions rest on ★3 methodology — established alerting design practice, AI-specific threshold calibration less standardised — and should be read as professional assessment."

**Fail:** "Sampled production AI systems display quality/drift metrics on a dashboard only; no threshold or automated alerting exists. A historical metric breach was identified in the underlying data with no corresponding alert or response action taken. This is a foundational monitoring gap: detection of degradation depends entirely on passive human observation."

**Partial:** "Threshold-driven alerting exists for accuracy and latency metrics but not for hallucination rate or distributional drift, which remain dashboard-only. Remediation should extend threshold design to the full metric set, prioritising hallucination rate given its direct customer-harm link."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (breaches are detected and acted upon promptly, limiting cumulative exposure)
  Likelihood: 2 (metric breaches occur periodically as a normal feature of production operation)
  Detectability: 1 (active, threshold-triggered alerting provides near-real-time detection by design)
  Recoverability: 2 (prompt detection enables prompt remediation via the connected response playbook)
  Novelty: 2 (the concept of threshold-triggered monitoring is familiar from infrastructure monitoring; the AI-specific extension is a natural, if sometimes neglected, extension)

If controls are absent or degraded:
  Severity: 3 (a material degradation event persists undetected for an extended period, affecting multiple customers/decisions)
  Likelihood: 3 (probable — without threshold-triggered alerting, detection depends entirely on inconsistent human dashboard review)
  Detectability: 4 (dashboard-only monitoring is functionally equivalent to no monitoring for practical detection purposes)
  Recoverability: 3 (extended undetected exposure means remediation, once discovered, must address a larger accumulated harm)
  Novelty: 3 (the "dashboard is not monitoring" distinction is easy to overlook without deliberate scrutiny)

Residual risk interpretation: This IRQ is foundational — nearly every other detection-dependent control in the RES and GOV domains relies on this one actually functioning; it should be treated as a priority baseline capability rather than an optional enhancement.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Undetected degradation can persist and compound across multiple customers/decisions before any other control engages |
| **Likelihood** | 3 | Dashboard-only monitoring without active alerting is a common, easily-overlooked gap |
| **Detectability** | 4 | Absent threshold-triggered alerting, detection is functionally passive and unreliable |
| **Recoverability** | 3 | Extended undetected exposure increases the scale of remediation required once discovered |
| **Novelty** | 3 | The distinction between "visible on a dashboard" and "actively monitored" is easy for non-specialist reviewers to miss |

## 17. Regulatory Basis
> [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021)] states that, after 31 March 2025, maintaining operational resilience will be a dynamic activity, and that firms should have strategies, processes and systems that enable them to address risks to their ability to remain within their impact tolerance for each important business service (para 4.16); it states no monitoring expectation, and this canvas reads threshold-driven monitoring as one such system. [Regulation (EU) 2022/2554, DORA, Art. 10] requires mechanisms to promptly detect ICT-related incidents, implying active detection rather than passive dashboard availability. [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023)] establishes ongoing monitoring as a continuous model risk management obligation, not a one-time validation event.

## 18. Research Basis
> [NIST AI RMF 1.0, January 2023, MEASURE function] establishes the general expectation that AI system performance be continuously measured against defined criteria. No peer-reviewed research is required to establish the general distinction between passive dashboards and active threshold-triggered alerting, which is a long-established principle in site-reliability and statistical process control literature, applied here to AI-specific quality/drift metrics.
>
> [Rabanser, S., Günnemann, S., Lipton, Z., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", Advances in Neural Information Processing Systems 32 (NeurIPS 2019); preprint arXiv:1810.11953] is the peer-reviewed method study closest to the detection step. It compares methods for detecting a shift in the data that a model receives, and finds that a two-sample test applied after dimensionality reduction with a pre-trained classifier performs best across the shifts it tests. Its main experiments use the MNIST and CIFAR-10 image datasets, and its authors name detection on online data, and other domains including natural language processing, as open work. It compares detection statistics. It does not test an alerting pipeline, so it informs the choice of detection method and not the alert-to-response chain that field 11 tests. The authors state that their code is at github.com/steverab/failing-loudly. No ★ change follows from this addition.
>
> **[FAIAS Incident Register, row 77, "Anthropic postmortem of three infrastructure bugs", 2025]** — the provider's own postmortem records that detection depended on people reading user reports: "These initial reports were difficult to distinguish from normal variation in user feedback", and the provider states that "we relied too heavily on noisy evaluations". A provider-side serving fault ran for weeks before it was found. The postmortem does not say whether the provider had automatic alert thresholds linked to a response. The provider is not a financial-services firm.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-GOV-008 (I.3 Validation & Oversight: monitoring signals must reach accountable governance bodies)
  - IRQ-RES-006 (G.3 Monitoring & Alerting: slow-decay detection specifically requires threshold sensitivity to gradual change)
  - IRQ-MOD-010 (B.5 Distribution Shift: monitoring feeds shift-type-specific revalidation triggers)
  - IRQ-TPR-004 (F.2 Model Change Management: canary testing depends on this monitoring capability)
```

## 20. References
```
[1] Prudential Regulation Authority, 2022. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2022 (11 March 2022, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss

[2] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 10.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[3] Prudential Regulation Authority, 2026. "SS1/23 — Model risk management principles for banks."
    Published: April 2026 (16 April 2026, updating 17 May 2023)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss

[4] NIST, 2023. "Artificial Intelligence Risk Management Framework (AI RMF) Version 1.0."
    Published: January 2023
    URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf

[5] Rabanser, S., Günnemann, S., Lipton, Z., 2019. "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift." Advances in Neural Information Processing Systems 32 (NeurIPS 2019). Preprint: arXiv:1810.11953. Code stated in the paper: github.com/steverab/failing-loudly.
    Published: 2019
    URL: https://proceedings.neurips.cc/paper/2019/hash/846c260d715e5b854ffad5f70a516c88-Abstract.html
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.3 (Operational Resilience domain, Monitoring & Alerting)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): "We have a dashboard" is conflated with "we have monitoring"; the distinction is invisible without deliberate scrutiny.
✓ Test 2 (Plausible Harm): Grounded in PRA SS1/21 (operational resilience maintained as a dynamic activity, para 4.16) and DORA Art. 10 detection obligations.
✓ Test 3 (Testable): Answerable via staged breach-injection testing of the alert-to-response chain.
✓ Test 4 (Decision-Relevant): Outcome gates whether every downstream detection-dependent control can be relied upon.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.3.0 (2026-10): Field 9 — the DORA citation narrowed from "detection and response mechanisms" to Art. 10(2): detection mechanisms that define alert thresholds and criteria to trigger ICT-related incident response processes. Field 20 — reference [4], AI RMF 1.0, given the URL of NIST AI 100-1 in place of the URL of NIST AI 600-1. ★3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS1/21 gives its current version, March 2022 (11 March 2022, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9, 17 and 21 — the PRA SS1/21 limb states what the statement says, that maintaining operational resilience is a dynamic activity (para 4.16), in place of an "ongoing monitoring expectation", which SS1/21 does not state; threshold-driven monitoring is stated as the canvas's reading. The DORA and SS1/23 limbs are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/21 cited as its March 2022 version (11 March 2022, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 77, Anthropic postmortem of three infrastructure bugs, in a provider's own serving infrastructure). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — Rabanser, Günnemann and Lipton (NeurIPS 2019) cited as the peer-reviewed method study for dataset-shift detection, with its limits stated. Field 20 References — entry [5] added. Research-basis review date moved. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
```

---
---

