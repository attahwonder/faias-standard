# CANVAS: IRQ-CON-001

## 1. IRQ ID & Title
**IRQ-CON-001: Undetected Subgroup and Intersectional Outcome Disparity in AI-Influenced Decisions**

Register question: "Do outcome distributions differ materially across protected and vulnerable groups, tested at subgroup and intersectional level with fairness metrics and thresholds that were fixed and recorded before results were seen — and is any post-hoc selection or substitution of a fairness metric itself documented and treated as a finding?"

## 2. Business Activities Affected
- **Credit and underwriting decisioning:** AI-assisted approval, limit-setting or pricing decisions may produce materially different approval rates or terms across protected characteristics (age, sex, ethnicity, disability) or intersections thereof (e.g. older women in a specific postcode band), without this being visible in single-attribute analysis alone.
- **Insurance underwriting and claims:** AI-assisted risk scoring or claims triage may systematically disadvantage a protected or intersectional subgroup even where no single protected attribute is used as an input.
- **Fraud and financial crime screening:** AI-assisted alerting may generate disproportionately higher false-positive rates for certain ethnic or national-origin groups, causing disproportionate friction or account restriction.

## 3. AI Behaviour(s)
- Learns statistical patterns from historical outcome data that may itself encode past discriminatory practice or societal disparity, then reproduces or amplifies that pattern in new decisions.
- Produces outcome distributions (approval rates, scores, pricing, alert rates) that can be measured in aggregate but are rarely disaggregated to subgroup or intersectional level in routine model monitoring.
- Optimises for an overall accuracy or profitability metric that can be satisfied while producing systematically worse outcomes for a numerically small intersectional subgroup, without materially affecting the aggregate metric the model was tuned against.

## 4. Failure Mode
> The system produces materially different outcome distributions for a protected or intersectional subgroup relative to the wider population, and this disparity goes undetected because fairness testing, where it exists, is conducted only at single-attribute level or on the aggregate population, not at the subgroup and intersectional level where the harm actually concentrates.

## 5. Potential Consequences
- **Customer:** Members of a protected or intersectional subgroup are systematically declined, priced worse, or flagged more often, without individual recourse because no single decision looks anomalous in isolation.
- **Institution:** Equality Act 2010 indirect discrimination claim; FCA Consumer Duty fair-value and fair-treatment breach finding; remediation costs across an entire affected cohort once the pattern is identified.
- **Market/Regulator:** Regulatory finding of systemic unfair treatment; reputational damage disproportionate to any single decision, because the harm is patterned and cohort-wide once discovered.

## 6. Failure Chain
```
Historical outcome data reflects past societal or institutional
disparity (e.g. differential historical approval rates)
  ↓ (IRQ-DAT-005: training/reference data representativeness gap)
Model learns and reproduces the disparity pattern in new decisions
  ↓ (IRQ-CON-001 — THIS IRQ: fairness testing, if it exists, is
     conducted only at aggregate/single-attribute level)
Subgroup/intersectional disparity persists undetected in production
  ↓ (IRQ-GOV-007: validation governance does not mandate
     intersectional fairness testing as a release gate)
Pattern surfaces only via external complaint, journalist investigation,
or regulatory thematic review — long after cohort-wide harm accrued
  ↓
Equality Act / Consumer Duty finding; cohort-wide remediation exercise

Control Breakpoints:
  • IRQ-CON-001: subgroup and intersectional fairness metrics tested
    pre-deployment and periodically in production
  • IRQ-DAT-005: representativeness gap identified and documented
    before it can propagate into model behaviour
  • IRQ-GOV-007: validation governance mandates intersectional testing
    as a release and periodic-revalidation gate
```

## 7. Why a Domain Expert May Miss It
- Traditional fair-lending or underwriting review typically checks disparate impact on single protected characteristics (e.g. sex alone, ethnicity alone); intersectional harm (e.g. disabled women over 60) can be statistically invisible in single-attribute analysis while being severe for the intersectional cohort.
- "The model doesn't use protected characteristics as an input" is frequently treated as sufficient evidence of fairness by non-AI-specialist reviewers, when proxy effects and non-linear interactions can reproduce disparate outcomes without any protected attribute being directly used (see CON-002).
- Aggregate accuracy or approval-rate parity across large groups can mask severe disparity in a numerically small intersectional subgroup, because that subgroup's outcomes barely move the aggregate metric.
- Fairness-metric selection itself requires a value judgement (e.g. demographic parity vs equalised odds vs calibration — these are mathematically incompatible in general, per Kleinberg et al.'s impossibility result); a domain expert without AI fairness literacy may not realise "we tested fairness" can mean materially different things depending on which metric was chosen.

## 8. Assurance Objective
**AO-CON-001:** The AI system's outcome distributions shall be tested at subgroup and intersectional level against fairness metrics and thresholds that are fixed and recorded before results are seen, with material disparities documented and formally accepted or remediated before and during deployment. The same applies to the error rates, for each subgroup, of any perception component (identity verification, liveness checking, voice authentication or speech transcription) upstream of a customer outcome. Any post-hoc selection or substitution of a fairness metric after results are seen is itself a control failure, regardless of what the substituted metric shows.

## 9. Expected Controls (Traced)
- **Subgroup and intersectional outcome testing** — [Equality Act 2010, indirect discrimination provisions, s.19] — outcome distributions are disaggregated below single-attribute level to detect intersectional disparity.
- **Fairness metric selection and justification** — [Kleinberg, Mullainathan & Raghavan, 2016, "Inherent Trade-Offs in the Fair Determination of Risk Scores"] — Emerging Practice; the firm documents which fairness definition (demographic parity, equalised odds, calibration) was selected and why, given that these are provably incompatible in general.
- **Consumer Duty fair-treatment monitoring** — [FCA, PS22/9, July 2022, and FG22/5, July 2022, "Final non-Handbook Guidance for firms on the Consumer Duty"] — outcomes monitoring extends to AI-influenced decisions specifically, not only manual processes.
- **Model validation governance gating on fairness testing** — [linked IRQ-GOV-007] — release and periodic revalidation are conditioned on subgroup/intersectional fairness evidence, not aggregate accuracy alone.
- **MAS FEAT principles (fairness, ethics, accountability, transparency)** — [Monetary Authority of Singapore, "FEAT Principles", 2018, and Veritas Initiative toolkit] — cited as an internationally recognised fairness-assessment framework; [UNVERIFIED — no FCA/PRA domestic requirement equivalent to FEAT's named fairness-assessment methodology was located; Consumer Duty (PRIN 2A: the cross-cutting obligations, PRIN 2A.2, and the four retail customer outcomes, PRIN 2A.3 to 2A.6) remains the only confirmed domestic anchor] (verified 29 Jul 2026; PRIN 2A provisions checked against the Handbook on 8 Oct 2026).

## 10. Expected Evidence (Tagged L1–L5)
- Policy statement asserting "the model is regularly tested for fairness" without metric or subgroup detail — **L1**.
- Fairness testing methodology document specifying which metrics, which subgroups (including intersectional combinations), and acceptance thresholds — **L2**.
- Dated record of the fairness metric(s) and threshold(s) fixed before subgroup/intersectional test execution — evidence format not prescribed, but the record must predate results — **L2**.
- Non-production test results: subgroup and intersectional outcome distributions measured on a held-out or synthetic representative dataset against the documented metrics — **L3**.
- Independent model risk or internal audit report confirming intersectional fairness testing was performed as designed and findings were escalated appropriately — **L4**.
- Production monitoring data (e.g. quarterly): subgroup/intersectional outcome distributions tracked over time, with any material drift flagged and investigated — **L5**.

## 11. Independent Test
> On a non-production, held-out dataset constructed to be representative of the deployed population (or, where representativeness cannot be confirmed, a clearly labelled synthetic proxy), compute outcome distributions (approval rate, average score, average price, or alert rate as applicable) disaggregated by each protected characteristic individually and by defined intersectional combinations (minimum: two-way intersections for the highest-volume protected characteristics). Compare against at least two fairness metrics (e.g. demographic parity and equalised odds) and document where they diverge. No production customer data or live decisioning system is used. Where an AI component performs identity verification, liveness checking, voice authentication or speech transcription upstream of a customer outcome, additionally compute subgroup-disaggregated error rates for that component: false match and false non-match rates for identity verification and voice authentication; for liveness checking, the rate at which presentation attacks are missed and the rate at which genuine presentations are wrongly rejected (the APCER and BPCER of NISTIR 8280's Figure 1); word error rate for speech transcription. Where the component applies a decision threshold, compute both error rates at the threshold configured for deployment and report them for each subgroup at that single threshold rather than as an aggregate, as a single error type or at another threshold; report word error rate for each subgroup rather than as an aggregate. Where no subgroup-labelled evaluation set in the component's modality is available, the component is recorded as untestable and its error rates are not computed by the independent test; the Pass, Fail or Partial result is reached without that computation, and the untested component is reported beside that result as a coverage gap (Field 14). — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (subgroup fairness-metric testing draws on a substantial and increasingly consistent body of published research; no single agreed FS benchmark or regulator-mandated test suite exists, so professional judgement governs metric selection and threshold-setting).

## 12. Pass Indicators
- Fairness testing is conducted at subgroup and intersectional level, not only aggregate/single-attribute level.
- Chosen fairness metric(s) are documented and justified given the known trade-offs between metrics.
- No material, unexplained disparity is found for any tested subgroup or intersectional combination; where disparity exists, a documented and formally accepted business justification exists.
- Production monitoring shows subgroup/intersectional outcome tracking is active, not a one-off pre-deployment exercise.
- Where a perception component — identity verification, liveness checking, voice authentication or speech transcription — sits upstream of a customer outcome, the firm's own testing reports its error rates for each subgroup — both error types at the threshold configured for deployment where the component applies one, word error rate for speech transcription — and the independent test finds no material unexplained disparity in them, or a documented and formally accepted justification exists where disparity is found. Where the component is recorded as untestable (Field 11), the limb on the independent test does not apply, and the gap is reported beside the result (Field 14).

## 13. Fail Indicators
- Fairness testing, where it exists, is conducted only at aggregate or single-attribute level; intersectional combinations are untested.
- Material outcome disparity is found for a protected or intersectional subgroup with no documented business justification or remediation plan.
- Only one fairness metric was tested with no documentation of why alternative metrics (which may show a different result) were not also considered.
- A fairness metric is selected, changed or substituted after subgroup/intersectional results have been seen; this fails on timing alone, whatever the eventually-chosen metric shows.
- No production monitoring exists to detect whether disparity has emerged or worsened since pre-deployment testing.
- For a perception component upstream of a customer outcome, the firm's own testing reports its error rates only in aggregate or, where the component applies a decision threshold, as a single error type or at a threshold other than the one configured for deployment, or does not report them.

## 14. Reporting Language
**Pass:** "Subgroup and intersectional fairness testing has been performed against justified metrics; no material unexplained disparity was found, and production monitoring confirms this remains the case. Conclusions rest on ★3 methodology — credible research-grounded, no agreed FS benchmark — and should be read as professional assessment."

**Fail:** "No subgroup or intersectional fairness testing exists beyond aggregate accuracy monitoring. This is a direct conduct risk: intersectional disparity, if present, would currently go undetected until surfaced by complaint or external review, at which point cohort-wide harm would already have accrued."

**Partial:** "Single-attribute fairness testing exists and shows no material disparity, but intersectional combinations (e.g. age × disability) have not been tested. Remediation should extend the existing testing methodology to intersectional level before this can be relied upon as comprehensive fairness assurance."

**Untested perception component (stated beside the result, in the report and in the opinion):** "The [identity verification / liveness checking / voice authentication / speech transcription] component upstream of [customer outcome] could not be tested independently for disparity in its error rates between subgroups, because no subgroup-labelled evaluation set in its modality was available; the result above does not cover those error rates beyond the firm's own testing of them. A disparity there, if present, would not show in balanced outcome distributions downstream."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (cohort-wide unfair treatment; Equality Act and Consumer Duty exposure)
  Likelihood: 2 (foreseeable given known limitations of aggregate-only testing; not routine given genuine subgroup testing in place)
  Detectability: 2 (detectable via periodic subgroup monitoring; not real-time)
  Recoverability: 3 (remediable via targeted model adjustment and cohort remediation within weeks to months)
  Novelty: 3 (fairness-metric trade-offs and intersectional analysis are AI/statistics-specific knowledge beyond traditional fair-lending review)

If controls are absent or degraded:
  Severity: 4 (systemic, cohort-wide discriminatory outcome; material regulatory enforcement and reputational risk)
  Likelihood: 3 (probable given documented tendency of models to reproduce historical disparity absent explicit testing)
  Detectability: 4 (silent failure; typically surfaces only via external complaint, thematic review or journalist investigation, often years after deployment)
  Recoverability: 3 (multi-month remediation exercise across an entire affected cohort; potential redress scheme)
  Novelty: 4 (domain expert very likely to miss intersectional and proxy-driven disparity absent AI fairness literacy)

Residual risk interpretation: High priority given the combination of high severity, poor detectability absent explicit testing, and high novelty; this is a domain where "we didn't use protected characteristics" is commonly and wrongly treated as sufficient assurance.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Cohort-wide unfair treatment; Equality Act indirect discrimination and Consumer Duty fair-treatment exposure |
| **Likelihood** | 2 | Foreseeable given known tendency of models to reproduce historical disparity; not routine where genuine subgroup testing exists |
| **Detectability** | 3 | Aggregate-only monitoring will not surface subgroup/intersectional disparity; requires deliberate disaggregated testing to detect |
| **Recoverability** | 3 | Remediable via targeted model adjustment within weeks to months once identified |
| **Novelty** | 4 | Intersectional analysis and fairness-metric incompatibility (Kleinberg et al.) are outside traditional fair-lending review knowledge |

## 17. Regulatory Basis
> [Equality Act 2010, s.19, indirect discrimination provisions] prohibits practices that disadvantage a protected group without objective justification, and applies regardless of whether a protected characteristic is a direct model input. [FCA, PS22/9, July 2022, and FG22/5, July 2022, "Final non-Handbook Guidance for firms on the Consumer Duty"] requires firms to monitor for and act on evidence of poor outcomes for groups of customers, including those with characteristics of vulnerability, which extends to AI-influenced decisioning.

## 18. Research Basis
> [Kleinberg, Mullainathan & Raghavan, 2016, "Inherent Trade-Offs in the Fair Determination of Risk Scores", ITCS 2017] establishes that common fairness metrics (calibration, balance for positive/negative class) are mutually incompatible in general, with exactly two named exceptions in which the metrics coincide: perfect prediction, and equal base rates across the compared groups. Outside these two cases, "the model was tested for fairness" requires specifying which metric — and that specification must be fixed before results are seen (see the amended register question and AO-CON-001), since a metric chosen after the fact is chosen precisely because it passes. [Buolamwini & Gebru, 2018, "Gender Shades", FAT* 2018] documents severe intersectional accuracy disparity undetected by single-attribute analysis in a widely cited computer vision context, illustrating the general intersectional-blind-spot phenomenon relevant by analogy to FS scoring models. [Apple Card / NYDFS, 2019 incident, widely reported] — a credit-line-allocation algorithm was alleged to produce disparate outcomes by sex; NYDFS investigation found no direct evidence of intentional discrimination but highlighted the opacity and difficulty of proving/disproving algorithmic fairness claims after the fact, reinforcing the case for pre-emptive subgroup testing. [CONFIRMED — New York State Department of Financial Services, "Report on Apple Card Investigation," 23 March 2021, https://www.dfs.ny.gov/reports_and_publications/202103_report_apple_card_investigation — DFS found no evidence that Goldman Sachs' credit decisioning process used prohibited factors or resulted in unlawful discrimination under fair lending laws, while noting algorithmic decision-making creates challenges for regulators and consumers in identifying disparate impact] (verified 29 Jul 2026).
>
> **Pre-registered-metric addition (v1.2.0) — the estimator is part of the specification.** [Huang, F., Hooker, G., 2026, "Fairness Testing for Algorithmic Pricing", arXiv:2605.11614, 12 May 2026; the full treatment of this paper is held at IRQ-CON-002 Field 18] tests conditional demographic parity on quoted premiums from 34 Illinois auto insurers and reports that "every insurer fails the conditional demographic parity test, with minority zip codes paying $34-$158 more per year than comparable-risk white zip codes". Its bearing on *this* canvas is the pre-registration requirement in the amended register question: where a firm fixes a fairness metric and threshold before results are seen, the paper establishes that fixing the metric is not sufficient, because for a deterministic algorithmic system the *variance estimator* determines whether the threshold is ever crossed — "rendering classical standard errors invalid in both direction and magnitude". A reviewer should expect the pre-registered record to name the estimator and the significance procedure alongside the metric and the threshold, or post-hoc estimator choice reopens the selection risk this IRQ exists to close. **Limits, stated:** a single v1 preprint, not peer-reviewed; US auto insurance, not a UK financial-services setting. No ★ change arises.
>
> **Perception-component addition (v1.2.1) — the disparity sits in the error rate, not only in the outcome distribution.** [National Institute of Standards and Technology, 2019, "Face Recognition Vendor Test (FRVT) Part 3: Demographic Effects", NISTIR 8280, December 2019] measured 189 mostly commercial algorithms from 99 developers across 18.27 million images of 8.49 million people drawn from four operational US government photo datasets, and found that "false positives rates often vary by factors of 10 to beyond 100 times" across demographic groups, with false positives "higher in women than men, and this is consistent across algorithms and datasets" and elevated in the elderly and in children. It also records the reporting rule the differential turns on: because "most systems are configured with a fixed threshold, it is necessary to report both false negative and false positive rates for each demographic group at that threshold", which "is rarely done". [Koenecke, A., Nam, A., Lake, E., Nudell, J., Quartey, M., Mengesha, Z., Toups, C., Rickford, J. R., Jurafsky, D., Goel, S., 2020, "Racial disparities in automated speech recognition", Proceedings of the National Academy of Sciences 117(14), 7684–7689] found "an average word error rate (WER) of 0.35 for black speakers compared with 0.19 for white speakers" across five independently developed commercial systems, on a sample matched for age, gender and snippet duration. Both establish a disparity that outcome-distribution testing does not surface: where a component's function is perception rather than decision, the disparity sits in the error rate — at the deployed threshold where the component applies one — and a system whose outcome distributions are balanced may still misverify or mistranscribe one subgroup at several times the rate of another. Neither study is set in financial services; both are carried for the mechanism, which transfers wherever identity verification, liveness checking, voice authentication or speech transcription sits upstream of a customer outcome.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-DAT-005 (A.1 Training Data Provenance: representativeness gap upstream of disparity)
  - IRQ-CON-002 (H.1 Discrimination & Proxy Bias: proxy variables as a mechanism for undetected disparity)
  - IRQ-GOV-007 (I.3 Validation Governance: fairness testing as a release/revalidation gate)
  - IRQ-CON-005 (H.2 Access & Exclusion: disparity manifesting as financial exclusion)
  - IRQ-CON-006 (H.2 Price Fairness: disparity manifesting as differential pricing)
```

## 20. References
```
[1] Equality Act 2010. Section 19, Indirect Discrimination.
    URL: https://www.legislation.gov.uk/ukpga/2010/15/section/19

[2] Financial Conduct Authority, 2022. "PS22/9 — A new Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publications/policy-statements/ps22-9-new-consumer-duty

[3] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf

[4] Kleinberg, J., Mullainathan, S. & Raghavan, M., 2016. "Inherent Trade-Offs in the Fair Determination of Risk Scores." Innovations in Theoretical Computer Science (ITCS) 2017.
    URL: https://arxiv.org/abs/1609.05807

[5] Buolamwini, J. & Gebru, T., 2018. "Gender Shades: Intersectional Accuracy Disparities in Commercial Gender Classification." Conference on Fairness, Accountability and Transparency (FAT*) 2018.
    URL: http://proceedings.mlr.press/v81/buolamwini18a.html

[6] New York State Department of Financial Services, 2021. "Report on Apple Card Investigation." 23 March 2021. https://www.dfs.ny.gov/reports_and_publications/202103_report_apple_card_investigation (verified 29 Jul 2026).

[7] Monetary Authority of Singapore, 2018. "Principles to Promote Fairness, Ethics, Accountability and Transparency (FEAT) in the Use of Artificial Intelligence and Data Analytics."
    Published: November 2018
    URL: https://www.mas.gov.sg/-/media/MAS/News-and-Publications/Monographs-and-Information-Papers/FEAT-Principles-Final.pdf

[8] National Institute of Standards and Technology, 2019. "Face Recognition Vendor Test (FRVT) Part 3: Demographic Effects." NISTIR 8280.
    Published: December 2019
    URL: https://nvlpubs.nist.gov/nistpubs/ir/2019/NIST.IR.8280.pdf

[9] Koenecke, A., Nam, A., Lake, E., Nudell, J., Quartey, M., Mengesha, Z., Toups, C., Rickford, J. R., Jurafsky, D. & Goel, S., 2020. "Racial disparities in automated speech recognition." Proceedings of the National Academy of Sciences, 117(14), pp. 7684–7689.
    URL: https://www.pnas.org/doi/10.1073/pnas.1915768117
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.1 (Conduct & Fairness domain, Discrimination & Proxy Bias)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Traditional fair-lending review checks single-attribute disparate impact; intersectional and metric-choice blind spots are AI/statistics-specific.
✓ Test 2 (Plausible Harm): Grounded in Kleinberg et al. (2016), Buolamwini & Gebru (2018), and the Apple Card/NYDFS incident.
✓ Test 3 (Testable): Answerable via disaggregated subgroup/intersectional outcome testing on a held-out dataset.
✓ Test 4 (Decision-Relevant): Outcome gates deployment/continued operation pending demonstrated absence of material unexplained disparity.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.0.1 (2026-07-31): Pre-registration amendment — fairness metric(s) and threshold(s) must be fixed and recorded before subgroup/intersectional results are seen; post-hoc metric selection or substitution is itself a control failure, whatever the chosen metric shows. Kleinberg, Mullainathan & Raghavan (ITCS 2017) anchor restated with its two named exceptions (perfect prediction; equal base rates). Credit: the pre-registration insight originates in the standard programme's own retired research battery, which identified post-hoc fairness-metric selection as a distinctive risk before this amendment was drafted.
- v1.2.0 (2026-09-12): Field 18 — Huang & Hooker (arXiv:2605.11614) added as co-target to IRQ-CON-002, for the conditional-demographic-parity result (all 34 Illinois insurers fail, $34–$158 per year) and for the consequence that the pre-registered record must name the variance estimator and significance procedure alongside the metric and threshold, since for deterministic output the estimator determines whether the threshold is crossed. Full treatment of the paper is held at IRQ-CON-002 Field 18. ★3 unchanged.
- v1.2.1 (2026-09-19): Field 18 — NISTIR 8280 (2019) and Koenecke et al. (PNAS, 2020) added for the perception-component limb, with reference entries [8] and [9] added at Field 20. What NISTIR 8280 adds over the Gender Shades citation already carried: scale (189 algorithms, 99 developers, 18.27 million images), a national standards body as the source, recognition — one-to-one verification and one-to-many identification — where Gender Shades evaluated classification, and an explicit fixed-threshold reporting rule. The demographic evaluation is documented and published — NIST IR 8429, "Face Recognition Vendor Test (FRVT) Part 8: Summarizing Demographic Differentials", July 2022, listed on NIST's demographics page as "FRTE Part 8", with the demographic summary table last updated on 5 March 2025 — but adoption by two or more independent institutions is not established, so ★4's adoption limb ("adopted by ≥2 independent institutions", ASSURANCE_MODEL.md) is not met. Field 11 — subgroup-disaggregated error rates added for perception components, the measure stated per component type and the deployed-threshold rule confined to components that apply a decision threshold, the component recorded as untestable where no subgroup-labelled evaluation set is available; Fields 12 and 13 — one Pass and one Fail indicator added for that limb, the reporting subject of both named as the firm's own testing. Field 8 — the assurance objective names the same limb. Research-basis review date moved. ★3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 13 Fail Indicators — the perception-component indicator also covers the firm's own testing that does not report the component's error rates. ★3 unchanged; no change to the risk profile.
- v1.3.3 (2026-10-09): Fields 11, 12 and 14 — a perception component with no subgroup-labelled evaluation set in its modality no longer prevents a Pass. Field 11 reaches the Pass, Fail or Partial result without the independent computation of the component's error rates and reports the untested component beside that result as a coverage gap, in place of "a coverage gap, not a pass"; the Field 12 Pass indicator for the component does not apply its independent-test limb in that case; Field 14 adds reporting language for the gap, stated beside the result in the report and in the opinion. The grading of this case changes. ★3 unchanged; no change to the risk profile.
- v1.3.3 (2026-10-09): Field 9 Expected Controls — the MAS FEAT note names the Consumer Duty provisions that exist (PRIN 2A.2 and PRIN 2A.3 to 2A.6) in place of a "general fair-treatment outcome", which PRIN 2A does not contain; the note's date states what it covers. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within weeks to months, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. The other axes, the ★ rating and the research basis are unchanged.
- v1.3.3 (2026-10-09): Fields 9 and 17 — the FCA finalised guidance FG22/5 is cited under its issued title, "Final non-Handbook Guidance for firms on the Consumer Duty", in place of a description set in quotation marks. Form corrections only. No change to the ★ rating or the risk profile.
```

---
---

