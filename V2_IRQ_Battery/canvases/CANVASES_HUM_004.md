# CANVAS: IRQ-HUM-004

## 1. IRQ ID & Title
**IRQ-HUM-004: Human Intervention Point Positioned Too Late to Be Effective**

Register question: "Is the human intervention point positioned where intervention is still effective — before irreversible agent actions — with oversight capacity dimensioned against AI throughput and reconstructable behaviour?"

## 2. Business Activities Affected
- **Underwriting review:** If human sign-off occurs after a conditional offer has already been communicated to the customer, correction requires costly unwind rather than prevention.
- **Claims approval:** If an agentic claims workflow disburses a payment before human review of the settlement rationale, the intervention point is structurally too late to prevent the harm it is meant to catch.
- **AML case handling:** If an agent auto-closes an alert as "no typology found" and only samples a subset for post-hoc human review, the intervention point cannot prevent a missed typology in the unsampled majority.

## 3. AI Behaviour(s)
- Executes multi-step workflows that culminate in an action (payment, communication, case closure) which is difficult or costly to reverse once taken.
- Operates at a throughput materially exceeding the rate at which the assigned human reviewers can meaningfully process each decision.
- Generates outputs and logs that may not capture the full intermediate reasoning or trajectory, limiting the reviewer's ability to reconstruct how a decision was reached even when review does occur.

## 4. Failure Mode
> The human checkpoint is positioned after the point at which the AI's action becomes materially difficult to reverse, and/or the volume of decisions routed to that checkpoint exceeds the reviewers' genuine capacity to process them — so the oversight function exists on paper but cannot, structurally, intervene before harm occurs.

## 5. Potential Consequences
- **Customer:** Harm has already crystallised (payment made, communication sent, case closed) by the time any human involvement occurs, converting "oversight" into after-the-fact discovery rather than prevention.
- **Institution:** Unwind costs, correction costs and reputational damage from having to reverse or apologise for actions the "human-approved" workflow was meant to prevent; regulatory finding that oversight was designed ineffectively.
- **Regulator/market:** Supervisory concern that agentic and AI-assisted workflows in general are being deployed with cosmetic rather than functional human oversight, prompting broader scrutiny.

## 6. Failure Chain
```
Agentic or high-throughput AI workflow executes multi-step actions
toward an irreversible outcome (payment, communication, closure)
  ↓ (IRQ-AGT-012: irreversibility gate not structurally enforced in the
     orchestration layer)
Human checkpoint positioned after the irreversible action, or overseer
capacity is dimensioned for a lower throughput than the AI actually
generates
  ↓ (IRQ-HUM-004 — THIS IRQ: intervention point too late or under-
     resourced to be effective)
Reviewer either cannot process the volume in time, or reviews only
after the action has already taken effect
  ↓ (IRQ-AGT-011: incomplete trajectory traces further limit the
     reviewer's ability to reconstruct what happened, even post-hoc)
Harm has crystallised before any human judgement was exercised
  ↓
Customer/financial harm → costly unwind → regulatory finding that
"human oversight" was structurally incapable of preventing the outcome

Control Breakpoints:
  • IRQ-AGT-012: irreversibility gates enforced in the orchestration
    layer, structurally preventing action before sign-off
  • IRQ-HUM-004: capacity dimensioning — reviewer headcount/time
    matched to actual AI throughput, verified not assumed
  • IRQ-AGT-011: complete, reviewable trajectory traces enabling
    effective (not merely nominal) review
```

## 7. Why a Domain Expert May Miss it
- Assumption: "there is a human sign-off step in the process diagram, therefore oversight exists" — the process diagram does not show where in the sequence the sign-off sits relative to irreversibility, which is the material fact.
- Traditional process design places checkpoints where they have always been placed in the manual process; when AI accelerates upstream steps, the checkpoint's relative position (before or after the point of no return) can silently shift without anyone redesigning the workflow.
- Capacity planning for review teams is often set against the pre-AI decision volume, without recalculating whether the same headcount can meaningfully review the AI-accelerated volume — a straightforward capacity-planning gap that AI throughput increases make newly material.
- Testing gap: staging/UAT testing typically validates that the checkpoint exists and functions, not whether it exists at a point in the sequence, and at a review rate, that is still capable of altering the outcome.

## 8. Assurance Objective
**AO-HUM-004:** The human intervention point in any AI-assisted or agentic workflow shall be positioned before the point of practical irreversibility, and shall be resourced with reviewer capacity genuinely dimensioned against the AI system's actual throughput, with sufficient reconstructable detail to support effective review.

## 9. Expected Controls (Traced)
- **Irreversibility-point mapping for each workflow** — [linked IRQ-AGT-012; EU AI Act, Regulation (EU) 2024/1689, Article 14(4)(e), Aug 2024, requiring the ability to intervene or interrupt operation] — explicit mapping of where in each workflow the action becomes materially difficult to reverse, with the human checkpoint verified to sit before that point.
- **Reviewer capacity dimensioning against measured AI throughput** — [linked IRQ-HUM-002; FCA, Handbook SYSC 4.1.1R] — headcount and time-per-case allocation calculated against the AI system's actual production decision rate, not the pre-AI baseline.
- **Complete, reconstructable action/decision traces** — [linked IRQ-AGT-011; FCA, Handbook SYSC 9, Record Keeping] — sufficient logging of intermediate steps to allow a reviewer to understand not just the final recommendation but the path that produced it.
- **Structural (not merely procedural) gating of irreversible actions pending sign-off** — [OWASP Agentic AI: Threats and Mitigations, Feb 2025, human-in-the-loop control category] — the orchestration layer, not a prompt instruction, enforces that irreversible actions cannot proceed without recorded human sign-off.
- **EU AI Act Article 14(4) intervention-effectiveness requirement** — [EU AI Act, Regulation (EU) 2024/1689, Article 14(4), Aug 2024] — human oversight measures must include the ability to intervene in operation or interrupt the system through a "stop" button or similar procedure, which presupposes the checkpoint is positioned where such intervention remains meaningful.

## 10. Expected Evidence (Tagged L1–L5)
- Process diagram showing a human sign-off step exists — **L1** (says nothing about position relative to irreversibility or capacity).
- Documented irreversibility-point mapping and capacity-dimensioning calculation — **L2**.
- Code/orchestration review confirming the irreversible action is technically blocked pending human sign-off (not merely a prompt-level instruction) — **L3**.
- Staging test: measured time from AI recommendation to reviewer decision across a representative case volume, compared against the time-to-irreversibility for the same case type — **L3**.
- Independent audit of trajectory-trace completeness for a sample of reviewed decisions, confirming reviewers had sufficient reconstructable detail — **L4**.
- Production data: proportion of decisions where human sign-off occurred before versus after the irreversible action actually took effect, and average review queue backlog — **L5**.

## 11. Independent Test
> In a non-production environment, map the full workflow for each in-scope AI-assisted or agentic process (underwriting offer issuance, claims settlement, AML case closure) to identify the precise point of practical irreversibility. Replay a representative volume of dev/test cases at the AI system's actual measured throughput rate and measure whether the human checkpoint's position in the workflow structurally precedes that irreversibility point, and whether the assigned reviewer capacity (time-per-case × headcount) can process the replayed volume without a growing backlog. Separately, sample completed reviews and assess whether the trajectory trace available to the reviewer was sufficient to reconstruct the material factors behind the AI's recommendation. Executed entirely on de-identified dev/test data and simulated throughput; no live workflows are triggered. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (capacity-dimensioning and irreversibility mapping draw on established process-engineering and queuing-theory concepts, but their specific application to AI/agentic throughput and human-oversight-effectiveness testing is FS-context-bespoke with no agreed benchmark; test design and irreversibility-point judgement rely heavily on assessor expertise).

## 12. Pass Indicators
- Irreversibility-point mapping confirms the human checkpoint precedes the point of no return for every in-scope workflow.
- Simulated replay at actual AI throughput shows no material backlog growth in the review queue.
- Irreversible actions are technically blocked pending sign-off at the orchestration layer, confirmed by code/config review.
- Trajectory traces reviewed in the sample are sufficient for reviewers to reconstruct the material path to the AI's recommendation.
- Production data confirms sign-off precedes the irreversible action in the large majority of cases, with any exceptions investigated.

## 13. Fail Indicators
- Irreversibility-point mapping shows the human checkpoint sits after the point of no return for one or more in-scope workflows.
- Simulated replay shows the review queue backlog growing without bound at actual AI throughput, indicating structural under-capacity.
- Irreversible actions can proceed via a code path that bypasses the sign-off step (gating is procedural/prompt-level only).
- Trajectory traces available to reviewers are materially incomplete, preventing genuine reconstruction of the AI's reasoning path.
- Production data shows a material proportion of decisions where the irreversible action occurred before sign-off was recorded.

## 14. Reporting Language
**Pass:** "Irreversibility-point mapping and throughput-replay testing confirm the human checkpoint for [workflow] structurally precedes the point of practical irreversibility, reviewer capacity is dimensioned to actual AI throughput without backlog growth, and trajectory traces are sufficient for genuine reconstruction. This is a ★2 assessment — credible but bespoke methodology — and should be retested whenever workflow design or AI throughput materially changes."

**Fail:** "Irreversibility-point mapping shows the human checkpoint for [workflow] sits after the point at which the AI's action becomes materially difficult to reverse, and throughput-replay testing shows the assigned reviewer capacity cannot process the actual production volume without backlog. This oversight point cannot function as a genuine control against irreversible harm as currently positioned and resourced; the workflow should not be relied upon as human-overseen until the checkpoint is moved earlier or capacity is increased."

**Partial:** "The checkpoint for [decision type A] precedes irreversibility with adequate capacity, but for [decision type B], introduced more recently, the same checkpoint sits after the point of no return due to a workflow change that was not re-mapped. Remediation should re-map [decision type B] and reposition the checkpoint before continued reliance."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (irreversible actions taken without effective prior
    human oversight can directly cause financial or customer harm)
  Likelihood: 2 (unlikely given active irreversibility-mapping and
    capacity monitoring; requires workflow change to go unmapped)
  Detectability: 2 (detectable via throughput/backlog monitoring and
    periodic irreversibility-point audit)
  Recoverability: 2 (reversible in most cases within days via manual
    unwind/correction; some cases — e.g. executed payments — carry
    genuine irreversibility)
  Novelty: 3 (domain expert recognises "there must be a sign-off step"
    but is likely to miss that its position relative to irreversibility,
    and its capacity dimensioning against AI throughput specifically,
    are the material questions)

Residual risk interpretation: Acceptable with active irreversibility
mapping and capacity monitoring, re-validated at every material
workflow or throughput change (a common trigger given how frequently
AI-assisted throughput increases outpace review-team resourcing
decisions).

If controls are absent or degraded:
  Severity: 4 (systemic execution of irreversible actions — payments,
    communications, closures — without any effective prior human
    check, across the full volume processed under the workflow)
  Likelihood: 3 (probable once AI throughput materially exceeds the
    review team's original capacity assumptions, a common and
    foreseeable drift)
  Detectability: 3 (silent until backlog, complaint or incident forces
    investigation of checkpoint timing)
  Recoverability: 3 (multi-week remediation; some individual actions
    genuinely irreversible)
  Novelty: 4 (process diagrams assert a human step exists with no
    analysis of its position relative to irreversibility or its
    capacity; the gap is invisible without today's specific mapping
    exercise)

Residual risk: Critical if unmonitored, given the direct link to
irreversible harm and the plausibility of throughput silently
outpacing capacity.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Irreversible actions taken without effective prior human oversight directly risk financial or customer harm |
| **Likelihood** | 3 | Probable once AI throughput exceeds original review-capacity assumptions, a foreseeable and common drift pattern |
| **Detectability** | 2 | Detectable via backlog and irreversibility-point monitoring, but requires deliberate mapping design |
| **Recoverability** | 2 | Most cases reversible within days via manual unwind; some individual actions (executed payments) carry genuine irreversibility, pulling toward 3 in specific cases |
| **Novelty** | 3 | Domain expert assumes a sign-off step is sufficient without analysing its position relative to irreversibility or its capacity dimensioning against AI-specific throughput |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Article 14(4)(e), Aug 2024] requires human oversight measures to include the ability to intervene in the operation of a high-risk AI system or interrupt it through a stop mechanism — which presupposes the intervention point retains practical effect. [FCA, Handbook SYSC 4.1.1R] and [FCA, Handbook SYSC 9, Record Keeping] together require robust governance arrangements and sufficient records to reconstruct decisions. Section pinpoints [UNVERIFIED — cited modules (SYSC 4, SYSC 9, SYSC 15A, PRA SS1/21/PS21/3, EU AI Act Art. 14 — SYSC 19D removed 25 Aug 2026: it is the dual-regulated firms Remuneration Code and was mis-cited; SYSC 4.1.1R substituted, verified from the Handbook) confirmed extant on FCA Handbook/BoE/eur-lex; no AI-specific sub-clause pinpoint published by the regulator to cite beyond module level] (verified 29 Jul 2026).

## 18. Research Basis
> [OWASP GenAI Security Project, "Agentic AI: Threats and Mitigations", Feb 2025] documents the general pattern of human-in-the-loop controls being rendered ineffective by positioning or throughput mismatch in agentic systems. [Amershi, S. et al., 2019, "Guidelines for Human-AI Interaction", CHI 2019] provides established interaction-design guidance (notably G9: "Support efficient correction") relevant to positioning intervention points where correction remains practically possible. Public financial-services-adjacent incident: [Knight Capital Americas LLC, incident of 1 August 2012; SEC Release No. 70694, 16 October 2013] illustrates the consequence of an automated system executing high volumes of irreversible actions faster than any human checkpoint could intervene, the closest available real-world analogue for this failure mode.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-AGT-012 (C.7 Workflow & Action Safety: irreversibility gates
    structurally enforced in the orchestration layer)
  - IRQ-AGT-011 (C.7 Workflow & Action Safety: complete reviewable
    action traces enabling effective, not merely nominal, review)
  - IRQ-HUM-002 (D.1 Automation Bias: throughput/dwell-time analysis,
    shared measurement basis for capacity dimensioning)
  - IRQ-RES-003 (G.2 Containment & Recovery: tested containment/halt
    mechanism as the structural backstop to this checkpoint)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Article 14: Human Oversight."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[2] OWASP GenAI Security Project, 2025. "Agentic AI: Threats and Mitigations."
    Published: February 2025
    URL: https://genai.owasp.org/

[3] Amershi, S., Weld, D., Vorvoreanu, M. et al., 2019. "Guidelines for Human-AI Interaction." CHI 2019.
    Accessed: 2026-07-29

[4] U.S. Securities and Exchange Commission, 2013. "In the Matter of Knight Capital Americas LLC." SEC Release No. 70694.
    Published: 2013-10-16
    URL: https://www.sec.gov/litigation/admin/2013/34-70694.pdf

[5] Financial Conduct Authority. "Handbook SYSC 4" and "Handbook SYSC 9."
    URL: https://www.handbook.fca.org.uk/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.3 (Human Oversight, Escalation & Override Design)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs treat the existence of a sign-off step in the process diagram as sufficient; its position relative to irreversibility and its capacity dimensioning are not standard process-audit questions.
✓ Test 2 (Plausible Harm): Grounded in OWASP Agentic AI Threats and Mitigations (2025), Amershi et al.'s (2019) HAI guidelines, and the Knight Capital incident as a real-world analogue.
✓ Test 3 (Testable): Answerable via irreversibility-point mapping and throughput-replay testing; measurable backlog and timing data.
✓ Test 4 (Decision-Relevant): Directly determines whether an AI-assisted or agentic workflow's human checkpoint can be relied upon, gating deployment or requiring workflow redesign.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

