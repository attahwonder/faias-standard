# CANVAS: IRQ-MOD-003

## 1. IRQ ID & Title
**IRQ-MOD-003: Undetermined Reasoning-Length Degradation in Long or Multi-Constraint Tasks**

Register question: "For reasoning models, does output quality degrade on long or multi-constraint tasks, and has the effective reasoning length/complexity limit been established for this use?"

## 2. Business Activities Affected
- **Complex affordability assessment:** A reasoning model asked to reconcile multiple income streams, debts, dependants and policy exceptions in one pass may satisfy earlier constraints while silently dropping or misapplying later ones as task length grows.
- **AML case narrative synthesis:** Multi-entity, multi-jurisdiction investigations requiring the model to hold many facts and rules simultaneously are exactly where reasoning degradation is most consequential and least visible.
- **Claims liability reasoning:** Multi-party liability claims with several contractual and regulatory constraints in play risk an internally inconsistent recommendation that "looks" thorough.

## 3. AI Behaviour(s)
- Performs step-by-step or extended reasoning to satisfy multiple constraints or synthesise long inputs.
- Produces fluent, internally-plausible output regardless of whether all constraints were actually tracked and satisfied.
- Reasoning quality is not visibly self-reported; the model does not reliably flag when it has begun dropping earlier constraints.

## 4. Failure Mode
> Output quality on long or multi-constraint tasks degrades — constraints satisfied early in the task are silently dropped, contradicted, or under-weighted later — without the model signalling that degradation, and without the firm having established the task-length/complexity point at which this occurs for its own use case.

## 5. Potential Consequences
- **Customer:** A materially wrong decision (e.g. an affordability calculation that satisfies four of five debt constraints but silently drops the fifth) presented with the same fluency and confidence as a fully correct one.
- **Institution:** Reliance on reasoning-length limits that were never empirically established; SS1/23 validation gap; remediation across all cases handled at or beyond the undetermined limit.
- **Regulator/market:** Inability to demonstrate that model outputs on complex, multi-constraint cases were validated at the actual complexity level used in production.

## 6. Failure Chain
```
Reasoning model deployed for multi-constraint task
(e.g. multi-income, multi-debt affordability assessment)
  ↓ (IRQ-MOD-001: capability envelope not empirically bounded by task complexity)
Task length/constraint count increases in production beyond validated cases
  ↓ (IRQ-MOD-003 — THIS IRQ: no measured reasoning-length degradation limit)
Model silently drops or misapplies a subset of constraints
while maintaining fluent, confident output
  ↓ (IRQ-MOD-006: expressed confidence does not track actual constraint-satisfaction accuracy)
Reviewer sees a well-formatted, plausible output and has no signal
that a constraint was dropped
  ↓ (IRQ-HUM-001: automation bias; reviewer does not re-derive the full reasoning independently)
Materially wrong underwriting/AML/claims decision issued
  ↓
Complaint or downstream reconciliation discovers dropped constraint →
FOS/regulatory finding → remediation across similarly-complex cases

Control Breakpoints:
  • IRQ-MOD-001: capability-envelope testing stratified by task complexity, not just task type
  • IRQ-MOD-003: reasoning-length/complexity degradation explicitly measured and bounded
  • IRQ-MOD-006: calibration testing extended to complex multi-constraint conditions
  • IRQ-HUM-004: escalation/decomposition rule for tasks beyond the established complexity limit
```

## 7. Why a Domain Expert May Miss It
- Credit and claims SMEs are trained to check the final answer's plausibility, not to independently re-verify that every constraint was actually applied — a long, well-structured output reads as more thorough, not less reliable.
- The intuition that "more reasoning steps = more careful analysis" is the opposite of what degrades: additional length increases the chance an earlier constraint is silently dropped.
- Traditional model validation tests accuracy on representative cases of typical complexity; it rarely stratifies test cases by number of constraints or input length to find where degradation begins.
- Reasoning models can produce a chain-of-thought that appears to address all constraints even when the final answer does not reflect all of them — the visible reasoning is not a reliable audit trail (links IRQ-MOD-009).

## 8. Assurance Objective
**AO-MOD-003:** The effective reasoning-length and multi-constraint complexity limit beyond which output quality degrades shall be empirically established for this use case, and tasks approaching or exceeding that limit shall be detected and handled through decomposition, escalation, or explicit accuracy caveats rather than presented as equally reliable.

## 9. Expected Controls (Traced)
- **Reasoning-length/complexity degradation testing** — [Emerging Practice; informed by Liu et al., 2023, "Lost in the Middle" and general reasoning-model capability literature] — test suite stratified by number of constraints and input length, measuring per-constraint satisfaction rate, not just final-answer plausibility.
- **Task decomposition for complex cases** — [linked IRQ-AGT-001 for agentic decomposition patterns; Emerging Practice for single-model use] — complex multi-constraint tasks are broken into smaller sub-tasks each within the established reliable-length limit, with results reconciled explicitly.
- **Per-constraint verification rather than final-answer-only review** — [linked IRQ-HUM-002 (review effectiveness); PRA SS1/23 development/validation principles] — human or automated review checks that each individual constraint was correctly applied, not only that the final output looks plausible.
- **Usage limits reflecting the tested complexity boundary** — [linked IRQ-MOD-001, IRQ-GOV-003] — conditions of use cap task length/constraint count at the empirically validated limit, technically enforced.
- **Calibration testing extended to complex conditions** — [linked IRQ-MOD-006; Farquhar et al., 2024] — confidence/uncertainty signals are validated specifically at high constraint-count, not only on simple cases.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor claim that the model "reasons reliably over long contexts" — **L1** (assertion only; flag).
- Design documentation defining the intended maximum task complexity/length and the decomposition strategy for cases exceeding it — **L2**.
- Staging test results measuring per-constraint satisfaction rate across a range of constraint counts (e.g. 2, 4, 6, 8 simultaneous constraints), identifying the degradation point — **L3**.
- Code/configuration review confirming task-length or constraint-count limits are enforced (not policy-only) — **L3**.
- Independent validation report assessing the reasoning-degradation testing methodology and results — **L4**.
- Production data on task complexity distribution and any post-decision QA findings of dropped constraints — **L5**.

## 11. Independent Test
> In a non-production environment, construct a graduated test set for the deployed use case with increasing numbers of simultaneous constraints (e.g. affordability cases with 2, 4, 6, 8 co-active debt/income/exception rules), each with a known ground-truth correct application of every constraint. Run the pipeline and measure, per case: (1) the proportion of constraints correctly applied; (2) whether expressed confidence/fluency remains constant even as per-constraint accuracy falls; (3) the constraint count at which per-constraint accuracy drops below the firm's defined tolerance. Compare stated chain-of-reasoning against actual constraint application to test reasoning-faithfulness (links IRQ-MOD-009). Executed entirely on synthetic/anonymised cases in staging. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (harm mechanism is plausible and partially evidenced by adjacent long-context research such as "Lost in the Middle"; no standard benchmark exists for FS multi-constraint reasoning degradation, and the graduated test design rests on the tester's own construction of constraint complexity).

## 12. Pass Indicators
- A graduated degradation curve is measured and a defensible complexity/length limit is documented.
- Within the documented limit, per-constraint accuracy meets the firm's tolerance; beyond it, the system decomposes, escalates, or issues an explicit lower-confidence signal rather than an equally fluent answer.
- Usage limits are technically enforced (e.g. workflow blocks or routes cases exceeding the tested constraint count).
- Reviewer guidance and tooling support per-constraint verification, not only final-answer plausibility checks.

## 13. Fail Indicators
- No degradation testing exists; validation covers only simple, low-constraint representative cases.
- Per-constraint accuracy falls materially as complexity increases while confidence/fluency remains constant — the degradation is invisible to reviewers.
- No task-length or constraint-count limit is enforced; complex production cases regularly exceed anything tested.
- Chain-of-reasoning shown to reviewers does not reliably reflect which constraints were actually satisfied (links IRQ-MOD-009 fail condition).

## 14. Reporting Language
**Pass:** "Reasoning-length and multi-constraint degradation has been empirically tested; a defensible complexity limit is documented and technically enforced, with decomposition or escalation applied beyond it. Per-constraint accuracy within the tested limit meets the firm's tolerance. Conclusions rest on ★2 methodology — bespoke test design, no industry benchmark — and should be treated as professional assessment, refreshed as task complexity in production evolves."

**Fail:** "Testing demonstrates that as the number of simultaneous constraints increases, per-constraint accuracy falls materially while the model's output remains equally fluent and confident, giving reviewers no signal that a constraint was dropped. No complexity limit is enforced in production, and cases at the tested-worst complexity level are common in the current task mix. This creates a direct path to materially wrong, undetected decisions on the firm's most complex cases; usage should be restricted pending decomposition controls and complexity limits."

**Partial:** "Degradation testing has been performed up to [n] simultaneous constraints, but production cases regularly involve up to [m > n] constraints, an untested range. The assurance objective is not met for cases above [n] constraints; usage should be capped at the tested complexity level pending further testing."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (multiple customers exposed to wrong decisions on the most complex cases;
              regulatory notice risk)
  Likelihood: 2 (requires production task complexity to exceed the tested/enforced limit,
              which controls should prevent)
  Detectability: 2 (per-constraint review and QA sampling surface dropped constraints within
              days)
  Recoverability: 2 (identifiable via case-level constraint audit; re-decisioning feasible)
  Novelty: 4 (the counter-intuitive direction of the failure — more apparent thoroughness
              correlating with lower reliability — is very likely to be missed by a
              non-AI-specialist reviewer)

Interpretation: acceptable residual risk with degradation testing, enforced complexity limits
and per-constraint review; highest concern is Novelty, given how strongly fluency signals
"thoroughness" to human reviewers.

If controls are absent or degraded:
  Severity: 4 (systematic, undetected wrong decisions concentrated in the most complex — often
              highest-value or highest-vulnerability — cases)
  Likelihood: 4 (complex multi-constraint cases occur routinely in underwriting/AML/claims;
              nothing structurally caps task complexity)
  Detectability: 4 (silent; fluent output with no per-constraint signal; found only via
              downstream reconciliation or complaint)
  Recoverability: 3 (requires full constraint-level re-audit of complex-case population)
  Novelty: 4
Residual risk: Critical. Deployment gate should not be passed for complex multi-constraint use
without degradation testing.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Wrong decisions concentrate in the most complex, often highest-materiality cases; regulatory notice risk. |
| **Likelihood** | 2 | Probable only if enforced complexity limits are absent; controlled deployments should prevent this, making it plausible-if-controls-lapse rather than default. |
| **Detectability** | 3 | Fluent output gives no signal that a constraint was dropped; detection needs deliberate per-constraint audit, not routine review. |
| **Recoverability** | 2 | Once identified, affected cases are traceable and re-decisionable via case-level review. |
| **Novelty** | 4 | The failure direction — apparent thoroughness masking lower reliability — directly inverts the SME's usual quality heuristic; highly likely to be missed without AI-specific knowledge. |

## 17. Regulatory Basis
> [PRA SS1/23, May 2023, effective 17 May 2024, Principle 3/4 — validation must reflect the actual conditions of use, including task complexity] — the primary anchor; no explicit regulatory text addresses "reasoning-length degradation" as such. [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] — foreseeable-harm obligation is engaged where complex-case decisions are systematically less reliable without disclosure or mitigation. This IRQ operationalises SS1/23's use-fidelity expectation for a failure mode specific to reasoning models. [UNVERIFIED — no further pinpoint exists for a mechanism not named in the regulatory text] (verified 29 Jul 2026).

## 18. Research Basis
> [Liu, N.F., et al., 2023, "Lost in the Middle: How Language Models Use Long Contexts", arXiv:2307.03172] — demonstrates a U-shaped performance curve over long contexts: information in the middle of a long input (such as a constraint stated among several others) is used less reliably than information at its start or end. [Shi, F., et al., 2023, "Large Language Models Can Be Easily Distracted by Irrelevant Context", arXiv:2302.00093] — shows accuracy degrades sharply when irrelevant information is added to the problem context, supporting the general mechanism of context-driven degradation.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-MOD-001 (B.1: capability envelope — this IRQ is the complexity-dimension special case)
  - IRQ-MOD-006 (B.3: calibration must be validated at high constraint-count, not only simple cases)
  - IRQ-MOD-009 (B.4: chain-of-thought faithfulness — the visible reasoning may not reflect actual constraint handling)
  - IRQ-AGT-001 (C.1: task decomposition as an agentic mitigation pattern)
  - IRQ-HUM-002 (D.1: review effectiveness — per-constraint verification vs final-answer-only review)
```

## 20. References
```
[1] Liu, N.F., Lin, K., Hewitt, J., et al., 2023. "Lost in the Middle: How Language Models
    Use Long Contexts." arXiv:2307.03172.
[2] Shi, F., Chen, X., Misra, K., et al., 2023. "Large Language Models Can Be Easily
    Distracted by Irrelevant Context." arXiv:2302.00093.
[3] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[4] FCA, 2022. "PS22/9: A New Consumer Duty." PRIN 2A in force 31 July 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.1 (Model domain, Capability Uncertainty)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): The failure direction inverts the usual quality heuristic (longer,
  more thorough-looking output = more reliable); credit/claims SMEs would very likely miss it.
✓ Test 2 (Plausible Harm): Grounded in long-context attention research (Liu et al. 2023;
  Shi et al. 2023) demonstrating that models under-use information in the middle of long inputs and are distracted by irrelevant context.
✓ Test 3 (Testable): Fully testable via graduated constraint-count staging tests; no
  production data required.
✓ Test 4 (Decision-Relevant): Outcome sets the enforced task-complexity limit and determines
  whether decomposition/escalation controls are required before deployment on complex cases.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

