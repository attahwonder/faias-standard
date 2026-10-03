# CANVAS: IRQ-HUM-008

## 1. IRQ ID & Title
**IRQ-HUM-008: Absence of a Genuine Human Re-Decision Contest Route**

Register question: "Can an affected customer or colleague obtain a genuine human re-decision — not a re-run of the same model — through a defined contest route with tracked outcomes?"

## 2. Business Activities Affected
- **Underwriting review:** A declined applicant must be able to obtain a genuine reassessment of their application by a human underwriter exercising independent judgement, not merely a second pass of the same AI system with the same inputs.
- **Claims approval:** A customer disputing a settlement offer needs a contest route that results in a human re-evaluating the claim from the underlying evidence, not a re-run of the AI drafting process that produced the original offer.
- **AML case handling:** A colleague (e.g. a relationship manager) disputing an AI-driven account restriction on behalf of a customer needs a route to genuine human reconsideration of the underlying evidence, not a repeat of the automated screening.

## 3. AI Behaviour(s)
- Produces the initial decision or recommendation that the customer or colleague wishes to contest.
- May be the same system, potentially with the same inputs, invoked again when a "review" or "appeal" is requested, without any structural guarantee that a human independently re-derives the outcome.
- Provides no inherent signal distinguishing "this was re-run through the same automated pipeline" from "this was genuinely reconsidered by a human."

## 4. Failure Mode
> The contest route presented to customers or colleagues as an "appeal" or "review" in substance re-runs the same or a similar AI process on the same evidence, without a human genuinely reconsidering the decision from first principles, so the appeal cannot meaningfully change an incorrect outcome and the firm's contestability claim is not supported in practice.

## 5. Potential Consequences
- **Customer:** A genuinely wrong decision is not correctable through the appeal route, compounding the original harm and denying the customer the substantive review regulation and fairness principles are meant to guarantee.
- **Institution:** FOS findings that the firm's appeal/review process is not a genuine re-decision, with associated redress and process-redesign cost; reputational damage from the perception of a "computer says no, twice" pattern.
- **Regulator/market:** Regulatory concern (Consumer Duty, and by analogy EU AI Act contestability expectations) that AI-driven decisioning at scale is not matched by a genuine, scaled contestability mechanism, inviting supervisory scrutiny of the whole decisioning framework.

## 6. Failure Chain
```
Initial AI-influenced decision reached; customer/colleague requests
review or appeal
  ↓ (IRQ-HUM-006: if accountability for the original decision was
     never clearly attributable, it is unclear who should conduct the
     genuine re-decision)
Appeal route re-invokes the same or a similar AI process on the same
evidence, framed internally as "review" for operational convenience
  ↓ (IRQ-HUM-008 — THIS IRQ: contest route is not a genuine human
     re-decision — same inputs, same or similar model, same outcome)
Customer receives an "appeal outcome" that is procedurally distinct
but substantively identical to the original decision
  ↓ (IRQ-CON-008: transparency obligations are undermined if customers
     are not told the appeal process did not involve genuine human
     reconsideration)
Genuinely wrong original decisions are not correctable through the
route the firm presents as a remedy
  ↓
Customer complaint to FOS → FOS finds the appeal process was not a
genuine review → regulatory finding and redress across the affected
population

Control Breakpoints:
  • IRQ-HUM-006: clear accountability for who conducts the genuine
    re-decision, distinct from who/what produced the original decision
  • IRQ-HUM-008: contest route structurally requires human re-derivation
    from underlying evidence, not automated re-run, with outcomes
    tracked
  • IRQ-CON-008: transparent disclosure of what the appeal process
    actually involves
```

## 7. Why a Domain Expert May Miss It
- Assumption: "we have an appeals process, so contestability is satisfied" — the existence of a labelled appeals process is conflated with its substance; a process can be procedurally present and substantively non-functional simultaneously.
- Complaints-handling SMEs are trained on FOS process compliance (timeliness, communication standards, record-keeping) and may not have a natural checkpoint for asking whether the underlying re-decision was genuinely independent of the original automated process, since this question did not arise in pre-AI decisioning.
- Operational-efficiency pressure creates an unintentional incentive to make the appeal process resemble the original automated process as closely as possible, since building a genuinely separate human re-decision pathway is materially more resource-intensive — a cost/genuineness tension that is easy to resolve implicitly in favour of cost without a deliberate decision.
- Testing gap: appeal process quality is typically measured on timeliness and customer satisfaction with the communication, not on whether appeal outcomes ever actually differ from original outcomes at a rate consistent with genuine independent reconsideration.

## 8. Assurance Objective
**AO-HUM-008:** A defined contest route shall be available to affected customers and colleagues, structurally requiring a human decision-maker to independently re-derive the outcome from underlying evidence rather than re-running the same automated process, with outcomes tracked and monitored for a rate consistent with genuine independent reconsideration.

## 9. Expected Controls (Traced)
- **Structural separation of the appeal decision-maker and process from the original automated decisioning pipeline** — [FCA, DISP (Dispute Resolution: Complaints) Handbook] — the individual and process conducting the review are organisationally and procedurally distinct from the system that produced the original decision.
- **Appeal-outcome divergence-rate monitoring** — [linked IRQ-HUM-001; NIST AI RMF 1.0, MANAGE-4, Jan 2023, adapted] — the rate at which appeal outcomes differ from original outcomes is tracked; a rate at or near zero on a system with a known non-zero error rate is a red flag for a non-genuine appeal process, mirroring the disagreement-rate logic of IRQ-HUM-001.
- **EU AI Act contestability-adjacent transparency requirement** — [EU AI Act, Regulation (EU) 2024/1689, Article 13, Aug 2024] — while the Act does not create a standalone "right to contest," the transparency obligations it imposes support a customer's ability to understand and meaningfully challenge an AI-influenced decision.
- **FCA Consumer Duty fair-value and good-outcomes standard applied to the appeal process itself** — [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] — the appeal process itself is a customer-facing service subject to the Duty's good-outcomes expectation, not merely the original decision.
- **Transparent disclosure of what the review process involves** — [linked IRQ-CON-008; FCA, Handbook PRIN 2A] — customers are told, in comprehensible terms, whether their appeal will involve genuine human reconsideration and what evidence will be re-examined.

## 10. Expected Evidence (Tagged L1–L5)
- Customer-facing documentation stating "you can appeal any decision" — **L1**.
- Documented appeal-process design specifying the decision-maker's independence from the original automated pipeline — **L2**.
- Process walkthrough/design review confirming the appeal workflow structurally routes to a human re-derivation step, not an automated re-run — **L3**.
- Staging test: a sample of dev/test appeal cases run through the actual appeal workflow, confirming the underlying evidence (not just the AI's prior output) is genuinely re-examined — **L3**.
- Independent audit of historical appeal-outcome divergence rate compared against the AI system's known error rate — **L4**.
- Production data: appeal-outcome divergence rate trended over a sustained period, with any decline investigated — **L5**.

## 11. Independent Test
> In a non-production environment, construct a set of dev/test cases with a known ground truth, seeded with a defined proportion of deliberately incorrect original AI decisions, and route these through the firm's actual appeal/review workflow as if genuinely contested. Measure whether the appeal process correctly overturns the seeded-incorrect decisions, and separately measure whether the appeal decision-maker is presented with, and engages with, underlying evidence beyond the AI's original output and rationale. Compare the appeal workflow's process steps against the original decisioning workflow to confirm structural (not merely nominal) separation. Executed entirely on de-identified dev/test case files; no live customer appeals are affected. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (adapts the established seeded-error paradigm from IRQ-HUM-001, itself ★3, to the appeal-specific context; the FS-specific application to contestability testing is bespoke with no agreed benchmark, and process-separation assessment relies on assessor judgement of what constitutes "structural" versus "nominal" separation).

## 12. Pass Indicators
- The appeal workflow correctly overturns the large majority of seeded-incorrect original decisions in the test.
- The appeal decision-maker is shown to engage with underlying evidence, not only the AI's original output and rationale, evidenced in case notes or workflow logs.
- The appeal process is structurally (organisationally and procedurally) distinct from the original decisioning pipeline.
- Production appeal-outcome divergence rate is non-zero and consistent with the AI system's known error rate.
- Customers are told in comprehensible terms what the appeal process involves.

## 13. Fail Indicators
- The appeal workflow fails to overturn a material proportion of seeded-incorrect original decisions, indicating the appeal process reproduces the original error.
- The appeal decision-maker's workflow provides only the AI's original output and rationale, with no route to independently examine underlying evidence.
- The appeal process shares the same system, prompt or pipeline as the original decision with no structural separation.
- Production appeal-outcome divergence rate is at or near zero despite a known non-zero AI error rate.
- Customers are told an appeal is available with no disclosure of what the review substantively involves.

## 14. Reporting Language
**Pass:** "Seeded-error testing of the appeal workflow shows the large majority of deliberately incorrect original decisions are correctly overturned, and the appeal decision-maker demonstrably engages with underlying evidence beyond the AI's original rationale. The appeal process is structurally distinct from the original decisioning pipeline. This is a ★2 assessment — adapts an established seeded-error paradigm to a bespoke contestability context — and should be re-tested at each material change to either workflow."

**Fail:** "Seeded-error testing shows the appeal workflow reproduces the majority of deliberately incorrect original decisions unchanged, and the appeal decision-maker's workflow provides no route to examine evidence beyond the AI's original output. This indicates the appeal process functions as a re-run of the original automated decision rather than a genuine human re-decision, and the firm's contestability claim is not supported in substance; remediation should structurally separate the appeal process before continued customer-facing representation of an 'appeal' being available."

**Partial:** "The appeal workflow correctly overturns seeded errors for [decision type A] but not [decision type B], where the appeal process was implemented as an automated escalation rather than a genuine human re-decision route. Remediation should redesign the [decision type B] appeal path before continued reliance."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (an ineffective appeal route does not itself cause the
    original harm but denies correction, compounding harm for
    affected individuals who sought redress)
  Likelihood: 2 (unlikely to be material if divergence-rate monitoring
    and structural separation are actively maintained)
  Detectability: 2 (detectable via divergence-rate monitoring and
    periodic seeded-error testing, ahead of a FOS finding)
  Recoverability: 2 (reversible via appeal-process redesign once
    identified; days-to-weeks)
  Novelty: 3 (domain expert assumes a labelled appeals process
    satisfies the fairness/contestability requirement; testing whether
    the appeal is structurally independent of the original AI process
    is not standard complaints-handling audit practice)

Residual risk interpretation: Acceptable with active divergence-rate
monitoring and periodic seeded-error testing, ideally sharing
infrastructure with IRQ-HUM-001's programme; the operational-efficiency
pressure toward a non-genuine appeal process is a recurring dynamic
requiring ongoing vigilance, not a one-off design decision.

If controls are absent or degraded:
  Severity: 3 (genuinely wrong decisions across the customer population
    have no working correction mechanism, compounding harm at scale)
  Likelihood: 3 (probable given the operational-efficiency incentive to
    make the appeal process resemble the original automated process)
  Detectability: 3 (invisible until FOS or a forensic audit examines
    appeal-outcome divergence specifically)
  Recoverability: 3 (multi-week remediation; FOS redress across the
    affected population of appellants)
  Novelty: 4 (customer-facing documentation asserts an appeal is
    available with no divergence-rate evidence that it functions; the
    gap is invisible without today's specific seeded-error test)

Residual risk: High. Directly compounds any harm identified in
IRQ-HUM-001/002/006/007, since it removes the correction mechanism the
firm and customers depend on when the primary controls fail.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Does not itself cause the original harm but denies correction, compounding harm for individuals who sought redress; escalates with volume |
| **Likelihood** | 3 | Probable given the operational-efficiency incentive to make appeal processes resemble the original automated pipeline absent active monitoring |
| **Detectability** | 2 | Detectable via divergence-rate monitoring and periodic seeded-error testing, ahead of a FOS finding, if such monitoring is active |
| **Recoverability** | 2 | Reversible via appeal-process redesign once identified, typically within weeks |
| **Novelty** | 3 | Domain expert assumes a labelled appeals process satisfies the requirement; structural-independence testing of the appeal route is not standard complaints-handling audit practice |

## 17. Regulatory Basis
> [FCA, DISP (Dispute Resolution: Complaints) Handbook] governs complaints-handling process requirements, which this canvas interprets as requiring substantive, not merely procedural, review where an AI-influenced decision is contested. [FCA, Handbook PRIN 2A, Consumer Duty, Jul 2023] applies the good-outcomes standard to the appeal process itself. [EU AI Act, Regulation (EU) 2024/1689, Article 13, Aug 2024] transparency obligations support a customer's ability to meaningfully challenge a decision, though the Act does not create a standalone contestability right; this is noted as an interpretive extension, not a direct requirement. Section pinpoints [UNVERIFIED — cited modules (SYSC 4, SYSC 9, SYSC 15A, PRA SS1/21/PS21/3, EU AI Act Art. 14 — SYSC 19D removed 25 Aug 2026: it is the dual-regulated firms Remuneration Code and was mis-cited; SYSC 4.1.1R substituted, verified from the Handbook) confirmed extant on FCA Handbook/BoE/eur-lex; no AI-specific sub-clause pinpoint published by the regulator to cite beyond module level] (verified 29 Jul 2026).

## 18. Research Basis
> [Vaccaro, K., Sandvig, C. & Karahalios, K., 2020, "'At the End of the Day Facebook Does What It Wants': How Users Experience Contesting Algorithmic Content Moderation", CSCW 2020] documents user experience of algorithmic-decision contestation processes that are procedurally present but substantively unresponsive, directly analogous to this IRQ's failure mode. [Lyons, H., Velloso, E. & Miller, T., 2021, "Conceptualising Contestability: Perspectives on Contesting Algorithmic Decisions", CSCW 2021] provides the conceptual framework distinguishing genuine contestability (ability to change the outcome) from mere notice-and-appeal-in-name, informing the pass/fail criteria used here.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-006 (D.4 Accountability & Contestability: accountability
    for the original decision, prerequisite for a genuine re-decision)
  - IRQ-HUM-001 (D.1 Automation Bias: shared seeded-error test
    infrastructure, applied here to appeal-outcome divergence)
  - IRQ-CON-008 (H.3 Feedback Loops & Transparency: disclosure of what
    the appeal process substantively involves)
  - IRQ-CON-003 (H.2 Customer Outcomes, Vulnerability & Access:
    vulnerable-customer treatment within the appeal route specifically)
  - IRQ-CON-010 (H.2 Customer Outcomes, Vulnerability & Access:
    the effort required to reach the contest route, and friction in
    the wider journey, as distinct from the route's own adequacy)
```

## 20. References
```
[1] Vaccaro, K., Sandvig, C. & Karahalios, K., 2020. "'At the End of the Day Facebook Does What It Wants': How Users Experience Contesting Algorithmic Content Moderation." Proceedings of the ACM on Human-Computer Interaction, CSCW 2020.
    Accessed: 2026-07-29

[2] Lyons, H., Velloso, E. & Miller, T., 2021. "Conceptualising Contestability: Perspectives on Contesting Algorithmic Decisions." Proceedings of the ACM on Human-Computer Interaction, CSCW 2021.
    Accessed: 2026-07-29

[3] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Article 13."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[4] Financial Conduct Authority. "DISP: Dispute Resolution: Complaints" and "Handbook PRIN 2A: The Consumer Duty."
    URL: https://www.handbook.fca.org.uk/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.4 (Human Oversight, Accountability & Contestability)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs treat a labelled appeals process as satisfying contestability; complaints-handling audit practice checks timeliness and communication, not structural independence from the original automated pipeline.
✓ Test 2 (Plausible Harm): Grounded in Vaccaro et al.'s (2020) documented user experience of unresponsive algorithmic appeal processes and Lyons, Velloso & Miller's (2021) contestability framework.
✓ Test 3 (Testable): Answerable via seeded-error testing of the appeal workflow specifically, adapted from IRQ-HUM-001's methodology.
✓ Test 4 (Decision-Relevant): Directly determines whether the firm's contestability claim is substantively true, gating whether the appeal process requires structural redesign.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 19 — IRQ-CON-010 added as the reciprocal cross-reference, delineated as the effort required to reach the contest route, and friction in the wider journey, as distinct from the route's own adequacy. No other field changed; ★2 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

