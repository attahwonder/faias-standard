# CANVAS: IRQ-CON-008

## 1. IRQ ID & Title
**IRQ-CON-008: Absent or Inadequate Disclosure of Material AI Influence on Customer Decisions**

Register question: "Are customers told, in a comprehensible way, when AI materially influences decisions or interactions affecting them, consistent with regulatory expectations?"

## 2. Business Activities Affected
- **Credit and insurance decisioning:** Customers may not be told that an AI system materially influenced a decline, price or term, undermining their ability to understand and, where relevant, contest the basis for the decision.
- **Customer service and complaint handling:** Customers interacting with an AI chatbot or virtual assistant may not be clearly told they are interacting with an automated system, or that AI drafted a response subsequently sent under human sign-off.
- **Marketing and personalisation:** Customers may not understand that AI-driven personalisation is shaping the products, prices or content they are shown, differently from other customers.

## 3. AI Behaviour(s)
- Materially influences a decision or interaction outcome (decline, price, content, routing) without a corresponding, comprehensible disclosure being generated or delivered to the affected customer.
- May operate in combination with human sign-off (human-in-the-loop) in a way that technically satisfies "a human made the decision" while the AI's influence on that human's judgement was substantial and undisclosed.
- Disclosure, where it exists, may be delivered in generic terms-and-conditions language rather than tested for comprehension by the actual customer population at the point of the AI-influenced interaction.

## 4. Failure Mode
> A customer is subject to a decision or interaction materially influenced by AI without receiving disclosure that is both present and comprehensible at the relevant point, such that the customer cannot understand, and where applicable exercise their right to contest, the basis for the outcome.

## 5. Potential Consequences
- **Customer:** Customer is unaware that AI shaped an outcome affecting them, and therefore does not know that a contest/override route (per IRQ-HUM-008) may exist, or lacks the context needed to exercise it effectively.
- **Institution:** FCA Consumer Duty consumer-understanding outcome breach; broader transparency/AI-governance credibility risk if a lack of disclosure is publicised, particularly given rising customer and media attention to AI use in financial services.
- **Regulator:** Regulatory finding that AI-use disclosure is inadequate, undermining the firm's broader claim of contestability and accountability (cross-linked to HUM-007/HUM-008).

## 6. Failure Chain
```
AI materially influences a decision or interaction outcome
  ↓ (IRQ-CON-008 — THIS IRQ: no disclosure is generated, or
     disclosure exists only in generic T&Cs, untested for
     comprehension at the point of the actual interaction)
Customer is unaware AI materially shaped the outcome
  ↓ (IRQ-HUM-007: customer lacks the explanation content needed
     to exercise independent judgement)
Customer does not know a contest/human-re-decision route may be
available, or cannot frame a meaningful contest without understanding
AI's role
  ↓ (IRQ-HUM-008: contest route, even if technically available,
     goes unused because the customer doesn't know to invoke it)
Customer accepts an outcome they might otherwise have contested;
harm goes unaddressed and invisible to the firm

Control Breakpoints:
  • IRQ-CON-008: AI-use disclosure generated and delivered at the
    point of the material interaction, tested for comprehension
  • IRQ-HUM-007: explanation content sufficiency tested with the
    actual user population
  • IRQ-HUM-008: contest route is genuinely accessible once a
    customer is aware AI was materially involved
```

## 7. Why a Domain Expert May Miss It
- Compliance and legal SMEs often equate "disclosed" with "included in the terms and conditions or privacy notice", which satisfies a narrow legal-disclosure test but not the Consumer Duty's higher bar of tested comprehension at the point of the actual interaction.
- Where a human formally signs off a decision that was substantially AI-drafted or AI-recommended, a domain expert may treat the interaction as "human decision, no AI disclosure needed" without examining how much the AI actually shaped the human's judgement — this is the same underlying issue as automation bias (HUM-001), but from the customer transparency angle rather than the reviewer-behaviour angle.
- Product and technology teams may treat "the customer knows they're using a chatbot" (interface-level disclosure) as equivalent to "the customer understands AI materially influenced the substantive decision they cared about" (outcome-level disclosure) — these are different disclosures and satisfying one does not satisfy the other.
- Disclosure comprehension testing is a specific and non-trivial user-research discipline; a domain expert accustomed to legal-sufficiency review (does the wording exist and is it accurate) may not think to test whether real customers actually understand it.

## 8. Assurance Objective
**AO-CON-008:** Where AI materially influences a decision or interaction affecting a customer, the firm shall provide disclosure that is present at the relevant point and comprehensible to the actual customer population, tested rather than merely asserted.

## 9. Expected Controls (Traced)
- **Point-of-interaction AI-use disclosure** — [FCA, FG22/5, July 2022, Consumer Duty consumer-understanding outcome] — disclosure is delivered at the point of the material interaction, not only in generic terms and conditions.
- **Comprehension testing of disclosure content** — [FCA, FG22/5, July 2022, requiring communications to be tested for understanding with the actual target audience, not merely reviewed for legal accuracy] — Emerging Practice specifically for AI-use disclosure; comprehension testing methodology for this specific disclosure type is less standardised than for general product communications.
- **Substantive-influence disclosure distinct from interface-level disclosure** — Emerging Practice; explicitly distinguishing "you are talking to a chatbot" from "AI materially shaped this decision", and testing whether the latter — the one that matters for contestability — is actually delivered.
- **Human-sign-off transparency** — [linked IRQ-HUM-007/IRQ-HUM-008] — where a human formally signs off an AI-recommended decision, the degree of AI influence on that judgement is itself assessed and, where material, disclosed.
- **Contest-route signposting alongside disclosure** — [linked IRQ-HUM-008] — AI-use disclosure is paired with clear signposting of the available contest/human-re-decision route, not delivered as a standalone notice.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "AI use is disclosed in our privacy notice/T&Cs" with no point-of-interaction or comprehension evidence — **L1**.
- Design documentation specifying where and how point-of-interaction AI-use disclosure is delivered for each material decision/interaction type — **L2**.
- Non-production comprehension test results: a representative sample of customers reviews the disclosure and is assessed for understanding of (a) AI's material role and (b) the availability of a contest route — **L3**.
- Independent conduct-risk or internal audit review confirming disclosure design and comprehension testing meet an internally defined bar across all material AI-influenced interaction types — **L4**.
- Production data: complaint or customer query analysis assessing whether customers report awareness (or lack of awareness) of AI's role at the point they seek to contest a decision — **L5**.

## 11. Independent Test
> Using a representative sample of actual or recruited customers (or, where live customer testing is infeasible, a closely matched panel), present the AI-use disclosure as currently delivered at the point of a material interaction (e.g. a credit decline, a price quote, a chatbot-drafted response) and assess, via structured comprehension questions, whether participants understand (a) that AI materially influenced the outcome and (b) that a contest/human-re-decision route exists and how to access it. Non-production test; no live customer decisioning affected. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (Consumer Duty comprehension-testing methodology is established generally for customer communications — ★3 for that general component; testing specifically for AI-influence comprehension is a newer, bespoke application with no agreed FS benchmark — blended rating reflects the more novel component).

## 12. Pass Indicators
- Point-of-interaction disclosure exists for all material AI-influenced decision/interaction types, distinct from generic T&Cs disclosure.
- Comprehension testing demonstrates a defined, documented threshold of customer understanding of AI's material role and the availability of a contest route.
- Human-sign-off interactions have been assessed for degree of AI influence, with material influence disclosed rather than assumed covered by "a human decided".
- Contest-route signposting is paired with the disclosure, not delivered separately or omitted.

## 13. Fail Indicators
- Disclosure exists only in generic terms and conditions or privacy notice language, with no point-of-interaction delivery for material decisions.
- No comprehension testing has been performed; disclosure adequacy is asserted based on legal-sufficiency review alone.
- Human-sign-off interactions are treated as requiring no AI disclosure regardless of how substantially the AI shaped the human's judgement.
- Customers report, via complaints or queries, being unaware AI was materially involved in a decision they are trying to contest.

## 14. Reporting Language
**Pass:** "Point-of-interaction AI-use disclosure is delivered for all material AI-influenced decisions, comprehension testing confirms customers understand both AI's role and the availability of a contest route, and human-sign-off interactions have been assessed for degree of AI influence. Conclusions rest on ★2 methodology — established comprehension-testing practice applied to a bespoke, less-standardised AI-influence-specific test — and should be read as a point-in-time professional assessment."

**Fail:** "AI-use disclosure exists only within generic terms and conditions; no point-of-interaction disclosure or comprehension testing has been performed for material AI-influenced decisions. This is a direct Consumer Duty consumer-understanding risk: customers currently have no meaningful basis to know AI materially shaped a decision affecting them, undermining their ability to exercise a contest route even where one technically exists."

**Partial:** "Point-of-interaction disclosure exists for credit decisioning and comprehension testing confirms adequate understanding, but chatbot-drafted correspondence subsequently issued under human sign-off carries no equivalent disclosure of the AI's substantive drafting role. Remediation should extend disclosure and comprehension testing to this interaction type."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (individual customer lacks full context but underlying decision quality is not itself necessarily impaired; primarily a transparency/contestability gap)
  Likelihood: 2 (foreseeable given the common gap between interface-level and substantive-influence disclosure; mitigated where comprehension testing is active)
  Detectability: 2 (comprehension testing and complaint-pattern monitoring surface gaps within a reporting cycle)
  Recoverability: 2 (remediable via disclosure redesign and re-testing within weeks to months)
  Novelty: 3 (distinguishing interface-level from substantive-influence disclosure, and testing the latter's comprehension specifically for AI, is a genuinely newer discipline)

If controls are absent or degraded:
  Severity: 3 (systemic undermining of contestability across all AI-influenced decisions; Consumer Duty and accountability-framework breach)
  Likelihood: 3 (probable given the common conflation of generic T&Cs disclosure with tested, point-of-interaction, substantive disclosure)
  Detectability: 3 (silent failure from the firm's perspective; typically surfaces only via complaint escalation or thematic review specifically probing AI transparency)
  Recoverability: 2 (remediable via disclosure redesign, though prior undisclosed decisions may warrant retrospective review)
  Novelty: 4 (domain expert very likely to treat generic legal disclosure as sufficient, missing the comprehension and point-of-interaction requirements entirely)

Residual risk interpretation: Moderate-to-high priority; while individual severity is more contained than some other CON IRQs, this failure mode directly undermines the effectiveness of the accountability/contestability framework (HUM-007/HUM-008) that other controls rely upon as a backstop, so its systemic importance exceeds its standalone severity rating.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Systemic undermining of contestability across all AI-influenced decisions; directly weakens the accountability backstop other controls rely upon |
| **Likelihood** | 3 | Probable given the common conflation of generic legal disclosure with tested, point-of-interaction, substantive-influence disclosure |
| **Detectability** | 3 | Silent from the firm's perspective; typically surfaces only via complaint escalation or thematic review specifically probing AI transparency |
| **Recoverability** | 2 | Remediable via disclosure redesign and re-testing within weeks to months |
| **Novelty** | 4 | Domain expert very likely to treat generic legal/T&Cs disclosure as sufficient, missing the comprehension and point-of-interaction requirements |

## 17. Regulatory Basis
> [FCA, PS22/9, July 2022, and FG22/5, July 2022, "Consumer Duty final guidance"] establishes the consumer-understanding outcome, requiring communications to be tested for comprehension with the actual target audience, and requires customers to have the information they need, when they need it. [UNVERIFIED — no FCA-specific AI transparency/disclosure guidance beyond the general Consumer Duty communications requirement and the general "AI and the FCA: our approach" position was located] (verified 29 Jul 2026).

## 18. Research Basis
> [Belton, C., Bogiatzis-Gibbons, D., Keeley, I., Spang, J., Turkay, C. & Pi, Y., "Credit where credit is due: How can we explain AI's role in credit decisions for consumers?" FCA Research Note, 24 February 2025] is FS-specific, empirical and directly on point. In a UK regulator experimental study, participants tried to identify errors (bad input data versus flawed algorithm logic) in AI-assisted credit decisions under different explanation designs; the explanation method significantly affected — and in the data-error condition, impaired — participants' ability to detect errors, and participants' self-reported confidence rose even as actual error-detection performance fell. This is the mechanism this claim is concerned with directly: disclosure and explanation can raise a customer's confidence in an AI-influenced decision while lowering their actual ability to identify when it is wrong, so disclosure that is merely present is not evidence that it is comprehended or that it functions as a check.
>
> [Consumer Financial Protection Bureau, "Chatbots in consumer finance," 6 June 2023] provides supporting, if qualitative, US evidence that chatbots' limited nature and lack of human escalation "may not be apparent" to customers signing up for a financial relationship — a disclosure-awareness gap evidenced via complaint-database review rather than a representative comprehension test, and consistent in direction with, but weaker than, Belton et al.
>
> **Research basis last reviewed:** 25 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-007 (D.4 Accountability & Contestability: explanation adequacy tested with actual users)
  - IRQ-HUM-008 (D.4 Accountability & Contestability: functioning contest/human-re-decision route)
  - IRQ-CON-006 (H.2 Price Fairness: disclosure of AI's role in pricing specifically)
  - IRQ-CON-010 (H.2 Customer Outcomes, Vulnerability & Access:
    disclosure of AI's material influence is necessary and not
    sufficient where the journey separately frictions exit;
    TP-CON-008's non-production journey reproduction is the nearest
    adjacent procedure)
```

## 20. References
```
[1] Financial Conduct Authority, 2022. "PS22/9 — A new Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publications/policy-statements/ps22-9-new-consumer-duty

[2] Financial Conduct Authority, 2022. "FG22/5 — Final non-Handbook Guidance for firms on the Consumer Duty."
    Published: July 2022
    URL: https://www.fca.org.uk/publication/finalised-guidance/fg22-5.pdf
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** H.3 (Conduct & Fairness domain, Feedback Loops & Transparency)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Compliance SMEs commonly equate generic T&Cs disclosure with tested, point-of-interaction, substantive AI-influence disclosure — these are materially different bars.
✓ Test 2 (Plausible Harm): Grounded directly in the FCA's Consumer Duty consumer-understanding outcome and its comprehension-testing requirement.
✓ Test 3 (Testable): Answerable via structured comprehension testing of disclosure content with a representative customer sample.
✓ Test 4 (Decision-Relevant): Outcome gates whether the firm's contestability framework (HUM-007/008) can function as intended, since customers must first know AI was involved.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Field 19 — IRQ-CON-010 added as the reciprocal cross-reference (disclosure of AI's material influence is necessary and not sufficient where the journey separately frictions exit; TP-CON-008's non-production journey reproduction is the nearest adjacent procedure). No other field changed; ★2 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

