# CANVAS: IRQ-DAT-005

## 1. IRQ ID & Title
**IRQ-DAT-005: Training Data Under-Representing the Current Customer Book**

Register question: "Does the training or reference data materially under-represent segments of the firm's current customer book, product set or market conditions?"

## 2. Business Activities Affected
- **Credit scoring and affordability assessment:** A model trained predominantly on a legacy customer profile mishandles newer segments (e.g. gig-economy income, thin-file applicants, recent product launches).
- **Insurance pricing and underwriting:** Reference data reflecting an outdated market mix under-prices or over-prices risk for segments that have grown since the data was collected.
- **AML/fraud detection:** Reference typologies trained on historical patterns miss newly prevalent fraud vectors or customer segments underrepresented in the original data collection window.

## 3. AI Behaviour(s)
- Optimises for the distribution present in its training/reference data, regardless of whether that distribution still matches the current customer book.
- Produces confident outputs for underrepresented segments with no inherent signal that its training exposure to that segment was thin.
- Is validated against test sets often drawn from the same (potentially unrepresentative) source as the training data, masking the gap.

## 4. Failure Mode
> The training or reference data materially under-represents segments of the firm's current customer book, product set or market conditions, so the model's demonstrated performance does not generalise to the population it is actually deployed against.

## 5. Potential Consequences
- **Customer:** Underrepresented segments receive systematically worse-calibrated decisions (declines, pricing, fraud false positives) without this being visible in aggregate performance metrics.
- **Institution:** Model risk materialises silently — aggregate accuracy looks fine while a growing customer segment is poorly served, until volume makes the gap material.
- **Regulator:** Consumer Duty fair-access and outcome obligations, and EU AI Act Art. 10(3) representativeness requirements, are breached if this is undetected.

## 6. Failure Chain
```
Training/reference data collected at a point in time or from a source
that does not track the current customer book, product mix or market
  ↓ (IRQ-DAT-005 — THIS IRQ: representativeness gap undetected)
Model trained/validated on this unrepresentative population;
aggregate accuracy metrics look acceptable
  ↓ (IRQ-DAT-011: population drift compounds the original gap over time)
Underrepresented segment grows in the live book (new product,
demographic shift, market change) without model re-validation
  ↓ (IRQ-MOD-010: distribution-shift-specific validation absent)
Model performs systematically worse for that segment; not visible
in blended aggregate KPIs
  ↓
Fair-access/Consumer Duty finding or financial loss concentrated in
the underrepresented segment

Control Breakpoints:
  • IRQ-DAT-005: representativeness assessment against current book at model build/refresh
  • IRQ-DAT-011: population drift monitoring triggers re-assessment
  • IRQ-MOD-010: segment-stratified validation, not aggregate-only
```

## 7. Why a Domain Expert May Miss It
- Aggregate accuracy and KPI dashboards are the default review artefact; segment-level under-representation is invisible unless explicitly stratified.
- "The model was validated and approved" is treated as a permanent state, when representativeness is a point-in-time property that decays as the customer book evolves (a book grown 20% in a new segment since approval is a different population).
- Credit/underwriting SMEs know about population shift conceptually but rarely have the tooling or mandate to re-run representativeness checks outside a full model redevelopment cycle.
- New product launches are often assumed "covered" by the nearest existing model category without an explicit representativeness gap analysis.

## 8. Assurance Objective
**AO-DAT-005:** The firm shall assess and document the representativeness of training and reference data against its current customer book, product set and market conditions, at build and at defined refresh intervals, with material gaps disclosed.

## 9. Expected Controls (Traced)
- **Segment-stratified representativeness assessment at model build** — [EU AI Act, Regulation (EU) 2024/1689, Art. 10(3), representativeness requirement] — training data population compared against the current customer book by segment, product and geography.
- **Periodic re-assessment triggered by population drift signals** — [linked IRQ-DAT-011; Koh et al., 2021, "WILDS: A Benchmark of in-the-Wild Distribution Shifts"] — representativeness is re-tested, not assumed permanent, on a defined cadence or drift-trigger basis.
- **Segment-stratified (not aggregate-only) performance validation** — [D'Amour et al., 2020/22, "Underspecification Presents Challenges for Credibility in Modern Machine Learning", JMLR] — validation reporting disaggregates performance by segment so under-representation effects are visible.
- **New-product/segment gap analysis before extending an existing model's scope** — [PRA SS1/23 development principle] — explicit assessment before a model is applied to a customer segment or product it was not built to cover.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the training data is representative of our customers" with no comparison — **L1**.
- Representativeness assessment methodology and current-book comparison document at model build — **L2**.
- Segment-stratified validation results showing performance by customer segment, product and vintage — **L3**.
- Independent validation report confirming representativeness assessment was inspected against current book data, not asserted — **L4**.
- Production monitoring: segment-level outcome/performance metrics tracked over time, with drift-triggered re-assessment records — **L5**.

## 11. Independent Test
> In a non-production environment, compare the statistical composition of the training/reference dataset (by segment, product, vintage, geography) against a current snapshot of the live customer book. Quantify the gap using standard distributional comparison methods (e.g. population stability index, two-sample tests per Rabanser et al., 2019). Where representativeness gaps are found, evaluate model performance specifically on a held-out sample matching the underrepresented segment, comparing it against aggregate reported performance. Methodology follows established distribution-shift detection practice (Rabanser et al., 2019; Koh et al., 2021), well-precedented but requiring firm-specific segment definitions. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (published, multiply-used statistical shift-detection methods; segment definition and materiality thresholds require professional judgement, so short of ★4).

## 12. Pass Indicators
- Representativeness assessment on file at build and refreshed on a defined cadence, comparing training data against current book composition.
- No segment shows a material distributional gap (e.g. PSI above the firm's documented threshold) without a corresponding validated performance check.
- Segment-stratified validation results are reported alongside aggregate accuracy, not instead of it.
- New product/segment extensions of an existing model are preceded by an explicit gap analysis.

## 13. Fail Indicators
- No representativeness comparison exists; validation reporting is aggregate-only.
- A materially grown or new customer segment is absent or thin in the training data with no documented gap analysis.
- Segment-stratified performance, when tested, shows material degradation for an underrepresented segment invisible in aggregate KPIs.
- An existing model is extended to a new product without a documented representativeness check.

## 14. Reporting Language
**Pass:** "Training data composition for [model] was compared against the current customer book; no segment shows a material representativeness gap against the documented threshold. Segment-stratified validation confirms performance parity across segments, not merely acceptable aggregate accuracy (★3 methodology)."

**Fail:** "Training data for [model] materially under-represents [segment], which now constitutes [x]% of the live book. Segment-stratified testing found performance materially worse for this segment than the reported aggregate accuracy suggests. This is a fair-access and model-risk finding: the model's approved performance claim does not generalise to a growing part of the population it serves."

**Partial:** "Representativeness assessment exists at initial model build but has not been refreshed since [date], despite [x]% growth in [segment]. The assurance objective requires re-assessment before continued reliance on the original representativeness claim."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (segment-level poor decisions at scale; fair-access/Consumer Duty exposure)
  Likelihood: 2 (requires the refresh cadence or drift trigger to be missed, plausible over long model lifespans)
  Detectability: 2 (segment-stratified monitoring, once in place, surfaces this within a monitoring cycle)
  Recoverability: 2 (remediable via retraining/recalibration on updated data)
  Novelty: 2 (representativeness is a familiar model-risk concept; the AI-specific element is the silent aggregate-metric masking)

If controls are absent or degraded:
  Severity: 3 (sustained poor outcomes for a growing segment, undetected for extended periods)
  Likelihood: 3 (representativeness decay over a multi-year model lifespan without refresh is a common, foreseeable pattern)
  Detectability: 4 (aggregate KPIs mask segment-level degradation entirely without stratified monitoring)
  Recoverability: 2 (retraining/recalibration once identified)
  Novelty: 2
Residual risk: material and cumulative; the primary danger is that aggregate metrics actively conceal it.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Systematic poor outcomes for a customer segment at scale; Consumer Duty fair-access exposure. |
| **Likelihood** | 2 | Plausible over a model's lifespan if refresh/drift-trigger discipline lapses; not the default with active MRM. |
| **Detectability** | 3 | Requires deliberate segment-stratified monitoring; aggregate KPIs actively conceal the gap. |
| **Recoverability** | 2 | Remediable via retraining/recalibration on updated data within a defined cycle. |
| **Novelty** | 2 | Representativeness is a recognised model-risk concept; the AI-specific twist is aggregate-metric concealment. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(3)] requires training, validation and testing data to be sufficiently representative of the persons or groups of persons in respect of whom the AI system is intended to be used. [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] fair-access and outcomes obligations engage where representativeness gaps produce systematically worse outcomes for a segment. [PRA SS1/23, Principle 3] development principle requires data fit for the model's intended population. (verified 29 Jul 2026)

## 18. Research Basis
> [Koh, P.W., et al., 2021, "WILDS: A Benchmark of in-the-Wild Distribution Shifts", arXiv:2012.07421] — real-world shift benchmarks demonstrating large in-the-wild performance drops from population mismatch. [D'Amour, A., et al., 2020/22, "Underspecification Presents Challenges for Credibility in Modern Machine Learning", JMLR, arXiv:2011.03395] — identical test performance can mask divergent deployment behaviour, directly explaining why aggregate metrics conceal segment-level representativeness gaps. [Rabanser, S., et al., 2019, "Failing Loudly: An Empirical Study of Methods for Detecting Dataset Shift", arXiv:1810.11953] — practical two-sample-test shift-detection methodology underpinning the independent test above.
>
> **[FAIAS Incident Register, row 59, "Upstart Holdings FY2022 Form 10-K", 2023]** — the company's own annual report states that "the bulk of the data gathered and the development of our AI models have largely occurred during a period of sustained economic growth or during the COVID-19 pandemic", and that "Our AI models have not been extensively tested during other adverse economic cycles". It also records that loans from 2021 to mid-2022 bought by institutional investors underperformed target returns; the filing does not link the data gap to that result, so the row does not show that the gap caused it.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-011 (A.5: statistical/semantic/source drift — the temporal compounding of this gap)
  - IRQ-MOD-010 (B.5: distribution-shift-specific validation, incl. population shift)
  - IRQ-CON-001 (H.1: subgroup outcome equity — the fairness-facing symptom)
  - IRQ-GOV-012 (I.2: operating-envelope drift — new product/segment extension without re-approval)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10(3).
[2] FCA, 2022. "PS22/9: A New Consumer Duty" and "FG22/5." PRIN 2A in force 31 July 2023.
[3] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023).
[4] Koh, P.W., et al., 2021. "WILDS: A Benchmark of in-the-Wild Distribution Shifts." arXiv:2012.07421.
[5] D'Amour, A., et al., 2020. "Underspecification Presents Challenges for Credibility in
    Modern Machine Learning." JMLR. arXiv:2011.03395.
[6] Rabanser, S., Günnemann, S., Lipton, Z., 2019. "Failing Loudly: An Empirical Study of
    Methods for Detecting Dataset Shift." arXiv:1810.11953.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Aggregate KPI dashboards actively conceal segment-level
  representativeness gaps; SMEs rarely have stratified tooling by default.
✓ Test 2 (Plausible Harm): Grounded in D'Amour et al. (2020) underspecification findings
  and WILDS benchmark evidence of real-world shift impact.
✓ Test 3 (Testable): Distributional comparison and segment-stratified holdout testing are
  executable in non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates model refresh timing and new-product/segment extension approval.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 59, Upstart Holdings Form 10-K for 2022: the data-gap statement is the evidence, and the filing does not link the outcome to it). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
```

---
---

