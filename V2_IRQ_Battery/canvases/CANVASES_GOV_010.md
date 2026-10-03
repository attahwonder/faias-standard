# CANVAS: IRQ-GOV-010

## 1. IRQ ID & Title
**IRQ-GOV-010: Retained Records Insufficient to Reconstruct a Consequential AI-Influenced Decision**

Register question: "Would retained records — inputs, outputs, versions, agent traces, human decisions — allow full reconstruction of any consequential decision for audit, complaint or regulatory purposes?"

## 2. Business Activities Affected
- **Complaint handling and FOS referrals:** where a customer disputes an AI-influenced decision, the firm must be able to reconstruct exactly what the system was asked, what it produced, which version was running, and what a human decision-maker did with the output — without this, the firm cannot substantively respond to the complaint.
- **Regulatory enquiry and enforcement investigation:** a regulator investigating a specific decision or pattern of decisions will request the full record; gaps force the firm to rely on reconstruction from memory or inference, which is both slower and weaker evidentially.
- **Internal post-incident review:** root-cause analysis after any AI-related incident depends entirely on the retained record; a gap in agent traces, model versioning or human decision logging can make root cause permanently unknowable.

## 3. AI Behaviour(s)
- Generates outputs and, where agentic, executes multi-step actions and tool invocations, all of which are candidate record-keeping events; the system does not inherently guarantee retention, completeness or non-repudiation of any of these events without an explicit record-keeping architecture.

## 4. Failure Mode
> The retained record for a consequential AI-influenced decision — comprising inputs, outputs, model/prompt version, intermediate agent traces (where applicable) and the human decision-maker's action — is incomplete, non-attributable, prematurely purged, or not reconstructable in the sequence in which events actually occurred, such that the firm cannot fully reconstruct what happened for audit, complaint-handling or regulatory purposes.

## 5. Potential Consequences
- **Customer:** A legitimate complaint cannot be properly investigated because the specific inputs, model version or agent trajectory behind the disputed decision were never retained or cannot be retrieved, leaving the customer without a substantive response and the firm unable to identify whether the decision was actually correct.
- **Institution:** In litigation or FOS referral, an inability to produce the record is treated adversely — the firm bears the evidential burden and an absent record is generally construed against it; remediation costs escalate where a systemic gap means an entire cohort of decisions cannot be reconstructed.
- **Regulator/market:** EU AI Act Art. 12 (record-keeping/logging) and Art. 19 (log retention) create explicit, binding logging and retention obligations for in-scope high-risk systems; a firm unable to produce records on request faces a direct compliance finding, and FCA/PRA record-keeping expectations under SYSC apply more broadly across all AI-influenced regulated decisions.

## 6. Failure Chain
```
AI system supports or makes a consequential decision (credit, claims, AML
disposition); inputs, outputs, model version, agent trace and human action are
generated as transient artefacts during execution
  ↓ (IRQ-AGT-011: agentic action traces may not be captured completely, especially
  abandoned branches or intermediate tool calls)
Record-keeping architecture retains some but not all artefact types, or retains
them without reliable cross-linkage (e.g. output retained but not the exact
model/prompt version that produced it, or agent trace retained but not linked
to the specific human reviewer's subsequent action)
  ↓ (IRQ-GOV-010 — THIS IRQ: retained record does not allow full reconstruction)
Retention period lapses on some artefact types before a complaint, audit or
regulatory request arrives, or records are purged inconsistently across systems
  ↓ (IRQ-DAT-010: memory/conversation store retention not aligned to the
  decision-record retention requirement)
Customer complaint, audit request or regulatory enquiry arrives; the firm
attempts reconstruction and finds a material gap
  ↓
Complaint cannot be substantively investigated / regulatory response is
incomplete → adverse finding, potential enforcement, reputational damage,
and root cause of the underlying issue (if any) remains unresolved

Control Breakpoints:
  • IRQ-AGT-011: complete, tamper-evident action traces as the primary agentic input
    to this IRQ's record set
  • IRQ-GOV-010: cross-linked, retained record set spanning inputs, outputs, version,
    trace and human decision, tested for actual reconstructability
  • IRQ-DAT-010: retention schedule alignment between memory/conversation stores and
    the decision-record retention requirement
  • IRQ-HUM-006: named decision-level accountability gives the human-action component
    of the record an attributable owner
```

## 7. Why a Domain Expert May Miss It
- SMEs experienced with structured, tabular decision systems (a credit-scoring engine with a fixed input/output schema) assume record retention is straightforward; they may not appreciate that a GenAI/agentic system's "decision" is the product of a specific prompt, a specific model version, a multi-step trajectory and a human's subsequent action — four artefact types that must all be retained and cross-linked, not one row in a decision table.
- Retention policy is often set at the system level (e.g. "logs retained for 7 years") without checking that every component (prompt/version metadata, intermediate agent tool calls, the human reviewer's specific action against the specific output) is actually captured by that policy, rather than only the final customer-facing output.
- Model or prompt version metadata is frequently the artefact most likely to be missing, because it is generated by the infrastructure layer (deployment pipeline, prompt-management system) rather than the application layer that most logging effort focuses on — a reviewer checking "are outputs logged" can miss that version linkage is absent.
- Agentic abandoned branches (a plan the agent started but did not complete, or a tool call that failed) are easy to omit from logging because they did not produce the final output — but they may be exactly where an anomalous decision path first diverged.

## 8. Assurance Objective
**AO-GOV-010:** Retained records for every consequential AI-influenced decision shall span inputs, outputs, model/prompt version, agent traces (where applicable) and the human decision-maker's action, cross-linked and retained for a period sufficient to support audit, complaint and regulatory reconstruction, and this reconstructability shall be demonstrated by test, not assumed from the existence of individual logs.

## 9. Expected Controls (Traced)
- **Cross-linked retention of inputs, outputs, model/prompt version and human decision action for every consequential decision** — [EU AI Act, Regulation (EU) 2024/1689, Art. 12 (record-keeping) and Art. 19 (log retention)] — the direct binding anchor for in-scope high-risk systems, requiring automatic logging capable of enabling traceability of the system's functioning.
- **Complete, tamper-evident agentic action traces, including abandoned branches and intermediate tool calls** — [linked IRQ-AGT-011; NIST AI 100-1, Jan 2023, MEASURE function traceability guidance] — closes the specific agentic-trace gap this IRQ depends on as an upstream input.
- **Retention period aligned to the longer of regulatory (EU AI Act Art. 19; FCA/PRA record-keeping under SYSC) and complaint-handling (FOS time-limit) requirements, applied consistently across all artefact types including memory/conversation stores** — [FCA, DISP rules on complaint time limits; linked IRQ-DAT-010] — prevents differential purging where one artefact type's retention policy is shorter than another's for the same decision.
- **Periodic reconstruction test: sample a historical decision and attempt full reconstruction from retained records alone, timed and scored for completeness** — [Emerging Practice, drawing on internal-audit evidentiary-sufficiency testing methodology] — no AI-specific published standard defines this test; included as good practice given the EU AI Act's traceability requirement is otherwise untested until an actual request arrives.
- **Named decision-level accountability record linking the human reviewer's identity and action to the specific output reviewed** — [linked IRQ-HUM-006; FCA SM&CR] — closes the human-action-attribution component of the record set.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "all decisions are logged" — **L1** (assertion; does not evidence cross-linkage or reconstructability).
- Record-keeping architecture documentation specifying which artefact types are retained, for how long, and how they are cross-linked — **L2**.
- Code/configuration inspection confirming version metadata (model/prompt) is actually captured and linked to each output at the point of generation — **L3**.
- Reconstruction test results: a sample of historical decisions reconstructed end-to-end from retained records alone, with completeness scored and time-to-reconstruct measured — **L3**.
- Internal audit or independent assessment of record-keeping architecture against the EU AI Act Art. 12/19 requirements (for in-scope systems) — **L4**.
- Evidence from an actual historical complaint, audit or regulatory request: the record set that was in fact produced, and whether it was judged complete by the requesting party — **L5**.

## 11. Independent Test
> Select a risk-based sample of historical consequential decisions (spanning static predictive, generative-assistant and agentic system types) across the AI inventory. For each, attempt full reconstruction using only the retained record set: identify the exact input, the exact output, the model/prompt version in effect at the time, the complete agent trajectory (including any abandoned branches, where applicable), and the specific human reviewer's action and rationale. Score each reconstruction attempt as complete, partially complete (specify the missing artefact type), or not reconstructable. Separately, verify retention-period alignment across artefact types for the same decisions, checking for premature purge of any single artefact type ahead of the others. Methodology follows standard internal-audit evidentiary-sufficiency and record-reconstruction testing practice, extended to the AI-specific artefact set (model/prompt version, agent trace) with no AI-specific benchmark for acceptable reconstruction completeness. Conducted against retained records only; no production system access required beyond retrieving historical records. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established record-reconstruction and evidentiary-sufficiency testing methodology adapted from internal audit practice; no AI-specific benchmark defines the precise artefact set or completeness threshold required, though the EU AI Act Art. 12 traceability requirement provides an external reference point for in-scope systems, so professional judgement determines adequacy for the remainder).

## 12. Pass Indicators
- 100% of sampled decisions are fully reconstructable from retained records alone, across all artefact types (input, output, version, agent trace, human action).
- No premature purge identified: retention periods are aligned and consistently applied across all artefact types for the same decision.
- Model/prompt version metadata is captured and linked at generation time, not reconstructed retrospectively from indirect evidence.
- Agentic traces include abandoned branches and intermediate tool calls, not only the final output path.
- At least one real historical complaint/audit/regulatory request evidences a record set judged complete by the requesting party.

## 13. Fail Indicators
- A material proportion of sampled decisions cannot be fully reconstructed; commonly, model/prompt version metadata or agentic intermediate traces are the missing artefact.
- Retention periods differ across artefact types for the same decision, such that one component (e.g. conversation memory) has already been purged while another (e.g. final output) remains.
- Reconstruction requires inference or assumption (e.g. "the model version was probably X based on deployment date") rather than direct evidence.
- A real historical complaint or regulatory request found the record set incomplete, and no remediation of the underlying gap has since occurred.
- Abandoned agentic branches and failed tool calls are systematically absent from retained traces.

## 14. Reporting Language
**Pass:** "Reconstruction testing on [n] sampled historical decisions across static, generative and agentic system types achieved full reconstruction from retained records alone in [n]/[n] cases, with no retention misalignment identified across artefact types. Conclusions rest on ★3 methodology — established record-reconstruction testing practice, referenced against EU AI Act Art. 12 traceability requirements for in-scope systems — and should be read as professional assessment."
**Fail:** "Testing found that [n] of [sample size] sampled decisions could not be fully reconstructed from retained records, most commonly due to missing model/prompt version metadata or absent agentic intermediate traces. This does not meet the reconstructability standard required for audit, complaint-handling or regulatory response, exposes the firm to an adverse evidential finding in the event of a complaint or FOS referral, and constitutes a direct compliance gap under EU AI Act Art. 12/19 for in-scope systems. Remediation should close the identified artefact gaps and re-test before reliance is placed on record-keeping for these systems."
**Partial:** "Reconstruction is complete for outputs and human decisions but agentic intermediate traces (abandoned branches, failed tool calls) are not retained for [x]% of the sample. The assurance objective is not yet met for full trajectory reconstruction; remediation should extend trace capture within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a record-keeping gap compounds the consequence of whatever underlying
              decision issue it prevents investigation of; standalone severity from
              the gap itself is a compliance and evidential-burden issue)
  Likelihood: 2 (plausible where retention architecture was designed per system
              without a cross-artefact reconciliation check; reduces materially with
              periodic reconstruction testing)
  Detectability: 3 (invisible until an actual complaint, audit or regulatory request
              tests the record set in practice; a "logs exist" assertion does not
              surface cross-linkage or completeness gaps)
  Recoverability: 2 (a documentation/architecture remediation fixes the control
              going forward, but decisions made during the gap period cannot be
              retrospectively reconstructed if the underlying artefacts were never
              captured)
  Novelty: 3 (a governance SME familiar with structured decision-system logging may
              not anticipate that a GenAI/agentic "decision" comprises four
              cross-linked artefact types rather than one row in a decision table)

Interpretation: acceptable residual risk with periodic reconstruction testing and
retention-period alignment across artefact types; the principal concern is that this
control is typically discovered to have failed only when it is actually needed —
during a live complaint or regulatory request — at which point the gap cannot be
retrospectively cured for past decisions.

If controls are absent or degraded:
  Severity: 3 (adverse evidential finding in litigation/FOS referral; direct EU AI
              Act Art. 12/19 compliance exposure for in-scope systems; root cause
              of underlying incidents becomes permanently unknowable)
  Likelihood: 3 (foreseeable given the well-documented tendency for version metadata
              and agentic intermediate traces to be under-logged relative to final
              outputs)
  Detectability: 4 (silent until tested by an actual request; no proactive signal
              indicates the gap exists)
  Recoverability: 3 (the control itself is fixable, but specific past decisions
              affected by the gap cannot be retrospectively reconstructed — this
              portion of the harm is genuinely irreversible)
  Novelty: 3
Residual risk: High if reconstruction is untested; the irreversibility of the
past-decision component elevates this beyond a routine documentation finding.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Adverse evidential finding in complaint/FOS/litigation contexts, direct EU AI Act Art. 12/19 exposure, and permanent loss of root-cause capability for affected decisions. |
| **Likelihood** | 2 | Plausible where retention architecture lacks cross-artefact reconciliation; reduces materially with periodic reconstruction testing. |
| **Detectability** | 4 | Silent until an actual complaint, audit or regulatory request tests the record set in practice; no proactive signal otherwise indicates the gap. |
| **Recoverability** | 3 | The control is fixable going forward, but specific past decisions affected by a genuine artefact gap cannot be retrospectively reconstructed. |
| **Novelty** | 3 | A governance SME versed in structured decision-system logging may not anticipate the four-artefact-type, cross-linked nature of a GenAI/agentic decision record. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 12 (record-keeping) and Art. 19 (log retention)] requires automatic logging capable of ensuring a level of traceability of the AI system's functioning throughout its lifecycle, for high-risk systems, with logs retained per Art. 19 for a period appropriate to the system's purpose. [FCA/PRA record-keeping expectations under SYSC and DISP] require firms to retain records sufficient to reconstruct decisions for audit, complaint and regulatory purposes across all regulated activities, applicable regardless of EU AI Act in-scope status. [PRA, SS1/23, May 2023] governance and monitoring principles require evidence sufficient to support ongoing oversight, which presupposes reconstructable records. Section pinpoints [UNVERIFIED — cited modules/articles confirmed extant (PRA SS1/23, SS1/21, PS21/3, ISO/IEC 42001:2023, EU AI Act Arts. 9/11/12/19); no AI-specific sub-clause pinpoint published by the regulator beyond module/clause level cited] (verified 29 Jul 2026).

## 18. Research Basis
> [Chan, A., et al., 2024, "Visibility into AI Agents," Proc. FAccT 2024 (arXiv:2401.13138)] documents the specific challenge of capturing complete, reviewable agentic action traces including intermediate and abandoned steps, directly relevant to this IRQ's agentic-trace component. No FS-specific empirical literature quantifies record-reconstruction failure rates for deployed GenAI/agentic decision systems; this control area otherwise draws on internal-audit evidentiary-sufficiency practice rather than a dedicated research literature.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-AGT-011 (C.7: complete, tamper-evident agentic action traces — the primary
    upstream input this IRQ's record set depends on for agentic systems)
  - IRQ-DAT-010 (A.4: memory/conversation store retention — must align its schedule
    to this IRQ's decision-record retention requirement, not a separate shorter one)
  - IRQ-HUM-006 (D.4: named decision-level accountability — supplies the attributable
    human-action component of the record set)
  - IRQ-HUM-008 (D.4: contestability — a functioning contest route depends on this
    IRQ's records being reconstructable to support a genuine re-decision)
  - IRQ-GOV-009 (I.4: documentation adequacy — a related but distinct artefact set;
    this IRQ concerns decision-event records, GOV-009 concerns system description)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L 12.7.2024. Art. 12 (Record-Keeping) and Art. 19 (Automatically Generated Logs).
[2] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[3] Chan, A., Salganik, R., Markelius, A., et al., 2024. "Visibility into AI Agents."
    Proc. ACM FAccT 2024. arXiv:2401.13138.
[4] FCA. "DISP — Dispute Resolution: Complaints." FCA Handbook (complaint time-limit
    rules governing retention alignment).
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): SMEs used to structured decision-system logging (one row per
  decision) do not anticipate that a GenAI/agentic decision comprises four cross-linked
  artefact types (input, output, version, agent trace, human action) any one of which can
  be the silent gap.
✓ Test 2 (Plausible Harm): Grounded in EU AI Act Art. 12/19's binding logging/retention
  obligation and FCA/PRA record-keeping expectations; failure here is only discovered when
  an actual complaint or regulatory request tests the record set, by which point past
  decisions cannot be retrospectively reconstructed.
✓ Test 3 (Testable): Testable via sampled historical-decision reconstruction attempts scored
  for completeness, and retention-alignment checks across artefact types. ★3 methodology.
✓ Test 4 (Decision-Relevant): Gates whether the firm can substantively respond to a complaint,
  audit or regulatory enquiry about any specific AI-influenced decision.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.0 (2026-10): Field 9 — the cross-reference to IRQ-DAT-010, written without its leading zero, corrected. ★3 unchanged.
```

---
---

