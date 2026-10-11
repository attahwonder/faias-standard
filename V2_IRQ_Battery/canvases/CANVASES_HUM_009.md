# CANVAS: IRQ-HUM-009

## 1. IRQ ID & Title
**IRQ-HUM-009: Evidential Standard for AI-Triggered Adverse Allegations**

Register question: "Where AI output initiates, or materially contributes to, an adverse allegation, decision or sanction against a customer or colleague, is the evidential standard applied to that output defined and proportionate to the consequence — is the underlying evidence and reasoning disclosed to the subject, and is the subject relieved of any burden to disprove the system before the adverse action takes effect?"

## 2. Business Activities Affected
- **Fraud and financial-crime case management:** An AI system flags a transaction, application or customer as suspected fraud; the flag alone triggers account restriction, a suspicious activity report or a law-enforcement referral, with no defined threshold for how much corroborating evidence is required before that step.
- **Credit and account decisioning:** An AI-generated risk score or anomaly classification drives a decline, account closure or repayment demand framed as suspected misconduct rather than ordinary credit risk, without the customer being shown the basis for the distinction.
- **Colleague conduct and surveillance-driven investigations:** AI-generated communications surveillance or anomaly detection initiates a disciplinary or conduct investigation against an employee, treated by the investigating manager as sufficient grounds on its own rather than as one input requiring corroboration.

## 3. AI Behaviour(s)
- Generates a flag, score or classification (fraud, misconduct, ineligibility) presented alongside a rationale, in a register that reads as an evidenced finding rather than a probabilistic signal.
- Produces no standardised statement of the evidential basis, confidence or limitations underlying the flag that is distinguishable from an ordinary risk score used for routine decisioning.
- Is embedded in a workflow where a human "reviews and actions" the flag as a required step, but that step is not designed around a defined evidential threshold, disclosure obligation or burden-of-proof rule.

## 4. Failure Mode
> An adverse allegation, decision or sanction against a customer or colleague is initiated or materially driven by AI output that a human decision-maker treats as sufficient evidence on its own, with no defined evidential-sufficiency threshold, no disclosure of the underlying evidence and reasoning to the subject, and no explicit rule keeping the burden of justifying the action with the institution rather than requiring the subject to disprove the system.

## 5. Potential Consequences
- **Customer/colleague:** Wrongly sanctioned — account restriction, debt demand, disciplinary action, referral to a third party — with no visibility of the basis for the allegation and no practical route to rebut it before the action takes effect.
- **Institution:** Findings of unfair or unlawful process where the same undisclosed, evidentially unsupported practice affected a batch of cases; large-scale redress and remediation cost; individual accountability exposure for the manager who actioned the flag.
- **Market/regulator:** Precedent scrutiny of every AI-triggered adverse-action process the firm operates, once one instance of AI output being wrongly treated as dispositive evidence is demonstrated.

## 6. Failure Chain
```
AI generates a fraud, misconduct or ineligibility flag with a
confident, evidence-styled rationale
  ↓ (IRQ-MOD-006: confidence not calibrated to actual accuracy of the
     flag)
No defined evidential-sufficiency threshold exists for what "enough"
looks like before the flag can support adverse action
  ↓ (IRQ-HUM-009 — THIS IRQ: evidential standard absent — flag treated
     as dispositive on its own)
Adverse action proceeds; subject is not shown the underlying evidence
and reasoning, or only on request/after complaint
  ↓ (IRQ-HUM-008: even where a contest route exists, the subject has
     nothing concrete to contest — the appeal route is meaningless
     without disclosure)
Subject bears the practical burden of disproving a system they cannot
see inside
  ↓
Wrongful sanction → complaint or investigation reveals no disclosed
evidential basis → regulatory/reputational finding

Control Breakpoints:
  • IRQ-HUM-009: a documented, proportionate evidential-sufficiency
    threshold applied before AI output can support adverse action
  • IRQ-HUM-009: disclosure of the evidence and reasoning to the
    subject as a matter of course, not on request
  • IRQ-HUM-008: a genuine contest route, which depends on this IRQ's
    disclosure control to be meaningful
  • IRQ-GOV-010: record-keeping sufficient to reconstruct the evidence
    and reasoning behind the original flag
```

## 7. Why a Domain Expert May Miss It
- Assumption: human-oversight design typically treats AI output as one input among several feeding a decision, not as something that could function as dispositive evidence on its own; the specific risk of an AI flag being treated as sufficient proof, with the burden then falling on the subject, is not the failure mode conventional oversight design tests for.
- Conventional complaints-handling and case-review audit checks that a decision was communicated and that a route to complain exists; it does not check whether the underlying evidence and reasoning were disclosed to the subject before or at the point the adverse action was taken, which is a different and prior question.
- Process gap: fraud, conduct and financial-crime investigation practice is built around human-originated allegations, where an investigator can articulate the evidential basis on request; an AI-originated flag is treated procedurally the same way, but the underlying reasoning may not be reconstructable or comprehensible to a non-specialist reviewer, let alone the subject.
- Testing gap: standard case-quality audits check whether the final decision was correct, not whether the evidential standard applied to the AI-originated input met a defined threshold or whether disclosure occurred — the sufficiency and disclosure questions are invisible to outcome-focused review.

## 8. Assurance Objective
**AO-HUM-009:** Where AI output initiates or materially contributes to an adverse allegation, decision or sanction against a customer or colleague, the institution shall apply a documented, proportionate evidential-sufficiency threshold before acting, disclose the underlying evidence and reasoning to the subject as a matter of course, and shall not require the subject to disprove the AI output before the adverse action is reversed or suspended.

## 9. Expected Controls (Traced)
- **Documented evidential-sufficiency threshold, proportionate to consequence severity** — [Emerging Practice; no established cross-sector or financial-services-specific standard for "evidential sufficiency of an AI-originated allegation" has been identified] — a defined threshold for what evidential basis is required, scaled to the severity of the consequence, before AI output can support adverse action.
- **Disclosure of the evidence and reasoning to the subject as a matter of course, not on request** — [Robodebt Royal Commission, Report Vol. 1, 2023] — the Commission's findings on the Australian income-averaging debt-recovery scheme are the clearest documented account of the harm that follows when an automated assertion is acted on without the underlying basis being made available to the person it is asserted against.
- **Explanation on request where the EU AI Act applies, narrower than disclosure as a matter of course** — [EU AI Act, Regulation (EU) 2024/1689, consolidated text of 27 July 2026, Article 86] — Article 86(1) gives a person subject to a decision taken by the deployer on the basis of the output from a high-risk AI system listed in Annex III (point 2 excepted), where the decision produces legal effects or similarly significantly affects that person in a way that they consider to have an adverse impact on their health, safety or fundamental rights, the right to obtain from the deployer "clear and meaningful explanations of the role of the AI system in the decision-making procedure and the main elements of the decision taken". The right is the person's to exercise, in respect of a decision already taken, and Annex III point 5(b) excludes "AI systems used for the purpose of detecting financial fraud"; disclosure of the evidence and reasoning as a matter of course, at or before the point of action, is additional to and not satisfied by compliance with Article 86. Scope and application dates are stated under Regulatory Basis.
- **An explicit rule that the burden of justifying the adverse action sits with the institution, not the subject** — [Robodebt Royal Commission, Report Vol. 1, 2023, p. v] — the Commission's central finding, that the scheme "neither produced accurate results nor complied with the income calculation provisions of the Social Security Act 1991 (Cth)," documents in practice what happens when the burden is left with the person asserted to owe a debt rather than with the institution asserting it.
- **An evidential-standard control that is additional to, not satisfied by, the general complaints-handling framework** — [FCA, Handbook DISP 1.1.3R (application) with DISP 1.3.1R (effective complaints-handling procedures)] — the existing complaints-handling rule presupposes a decision has already been made and communicated and gives the customer a route to complain about it; it does not itself set an evidential-sufficiency threshold for the AI-originated allegation feeding that decision, so compliance with the complaints-handling framework alone does not satisfy this control.
- **Periodic case-file sampling against the documented evidential standard** — [Emerging Practice; extends conventional case-quality audit to test evidential sufficiency and disclosure specifically, rather than outcome correctness alone] — a defined sample of adverse-action case files is reviewed on a recurring cycle to confirm the threshold was applied and disclosure occurred, not assumed from policy.

## 10. Expected Evidence (Tagged L1–L5)
- Policy assertion that "adverse actions are reviewed by a human before being actioned" — **L1**.
- Documented evidential-sufficiency threshold and disclosure policy, distinct from the general complaints-handling framework — **L2**.
- Design or process walkthrough confirming disclosure of the evidence and reasoning is generated at or before the point of action, not only on request — **L3**.
- Case-file sample (dev/test or de-identified historical) reviewed against the documented threshold and disclosure requirement — **L3**.
- Independent audit tracing a sample of real historical adverse-action case files to confirm the evidential threshold was applied, disclosure occurred, and the burden was not reversed onto the subject — **L4**.
- Production complaint or appeal outcome data indicating whether subjects were able to meaningfully contest allegations they had been shown the basis for — **L5**.

## 11. Independent Test
> In a non-production environment, review the documented evidential-standard policy against a sample of adverse-action case files — real historical case files, de-identified, or dev/test equivalents — initiated or materially driven by AI output. For each sampled case, check: (1) whether a defined evidential-sufficiency threshold was applied and met before the adverse action was taken, (2) whether the underlying evidence and reasoning were disclosed to the subject at or before the point of action, and (3) whether the process required the subject to disprove the allegation rather than requiring the institution to justify it. No published testing methodology exists for evidential sufficiency of an AI-originated allegation as a discipline — stated plainly, not implied. This is a professional-judgement documentation and case-file review, not a quantitative or benchmarked test. Executed entirely on de-identified or dev/test case files; no live adverse action is affected by the test. — **★1 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the harm mechanism is strongly evidenced across independent jurisdictions, but there is no established review methodology and no comparable published benchmark for what a proportionate evidential standard means for AI output specifically; judgement dominates entirely).

## 12. Pass Indicators
- A documented evidential-sufficiency threshold exists, proportionate to consequence severity, and the sampled case files meet it.
- Disclosure of the evidence and reasoning occurred at or before the point of action for the large majority of sampled cases, not only on request or after complaint.
- No sampled case shows the subject bearing the burden of disproving the AI-originated allegation before the action was reversed or suspended.
- The evidential-standard policy is documented as distinct from, and additional to, the general complaints-handling framework.
- Case-file sampling against the evidential standard is repeated on a recurring cycle, not treated as a one-off validation.

## 13. Fail Indicators
- No documented evidential-sufficiency threshold exists; adverse action proceeds on AI output alone with no defined basis.
- Disclosure of the evidence and reasoning occurs only on request, after complaint, or not at all.
- Sampled cases show the subject bore the practical burden of disproving the allegation.
- The firm treats compliance with the general complaints-handling framework as if it independently satisfied the evidential-standard requirement.
- No case-file sampling or documentation review against an evidential standard has ever been performed; the control is asserted, not evidenced.

## 14. Reporting Language
**Pass:** "Case-file sampling against the documented evidential-sufficiency threshold shows AI-originated adverse allegations meet a defined, proportionate evidential standard, with disclosure of the evidence and reasoning occurring at or before the point of action and no reversal of the burden of proof onto the subject. This is a ★1 assessment — the underlying harm mechanism is strongly evidenced but no established review methodology or benchmark exists for this control — and should be re-sampled on a recurring cycle."

**Fail:** "Case-file sampling shows adverse action proceeding on AI-originated flags with no documented evidential-sufficiency threshold and no disclosure of the underlying evidence and reasoning to the subject before or at the point of action. This pattern places the practical burden of disproof on the subject and is consistent with the failure mechanism documented in comparable public-sector incidents; the affected process should not continue unchanged until an evidential standard and disclosure practice are established."

**Partial:** "The documented evidential-sufficiency threshold is applied and disclosure occurs for [decision type A], but [decision type B] relies on the general complaints-handling framework alone, with no distinct evidential-standard policy or proactive disclosure. Remediation should extend the evidential-standard control to [decision type B] before continued reliance."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (customers or colleagues wrongly sanctioned; regulatory
    and reputational exposure if the practice affects a batch of
    similarly-actioned cases)
  Likelihood: 2 (unlikely if a documented evidential-sufficiency
    threshold and disclosure practice are active and periodically
    sampled)
  Detectability: 2 (detectable via periodic case-file sampling ahead
    of a complaint or investigation; not real-time)
  Recoverability: 3 (reversible within days-to-weeks via case
    re-review and remediation of the affected batch)
  Novelty: 4 (domain expert very likely to miss it — human-oversight
    design conventionally treats AI output as one input among several,
    not as something that could function as dispositive evidence with
    the burden falling on the subject)

Residual risk interpretation: Acceptable if the evidential-sufficiency
threshold and disclosure practice remain active and are periodically
sampled. Novelty is the priority axis — the failure mode is genuinely
outside conventional oversight-design and complaints-handling practice,
so a one-off validation would understate the risk of drift.

If controls are absent or degraded:
  Severity: 4 (systemic, batch-level wrongful sanctions across every
    case actioned under the same undisclosed evidential practice — the
    scale documented in comparable public-sector cases)
  Likelihood: 3 (probable absent an active threshold and disclosure
    practice, given how naturally an AI flag reads as a finished
    finding rather than a probabilistic signal)
  Detectability: 3 (invisible until a complaint, investigation or
    external inquiry specifically tests disclosure and evidential
    sufficiency — not visible from outcome-focused case audit)
  Recoverability: 4 (multi-week-to-multi-year remediation and redress
    across the affected population, as evidenced in comparable
    public-sector incidents)
  Novelty: 4 (governance papers assert a human review step exists with
    no evidential-standard or disclosure evidence behind it; the gap
    is invisible without today's specific case-file review)

Residual risk: Critical if unmonitored, given both the severity
demonstrated in comparable incidents and the low cost of periodic
case-file sampling relative to the harm avoided.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Customers or colleagues wrongly sanctioned with no visibility of the basis; regulatory and reputational exposure if the practice affects a batch of cases |
| **Likelihood** | 3 | Probable absent an active evidential-sufficiency threshold and disclosure practice; an AI flag naturally reads as a finished finding rather than a probabilistic signal |
| **Detectability** | 2 | Detectable via periodic case-file sampling ahead of a complaint or investigation, but not visible from outcome-focused case audit alone |
| **Recoverability** | 3 | Reversible within days-to-weeks via case re-review and remediation of the affected batch, assuming the gap is caught before it compounds across a large population |
| **Novelty** | 4 | Domain expert very likely to miss it; conventional human-oversight and complaints-handling design does not test evidential sufficiency or disclosure specific to AI-originated allegations |

## 17. Regulatory Basis
> [FCA, Handbook DISP 1.3.1R] requires effective and transparent complaints-handling procedures once a customer complains, and is cited here as the adjacent framework the evidential-standard control would sit alongside. It presupposes a decision has already been made and communicated, and does not itself set an evidential-sufficiency threshold for the AI-originated allegation feeding that decision — compliance with DISP alone does not satisfy the control this canvas describes. [EU AI Act, Regulation (EU) 2024/1689, consolidated text of 27 July 2026, Article 86(1)] gives an affected person subject to a decision taken by the deployer on the basis of the output from a high-risk AI system listed in Annex III, except point 2, which produces legal effects or similarly significantly affects that person in a way that they consider to have an adverse impact on their health, safety or fundamental rights, the right to obtain from the deployer clear and meaningful explanations of the role of the AI system in the decision-making procedure and the main elements of the decision taken. Article 86(2) disapplies the right where exceptions or restrictions follow from Union law, or from national law in compliance with Union law, and Article 86(3) applies it only to the extent that Union law does not otherwise provide it. Annex III includes creditworthiness evaluation and credit scoring of natural persons, except AI systems used to detect financial fraud (point 5(b)), and decisions in work-related relationships, including the monitoring and evaluation of performance and behaviour (point 4(b)). The Act reaches a deployer established or located in the Union, or one in a third country where the output of the AI system is used in the Union (Article 2(1)(b) and (c)). The right is the person's to exercise, in respect of a decision already taken, and it sets no evidential-sufficiency threshold, so it meets the disclosure limb of this canvas only in part and does not meet the evidential-standard limb. Article 86 sits in Chapter IX, which Article 113 does not except from the Regulation's general application date of 2 August 2026; Chapter III Sections 1 to 3, which include the classification of Annex III systems as high-risk (Article 6(2)), apply to those systems from 2 December 2027 (Article 113, third paragraph, point (c)(i), as amended by Regulation (EU) 2026/1744). This canvas states both dates and draws no inference from them (Articles 2, 6, 86 and 113 and Annex III read in the consolidated text, verified 2026-10-09). No explicit regulatory requirement specific to the evidential standard for AI-triggered adverse allegations has been identified; this IRQ addresses a prudential and conduct-fairness gap under general governance and Consumer Duty expectations rather than a directly enforceable rule (verified 2026-07-31).

## 18. Research Basis
> The Australian **Robodebt Royal Commission** Report, Vol. 1 (2023), p. v, found of the income-averaging debt-recovery scheme that, "as used, it neither produced accurate results nor complied with the income calculation provisions of the Social Security Act 1991 (Cth)" — the scheme reversed the practical burden onto welfare recipients to disprove a debt the algorithm asserted, without disclosing the underlying calculation in a form recipients could meaningfully contest. The **Michigan Unemployment Insurance Agency's MiDAS system** adjudicated fraud determinations algorithmically with no human review for approximately two years (2013–2015), producing a fraud-determination error rate pleaded at 93%, and falsely accused tens of thousands of claimants of fraud, triggering wage garnishment and, for some, bankruptcy. The 93% is recorded in *Cahoo v. SAS Analytics Inc.*, Nos. 18-1295/1296 (United States Court of Appeals for the Sixth Circuit, 3 January 2019), slip opinion p.6 — "the Michigan Auditor General reviewed over 22,000 of MiDAS' fraud determinations and found that 93% of them did not actually involve fraud" — which the court takes at footnote 8, p.17, as the plaintiffs' allegation accepted as true at the pleading stage rather than as a finding of its own; the remaining figures are reported by IEEE Spectrum, GovTech and the University of Michigan's Ford School. The UK **Home Office/ETS TOEIC voice-recognition programme**, per the National Audit Office's May 2019 investigation, used automated voice-recognition to flag English-language tests as invalid at a rate contested between under 1% and up to 20–30% depending on whose estimate is used; over 11,000 people left the UK by March 2019, including forced removals, and the NAO found it "difficult to estimate accurately" how many individuals may have been wrongly identified.
>
> **[FAIAS Incident Register, row 27, "Robodebt (Australia)", 2023]** — an automated income-averaging debt-recovery scheme whose asserted debts were acted on without the calculation being disclosed to the person asserted to owe them, and with the practical burden of disproving the assertion left with that person.
>
> **[FAIAS Incident Register, row 28, "Michigan MiDAS", 2015]** — fraud determinations adjudicated by an automated system with no human review, enforced by wage garnishment before the person had any disclosed basis on which to contest them.
>
> **[FAIAS Incident Register, row 29, "UK Home Office/ETS TOEIC", 2019]** — an automated voice-matching output treated as sufficient to invalidate an English-language test and to found adverse immigration action, with the burden of disproving the match falling on the person accused.
>
> **[FAIAS Incident Register, row 14, "UK Post Office Horizon scandal", 2025]**, citing [Williams, Sir Wyn (Chair), 2025, "Post Office Horizon IT Inquiry Report: Volume 1", HC 1119, presented to Parliament pursuant to section 26 of the Inquiries Act 2005, ordered to be printed 8 July 2025, §§1.7–1.9 and footnote 8] — a fourth instance at national scale of the same failure shape. The Inquiry found at §1.7 that in prosecutions across the United Kingdom "the Post Office and/or the prosecuting authorities asserted either expressly, or by implication that the data produced by Horizon was wholly reliable", and at §1.8 that the same assertion was used to hold postmasters liable under their contracts for apparent branch losses; at §1.9 it recorded that "many hundreds of people have been convicted, wrongly, of criminal offences, and many thousands of people have been held responsible, wrongly, for losses which were illusory, as opposed to real." It is cited as an automation analogue: the transferable element is the evidential treatment of system output as sufficient in itself, with the burden of accounting for the discrepancy falling on the subject, and not the technique that produced the output. The Chair records at footnote 8 that he is "precluded by section 2 Inquiries Act 2005 from determining criminal or civil liability", so these are findings of fact and conduct.
>
> **[FAIAS Incident Register, row 13, "Dutch childcare benefits scandal (toeslagenaffaire)", 2021]**, citing [Amnesty International, 2021, "Xenophobic Machines: Discrimination through unregulated use of algorithms in the Dutch childcare benefits scandal", Index EUR 35/4686/2021, October 2021] — a further instance of an adverse fraud allegation driven by automated output whose basis the subject could not see. The report records that the risk classification model "was a black box system that included a self-learning algorithm" in which even "[t]he civil servant (as the system user) did not have access to any details about what information had been used as the basis for assigning a specific risk score to an applicant", and that affected parents and caregivers "were deprived of meaningful information about the results of the risk classification model in their individual cases" and so "were unable to defend themselves against the system." It is a non-governmental organisation's report rather than a judicial or supervisory finding, and it is cited for the evidential and disclosure mechanism rather than for the discrimination analysis that is the report's own subject.
>
> Five independent systems in four jurisdictions, the same failure shape: automated or algorithmic output treated as sufficient evidence for an adverse action, with no disclosed basis and the burden falling on the person accused.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-008 (D.4 Accountability & Contestability: the contest
    route tested there is meaningless without the disclosure this
    IRQ requires)
  - IRQ-GOV-010 (I.4 Documentation, Records & Regulatory:
    record-keeping sufficient to reconstruct the evidence and
    reasoning behind the original AI-originated flag)
  - IRQ-GOV-013 (I.4 Documentation, Records & Regulatory: cohort-level
    identification — where an allegation-generating defect is found, the
    same failure signature must find every affected subject, not only
    the one who contested)
```

## 20. References
```
[1] Royal Commission into the Robodebt Scheme, 2023. "Report", Volume 1.
    Published: 2023-07-07
    URL: https://robodebt.royalcommission.gov.au/publications/report

[2] National Audit Office, 2019. "Investigation into the response to cheating in English language tests."
    Published: 2019-05-24
    URL: https://www.nao.org.uk/reports/investigation-into-the-response-to-cheating-in-english-language-tests/

[3] IEEE Spectrum; GovTech; University of Michigan, Gerald R. Ford School of Public Policy — reporting on the Michigan Unemployment Insurance Agency's MiDAS system, 2013–2015.
    Accessed: 2026-07-31

[4] Financial Conduct Authority. "Handbook DISP 1.3: Complaints handling rules."
    URL: https://www.handbook.fca.org.uk/handbook/DISP/1/3.html

[5] United States Court of Appeals for the Sixth Circuit, 2019. "Cahoo v. SAS Analytics Inc." Nos. 18-1295/1296, opinion.
    Published: 2019-01-03
    URL: https://www.opn.ca6.uscourts.gov/opinions.pdf/19a0001p-06.pdf

[6] Williams, Sir Wyn (Chair), 2025. "Post Office Horizon IT Inquiry Report: Volume 1." HC 1119.
    Published: 2025-07-08
    URL: https://www.postofficehorizoninquiry.org.uk/sites/default/files/2025-07/Post%20Office%20Horizon%20IT%20Inquiry%20Final%20Report%20Volume%201_0.pdf

[7] Amnesty International, 2021. "Xenophobic Machines: Discrimination through unregulated use of algorithms in the Dutch childcare benefits scandal." Index EUR 35/4686/2021.
    Published: October 2021
    URL: https://www.amnesty.org/en/documents/eur35/4686/2021/en/

[8] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act)", consolidated text of 27 July 2026: Articles 2, 6, 86 and 113 and Annex III.
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj
    Consolidated text: http://publications.europa.eu/resource/celex/02024R1689-20260727
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.4 (Human Oversight, Accountability & Contestability)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Human-oversight design conventionally treats AI output as one input among several; the risk of AI output functioning as dispositive, undisclosed evidence with the burden on the subject is not the failure mode conventional oversight or complaints-handling audit tests for.
✓ Test 2 (Plausible Harm): Grounded in three independent, well-documented public-sector incidents (Robodebt, Michigan MiDAS, UK Home Office/ETS TOEIC) evidencing the same failure shape across three jurisdictions. At v1.2.1, field 18 grounds it in five independent systems in four jurisdictions, adding the Post Office Horizon and Dutch childcare benefits cases.
✓ Test 3 (Testable): Answerable via documentation review and case-file sampling against a defined evidential-sufficiency and disclosure standard, in non-production.
✓ Test 4 (Decision-Relevant): A consequential AI-triggered adverse-action process with no evidential-standard policy is not authorisable under this domain's own contestability logic — a contest route is meaningless if the subject is never shown what they are contesting.

**Change Log:**
- v1.0 (2026-07-31): Initial publication; all four tests passed.
- v1.2.1 (2026-09-19): Field 18 — incident-register citations added in the reserved form (rows 27, 28, 29, 14 and 13); the field's closing sentence moved to the end of the field and restated as five independent systems in four jurisdictions, to match the citations the field now carries. Erratum in the same field: the Michigan MiDAS error rate, "reported at 85–93% depending on measurement window", is corrected to a fraud-determination error rate pleaded at 93%, pinpointed to Cahoo v. SAS Analytics Inc. (6th Cir., 3 January 2019), slip op. p.6, which the court takes at n.8 as the plaintiffs' allegation accepted as true; the 85% limb, which no located primary carries, is withdrawn. The press-sourced count of those falsely accused is restated as tens of thousands, the three named accounts giving 20,000-plus, 34,000-plus and about 40,000. Field 20 — entries [5]–[7] added for the opinion, the Inquiry report and the Amnesty International report, and entry [2]'s publication date corrected to 24 May 2019. Field 21 — the Test 2 record annotated with the widened evidence base. Research-basis review date moved. No change to controls, test, ★1 or risk profile.
- v1.3.3 (2026-10-09): Fields 9, 17 and 20 — EU AI Act Article 86 (right to explanation of individual decision-making) added with its scope and its application dates, read in the consolidated text of 27 July 2026, and stated as narrower than this canvas's disclosure control: the person exercises the right in respect of a decision already taken, Annex III point 5(b) excludes systems used to detect financial fraud, and the Article sets no evidential-sufficiency threshold. Reference [8] added. The Independent Test and the ★1 rating are unchanged.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within days-to-weeks, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. In the controls-absent case, which gives multi-week-to-multi-year remediation, Recoverability is scored 4 in place of 3, as ASSURANCE_MODEL.md §7 scores years-long recovery 4. The other axes, the ★ rating and the research basis are unchanged.
```
