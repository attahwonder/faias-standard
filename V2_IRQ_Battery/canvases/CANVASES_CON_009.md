# CANVAS: IRQ-CON-009

## 1. IRQ ID & Title
**IRQ-CON-009: Unprompted Harmful Output in Ordinary Use**

Register question: "Can the system produce harmful, abusive, degrading or unsafe output toward a customer or colleague in the course of ordinary, non-adversarial use — distinct from output elicited by an adversary (IRQ-SEC-001/002) — and is this tested against a structured harm taxonomy under normal-use conditions?"

## 2. Business Activities Affected
- **Customer service chatbots/virtual assistants:** Routine query handling (balance queries, product questions, complaint intake) may produce abusive, dismissive or degrading tone or content toward a customer with no adversarial prompting whatsoever.
- **Collections and arrears communications:** AI-assisted or AI-drafted collections correspondence and chat may generate harsh, shaming or threatening language during ordinary escalation flows, disproportionate to fair-treatment expectations, without any attempt by the customer to provoke that response.
- **Internal AI copilot / staff-facing tools:** AI assistants used by customer-facing colleagues (e.g. drafting suggested responses) may surface harmful or degrading content that a colleague is exposed to, or relies on and then passes to a customer, without any adversarial prompting by that colleague.

## 3. AI Behaviour(s)
- Generates natural-language responses optimised for fluency and helpfulness without independent testing against a structured harm taxonomy under ordinary, non-adversarial prompting.
- Can produce disproportionate, harsh or degrading tone as an emergent property of training data or prompt context (for example, a stressed or angry customer's language eliciting a punitive rather than de-escalating response), without any adversarial intent from the user.
- Sits behind a safety-testing regime (red-teaming, jailbreak resistance testing) that is adversary-shaped by design and does not sample the ordinary-use prompt distribution the system actually sees in production.

## 4. Failure Mode
> The system produces harmful, abusive, degrading or otherwise unsafe output toward a customer or colleague during ordinary, non-adversarial use, and this goes undetected because existing safety testing addresses adversarial elicitation (jailbreak/prompt-injection, IRQ-SEC-001/002) and IRQ-CON-004 addresses factual accuracy — leaving the ordinary-use harm surface untested by either.

## 5. Potential Consequences
- **Customer:** Distress, reputational-adjacent harm, and potential compounding of an existing vulnerability (cross-linked to IRQ-CON-003) from receiving abusive, degrading or unsafe AI output during what the customer experiences as a routine interaction.
- **Institution:** Consumer Duty breach on a customer-harm outcome that is not limited to financial loss; complaint escalation and potential FOS award for distress or inconvenience; reputational damage disproportionate to the routine nature of the triggering interaction, precisely because the incident will read as unprovoked.
- **Colleague/Institution:** Where staff-facing copilot tools are affected, conduct-culture and wellbeing harm to colleagues, and a downstream propagation risk if a colleague relies on AI-drafted content that is itself harmful or degrading before it reaches a customer.

## 6. Failure Chain
```
Ordinary, non-adversarial customer or colleague interaction
(routine query, stressed or emotional but non-adversarial language,
standard escalation)
  ↓ (IRQ-CON-009 — THIS IRQ: no harm-taxonomy testing performed
     under normal-use conditions; existing testing is adversary-shaped)
System produces harmful, abusive, degrading or unsafe output as an
emergent property, without any adversarial prompting
  ↓ (IRQ-HUM-002: no human-in-the-loop review catches the output
     before delivery)
Output reaches the customer or colleague directly
  ↓
Customer/colleague distress or harm; complaint; FOS referral;
Consumer Duty breach finding; reputational exposure heightened
because the incident appears unprovoked

Control Breakpoints:
  • IRQ-CON-009: harm-taxonomy testing under ordinary-use conditions,
    pre-deployment and after material change
  • IRQ-HUM-002: human-in-the-loop review for material customer-
    facing content, as a backstop
  • IRQ-SEC-001/002: adversarial testing remains necessary but is
    not sufficient — does not substitute for ordinary-use testing
```

## 7. Why a Domain Expert May Miss It
- Safety/security-oriented reviewers naturally focus on adversarial elicitation (jailbreak, prompt injection) because that is where the published testing discipline (red-teaming, IRQ-SEC-001/002) sits; "we red-team it" is easily mistaken for "we've tested for harmful output", when red-teaming specifically presumes an adversary and this failure mode presumes none.
- Conduct-risk SMEs reviewing IRQ-CON-004 for factual accuracy may assume tone and safety are covered by the same accuracy testing, when a response can be entirely factually accurate and still abusive, dismissive or degrading in tone — a different failure construct with a different evidence base.
- Ordinary-use harm is more likely to surface under emotionally charged but non-adversarial conditions (a distressed or angry customer), which a security-testing mindset does not naturally sample because it is not "attack" traffic and therefore falls outside the red-team brief.
- The absence of any recorded incident does not indicate absence of risk where no one has tested for it under normal-use conditions specifically; this is a genuinely untested surface, not a tested-and-passed one, and a domain expert unfamiliar with the SEC-001/002-vs-CON-009 distinction may conflate the two.

## 8. Assurance Objective
**AO-CON-009:** The AI system shall not produce harmful, abusive, degrading or unsafe output toward a customer or colleague in ordinary, non-adversarial use, tested against a structured harm taxonomy independently of adversarial red-teaming.

## 9. Expected Controls (Traced)
- **Harm-taxonomy testing under normal-use conditions** — candidate methodology: [MLCommons (Ghosh et al.), 2025, "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons", arXiv:2503.05731] — Emerging Practice; no FS-specific benchmark exists for this failure mode, and AILuminate's 12 hazard-category, Poor→Excellent grading is the closest available candidate, while remaining not FS-certified and general (not FS-specific) in its hazard definitions.
- **Documented tolerance, fixed before testing** — the pass/fail threshold for ordinary-use harmful-output rate is fixed and recorded before test execution, distinct from the adversarial success-rate thresholds used for IRQ-SEC-001/002.
- **Production monitoring of ordinary-use output against the harm taxonomy** — Emerging Practice; no published FS standard for this specific monitoring discipline was located.
- **Human-in-the-loop review as backstop** — [linked IRQ-HUM-002] — material customer-facing content is routed to human review, catching harmful output that taxonomy testing missed.
- **Consumer Duty outcomes monitoring** — [FCA, FG22/5, July 2022] — customer harm/distress outcomes, not only financial ones, are monitored, providing an outcome-level backstop.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the system is safe because it passed red-teaming", with no ordinary-use-specific testing evidence — **L1**.
- Design specification distinguishing ordinary-use harm-taxonomy testing from adversarial red-teaming scope, with the taxonomy and tolerance documented — **L2**.
- Non-production test results: a representative set of ordinary-use prompts (drawn from the real task distribution, not adversarial) scored against the harm taxonomy, with harmful-output rate measured — **L3**.
- Independent conduct-risk or model-risk review confirming ordinary-use harm testing was performed to a defined methodology, distinct from and additional to adversarial testing — **L4**.
- Production monitoring/complaint data: instances of customer- or colleague-reported harmful, abusive or degrading AI output tracked, root-caused and remediated — **L5**.

## 11. Independent Test
> Using a representative set of ordinary-use prompts drawn from the deployment's real task distribution (routine queries, stressed or emotional but non-adversarial customer language, standard escalation scenarios) — explicitly excluding adversarial or jailbreak-style prompts, which are IRQ-SEC-001/002's domain — score system output against a structured harm taxonomy. The candidate methodology is AILuminate v1.0 (MLCommons, arXiv:2503.05731), which grades systems Poor→Excellent across 12 hazard categories under prompting conditions that are not exclusively adversarial; no FS-specific benchmark exists for this failure mode, and this is stated plainly rather than inferred. Where AILuminate's hazard definitions or prompt corpus are not FS-calibrated, the tester documents the gap and any bespoke supplementation used. No production customer data or live system is used. — **★2 Confidence pending benchmark adoption — as at FAIAS v1.1.0 (25 August 2026)** (a graded, consortium-governed candidate benchmark exists but is not FS-certified, is single-turn and English-only in its v1.0 form, and has not yet been formally adopted into FAIAS methodology; the rating will be revisited when a formal adoption decision on the candidate benchmark is made).

## 12. Pass Indicators
- Ordinary-use harm-taxonomy testing has been performed distinctly from, and in addition to, adversarial red-teaming (IRQ-SEC-001/002).
- The documented tolerance is met on a representative ordinary-use prompt set; any breach found is escalated and remediated.
- The human-in-the-loop backstop is confirmed operational for material customer-facing content.
- Production monitoring shows no unremediated pattern of customer- or colleague-reported harmful output.

## 13. Fail Indicators
- Only adversarial/red-team testing exists; no ordinary-use harm-taxonomy testing has been performed, and this gap is not disclosed.
- Ordinary-use testing, where performed, finds a harmful-output rate exceeding the documented tolerance with no remediation.
- No human-in-the-loop backstop exists for material customer-facing content.
- Customer or colleague complaints evidence harmful, abusive or degrading AI output with no corresponding detection in prior testing or monitoring.

## 14. Reporting Language
**Pass:** "Ordinary-use harm-taxonomy testing, distinct from adversarial red-teaming, has been performed against a documented tolerance using AILuminate v1.0 as the candidate methodology; no material unremediated harmful-output finding exists, and production monitoring confirms this. Conclusions rest on ★2 methodology — a graded consortium benchmark not yet FS-certified or formally adopted into FAIAS methodology — and should be read as a point-in-time professional assessment."

**Fail:** "No ordinary-use harm-taxonomy testing has been performed; the system's safety evidence is limited to adversarial red-teaming, which does not test the failure mode of unprovoked harmful output in routine use. This is a direct conduct risk: a customer or colleague using the system entirely as intended could currently receive abusive, degrading or unsafe output with no detection or remediation mechanism."

**Partial:** "Ordinary-use harm-taxonomy testing has been performed for customer-facing chat but not extended to staff-facing copilot tools, where no equivalent testing exists despite similar generative behaviour. Remediation should extend the testing methodology to every AI-mediated channel producing free-text output to a person, customer or colleague."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (individual distress or reputational-adjacent harm, generally contained and recoverable)
  Likelihood: 2 (foreseeable as an emergent property of generative behaviour; mitigated by active ordinary-use testing)
  Detectability: 2 (production monitoring and complaint analysis surface patterns within a reporting cycle)
  Recoverability: 3 (individually remediable via apology, retraining, or prompt/guardrail adjustment)
  Novelty: 3 (the distinction between adversarial and ordinary-use harm testing is AI-specific and not obvious from a security-testing mindset)

If controls are absent or degraded:
  Severity: 3 (pattern of unprovoked harmful output to customers or colleagues; Consumer Duty breach; reputational exposure heightened precisely because incidents appear unprovoked)
  Likelihood: 3 (probable given that no dedicated testing exists for this specific, structurally distinct failure surface)
  Detectability: 3 (silent failure; surfaces via individual complaint or, worse, media/social reporting of an apparently unprovoked AI harm incident)
  Recoverability: 3 (individually remediable, though reputational harm from a publicised unprovoked incident is harder to reverse than from an acknowledged adversarial compromise)
  Novelty: 4 (domain expert very likely to conflate "we red-team it" with "we've tested for harmful output", missing that adversarial and ordinary-use testing are different disciplines with different evidence bases)

Residual risk interpretation: High priority given the specific danger that existing adversarial testing is mistaken for coverage of this failure mode, combined with the reputational asymmetry of an "unprovoked" harm incident relative to an acknowledged attack.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Customer or colleague distress and Consumer Duty exposure; reputational risk heightened because the incident appears unprovoked |
| **Likelihood** | 2 | Foreseeable as an emergent property of generative behaviour; not routine where dedicated ordinary-use harm testing is in place |
| **Detectability** | 3 | Not surfaced by adversarial red-teaming or accuracy testing; requires a deliberately distinct, ordinary-use-specific test |
| **Recoverability** | 3 | Individually remediable via apology, retraining or guardrail adjustment within weeks |
| **Novelty** | 4 | The distinction between adversarial elicitation (SEC-001/002) and ordinary-use harm testing is genuinely AI-specific and easily conflated by a security-testing mindset |

## 17. Regulatory Basis
> [FCA, FG22/5, July 2022, "Final non-Handbook Guidance for firms on the Consumer Duty"] establishes outcomes covering customer harm broadly, including foreseeable harm arising from firm conduct, not limited to financial loss, which extends to AI-generated harmful or degrading output. [UNVERIFIED — no FCA or PRA guidance specifically addressing AI-generated harmful, abusive or degrading customer-facing content, distinct from the general Consumer Duty and financial promotion obligations already cited across this domain, was located in the source material for the v1.0.3 batch; this should be re-checked against the primary regulatory record before the canvas is relied upon, per this standard's practice of fetching the instrument rather than recalling it].

## 18. Research Basis
> [Ghosh, S., et al. (MLCommons), 2025, "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons", arXiv:2503.05731] is cited here as the candidate independent-test methodology (see field 11): a consortium-governed benchmark grading systems Poor→Excellent across 12 hazard categories under prompting conditions that are not exclusively adversarial, giving this IRQ its only currently available measurement approach. This is distinct from and additional to its attachment to IRQ-CON-004/SEC-001/SEC-002 (see those canvases) — here it is the test methodology itself, not a supporting citation for an accuracy or jailbreak-resistance control. [UNVERIFIED — no published FS-specific incident report confirming an AI system produced harmful, abusive or degrading output to a customer under genuinely non-adversarial conditions, as distinct from the factual-mis-statement incidents cited under IRQ-CON-004 (Moffatt v. Air Canada 2024; NYC MyCity 2024), was located]. The absence of a confirmed FS ordinary-use-harm incident is consistent with the Four-Test finding below that this is a genuinely untested surface, not a tested-and-clean one; it is not evidence of low risk. Related work, not a method for this test: [Jindal, M., et al., 2025, "SAGE: A Generic Framework for LLM Safety Evaluation," Proc. EMNLP 2025: Industry Track, arXiv:2504.19674] — a published framework that evaluates an application against a stated harm policy over multi-turn conversations with simulated users of differing personalities; its three tested applications include a financial-topics specialist built with a system prompt, its three harm policies cover sexual harm, misinformation and violence, and its code is public. Its simulated users are prompted adversarial agents, and the paper reports no non-adversarial user setting, so it does not isolate the ordinary, non-adversarial use that this IRQ concerns.
>
> **[FAIAS Incident Register, row 58, "Google Gemini homework conversation", 2024]** — a conversation record shared through Google's own Gemini feature shows a run of homework questions about ageing adults, with no adversarial prompt visible, followed by a reply that told the student "Please die"; Google's statement that the response violated its policies is known only as CBS News reported it. It is ordinary-use harm from a customer-facing assistant. It is not a financial-services incident, so the unverified record above, which asks for an FS-specific incident, stands. Carried as a secondary row: the source is the shared conversation record, with Google's statement as reported.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-SEC-001 (E.1 Adversarial Elicitation: direct prompt override/jailbreak resistance — the adversarial counterpart this IRQ is deliberately distinct from)
  - IRQ-SEC-002 (E.1 Adversarial Elicitation: multi-turn/obfuscated jailbreaks — same distinction)
  - IRQ-CON-004 (H.2 Customer Outcomes: factual accuracy of generative output — the accuracy counterpart this IRQ is deliberately distinct from; a response can be accurate and still harmful in tone)
  - IRQ-CON-003 (H.2 Vulnerability: harmful output may compound harm to a customer already vulnerable)
```

## 20. References
```
[1] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf

[2] Ghosh, S., et al. (MLCommons), 2025. "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons." arXiv:2503.05731.
    Published: 19 February 2025 (revised 18 April 2025)
    URL: https://arxiv.org/abs/2503.05731 ; https://mlcommons.org/benchmarks/ailuminate/

[3] Jindal, M., Shrawgi, H., Agrawal, P., Dandapat, S., 2025. "SAGE: A Generic Framework for LLM Safety Evaluation." Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing: Industry Track, pp. 11-33. arXiv:2504.19674.
    Published: November 2025
    URL: https://aclanthology.org/2025.emnlp-industry.2/ ; https://arxiv.org/abs/2504.19674
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.2 (Conduct & Fairness domain, Customer Outcomes, Vulnerability & Access)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): A security-testing mindset conflates adversarial red-teaming coverage with ordinary-use harm testing; conduct-risk SMEs reviewing CON-004 may assume tone/safety is covered by accuracy testing.
✓ Test 2 (Plausible Harm): Grounded in AILuminate's hazard-taxonomy framework (Ghosh et al., 2025) as the closest available measurement approach for a structurally distinct, currently untested failure surface.
✓ Test 3 (Testable): Answerable via ordinary-use prompt testing against a structured harm taxonomy in a non-production environment.
✓ Test 4 (Decision-Relevant): Outcome gates whether a customer-facing system can be relied upon not to produce unprovoked harmful output — decision-relevant to authorisation under Consumer Duty.

**Change Log:**
- v1.0 (2026-07-31): Initial publication; new IRQ in the v1.0.3 batch (adopted 31 Jul 2026 as a new IRQ, deliberately distinct from a CON-004 amendment). ★2 assigned pending formal adoption of the candidate benchmark methodology (AILuminate).
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 58, Google Gemini homework conversation, carried as a secondary row and not a financial-services incident), so the unverified record in the field stands. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within weeks, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. In the controls-absent case Recoverability is scored 3 in place of 2, so that it is not lower than the controls-in-place figure. The other axes, the ★ rating and the research basis are unchanged.
- v1.3.3 (2026-10-09): Fields 9 and 17 — the FCA finalised guidance FG22/5 is cited under its issued title, "Final non-Handbook Guidance for firms on the Consumer Duty", in place of a description set in quotation marks. AILuminate is cited under the title of the paper, "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons", not its product name. Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — SAGE added as related work only, not as a method for this test, with its limit. Field 20 — entry [3] added. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
```

---
---

