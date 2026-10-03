# CANVAS: IRQ-AGT-011

## 1. IRQ ID & Title
**IRQ-AGT-011: Consequential Actions Occurring in Hidden Chains Without Reviewable Traces**

Register question: "Are all agent actions — including intermediate tool calls and abandoned branches — captured in reviewable traces, or can consequential actions occur in hidden chains?"

## 2. Business Activities Affected
- **All agent-automated decisions and transactions:** Every business activity elsewhere in this domain (AML investigation, payments, claims, lending) depends on this control as a prerequisite: none of the drift-detection, conformance-checking or attribution controls described in other AGT canvases can function without complete traces.
- **Incident investigation and complaint response:** When a customer disputes an AI-influenced outcome, the firm's ability to reconstruct exactly what the agent did — including abandoned reasoning branches and intermediate tool calls that did not make it into the final output — determines whether the dispute can be resolved with evidence rather than assertion.
- **Regulatory examination:** Supervisors reviewing an agentic system's conduct require a complete, tamper-evident record of what the system actually did, not merely its final output.

## 3. AI Behaviour(s)
- Executes a sequence of reasoning steps, tool calls and intermediate outputs to arrive at a final action or response, some of which may be abandoned, retried or superseded during execution.
- Some intermediate steps (failed tool calls, abandoned reasoning paths, retried actions) may not be surfaced in the final output or in default logging, particularly where logging is configured to capture only the final result for storage-efficiency reasons.
- Operates across potentially multiple systems, sessions or sub-agents (per IRQ-AGT-006/007), each of which may log independently and incompletely, such that no single trace captures the full picture.

## 4. Failure Mode
> A consequential action taken by the agent — or a step in the chain leading to it, including an abandoned branch or intermediate tool call — is not captured in a complete, reviewable, tamper-evident trace, such that the firm cannot reconstruct what actually happened for audit, complaint-handling or regulatory purposes.

## 5. Potential Consequences
- **Customer:** A dispute over an AI-influenced decision cannot be resolved with evidence because the trace is incomplete; the customer's contest right (per IRQ-HUM-008) becomes hollow without a reconstructable record.
- **Institution:** Every other agentic control in this domain — drift detection (AGT-001/002), conformance checking (AGT-010), multi-agent attribution (AGT-007), memory validation (AGT-008) — depends on trace completeness; its absence is a single point of failure for the whole domain's assurance case.
- **Regulator/market:** Inability to reconstruct a consequential AI-influenced decision on request is itself a supervisory finding, independent of whether the underlying decision was correct.

## 6. Failure Chain
```
Agent executes a multi-step task involving tool calls, intermediate
reasoning, and possibly abandoned or retried branches
  ↓ (IRQ-AGT-011 — THIS IRQ: logging configured to capture only final
     output, or distributed across systems with no unified record)
Intermediate steps — including a failed or abandoned action that
nonetheless had a side effect, or a tool call whose result was later
discarded — are not retained
  ↓ (IRQ-GOV-010: record-keeping standard not met for full decision
     reconstruction)
An incident, complaint or regulatory enquiry requires reconstruction of
what the agent actually did
  ↓ (IRQ-HUM-008: customer contest route cannot produce genuine evidence
     of what happened, only the final output)
Investigation cannot establish root cause or confirm/refute the
customer's account; response is asserted rather than evidenced
  ↓
Regulatory/complaint escalation → finding that record-keeping was
inadequate for a consequential automated decision → remediation and
reputational cost, independent of the original decision's correctness

Control Breakpoints:
  • IRQ-AGT-011: complete, structured, tamper-evident logging of every
    step including abandoned branches
  • IRQ-GOV-010: retention periods and reconstruction capability meeting
    audit/regulatory requirements
  • IRQ-AGT-006/007: multi-agent/sub-agent logging unified into a single
    reconstructable record, not fragmented across components
```

## 7. Why a Domain Expert May Miss It
- Traditional audit trail requirements were designed around discrete, human-initiated transactions with a clear start and end; SMEs may assume "we log the transaction" is sufficient without recognising that an agent's *path* to a transaction — including steps that did not become the final output — is itself part of what needs to be reconstructable.
- Storage-cost and engineering-simplicity pressures naturally push toward logging only final outputs; this looks like a reasonable engineering trade-off rather than an assurance gap, unless someone explicitly asks "could we reconstruct an abandoned branch that had a side effect?"
- Multi-agent and multi-system architectures fragment logging by default (each component logs its own view); SMEs reviewing "is there an audit trail?" may see that each component individually logs something, without checking whether the combination reconstructs a coherent whole.
- Testing gap: audit-readiness testing typically checks whether the final decision can be explained, not whether every intermediate step — including ones that did not survive to the final output — can be reconstructed.

## 8. Assurance Objective
**AO-AGT-011:** Every agent action, including intermediate tool calls, abandoned reasoning branches and multi-component/sub-agent steps, shall be captured in a complete, tamper-evident, unified trace sufficient to reconstruct the full path to any consequential outcome.

## 9. Expected Controls (Traced)
- **Complete action logging including abandoned/retried branches, not only final output** — [Chan et al., "Visibility into AI Agents," FAccT 2024, arXiv:2401.13138, identifiers/real-time monitoring/activity-log recommendations] — logging configuration explicitly captures intermediate steps that did not survive to the final result.
- **Tamper-evident log design** — [ISO/IEC 27001 logging and monitoring controls, applied by analogy; FCA/PRA record-keeping expectations] — logs are protected against retrospective alteration, supporting their evidential value in disputes and examinations.
- **Unified trace across multi-agent/multi-system components** — [linked IRQ-AGT-006, IRQ-AGT-007; NIST AI 600-1, Jul 2024] — logging is designed and tested to reconstruct a coherent end-to-end record even where multiple agents or systems were involved.
- **Retention periods meeting regulatory record-keeping requirements** — [linked IRQ-GOV-010; FCA SYSC/DISP record-keeping rules] — traces are retained for the period required to support audit, complaint and regulatory response.
- **Periodic reconstruction testing** — [PRA SS1/23 ongoing monitoring/validation principle] — the firm periodically exercises full reconstruction of a real or representative case from the trace alone, to confirm the control functions in practice, not only on paper.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "we log everything" with no specification of what "everything" includes — **L1**.
- Logging architecture documentation specifying exactly which events (including abandoned branches, retries, sub-agent steps) are captured and retained — **L2**.
- Configuration inspection confirming the logging pipeline actually captures the documented event set across all components, including secondary/fallback paths — **L3**.
- Staging test results: a deliberately constructed multi-step task with an abandoned branch and a retried tool call, followed by an attempted full reconstruction from the logs alone — **L3**.
- Independent audit confirming tamper-evidence, retention compliance and reconstruction capability — **L4**.
- Production reconstruction exercise: a real or representative case fully reconstructed from logs alone, with time-to-reconstruct and completeness assessed — **L5**.

## 11. Independent Test
> In a non-production environment, execute a representative multi-step agentic task deliberately engineered to include an abandoned reasoning branch (the agent starts down one path, then changes approach), a retried tool call (a first attempt fails and is retried with different parameters), and, where applicable, a sub-agent delegation. Attempt to fully reconstruct the end-to-end path — including the abandoned branch and the failed first attempt — using only the retained logs, with no access to the live system. Measure: (1) completeness of reconstruction (were the abandoned/retried steps recoverable, or only the final successful path); (2) time-to-reconstruct; (3) whether logs from any sub-agent or secondary system were captured and correctly correlated into the unified trace. Methodology informed by Chan et al.'s visibility/activity-log framework. No production data used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (Chan et al. provides credible, published research grounding for the required logging properties; the specific reconstruction-completeness test is bespoke to the firm's logging architecture, with no external benchmark).

## 12. Pass Indicators
- Full reconstruction of the abandoned branch and retried tool call succeeds using logs alone, with no gap.
- Sub-agent/multi-system logs are correctly correlated into a single coherent trace.
- Logs are demonstrably tamper-evident (e.g. cryptographic integrity checks, write-once storage, or equivalent).
- Retention periods meet or exceed the firm's regulatory record-keeping requirement for the relevant business activity.
- A production reconstruction exercise on a real case succeeds within a reasonable time.

## 13. Fail Indicators
- The abandoned branch or retried tool call cannot be reconstructed; only the final successful path is recoverable from logs.
- Sub-agent or secondary-system logs exist but cannot be correlated into a unified trace (fragmented record).
- Logs are mutable with no tamper-evidence mechanism.
- Retention period is shorter than the regulatory requirement for the business activity in question.
- A production reconstruction exercise fails or takes materially longer than an acceptable investigation timeline.

## 14. Reporting Language
**Pass:** "Testing on a deliberately engineered multi-step task with an abandoned branch, a retried tool call and a sub-agent delegation confirms full end-to-end reconstruction is possible from retained logs alone, correctly correlated across components, with tamper-evident storage and retention meeting regulatory requirements. This is a ★2 assessment — credible published visibility research, bespoke reconstruction testing — and should be re-verified whenever the logging architecture or agent topology changes."

**Fail:** "Testing demonstrates that an abandoned reasoning branch and a retried tool call — despite the retry having had a side effect — are not recoverable from the retained logs, which capture only the final successful output. This means the firm cannot currently reconstruct the actual path to a consequential decision for audit, complaint-handling or regulatory purposes, which is itself a supervisory finding independent of whether any individual decision was correct. This should be remediated as a foundational control before further reliance is placed on any other agentic assurance control in this domain."

**Partial:** "Reconstruction succeeds for the primary agent but not for its sub-agent delegations, whose logs are captured separately and cannot currently be correlated into a unified trace, affecting [x]% of tasks involving delegation. Remediation should prioritise unifying multi-component logging."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (bounded to audit/evidential gaps for the specific cases affected;
              no direct customer harm from the logging gap itself)
  Likelihood: 2 (requires the logging pipeline to have a specific unaddressed
               gap — abandoned branches, sub-agent correlation — despite
               otherwise sound design)
  Detectability: 2 (periodic reconstruction testing surfaces gaps proactively
                    rather than only during a live incident)
  Recoverability: 2 (logging architecture gaps are fixable prospectively;
                     retrospective reconstruction of past cases may not be)
  Novelty: 3 (requires recognising that abandoned/intermediate steps, not just
              final outputs, are part of the required evidential record)

Interpretation: acceptable with complete, unified, periodically-tested logging;
highest concern is that this control underpins every other agentic assurance
control — its failure is silent until an incident specifically requires
reconstruction, by which point past gaps cannot be retrofitted.

If controls are absent or degraded:
  Severity: 4 (undermines every other agentic control's evidential basis;
              inability to respond to regulatory examination of any
              consequential agentic decision)
  Likelihood: 3 (storage-efficiency-driven "final output only" logging is a
               common default engineering pattern, not a rare gap)
  Detectability: 4 (invisible until a specific incident requires
                    reconstruction — by definition, too late to fix
                    retrospectively for that case)
  Recoverability: 4 (past gaps in the evidential record cannot be
                     retrospectively filled; only prospective fix is possible)
  Novelty: 3
Residual risk: Critical. This is a foundational, cross-cutting control for the
entire Agentic domain and should be verified before relying on any other
agentic assurance conclusion.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 4 | Undermines the evidential basis of every other agentic control and the firm's ability to respond to regulatory examination of any consequential decision. |
| **Likelihood** | 3 | Storage-efficiency-driven "final output only" logging and fragmented multi-component logs are common default patterns absent deliberate design. |
| **Detectability** | 4 | Invisible until a specific incident requires reconstruction — by which point the gap for that case cannot be retrospectively fixed. |
| **Recoverability** | 4 | Past evidential gaps cannot be filled retrospectively; only a prospective architectural fix is possible, and it does not repair the historical record. |
| **Novelty** | 3 | Recognising that abandoned/intermediate steps form part of the required evidential record, not just the final output, is a non-obvious extension of traditional audit-trail thinking. |

## 17. Regulatory Basis
> [FCA/PRA record-keeping expectations under SYSC and DISP] require firms to retain records sufficient to reconstruct decisions for audit, complaint and regulatory purposes; an incomplete agentic trace does not meet this standard where the AI system materially influenced the decision. [PRA SS1/23, May 2023] requires governance and monitoring evidence for models within MRM scope, including agentic components. [EU AI Act, Regulation (EU) 2024/1689, Art. 12 (record-keeping/logging) and Art. 19 (log retention)] establishes explicit automatic-logging and retention obligations for high-risk AI systems, directly applicable where the agent supports credit or other Annex III high-risk activities (from 2 Dec 2027, per the Digital Omnibus postponement of Annex III deadlines agreed Jul 2026). (corrected & verified 29 Jul 2026)

## 18. Research Basis
> [Chan, A., et al., 2024, "Visibility into AI Agents," FAccT 2024, arXiv:2401.13138] — establishes identifiers, real-time monitoring and activity logs as the core requirements for agent oversight, directly informing this IRQ's control set. [Microsoft AI Red Team, 2025, "Taxonomy of Failure Modes in Agentic AI Systems," April 2025] — names "hidden chains" and incomplete observability as a recognised agentic failure category. [Anthropic, 2024, "Sabotage Evaluations for Frontier Models"] — evaluation framework premised on the ability to observe and audit an agent's actual behaviour, underscoring why complete traces are a prerequisite for any downstream agentic assurance activity.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-GOV-010 (I.4: record-keeping standard supporting full decision
    reconstruction — the governance-domain counterpart to this control)
  - IRQ-AGT-001 / IRQ-AGT-010 (C.1/C.7: drift and conformance detection —
    both structurally depend on this IRQ's trace completeness)
  - IRQ-AGT-007 (C.4: multi-agent attribution — requires unified, per-agent
    traces this IRQ provides)
  - IRQ-HUM-008 (D.4: customer contest route — requires genuine reconstructable
    evidence, not assertion, to be meaningful)
  - IRQ-HUM-004 (D.3: oversight reconstruction capacity — depends on the trace
    completeness this IRQ establishes)
  - IRQ-AGT-002 / IRQ-AGT-013 (C.1/C.7: intent-change and GUI-action evidence —
    both rely on this IRQ's traces to establish what the agent knew and perceived)
```

## 20. References
```
[1] Chan, A., et al., 2024. "Visibility into AI Agents." Proc. FAccT 2024.
    arXiv:2401.13138.
[2] Microsoft AI Red Team, 2025. "Taxonomy of Failure Modes in Agentic AI Systems."
    April 2025.
[3] Anthropic, 2024. "Sabotage Evaluations for Frontier Models." October 2024.
[4] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act,"
    Articles 12 and 19. OJ L 12.7.2024.
[5] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: C.7 (Agentic domain, Workflow & Action Safety)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): SMEs equate "we log transactions" with adequate audit
  trail, missing that abandoned branches and intermediate steps — not part of
  traditional discrete-transaction logging — are part of what must be
  reconstructable for an agentic system.
✓ Test 2 (Plausible Harm): Grounded in Chan et al.'s visibility/activity-log
  research and Microsoft's failure-mode taxonomy naming hidden chains explicitly.
✓ Test 3 (Testable): Fully testable via engineered multi-step tasks with abandoned/
  retried branches, reconstructed from logs alone in a non-production environment.
  ★2 methodology, honestly caveated.
✓ Test 4 (Decision-Relevant): Foundational — gates reliance on every other
  agentic control in this domain; sets logging architecture requirements as a
  condition of use for any consequential agentic deployment.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed; flagged as a
  foundational, cross-cutting control for the domain.
```

---
---

