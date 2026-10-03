# CANVAS: IRQ-CON-004

## 1. IRQ ID & Title
**IRQ-CON-004: Uncontrolled Generative Mis-Statement in Customer-Facing Content**

Register question: "Can generative outputs delivered to customers contain mis-statements about products, terms, fees or rights, and is pre-delivery accuracy control evidenced?"

## 2. Business Activities Affected
- **Customer service chatbots/virtual assistants:** Generative responses about product terms, fees, interest rates or customer rights may be factually incorrect (hallucinated or based on stale source material), and delivered directly to the customer without human review.
- **Marketing and product communications:** AI-drafted marketing copy or product descriptions may misstate terms, benefits or eligibility criteria, creating a misleading financial promotion.
- **Complaints and correspondence drafting:** AI-drafted responses to complaints may misstate the customer's rights (e.g. FOS referral rights, cancellation rights) or the firm's obligations.

## 3. AI Behaviour(s)
- Generates natural-language responses to customer queries or drafts customer-facing content by predicting plausible-sounding text, which can be fluent and confident while being factually incorrect.
- May draw on a knowledge base or retrieval source that is stale, incomplete, or mismatched to the specific product/customer, without a reliable signal to the customer or downstream reviewer that the content might be inaccurate.
- Where deployed without human-in-the-loop review before customer delivery, has no independent check on the accuracy of what is sent.

## 4. Failure Mode
> The system generates and delivers, or causes to be delivered, customer-facing content containing a material mis-statement about products, terms, fees or customer rights, without a pre-delivery accuracy control having caught the error before the customer received it.

## 5. Potential Consequences
- **Customer:** Customer relies on incorrect information (e.g. wrong fee, wrong cancellation window, wrong eligibility criterion) and suffers financial loss or makes a decision they would not otherwise have made.
- **Institution:** FCA Consumer Duty breach (consumer understanding and products/services outcomes); potential financial promotion rule breach if marketing content is affected; redress costs and reputational damage from a publicised misstatement incident.
- **Regulator:** Regulatory finding that generative AI content was deployed to customers without adequate accuracy control, undermining confidence in the firm's broader AI governance.

## 6. Failure Chain
```
Knowledge base/retrieval source is stale, incomplete or mismatched
to the specific product/customer context
  ↓ (IRQ-DAT-007/IRQ-MOD-004: retrieval staleness and hallucination
     risk, addressed in DAT/MOD domains)
Model generates fluent, confident but factually incorrect
customer-facing content
  ↓ (IRQ-CON-004 — THIS IRQ: no pre-delivery accuracy control exists,
     or exists but is not applied consistently to all channels/content
     types)
Content delivered directly to customer without human review
  ↓ (IRQ-HUM-002: human-in-the-loop review design gap)
Customer relies on incorrect information; financial loss or
unsuitable decision results
  ↓
Complaint; FOS referral; Consumer Duty consumer-understanding
breach finding

Control Breakpoints:
  • IRQ-CON-004: pre-delivery accuracy control (fact-checking,
    template-grounding, human review for material content) applied
    consistently across channels
  • IRQ-MOD-004: hallucination measurement and filtering upstream
  • IRQ-HUM-002: human-in-the-loop review design for material
    customer-facing content
```

## 7. Why a Domain Expert May Miss It
- A financial promotions or customer communications SME trained on human-drafted content review processes may assume the same review gate automatically applies to AI-generated content, when in practice generative AI content is often deployed at a volume and speed that bypasses traditional pre-approval review.
- Generative model outputs are typically fluent and confident in tone regardless of underlying accuracy, which can make an inaccurate response look indistinguishable from an accurate one to a reviewer without AI-specific hallucination awareness (this is the same underlying phenomenon as IRQ-MOD-004, applied specifically to customer delivery).
- "The knowledge base is accurate" is often verified once at build time; a domain expert may not appreciate that retrieval-augmented generation can still produce an inaccurate combination even from an accurate source, if retrieval selects the wrong document or the model synthesises across sources incorrectly.
- Low-stakes-seeming content (e.g. a chatbot answering "what is my overdraft fee") can carry high individual-customer financial consequence even though each individual interaction looks routine; the aggregate volume of small individual harms may not trigger conventional incident-severity thresholds.

## 8. Assurance Objective
**AO-CON-004:** Customer-facing generative content shall be subject to a pre-delivery accuracy control proportionate to the materiality of the content, such that mis-statements about products, terms, fees or rights are detected before customer delivery.

## 9. Expected Controls (Traced)
- **Pre-delivery accuracy/fact-checking control** — [linked IRQ-MOD-004, hallucination detection and filtering] — [OWASP Top 10 for LLM Applications 2025, LLM09 Misinformation (which subsumes the v1.1 "Overreliance" category)] — customer-facing generative output is checked against a source of truth before delivery, proportionate to content materiality.
- **Human-in-the-loop review for material content** — [linked IRQ-HUM-002] — [FCA, FG22/5, July 2022, Consumer Duty consumer-understanding outcome] — [Buçinca et al., 2021, "To Trust or to Think: Cognitive Forcing Functions," CSCW, DOI 10.1145/3449287] — content addressing terms, fees, rights or eligibility is routed to human review before delivery, or restricted to template-grounded (non-generative) responses for these topics.
- **Financial promotion compliance review extended to AI-generated marketing content** — [FCA, Handbook COBS 4, Financial Promotion rules] — AI-drafted marketing content is subject to the same approval gate as human-drafted content, with no AI-specific bypass.
- **Retrieval/knowledge-base accuracy and staleness control** — [linked IRQ-DAT-007] — the underlying source material is current and validated, as a precondition for any generative response to be reliably accurate.
- **Customer-understanding testing** — [FCA, FG22/5, July 2022] — Emerging Practice; testing whether generated content is not only factually accurate but also comprehensible to the actual customer population is less standardised than accuracy testing alone.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the chatbot is accurate" with no test evidence — **L1**.
- Design specification identifying which content topics (terms, fees, rights) require human review vs may be delivered generatively without review — **L2**.
- Non-production test results: a set of representative customer queries on terms/fees/rights run through the system, with factual accuracy independently checked against source documentation — **L3**.
- Independent compliance or internal audit review confirming the pre-delivery accuracy control operates as designed across all customer-facing channels — **L4**.
- Production monitoring/complaint analysis: instances of customer-reported inaccuracy in AI-generated content tracked, root-caused, and remediated — **L5**.

## 11. Independent Test
> Construct a representative set of customer queries covering material topics (fees, terms, cancellation/rights, eligibility) drawn from actual complaint themes or FAQ logs, and run them through the generative system in a non-production environment. Independently fact-check each response against current source documentation (product terms, tariff of charges, regulatory rights information) and record the material mis-statement rate. Separately assess whether the pre-delivery control (human review or template-grounding) would have caught each mis-statement found. No production customer data or live channel is used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (hallucination/accuracy testing draws on emerging but credible research methods; no single agreed FS benchmark exists for "customer-facing generative accuracy testing", and the materiality-topic taxonomy used is bespoke to the firm).

## 12. Pass Indicators
- A defined set of material topics (terms, fees, rights, eligibility) is routed to human review or restricted to template-grounded response, not open generative response.
- Independent fact-checking test finds no material mis-statement in sampled responses, or any found are caught by the pre-delivery control before customer delivery.
- Financial promotion review is confirmed to apply to AI-generated marketing content with no bypass.
- Production complaint analysis shows no unremediated pattern of AI-content-driven customer harm.

## 13. Fail Indicators
- No topic-based routing exists; generative responses are delivered on material topics (fees, rights, eligibility) without human review or grounding restriction.
- Independent fact-checking test finds a material mis-statement rate with no corresponding pre-delivery control that would have caught it.
- AI-generated marketing content is found to have bypassed the standard financial promotion approval gate.
- Customer complaints reveal a pattern of AI-content inaccuracy with no evidence of prior detection or remediation.

## 14. Reporting Language
**Pass:** "Material customer-facing topics (fees, terms, rights) are routed to human review or template-grounded response; independent fact-checking testing found no material unmitigated mis-statement risk. Conclusions rest on ★2 methodology — bespoke, professional-judgement-dominant testing with no agreed FS benchmark — and should be read as a point-in-time assessment."

**Fail:** "Generative responses on material topics (fees, terms, rights) are delivered directly to customers without human review or grounding restriction, and independent testing found a material mis-statement rate. This is a direct Consumer Duty risk: customers are currently receiving unchecked generative content on topics with direct financial consequence."

**Partial:** "Human review is applied to fee- and term-related queries but not to rights/eligibility queries, where testing found a non-trivial mis-statement rate. Remediation should extend the review gate to cover rights and eligibility content before the control can be relied upon comprehensively."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (individual customer financial loss or unsuitable decision, generally recoverable via correction)
  Likelihood: 2 (foreseeable given known hallucination tendency; mitigated by routing/review control)
  Detectability: 2 (customer complaint or periodic fact-checking audit surfaces issues within weeks)
  Recoverability: 2 (individually correctable via customer communication and, where needed, compensation)
  Novelty: 3 (generative fluency masking inaccuracy is an AI-specific phenomenon distinct from traditional human-drafted content error)

If controls are absent or degraded:
  Severity: 3 (multiple customers financially disadvantaged by systematic mis-statement; Consumer Duty and financial promotion breach risk)
  Likelihood: 3 (probable given demonstrated hallucination rates in generative systems absent grounding/review control)
  Detectability: 3 (silent failure; fluent incorrect content is not obviously distinguishable from correct content without independent fact-checking)
  Recoverability: 2 (individually remediable, though volume of small individual harms may only surface as a pattern late)
  Novelty: 4 (domain expert very likely to underestimate hallucination risk in fluent, confident-sounding generative output)

Residual risk interpretation: High priority given the direct financial-consequence pathway to individual customers and the high novelty of generative fluency masking inaccuracy to a non-AI-specialist reviewer.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Multiple customers may be financially disadvantaged by systematic generative mis-statement on material topics |
| **Likelihood** | 3 | Probable given demonstrated hallucination tendency absent grounding/review control on material topics |
| **Detectability** | 3 | Fluent incorrect content is not obviously distinguishable from correct content without independent fact-checking |
| **Recoverability** | 2 | Individually remediable via correction/compensation, though pattern-level harm may surface late |
| **Novelty** | 4 | Generative fluency masking factual inaccuracy is an AI-specific phenomenon outside traditional content-review experience |

## 17. Regulatory Basis
> [FCA, FG22/5, July 2022, "Consumer Duty final guidance"] requires firms to ensure customer communications support good understanding and do not mislead. [FCA, Handbook COBS 4, Financial Promotion rules] requires promotional content to be clear, fair and not misleading, and applies regardless of whether content is human- or AI-drafted. [UNVERIFIED — the FCA has published general AI positioning ("AI and the FCA: our approach," ongoing; AI Update, Apr 2024) but no GenAI-specific customer-communications rule beyond Consumer Duty/COBS 4 was located] (verified 29 Jul 2026).

## 18. Research Basis
> [Ji, Z., et al., 2023, "Survey of Hallucination in Natural Language Generation", ACM Computing Surveys (arXiv:2202.03629)] establishes the canonical taxonomy and prevalence of hallucination in generative systems, directly relevant to the risk that customer-facing content is fluent but inaccurate. [Magesh, V., et al., 2024, "Hallucination-Free? Assessing the Reliability of Leading AI Legal Research Tools", Stanford HAI/JELS (arXiv:2405.20362)] evidences that even commercial retrieval-grounded tools hallucinate in 17–33% of outputs, undermining any assumption that grounding alone controls customer-facing accuracy. [Incident register: Moffatt v. Air Canada, tribunal ruling Feb 2024 — chatbot invented a bereavement-fare policy and the firm was held liable for the mis-statement; NYC "MyCity" business chatbot, Mar–Apr 2024 — RAG grounding on official sources still produced unlawful guidance] — direct, documented incidents of customer-facing generative mis-statements crystallising as liability.
>
> [Abdulhai, Cheng, Shrivastava, Jaques, Gal & Levine, 2025, "Evaluating & Reducing Deceptive Dialogue From Language Models with Multi-turn RL", arXiv:2510.14318] introduces a human-validated belief misalignment metric, quantifying deceptive behaviour turn-by-turn across multi-turn dialogue and correlating more closely with human judgement than five established deception metrics. For customer-facing conversational systems, deception measured per turn across realistic multi-turn dialogue is a mechanism by which a customer's understanding of a product, fee or right can be progressively distorted, and the paper shows this occurs at material rates (~26% of turns) without any adversarial instruction — extending CON-004's mis-statement concern from single-message factual accuracy to cumulative belief distortion over a conversation. Where remediation is claimed, the paper's reported 77.6% reduction from multi-turn RL training against instruction-tuned baselines is a published reference point, not a FAIAS-adopted benchmark. Validated on four research dialogue scenarios, none of them regulated financial conversations; transfer to FS customer journeys is an inference the tester must justify.
>
> [Ghosh, S., et al. (MLCommons), 2025, "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons", arXiv:2503.05731] — a consortium-governed benchmark grading systems Poor→Excellent across 12 hazard categories, including a specialised-advice category covering unqualified financial advice. For customer-facing deployments this supplies a published, graded floor test that the system resists producing hazardous content — including out-of-scope financial advice — in the customer channel. **Boundary note (deliberate re-homing — see Change Log):** AILuminate grades a system's propensity to produce *harmful content* under hazard-eliciting prompts; it does not measure factual accuracy, hallucination rate or confidence calibration, and is attached here and to IRQ-SEC-001/IRQ-SEC-002, expressly **not** to IRQ-MOD-004 or IRQ-MOD-006. A system can score Excellent on AILuminate while confabulating freely — CON-004's accuracy controls (Ji et al. 2023; Magesh et al. 2024, above) remain separately evidenced and are not satisfied by an AILuminate result. v1.0 is single-turn and English-only by its own stated limitations; not FS-certified.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-MOD-004 (B.2 Hallucination: upstream hallucination measurement and filtering)
  - IRQ-HUM-002 (D.1: review gate design for material content)
  - IRQ-DAT-007 (A.3 Retrieval Data: staleness control as a precondition for accuracy)
  - IRQ-CON-003 (H.2 Vulnerability: compounding harm where a vulnerable customer receives an inaccurate response)
```

## 20. References
```
[1] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf

[2] Financial Conduct Authority. Handbook COBS 4, Financial Promotion rules.
    URL: https://www.handbook.fca.org.uk/handbook/COBS/4/

[3] OWASP, 2025. "OWASP Top 10 for LLM Applications 2025," LLM09 Misinformation.
    Published: 2024 (2025 edition)
    URL: https://genai.owasp.org/llm-top-10/ *(publisher's canonical page; it bot-blocks
    automated fetches — every fetch attempted returned HTTP 403, while OWASP's canonical
    GitHub Markdown repository serves the same content and was the route used for verification)*

[4] Ji, Z., et al., 2023. "Survey of Hallucination in Natural Language Generation." ACM Computing Surveys. arXiv:2202.03629.
[4a] Magesh, V., et al., 2024. "Hallucination-Free? Assessing the Reliability of Leading AI Legal Research Tools." Stanford HAI / Journal of Empirical Legal Studies. arXiv:2405.20362.
[4b] Civil Resolution Tribunal (BC), 2024. Moffatt v. Air Canada, 2024 BCCRT 149. Ruling 14 February 2024.

[5] Abdulhai, M., et al., 2025. "Evaluating & Reducing Deceptive Dialogue From Language Models with Multi-turn RL." arXiv:2510.14318.
    Published: 16 October 2025
    URL: https://arxiv.org/abs/2510.14318

[6] Ghosh, S., et al. (MLCommons), 2025. "AILuminate: Introducing v1.0 of the AI Risk and Reliability Benchmark from MLCommons." arXiv:2503.05731.
    Published: 19 February 2025 (revised 18 April 2025)
    URL: https://arxiv.org/abs/2503.05731 ; https://mlcommons.org/benchmarks/ailuminate/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.2 (Conduct & Fairness domain, Customer Outcomes, Vulnerability & Access)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Communications/compliance SMEs may assume traditional pre-approval review automatically applies to AI-generated content, when volume/speed often bypasses it.
✓ Test 2 (Plausible Harm): Grounded in hallucination research (Ji et al., 2023; Magesh et al., 2024), documented incidents (Moffatt v. Air Canada, 2024) and direct Consumer Duty/financial promotion regulatory exposure.
✓ Test 3 (Testable): Answerable via representative-query fact-checking testing in a non-production environment.
✓ Test 4 (Decision-Relevant): Outcome gates whether generative content can be delivered on material topics without human review.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.0.1 (2026-07): QA correction — removed unverifiable placeholder citation ("Ray et al., 2023", traced to a REVIEW_QUESTION_TEMPLATE.md illustrative example, not a real register source); replaced with register-backed research (Ji et al. 2023; Magesh et al. 2024) and documented incidents (Moffatt v. Air Canada 2024; NYC MyCity 2024).
- v1.0.2 (2026-07-31): Research Basis additions — Abdulhai et al. (2025) belief misalignment metric and AILuminate v1.0. AILuminate is a deliberate re-homing: it attaches here and to IRQ-SEC-001/IRQ-SEC-002, expressly not to IRQ-MOD-004 or IRQ-MOD-006, because it grades harmful-content propensity, not factual accuracy or calibration — recorded here to preserve the correction at review. No ★ change.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

