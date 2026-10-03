# CANVAS: IRQ-CON-006

## 1. IRQ ID & Title
**IRQ-CON-006: Unfair Differential Pricing Untethered from Cost or Risk**

Register question: "Where AI influences pricing or value, can it produce differential pricing untethered from cost or risk (e.g. inertia pricing, willingness-to-pay exploitation)?"

## 2. Business Activities Affected
- **Insurance renewal pricing:** AI-driven pricing optimisation may systematically price loyal/inert customers higher than new customers with equivalent risk, exploiting demonstrated low price-sensitivity (inertia pricing) rather than pricing to genuine risk or cost.
- **Personal loan and credit card pricing:** AI-driven willingness-to-pay estimation may set individualised pricing based on inferred price sensitivity or behavioural signals unrelated to credit risk or cost of funds.
- **Add-on product and cross-sell pricing:** AI-driven dynamic pricing for ancillary products may exploit customer inattention or behavioural signals to maximise extraction rather than reflecting fair value.

## 3. AI Behaviour(s)
- Estimates individual or segment-level price elasticity/willingness-to-pay from behavioural and historical data, and can set price to maximise expected revenue extraction from low-elasticity customers rather than reflecting genuine cost or risk differences.
- Learns that customer inertia (failure to switch or negotiate) is itself predictive of tolerance for a price increase, and can price accordingly without any risk or cost signal being involved at all.
- Optimises a revenue or margin metric that, absent an explicit fair-value constraint, treats price discrimination based on behavioural inertia as simply "successful pricing", with no inherent signal that this constitutes unfair value.

## 4. Failure Mode
> The system sets or recommends a price for an individual customer or segment that is materially untethered from genuine cost or risk differences, and is instead driven by inferred price sensitivity, inertia, or willingness-to-pay signals, absent a fair-value test that would flag this as inconsistent with Consumer Duty price-and-value expectations.

## 5. Potential Consequences
- **Customer:** Loyal or low-price-sensitivity customers systematically pay more than new or price-sensitive customers for materially the same product, without a cost or risk basis for the difference.
- **Institution:** FCA Consumer Duty price and value outcome breach; potential General Insurance Pricing Practices remedy analogues extended to AI-driven pricing; redress costs if a systemic pattern is confirmed.
- **Regulator/Market:** Regulatory finding echoing the FCA's prior general insurance pricing intervention (addressing "loyalty penalty" pricing), now applied to a newer AI-driven pricing mechanism; reputational damage from perceived exploitation of loyal customers.

## 6. Failure Chain
```
AI pricing model incorporates behavioural/inertia signals alongside
(or instead of) genuine cost/risk factors
  ↓ (IRQ-CON-006 — THIS IRQ: no fair-value/price-tethering test
     performed to isolate inertia-driven pricing from risk-based
     pricing)
Model recommends or sets price optimised for revenue extraction from
low-elasticity (inert) customers
  ↓ (IRQ-GOV-006: board risk appetite does not explicitly address
     price-fairness for AI-driven pricing)
Systematic price differential accrues across the loyal/inert customer
base, individually invisible but cumulatively material
  ↓
Regulatory thematic review or "loyalty penalty" style finding;
Consumer Duty price and value breach; redress exercise

Control Breakpoints:
  • IRQ-CON-006: price-fairness testing explicitly isolates
    inertia/behavioural pricing effects from genuine cost/risk
    differentiation
  • IRQ-CON-005: exclusion-effect testing lens applied to pricing
    outcomes specifically
  • IRQ-GOV-006: board risk appetite explicitly extends to AI-driven
    pricing fairness, not only credit/insurance underwriting risk
```

## 7. Why a Domain Expert May Miss It
- Pricing actuaries and product SMEs are accustomed to price differentiation being risk- or cost-based by design (e.g. insurance underwriting factors); an AI pricing model that incorporates behavioural elasticity signals may be reviewed using the same "is this actuarially justified" lens without recognising that elasticity-based pricing is a categorically different (and potentially unfair) basis.
- "The model improves overall profitability" is a metric pricing teams are typically incentivised to optimise; a domain expert focused on commercial performance may not independently ask whether the profitability improvement specifically derives from exploiting inert customers.
- The FCA's 2021 general insurance pricing intervention addressed "loyalty penalty" pricing through a rules-based remedy (equivalent new/renewal pricing); a domain expert may believe this issue is "solved" by that remedy without recognising that an AI model can reconstruct an equivalent effect through more granular individualised elasticity pricing that a blunt new/renewal rule does not fully prevent.
- Individual price differences may be small and defensible in isolation; the systemic pattern (this segment consistently pays more, unrelated to risk) is only visible in aggregate analysis specifically designed to isolate elasticity effects from risk effects.

## 8. Assurance Objective
**AO-CON-006:** AI-influenced pricing shall be tested to isolate and constrain price differentiation driven by inferred price sensitivity or inertia from differentiation driven by genuine cost or risk, consistent with Consumer Duty fair-value expectations.

## 9. Expected Controls (Traced)
- **Price-fairness / fair-value testing isolating elasticity from risk/cost** — [FCA, PS22/9, July 2022, Consumer Duty price and value outcome] — Emerging Practice; a specific, standardised methodology for decomposing AI-set prices into risk/cost-justified vs elasticity-driven components is not established, extending the intent of the FCA's general insurance pricing remedy to a more granular AI context.
- **General Insurance Pricing Practices remedy principle, extended to AI-driven granular pricing** — [FCA, PS21/5, May 2021, "General insurance pricing practices"] — the underlying "no unjustified new/renewal or loyalty differential" principle is applied and tested against AI-driven individualised pricing, not only the blunt product-level remedy originally mandated.
- **Board risk appetite extension to AI pricing fairness** — [linked IRQ-GOV-006] — pricing-specific fairness risk appetite is explicitly documented, not assumed to be covered by general credit/insurance risk appetite.
- **Segment-level price differential monitoring** — [linked IRQ-CON-005] — the exclusion-testing lens is applied specifically to pricing outcomes to detect systematic differential untethered from risk.
- **Customer communication/transparency on pricing basis** — [linked IRQ-CON-008] — where AI materially influences price, the basis is disclosed in a manner consistent with transparency expectations.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "pricing is risk-based" with no decomposition analysis performed — **L1**.
- Design documentation identifying which pricing model features are risk/cost factors vs behavioural/elasticity factors — **L2**.
- Non-production test results: price decomposition analysis on a representative customer set, isolating the elasticity-driven component of price and comparing it against risk/cost-only pricing — **L3**.
- Independent pricing/actuarial or internal audit review confirming the decomposition methodology and findings — **L4**.
- Production monitoring data: price differential between loyal/inert and new/price-sensitive customer segments tracked over time, controlling for risk/cost, with material gaps investigated — **L5**.

## 11. Independent Test
> On a non-production representative dataset, fit or inspect the pricing model's feature contributions to decompose the final price into a risk/cost-justified component and a behavioural/elasticity-driven component (e.g. via feature ablation: recompute price with elasticity/inertia features removed and compare). Measure the magnitude of the elasticity-driven component for loyal/inert customer segments versus new/price-sensitive segments with equivalent risk/cost profiles. No production customer data or live pricing system is used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the FCA's general insurance pricing intervention establishes the regulatory principle and a precedent methodology at product level; decomposition testing at the individualised AI-model level is bespoke, with no agreed FS benchmark for isolating elasticity from risk within a single model).

## 12. Pass Indicators
- Price decomposition testing demonstrates the elasticity/inertia-driven component of price, if any, is immaterial or explicitly bounded within a board-approved fair-value tolerance.
- No material, unexplained price differential is found between loyal/inert and new/price-sensitive customers with equivalent risk/cost profiles.
- Board risk appetite explicitly addresses AI-driven pricing fairness.
- Production monitoring confirms the pattern remains within tolerance over time.

## 13. Fail Indicators
- No decomposition testing exists; pricing is assumed risk-based without verification.
- Decomposition testing finds a material elasticity-driven price differential between loyal/inert and price-sensitive equivalent-risk customers, with no board-approved tolerance or remediation.
- Board risk appetite does not address AI-driven pricing fairness specifically.
- Production monitoring shows a persistent, unremediated price differential pattern.

## 14. Reporting Language
**Pass:** "Price decomposition testing confirms the elasticity/inertia-driven component of AI-influenced pricing is immaterial and within board-approved fair-value tolerance; no material unexplained price differential was found between loyal and price-sensitive equivalent-risk customers. Conclusions rest on ★2 methodology — bespoke, professional-judgement-dominant testing extending an established regulatory principle — and should be read as a point-in-time assessment."

**Fail:** "No price decomposition testing has been performed; pricing is assumed risk-based without verification. This is a direct Consumer Duty price-and-value risk, and echoes the pattern the FCA's general insurance pricing intervention was designed to address, now potentially reconstructed via AI-driven individualised elasticity pricing."

**Partial:** "Decomposition testing was performed for the primary product line and found no material unexplained differential, but has not yet been extended to ancillary/add-on product pricing, where elasticity-based dynamic pricing is also in use. Remediation should extend the testing scope before comprehensive assurance can be given."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (individually modest price differential, bounded within a board-approved tolerance)
  Likelihood: 2 (foreseeable given commercial incentive to price to elasticity; mitigated by active decomposition testing)
  Detectability: 2 (segment-level price monitoring surfaces gaps within a reporting cycle)
  Recoverability: 2 (remediable via pricing model adjustment within weeks to months)
  Novelty: 3 (decomposing AI-driven individualised elasticity pricing from risk-based pricing is a more granular version of a known regulatory concern, requiring AI-specific methodology)

If controls are absent or degraded:
  Severity: 3 (systemic unfair pricing across a loyal/inert customer segment; Consumer Duty breach; echoes a previously remediated industry-wide issue, compounding reputational risk)
  Likelihood: 3 (probable given clear commercial incentive to price to elasticity absent an explicit constraint)
  Detectability: 4 (silent, individually-small differential; visible only via deliberate decomposition analysis, not routine pricing review)
  Recoverability: 3 (multi-month remediation including pricing model redesign and potential redress to affected customers)
  Novelty: 4 (domain expert very likely to treat AI-driven pricing as simply a more sophisticated version of already-approved actuarial pricing, missing the elasticity-exploitation mechanism)

Residual risk interpretation: High priority given the precedent of prior regulatory intervention on an analogous issue (general insurance pricing practices) — a recurrence via a more sophisticated AI mechanism would be viewed particularly unfavourably by the regulator.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Systemic unfair pricing echoing a previously remediated industry issue; Consumer Duty breach |
| **Likelihood** | 2 | Foreseeable given commercial incentive to price to elasticity; mitigated where active decomposition testing exists |
| **Detectability** | 4 | Silent, individually-small price differential; visible only via deliberate decomposition analysis |
| **Recoverability** | 3 | Multi-month remediation including pricing model redesign and potential customer redress |
| **Novelty** | 4 | Domain expert likely to treat AI pricing as a sophistication of already-approved actuarial pricing, missing the elasticity-exploitation mechanism |

## 17. Regulatory Basis
> [FCA, PS22/9, July 2022, "A new Consumer Duty"] establishes the price and value outcome, requiring fair value relative to cost/benefit. [FCA, PS21/5, May 2021, "General insurance pricing practices"] establishes the specific regulatory precedent addressing loyalty-penalty/elasticity-driven pricing in a product-level remedy, directly relevant by extension to AI-driven individualised pricing.

## 18. Research Basis
> [FCA, General Insurance Pricing Practices Market Study, Final Report MS18/1.3, 22 September 2020, and PS21/5, "General insurance pricing practices: Feedback to CP20/19 and final rules," May 2021] is the strongest available citation for this claim: an FS-specific, empirical, regulator-run study built on firm-level pricing data, naming the pricing-model mechanism (margin-optimisation, conversion and retention modelling) and quantifying the harm directly. It found insurers used these models to identify price-insensitive, low-switching customers — correlated with lower awareness and vulnerability — and raise their price at each renewal, decoupled from risk: customers of five-or-more years' tenure paid on average 85% more for motor and 122% more for home insurance than an equivalent new customer, an estimated £1.2bn overcharged in 2018, and the practice was banned from January 2022 (an estimated £4.2bn consumer saving over ten years). This evidences the loyalty-penalty/inertia-pricing mechanism at scale in a UK financial-services market, though the study does not isolate machine learning specifically as against statistical or actuarial pricing models more broadly — a distinction to carry into any citation of it as ML-specific evidence.
>
> This should be read against a tempering finding from the same regulator on a related pricing question. [FCA, "Motor Insurance Pricing and Local Area Ethnicity in England and Wales" (Research Note), 10 December 2025] tested the best-known UK claim of algorithmically-linked price disparity and found it substantially collapses once risk is controlled for — **as illustrated by the FCA's own worked example**, a raw ~£300 ethnicity-linked premium differential shrinking to a £28 residual on a £627 premium once claims costs and other risk factors are taken into account (the figures are that worked example, not a population-wide result). The finding does not concern inertia pricing directly (it concerns a different, protected-characteristic-linked differential), but it is directly relevant as a caution: a price differential that looks untethered from risk at first inspection can substantially collapse once genuine cost/risk factors are properly controlled for, and the FCA states it "did not have access to the full algorithms or set of risk factors used by insurers" even in reaching that residual. This does not weaken the loyalty-penalty finding itself — MS18/1.3 and PS21/5 quantified and remediated an identified, admitted mechanism, not an inferred one — but it should temper any assumption that every observed pricing differential in AI-influenced pricing is elasticity-driven rather than risk-based, reinforcing why this claim's own control (price decomposition testing) is the correct response, not an assumption in either direction.
>
> **[FAIAS Incident Register, row 41, "Allstate retention pricing", 2021]** — a supervisor's own actuary concluded that the insurer had selected smaller discounts, or higher rate relativities, than were actuarially indicated for classes of policyholders it understood to be price-insensitive — accident- and violation-free drivers continuously insured with it for seven or more years, holders of multiple other policies with it, and drivers with at least 39 years' driving experience — so that "the final rates that Allstate charged these policyholders were actuarially unsound and unfairly discriminatory", and the intervenor's actuary recorded, of the first two of those classes, that those policyholders "were known by Allstate to have a lower elasticity of demand and were more likely to renew with Allstate even though they were charged premiums in excess of those based upon an actuarially sound estimate of the cost of risk transfer"; a separate customer-retention model that Allstate proposed in other states was rejected, withdrawn or removed in several of them and approved in others [California Department of Insurance (Cimini) and Consumer Watchdog (Schwartz), 2021, pre-filed direct testimony of Edward Cimini Jr. and of Allan I. Schwartz, both signed 22 October 2021 (public versions served 25 and 28 October 2021), in the proceeding In the Matter of the Rating Practices of Allstate Insurance Company and Allstate Indemnity Company (File No. NC-2018-00001) before the Insurance Commissioner of the State of California, brought by the California Department of Insurance's Rate Enforcement Bureau with Allstate as respondent; The Markup, 2020, "Suckers List: How Allstate's Secret Auto Insurance Algorithm Squeezes Big Spenders", 25 February 2020, and 2022, "Newly Public Documents Allege Allstate Overcharged Loyal California Customers $1 billion", 1 February 2022]. This is expert testimony filed in that proceeding — the Department's actuary for the Department, the intervenor's for Consumer Watchdog — together with reported regulatory rejections, withdrawals and removals of a related model in other states, not an adjudicated finding, the insurer denying the allegations as reported, and the sources do not establish the pricing mechanism as machine learning.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)
>
> **URO-4: Huang & Hooker, "Fairness Testing for Algorithmic Pricing", arXiv:2605.11614v1, 12 May 2026 — whether §11's decomposition test is the right instrument, given the paper holds standard OLS pricing-fairness audits invalid for deterministic pricing output and supplies a corrected estimator — resolve by 2027-03-11.** The ★ above stands untouched while this observation is open (§6A.2).

## 19. Related IRQs
```
Related IRQs:
  - IRQ-CON-005 (H.2 Access & Exclusion: exclusion via pricing rather than eligibility)
  - IRQ-GOV-006 (I.2 Approval, Tiering & Policy: board risk appetite extension to pricing fairness)
  - IRQ-CON-008 (H.3 Transparency: disclosure of AI's role in pricing)
  - IRQ-CON-010 (H.2 Customer Outcomes, Vulnerability & Access:
    whether the system's own journey design engineers the inertia
    this IRQ prices to, as distinct from pricing to it)
```

## 20. References
```
[1] Financial Conduct Authority, 2022. "PS22/9 — A new Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publications/policy-statements/ps22-9-new-consumer-duty

[2] Financial Conduct Authority, 2021. "PS21/5 — General insurance pricing practices: Feedback to CP20/19 and final rules."
    Published: May 2021
    URL: https://www.fca.org.uk/publication/policy/ps21-5.pdf

[3] California Department of Insurance and Consumer Watchdog, 2021. Pre-filed direct testimony of Edward Cimini Jr., for the Department, and of Allan I. Schwartz, for the intervenor Consumer Watchdog, both signed 22 October 2021 (public redacted versions served 25 and 28 October 2021), in In the Matter of the Rating Practices of Allstate Insurance Company and Allstate Indemnity Company, File No. NC-2018-00001, before the Insurance Commissioner of the State of California. Expert testimony filed in that proceeding; not an adjudicated finding. Read at the documents as The Markup published them (Cimini, pp.7–8, repeated at p.10 and ¶34; Schwartz, pp.37–38).
    URL: https://www.documentcloud.org/documents/21185966-2021-10-25-final-pdt-of-edward-cimini-jr
    URL: https://www.documentcloud.org/documents/21185965-2021-10-28-pre-filed-direct-testimony-of-allan-i-schwartz

[4] The Markup, 2020 and 2022. "Suckers List: How Allstate's Secret Auto Insurance Algorithm Squeezes Big Spenders" (25 February 2020) and "Newly Public Documents Allege Allstate Overcharged Loyal California Customers $1 billion" (1 February 2022).
    URL: https://themarkup.org/allstates-algorithm/2020/02/25/car-insurance-suckers-list
    URL: https://themarkup.org/allstates-algorithm/2022/02/01/newly-public-documents-allege-allstate-overcharged-loyal-california-customers-1-billion
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.2 (Conduct & Fairness domain, Customer Outcomes, Vulnerability & Access)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Pricing/actuarial SMEs may believe the general insurance pricing remedy already "solved" loyalty-penalty pricing, missing its reconstruction via granular AI-driven elasticity pricing.
✓ Test 2 (Plausible Harm): Grounded directly in the FCA's PS21/5 general insurance pricing intervention and Consumer Duty price-and-value outcome.
✓ Test 3 (Testable): Answerable via price decomposition/ablation testing in a non-production environment.
✓ Test 4 (Decision-Relevant): Outcome gates whether AI-influenced pricing can be relied upon as genuinely risk/cost-based.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Field 18 — URO-4 opened on Huang & Hooker, "Fairness Testing for Algorithmic Pricing" (arXiv:2605.11614v1, 12 May 2026): whether field 11's decomposition test is the right instrument, given the paper holds standard OLS pricing-fairness audits invalid for deterministic pricing output and supplies a corrected estimator; resolve by 2027-03-11, the ★ standing untouched while the observation is open (§6A.2). Field 19 — IRQ-CON-010 added as the reciprocal cross-reference (whether the system's own journey design engineers the inertia this IRQ prices to, as distinct from pricing to it). ★2 unchanged.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form (row 41), labelled on its face as pre-filed expert testimony in the Department's proceeding on Allstate's rating practices and other states' reported decisions on a separate retention model rather than an adjudicated finding, with the insurer's denial recorded as reported, quoting the testimony at the documents themselves, and carrying the caveat that the sources do not establish the pricing mechanism as machine learning; reference entries [3] and [4] added at Field 20. Research-basis review date moved. ★2 unchanged; URO-4 remains open.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

