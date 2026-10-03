# CANVAS: IRQ-HUM-007

## 1. IRQ ID & Title
**IRQ-HUM-007: Explanation Inadequacy Undermining Independent Judgement**

Register question: "Do decision-makers relying on AI outputs receive explanations sufficient in content and timeliness to exercise independent judgement, tested with the actual user population?"

## 2. Business Activities Affected
- **Underwriting review:** Underwriters need an explanation of why the AI recommends decline or approval that is substantively useful (which factors, what evidence, what confidence), not a generic disclaimer, in order to genuinely exercise independent judgement.
- **Claims approval:** Claims handlers reviewing an AI-drafted settlement rationale need the explanation to surface the actual driving factors (liability evidence, precedent cases used), not a post-hoc plausible-sounding narrative that may not reflect the model's actual reasoning.
- **AML case handling:** Investigators need explanations of why an AI flagged or cleared a typology to be specific enough to independently verify, not a generic "pattern consistent with known typology X" statement.

## 3. AI Behaviour(s)
- Generates natural-language explanations or rationale alongside its recommendation, often post-hoc rather than reflecting the actual computational process that produced the output.
- Presents explanations with the same fluent, confident register regardless of whether the explanation is accurate, complete or faithful to the underlying decision process.
- Explanation format and content are typically designed by developers, not validated against what the actual reviewing population needs to exercise genuine independent judgement.

## 4. Failure Mode
> The explanation provided to the human decision-maker is insufficient — in content, faithfulness or timeliness — to enable genuine independent judgement, but its fluent presentation creates the impression of adequate explanation, and this inadequacy has never been tested with the actual reviewing population under realistic conditions.

## 5. Potential Consequences
- **Customer:** Decisions are made (or upheld on review) based on explanations that do not actually let the reviewer catch a wrong recommendation, undermining the value of the human checkpoint the firm relies upon.
- **Institution:** Regulatory finding that explanation adequacy was asserted, not validated, undermining both the human-oversight defence and any customer-facing "right to explanation" claims.
- **Regulator/market:** FCA Consumer Duty and EU AI Act transparency expectations are not met in substance even if a technical explanation feature exists, exposing the firm to supervisory findings distinct from the underlying decision-quality question.

## 6. Failure Chain
```
Model generates a post-hoc, fluent explanation alongside its
recommendation
  ↓ (IRQ-MOD-009: the stated reasoning may not faithfully represent the
     factors actually driving the output — a model-layer risk this IRQ
     inherits)
Explanation format/content designed by developers without validation
against actual reviewer comprehension or decision-making needs
  ↓ (IRQ-HUM-007 — THIS IRQ: explanation inadequate to support
     independent judgement, untested with real users)
Reviewer reads a fluent explanation, assumes it is adequate, and does
not seek further verification
  ↓ (IRQ-HUM-001: automation bias compounds — a plausible explanation
     reduces, rather than increases, the reviewer's scrutiny)
Reviewer's "independent judgement" is in substance dependent on an
unfaithful or insufficient explanation
  ↓
Wrong decision proceeds; post-hoc investigation reveals the explanation
never actually supported genuine independent verification

Control Breakpoints:
  • IRQ-MOD-009: documented faithfulness caveats on model-stated
    reasoning, feeding into what explanation content can be trusted
  • IRQ-HUM-007: explanation-adequacy testing with the real reviewing
    population, not developer assumption
  • IRQ-HUM-001: reviewer training to treat a fluent explanation as a
    starting point for verification, not a substitute for it
```

## 7. Why a Domain Expert May Miss It
- Assumption: "the system provides an explanation, so the transparency/explainability requirement is met" — presence of an explanation feature is conflated with adequacy of that explanation for the specific decision-making purpose it is meant to serve.
- Traditional model-risk-management explainability practice (e.g. SHAP/LIME feature-importance outputs for structured credit models) does not directly transfer to generative explanations, which can be fluent and specific-sounding while being unfaithful to the model's actual computation — a distinction MRM practitioners trained on structured models may not intuitively apply to LLM-generated rationale.
- Process gap: explanation design is typically a product/engineering decision, validated (if at all) for general comprehensibility, not specifically tested for whether it gives the actual reviewing population — underwriters, claims handlers, investigators — what they need to exercise independent professional judgement.
- Testing gap: usability testing of an explanation feature, where it occurs, often measures user satisfaction or comprehension of the explanation's language, not whether the explanation actually changes the reviewer's decision behaviour or catch rate on wrong recommendations.

## 8. Assurance Objective
**AO-HUM-007:** Explanations provided to human decision-makers relying on AI outputs shall be demonstrated, through testing with the actual user population, to be sufficient in content, faithfulness and timeliness to support genuine independent judgement, not merely to be present or superficially comprehensible.

## 9. Expected Controls (Traced)
- **Explanation-adequacy testing with the actual reviewing population** — [Emerging Practice, informed by Doshi-Velez & Kim, 2017, "Towards A Rigorous Science of Interpretable Machine Learning", arXiv:1702.08608, human-grounded evaluation framework] — explanations tested on real underwriters/claims handlers/investigators, measuring decision-behaviour impact, not just comprehension surveys.
- **Faithfulness caveats on model-stated reasoning propagated into explanation design** — [linked IRQ-MOD-009] — where the underlying model's stated reasoning is known to be potentially unfaithful, explanation content and reviewer training are designed with that caveat explicit, rather than presenting the explanation as a ground-truth account of the decision process.
- **EU AI Act Article 13 transparency and Article 14 oversight-support requirements** — [EU AI Act, Regulation (EU) 2024/1689, Articles 13 and 14, Aug 2024] — high-risk AI systems must be sufficiently transparent to enable users to interpret output and use it appropriately, directly requiring adequacy, not mere presence, of explanation.
- **FCA Consumer Duty and PRIN 2A comprehensibility standard** — [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] — informs the standard against which internal decision-maker explanations, and any customer-facing explanation, should be assessed for genuine comprehensibility.
- **Timeliness requirement matched to the decision workflow's time constraints** — [linked IRQ-HUM-002; FCA, Handbook SYSC 4.1.1R] — explanation must be deliverable within the time the reviewer actually has available, not only theoretically adequate given unlimited time.

## 10. Expected Evidence (Tagged L1–L5)
- Product documentation asserting "the system provides an explanation for every recommendation" — **L1**.
- Explanation design specification (content, format, faithfulness caveats) — **L2**.
- Usability testing results measuring reviewer comprehension of explanation language in a controlled setting — **L3**.
- Staging test: explanation-adequacy exercise with a representative sample of actual reviewers, measuring whether access to the explanation changes decision behaviour or catch rate on seeded incorrect recommendations (cross-referenced with IRQ-HUM-001's seeded-error methodology) — **L3**.
- Independent audit assessing explanation faithfulness against the model's actual computational basis, where technically feasible — **L4**.
- Production data: reviewer feedback or override patterns correlated with explanation quality/type across a sustained period — **L5**.

## 11. Independent Test
> In a non-production environment, using the same seeded-error case-set methodology as IRQ-HUM-001, run two arms with a representative sample of the actual reviewing population (underwriters, claims handlers or AML investigators, as applicable): one arm receives the AI's current explanation alongside the recommendation, the other receives the recommendation with a deliberately minimal or absent explanation (or, where feasible, a third arm with a redesigned explanation). Measure the difference in seeded-error catch rate, decision confidence, and time-to-decision across arms. Where feasible, supplement with a structured comprehension interview on a subsample to assess whether reviewers can correctly restate the actual basis for the AI's recommendation. Executed on de-identified dev/test case files with real reviewing staff in a staging exercise; no live decisions are affected. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (human-grounded interpretability evaluation, per Doshi-Velez & Kim's framework, is credible published methodology, but its specific application — comparing catch-rate impact of explanation presence/quality in an FS review context — is bespoke test design with no agreed FS benchmark; heavily dependent on case-set and explanation-variant design).

## 12. Pass Indicators
- Seeded-error catch rate is measurably higher in the arm with the current explanation than in the minimal/no-explanation arm, demonstrating the explanation adds genuine verification value.
- Comprehension interviews show reviewers can substantively and correctly restate the actual basis for the AI's recommendation, not just repeat surface language from the explanation.
- Explanation delivery time fits within the reviewer's actual available decision time in the workflow, evidenced by the IRQ-HUM-002 dwell-time data.
- Explanation content is designed with explicit faithfulness caveats where the underlying model's stated reasoning is known to be potentially unfaithful.
- Explanation-adequacy testing has been conducted with the real reviewing population, not only in generic usability testing.

## 13. Fail Indicators
- Seeded-error catch rate shows no meaningful difference between the explanation and minimal/no-explanation arms, indicating the explanation adds no genuine verification value despite its presence.
- Comprehension interviews show reviewers can repeat explanation language but cannot substantively restate or engage with the actual basis for the recommendation.
- Explanation delivery is too slow or too lengthy to be genuinely used within the reviewer's actual available decision time, so it is skipped in practice.
- No faithfulness caveats exist; the explanation is presented and treated internally as a ground-truth account of the model's reasoning.
- No testing has ever been conducted with actual reviewing staff; explanation adequacy is asserted by the development team.

## 14. Reporting Language
**Pass:** "Explanation-adequacy testing with a representative sample of [reviewing population] shows seeded-error catch rate is measurably higher with the current explanation than without it, and comprehension interviews confirm reviewers can substantively restate the actual basis for recommendations. This is a ★2 assessment — credible human-grounded evaluation methodology, bespoke test design — and should be re-tested whenever explanation design or the underlying model changes materially."

**Fail:** "Explanation-adequacy testing shows no measurable difference in seeded-error catch rate between reviewers given the current explanation and reviewers given no explanation at all, indicating the explanation does not currently support genuine independent judgement despite its fluent presentation. This undermines the human-oversight defence the firm relies on for this workflow and should be remediated with a redesigned, tested explanation before continued reliance on the current format."

**Partial:** "Explanation-adequacy testing shows a meaningful catch-rate improvement for [decision type A] but no improvement for [decision type B], where the explanation format does not surface the specific evidence type reviewers need. Remediation should redesign explanation content specifically for [decision type B] before continued reliance."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (explanation inadequacy alone does not directly cause
    harm but undermines the human checkpoint's ability to catch harm
    that originates elsewhere in the chain)
  Likelihood: 2 (unlikely to be material if explanation-adequacy
    testing with real reviewers is active and repeated at model change)
  Detectability: 2 (detectable via the seeded-error comparison
    methodology, ahead of any real event)
  Recoverability: 2 (reversible via explanation redesign once
    identified; days-to-weeks, with re-testing)
  Novelty: 3 (domain expert assumes an explanation feature satisfies
    the requirement; testing explanation adequacy against actual
    decision-behaviour impact, rather than comprehensibility alone, is
    not standard practice outside specialist interpretability research)

Residual risk interpretation: Acceptable with active testing tied to
the same seeded-error infrastructure used for IRQ-HUM-001, which makes
this a relatively low-marginal-cost control to maintain once the
underlying seeded-error case-set methodology exists.

If controls are absent or degraded:
  Severity: 3 (the human checkpoint the firm relies on to catch AI
    error is materially weaker than assumed, across the full decision
    volume relying on the current explanation design)
  Likelihood: 3 (probable — post-hoc, potentially unfaithful
    explanations from generative models are a well-documented pattern,
    and explanation design is rarely tested for decision-behaviour
    impact by default)
  Detectability: 3 (invisible without a specific comparative test;
    comprehensibility surveys alone would not surface this)
  Recoverability: 3 (multi-week remediation requiring explanation
    redesign and re-testing)
  Novelty: 4 (product documentation asserts explanation adequacy with
    no decision-behaviour-impact evidence; the gap is invisible
    without today's specific comparative test design)

Residual risk: High. Should be prioritised, particularly where it can
share test infrastructure with IRQ-HUM-001's seeded-error programme.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Does not directly cause harm but materially weakens the human checkpoint relied upon to catch harm originating elsewhere |
| **Likelihood** | 3 | Probable given the well-documented pattern of post-hoc, potentially unfaithful generative explanations and the rarity of decision-behaviour-impact testing by default |
| **Detectability** | 2 | Detectable via the seeded-error comparative test methodology, ahead of any real event, if such testing is active |
| **Recoverability** | 2 | Reversible via explanation redesign and re-testing once identified, typically within weeks |
| **Novelty** | 3 | Domain expert assumes presence of an explanation feature satisfies the requirement; testing for decision-behaviour impact rather than comprehensibility alone is specialist practice |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Article 13, "Transparency and Provision of Information to Deployers", Aug 2024] requires high-risk AI systems to be sufficiently transparent to enable deployers to interpret output and use it appropriately; [Article 14] requires human overseers to be able to correctly interpret system output — both directly requiring adequacy of explanation, not mere presence. [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] sets a comprehensibility standard relevant by analogy to internal decision-maker explanations. Section pinpoints [UNVERIFIED — cited modules (SYSC 4, SYSC 9, SYSC 15A, PRA SS1/21/PS21/3, EU AI Act Art. 14 — SYSC 19D removed 25 Aug 2026: it is the dual-regulated firms Remuneration Code and was mis-cited; SYSC 4.1.1R substituted, verified from the Handbook) confirmed extant on FCA Handbook/BoE/eur-lex; no AI-specific sub-clause pinpoint published by the regulator to cite beyond module level] (verified 29 Jul 2026).

## 18. Research Basis
> [Doshi-Velez, F. & Kim, B., 2017, "Towards A Rigorous Science of Interpretable Machine Learning", arXiv:1702.08608] establishes the human-grounded evaluation framework (measuring task performance impact, not just comprehensibility) this canvas's Independent Test adapts. [Lipton, Z.C., 2018, "The Mythos of Model Interpretability", ACM Queue, 16(3)] documents the gap between an explanation feeling satisfying and an explanation being faithful or decision-useful — directly relevant to why fluent generative explanations can create false confidence. [Bansal, G. et al., 2021, "Does the Whole Exceed its Parts? The Effect of AI Explanations on Complementary Team Performance", CHI 2021] provides empirical evidence that explanations can, in some conditions, reduce rather than improve human-AI team decision accuracy — directly supporting the need for empirical (not assumed) testing of explanation adequacy.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-MOD-009 (B.4 Specification Gaming & Reasoning Integrity:
    faithfulness of model-stated reasoning, upstream input to
    explanation design)
  - IRQ-HUM-001 (D.1 Automation Bias: shared seeded-error test
    infrastructure and the risk that a fluent explanation reduces
    rather than increases scrutiny)
  - IRQ-CON-008 (H.3 Feedback Loops & Transparency: customer-facing
    disclosure and comprehension testing, parallel obligation)
  - IRQ-HUM-008 (D.4 Accountability & Contestability: adequate
    explanation is a prerequisite for a meaningful contest route)
```

## 20. References
```
[1] Doshi-Velez, F. & Kim, B., 2017. "Towards A Rigorous Science of Interpretable Machine Learning." arXiv:1702.08608.
    URL: https://arxiv.org/abs/1702.08608
    Accessed: 2026-07-29

[2] Lipton, Z.C., 2018. "The Mythos of Model Interpretability." ACM Queue, 16(3), 31–57.
    Accessed: 2026-07-29

[3] Bansal, G., Wu, T., Zhou, J. et al., 2021. "Does the Whole Exceed its Parts? The Effect of AI Explanations on Complementary Team Performance." CHI 2021.
    Accessed: 2026-07-29

[4] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Articles 13 and 14."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[5] Financial Conduct Authority, 2023. "Handbook PRIN 2A: The Consumer Duty."
    Published: 2023-07-31
    URL: https://www.fca.org.uk/firms/consumer-duty
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.4 (Human Oversight, Accountability & Contestability)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs conflate the presence of an explanation feature with its adequacy; MRM practitioners trained on structured-model feature-importance outputs may not apply the same scrutiny to generative post-hoc rationale.
✓ Test 2 (Plausible Harm): Grounded in Doshi-Velez & Kim (2017), Lipton (2018), and Bansal et al.'s (2021) empirical finding that explanations can reduce human-AI team accuracy.
✓ Test 3 (Testable): Answerable via a comparative seeded-error test measuring catch-rate impact of explanation presence/quality with real reviewers.
✓ Test 4 (Decision-Relevant): Directly determines whether the human checkpoint's reliance on AI-generated explanations is well-founded, gating explanation redesign investment.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

