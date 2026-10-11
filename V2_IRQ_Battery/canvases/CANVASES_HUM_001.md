# CANVAS: IRQ-HUM-001

## 1. IRQ ID & Title
**IRQ-HUM-001: Undetected Automation Bias in Human Review of AI Outputs**

Register question: "Do human reviewers detectably discriminate between correct and incorrect AI outputs, or does acceptance without challenge indicate automation bias — and are disagreement rates monitored?"

## 2. Business Activities Affected
- **Underwriting review:** Underwriters reviewing AI-recommended credit decisions may accept incorrect declines or approvals without independently re-deriving the outcome, particularly under volume pressure.
- **Claims approval:** Claims handlers reviewing AI-drafted liability or quantum assessments may rubber-stamp confidently-worded but wrong recommendations, especially where the AI output resembles prior correct outputs.
- **AML case handling:** Investigators reviewing AI-generated typology assessments or SAR-narrative drafts may accept a "no typology found" conclusion without independently checking evidence the model may have missed or misweighted.

## 3. AI Behaviour(s)
- Presents a recommendation or draft decision alongside supporting rationale, in a fluent, confident register regardless of underlying correctness.
- Produces outputs with no explicit or reliable signal distinguishing high-confidence-and-correct from high-confidence-and-wrong cases.
- Is placed in a workflow position where a human "reviews and confirms" the output as the final control step before the decision takes effect.

## 4. Failure Mode
> The human reviewer accepts the AI's recommendation without independently verifying it against source evidence, and this acceptance pattern is indistinguishable — in throughput and sign-off records — from genuine review, so the organisation cannot tell whether its human checkpoint is functioning or has become a formality.

## 5. Potential Consequences
- **Customer:** Incorrect credit decline, wrongly settled or under-settled claim, or missed AML typology reaches the customer or regulator with an apparently "human-approved" decision trail.
- **Institution:** FOS/regulatory findings that human sign-off was not a genuine control; SM&CR individual accountability exposure for the named approver; remediation cost across a batch of similarly-accepted decisions.
- **Market/regulator:** Erosion of confidence that "human in the loop" claims made in governance papers reflect real oversight, inviting closer supervisory scrutiny of AI-assisted decisioning generally.

## 6. Failure Chain
```
AI generates confident, fluent recommendation (correct or incorrect,
indistinguishable in presentation)
  ↓ (IRQ-MOD-006: confidence not calibrated to actual accuracy)
Reviewer workload/time pressure and no training in AI-specific challenge
behaviours
  ↓ (IRQ-HUM-001 — THIS IRQ: automation bias, acceptance without
     independent verification)
Reviewer signs off; disagreement-rate and error-detection metrics not
tracked, so bias is invisible to management
  ↓ (IRQ-HUM-002: sign-off may itself be approval theatre — throughput/
     dwell time never checked)
Incorrect decision proceeds as if human-reviewed
  ↓
Customer harm (decline, under-settlement, missed typology) →
complaint/SAR gap → regulatory finding of inadequate human oversight

Control Breakpoints:
  • IRQ-MOD-006: confidence calibration would give the reviewer a
    genuine risk signal to act on
  • IRQ-HUM-001: disagreement-rate monitoring surfaces bias before harm
    accumulates across a batch
  • IRQ-HUM-002: throughput/dwell-time analysis distinguishes genuine
    review from approval theatre
  • IRQ-GOV-003: technical enforcement of the review step (cannot be
    bypassed) versus a merely stated policy requirement
```

## 7. Why a Domain Expert May Miss It
- Assumption: "a human signature on the file means the decision was reviewed" — false when the signature reflects workflow compliance rather than independent judgement; traditional QA audits check that sign-off occurred, not whether it was substantive.
- Credit/claims/AML SMEs are trained to assess case-level correctness, not to design or interpret disagreement-rate statistics; this is a measurement-methodology gap, not a domain-knowledge gap.
- Automation bias is strongest precisely when the AI is usually right — the very success of the system erodes the reviewer's vigilance, a counter-intuitive dynamic well documented in aviation and clinical decision-support research but rarely part of banking QA training.
- Testing gap: conventional QA sampling checks outcome accuracy, not whether the human step added independent value over the AI output alone; without a counterfactual (would the reviewer have caught this error unaided?), automation bias is statistically invisible.

## 8. Assurance Objective
**AO-HUM-001:** Human reviewers of AI-assisted decisions shall demonstrably discriminate between correct and incorrect AI outputs at a measured rate, with disagreement and error-detection rates monitored on an ongoing basis to detect degradation into automation bias.

## 9. Expected Controls (Traced)
- **Disagreement-rate and override-rate monitoring** — [NIST AI RMF 1.0, MANAGE-4, Jan 2023] — track the rate at which human reviewers modify or reject AI recommendations over time; a rate approaching zero on a system with known non-zero error rate is itself a red flag.
- **Reviewer training on AI-specific challenge behaviours** — [Parasuraman & Riley, 1997, "Humans and Automation: Use, Misuse, Disuse, Abuse", Human Factors, 39(2)] — train reviewers explicitly on automation bias and complacency as a distinct failure mode from ordinary case error, per the foundational human-factors taxonomy.
- **Injected-error / seeded-case testing of reviewer detection rate** — [Skitka, Mosier & Burdick, 2000, "Accountability and automation bias", International Journal of Human-Computer Studies, 52(4)] — periodically insert known-incorrect AI outputs into the review stream (in test/staging) and measure catch rate.
- **EU AI Act Article 14 human oversight design requirement** — [EU AI Act, Regulation (EU) 2024/1689, Article 14, Aug 2024] — high-risk AI systems must be designed to enable effective human oversight, including the ability of the overseer to correctly interpret system output and decide not to use it.
- **FCA Consumer Duty outcome monitoring** — [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] — firms must monitor whether products and services deliver good customer outcomes, which extends to whether the human-AI review step actually protects customers from AI error.

## 10. Expected Evidence (Tagged L1–L5)
- Governance paper asserting "all AI recommendations are human-reviewed before action" — **L1**.
- Documented reviewer training curriculum covering automation bias and challenge expectations — **L2**.
- Design specification for disagreement-rate and error-detection dashboards — **L2**.
- Staging test results: seeded-error case set (e.g. 40 known-incorrect AI recommendations inserted into a review queue) with measured reviewer catch rate — **L3**.
- Independent HF/E-informed audit of reviewer challenge behaviour, using verified transcripts or case annotations — **L4**.
- Historical disagreement-rate and override-rate data from a comparable AI-assisted review deployment (internal or externally reported), trended over time — **L5**.

## 11. Independent Test
> In a non-production staging environment, construct a case set of historical (fully anonymised, dev/test) underwriting, claims or AML decisions with a known ground truth, seeded with a defined proportion (e.g. 15–20%) of deliberately incorrect AI recommendations that are individually plausible (fluent, well-reasoned, but wrong). Route the set through the normal human review workflow under realistic time constraints, blind to which cases are seeded. Measure: (1) the reviewer catch rate on seeded errors versus the AI's actual known error rate on the unseeded majority, (2) time-to-decision per case, and (3) whether catch rate correlates with dwell time or case complexity. Methodology follows the accountability/automation-bias seeded-error paradigm established in Skitka et al. (1999, 2000) and applied in Goddard, Roudsari & Wyatt's (2012) systematic review of automation bias in clinical decision support. Executed entirely on de-identified dev/test case files; no live customer decisions are affected. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, multi-decade human-factors research methodology with converging results across aviation, clinical and process-control domains; no single agreed FS-specific benchmark, so professional judgement is needed in case-set design and seeding ratio).

## 12. Pass Indicators
- Seeded-error catch rate meets or exceeds the firm's defined minimum threshold (e.g. ≥80% of seeded errors flagged or challenged).
- Disagreement/override rate in production is non-zero and stable or trending consistent with the AI system's known error profile, not suspiciously near zero.
- Catch rate does not degrade materially as case volume or time pressure increases within normal operating conditions.
- Reviewer training records show completion and periodic refresh on automation-bias-specific content, not generic AI-awareness training.
- Disagreement-rate monitoring is live in production and reviewed by a named accountable function on a defined cadence.

## 13. Fail Indicators
- Seeded-error catch rate is materially below threshold, or approaches zero — reviewers accept fluent-but-wrong outputs indiscriminately.
- Production disagreement/override rate is at or near zero despite a known non-zero AI error rate, and no one has investigated why.
- Catch rate collapses under realistic volume/time pressure, indicating the review step cannot function as designed at production throughput.
- No seeded-error or equivalent testing has ever been performed; reviewer effectiveness is asserted, not measured.
- Reviewer training exists only as a generic AI-literacy module with no automation-bias-specific content.

## 14. Reporting Language
**Pass:** "Seeded-error testing on de-identified dev/test case files shows human reviewers detect and challenge [X]% of deliberately incorrect AI recommendations, consistent with genuine independent review rather than acceptance without challenge. Production disagreement-rate monitoring is live and shows a rate consistent with the system's known error profile. This is a ★3 assessment — credible, multi-decade human-factors methodology, no FS-specific benchmark — and should be re-tested at each material model or workflow change."

**Fail:** "Seeded-error testing demonstrates reviewers accept fluent, incorrect AI recommendations at a rate indicating automation bias rather than substantive review; production disagreement-rate monitoring does not exist, so this pattern would be invisible without today's test. This represents a critical gap in the human oversight control the firm relies on to catch AI error before customer or regulatory harm; deployment for decisions currently framed as 'human-reviewed' should not proceed unchanged."

**Partial:** "Seeded-error catch rate meets threshold for [business line A] but falls below threshold for [business line B], where reviewer caseload is materially higher. The control is not demonstrated to generalise across current operating volumes; remediation should target caseload or training before extending reliance."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (multiple customers/cases affected by undetected AI
    error before the review layer catches it; regulatory notice risk)
  Likelihood: 2 (unlikely to cause harm given trained reviewers and
    active disagreement-rate monitoring; requires control degradation)
  Detectability: 2 (disagreement-rate monitoring surfaces drift within
    weeks; not real-time per-decision)
  Recoverability: 3 (reversible within days via case re-review and
    customer remediation; moderate operational cost)
  Novelty: 3 (domain expert would recognise "review the AI's work" as
    a control but is likely to miss that AI fluency specifically
    degrades reviewer vigilance in a way ordinary QA does not detect)

Residual risk interpretation: Acceptable if seeded-error testing and
disagreement-rate monitoring remain active and reviewed. Novelty is
the priority axis — automation bias is a known HF/E phenomenon but
rarely built into banking QA design, so periodic re-testing (not a
one-off validation) is essential as reviewers habituate to the system.

If controls are absent or degraded:
  Severity: 4 (systemic, batch-level harm across many decisions
    processed under the same unchallenged AI pattern)
  Likelihood: 4 (near-certain given decades of converging automation-
    bias research; the human checkpoint becomes cosmetic)
  Detectability: 3 (only surfaces via complaint, SAR gap, or forensic
    post-hoc review — no real-time signal)
  Recoverability: 3 (multi-week remediation across the affected batch;
    regulatory engagement)
  Novelty: 4 (governance papers assert human review is a control with
    no measurement basis; the gap is invisible until tested)

Residual risk: Critical if unmonitored. Prioritise for immediate
remediation given the ease of testing relative to the harm avoided.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Multiple customers/cases harmed if the review layer is compromised; regulatory notice risk under Consumer Duty and SM&CR |
| **Likelihood** | 3 | Probable if disagreement-rate monitoring and seeded-error testing are absent; automation bias is a well-replicated finding, not an edge case |
| **Detectability** | 2 | Detected via disagreement-rate trend or periodic audit within weeks, not real-time; requires deliberate measurement design |
| **Recoverability** | 3 | Reversible within days via re-review and remediation of the affected case batch; moderate operational and reputational cost |
| **Novelty** | 3 | Domain expert recognises "human review" as necessary but is likely to miss that fluency-driven acceptance is measurable and requires AI-aware test design, not standard QA |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Article 14, "Human Oversight", Aug 2024] requires high-risk AI systems to be designed such that natural persons can effectively oversee them, including correctly interpreting output and deciding not to rely on it. [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] requires firms to monitor whether outcomes are good for customers, extending to whether AI-assisted review genuinely protects customers from error. [FCA/PRA, Senior Managers & Certification Regime] creates individual accountability for the senior manager responsible for AI-assisted decisioning functions, which is undermined if human review is not substantively effective. Section pinpoints for SM&CR application to this specific control [UNVERIFIED — SM&CR module (SYSC 2, 4, 24-25) and PRIN 2A/SYSC 4 anchors confirmed extant (SYSC 19D removed 25 Aug 2026 — Remuneration Code, mis-cited; SYSC 4.1.1R substituted, Handbook-verified) on FCA Handbook online; no live sub-clause pinpoint mapping AI-assisted-decisioning review specifically has been published by the FCA to cite] (verified 29 Jul 2026).

## 18. Research Basis
> [Parasuraman & Riley, 1997, "Humans and Automation: Use, Misuse, Disuse, Abuse", Human Factors, 39(2), 230–253] establishes the foundational taxonomy of automation bias and complacency. [Skitka, Mosier & Burdick, 1999, "Does automation bias decision-making?", International Journal of Human-Computer Studies, 51(5), 991–1006] and [Skitka, Mosier & Burdick, 2000, "Accountability and automation bias", International Journal of Human-Computer Studies, 52(4), 701–717] empirically demonstrate omission and commission errors driven by automation reliance, and the seeded-error testing paradigm this canvas's Independent Test adapts. [Goddard, Roudsari & Wyatt, 2012, "Automation bias: a systematic review of frequency, effect mediators, and mitigators", Journal of the American Medical Informatics Association, 19(1), 121–127] synthesises effect sizes and mitigation strategies across clinical decision-support studies, directly informing the pass/fail thresholds used here.
>
> **[FAIAS Incident Register, row 38, "Douglas v. Deutsche Bank National Trust Company", 2026]**, citing [District of Columbia Court of Appeals, 2026, "Douglas v. Deutsche Bank National Trust Company", No. 24-CV-1099, published order filed 3 September 2026] — the first documented incident cited by this canvas. Counsel for a financial institution "used Google's generative artificial intelligence search tool to assist in locating case authority" and filed a brief in which, on counsel's own confirmation to the court, "four of the brief's cited authorities did not exist"; the court ordered "that appellee's brief is stricken" and referred the matter "to the Office of Disciplinary Counsel for any investigation it deems appropriate". The verification step that should have tested the output against source material did not operate, and nothing on the face of the filing distinguished the unverified brief from a verified one — which is the acceptance pattern this canvas's seeded-error design exists to detect. The court also stated that, had any of the firm's attorneys "reviewed the brief prior to filing, they would have discovered the errors", and called their failure to do so "highly concerning" (p.5). The controls that failed were lawyers' professional duties rather than an instrumented review workflow of the kind the Independent Test samples, so the incident evidences the failure mode and not its rate in a firm's own review process.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-MOD-006 (B.3 Calibration: confidence calibration gives
    reviewers a genuine risk signal to act on)
  - IRQ-HUM-002 (D.1 Automation Bias: approval-theatre throughput/
    dwell-time analysis, complementary measurement)
  - IRQ-GOV-003 (I.2 Approval, Tiering & Policy: technical enforcement
    that the review step cannot be bypassed)
  - IRQ-CON-004 (H.2 Customer Outcomes: customer-facing accuracy
    control downstream of this review layer)
```

## 20. References
```
[1] Parasuraman, R. & Riley, V., 1997. "Humans and Automation: Use, Misuse, Disuse, Abuse." Human Factors, 39(2), 230–253.
    Accessed: 2026-07-29

[2] Skitka, L.J., Mosier, K.L. & Burdick, M., 1999. "Does automation bias decision-making?" International Journal of Human-Computer Studies, 51(5), 991–1006.
    Accessed: 2026-07-29

[3] Skitka, L.J., Mosier, K.L. & Burdick, M., 2000. "Accountability and automation bias." International Journal of Human-Computer Studies, 52(4), 701–717.
    Accessed: 2026-07-29

[4] Goddard, K., Roudsari, A. & Wyatt, J.C., 2012. "Automation bias: a systematic review of frequency, effect mediators, and mitigators." Journal of the American Medical Informatics Association, 19(1), 121–127.
    Accessed: 2026-07-29

[5] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Article 14: Human Oversight."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[6] Financial Conduct Authority, 2023. "Handbook PRIN 2A: The Consumer Duty."
    Published: 2023-07-31
    URL: https://www.fca.org.uk/firms/consumer-duty

[7] District of Columbia Court of Appeals, 2026. "Douglas v. Deutsche Bank National Trust Company." No. 24-CV-1099, published order.
    Filed: 2026-09-03
    URL: https://www.dccourts.gov/sites/default/files/2026-09/Douglas%20v.%20Deutsche%20Bank%20Nat%27l%20Trt%20Co.%2024-CV-1099%20ORDER.pdf
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.1 (Human Oversight, Automation Bias)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Underwriting/claims/AML SMEs assume a documented sign-off equals genuine review; automation-bias research shows this is frequently false and undetectable without seeded-error testing.
✓ Test 2 (Plausible Harm): Grounded in decades of converging human-factors research (Parasuraman & Riley 1997; Skitka et al. 1999, 2000; Goddard et al. 2012) across aviation, process control and clinical decision support.
✓ Test 3 (Testable): Answerable via seeded-error staging test with measured catch rate; disagreement-rate monitoring provides an ongoing production signal.
✓ Test 4 (Decision-Relevant): Outcome directly informs whether the human review step can be relied upon as a control, gating deployment or requiring redesign of the review workflow.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form (row 38, Douglas v. Deutsche Bank National Trust Company), the first incident evidence this canvas carries. Field 20 — entry [7] added for the order. Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within days; ASSURANCE_MODEL.md §7 scores recovery within hours 2 and recovery within days 3. The other axes, the ★ rating and the research basis are unchanged.
```

---
---

