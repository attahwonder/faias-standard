# CANVAS: IRQ-CON-007

## 1. IRQ ID & Title
**IRQ-CON-007: Unmanaged Performative Feedback Loops Entrenching Unfair Outcomes**

Register question: "Can the system's own decisions reshape the data it later learns from — feedback loops or performative effects that entrench or amplify unfair patterns?"

## 2. Business Activities Affected
- **Credit decisioning:** Declined applicants generate no repayment outcome data by definition (never observed), so retraining on observed outcomes only reinforces the original decision boundary, entrenching whatever bias existed at the point of first deployment.
- **Fraud/AML alerting:** Customers or transaction patterns the model does not flag are never investigated, so "confirmed" ground truth used for retraining is itself shaped by the model's own prior alerting decisions, creating a self-confirming loop.
- **Collections and risk segmentation:** Segment-level treatment decisions (e.g. who receives forbearance offers) shape subsequent repayment behaviour and thus the "risk" label used to retrain the segmentation model, entrenching the original segmentation.

## 3. AI Behaviour(s)
- Makes a decision (decline, flag, segment, treat) that determines whether and how a customer's subsequent behaviour is even observed by the firm.
- Is retrained or recalibrated periodically using outcome data drawn from the population the model itself selected or shaped, rather than from a representative sample of the full population including counterfactual (not-selected) cases.
- Can amplify an initial disparity over successive retraining cycles even without any single retraining step introducing new bias, purely through the compounding structure of the feedback loop (a performative/self-fulfilling-prophecy effect).

## 4. Failure Mode
> The system's decisions determine which subsequent data becomes observable for retraining, creating a feedback loop in which the model's own prior decisions shape the "ground truth" used to validate or retrain it, entrenching or amplifying an initial disparity or error over successive cycles without this being visible as a retraining-integrity problem.

## 5. Potential Consequences
- **Customer:** A customer or segment initially (rightly or wrongly) disadvantaged is never given the opportunity to generate contrary evidence, because the model's own decision prevented the outcome data from ever being observed — a self-perpetuating disadvantage.
- **Institution:** Fair-lending/Consumer Duty exposure compounds over time as the entrenchment deepens, and remediation becomes progressively harder because the "ground truth" data itself is contaminated by the original decision.
- **Regulator/Market:** A regulatory finding that model retraining practices have been unknowingly amplifying, rather than correcting, an unfair pattern over multiple cycles — a more serious governance finding than a single point-in-time miscalibration.

## 6. Failure Chain
```
Model makes an initial decision (decline/flag/segment) that determines
which subsequent outcomes are observed
  ↓ (IRQ-CON-001/IRQ-CON-002: initial disparity or proxy effect,
     if present, is the seed of the loop)
Retraining/recalibration uses outcome data drawn only from the
model-selected population, not a representative sample including
counterfactual cases
  ↓ (IRQ-CON-007 — THIS IRQ: no feedback-loop mapping or correction
     mechanism exists; retraining pipeline treats observed outcomes
     as if they were a representative ground truth)
Model is retrained to be more confident in its original decision
boundary, because the only evidence available confirms it
  ↓ (IRQ-MOD-012: recursive collapse risk compounds if model outputs
     themselves later re-enter training data)
Disparity entrenches and amplifies over successive retraining cycles;
by the time it is investigated, ground-truth data is itself
contaminated, making remediation materially harder

Control Breakpoints:
  • IRQ-CON-007: feedback-loop pathways explicitly mapped; retraining
    incorporates counterfactual/exploration data, not only
    model-selected outcomes
  • IRQ-CON-001: initial disparity testing reduces the severity of the
    seed the loop amplifies
  • IRQ-MOD-012: output-to-training feedback paths (recursive
    collapse) identified and filtered separately
```

## 7. Why a Domain Expert May Miss It
- Model risk management conventionally validates a model against "the data available", without asking the more subtle question of whether the available data is itself an artefact of the model's own prior decisions — this is a distinctly AI/statistics-specific insight (selection bias induced by the decision system itself), not a traditional model validation check.
- Retraining/recalibration is often viewed procedurally as inherently corrective ("we retrain regularly to keep the model current"), when in a feedback-loop context regular retraining without counterfactual data can be actively harmful, entrenching rather than correcting bias — this is counter-intuitive to a governance process built around "retraining = improvement".
- The effect compounds gradually across multiple retraining cycles, meaning no single retraining event looks anomalous; a domain expert reviewing one retraining cycle in isolation will not see the cumulative entrenchment.
- Credit risk and AML SMEs are trained to distinguish "reject inference" as a known statistical challenge in credit modelling, but may not extend the same underlying insight (the observed sample is shaped by the decision system) to newer AI-driven fraud/AML or segmentation contexts where the analogous issue is less established as a named, checked-for problem.

## 8. Assurance Objective
**AO-CON-007:** The firm shall map feedback-loop pathways by which the AI system's own decisions shape subsequently observed data, and shall incorporate counterfactual or exploration data into retraining/recalibration to prevent entrenchment or amplification of unfair patterns.

## 9. Expected Controls (Traced)
- **Feedback-loop pathway mapping** — [research-grounded: performative prediction literature] — Emerging Practice; the firm explicitly identifies which decisions determine subsequently observed outcome data, as a named step in model documentation, not left implicit.
- **Reject inference / counterfactual data techniques** — [established credit-risk-modelling practice, e.g. reweighting or augmentation for declined applicants; see Anderson, R., 2007, "The Credit Scoring Toolkit: Theory and Practice for Retail Credit Risk Management and Decision Automation," Oxford University Press, ISBN 9780199226405] — [UNVERIFIED — no direct FCA/PRA regulatory citation mandating reject-inference technique beyond general MRM expectations was located] (verified 29 Jul 2026) — extended here explicitly to AI-driven decisioning, and to non-credit contexts (fraud/AML, segmentation) where the analogous technique is less standardised.
- **Periodic entrenchment/drift-of-disparity testing across retraining cycles** — [linked IRQ-CON-001, extended longitudinally] — Emerging Practice; testing whether subgroup disparity is widening across successive retraining cycles, not only tested once at each point in time.
- **Model validation governance sign-off explicitly addressing feedback-loop risk** — [linked IRQ-GOV-007] — retraining approval requires demonstration that counterfactual/exploration data considerations were addressed, not solely that the retrained model performs well on the (potentially contaminated) available data.
- **Exploration/randomised holdout in decisioning where feasible** — Emerging Practice; a small, governed proportion of borderline cases decisioned via a randomised or exploratory approach specifically to generate uncontaminated counterfactual outcome data — genuinely novel practice for most FS firms, with limited precedent.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "we retrain regularly" with no feedback-loop or counterfactual-data analysis — **L1**.
- Model documentation explicitly mapping which decisions shape subsequently observed outcome data, and what (if any) counterfactual data strategy is used — **L2**.
- Non-production analysis: simulated or historical multi-cycle retraining test showing whether disparity widens, narrows or is stable across cycles when counterfactual data is included vs excluded — **L3**.
- Independent model risk or internal audit review confirming feedback-loop risk was explicitly assessed as part of retraining governance sign-off — **L4**.
- Production longitudinal monitoring: subgroup disparity metrics (per IRQ-CON-001) tracked across successive retraining cycles, with any widening trend investigated — **L5**.

## 11. Independent Test
> Using historical or synthetic multi-cycle data, simulate the retraining process twice: once using only outcomes for the model-selected/accepted population (as the current pipeline does), and once incorporating a defined counterfactual/reject-inference technique. Compare subgroup disparity metrics (per IRQ-CON-001 methodology) across simulated successive cycles under each approach, to quantify whether the current pipeline design entrenches disparity relative to a counterfactual-aware alternative. Non-production environment; historical or synthetic data only. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (reject inference is an established technique in credit-risk modelling specifically — ★3 for that component; extending the same logic to a general "performative feedback loop" test across multiple retraining cycles, and to non-credit contexts, is research-grounded but bespoke, with no agreed FS benchmark — blended rating reflects the weaker, more novel component).

## 12. Pass Indicators
- Feedback-loop pathways are explicitly mapped in model documentation, naming which decisions shape subsequently observed data.
- A counterfactual/reject-inference or equivalent technique is in active use for retraining, not merely considered and rejected without documented rationale.
- Multi-cycle simulation/longitudinal monitoring shows subgroup disparity is stable or narrowing across retraining cycles, not widening.
- Retraining governance sign-off explicitly addresses feedback-loop risk as a named consideration.

## 13. Fail Indicators
- No feedback-loop mapping exists; retraining treats observed outcomes as representative ground truth without qualification.
- No counterfactual/reject-inference technique is used, with no documented rationale for its absence.
- Longitudinal monitoring (where it exists) shows subgroup disparity widening across successive retraining cycles, indicating active entrenchment.
- Retraining governance sign-off does not address feedback-loop risk as a distinct consideration from general model performance.

## 14. Reporting Language
**Pass:** "Feedback-loop pathways are explicitly mapped, counterfactual data techniques are in active use for retraining, and longitudinal monitoring shows subgroup disparity is stable across retraining cycles. Conclusions rest on a blended methodology — ★3 for the credit-risk-established reject-inference component, ★2 for the broader multi-cycle feedback-loop testing — and should be read accordingly."

**Fail:** "No feedback-loop mapping or counterfactual data technique exists; retraining treats model-selected outcome data as representative without qualification. This is a direct and serious conduct risk: any initial disparity present in the system is likely being entrenched, not corrected, by the firm's own retraining practice, and the longer this continues undetected the harder remediation becomes."

**Partial:** "Reject inference is applied for the primary credit decisioning model but the equivalent feedback-loop consideration has not been extended to the fraud/AML alerting model, where the same self-confirming dynamic is structurally present. Remediation should extend the counterfactual-data approach to this model before comprehensive assurance can be given."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (gradual, generally slow-moving entrenchment risk, actively countered by counterfactual technique)
  Likelihood: 2 (foreseeable structurally in any decision-then-retrain pipeline; mitigated by active counterfactual data use)
  Detectability: 3 (requires longitudinal, multi-cycle monitoring specifically designed to detect this; not visible in single-cycle validation)
  Recoverability: 2 (correctable via counterfactual technique introduction; historical entrenchment may take further cycles to fully unwind)
  Novelty: 4 (feedback-loop/performative-prediction entrenchment is a genuinely advanced, largely unfamiliar concept outside AI/statistics-specific expertise)

If controls are absent or degraded:
  Severity: 3 (progressively entrenched, cohort-wide unfair pattern; compounding regulatory and remediation difficulty over time)
  Likelihood: 3 (probable as a structural consequence of any decide-then-retrain pipeline lacking counterfactual data)
  Detectability: 4 (very difficult to detect without deliberate multi-cycle longitudinal analysis; single-cycle validation will not reveal it)
  Recoverability: 4 (once entrenched across multiple cycles, the ground-truth data itself is contaminated, making remediation genuinely difficult — may require years of counterfactual data collection to unwind)
  Novelty: 4 (domain expert very likely to view "regular retraining" as inherently corrective, missing the entrenchment mechanism entirely)

Residual risk interpretation: This is one of the highest-novelty, hardest-to-detect and hardest-to-recover-from IRQs in the domain; even though single-cycle severity looks moderate, the compounding, self-concealing nature of the failure mode warrants sustained governance attention disproportionate to its apparent point-in-time severity.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Progressively entrenched, cohort-wide unfair pattern that compounds regulatory and remediation difficulty over time |
| **Likelihood** | 3 | Probable as a structural consequence of any decide-then-retrain pipeline lacking counterfactual data |
| **Detectability** | 4 | Very difficult to detect without deliberate multi-cycle longitudinal analysis; single-cycle validation will not reveal it |
| **Recoverability** | 4 | Once entrenched across multiple cycles, ground-truth data is itself contaminated; may require years of counterfactual data collection to unwind |
| **Novelty** | 4 | Feedback-loop/performative-prediction entrenchment is far outside traditional model validation practice for most FS domain experts |

## 17. Regulatory Basis
> No specific FCA/PRA rule names "feedback loop entrenchment" directly; this IRQ addresses a structural model-risk-management gap under general Consumer Duty (outcomes must remain fair over time, not only at initial launch) and general model risk governance expectations. [UNVERIFIED — no FCA/PRA model risk management publication explicitly addressing retraining-induced feedback loops was located as at 29 Jul 2026; SS1/23 remains the current MRM principles document, with no confirmed successor] (verified 29 Jul 2026).

## 18. Research Basis
> [Perdomo, Zrnic, Mendler-Dünner & Hardt, 2020, "Performative Prediction", ICML 2020] formally establishes the mechanics by which a deployed model's predictions shape the distribution it is subsequently trained on, providing the core theoretical grounding for this IRQ. [Ensign et al., 2018, "Runaway Feedback Loops in Predictive Policing", FAT* 2018] documents an empirically demonstrated feedback-loop entrenchment case in a public-sector predictive system, directly analogous in mechanism to the fraud/AML alerting scenario described here. Reject inference as an established credit-risk-modelling counter-technique is documented in the credit scoring literature [CONFIRMED — Anderson, R., 2007, "The Credit Scoring Toolkit: Theory and Practice for Retail Credit Risk Management and Decision Automation," Oxford University Press, ISBN 9780199226405] (verified 29 Jul 2026). Limit on the reject-inference component: [Kozodoi, N., Lessmann, S., Alamgir, M., Moreira-Matias, L. and Papakonstantinou, K., 2025, "Fighting sampling bias: A framework for training and evaluating credit scoring models," European Journal of Operational Research 324(2), 616–628, DOI 10.1016/j.ejor.2025.01.040] tested reject-inference methods, including the authors' own bias-aware self-learning method, on synthetic data and on one lender's data: 59,593 consumer micro-loan applications to a FinTech lender in Spain (2013 to 2019), with a holdout of 1,967 applications granted credit without scoring that represents the full applicant population. The abstract of the arXiv preprint (arXiv:2407.13009v1, 17 July 2024) concludes that reject inference is a difficult problem with "modest potential" to improve scorecard performance, and that addressing sampling bias in scorecard evaluation is the more promising route; the journal abstract states the second conclusion in different words. The same paper also reports gains from its own method on that data. Its real-data evidence covers one lender and one data set, the preprint gives no data-availability statement, and the paper is evidence about the component and not a test method. It limits the evidence for the reject-inference component of this IRQ and does not by itself show that component to be ineffective; the ★ ratings of this canvas are unchanged. Recorded with its provenance: the "modest potential" wording was read in the preprint (7 October 2026); the journal abstract was read as a publisher-abstract copy, and the journal full text has not been read.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-CON-001 (H.1 Discrimination & Proxy Bias: initial disparity as the seed the loop amplifies)
  - IRQ-MOD-012 (B.5 Distribution Shift & Evaluation Integrity: recursive synthetic-content collapse, a related but distinct feedback mechanism)
  - IRQ-MOD-007 (B.4 Specification Gaming: metric/intent divergence that can motivate exploiting the feedback loop)
  - IRQ-GOV-007 (I.3 Validation Governance: retraining sign-off gate addressing feedback-loop risk)
```

## 20. References
```
[1] Perdomo, J., Zrnic, T., Mendler-Dünner, C. & Hardt, M., 2020. "Performative Prediction." International Conference on Machine Learning (ICML) 2020.
    URL: https://arxiv.org/abs/2002.06673

[2] Ensign, D., Friedler, S.A., Neville, S., Scheidegger, C. & Venkatasubramanian, S., 2018. "Runaway Feedback Loops in Predictive Policing." Conference on Fairness, Accountability and Transparency (FAT*) 2018.
    URL: https://arxiv.org/abs/1706.09847
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.3 (Conduct & Fairness domain, Feedback Loops & Transparency)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): "We retrain regularly" is conventionally viewed as inherently corrective; the entrenchment mechanism via model-selected outcome data is a distinctly AI/statistics-specific insight.
✓ Test 2 (Plausible Harm): Grounded in Perdomo et al.'s formal performative prediction framework and the empirically demonstrated Ensign et al. predictive-policing feedback loop.
✓ Test 3 (Testable): Answerable via multi-cycle simulation comparing counterfactual-aware vs current retraining pipelines.
✓ Test 4 (Decision-Relevant): Outcome gates whether the retraining pipeline can be trusted to correct, rather than entrench, disparity over time.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.3.3 (2026-10-09): Field 18 Research Basis — Kozodoi et al. (European Journal of Operational Research, 2025) added as a stated limit on the reject-inference component; the preprint and journal wordings are distinguished. Research-basis review date moved. ★ ratings unchanged.
- v1.3.3 (2026-10-09): Field 9 Expected Controls — the Anderson (2007) citation takes its full title, "The Credit Scoring Toolkit: Theory and Practice for Retail Credit Risk Management and Decision Automation". Form corrections only. No change to the ★ rating or the risk profile.
```

---
---

