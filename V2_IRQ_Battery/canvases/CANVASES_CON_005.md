# CANVAS: IRQ-CON-005

## 1. IRQ ID & Title
**IRQ-CON-005: AI-Driven Financial Exclusion via Eligibility, Pricing or Servicing Decisions**

Register question: "Could AI-driven eligibility, pricing or servicing decisions systematically exclude customer segments from fair access to products (financial exclusion)?"

## 2. Business Activities Affected
- **Account opening and eligibility screening:** AI-assisted eligibility or affordability screening may systematically decline or deprioritise segments (e.g. thin-file customers, gig-economy income patterns, digitally-excluded older customers) from products they could reasonably access.
- **Pricing and product tiering:** AI-driven segmentation for pricing or product-tier allocation may effectively exclude a segment from beneficial terms available to comparable customers.
- **Digital-only servicing channels:** AI-driven channel design (e.g. digital-only onboarding or servicing) may exclude customers who cannot or do not engage digitally, without an accessible alternative route.

## 3. AI Behaviour(s)
- Scores or classifies customers using data patterns that may correlate with data availability itself (e.g. thin credit file, non-traditional income documentation) rather than genuine risk or suitability, systematically disadvantaging segments with sparser data footprints.
- Learns from a historical customer base that may itself under-represent currently excluded segments, reinforcing rather than correcting historical access gaps (cross-linked to DAT representativeness).
- Optimises for a portfolio-level profitability or risk metric that can be improved by excluding a marginally profitable or higher-variance segment entirely, even where individual members of that segment would be acceptable risks.

## 4. Failure Mode
> The system's eligibility, pricing or servicing logic systematically excludes an identifiable customer segment from fair access to a product or service, where that exclusion is not justified by genuine risk or cost differences and would not survive scrutiny under the firm's own risk appetite if surfaced explicitly.

## 5. Potential Consequences
- **Customer:** Individuals in the excluded segment are denied reasonable access to mainstream financial products, potentially pushed toward higher-cost alternative credit or excluded from essential banking services entirely.
- **Institution:** FCA Consumer Duty breach (products and services outcome, requiring products to be designed to meet the needs of the target market, including consideration of access); reputational and political/media risk given financial inclusion's public salience.
- **Regulator/Market:** Regulatory thematic review finding of systemic exclusion; broader market/political scrutiny of AI-driven access decisions in financial services.

## 6. Failure Chain
```
Historical customer base under-represents currently excluded segments
(thin-file, gig-economy income, digitally excluded)
  ↓ (IRQ-DAT-005: training data representativeness gap)
Model learns to systematically disadvantage segments correlated with
sparse data availability, not genuine risk
  ↓ (IRQ-CON-005 — THIS IRQ: no exclusion-effect testing performed
     against the firm's own risk appetite for access)
Eligibility/pricing/servicing decisions systematically exclude the
segment at scale, undetected because it presents as "declined for
risk reasons" case by case
  ↓ (IRQ-CON-001: subgroup outcome testing, if absent, fails to
     surface the pattern)
Pattern surfaces via financial inclusion campaigning body, media
investigation, or regulatory thematic review

Control Breakpoints:
  • IRQ-CON-005: exclusion-effect testing against the firm's own risk
    appetite, distinguishing genuine risk-based decline from
    data-availability-driven exclusion
  • IRQ-DAT-005: representativeness gap identified before it
    propagates into systematic exclusion
  • IRQ-GOV-006: board-approved risk appetite explicitly addresses
    access/exclusion, not only conventional credit risk
```

## 7. Why a Domain Expert May Miss It
- Credit risk SMEs are trained to view individual declines as legitimate risk-based decisions; the pattern of systematic segment-level exclusion is only visible in aggregate, and a case-by-case review of declined applications will not surface it.
- "Thin-file" or non-traditional income customers are conventionally treated as genuinely higher-risk by traditional underwriting; an AI model may over-penalise data sparsity itself (as distinct from genuine risk) in ways a traditional credit-risk SME would not distinguish without specific testing.
- Financial exclusion is often framed as a corporate social responsibility or financial inclusion strategy topic, separate from model risk/conduct review, meaning the technical mechanism by which an AI model drives exclusion may never reach the teams responsible for AI model governance.
- Digital-channel design decisions (e.g. AI-driven onboarding flows) are often owned by product/technology teams without conduct-risk sign-off, meaning "digital-only AI channel excludes non-digital customers" can be a design decision made outside conduct-risk visibility entirely.

## 8. Assurance Objective
**AO-CON-005:** Eligibility, pricing and servicing decisions materially influenced by AI shall be tested for systematic segment-level exclusion effects against the firm's board-approved risk appetite, distinguishing genuine risk/cost-based differentiation from unjustified exclusion.

## 9. Expected Controls (Traced)
- **Exclusion-effect testing against risk appetite** — [linked IRQ-GOV-006, board-approved AI risk appetite] — [FCA, PS22/9 / FG22/5, July 2022, Consumer Duty products and services outcome] — segment-level eligibility/decline rates are tested and compared against genuine risk/cost differentiation, not accepted as self-evidently risk-based.
- **Data-sparsity vs genuine-risk disaggregation** — Emerging Practice; no standardised FS methodology exists for isolating "penalised for thin data" from "penalised for genuine risk" within a single model's decision logic.
- **Alternative-channel access for digitally excluded customers** — [FCA, FG21/1, February 2021, vulnerable customer guidance, capability driver] — a non-AI-mediated or human-assisted channel remains available and is actively offered, not merely theoretically accessible.
- **Financial inclusion / access impact assessment as part of model governance sign-off** — Emerging Practice; ensuring financial inclusion considerations reach AI model governance rather than remaining siloed in a separate CSR/inclusion strategy function.
- **Subgroup outcome monitoring** — [linked IRQ-CON-001] — segment-level decline/access rates are monitored as a specific lens distinct from general subgroup fairness testing.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "declines are risk-based" with no segment-level exclusion analysis — **L1**.
- Design documentation distinguishing which model features are risk-genuine vs data-availability-correlated, and how this distinction was tested — **L2**.
- Non-production test results: segment-level (e.g. thin-file, gig-economy income) eligibility/decline rate comparison against a matched genuine-risk cohort — **L3**.
- Independent conduct-risk or internal audit review confirming exclusion-effect testing was performed and any material exclusion was escalated to the risk-appetite owner — **L4**.
- Production monitoring data: segment-level access/decline rates tracked over time against risk appetite thresholds, with breaches investigated — **L5**.

## 11. Independent Test
> On a non-production dataset, construct matched cohorts of customers with genuinely comparable risk profiles but differing data-availability characteristics (e.g. thin-file vs thick-file, gig-economy vs salaried income documentation), and compare eligibility/decline rates and pricing outcomes. Where a material gap is found, use feature-importance analysis to assess whether the gap is attributable to data-sparsity penalisation rather than genuine risk differentiation. No production customer data or live decisioning system is used. — **★1 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (downgraded from ★2). The harm mechanism — segment-level exclusion driven by data-sparsity penalisation rather than genuine risk — remains theoretically plausible and consistent with known model behaviour, but no published study has audited or instrumented a live AI/ML underwriting model to establish it empirically; the FCA, in the work cited at field 18, did not have access to the full algorithms or set of risk factors used by insurers, and EIOPA's review there, being questionnaire-based, did not examine the algorithms, so neither could test the hypothesis against a model, and the published work located that did obtain access to deployed credit models — among it a US supervisor's examinations of credit card lenders' credit scoring models, including models built with AI or ML, and one fair-lending monitorship of a consumer-lending model — measured disparity by protected characteristic, not exclusion by data sparsity. The matched-cohort methodology this Independent Test specifies is itself untested against a real deployed model outside this standard, and that published work applied different methods — disparity metrics by protected characteristic and a search for less discriminatory alternatives — so assurance depends entirely on the assessor's construction of the matched cohorts and interpretation of the feature-importance analysis, with no benchmark or precedent to check the result against.

## 12. Pass Indicators
- Segment-level exclusion testing has been performed comparing matched-risk cohorts across data-availability characteristics.
- Any material exclusion gap found is attributable to a documented, board-accepted risk/cost justification, not unexamined data-sparsity penalisation.
- An actively offered alternative channel exists for digitally excluded customers, not merely a theoretical option.
- Production monitoring tracks segment-level access rates against the firm's risk appetite.

## 13. Fail Indicators
- No segment-level exclusion testing exists; individual declines are assumed risk-based without matched-cohort comparison.
- A material exclusion gap is found with no risk/cost justification, indicating unexamined data-sparsity penalisation.
- No alternative channel exists (or it exists only nominally) for customers excluded from a digital-only AI channel.
- No production monitoring of segment-level access rates against risk appetite.

## 14. Reporting Language
**Pass:** "Segment-level exclusion testing across data-availability characteristics found no unjustified access gap; alternative channels remain actively available for digitally excluded customers. Conclusions rest on ★1 methodology — the harm mechanism is theoretically plausible but no published study has audited a live AI/ML underwriting model to establish it, and the matched-cohort approach is itself untested against a real deployed model, so result quality depends entirely on assessor expertise — and should be read as expert opinion, not evidence."

**Fail:** "No segment-level exclusion testing has been performed. This is a direct Consumer Duty and financial inclusion risk: individual declines are assumed risk-based without verification that data-sparsity, rather than genuine risk, is not driving systematic segment exclusion."

**Partial:** "Segment-level testing was performed for thin-file customers and found no material unjustified gap, but gig-economy income documentation patterns have not been separately tested. Remediation should extend the methodology to this cohort before comprehensive assurance can be given."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (segment-level access disadvantage, generally proportionate to genuine risk once tested)
  Likelihood: 2 (foreseeable given data-sparsity correlation with certain segments; mitigated by active testing)
  Detectability: 2 (segment-level monitoring surfaces gaps within a reporting cycle)
  Recoverability: 2 (remediable via model adjustment and alternative-channel provision within weeks to months)
  Novelty: 3 (isolating data-sparsity penalisation from genuine risk is a specific, AI-model-behaviour insight beyond traditional underwriting review)

If controls are absent or degraded:
  Severity: 3 (systemic segment exclusion; Consumer Duty breach; reputational and political/media exposure given financial inclusion's public salience)
  Likelihood: 3 (probable given known tendency of models to penalise data sparsity as a proxy for risk)
  Detectability: 4 (silent, case-by-case failure that looks individually legitimate; typically surfaces only via external campaigning body, media investigation or thematic review)
  Recoverability: 3 (multi-month remediation including model redesign, alternative channel build-out, and potential redress consideration)
  Novelty: 4 (domain expert very likely to treat individual declines as self-evidently risk-based without segment-level testing)

Residual risk interpretation: High priority given very poor detectability absent deliberate testing and the public/political salience of financial exclusion as a conduct issue.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Systemic segment exclusion; Consumer Duty breach with reputational and political/media exposure |
| **Likelihood** | 2 | Foreseeable given known data-sparsity-as-risk-proxy tendency; mitigated where active testing exists |
| **Detectability** | 4 | Silent, case-by-case failure indistinguishable from legitimate risk-based decline without deliberate segment-level testing |
| **Recoverability** | 3 | Multi-month remediation including model redesign and alternative-channel build-out once identified |
| **Novelty** | 4 | Individual declines are conventionally assumed self-evidently risk-based; segment-level data-sparsity effects are an AI-specific blind spot |

## 17. Regulatory Basis
> [FCA, PS22/9, July 2022, and FG22/5, July 2022, "Consumer Duty final guidance"] requires products and services to be designed to meet the needs of the identified target market, including consideration of access and exclusion effects. [FCA, FG21/1, February 2021] addresses capability-driven vulnerability, relevant to digitally excluded customers lacking an alternative channel. [UNVERIFIED — no FCA financial inclusion strategy publication specifically naming AI-driven exclusion was located; FG21/1 (vulnerability) and Consumer Duty remain the closest confirmed anchors] (verified 29 Jul 2026).

## 18. Research Basis
> No published research at level (a) — an empirical finding that an identifiable customer segment is systematically excluded from access to a financial product, with an AI or algorithmic decision system audited or instrumented as the demonstrated mechanism — was located, across searches covering UK, EU and US regulators and supervisors, fair-lending monitorships, central-bank and academic literature, and insurance/poverty-premium work. This is not a search failure: the located work that had access to a deployed model examined a different question — disparity by protected characteristic — and the work that asked this question did not examine the models; the constraint is examination of a deployed model where this question is asked, not analytical technique.
>
> [FCA, "Motor Insurance Pricing and Local Area Ethnicity in England and Wales" (Research Note), 10 December 2025] found the best-known UK claim of algorithmically-linked price disparity substantially collapses once risk is controlled for: **as illustrated by the FCA's own worked example**, a raw ~£300 ethnicity-linked motor premium differential shrinks to a £28 residual on a £627 premium once claims costs and other risk factors are taken into account. The regulator states plainly that it "did not have access to the full algorithms or set of risk factors used by insurers." The regulator with the strongest UK mandate to test this could not open the model it was investigating. *(Precision note: the £300/£28/£627 figures are the Note's Luton worked example, not a population-wide result; the framing above states them as the illustration they are.)*
>
> [EIOPA, *Big Data Analytics in Motor and Health Insurance: A Thematic Review*, April 2019] — a questionnaire-based review, "essentially descriptive of the information gathered" from insurance firms, national supervisors and consumer associations (Annex I, p.50) — built a six-indicator test specifically for the exclusion hypothesis and found no convergent signal across 222 insurers in 28 jurisdictions, while stating its own instrument is "not possible to proof financial inclusion/exclusion issues by these indicators" — a weak null on 2018 data, not a disproof. EIOPA has not revisited these indicators since: its AI Governance and Risk Management Opinion of August 2025 [EIOPA-BoS-25-360] returns zero occurrences of "exclusion" on independent word-search of the full document.
>
> Where the access-margin literature is rigorous, it runs the other way. [Fuster, A., Goldsmith-Pinkham, P., Ramadorai, T. & Walther, A., 2022, "Predictably Unequal? The Effects of Machine Learning on Credit Markets," *Journal of Finance*, DOI 10.1111/jofi.13090] finds machine learning increases rate dispersion within and across groups, but on the access margin specifically "marginally increases overall credit access and marginally reduces acceptance-rate disparity." [Berg, T., Burg, V., Gombović, A. & Puri, M., 2020, "On the Rise of FinTechs — Credit Scoring Using Digital Footprints," *Review of Financial Studies* 33(7)] finds digital-footprint scoring "affects access to credit" for customers a bureau score cannot reach, extending scorability rather than excluding on the margin it tests.
>
> The honest conclusion is not that AI does not cause segment-level exclusion; it is that the FCA, in the work cited above, did not have access to the full algorithms or set of risk factors, and EIOPA's questionnaire-based review did not examine them, and that the published work located which obtained such access examined a different question — disparity by protected characteristic, not exclusion by data sparsity. [Relman Colfax PLLC, 2021–2024, "Fair Lending Monitorship of Upstart Network's Lending Model", four public reports, 14 April 2021 to 27 March 2024; the quotations from the Fourth and Final Report, 27 March 2024, n.8 (p.6) and pp.8–9] tested a machine-learning consumer-lending model with "more complete access to Upstart's model and underlying data", identified "statistically and practically significant" adverse "approval/denial disparities for Black applicants", and stated expressly that "[t]hese findings do not, standing alone, demonstrate a fair lending violation"; the disparities were measured without an assessment of business necessity, the monitor having proceeded on the assumption that the model was necessary to a legitimate interest, and the monitorship closed without agreement between the parties on the methodology for judging whether a less discriminatory alternative model performs comparably. [Consumer Financial Protection Bureau, 2025, "Supervisory Highlights: Advanced Technologies Special Edition", Issue 38, Winter 2025, §2.1.1, p.4] records that examiners reviewed credit card lenders' credit scoring models, "including models built with AI or ML technology", found "disparities in underwriting and pricing outcomes for Black or African American and Hispanic applicants", and identified alternative models that "used the same credit strategy, machine learning algorithm, and external configuration variables as the institutions' models" — a supervisory finding on examined models, published without naming the institutions and addressed to disparity by protected characteristic. No supervisory finding, judgment or ombudsman decision located establishes the data-sparsity exclusion this question tests. That constraint — no access where this question has been asked, and a different question where access was had — not an absence of concern, is the basis for this claim's rating, and it is the case for independent assurance stated in the standard's own register, not sold as one: a testing regime with model access is the only route by which this question could be answered from outside the firm.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-CON-001 (H.1 Discrimination & Proxy Bias: subgroup outcome testing as a complementary lens)
  - IRQ-DAT-005 (A.1 Training Data Provenance: representativeness gap upstream of exclusion)
  - IRQ-GOV-006 (I.2 Approval, Tiering & Policy: board-approved risk appetite as the exclusion-testing benchmark)
  - IRQ-CON-006 (H.2 Price Fairness: exclusion via pricing rather than eligibility)
  - IRQ-CON-010 (H.2 Customer Outcomes, Vulnerability & Access:
    narrowing of options by engineered journey friction rather than
    by an eligibility, pricing or servicing decision; CON-005 §2's
    digital-only channel limb is the nearest overlap)
```

## 20. References
```
[1] Financial Conduct Authority, 2022. "PS22/9 — A new Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publications/policy-statements/ps22-9-new-consumer-duty

[2] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf

[3] Financial Conduct Authority, 2021. "FG21/1 — Guidance for firms on the fair treatment of vulnerable customers."
    Published: February 2021
    URL: https://www.fca.org.uk/publications/finalised-guidance/guidance-firms-fair-treatment-vulnerable-customers

[4] Relman Colfax PLLC, 2021–2024. "Fair Lending Monitorship of Upstart Network's Lending Model." Initial Report, 14 April 2021;
    Second Report, 10 November 2021; Third Report, 16 September 2022; Final Report, 27 March 2024.
    URL: https://www.relmanlaw.com/cases-upstart-network-fair-lending-counseling

[5] Consumer Financial Protection Bureau, 2025. "Supervisory Highlights: Advanced Technologies Special Edition." Issue 38, Winter 2025.
    Published: January 2025
    URL: https://files.consumerfinance.gov/f/documents/cfpb_supervisory-highlights-advanced-technologies_2025-01.pdf
    Read at the Internet Archive capture of 18 January 2025.

[6] European Insurance and Occupational Pensions Authority, 2019. "Big Data Analytics in Motor and Health Insurance: A Thematic Review." Annex I (Methodology), p.50.
    Published: 2019 (the document states no month; EIOPA's file name carries April 2019)
    URL: https://register.eiopa.europa.eu/Publications/EIOPA_BigDataAnalytics_ThematicReview_April2019.pdf

[7] European Insurance and Occupational Pensions Authority, 2025. "Opinion on AI Governance and Risk Management." EIOPA-BoS-25-360.
    Published: 6 August 2025
    URL: https://www.eiopa.europa.eu/publications/opinion-artificial-intelligence-governance-and-risk-management_en
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.2 (Conduct & Fairness domain, Customer Outcomes, Vulnerability & Access)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Credit risk SMEs treat individual declines as self-evidently risk-based; segment-level exclusion is only visible via deliberate matched-cohort testing.
✓ Test 2 (Plausible Harm): Grounded in Consumer Duty products-and-services access requirements; the data-sparsity-as-risk-proxy mechanism is reasoned from documented information asymmetries — no published study instruments it directly (field 18; hence ★1).
✓ Test 3 (Testable): Answerable via matched-cohort segment-level exclusion testing in a non-production environment.
✓ Test 4 (Decision-Relevant): Outcome gates whether eligibility/pricing logic can be relied upon as genuinely risk-based rather than exclusionary.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.1.0 (2026-08-25): ★ re-rated ★2 → ★1 on the evaluation-harm-evidence review (no credible research basis as scoped; access-to-evidence framing); caveats added to field 11 and the CON playbook sheet.
- v1.2.0 (2026-09-12): Field 19 — IRQ-CON-010 added as the reciprocal cross-reference (narrowing of options by engineered journey friction rather than by an eligibility, pricing or servicing decision; this canvas's field 2 digital-only channel limb is the nearest overlap). No other field changed; ★1 unchanged.
- v1.2.1 (2026-09-19): Fields 11 and 18 — erratum. The statement that no outside party has had algorithm access is corrected: the FCA, in the work cited, did not have access to the full algorithms or set of risk factors, and EIOPA's review did not examine the algorithms; a US supervisor's examinations of credit card lenders' credit scoring models, including models built with AI or ML, obtained access and reported disparities by protected characteristic; and one published fair-lending monitorship of a machine-learning consumer-lending model obtained access to the model and its underlying data and reported an approval disparity it expressly declined to characterise as a violation, the monitorship closing without agreement on the methodology for judging a less discriminatory alternative. Neither examined exclusion by data sparsity, and no supervisory finding, judgment or ombudsman decision located establishes it. The matched-cohort methodology this canvas specifies remains untested against a deployed model. No incident is added: the evidence does not reach this canvas's own bar on the unjustified-exclusion limb. Reference entries [4] to [7] added at Field 20 ([6] and [7] the EIOPA thematic review and Opinion cited in Field 18). Field 18 — the EIOPA thematic review's questionnaire basis stated from its methodology annex, as the ground for the statement that EIOPA's review, in the work cited, did not examine the algorithms; the search-coverage sentence names the US supervisory and monitorship material. Research-basis review date moved. ★1 unchanged; the rating question is carried to the next review with the monitorship's four reports and the supervisory findings as its evidence pack.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

