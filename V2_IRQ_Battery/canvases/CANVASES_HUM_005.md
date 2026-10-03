# CANVAS: IRQ-HUM-005

## 1. IRQ ID & Title
**IRQ-HUM-005: Untested Suspension Authority Against Commercial Pressure**

Register question: "Is authority to suspend or constrain the system assigned to named individuals with rehearsed criteria, and is there evidence they would exercise it against commercial pressure?"

## 2. Business Activities Affected
- **Underwriting review:** If a credit-decisioning AI is producing questionable outputs at scale, someone must have both the formal authority and the practical willingness to suspend it, even mid-quarter against revenue targets.
- **Claims approval:** A claims-triage AI degrading in quality needs a named individual empowered to halt or constrain it without waiting for a committee cycle that could take weeks.
- **AML case handling:** An AML-assistant AI showing signs of systematically missing typologies needs suspension authority that can act faster than the typical governance escalation path, given ongoing regulatory exposure during any delay.

## 3. AI Behaviour(s)
- Operates continuously in a business-critical workflow that generates revenue, throughput or regulatory-deadline pressure to keep running even when quality concerns emerge.
- Provides no self-limiting mechanism; suspension or constraint depends entirely on a human decision to act.
- Degradation in quality may be gradual (per IRQ-RES-006) rather than a hard failure, making the case for suspension inherently a judgement call under uncertainty and commercial pressure.

## 4. Failure Mode
> Formal suspension authority is assigned on paper to a named role, but the individual has never rehearsed the suspension decision, the criteria for triggering it are vague or absent, and there is no evidence they would actually exercise that authority against real commercial or operational pressure to keep the system running.

## 5. Potential Consequences
- **Customer:** A degrading or misbehaving AI system continues operating past the point it should have been suspended, compounding harm across an increasing volume of decisions.
- **Institution:** Regulatory and reputational damage is proportional to how long the system continued operating after warning signs emerged; SM&CR accountability exposure for the named individual who held but did not exercise suspension authority.
- **Regulator/market:** Supervisory finding that the firm's kill-switch/suspension governance was theoretical rather than operational, undermining confidence in the firm's broader AI risk management framework.

## 6. Failure Chain
```
AI system shows early warning signs of degraded quality or harmful
behaviour (drift, rising error rate, adverse pattern)
  ↓ (IRQ-RES-006: gradual-decay alerting may or may not surface the
     signal clearly)
Named individual holds formal suspension authority but has never
rehearsed the decision criteria or the mechanics of invoking it
  ↓ (IRQ-HUM-005 — THIS IRQ: suspension authority untested against
     real commercial pressure; hesitation under revenue/deadline
     pressure)
Decision to suspend is delayed pending "more data", committee
consultation, or informal pressure to keep the system running
  ↓ (IRQ-RES-003: even once triggered, the containment mechanism
     itself may not meet a defined time-to-stop objective)
System continues operating for an extended period after the warning
signs first appeared
  ↓
Harm compounds across the additional volume processed during the
delay → regulatory finding that suspension governance was theoretical

Control Breakpoints:
  • IRQ-HUM-005: rehearsed suspension criteria and decision authority,
    tested via simulation against commercial-pressure scenarios
  • IRQ-RES-003: tested containment mechanism with a defined and met
    time-to-stop objective once suspension is triggered
  • IRQ-RES-006: alerting design that surfaces gradual decay clearly
    enough to trigger the suspension decision in good time
```

## 7. Why a Domain Expert May Miss it
- Assumption: "we have a named individual with kill-switch authority in the governance paper, so this risk is covered" — the existence of formal authority says nothing about whether it has ever been exercised or rehearsed, which is the material question under commercial pressure.
- Traditional operational risk governance is comfortable with named accountable individuals for policy compliance, but rarely rehearses a genuinely adversarial scenario in which suspending a revenue-generating or deadline-critical system carries immediate, visible commercial cost to the decision-maker personally.
- Behavioural research on real-world safety authority (e.g. the diffusion-of-responsibility and normalisation-of-deviance dynamics documented in major safety-incident post-mortems) shows that formal authority is frequently not exercised in practice without prior rehearsal and psychological-safety reinforcement — a dynamic not captured by reviewing an org chart or a RACI matrix.
- Testing gap: governance audits typically confirm the authority is assigned (a document exists); they rarely run a simulated scenario testing whether the individual would actually pull the trigger against realistic pressure.

## 8. Assurance Objective
**AO-HUM-005:** Authority to suspend or constrain the AI system shall be assigned to named, senior individuals with documented, rehearsed criteria for exercising it, and the organisation shall hold evidence — through simulation or historical exercise — that this authority would be exercised against genuine commercial or operational pressure.

## 9. Expected Controls (Traced)
- **Named suspension authority with documented, specific trigger criteria** — [FCA, PS21/3, Operational Resilience, Mar 2021, containment/recovery expectations] — a specific individual (not a committee) holds authority, with objective, pre-agreed criteria for when suspension should be triggered.
- **Simulated suspension-decision exercises against realistic commercial-pressure scenarios** — [linked IRQ-RES-003; PRA SS1/21, scenario testing requirement] — periodic tabletop or live-fire exercises in which the named individual must decide whether to suspend under a scenario deliberately designed to include revenue, deadline or reputational counter-pressure.
- **SM&CR individual accountability mapping for the suspension role** — [FCA/PRA, Senior Managers & Certification Regime] — the suspension authority is mapped to a specific Senior Manager Function with documented accountability, reinforcing genuine ownership rather than diffuse committee responsibility.
- **Psychological-safety and non-retaliation policy specifically covering suspension decisions** — [Emerging Practice; drawing on established safety-culture literature, e.g. Reason, J., 1997, "Managing the Risks of Organizational Accidents"] — explicit organisational commitment that exercising suspension authority, even if later judged unnecessary, will not be treated as a performance failing.
- **EU AI Act Article 14(4)(e) stop-mechanism requirement** — [EU AI Act, Regulation (EU) 2024/1689, Article 14(4)(e), Aug 2024] — requires the practical ability to interrupt the system's operation, which this canvas interprets as extending to the human decision-maker's practical willingness to exercise that ability.

## 10. Expected Evidence (Tagged L1–L5)
- Governance chart naming the individual with suspension authority — **L1** (existence of the role only).
- Documented suspension trigger criteria and escalation procedure — **L2**.
- Design specification for the periodic tabletop/simulation exercise programme — **L2**.
- Staging/simulation exercise results: a realistic commercial-pressure scenario presented to the named individual, with the decision outcome and time-to-decision recorded — **L3**.
- Independent review of a historical (real, non-simulated) suspension or near-suspension event, if one has occurred, assessing whether authority was exercised appropriately and in good time — **L4**.
- Trend data across multiple simulation cycles showing whether decision-making under pressure is improving, stable or degrading — **L5** (where the exercise programme has run for multiple cycles).

## 11. Independent Test
> Design and run a realistic tabletop simulation, in a non-production governance exercise (not affecting any live system), presenting the named suspension-authority individual(s) with a scenario in which early warning signs of AI degradation are ambiguous, incomplete, and accompanied by explicit counter-pressure (e.g. a stated quarter-end revenue target, a regulatory deadline dependent on the system remaining live, or a senior stakeholder arguing for delay pending "more data"). Record whether, and how quickly, the individual decides to suspend or constrain the system, and assess the decision against the documented trigger criteria. Run with realistic time pressure and without advance notice of the specific scenario content. Methodology draws on established crisis-simulation and safety-culture assessment practice used in aviation and nuclear safety-critical decision training. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (safety-culture and crisis-decision simulation is a credible, long-established methodology in high-reliability industries, but its specific application to AI-suspension-authority testing in FS is bespoke and relies heavily on scenario design and assessor judgement; no FS-specific benchmark exists).

## 12. Pass Indicators
- The named individual suspends or constrains the system in the simulation within the time bound implied by the documented trigger criteria, despite the presented commercial counter-pressure.
- Decision rationale documented in the exercise references the objective trigger criteria rather than deferring to the counter-pressure.
- The exercise programme runs on a defined recurring cadence with documented outcomes tracked over time.
- SM&CR mapping for the suspension role is current and the individual confirms awareness of and comfort with the accountability.
- No evidence of retaliation or adverse performance consequence following any historical real exercise of suspension authority.

## 13. Fail Indicators
- The named individual delays or declines to suspend in the simulation despite the scenario meeting the documented trigger criteria, citing the presented commercial pressure.
- No trigger criteria exist, or they are vague enough that "genuine ambiguity" becomes a standing justification for inaction.
- No simulation or tabletop exercise has ever been conducted; suspension authority has never been tested in any form.
- The named individual is unaware they hold the authority, or believes it sits with a committee rather than with them personally.
- Anecdotal or documented evidence exists of a prior instance where raising a suspension concern was met with pushback affecting the individual's standing.

## 14. Reporting Language
**Pass:** "A realistic tabletop simulation, including deliberate commercial counter-pressure, shows the named suspension-authority individual suspends the system within the time bound implied by the documented trigger criteria, citing those criteria rather than deferring to the counter-pressure. This is a ★2 assessment — credible safety-culture methodology, bespoke scenario design — and should be re-run periodically as personnel, systems and commercial context change."

**Fail:** "Tabletop simulation shows the named suspension-authority individual delayed action despite the scenario clearly meeting the documented trigger criteria, citing the presented revenue-target counter-pressure as the reason for delay. Suspension authority as currently assigned should not be relied upon as an effective control; remediation should address both criteria clarity and organisational psychological safety before this authority can be considered operative."

**Partial:** "The named individual correctly suspended the system in the [scenario type A] simulation but hesitated materially in [scenario type B], where the counter-pressure was framed as a regulatory-deadline risk rather than a revenue risk. This suggests the trigger criteria are not equally robust across pressure types; remediation should extend criteria clarity and rehearsal to cover regulatory-deadline-framed pressure specifically."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (a degrading or harmful AI system continuing to operate
    compounds harm across an increasing decision volume)
  Likelihood: 2 (unlikely to fail given rehearsed, criteria-based
    decision-making and psychological-safety reinforcement)
  Detectability: 2 (simulation exercises surface the gap directly and
    periodically, ahead of any real event)
  Recoverability: 2 (once suspension is actually exercised, harm stops
    accumulating within the containment mechanism's tested time bound)
  Novelty: 3 (domain expert would recognise the need for a named
    accountable individual but is likely to miss that formal
    authority, untested under simulated commercial pressure, is
    frequently not exercised in practice — a documented organisational
    behaviour pattern, not an AI-specific novelty per se, but rarely
    tested in an AI governance context)

Residual risk interpretation: Acceptable if simulation exercises are
run on a recurring cadence and outcomes are trended; the value of this
control is disproportionately realised through rehearsal rather than
through the paper assignment of authority alone.

If controls are absent or degraded:
  Severity: 4 (a materially harmful AI system continues operating
    indefinitely because no one with real willingness to act holds
    genuine authority to stop it)
  Likelihood: 3 (probable under real commercial pressure absent
    rehearsal, consistent with documented diffusion-of-responsibility
    dynamics in safety-critical organisations)
  Detectability: 3 (only surfaces when a real event forces the
    decision, by which point harm is already accumulating)
  Recoverability: 3 (multi-week remediation; potential SM&CR
    enforcement action against the individual and the firm)
  Novelty: 4 (governance charts assert accountability with no evidence
    the authority would actually be exercised; the gap is invisible
    without a simulation-based test)

Residual risk: Critical if untested, given how directly this control
gates the effectiveness of every other containment mechanism in the
Resilience domain.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | A degrading or harmful system continuing to operate compounds harm across an increasing decision volume until stopped |
| **Likelihood** | 3 | Probable under real commercial pressure absent rehearsal; consistent with documented organisational-safety-culture research on diffusion of responsibility |
| **Detectability** | 2 | Simulation exercises can surface the gap directly and proactively, ahead of any real event, if the exercise programme is active |
| **Recoverability** | 2 | Once suspension is actually exercised, harm stops accumulating within the tested containment time bound |
| **Novelty** | 3 | Domain expert would recognise the need for named accountability but is likely to miss that untested formal authority is frequently not exercised under real pressure without rehearsal |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Article 14(4)(e), Aug 2024] requires the practical ability to interrupt a high-risk AI system's operation. [FCA, PS21/3, Mar 2021] and [PRA, SS1/21, Mar 2021] require tested containment and scenario-based exercising of operational resilience arrangements, which this canvas interprets as extending to the human decision-maker's tested willingness to act. [FCA/PRA, Senior Managers & Certification Regime] provides the individual accountability framework underpinning named suspension authority. Section pinpoints [UNVERIFIED — cited modules (SYSC 4, SYSC 9, SYSC 15A, PRA SS1/21/PS21/3, EU AI Act Art. 14 — SYSC 19D removed 25 Aug 2026: it is the dual-regulated firms Remuneration Code and was mis-cited; SYSC 4.1.1R substituted, verified from the Handbook) confirmed extant on FCA Handbook/BoE/eur-lex; no AI-specific sub-clause pinpoint published by the regulator to cite beyond module level] (verified 29 Jul 2026).

## 18. Research Basis
> [Reason, J., 1997, "Managing the Risks of Organizational Accidents", Ashgate] establishes the safety-culture and psychological-safety foundations for why formal authority is insufficient without organisational reinforcement to exercise it. [Vaughan, D., 1996, "The Challenger Launch Decision", University of Chicago Press] documents "normalisation of deviance" — the organisational dynamic by which warning signs are progressively discounted under schedule/commercial pressure — the closest documented real-world analogue to the failure mode this IRQ addresses. Public incident: [Boeing 737 MAX, U.S. House Committee on Transportation and Infrastructure, 2020, Final Committee Report] illustrates commercial-pressure-driven delay in exercising safety-critical stop authority in a comparably regulated, high-consequence industry.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-RES-003 (G.2 Containment & Recovery: the tested time-to-stop
    mechanism that this authority triggers)
  - IRQ-GOV-001 (I.1 Inventory & Ownership: named accountable owner
    mapping, upstream of suspension-authority assignment)
  - IRQ-HUM-002 (D.1 Automation Bias: shared psychological-safety and
    non-penalty theme, applied to override rather than suspension)
```

## 20. References
```
[1] Reason, J., 1997. "Managing the Risks of Organizational Accidents." Ashgate.
    Accessed: 2026-07-29

[2] Vaughan, D., 1996. "The Challenger Launch Decision: Risky Technology, Culture, and Deviance at NASA." University of Chicago Press.
    Accessed: 2026-07-29

[3] U.S. House Committee on Transportation and Infrastructure, 2020. "Final Committee Report: The Design, Development and Certification of the Boeing 737 MAX."
    Published: September 2020
    URL: https://transportation.house.gov/

[4] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Article 14: Human Oversight."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[5] Prudential Regulation Authority, 2021. "Supervisory Statement SS1/21."
    Published: 2021-03-29
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.3 (Human Oversight, Escalation & Override Design)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Governance charts naming an accountable individual are mistaken for evidence that the authority would actually be exercised; SMEs rarely test decision-making under simulated commercial pressure.
✓ Test 2 (Plausible Harm): Grounded in Reason (1997) safety-culture theory, Vaughan's (1996) normalisation-of-deviance research, and the Boeing 737 MAX case as a real-world regulated-industry analogue.
✓ Test 3 (Testable): Answerable via a tabletop simulation with recorded decision outcome and time-to-decision.
✓ Test 4 (Decision-Relevant): Directly gates whether the firm's containment/suspension framework can be relied upon as a genuine control rather than a paper exercise.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

