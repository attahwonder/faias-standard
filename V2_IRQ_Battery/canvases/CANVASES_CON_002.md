# CANVAS: IRQ-CON-002

## 1. IRQ ID & Title
**IRQ-CON-002: Undetected Proxy Discrimination via Facially Neutral Features**

Register question: "Could facially neutral features act as proxies for protected characteristics (postcode, device, shopping patterns), and has proxy analysis been performed?"

## 2. Business Activities Affected
- **Credit and insurance pricing:** Postcode, device type, browsing/shopping pattern or even typing cadence can correlate strongly with protected characteristics (ethnicity, age, disability), producing discriminatory outcomes despite no protected attribute being a direct model input.
- **Fraud screening:** Behavioural or device-based features used for fraud risk scoring may disproportionately flag customers from certain demographic groups if those features correlate with protected characteristics via historical patterns (e.g. shared devices in lower-income households).
- **Marketing and product eligibility targeting:** Facially neutral targeting features may systematically exclude or deprioritise protected groups from beneficial product offers.

## 3. AI Behaviour(s)
- Ingests a wide feature set that may include geographic, device, behavioural or transactional variables not obviously linked to protected characteristics, and learns statistical associations between these features and outcomes.
- Assigns predictive weight to a feature based on its correlation with the target outcome in historical data, without regard to whether that correlation is itself a proxy for a protected characteristic.
- Can combine several individually weak proxy signals (e.g. postcode + device + spending category) into a strong composite proxy for a protected characteristic, even where each individual feature's correlation is unremarkable.

## 4. Failure Mode
> The system relies on one or more facially neutral features that function as a statistical proxy for a protected characteristic, producing discriminatory outcomes that would not be detected by a review focused only on whether protected characteristics are directly used as model inputs.

## 5. Potential Consequences
- **Customer:** A customer is disadvantaged (declined, priced worse, flagged) because of a correlate of their protected characteristic (e.g. postcode correlating with ethnicity), without any transparent basis to challenge the specific reason.
- **Institution:** Equality Act 2010 indirect discrimination liability even absent intent; regulatory finding that "we don't use protected characteristics" was an inadequate fairness control.
- **Market/Regulator:** Reputational and enforcement risk once a proxy pattern is identified, particularly where the firm previously asserted the model was "characteristic-blind" as its fairness control.

## 6. Failure Chain
```
Wide feature set includes geographic, device, behavioural variables
correlated (via historical/societal pattern) with protected
characteristics
  ↓ (IRQ-DAT-001: training data provenance does not flag
     proxy-correlated features for review)
Model assigns predictive weight to proxy features because they
improve target-metric performance in historical data
  ↓ (IRQ-CON-002 — THIS IRQ: no proxy-variable analysis performed;
     "no protected characteristics used" wrongly treated as sufficient)
Model produces outcome disparity correlated with protected
characteristics via the proxy pathway
  ↓ (IRQ-CON-001: subgroup/intersectional testing, if absent, fails
     to surface the resulting disparity)
Pattern surfaces via external complaint, investigative journalism,
or regulatory thematic review

Control Breakpoints:
  • IRQ-CON-002: proxy-variable analysis performed on the full feature
    set, not only direct protected-characteristic screening
  • IRQ-DAT-001: feature provenance and correlation review flags
    candidate proxy variables at data-ingestion stage
  • IRQ-CON-001: subgroup/intersectional outcome testing catches
    resulting disparity even if the proxy mechanism itself is missed
```

## 7. Why a Domain Expert May Miss It
- The single most common (and insufficient) fairness assurance statement in traditional model governance is "the model does not use protected characteristics" — this is necessary but not remotely sufficient, and a domain expert without AI fairness literacy may accept it as conclusive.
- Proxy effects can arise from combinations of features that are each individually innocuous; a feature-by-feature review that checks each variable against an obvious protected-characteristic list will miss composite/interaction-driven proxies.
- Geographic features (postcode, branch catchment) are deeply embedded in UK financial services risk models for legitimate reasons (e.g. flood risk, local economic conditions); a domain expert may reflexively defend postcode's inclusion without separately testing whether it is also functioning as an ethnicity or deprivation proxy in this specific model.
- Proxy strength can change over time as population demographics and geographic settlement patterns shift, meaning a proxy analysis performed once at model build may become stale without a domain expert recognising the need for periodic re-testing.

## 8. Assurance Objective
**AO-CON-002:** The system's full feature set shall be analysed for proxy correlation with protected characteristics, individually and in combination, with material proxy risk documented and formally accepted or remediated.

## 9. Expected Controls (Traced)
- **Proxy-variable correlation analysis** — [Equality Act 2010, s.19, indirect discrimination; applies regardless of whether disadvantage arises from direct or proxy use of a protected characteristic] — the full feature set is tested for correlation with protected characteristics, not only direct inclusion.
- **Feature provenance and correlation review at data stage** — [linked IRQ-DAT-001] — candidate proxy variables (geography, device, behavioural pattern) are flagged for review before model training.
- **Composite/interaction proxy testing** — [research-grounded approaches to redundant encoding of protected attributes — an earlier citation here to "Fu, Aliferis et al." was unlocatable and removed 26 Aug 2026] — Emerging Practice; testing for combinations of individually weak features that jointly encode a protected characteristic is less standardised than single-feature correlation testing.
- **Periodic re-testing of proxy strength** — [linked IRQ-GOV-007 validation governance] — Emerging Practice; proxy correlation can drift as demographic and geographic patterns shift, requiring re-testing beyond a one-off model-build exercise.
- **Consumer Duty outcomes monitoring** — [FCA, FG22/5, July 2022] — outcome-level monitoring can surface proxy-driven disparity even where the proxy mechanism itself is not directly analysed.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the model does not use protected characteristics" with no proxy analysis performed — **L1**.
- Feature dictionary documenting all model inputs with a flag for candidate proxy variables (geography, device, behavioural) — **L2**.
- Non-production correlation analysis: statistical association between each flagged feature (and key feature combinations) and protected characteristics, measured on a held-out or synthetic representative dataset — **L3**.
- Independent model risk or internal audit review confirming proxy analysis was performed to a defined methodology and findings were escalated — **L4**.
- Production monitoring data showing outcome disparity correlated with a known or newly identified proxy variable, with remediation action taken — **L5**.

## 11. Independent Test
> On a non-production dataset with protected-characteristic labels available for testing purposes only (synthetic or held-out, never used in the production model), compute correlation between each model input feature (and a defined set of plausible feature combinations, e.g. postcode + device type) and each protected characteristic. Flag any feature or combination exceeding a documented correlation threshold for further review, and assess whether that feature materially drives model output (e.g. via feature-importance or ablation analysis). No production customer data or live decisioning system is used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (proxy discrimination as a general phenomenon is well documented in research; a standardised, benchmarked FS methodology for composite/interaction proxy testing does not exist, so test design and threshold-setting rely heavily on professional judgement).

## 12. Pass Indicators
- Full feature set, including combinations, has been tested for correlation with protected characteristics, not only individually.
- Any feature or combination found to be a material proxy has documented business justification, mitigation (e.g. removal, transformation) or formally accepted residual risk.
- Proxy testing has been repeated since model build (not a one-off historical exercise) given the risk of drift.
- Outcome-level monitoring is in place as a backstop to catch proxy-driven disparity even where the specific proxy mechanism was not identified.

## 13. Fail Indicators
- The only fairness assurance offered is "protected characteristics are not used as inputs", with no proxy correlation analysis performed.
- A feature or combination is later found to be a strong proxy with no prior analysis, business justification or mitigation on record.
- Proxy analysis, if performed, was a one-off exercise at model build with no periodic re-testing despite years of subsequent operation.
- No outcome-level monitoring exists to catch proxy-driven disparity as a backstop.

## 14. Reporting Language
**Pass:** "Proxy-variable correlation analysis has been performed on the full feature set, including composite combinations, with no material unmitigated proxy risk identified; outcome monitoring provides a backstop. Conclusions rest on ★2 methodology — research-grounded but bespoke, professional-judgement-dominant — and should be read as a point-in-time professional assessment, not a certified guarantee of proxy-freedom."

**Fail:** "No proxy-variable analysis has been performed; the firm's fairness assurance rests solely on the assertion that protected characteristics are not directly used as model inputs. This is an inadequate control: proxy discrimination via geography, device or behavioural features can and does produce disparate outcomes without any protected characteristic being a direct input."

**Partial:** "Individual feature proxy correlation has been tested and no material single-feature proxy was found, but composite/interaction combinations (e.g. postcode plus device type) have not been assessed. Remediation should extend the testing methodology to feature combinations before proxy-freedom can be relied upon."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (indirect discrimination exposure; disparate customer outcomes via an opaque mechanism)
  Likelihood: 2 (foreseeable where genuine feature diversity exists, e.g. geographic/behavioural data; mitigated by active proxy testing)
  Detectability: 3 (proxy mechanisms are inherently harder to detect than direct protected-characteristic use; requires deliberate statistical testing)
  Recoverability: 3 (remediable via feature removal/transformation and retraining within weeks to months)
  Novelty: 4 (proxy discrimination via composite/interaction features is a genuinely AI-specific concept largely outside traditional model governance)

If controls are absent or degraded:
  Severity: 4 (systemic indirect discrimination; regulatory enforcement and reputational risk, compounded by the firm's prior "characteristic-blind" assurance claim looking actively misleading in hindsight)
  Likelihood: 3 (probable given the prevalence of geographic and behavioural features in FS risk models and their known correlation with protected characteristics)
  Detectability: 4 (silent failure; typically surfaces only via external investigation or complaint, long after harm accrued)
  Recoverability: 3 (multi-month remediation including feature re-engineering, retraining and cohort redress assessment)
  Novelty: 4 (domain expert very likely to treat "no direct protected characteristic used" as sufficient assurance)

Residual risk interpretation: High priority given the combination of high severity, poor detectability, and the specific danger that this failure mode is actively masked by an intuitively plausible but insufficient existing control ("we don't use protected characteristics").
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Indirect discrimination exposure via an opaque, hard-to-challenge mechanism |
| **Likelihood** | 2 | Foreseeable given prevalence of geographic/behavioural features in FS models; mitigated where active proxy testing exists |
| **Detectability** | 3 | Requires deliberate statistical correlation testing; not surfaced by standard "protected characteristics not used" review |
| **Recoverability** | 3 | Remediable via feature removal/transformation and retraining within weeks to months |
| **Novelty** | 4 | Composite/interaction proxy discrimination is outside traditional model governance's single-feature review approach |

## 17. Regulatory Basis
> [Equality Act 2010, s.19, indirect discrimination provisions] applies to disadvantage arising from a facially neutral practice or criterion, regardless of whether a protected characteristic is directly used, and functionally covers proxy-driven disparate impact (indirect discrimination, s.19). [FCA, FG22/5, July 2022, "Final non-Handbook Guidance for firms on the Consumer Duty"] requires firms to monitor outcomes for groups of customers, providing an outcome-level backstop where proxy mechanisms are not independently identified.

## 18. Research Basis
> [Kleinberg, Mullainathan & Raghavan, 2016 — cited fully in IRQ-CON-001] establishes the broader fairness-metric context within which proxy analysis sits. [Prince & Schwarcz, 2020, "Proxy Discrimination in the Age of Artificial Intelligence and Big Data", Iowa Law Review] directly addresses the legal and technical mechanics of algorithmic proxy discrimination in a financial services-adjacent context. [Datta, Sen & Zick, 2016, "Algorithmic Transparency via Quantitative Input Influence: Theory and Experiments with Learning Systems", IEEE S&P] provides a feature-influence methodology relevant to detecting whether a flagged proxy variable materially drives model output. [UNVERIFIED — no published FS-specific incident report documenting a *confirmed* (as opposed to alleged/investigated-and-cleared) proxy discrimination finding, distinct from Apple Card, was located after search] (verified 29 Jul 2026).
>
> **Estimator-validity addition (v1.2.0) — the standard proxy-discrimination test is the wrong test.** [Huang, F., Hooker, G., 2026, "Fairness Testing for Algorithmic Pricing", arXiv:2605.11614, 12 May 2026, stat.AP] shows that the standard audit — regressing pricing output on a protected attribute and legitimate rating factors, then testing the coefficient with ordinary least squares standard errors — is structurally invalid for an algorithmic system: "Pricing algorithms are usually deterministic, so residuals reflect approximation error rather than sampling variability, rendering classical standard errors invalid in both direction and magnitude." The paper derives correct asymptotic variance estimators and, directly to the point of this IRQ, "the correct cross-covariance formula for proxy discrimination testing". Applied to quoted premiums from 34 Illinois auto insurers: "The standard proxy discrimination formula flags zero insurers. However, our corrected formula identifies all 34 as statistically significant, of which 16 exceed the substantive threshold." **Why it matters to this canvas specifically:** the paper bears on the proxy-variable correlation analysis in §9 and the correlation/ablation design in §11 **wherever a firm implements proxy testing as a regression audit with significance testing, which §11 does not itself prescribe** — §11 prescribes a documented correlation threshold and a feature-importance or ablation assessment, not a significance test. Where a firm does run the regression-and-significance form, a "no material proxy found" conclusion reached on classical standard errors may be an artefact of the estimator rather than a finding about the model. **Limits, stated:** a single v1 preprint, not peer-reviewed; US auto insurance quoted premiums, not a UK financial-services setting; and it is an empirical audit study, **not** an incident report — it therefore **narrows but does not clear** the `[UNVERIFIED — no published FS-specific incident report documenting a *confirmed* … proxy discrimination finding]` record above, whose wording is a separate open question. ★2 is unchanged by this addition.
>
> **[FAIAS Incident Register, row 56, "In the matter of Earnest Operations LLC", 2025]** — the Assurance of Discontinuance agreed between a state Attorney General and a student-loan lender alleges that the underwriting model's use of a school-level Cohort Default Rate subscore "resulted in disparate impact in approval rates and loan terms" (para 41) and that the lender "failed to conduct disparate impact testing on the effect of certain Weighted Inputs" (para 58(e)). A facially neutral, institution-level input is alleged to have acted as a proxy for a protected characteristic. These are the Attorney General's allegations, which the lender denies and does not admit (para 7), and not a confirmed finding: the incident narrows and does not clear the unverified record above, which asks for a confirmed finding.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-CON-001 (H.1 Discrimination & Proxy Bias: subgroup/intersectional outcome testing as a backstop)
  - IRQ-DAT-001 (A.1 Training Data Provenance: feature provenance review flags candidate proxies)
  - IRQ-GOV-007 (I.3 Validation Governance: periodic re-testing of proxy strength over time)
```

## 20. References
```
[1] Equality Act 2010. Section 19, Indirect Discrimination.
    URL: https://www.legislation.gov.uk/ukpga/2010/15/section/19

[2] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf

[3] Prince, A.E.R. & Schwarcz, D., 2020. "Proxy Discrimination in the Age of Artificial Intelligence and Big Data." Iowa Law Review, Vol. 105.
    URL: https://ilr.law.uiowa.edu/print/volume-105-issue-3/proxy-discrimination-in-the-age-of-artificial-intelligence-and-big-data/

[4] Datta, A., Sen, S. & Zick, Y., 2016. "Algorithmic Transparency via Quantitative Input Influence: Theory and Experiments with Learning Systems." IEEE Symposium on Security and Privacy 2016.
    URL: https://ieeexplore.ieee.org/document/7546525
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.1 (Conduct & Fairness domain, Discrimination & Proxy Bias)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): "The model doesn't use protected characteristics" is commonly and wrongly treated as sufficient fairness assurance by non-AI-specialist reviewers.
✓ Test 2 (Plausible Harm): Grounded in Prince & Schwarcz (2020) and the Equality Act's functional coverage of proxy-driven indirect discrimination (s.19).
✓ Test 3 (Testable): Answerable via statistical correlation and feature-influence testing on a held-out dataset with protected-characteristic labels.
✓ Test 4 (Decision-Relevant): Outcome gates whether "characteristic-blind" design can be relied upon as a fairness control.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Field 18 — Huang & Hooker, "Fairness Testing for Algorithmic Pricing" (arXiv:2605.11614, 12 May 2026) added as the primary home for the corrected cross-covariance formula for proxy-discrimination testing, with the finding that classical OLS standard errors are invalid for deterministic pricing output (standard formula flags zero of 34 Illinois insurers; the corrected formula flags all 34, 16 above the substantive threshold). Re-targeted here from IRQ-CON-006 on the adopted routing correction. Narrows but does not clear the UNVERIFIED no-confirmed-FS-incident record; that wording is held. ★2 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 — wording only: a pending question is now recorded as an open question. Research Basis unchanged; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 56, In the matter of Earnest Operations LLC, carried as the Attorney General's allegations, which the lender denies, and not as a confirmed finding), so the unverified record in the field is narrowed and not cleared. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within weeks to months, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. The other axes, the ★ rating and the research basis are unchanged.
- v1.3.3 (2026-10-09): Fields 17 and 18 — the FCA finalised guidance FG22/5 is cited under its issued title, "Final non-Handbook Guidance for firms on the Consumer Duty", in place of a description set in quotation marks. The Datta, Sen and Zick paper takes its full title, with the subtitle "Theory and Experiments with Learning Systems". Form corrections only. No change to the ★ rating or the risk profile.
```

---
---

