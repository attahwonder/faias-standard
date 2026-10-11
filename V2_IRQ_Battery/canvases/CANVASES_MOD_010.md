# CANVAS: IRQ-MOD-010

## 1. IRQ ID & Title
**IRQ-MOD-010: Unassessed Robustness Across Population, Covariate, Concept, Label, Temporal and Policy Shift**

Register question: "Has robustness been assessed against each relevant shift type — population, covariate, concept, label, temporal and policy shift — with revalidation triggers defined per type?"

## 2. Business Activities Affected
- **Credit scoring/underwriting:** The customer population, macroeconomic covariates, and the true relationship between features and default (concept) all shift over an economic cycle; a model validated pre-shift can silently misperform post-shift.
- **AML transaction monitoring:** Criminal typologies (concept shift) and product mixes (population/covariate shift) evolve; a model tuned on historical typologies degrades against novel ones.
- **Claims and pricing:** Regulatory changes to permissible pricing factors or claims handling rules (policy shift) can invalidate a model's learned associations even where the underlying population is stable.

## 3. AI Behaviour(s)
- Produces output based on patterns learned from historical training/validation data, with no inherent mechanism to detect that the world has since changed.
- Performance can remain stable on a stale internal test set while diverging materially from true production performance.
- Different shift types (who the customers are, how features relate to inputs, what the true label relationship is, when data was collected, what rules currently apply) each degrade the model through distinct mechanisms requiring distinct tests.

## 4. Failure Mode
> The model's robustness has not been separately assessed against each of the distinct shift types — population, covariate, concept, label, temporal and policy — so an undetected shift of any one type can degrade production performance without triggering revalidation, because no shift-type-specific trigger was ever defined.

## 5. Potential Consequences
- **Customer:** Wrong credit, AML or claims outcomes as the model's learned associations diverge from current reality, disproportionately affecting whichever segment the specific shift type has moved.
- **Institution:** A single generic "monitor accuracy" control fails to catch shift types that manifest as changed input distributions or changed rules rather than changed accuracy on a stale test set; SS1/23 ongoing-validation gap.
- **Regulator/market:** Findings that model risk management did not evidence robustness across the shift taxonomy the firm's own business is exposed to (economic cycle, evolving typologies, regulatory change).

## 6. Failure Chain
```
Model validated on a historical dataset representing one point in time
  ↓ (IRQ-DAT-011: input drift detection may exist but does not map to the full
     shift-type taxonomy)
One or more of population/covariate/concept/label/temporal/policy shift occurs in
the real world, unaccompanied by a corresponding shift-type-specific test
  ↓ (IRQ-MOD-010 — THIS IRQ: no shift-type-specific robustness assessment or revalidation
     trigger was ever defined)
Model continues operating on outdated learned associations
  ↓ (IRQ-RES-005: monitoring exists but is not calibrated to detect this specific shift type)
Performance degrades in a way invisible to generic accuracy monitoring
(e.g. concept shift changes what "high risk" means without changing input distributions)
  ↓ (IRQ-GOV-008: governance receives no escalation because no threshold was breached)
Systematic wrong decisions accumulate across the affected segment/period
  ↓
Discovery via external audit, adverse outcome pattern, or regulatory finding →
retrospective remediation across the undetected exposure period

Control Breakpoints:
  • IRQ-DAT-011: input-side drift detection (statistical/semantic/source) feeding this
    assessment
  • IRQ-MOD-010: shift-type-specific robustness testing with defined revalidation triggers
    per type
  • IRQ-RES-005/006: monitoring thresholds calibrated to each shift type, including gradual
    decay
  • IRQ-GOV-008: governance escalation triggered by shift-specific signals, not generic
    accuracy alone
```

## 7. Why a Domain Expert May Miss It
- Traditional model risk practice often treats "drift monitoring" as a single undifferentiated control; the idea that population, covariate, concept, label, temporal and policy shift are six distinct mechanisms each requiring its own test is a level of taxonomic precision most SMEs have not been trained in.
- Concept and label shift are particularly counter-intuitive: the input distribution can look completely stable while the true relationship between inputs and outcomes has changed (e.g. what behaviour indicates fraud risk shifts even though customer demographics do not) — a generic input-monitoring control will not catch this.
- Policy shift (a regulatory rule change invalidating a previously acceptable feature or threshold) is often treated as a compliance/legal matter disconnected from model revalidation, when it directly invalidates model behaviour.
- SMEs may assume a single validation exercise, once passed, remains valid indefinitely absent an obvious trigger (a major model change); shift can occur continuously and silently without any change to the model itself.

## 8. Assurance Objective
**AO-MOD-010:** Model robustness shall be separately assessed against population, covariate, concept, label, temporal and policy shift, with defined revalidation triggers specific to each shift type, so that degradation from any one shift mechanism is detectable and actionable.

## 9. Expected Controls (Traced)
- **Shift-type-specific test design** — [Koh et al., 2021, "WILDS: A Benchmark of in-the-Wild Distribution Shifts", arXiv:2012.07421; Gama et al., 2014, "A Survey on Concept Drift Adaptation", ACM CSUR] — dedicated test construction and metrics for each of the six shift types, not a single generic drift dashboard.
- **Two-sample statistical shift detection for input-side shift** — [Rabanser et al., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", arXiv:1810.11953] — implementable statistical methods for population/covariate shift detection at the input level.
- **Concept/label shift assessment via outcome monitoring** — [D'Amour et al., 2020/22, "Underspecification...", arXiv:2011.03395] — periodic re-measurement of the true input-output relationship against fresh ground truth, since concept/label shift is invisible to input-only monitoring.
- **Policy-shift mapping to model revalidation triggers** — [linked IRQ-GOV-011; PRA SS1/23 ongoing-validation principle] — regulatory or internal policy changes affecting permissible features, thresholds or rules are mapped to a mandatory model revalidation trigger.
- **Defined revalidation cadence and triggers per shift type** — [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), ongoing monitoring principle; linked IRQ-RES-005] — each shift type has a documented detection method, threshold, and revalidation response, not a single blanket "annual review."

## 10. Expected Evidence (Tagged L1–L5)
- Vendor/internal claim that "the model is monitored for drift" — **L1** (assertion only; does not specify shift-type coverage).
- Design documentation mapping each of the six shift types to a specific detection method and revalidation trigger — **L2**.
- Staging test results demonstrating each shift-type detection method functions as intended (e.g. injected covariate shift is detected; injected concept shift via re-labelled outcomes is detected) — **L3**.
- Independent validation report assessing coverage and adequacy of shift-type-specific testing — **L4**.
- Production monitoring data and revalidation history showing at least one shift type detected and acted upon in practice — **L5**.

## 11. Independent Test
> In a non-production environment, construct synthetic shift scenarios for each of the six shift types applied to a representative dataset for the deployed use case: (a) population shift — resample to change subgroup proportions; (b) covariate shift — alter the distribution of input features while holding the true relationship constant; (c) concept shift — alter the true input-output relationship (re-label a subset consistent with a changed real-world relationship) while holding inputs constant; (d) label shift — alter the base rate of outcomes; (e) temporal shift — use data from a materially different time period; (f) policy shift — simulate a rule change removing or altering a previously-used feature/threshold. For each scenario, measure whether the firm's existing monitoring/detection mechanism flags the shift and whether a revalidation trigger fires. Methodology per Koh et al. (2021, WILDS) and Rabanser et al. (2019). Executed entirely on synthetic/historical data in staging. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, peer-reviewed shift-detection methods exist with reasonable consensus for statistical shift types; concept/label/policy shift testing is more bespoke and professional-judgement-led, pulling the overall rating toward the middle of the ★3 band rather than ★4).

## 12. Pass Indicators
- Detection mechanisms exist and function for all six shift types in the staging test, each with a defined revalidation trigger.
- At least one shift type has been detected and acted upon in actual production history (evidencing the control works in practice, not only in theory).
- Policy-shift mapping demonstrably links regulatory/internal rule changes to a mandatory revalidation step.
- Governance escalation is calibrated to shift-specific signals, not solely generic accuracy metrics.

## 13. Fail Indicators
- Monitoring exists only for input-side statistical shift (population/covariate); concept, label and policy shift have no corresponding detection mechanism.
- No shift type has ever triggered a documented revalidation in production history, despite known economic-cycle or typology change over the review period.
- Policy/regulatory changes affecting model-relevant rules occur with no corresponding revalidation trigger or record.
- "Drift monitoring" is described only in general terms with no shift-type-specific design evidence.

## 14. Reporting Language
**Pass:** "Robustness testing and monitoring cover all six shift types — population, covariate, concept, label, temporal and policy — each with a defined detection method and revalidation trigger; production history evidences at least one shift type being detected and acted upon. Conclusions rest on ★3 methodology — credible but partially bespoke for concept/label/policy shift — and should be periodically refreshed."

**Fail:** "Monitoring is limited to input-side statistical drift; concept, label and policy shift have no corresponding detection mechanism or revalidation trigger, despite [n] known typology changes / regulatory changes over the review period with no corresponding revalidation record. This represents a material gap in ongoing model validation; a shift in the true input-output relationship or in applicable rules could degrade the model's performance with no mechanism to detect or respond to it."

**Partial:** "Detection mechanisms exist for population, covariate and temporal shift but not for concept, label or policy shift. The assurance objective is not fully met; interim mitigation should include a manual periodic re-assessment of concept/label/policy shift pending automated detection design."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (systematic degraded decisions across a segment or period affected by an
              undetected shift type; regulatory notice risk)
  Likelihood: 2 (shift-type-specific detection and revalidation triggers should catch
              material shift before it becomes systemic)
  Detectability: 2 (dedicated shift-type monitoring surfaces degradation within the defined
              cadence, typically weeks)
  Recoverability: 2 (revalidation and model update are a defined, resourced process once
              triggered)
  Novelty: 3 (the six-way shift taxonomy, particularly concept/label/policy shift as
              distinct from input drift, is a level of precision outside typical model risk
              practice)

Interpretation: acceptable residual risk with full shift-type coverage and calibrated
revalidation triggers; highest concern is Novelty for the less-intuitive shift types
(concept, label, policy).

If controls are absent or degraded:
  Severity: 4 (systemic, undetected performance degradation across an entire economic cycle
              or typology-change period, invisible to generic accuracy monitoring)
  Likelihood: 3 (economic cycles, evolving financial-crime typologies and regulatory change
              are routine, not exceptional, occurrences over a model's operational life)
  Detectability: 4 (concept/label shift in particular can occur with stable input
              distributions, defeating input-only monitoring entirely)
  Recoverability: 3 (requires retrospective identification of the shift point and affected
              population, then full model revalidation)
  Novelty: 3
Residual risk: Critical. Deployment gate should require at minimum concept and policy shift
coverage, not only input-side drift monitoring.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Undetected shift can systematically degrade decisions across an affected segment or period; regulatory notice risk under SS1/23 ongoing-validation expectations. |
| **Likelihood** | 3 | Economic cycles, evolving financial-crime typologies and regulatory change are routine over a model's operational life, not rare events. |
| **Detectability** | 3 | Input-only monitoring cannot detect concept or label shift, which can occur with a stable input distribution — a structural detection gap absent dedicated tests. |
| **Recoverability** | 2 | Once a shift is identified, revalidation and model update are a defined and resourced (if sometimes lengthy) process. |
| **Novelty** | 3 | The six-way shift taxonomy, and particularly concept/label/policy shift's invisibility to input-monitoring, is a level of precision beyond typical model risk practice. |

## 17. Regulatory Basis
> [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024, Principle 4 (independent model validation, including ongoing monitoring)] — the primary anchor; requires monitoring proportionate to the model's risk and use, which this IRQ interprets to require shift-type-specific coverage rather than a single generic metric. [Bank of England FPC, "Financial Stability in Focus: Artificial intelligence in the financial system", Apr 2025] — systemic concern about correlated model behaviour under shifting conditions supports the case for robust shift-type monitoring at firm level. No regulation names the six-way shift taxonomy explicitly; this IRQ operationalises SS1/23 for AI-specific shift mechanisms. (verified 29 Jul 2026)

## 18. Research Basis
> [Koh, P.W., et al., 2021, "WILDS: A Benchmark of in-the-Wild Distribution Shifts", arXiv:2012.07421] — real-world shift benchmarks demonstrating large, shift-type-specific performance drops. [D'Amour, A., et al., 2020/22, "Underspecification Presents Challenges for Credibility in Modern Machine Learning", arXiv:2011.03395] — evidences that identical held-out performance can mask divergent deployment behaviour under shift. [Gama, J., et al., 2014, "A Survey on Concept Drift Adaptation", ACM Computing Surveys] — canonical taxonomy and detection methods for concept drift specifically. [Rabanser, S., Günnemann, S., Lipton, Z., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", arXiv:1810.11953] — practical, implementable two-sample-test shift-detection methodology. [Chen, L., Zaharia, M., Zou, J., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009; Harvard Data Science Review 6(2), 2024] — temporal shift evidenced directly in a deployed LLM API.
>
> **[FAIAS Incident Register, row 5, "Zillow Offers collapse", 2021]**, citing [Zillow Group, Inc., 2021, "Zillow Group Reports Third-Quarter 2021 Financial Results & Shares Plan to Wind Down Zillow Offers Operations", Form 8-K Exhibit 99.1, United States Securities and Exchange Commission, 2 November 2021; and "Q3 2021 Shareholder Letter", Form 8-K Exhibit 99.3, 2 November 2021] — a first-party disclosure that the company's home-price forecasting error exceeded what it had modelled as possible, at a scale that ended the business line: the company recorded "a write-down of inventory of approximately $304 million within the Homes segment", expected "an additional $240 million to $265 million of losses to be recognized in Q4", announced "a reduction of Zillow's workforce by approximately 25%", and quoted its chief executive as saying that "the unpredictability in forecasting home prices far exceeds what we anticipated". It evidences the consequence this question guards against — a forecasting model operating under conditions its expected error was not estimated for, at portfolio scale — and it is the only first-party, quantified instance of that consequence this field carries, the remaining citations being research literature. It does **not** evidence the control gap: the filing names no shift type, says nothing about monitoring, revalidation triggers or detection, and does not attribute the outcome to an undetected population, covariate, concept, label, temporal or policy shift.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-DAT-011 (A.5: input-side statistical/semantic/source drift — the data-layer feed for
    this Model-domain robustness assessment)
  - IRQ-MOD-001 (B.1: capability envelope — overlaps with but is distinct from shift
    robustness; envelope is about task type, shift is about population/rule change over time)
  - IRQ-RES-005 / IRQ-RES-006 (G.3: monitoring and alerting infrastructure implementing
    shift-type-specific thresholds)
  - IRQ-GOV-008 (I.3: governance escalation on shift signals)
  - IRQ-TPR-004 (F.2: vendor-side model change as a distinct source of shift)
```

## 20. References
```
[1] Koh, P.W., Sagawa, S., Marklund, H., et al., 2021. "WILDS: A Benchmark of in-the-Wild
    Distribution Shifts." arXiv:2012.07421.
[2] D'Amour, A., Heller, K., Moldovan, D., et al., 2020 (rev. 2022). "Underspecification
    Presents Challenges for Credibility in Modern Machine Learning." arXiv:2011.03395.
[3] Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., Bouchachia, A., 2014. "A Survey on
    Concept Drift Adaptation." ACM Computing Surveys, 46(4).
[4] Rabanser, S., Günnemann, S., Lipton, Z., 2019. "Failing Loudly: An Empirical Study of
    Methods for Detecting Dataset Shift." arXiv:1810.11953.
[5] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over Time?"
    arXiv:2307.09009. Published in Harvard Data Science Review 6(2), 12 March 2024,
    https://doi.org/10.1162/99608f92.5317da47.
[6] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[7] Bank of England, Financial Policy Committee, 2025. "Financial Stability in Focus:
    Artificial intelligence in the financial system." April 2025.
[8] Zillow Group, Inc., 2021. "Zillow Group Reports Third-Quarter 2021 Financial
    Results & Shares Plan to Wind Down Zillow Offers Operations." Form 8-K,
    Exhibit 99.1; and "Q3 2021 Shareholder Letter", Form 8-K, Exhibit 99.3.
    United States Securities and Exchange Commission, 2 November 2021.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.5 (Model domain, Distribution Shift & Evaluation Integrity)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): The six-way shift taxonomy, and particularly that concept/label
  shift can occur with a stable input distribution, is a precision level outside typical
  model risk practice; "drift monitoring" is usually treated as one undifferentiated control.
✓ Test 2 (Plausible Harm): Grounded in distribution-shift benchmarking (Koh et al.),
  underspecification research (D'Amour et al.), concept-drift taxonomy (Gama et al.) and
  practical shift-detection methods (Rabanser et al.).
✓ Test 3 (Testable): Fully testable in staging via constructed shift scenarios for each of
  the six types; no production data required.
✓ Test 4 (Decision-Relevant): Outcome gates whether monitoring coverage is adequate across
  the full shift taxonomy and sets shift-type-specific revalidation triggers.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-14): §20 reference [7] and the §17 citation — erratum: the BoE FPC title corrected from "Artificial intelligence and financial stability" (§20) and "AI and financial stability" (§17) to "Artificial intelligence in the financial system" (the title the v1.1.1 closure verified as the instrument's). No change to controls, test, ★ or risk profile.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form (row 5, Zillow Offers collapse), bounded to the consequence the question guards against and stating expressly that the filing evidences no shift type and no absent revalidation trigger. Field 20 — entry [8] added for the filing, naming its Exhibits 99.1 and 99.3. Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Field 9 Expected Controls — the title of Rabanser et al. (arXiv:1810.11953) corrected to Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift (six words had been dropped). No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Fields 18 and 20 — the Chen, Zaharia and Zou citation (arXiv:2307.09009) now also gives its publication in Harvard Data Science Review 6(2), 2024. Research-basis review date moved. No change to the ★ rating or the risk profile.
```

---
---

