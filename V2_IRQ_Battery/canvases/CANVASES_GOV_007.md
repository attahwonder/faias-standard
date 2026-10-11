# CANVAS: IRQ-GOV-007

## 1. IRQ ID & Title
**IRQ-GOV-007: Validation Not Independent of Development, or Reliant on Vendor/Public Benchmark Claims**

Register question: "Was validation performed by a party independent of development, with authority to reject, using firm-relevant evaluations rather than vendor or public benchmark claims?"

## 2. Business Activities Affected
- **Every AI system's approval decision:** validation is the control that is supposed to catch development-team blind spots and vendor overclaiming before deployment; if it is not genuinely independent, the approval decision rests on unverified self-assessment.
- **Vendor/third-party model deployments specifically:** where the firm relies on a foundation model provider's own safety evaluations or public benchmark scores rather than firm-relevant testing, validation risk is highest because the firm has the least direct visibility into how the model was actually tested.
- **Fast-moving agile/product deployments:** organisational pressure to ship quickly creates the strongest incentive for validation to be delegated back to the development team itself ("self-validation"), undermining independence precisely where speed pressure is highest.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns the structural independence and authority of the human/organisational validation function, not the system's own outputs (which are the subject of the validation itself).

## 4. Failure Mode
> Validation of an AI system prior to deployment is performed by the same team (or a team lacking genuine authority to reject) that developed or procured it, or relies substantially on vendor-reported or public benchmark performance claims rather than firm-relevant evaluation on the firm's own data and use cases — so approval decisions rest on unverified self-assessment rather than genuine independent challenge.

## 5. Potential Consequences
- **Customer:** A system with material weaknesses (bias, hallucination rate, capability boundary failures) that self-assessment did not surface, or that benchmark scores did not reveal for the firm's specific use case, reaches customers without having been genuinely tested against it.
- **Institution:** The firm's approval records give false comfort — an approval paper that cites "validation complete" without genuine independence is not evidence of the safety it claims to represent, and cannot be relied upon in a subsequent incident investigation or regulatory challenge.
- **Regulator/market:** Independent validation is a cornerstone expectation of PRA SS1/23's model risk management principles; its absence for AI systems specifically is a direct, easily-identified supervisory finding, especially given the PRA's October 2025 roundtable presentation of its current thinking on AI and ML model risk under SS1/23.

## 6. Failure Chain
```
Development team (or procurement team under delivery pressure) performs its own
"validation," or validation relies on vendor safety-eval claims / public benchmark scores
  ↓ (IRQ-GOV-007 — THIS IRQ: no genuinely independent function with reject authority
  reviewed firm-relevant evidence)
Approval paper records "validated" with no independent challenge actually applied
  ↓ (IRQ-MOD-011: benchmark contamination or vendor overclaiming goes undetected)
System weaknesses that firm-relevant testing would have surfaced (bias for the firm's
customer base, hallucination on the firm's document types, capability boundary failures
for the firm's specific tasks) remain undiscovered
  ↓ (IRQ-GOV-006: appetite testing is meaningless if the underlying validation evidence
  feeding it is unverified)
System deploys with an approval record that overstates the actual assurance obtained
  ↓
Weakness materialises in production → post-incident review finds validation was
self-performed or benchmark-reliant → the approval record itself is discredited

Control Breakpoints:
  • IRQ-GOV-007: genuinely independent validation function with authority to reject
  • IRQ-MOD-011: firm-relevant, contamination-checked evaluation evidence (not vendor/public
    benchmark claims alone)
  • IRQ-GOV-001: named ownership creates the accountable party validation reports to
  • IRQ-GOV-006: appetite testing depends on validation evidence being genuinely independent
```

## 7. Why a Domain Expert May Miss It
- Traditional model risk management has a well-established independent validation function for statistical/credit models; SMEs may assume the same team automatically performs the same role for GenAI/agentic systems, without checking whether that team has the AI-specific competence or capacity to genuinely challenge, rather than rubber-stamp, a new technology.
- Vendor safety cards and published benchmark leaderboards look like rigorous, quantitative evidence; a reviewer unfamiliar with benchmark contamination risk (test items present in training data) or the gap between public benchmark tasks and the firm's actual use case can mistake this for firm-relevant validation.
- "Independent" is sometimes satisfied structurally (a different team signs the approval) without being satisfied substantively (that team lacks the authority, resourcing or genuine willingness to reject a deployment the business wants to proceed) — a governance-literate but not AI-literate reviewer can miss the substantive gap behind the structural tick-box.
- Under delivery pressure, "validation" can quietly become "confirmation" — a documentation exercise performed after the deployment decision is effectively already made — which looks procedurally similar to genuine pre-decision validation on paper.

## 8. Assurance Objective
**AO-GOV-007:** Validation of AI systems prior to deployment shall be performed by a function structurally and substantively independent of development and procurement, with genuine authority to reject, and shall be based on firm-relevant evaluation evidence rather than vendor or public benchmark claims alone.

## 9. Expected Controls (Traced)
- **Independent validation function organisationally and reporting-line separated from development/procurement, with documented authority to reject deployment** — [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023), Principle 4 — Independent Model Validation] — the direct, primary anchor for this control; SS1/23 explicitly requires validation independence for models, extended to AI/ML.
- **Firm-relevant evaluation on the firm's own data, use cases and customer population, distinct from vendor safety-card claims or public benchmark scores** — [linked IRQ-MOD-011; PRA MRM AI and ML roundtable presentation slides, October 2025, on development datasets that may not represent the target population and on testing in conditions unlike deployment; the extension to vendor-reported evidence is FAIAS's own] — closes the gap between "the vendor says it's safe" and "we tested it against our own risk."
- **Benchmark contamination screening where public benchmark scores are used as supplementary evidence** — [linked IRQ-MOD-011; academic literature on benchmark contamination] — where benchmark evidence is used at all, it is screened for the risk that test items appeared in training data.
- **Documented instances of validation exercising reject/restrict authority, evidencing the function is substantively (not just structurally) independent** — [ISO/IEC 42001:2023, clause 9 (performance evaluation)] — a functioning independence control produces a track record of actual challenge outcomes, not only pass records.
- **ECB revised Guide to Internal Models (2025) explicit machine-learning validation expectations** — [ECB, "Guide to Internal Models," revised Jul 2025] — for EU-supervised entities, provides an explicit supervisory analogue requiring independent human oversight and documentation of complex ML validation; cited as reinforcing evidence of the direction of supervisory expectation even where not directly binding on a UK-only firm.

## 10. Expected Evidence (Tagged L1–L5)
- Approval paper stating "validation complete" — **L1** (assertion; does not evidence independence or firm-relevance).
- Organisational chart/reporting-line documentation showing the validation function's separation from development/procurement — **L2**.
- Validation methodology document specifying use of firm-relevant evaluation data and contamination screening — **L2**.
- Sample validation report for a specific system showing firm-relevant test results (not solely vendor safety-card citation), methodology, and findings — **L3**.
- Internal audit review of the validation function's independence, resourcing and reject-authority track record — **L4**.
- Record of at least one instance where validation rejected, restricted or required remediation of a deployment, evidencing substantive (not merely structural) independence — **L5**.
- **Worked example — a vendor-reported result correctly caveated, 3 September 2026, amended 9 September 2026 (OpenAI, GPT-6 Astra System Card, §8.2.3 "Declining to Exploit a Honeypot During Difficult ExploitGym Problems").** The card reports a zero observed attack rate — "GPT-6 Astra did not make any attacks at the honeypot — it did, however, succeed at the assigned problem" — and in the same section states the limits itself: "This evaluation describes behavior under test conditions without cyber safeguards, not normal production use" and "A zero observed attack rate here does not establish that Astra would respect every authorization boundary in real-world settings." Its change log records the card being amended on 9 September 2026 to expand on those limits, "the absence of observed failures does not establish reliability across settings". **Why this is the useful worked example for this canvas, rated ★3 · P3:** it shows what a properly bounded vendor result looks like, so a reviewer applying limb (2) of §11 can distinguish a vendor disclosure that states its own scope from one that does not — and it shows that even a well-caveated vendor result is a **propensity** finding, not a capability finding: the same card, at §9.2.2.2, records that the model was instructed to attack the honeypot "as it had a low propensity to do so naturally" and measures successful attacks. Neither the zero rate nor its caveats make the result firm-relevant evidence, which is what limb (2) requires — **L1 as to the firm's own validation, notwithstanding the quality of the disclosure**.

## 11. Independent Test
> For a risk-based sample of approved AI systems, obtain the validation record and assess: (1) organisational and reporting-line separation of the validation function from development/procurement, (2) whether the evaluation evidence underpinning the validation conclusion is firm-relevant (firm's own data, use cases, customer population) or substantially vendor-reported/public-benchmark-derived, (3) whether any public benchmark evidence used was screened for contamination risk, and (4) whether the validation function has a documented track record of exercising reject/restrict authority (not solely pass outcomes). Interview validation function staff on their resourcing, AI-specific competence and experience of being overridden by commercial pressure. Methodology follows standard independent-validation-adequacy review practice as applied under SS1/23 to traditional models, extended to AI-specific firm-relevance and contamination-screening dimensions with no AI-specific benchmark for what constitutes adequate firm-relevant GenAI validation evidence. Conducted against governance records and interviews only; no production system access required. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established independent-validation-adequacy methodology directly anchored in SS1/23 Principle 4 and reinforced by the PRA's own October 2025 MRM AI/ML roundtable findings; no AI-specific benchmark defines the precise evidence threshold for "firm-relevant" GenAI validation, so professional judgement determines adequacy of the specific evidence reviewed).

## 12. Pass Indicators
- Validation function for 100% of the sample is organisationally separate from development/procurement, with documented reject authority.
- Validation conclusions are supported by firm-relevant evaluation evidence for 100% of the sample; vendor/public benchmark evidence, where used, is explicitly screened for contamination and used only as supplementary evidence.
- At least one documented instance exists of validation exercising reject/restrict authority in the review period, evidencing substantive independence.
- Interviewed validation staff describe adequate resourcing and AI-specific competence, and can cite instances of successfully challenging commercial pressure.
- Validation reports are dated prior to the deployment decision, not produced retrospectively to document a decision already made.

## 13. Fail Indicators
- Validation is performed by the same team that developed or procured the system, or by a nominally separate team with no documented reject authority.
- Validation conclusions rest substantially on vendor safety-card claims or public benchmark scores with no firm-relevant testing evidence.
- No instance of validation exercising reject/restrict authority exists across the sample — suggests a rubber-stamp function.
- Validation reports are dated after the deployment decision was effectively made (confirmation, not validation).
- Public benchmark evidence relied upon shows no contamination screening despite known contamination risk in the relevant benchmark literature.

## 14. Reporting Language
**Pass:** "Validation for [n] sampled systems is performed by a function structurally and substantively independent of development and procurement, with documented reject authority exercised in [n] instances in the review period. Validation conclusions rest on firm-relevant evaluation evidence; vendor/public benchmark evidence, where used, is screened for contamination. Conclusions rest on ★3 methodology — established independent-validation-adequacy review anchored in SS1/23 Principle 4 — and should be read as professional assessment."
**Fail:** "Testing found that validation for [n] of [sample size] systems was performed by the development team itself, or by a nominally separate function with no evidence of reject authority ever exercised, and that validation conclusions rest substantially on vendor safety-card claims rather than firm-relevant evaluation. This does not meet SS1/23 Principle 4's independent-validation expectation; approval records for these systems should be treated as unsupported by genuine independent challenge until validation is remediated."
**Partial:** "Validation is structurally independent and firm-relevant for internally developed systems, but relies substantially on vendor-reported evaluation for directly procured foundation-model deployments, affecting [x]% of the sample. The assurance objective is not yet met for that subset; remediation should extend firm-relevant evaluation to procured/vendor deployments within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (weak validation is a control-quality issue; realised severity depends on what
              undiscovered weaknesses turn out to be)
  Likelihood: 2 (plausible under delivery pressure and where AI-specific validation competence
              is scarce; less likely with a resourced, genuinely independent function)
  Detectability: 2 (found via internal audit review of the validation function itself; not
              visible from the approval paper's "validated" statement alone)
  Recoverability: 1 (reversible by re-validating with a genuinely independent function once
              found, though the deployment period without genuine validation cannot be undone)
  Novelty: 3 (a governance SME familiar with traditional model validation would likely assume
              the same function automatically extends its independence and competence to AI
              without checking; benchmark contamination risk specifically is an AI-native
              blind spot for a traditional-model-trained reviewer)

Interpretation: acceptable residual risk with a genuinely independent, AI-competent validation
function with a demonstrated reject-authority track record; the material concern is that this
IRQ is the primary structural safeguard against every other IRQ's self-assessed evidence being
taken at face value — its failure degrades confidence in the whole evidence base.

If controls are absent or degraded:
  Severity: 3 (systematic weaknesses across multiple deployed systems go undiscovered because
              the one control designed to independently surface them is compromised)
  Likelihood: 3 (foreseeable given the well-documented scarcity of AI-specific validation
              competence and the organisational pressure to ship quickly)
  Detectability: 4 (a self-validating or rubber-stamp function produces "validated" records
              indistinguishable on paper from genuine validation; only a dedicated audit of
              the function itself, not of individual systems, surfaces the gap)
  Recoverability: 2 (once found, re-validating affected systems with a genuinely independent
              function is achievable but effort-intensive across the affected population)
  Novelty: 3
Residual risk: High if independence is compromised; this IRQ is a structural safeguard whose
failure silently undermines confidence in every other governance and technical control.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Weak validation is a control-quality issue; realised severity is inherited from whatever weaknesses it failed to surface. |
| **Likelihood** | 3 | Probable under delivery pressure and given the well-documented industry-wide scarcity of AI-specific validation competence. |
| **Detectability** | 4 | A self-validating or rubber-stamp function is indistinguishable on paper from a genuine one; only a dedicated audit of the validation function's independence and track record surfaces it. |
| **Recoverability** | 2 | Re-validating with a genuinely independent function is achievable once found, but the deployment period without genuine validation cannot be retrospectively cured. |
| **Novelty** | 3 | Benchmark contamination risk and the gap between vendor safety-card claims and firm-relevant evidence are AI-native blind spots a traditional-model-trained validation reviewer would likely not anticipate. |

## 17. Regulatory Basis
> [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023), Principle 4 — Independent Model Validation] is the direct, primary anchor: validation must be performed by staff independent of development, with authority to require remediation or reject use, and this principle is confirmed to extend to AI/ML by the Bank of England and PRA letter of 22 April 2024. [PRA, "The PRA holds model risk management roundtable on artificial intelligence and machine learning technologies," published Nov 2025] reports two roundtable sessions (20 and 22 October 2025) at which the PRA presented its thinking on AI and ML model risk under SS1/23, and its presentation slides cover model tiering, development testing, independent validation and monitoring, evidencing this is an active area of supervisory attention. [ECB, "Guide to Internal Models," revised Jul 2025] provides explicit machine-learning validation expectations (explainability, human oversight, documentation) for EU-supervised entities, reinforcing the direction of expectation.

## 18. Research Basis
> No peer-reviewed academic literature specifically evaluates independent-validation-function adequacy for enterprise GenAI deployment; this control area is regulatory/audit practice rather than a research literature, consistent with this domain's evidentiary profile. Benchmark contamination as a distinct evidentiary risk (test items present in training data, undermining public benchmark score reliability) is well-documented in the broader machine-learning evaluation literature and is treated in this canvas as the AI-specific extension of the traditional "vendor claims are not independent evidence" validation principle [specific contamination-study citations retained in IRQ-MOD-011, this canvas's linked evidentiary anchor, to avoid duplication].
>
> **[FAIAS Incident Register, row 68, "Epic Sepsis Model external validation", 2021]** — an external validation of a vendor's sepsis-prediction model, already in wide use in hospitals, found poor discrimination (AUC 0.63): at an alert threshold of a score of 6 or higher, the model did not identify 67% of patients with sepsis (1,709 of 2,552) and alerted on 18% of hospitalisations (6,971 of 38,455), and the authors state that its ability to identify patients with sepsis "has not been adequately evaluated despite widespread use". Carried as a secondary row: a peer-reviewed study, abstract only, which does not say what the adopting hospitals relied on. The setting is healthcare, not financial services.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-MOD-011 (B.5: evaluation contamination and benchmark integrity — the firm-relevant-
    evidence dimension of this IRQ's validation-quality test)
  - IRQ-GOV-001 (I.1: named ownership — the accountable party validation reports findings to)
  - IRQ-GOV-004 (I.2: tiering — determines validation depth proportionate to risk)
  - IRQ-GOV-006 (I.2: risk appetite — depends on validation evidence being genuinely independent)
  - IRQ-SEC-002 (E.1: adversarial jailbreak testing — a specific validation activity this
    function should ensure is genuinely independent and firm-relevant, not vendor-claimed)
```

## 20. References
```
[1] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024. Principle 4 — Independent Model Validation.
[2] Bank of England/PRA, 2025. "The PRA holds model risk management roundtable on artificial
    intelligence and machine learning technologies." Published November 2025.
[3] Bank of England/PRA, 2025. "October 2025 MRM AI and ML Roundtable — presentation slides." PDF,
    October 2025.
[4] European Central Bank, 2025. "ECB revised Guide to Internal Models (incl. ML
    expectations)." Revised July 2025.
[5] Bank of England/PRA, 2024. "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI." 22 April 2024.
[6] OpenAI, 2026. "GPT-6 Astra System Card." 3 September 2026, amended 9 September 2026.
    URL: https://deploymentsafety.openai.com/gpt-6-astra
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.3 (Governance domain, Validation & Oversight)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): SMEs assume the existing independent validation function that
  works for statistical/credit models extends its independence and competence automatically
  to GenAI; vendor safety-card claims and public benchmarks look like rigorous evidence to a
  reviewer unfamiliar with contamination risk and firm-relevance gaps.
✓ Test 2 (Plausible Harm): Grounded directly in SS1/23 Principle 4 and the PRA's own October
  2025 MRM AI/ML roundtable dialogue; compromised validation independence silently degrades
  confidence in every other IRQ's self-assessed evidence.
✓ Test 3 (Testable): Testable via reporting-line review, evidence-source assessment, and
  interview-based track-record verification. ★3 methodology, anchored in a named regulatory
  principle.
✓ Test 4 (Decision-Relevant): Outcome determines whether the firm's entire approval-evidence
  base can be trusted, or must be treated as self-assessed and unverified.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 10 — the GPT-6 Astra System Card §8.2.3 zero-attack-rate statement added as a worked example of a vendor-reported result correctly caveated (the card disclaims the inference itself, and was amended 9 Sep 2026 to expand those limits), with the propensity-versus-capability distinction from §9.2.2.2 stated and the conclusion that a well-caveated vendor result is still not firm-relevant validation evidence. ★3 · P3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — the SS1/23 sentence names the Bank of England and PRA letter of 22 April 2024, in place of the PRA's April 2024 mapping. Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 17 and 20 — the PRA roundtable page is cited by its heading as published, "The PRA holds model risk management roundtable on artificial intelligence and machine learning technologies". Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 68, Epic Sepsis Model external validation, carried as a secondary row: a peer-reviewed study read at its abstract, in a healthcare setting). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Field 20 References — the Bank of England and PRA letter of 22 April 2024 cited by its title, The Bank and the PRA's response to DSIT/HMT: update on our approach to AI. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Fields 5, 9, 17 and 20 — the PRA's October 2025 roundtable page and slides are described as what they are: the page reports two roundtable sessions, and the slides cover model tiering, development testing, independent validation and monitoring under SS1/23. The statements that they addressed validation of non-deterministic or generative AI models are removed, and references [2] and [3] describe the page and the slides as what they are. ★3 and the risk profile unchanged.
```

---
---

