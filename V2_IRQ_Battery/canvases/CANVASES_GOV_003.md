# CANVAS: IRQ-GOV-003

## 1. IRQ ID & Title
**IRQ-GOV-003: Approval Conditions Stated but Not Technically Enforced or Monitored**

Register question: "Are approval conditions and usage restrictions (approved tasks, user groups, guardrails) technically enforced and monitored, or only stated in the approval paper?"

## 2. Business Activities Affected
- **All approved AI deployments with scoped conditions of use:** approval papers routinely restrict a system to specific tasks, user groups or output types (e.g., "triage only, no final decisions"; "internal staff only, not customer-facing"); every business activity relying on that restriction is exposed if it is not technically enforced.
- **Business-as-usual expansion of use:** teams naturally seek to use a working tool more broadly than originally approved (e.g., extending a drafting assistant from internal memos to customer correspondence) — the direct precursor to IRQ-GOV-012 envelope drift.
- **Access-controlled and permissioned processes:** any process where the approval restricted the system to a named user group (e.g., senior underwriters only) is exposed if access control is policy-only.

## 3. AI Behaviour(s)
- Executes whatever tasks it is technically capable of and given input for, regardless of what the approval paper says it is intended for — the system itself has no awareness of its own approval scope unless that scope is encoded as a technical constraint.
- Is accessible to whichever users hold a valid credential, regardless of whether that credential-holder is within the approved user group, unless access control is technically scoped.

## 4. Failure Mode
> Approval conditions and usage restrictions exist only as prose in an approval paper, with no corresponding technical enforcement (access control, task-scoping, guardrail configuration) or monitoring to detect breach, so the system is in practice used beyond its approved scope without anyone knowing.

## 5. Potential Consequences
- **Customer:** A system approved for internal-only use is exposed to customers, or a system approved for triage-only is relied upon for final decisions, without the additional controls (bias testing, human oversight) that broader use would have required.
- **Institution:** The approval paper becomes a fiction — governance decisions on record do not reflect actual production use; the firm cannot demonstrate to a regulator that stated conditions of use are real controls rather than aspirations.
- **Regulator/market:** A supervisory finding that approval conditions are unenforced converts what looked like a controlled deployment into evidence of governance theatre, with knock-on credibility damage to the whole approval framework.

## 6. Failure Chain
```
System approved with specific conditions of use (task scope, user group, guardrails)
recorded in the approval paper
  ↓ (IRQ-GOV-003 — THIS IRQ: no technical enforcement configured to match the paper)
Business users, under commercial pressure or convenience, use the system beyond
approved scope (broader tasks, wider user access, guardrails bypassed)
  ↓ (IRQ-GOV-012: this IS operating-envelope drift in its most common form)
No monitoring exists to detect the mismatch between approved and actual use
  ↓ (IRQ-GOV-008: no signal reaches governance to trigger re-approval)
Out-of-scope use continues, unassured by the controls the narrower approval assumed
  ↓
Failure occurs in a use case never actually tested or approved →
harm or incident → post-incident review discovers approval paper never matched reality →
governance credibility damage

Control Breakpoints:
  • IRQ-GOV-003: technical enforcement of conditions of use, not policy alone
  • IRQ-GOV-012: periodic reconciliation of actual vs approved envelope
  • IRQ-GOV-008: monitoring signals reach governance and trigger revalidation
  • IRQ-AGT-003: least-privilege tool scoping as the technical enforcement mechanism for agentic systems
```

## 7. Why a Domain Expert May Miss It
- In traditional model governance, "restricted to X" is usually enforced structurally because the model itself was built only to do X (e.g., a credit scorecard cannot draft marketing copy); SMEs are not used to a technology general-purpose enough that the same deployed system is technically capable of far more than its approval scope.
- Approval papers are the artefact SMEs are trained to review; they are not trained to separately verify that the platform configuration (access groups, system prompts, tool permissions) actually matches what the paper says.
- Guardrails are often described in the approval paper in the passive voice ("the system will only be used for X") without specifying who enforces it — reading this as a control, rather than an intention, is the blind spot.
- Business users expanding use incrementally (a few extra tasks at a time) does not look like a single "breach" event that would trigger a governance review under a traditional change-control mental model.

## 8. Assurance Objective
**AO-GOV-003:** Approval conditions and usage restrictions shall be technically enforced in the deployed platform and independently monitored for breach, such that actual use cannot silently diverge from the approved scope.

## 9. Expected Controls (Traced)
- **Technical access control matching approved user groups (role-based access control, SSO group scoping)** — [ISO/IEC 42001:2023, clause 8.1 (operational planning and control)] — approved conditions of use are operationalised as system configuration, not policy alone.
- **Task-scoping via system prompt/guardrail configuration with tamper-evident change control** — [OWASP LLM Top 10 guidance on excessive agency and system-prompt handling, 2025 edition; linked IRQ-MOD-013 change control] — restricts what the system will do even for authorised users, with changes to that scoping logged and reviewable.
- **Least-privilege tool exposure matching approved task scope for agentic systems** — [linked IRQ-AGT-003; OWASP LLM06/agency guidance 2025] — an agent's tool permissions are the technical enforcement mechanism for its approved action scope.
- **Periodic reconciliation of actual usage logs against approved conditions of use** — [PRA SS1/23, May 2023, ongoing monitoring and periodic validation expectations] — Emerging Practice: applying SS1/23's ongoing monitoring expectation specifically to conditions-of-use reconciliation (as distinct from model performance monitoring) is not yet standard MRM practice.
- **EU AI Act intended-purpose and use-restriction documentation with logging obligations where in scope** — [Regulation (EU) 2024/1689, Art. 9 (risk management) and Art. 12 (record-keeping/logging)] — for in-scope high-risk systems, logging supports post-hoc verification that use matched intended purpose.

## 10. Expected Evidence (Tagged L1–L5)
- Approval paper stating conditions of use — **L1** (states intent, provides no evidence of enforcement).
- Platform configuration documentation showing access control groups, task-scoping prompts and tool permissions as configured — **L2**.
- Configuration inspection confirming the technical settings actually match the approval paper's stated conditions (e.g., the access group in the identity system corresponds to the approved user group) — **L3**.
- Usage log analysis (staging or production-representative) reconciling actual task types and user identities against approved scope — **L3/L5** depending on log source.
- Internal audit report on conditions-of-use enforcement testing across a sample of approved systems — **L4**.
- Incident or exception log showing at least one detected and remediated breach of conditions of use, evidencing the monitoring is live — **L5**.

## 11. Independent Test
> For a risk-based sample of approved AI systems, obtain the approval paper's stated conditions of use (task scope, user group, guardrails) and independently inspect the corresponding platform configuration (access control lists, system prompt/guardrail settings, tool permission grants). For systems with usable production or production-representative logs, reconcile a sample of actual usage events against the approved scope, flagging any task type or user identity outside it. Attempt to exercise the system slightly outside its stated scope in a staging replica (e.g., attempt an out-of-scope task type, attempt access as a non-approved user role) to test whether technical controls, not just policy, prevent it. Methodology follows standard configuration-audit and control-testing practice (as-designed vs as-configured reconciliation), extended to AI-specific conditions of use with no AI-specific benchmark. Conducted in staging/configuration review only; no production data exercised for the out-of-scope attempt. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established configuration-audit methodology adapted from IT/cyber control testing; no AI-specific standard defines what "sufficient" technical enforcement looks like for GenAI conditions of use, so professional judgement determines adequacy).

## 12. Pass Indicators
- Platform configuration for 100% of the sample technically matches the approval paper's stated conditions of use (access groups, task scoping, tool permissions).
- Staging attempts to exercise the system outside its approved scope are blocked or flagged, not silently permitted.
- Usage log reconciliation finds no material volume of out-of-scope task types or user identities.
- At least one documented instance exists of the monitoring mechanism detecting and triggering remediation of an out-of-scope use.
- Changes to task-scoping configuration are logged and traceable to an approved change record.

## 13. Fail Indicators
- Platform configuration does not match the approval paper — e.g., access is open to a broader user group than approved, or no task-scoping guardrail is actually configured.
- Staging attempts to exercise the system outside approved scope succeed without any block or flag.
- Usage log reconciliation finds material out-of-scope use with no corresponding governance awareness or action.
- Enforcement relies solely on user training/policy ("staff are told not to use it for X") with no technical control (L1/L2 evidence only).
- No mechanism exists to detect conditions-of-use drift; the first anyone learns of out-of-scope use is via an incident.

## 14. Reporting Language
**Pass:** "Independent testing across [n] approved systems confirms that stated conditions of use are technically enforced in platform configuration — access control, task scoping and tool permissions match the approval paper — and that reconciliation of usage logs found no material out-of-scope use. Staging attempts to exercise the system beyond its approved scope were blocked. Conclusions rest on ★3 methodology — established configuration-audit practice with no AI-specific benchmark — and should be read as professional assessment."
**Fail:** "Testing found that conditions of use for [n] of [sample size] systems exist only in the approval paper: platform configuration permits access or tasks beyond the approved scope, and staging attempts to exercise the system out-of-scope succeeded without any technical block. Actual production use cannot be assumed to match approved scope; the assurance basis for the original approval — which assumed the narrower scope — should be treated as unsupported until enforcement and monitoring are implemented."
**Partial:** "Access control is technically enforced and matches approval for [n]% of the sample, but task-scoping guardrails are configuration-only in [x]% of cases with no logged monitoring of drift. The assurance objective is not yet met for that subset; remediation should implement usage reconciliation within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (severity is inherited from whatever the out-of-scope use turns out to be; the
              control itself is preventive, not the harm mechanism)
  Likelihood: 3 (probable absent enforcement — commercial pressure to extend a working tool
              beyond its narrow approval scope is a routine, foreseeable business behaviour)
  Detectability: 2 (detected within a review cycle via configuration audit or log reconciliation;
              not real-time without dedicated monitoring)
  Recoverability: 1 (reversible quickly by re-scoping configuration or re-approving the wider use)
  Novelty: 3 (domain expert reviewing the approval paper's prose would very likely miss that no
              corresponding technical control was ever configured)

Interpretation: acceptable residual risk with active enforcement and reconciliation; the
material concern is that this is the direct precursor mechanism to IRQ-GOV-012 envelope drift —
weak controls here are a leading indicator of envelope drift risk across the whole AI estate.

If controls are absent or degraded:
  Severity: 3 (out-of-scope use can extend into customer-facing, higher-stakes decisions the
              original narrower approval never assessed for bias, hallucination or oversight risk)
  Likelihood: 4 (near-certain over time absent enforcement — informal scope creep is standard
              organisational behaviour for any useful tool)
  Detectability: 4 (silent by default; nothing distinguishes in-scope from out-of-scope use
              without dedicated reconciliation)
  Recoverability: 2 (once discovered, requires retrospective assessment of harm across the
              unknown-duration drift window before simple re-scoping is sufficient)
  Novelty: 3
Residual risk: High without technical enforcement; this IRQ is a leading indicator for GOV-012.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Severity is inherited from the specific out-of-scope use; the control gap itself is preventive rather than a harm mechanism. |
| **Likelihood** | 3 | Probable if unenforced: extending a useful tool beyond its narrow approval is routine commercial behaviour, not requiring malicious intent. |
| **Detectability** | 3 | Silent by default absent reconciliation; discovered via periodic audit or, worse, via an incident in the unapproved use case. |
| **Recoverability** | 2 | Fast to re-scope once found, but any harm accrued during an unknown-duration drift window requires separate retrospective assessment. |
| **Novelty** | 3 | Domain experts reviewing approval-paper prose typically do not separately verify platform configuration; the paper-vs-reality gap is AI-platform-specific. |

## 17. Regulatory Basis
> [PRA, SS1/23, May 2023, ongoing monitoring and use principles] requires that model use is monitored against approved parameters, extending to technical enforcement of conditions of use for AI systems. [ISO/IEC 42001:2023, clause 8.1] requires operational planning and control to actually implement AI management system requirements, not merely document them. [Regulation (EU) 2024/1689 (EU AI Act), Art. 9 and Art. 12] requires risk management and record-keeping/logging for in-scope high-risk systems, supporting post-hoc verification of intended-use compliance. [FCA, "AI Update," Apr 2024] confirms SYSC governance requirements apply, including that stated controls must be operationally real. [Financial Services and Markets Act 2000, s.19(1)] provides the underlying statutory reason conditions of use must be technically enforced, not merely stated: "No person may carry on a regulated activity in the United Kingdom, or purport to do so, unless he is—(a) an authorised person; or (b) an exempt person." (s.19(2) names this the general prohibition.) Where an approval scopes an AI system's conditions of use precisely to keep its output inside the firm's permitted activities — e.g. triage or drafting only, not advice — an unenforced condition is not merely a governance gap; it is the mechanism by which the system's actual output could cross into activity the firm is not authorised to carry on, engaging s.19 directly rather than by analogy.

## 18. Research Basis
> No peer-reviewed academic literature specifically addressing conditions-of-use enforcement gaps in deployed enterprise GenAI was identified in the source registers; this control area is governance/audit practice rather than a research literature, consistent with this domain's evidentiary profile. [OWASP Top 10 for LLM Applications 2025] is treated as the closest available applied-practice source for guardrail/configuration control adequacy.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-012 (I.2: operating-envelope drift — this IRQ's failure is the direct precursor mechanism)
  - IRQ-GOV-004 (I.2: tiering — sets what conditions of use should be in the first place)
  - IRQ-AGT-003 (C.2: least-privilege tool exposure — the technical enforcement mechanism for agentic scope)
  - IRQ-GOV-008 (I.3: monitoring signals reaching governance — required to detect drift once it occurs)
  - IRQ-HUM-002 (D.1: approval theatre — parallel concept applied to human review checkpoints rather than platform configuration)
```

## 20. References
```
[1] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[2] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management system."
    Clause 8.1.
[3] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L, 12 July 2024. Art. 9, Art. 12.
[4] FCA, 2024. "AI Update." April 2024.
[5] OWASP Foundation, 2025. "OWASP Top 10 for LLM Applications 2025."
[6] United Kingdom, 2000. "Financial Services and Markets Act 2000." s.19
    (The general prohibition).
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.2 (Governance domain, Approval, Tiering & Policy)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): SMEs review approval-paper prose and treat stated conditions of
  use as controls; they do not routinely verify that platform configuration technically
  matches what the paper says, unlike traditional single-purpose models.
✓ Test 2 (Plausible Harm): Grounded in SS1/23's ongoing-monitoring expectation and the
  well-documented organisational tendency to extend useful tools beyond narrow approvals;
  this is the direct mechanism behind IRQ-GOV-012 envelope drift.
✓ Test 3 (Testable): Testable via configuration inspection, staging out-of-scope exercise
  attempts, and usage log reconciliation. ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome determines whether the original approval's assumed
  scope can be relied upon, and gates whether re-approval is needed for actual use.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.1 (2026-07-31): Added FSMA 2000 s.19 legal anchor to Regulatory Basis and
  References — conditions of use exist precisely to
  keep output inside permitted activities.
```

---
---

