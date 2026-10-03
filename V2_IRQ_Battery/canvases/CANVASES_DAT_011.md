# CANVAS: IRQ-DAT-011

## 1. IRQ ID & Title
**IRQ-DAT-011: Undetected Statistical, Semantic and Source Drift in Model Inputs**

Register question: "Are statistical, semantic and source drift in model inputs — including unannounced upstream reference-data changes — detected against defined baselines before performance degrades?"

## 2. Business Activities Affected
- **Credit and affordability decisioning:** Input feature distributions (income patterns, product mix, macroeconomic context) drift over time; undetected drift silently erodes model calibration.
- **AML transaction monitoring:** Reference typology and transaction-pattern data can shift as customer behaviour and fraud tactics evolve; source drift from an upstream data provider (schema or semantic change) can silently corrupt inputs.
- **Insurance pricing:** Underlying risk-factor data (claims patterns, external risk feeds) drifts with market conditions; undetected drift misprices risk.

## 3. AI Behaviour(s)
- Continues to score/generate against whatever inputs it receives, with no inherent awareness that the statistical distribution, semantic meaning, or upstream source of those inputs has shifted from its training baseline.
- Produces outputs with the same apparent confidence regardless of whether current inputs resemble the distribution it was validated against.
- Silently absorbs upstream schema or semantic changes (e.g. a reference field's units or definition changing) as if they were valid new data.

## 4. Failure Mode
> Statistical, semantic or source drift in model inputs — including unannounced upstream reference-data changes — occurs without detection against a defined baseline, so the model continues operating on inputs it was not validated against, and performance degradation is not caught before it accumulates into material customer or financial impact.

## 5. Potential Consequences
- **Customer:** Gradually degrading decision quality (credit, pricing, AML detection) affecting a growing share of interactions as drift accumulates, undetected.
- **Institution:** Model risk materialises as a slow leak rather than a single failure event, making root-cause attribution difficult once discovered; potential capital/loss impact if pricing or risk models are affected.
- **Regulator:** PRA SS1/23 ongoing-monitoring principle and EU AI Act Art. 15 robustness/accuracy-maintenance obligations are not met without drift detection.

## 6. Failure Chain
```
Upstream data source undergoes a statistical, semantic or schema
change (e.g. a reference field's definition or units silently change,
or the customer/macro population shifts) without notification
  ↓ (IRQ-DAT-011 — THIS IRQ: no baseline-referenced drift detection
     catches the change)
Model continues scoring against inputs it was not validated against;
outputs retain the same apparent confidence
  ↓ (IRQ-MOD-010: distribution-shift-specific validation, if it exists,
     is not triggered because the drift was never flagged)
Performance degrades gradually; no single event triggers investigation
  ↓ (IRQ-RES-006: alerting design, if aggregate-only, fails to surface
     gradual decay)
Accumulated degradation reaches material customer or financial impact
before discovery — typically via outcome-pattern audit, not real-time
monitoring
  ↓
Regulatory finding of inadequate ongoing monitoring; remediation and
retraining cost; potential retrospective decision review

Control Breakpoints:
  • IRQ-DAT-011: baseline-referenced statistical/semantic/source drift detection
  • IRQ-MOD-010: shift-specific revalidation triggers keyed to drift signals
  • IRQ-RES-006: alerting designed to surface gradual, not only hard, degradation
```

## 7. Why a Domain Expert May Miss It
- Model risk SMEs are trained to validate at build/refresh points; the assumption that a model, once validated, remains valid until the next scheduled review is the default mental model, not continuous drift awareness.
- Upstream data changes (a vendor updating a field's definition, a reference feed's units changing) are IT/data-engineering events that rarely trigger a model-risk review unless an explicit cross-team notification process exists.
- Aggregate performance dashboards can mask gradual drift for a long time, especially where the drift affects a growing but still-minority share of inputs (echoes the aggregate-metric-masking pattern in IRQ-DAT-005).
- "Statistical drift," "semantic drift" and "source drift" are three genuinely distinct phenomena requiring different detection methods; a single generic "monitoring dashboard" often addresses only one (usually statistical).

## 8. Assurance Objective
**AO-DAT-011:** Statistical, semantic and source drift in model inputs shall be detected against defined baselines, including unannounced upstream reference-data changes, before performance degradation accumulates to a material level.

## 9. Expected Controls (Traced)
- **Statistical drift detection against a defined baseline** — [Rabanser et al., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", arXiv:1810.11953] — two-sample-test or equivalent statistical monitoring of input feature distributions against the training/validation baseline.
- **Semantic drift and concept-drift detection** — [Gama et al., 2014, "A Survey on Concept Drift Adaptation", ACM CSUR, https://doi.org/10.1145/2523813] — canonical concept-drift detection methods applied to catch meaning-level, not just statistical, shifts in inputs.
- **Upstream source-change notification and schema monitoring** — [Emerging Practice — general data-engineering practice, no single published FS standard; grounded in ISO/IEC 5338:2023 lifecycle monitoring] — contractual or technical mechanisms detect and flag upstream schema/definition changes before they silently enter the pipeline.
- **Threshold-driven alerting with defined response playbooks** — [linked IRQ-RES-005/-006; PRA SS1/23 ongoing monitoring principle] — drift signals trigger a defined governance response, not a passive dashboard.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "we monitor model inputs" with no baseline/methodology detail — **L1**.
- Drift-detection methodology document specifying statistical, semantic and source-drift coverage separately — **L2**.
- Code/config inspection confirming drift-detection logic actually runs against a defined baseline in the production pipeline — **L3**.
- Staging test results: a synthetic drift event (statistical shift, semantic redefinition, upstream schema change) injected; detection latency and accuracy measured — **L3**.
- Independent audit of the drift-detection and escalation mechanism, including a sample historical drift event traced from occurrence to remediation — **L4**.
- Production monitoring data: drift-alert history over a defined period, with time-to-detection and time-to-remediation recorded — **L5**.

## 11. Independent Test
> In a non-production environment, inject three classes of synthetic drift into a representative input stream: (a) a statistical distribution shift in a key feature (e.g. gradual population-mix change), (b) a semantic/concept redefinition (e.g. a categorical field's meaning silently changes without a schema-level signal), and (c) an upstream source change (e.g. a reference feed's units or scale change). Measure detection latency (queries/time-to-alert) and false-negative rate for each drift class against the firm's documented baseline. Methodology follows Rabanser et al. (2019) two-sample-test shift detection and Gama et al. (2014) concept-drift taxonomy; source-change detection is tested against whatever contractual/technical notification mechanism exists. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (statistical and concept-drift detection methods are published, well-established and used by multiple independent groups; source-change/schema-drift detection specifically is less standardised, keeping the combined test just short of ★4).

## 12. Pass Indicators
- All three drift classes (statistical, semantic, source) are detected within the firm's documented time-to-alert SLA in staging testing.
- Drift alerts trigger a defined governance response (documented playbook), not a passive dashboard entry.
- A sample historical drift event, if any occurred, shows time-to-detection and time-to-remediation within acceptable bounds.
- Upstream data providers are contractually or technically obligated to notify schema/definition changes.

## 13. Fail Indicators
- One or more drift classes (commonly semantic or source drift) are undetected or detected only after material lag in staging testing.
- Monitoring exists for statistical drift only, with no coverage of semantic or source drift.
- No defined response playbook exists for a drift alert; alerts are logged but not acted upon.
- A historical drift event, when traced, shows a long undetected period before discovery via complaint or outcome-audit rather than monitoring.

## 14. Reporting Language
**Pass:** "Synthetic drift injection testing across statistical, semantic and source-drift classes found detection within the firm's documented SLA in all three cases, with defined governance responses triggered on alert. This is ★3 methodology, well-established for statistical and concept drift, less standardised for source-change detection specifically."

**Fail:** "Synthetic drift injection testing found that semantic and source-drift classes were undetected by current monitoring, which covers statistical drift only. A historical drift event traced during this review showed a [x]-week undetected period before discovery via [complaint/audit], during which the model operated on inputs materially different from its validation baseline. This represents a material ongoing-monitoring gap requiring remediation."

**Partial:** "Statistical and semantic drift detection are effective, but no mechanism exists to detect unannounced upstream source/schema changes, which historically account for [x]% of material drift events. Extend source-change monitoring before the assurance objective is met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (accumulated performance degradation affecting a growing share of decisions
              before discovery; regulatory ongoing-monitoring exposure)
  Likelihood: 2 (plausible where source-drift coverage specifically is weak, a common gap
                 even in otherwise mature monitoring estates)
  Detectability: 2 (once monitoring covers all three drift classes, detection occurs within
                    a defined SLA; the residual concern is coverage gaps, not detection speed)
  Recoverability: 2 (remediable via recalibration/retraining once drift is identified)
  Novelty: 2 (drift monitoring is a recognised model-risk discipline; the AI-specific nuance
              is the three-way statistical/semantic/source split, often under-covered)

If controls are absent or degraded:
  Severity: 3 (sustained degraded decisioning across a growing input population, undetected
              for an extended period)
  Likelihood: 3 (semantic and source-drift coverage gaps are a common default even where
                 statistical monitoring is mature)
  Detectability: 4 (aggregate performance metrics mask gradual drift; without dedicated
                    monitoring, discovery relies on complaint or periodic audit)
  Recoverability: 2 (remediable via recalibration/retraining once identified)
  Novelty: 2
Residual risk: material and cumulative; the primary danger is partial coverage creating a
false sense of complete monitoring.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Accumulated performance degradation across a growing share of decisions before discovery; ongoing-monitoring regulatory exposure. |
| **Likelihood** | 2 | Plausible where source-drift coverage specifically is weak, a common gap even in mature monitoring estates. |
| **Detectability** | 3 | Aggregate metrics mask gradual drift; detection requires dedicated, class-specific monitoring rather than a generic dashboard. |
| **Recoverability** | 2 | Remediable via recalibration/retraining once drift is identified. |
| **Novelty** | 2 | Drift monitoring is a familiar model-risk discipline; the AI-specific nuance is the statistical/semantic/source three-way split, frequently under-covered. |

## 17. Regulatory Basis
> [PRA SS1/23, May 2023, Principle 4 (independent model validation, including ongoing monitoring)] ongoing monitoring principle requires models to be monitored for continued fitness for purpose, extending to input drift. [EU AI Act, Regulation (EU) 2024/1689, Art. 15(1) and Art. 15(4)] requires accuracy, robustness and cybersecurity to be maintained throughout the lifecycle, implying drift detection as an ongoing obligation. (verified 29 Jul 2026)

## 18. Research Basis
> [Gama, J., et al., 2014, "A Survey on Concept Drift Adaptation", ACM Computing Surveys, https://doi.org/10.1145/2523813] — canonical drift taxonomy and detection methods, the structural basis for distinguishing statistical from semantic/concept drift. [Rabanser, S., Günnemann, S., Lipton, Z., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", arXiv:1810.11953] — practical, implementable two-sample-test shift-detection methodology. [Chen, Y., et al., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009] — empirical evidence that even a fixed API endpoint drifts substantially over months, illustrating that source drift is not a hypothetical concern.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-005 (A.1: representativeness at build — the point-in-time predecessor of ongoing drift)
  - IRQ-DAT-012 (A.5: retrieval/embedding/document drift — the retrieval-layer counterpart)
  - IRQ-MOD-010 (B.5: shift-type-specific validation and revalidation triggers)
  - IRQ-RES-005/-006 (G.3: monitoring/alerting capability and gradual-decay detection design)
```

## 20. References
```
[1] Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., Bouchachia, A., 2014. "A Survey on
    Concept Drift Adaptation." ACM Computing Surveys 46(4). https://doi.org/10.1145/2523813
[2] Rabanser, S., Günnemann, S., Lipton, Z., 2019. "Failing Loudly: An Empirical Study of
    Methods for Detecting Dataset Shift." arXiv:1810.11953.
[3] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over Time?"
    arXiv:2307.09009.
[4] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 15.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.5 (Data domain, Data Drift)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): "Validated once, valid until next review" is the default MRM
  mental model; continuous drift awareness, especially semantic/source drift, is not.
✓ Test 2 (Plausible Harm): Grounded in Gama et al. (2014) concept-drift taxonomy and
  Chen et al. (2023) empirical evidence of real-world source drift.
✓ Test 3 (Testable): Synthetic drift injection across three classes is executable in
  non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates model refresh/revalidation triggers and monitoring-design
  adequacy.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

