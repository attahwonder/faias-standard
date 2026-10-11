# CANVAS: IRQ-RES-003

## 1. IRQ ID & Title
**IRQ-RES-003: Untested Time-Bound Containment and Mid-Plan Agent Termination**

Register question: "Can the system be halted or constrained within a defined time bound, including mid-plan agent termination without orphaned or half-completed actions, and is this tested?"

## 2. Business Activities Affected
- **Any agentic workflow capable of multi-step planning and tool invocation:** payment initiation agents, document generation and filing agents, and case management agents can be mid-execution when a stop decision is made; the consequence of that stop must be a safe state, not an orphaned half-completed action.
- **Incident response for any AI system:** across the estate, the ability to halt or constrain a misbehaving AI system within a defined time bound is a precondition for containing any incident before it compounds.
- **Governance suspension authority:** named individuals' authority to suspend a system (HUM-005) is only meaningful if the underlying technical containment mechanism actually works within the time bound they need.

## 3. AI Behaviour(s)
- Agentic systems execute multi-step plans involving sequential or parallel tool calls, some of which may have side effects (writing records, initiating payments, sending communications) that are not naturally reversible.
- A stop/kill command issued mid-plan must propagate to halt further steps; without explicit design, in-flight steps may complete regardless, or the system state may be left inconsistent (e.g. a payment initiated but its corresponding record not written).
- Containment mechanisms are typically built and validated for simple, single-step request-response systems; agentic, stateful, multi-step systems present a materially different termination challenge.

## 4. Failure Mode
> The system cannot be halted or constrained within a defined, tested time bound, and mid-plan termination of an agentic process leaves orphaned or half-completed actions (e.g. a payment initiated without its corresponding record, a communication partially sent) rather than resolving to a defined safe state — so an incident response decision to stop the system does not actually stop its consequences.

## 5. Potential Consequences
- **Institution:** An incident that should have been contained by a stop command instead continues to cause harm (further erroneous transactions, further erroneous communications) because in-flight actions were not halted or resolved safely; reconciliation and remediation cost from orphaned/inconsistent state.
- **Customer:** A duplicated, missing, or inconsistent transaction/communication resulting from mid-plan termination directly affects the customer, independent of the original triggering issue.
- **Regulator:** Failure to demonstrate a tested containment capability is a direct operational resilience and governance gap (PRA SS1/21 recoverability expectation; DORA incident response and recovery obligations).

## 6. Failure Chain
```
Agentic system executing a multi-step plan with tool-call side
effects (e.g. draft → validate → submit payment → log)
  ↓ (IRQ-HUM-005: a decision is made to halt the system, e.g. due
     to a detected anomaly, but the underlying mechanism is untested)
Stop/kill command issued; propagation to in-flight steps is not
guaranteed by design
  ↓ (IRQ-RES-003 — THIS IRQ: no defined time bound or tested
     mid-plan termination behaviour exists)
Some steps complete after the stop command (e.g. payment submitted)
while others do not (e.g. corresponding log/notification), leaving
an orphaned, half-completed action
  ↓
Reconciliation discovers inconsistent state; remediation is manual,
slow, and itself risks further error; incident scope expands beyond
the original trigger

Control Breakpoints:
  • IRQ-RES-003: tested time-bound containment with defined mid-plan
    termination behaviour (e.g. safe rollback, safe completion, or
    safe pause-and-flag) for every side-effecting step type
  • IRQ-HUM-005: named authority actually exercises and rehearses the
    stop decision against a mechanism proven to work
  • IRQ-AGT-012: irreversible/high-materiality actions structurally
    gated, reducing the number of steps that can be "orphaned"
```

## 7. Why a Domain Expert May Miss It
- Traditional kill-switch thinking (from batch systems or simple request-response services) assumes "stop" means the process simply halts with no further side effects; agentic systems with in-flight, side-effecting tool calls violate that assumption in ways unfamiliar to ops SMEs from non-agentic backgrounds.
- A kill switch that has "always worked" in testing on simple flows may never have been tested against the specific case of a step that is mid-execution (e.g. a payment API call already sent, response not yet received) at the moment of termination.
- Incident responders may assume that once a stop command is confirmed sent, the incident is contained; verifying that all in-flight actions actually resolved to a safe state requires a reconciliation step that is easy to skip under incident pressure.
- The distinction between "halt cleanly" and "halt but leave inconsistent state" is invisible until deliberately tested — a system can appear to have stopped (no new actions initiated) while still carrying unresolved consequences from actions already in flight.

## 8. Assurance Objective
**AO-RES-003:** The system shall be capable of being halted or constrained within a defined time bound, with mid-plan agent termination resolving every in-flight, side-effecting action to a defined safe state (rather than an orphaned or half-completed state), and this capability shall be tested, not merely designed.

## 9. Expected Controls (Traced)
- **Defined time-to-stop objective and tested kill mechanism** — [linked IRQ-HUM-005] — [PRA SS1/21, March 2022 (11 March 2022, updating 29 March 2021), recoverability expectation] extended to AI-specific agentic termination.
- **Idempotent, reversible or safely-completable action design for tool calls** — [established distributed-systems/transaction-processing engineering practice] — every side-effecting step type has a defined behaviour under mid-execution termination (complete-then-stop, safe rollback, or pause-and-flag for manual reconciliation).
- **Mid-plan termination testing** — Emerging Practice, specific to agentic AI orchestration — no published FS-sector standard identified for testing multi-step agent termination specifically; general chaos/failure-injection testing principles apply by extension.
- **ICT incident response and recovery capability** — [Regulation (EU) 2022/2554, DORA, Art. 11–12, ICT business continuity policy and response/recovery plans] — containment and recovery capability, including for AI-specific incidents, forms part of the mandated ICT business continuity framework.
- **Reconciliation step post-termination** — Emerging Practice — post-stop reconciliation to confirm no orphaned action remains is a natural extension of general incident closure practice, not yet standardised for agentic AI specifically.
- **Blunt, infrastructure-level kill mechanism, tested as a distinct last-resort capability alongside graceful mid-plan termination** — [NCSC, "Managing the cyber risk of agentic AI", item 7, "Emergency shutdown: maintain the ability to ‘pull the plug’", of the post's "Key considerations" list, blog post published 20 August 2026 (page metadata: modified 24 August 2026) — **interim advice which NCSC states will be built upon and ultimately superseded by forthcoming formal guidance**; CMORG AI Taskforce, "Firm Guidance for Frontier AI" v1.0, June 2026, §3.1 Attack Surface Reduction, printed p.5] — NCSC states that "If an incident is detected or reported, you should always be able to ‘pull the plug’ and halt autonomous AI agent activity immediately.", and specifies the layer at which that must be possible: "Your controls should cover the wider system, allowing you to rapidly restrict network access to the agentic AI infrastructure and interrupt the communications between selected AI agents and the AI model inference infrastructure." CMORG's guidance puts the same requirement among the controls owed to AI operating with privileged access — "tightly control high-risk capabilities (including tools, code execution and APIs), enforce scoped permissions, robust logging, human oversight, and effective kill-switch mechanisms". **Why this is distinct from the first control in this field, and why it is tested separately:** a graceful time-bound termination command is issued *through* the orchestration layer and resolves to a defined safe state; an infrastructure cutoff does not depend on that layer responding at all, and is the only control that survives the orchestration layer itself being the thing that has failed. **Source status, stated:** NCSC's is an interim public-body blog post, not formal guidance; CMORG is an industry taskforce, not a regulator. The FCA's multi-firm review "Frontier AI and cyber resilience" (2 September 2026) is adjacent background on frontier-AI harness controls and **expressly does not set expectations**, so it is not cited as one here.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "we have a kill switch" with no test evidence — **L1**.
- Design specification documenting the defined safe-state behaviour for each side-effecting step type under mid-plan termination — **L2**.
- Staging test: trigger termination mid-plan at multiple points in a representative multi-step workflow; measure time-to-stop and verify resulting state against the defined safe-state design — **L3**.
- Independent audit or red-team exercise confirming no orphaned/inconsistent state was found across a representative set of termination scenarios — **L4**.
- Records of an actual production containment event (if one occurred) showing time-to-stop achieved and reconciliation outcome — **L5**.

## 11. Independent Test
> In a non-production environment, execute a representative multi-step agentic workflow with side-effecting tool calls (using test/synthetic transactions, not live customer data or funds); issue a termination command at multiple points during execution (before, during and after each side-effecting step). Measure time-to-stop against a defined objective and inspect resulting state for orphaned or inconsistent actions. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (kill-switch/containment testing for simple systems is reasonably standard engineering practice — ★3 for that component — but mid-plan agentic termination with in-flight side effects is a genuinely novel test design with no published FS benchmark, pulling overall confidence down).

## 12. Pass Indicators
- Termination testing across multiple mid-plan trigger points consistently meets the defined time-to-stop objective.
- No orphaned or half-completed action is found in any tested scenario; every side-effecting step resolves to its defined safe state.
- Reconciliation step confirms consistent state post-termination in all tested cases.
- Named containment authority (HUM-005) has personally exercised the mechanism, not merely reviewed its design.

## 13. Fail Indicators
- Termination testing has never been performed against a multi-step, side-effecting workflow; only simple single-step "stop" has been tested.
- Testing reveals orphaned or half-completed actions following mid-plan termination.
- Time-to-stop is undefined, or measured testing exceeds any stated objective.
- No reconciliation process exists to detect inconsistent state after a stop event.

## 14. Reporting Language
**Pass:** "Mid-plan termination testing across representative multi-step workflows consistently met the defined time-to-stop objective with no orphaned or inconsistent state identified. Conclusions rest on ★2 methodology — general kill-switch testing is established, but agentic mid-plan termination testing is novel and FS-bespoke — and should be interpreted as a point-in-time capability demonstration."

**Fail:** "No testing of mid-plan agentic termination has been performed; the firm's kill-switch capability has only been validated against simple, non-agentic flows. This is a critical containment gap: an incident response decision to halt the system cannot be relied upon to actually stop in-flight consequences."

**Partial:** "Termination testing has been performed for the payment-initiation agent but not extended to the document-generation or communication-sending agents sharing the same orchestration framework. Remediation should extend testing coverage across all side-effecting agentic workflows."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (contained, reconciled state achieved within the defined time bound)
  Likelihood: 2 (containment is invoked relatively infrequently, but agentic workflows with side effects are increasingly common)
  Detectability: 2 (post-termination reconciliation, if performed, surfaces any residual inconsistency promptly)
  Recoverability: 2 (defined safe states, by design, resolve to a recoverable position)
  Novelty: 3 (mid-plan agentic termination is a genuinely new engineering challenge beyond traditional kill-switch design)

If controls are absent or degraded:
  Severity: 3 (an incident response action fails to actually contain the incident; further erroneous transactions/communications continue)
  Likelihood: 2 (requires both an incident serious enough to trigger containment and an in-flight side-effecting step at that moment — plausible but not routine)
  Detectability: 3 (orphaned state may not be discovered until a separate reconciliation process, potentially days later)
  Recoverability: 3 (manual reconciliation of inconsistent state is slow and itself error-prone)
  Novelty: 4 (fully outside traditional kill-switch/containment testing scope for non-agentic systems)

Residual risk interpretation: This IRQ is a precondition for every other containment-dependent control in the register (HUM-005 authority is meaningless without a working mechanism); testing priority should be high even though incident frequency triggering it may be low.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | A failed containment action allows the original incident's consequences to continue or compound |
| **Likelihood** | 2 | Requires a containment-triggering incident to coincide with in-flight side-effecting actions; plausible but not routine |
| **Detectability** | 3 | Orphaned/inconsistent state may not surface until a separate reconciliation process |
| **Recoverability** | 3 | Manual reconciliation of inconsistent multi-step agentic state is slow and itself error-prone |
| **Novelty** | 4 | Mid-plan agentic termination with in-flight side effects is unfamiliar beyond traditional single-step kill-switch design |

## 17. Regulatory Basis
> [Regulation (EU) 2022/2554, DORA, Art. 11–12] requires ICT business continuity policy and disaster recovery/response plans, encompassing containment and recovery capability. [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021)] establishes the general recoverability expectation for important business services, which this IRQ extends explicitly to mid-plan agentic AI termination as a distinct, testable capability [UNVERIFIED — DORA Art. 11-12 and SS1/21 confirmed extant but do not name agentic AI containment specifically; no sector-specific rule was located] (verified 29 Jul 2026).

## 18. Research Basis
> No peer-reviewed research specifically documents "mid-plan agent termination safety" as a named FS risk area [UNVERIFIED — no such named study was located after search]; this IRQ is grounded in established distributed-systems/transaction-processing engineering principles (safe rollback, idempotent operations, saga pattern compensating transactions) applied to the newer context of LLM-driven agentic orchestration, where side-effecting tool calls introduce genuine termination-safety challenges not present in traditional batch or request-response systems.
>
> **[FAIAS Incident Register, row 76, "An agent used DNS to reach an external chatbot", 2026]** — the developer's own report records that after detection an agent's training run "did not stop automatically as expected" and was stopped by hand two and a half hours later, once the confusion over whether it should have been stopped was resolved. Detection in minutes still left the run going for hours. It evidences the delay in halting, not the safety of the stop itself. The developer is an AI laboratory and the environment an internal training run, not a financial-services firm.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-005 (D.3 Escalation & Override Design: named authority, tested willingness to invoke containment)
  - IRQ-AGT-012 (C.7 Workflow & Action Safety: irreversibility gates reduce orphan-risk surface area; and the agent-specific infrastructure-level halt — the emergency-shutdown limb sits in both canvases, the tested last-resort cutoff for any AI system here and the agent-specific halt there)
  - IRQ-RES-004 (G.2 Containment & Recovery: rollback to known-good state complements termination)
  - IRQ-AGT-002 (C.1 Planning & Goal Drift: goal stability testing relevant to when termination becomes necessary)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 11–12.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] Prudential Regulation Authority, 2022. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2022 (11 March 2022, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.2 (Operational Resilience domain, Containment & Recovery)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Traditional kill-switch thinking assumes clean, atomic stop; agentic side-effecting tool calls violate that assumption invisibly.
✓ Test 2 (Plausible Harm): Grounded in DORA business continuity/recovery obligations and general containment testing expectations.
✓ Test 3 (Testable): Answerable via mid-plan termination testing at multiple execution points.
✓ Test 4 (Decision-Relevant): Outcome gates whether the firm's incident containment capability can be relied upon for agentic systems.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Field 9 — a blunt, infrastructure-level kill mechanism added as an expected control distinct from graceful mid-plan termination, anchored to NCSC "Managing the cyber risk of agentic AI", "Emergency shutdown" item (20 Aug 2026, page metadata modified 24 Aug 2026; interim advice to be superseded) and CMORG "Firm Guidance for Frontier AI" v1.0 §3.1 (June 2026, printed p.5), with both source statuses stated and the FCA review expressly not cited as an expectation. Field 19 — the IRQ-AGT-012 cross-reference extended to name the emergency-shutdown split, per the owner's ruling of 12 September 2026, which places the limb in both canvases: the tested last-resort cutoff for any AI system here, the agent-specific infrastructure-level halt at IRQ-AGT-012, with AGT-003 keeping the network-restriction material. ★2 unchanged; no §11 change proposed — whether the test procedure should gain a separate last-resort step is held.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS1/21 gives its current version, March 2022 (11 March 2022, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 9 — the PRA SS1/21 limb cites a recoverability expectation, in place of a "recoverability/containment" expectation: SS1/21 states no containment expectation. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/21 cited as its March 2022 version (11 March 2022, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 76, OpenAI report on an agent that used DNS to reach an external chatbot, for the delay in halting and not the safety of the stop). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
```

---
---

