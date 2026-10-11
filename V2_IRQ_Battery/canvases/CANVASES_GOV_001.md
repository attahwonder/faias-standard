# CANVAS: IRQ-GOV-001

## 1. IRQ ID & Title
**IRQ-GOV-001: Absent or Nominal Accountable Ownership of AI Systems Across Their Lifecycle**

Register question: "Is there a named accountable owner, with appropriate seniority and SMCR mapping, for each AI system across its full lifecycle including third-party components?"

## 2. Business Activities Affected
- **All AI-supported customer-facing and back-office processes:** every deployment (lending, claims, AML, customer service, pricing) depends on a person who can authorise, restrict or suspend the system; without one, no other governance control has a decision-maker behind it.
- **Third-party and embedded AI:** where the AI capability is delivered inside a procured platform (CRM, HR tool, surveillance system), ownership is easily assumed to sit with the vendor or with whoever bought the platform, rather than with a named accountable individual inside the regulated firm.
- **Model change and incident response:** ownership is the trigger point for re-approval, escalation and suspension decisions; an absent or nominal owner stalls every downstream governance action.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns the human/organisational structure around the system, not the system's own outputs.
- The AI system operates continuously in production regardless of whether a specific individual is actively accountable for it at any given time.

## 4. Failure Mode
> An AI system operates in production with no individual holding genuine, senior, SMCR-mapped accountability for its safety and performance — ownership is either entirely absent, or nominal (a name on a spreadsheet with no real authority, engagement or capacity to act).

## 5. Potential Consequences
- **Customer:** Harms from the system (biased outcomes, hallucinated decisions, outages) go unactioned because no individual is positioned or empowered to intervene.
- **Institution:** Governance failures cannot be attributed to a Senior Manager under SM&CR, weakening the firm's ability to demonstrate individual accountability to the PRA/FCA; incident response is slow and diffuse.
- **Regulator/market:** Supervisory findings of diffuse or absent accountability for AI systems, consistent with the PRA/FCA's stated concern (DP5/22) that existing frameworks (SMCR) must be shown to actually apply to AI, not merely assumed to.

## 6. Failure Chain
```
AI system procured or built without a named senior owner assigned at go-live
  ↓ (IRQ-GOV-002: inventory may not even record the system to attach an owner to)
System enters production; "ownership" recorded as a team mailbox or committee
  ↓ (IRQ-GOV-001 — THIS IRQ: no individual has genuine, senior accountability)
Model degrades, drifts, or an incident occurs
  ↓ (IRQ-GOV-008: no accountable body actually receives and acts on the signal)
No individual has authority, context or incentive to suspend or restrict the system
  ↓ (IRQ-HUM-005: suspension authority undefined or unrehearsed)
Harm continues uninterrupted; SM&CR cannot attribute responsibility
  ↓
Customer detriment persists → complaint/incident escalates externally →
supervisory finding of diffuse accountability → enforcement/reputational damage

Control Breakpoints:
  • IRQ-GOV-002: complete inventory creates the object ownership attaches to
  • IRQ-GOV-001: named, senior, SMCR-mapped owner assigned at approval
  • IRQ-HUM-005: named individual holds tested suspension authority
  • IRQ-GOV-008: governance body receives and acts on monitoring signals
```

## 7. Why a Domain Expert May Miss It
- Traditional model governance (e.g., a credit scorecard) has a long-established owner (Head of Credit Risk); SMEs assume the same default applies automatically to a newly procured GenAI tool, without checking it was actually assigned.
- "Ownership" is frequently satisfied on paper (a name in a RAID log) without the accompanying seniority, capacity or SM&CR mapping that gives the assignment teeth — a documentation-literate reviewer can be satisfied by the existence of a name alone.
- Embedded/third-party AI (a chatbot bundled inside a CRM) is easy to treat as "the vendor's problem," so no internal owner is ever assigned, especially where procurement, not risk, led the buying decision.
- Multi-agent and shared-service deployments (one system used by several business units) create ownership ambiguity that a single-business-unit mental model does not anticipate.

## 8. Assurance Objective
**AO-GOV-001:** Every AI system in scope shall have a single named, sufficiently senior, SM&CR-mapped accountable owner across its full lifecycle — including where AI capability is delivered by, or embedded within, a third party.

## 9. Expected Controls (Traced)
- **Named senior accountable owner assigned at approval, recorded in governance records** — [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), Principle 1 (Model Identification) and governance expectations] — no model, including AI/ML models, proceeds to use without documented ownership.
- **SM&CR mapping of AI ownership to a Senior Manager Function or equivalent accountable individual** — [Bank of England and PRA, "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI," 22 April 2024, mapping DSIT principles onto SS1/23 and SMCR; FCA "AI Update," Apr 2024, confirming SMCR as the accountability anchor for AI] — ownership is not merely operational but attributable under the existing accountability regime.
- **Ownership requirement extended to embedded/third-party AI** — [ISO/IEC 42001:2023, clause 5 (Leadership) and clause 8 (Operation), AI management system leadership/roles requirements] — AI management system roles and responsibilities are assigned regardless of build-vs-buy origin.
- **Governance function (AI Management System / model risk function) that verifies ownership is genuine, not nominal** — [ISO/IEC 42001:2023, clause 9 (Performance evaluation); NIST AI RMF 1.0, Govern function, Jan 2023] — periodic verification that named owners are engaged, resourced and exercising the role.
- **EU AI Act provider/deployer role clarity where in scope** — [Regulation (EU) 2024/1689, Art. 9 (risk management system) and Art. 26 (deployer obligations)] — for in-scope high-risk systems, roles and responsible persons must be identifiable, reinforcing the ownership control.

## 10. Expected Evidence (Tagged L1–L5)
- AI inventory extract showing an "Owner" field populated for the system in question — **L1** (name alone is an assertion of ownership, not evidence it is genuine).
- Governance policy defining ownership criteria (seniority threshold, SM&CR mapping requirement, responsibilities) — **L2**.
- Approval paper/model risk record showing the named owner signed off acceptance of accountability at go-live — **L3**.
- Internal audit or model risk function review confirming the named owner is engaged (attends governance forums, has taken a documented ownership decision in the review period) — **L4**.
- SM&CR Statement of Responsibilities or equivalent mapping document showing the AI system falls within a Senior Manager's documented responsibilities — **L4**.
- Incident or change record showing the named owner made an actual decision (approval, restriction, escalation) in the last 12 months — **L5**.

## 11. Independent Test
> Select a risk-based sample of AI systems from the inventory (weighted to Tier 2–3 under TIERING_MODEL.md). For each, trace: (1) the named owner recorded at approval, (2) whether that individual is mapped to an SM&CR Statement of Responsibilities or equivalent senior accountability record, (3) evidence of at least one substantive ownership decision (approval, restriction, escalation, or sign-off on a change) in the last 12 months, and (4) whether the owner could correctly describe the system's approved operating envelope and known limitations in interview. Cross-check embedded/third-party AI systems specifically for whether an internal owner exists at all. Methodology follows standard internal-audit reconciliation and control-testing practice (walkthrough, sample tracing, interview) as applied to model governance under SS1/23, extended here to an AI-specific ownership object with no AI-specific benchmark. Conducted entirely against governance records and interviews; no production system access required. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established audit-sampling methodology; no AI-specific standard defines "genuine" versus "nominal" ownership, so the genuineness judgement rests on reviewer professional assessment — state this caveat in reporting).

## 12. Pass Indicators
- 100% of sampled systems have a named owner recorded at or before go-live, meeting the firm's documented seniority threshold.
- Named owners are traceable to an SM&CR Statement of Responsibilities or equivalent documented senior accountability for 100% of sampled systems.
- Interviewed owners correctly describe the system's operating envelope, known limitations and escalation route for their system in ≥90% of interviews.
- At least one substantive ownership decision is evidenced in the last 12 months for every sampled system.
- Embedded/third-party AI in the sample has an identified internal owner, not "vendor" recorded as the owner.

## 13. Fail Indicators
- Owner field is populated but the named individual cannot describe the system, is unaware they are the owner, or has never made a decision about it (nominal ownership).
- No SM&CR or equivalent mapping exists linking the named owner to formal senior accountability.
- Systems, particularly embedded/third-party AI, are found with no owner at all, or "the vendor" recorded as owner.
- Ownership is assigned at a level with no authority to restrict or suspend the system (e.g., a junior analyst holding nominal ownership of a Tier 3 system).
- Ownership record is stale — no review or reconfirmation since original go-live despite material system changes.

## 14. Reporting Language
**Pass:** "A sample of [n] AI systems, weighted to higher-tier deployments, evidences named, senior, SM&CR-mapped ownership with demonstrated substantive decision-making in the last 12 months. Embedded and third-party AI carries an identified internal owner, not vendor-only accountability. Conclusions rest on ★3 methodology — established audit-sampling practice applied to an AI-specific object with no AI-specific benchmark — and should be read as professional assessment."
**Fail:** "Testing found that recorded ownership is nominal for [n] of [sample size] systems: named individuals could not describe the system's operating envelope or evidence a substantive decision in the last 12 months, and [x] embedded/third-party AI systems had no internal owner at all. Governance and escalation controls that depend on a genuinely accountable owner cannot be relied upon until ownership is remediated and SM&CR-mapped."
**Partial:** "Ownership is genuine and SM&CR-mapped for directly procured and internally built systems, but embedded AI within third-party platforms lacks an identified internal owner in [x]% of the sample. The assurance objective is not yet met for that subset; remediation should extend ownership assignment to embedded AI within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (weakens escalation/incident response rather than causing direct harm itself; amplifies severity of other IRQ failures)
  Likelihood: 2 (plausible gap for embedded/third-party AI specifically; unlikely for directly built/procured Tier 2-3 systems with mature governance)
  Detectability: 2 (surfaced within a review cycle via inventory audit and interview; not real-time)
  Recoverability: 1 (immediately reversible by assigning and documenting a proper owner; low cost)
  Novelty: 2 (domain expert with AI governance context would flag this; standard enterprise model-governance controls, extended to AI, would normally catch it)

Interpretation: acceptable residual risk on its own; the material concern is that this IRQ is a
force multiplier — its failure degrades the effectiveness of every downstream governance and
escalation control in the file (IRQ-GOV-008, IRQ-HUM-005).

If controls are absent or degraded:
  Severity: 3 (governance and escalation failures cascade unaccountably across multiple systems)
  Likelihood: 3 (foreseeable where AI procurement outpaces governance process, especially embedded AI)
  Detectability: 3 (requires a dedicated inventory/ownership audit to surface; not visible from outside governance)
  Recoverability: 2 (reversible within days once identified, but the accountability gap during the exposure window cannot be retrospectively cured)
  Novelty: 3 (embedded/third-party AI ownership gaps are AI-specific; traditional procurement risk models do not anticipate AI capability arriving inside non-AI-branded software)
Residual risk: High if uncontrolled at scale; low-cost to remediate once identified.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Does not directly harm customers; weakens the accountability and escalation chain that would otherwise contain harm from other failure modes. |
| **Likelihood** | 3 | Probable for embedded/third-party AI specifically, where procurement rather than risk process often leads acquisition; less likely for directly governed Tier 2–3 systems. |
| **Detectability** | 2 | Detected via a targeted inventory/ownership audit within a review cycle; not visible through routine monitoring. |
| **Recoverability** | 1 | Cheaply and immediately reversible by assigning and documenting proper ownership once identified. |
| **Novelty** | 3 | Embedded AI ownership gaps are AI-specific (capability arriving inside non-AI-branded procured software); domain expert governance intuition, built for standalone models, may miss this vector. |

## 17. Regulatory Basis
> [PRA, SS1/23, "Model risk management principles for banks," April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024, Principle 1 — Model Identification, and governance expectations throughout] requires documented ownership and accountability for models, extending to AI/ML per the Bank of England and PRA letter of 22 April 2024. [Bank of England and PRA, "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI," 22 April 2024] explicitly maps AI governance onto existing SMCR accountability structures. [FCA, "AI Update," Apr 2024] confirms Consumer Duty, SYSC and SMCR — not a new AI rulebook — as the accountability anchor. [Regulation (EU) 2024/1689 (EU AI Act), Art. 9 and Art. 26] requires identifiable responsible roles for in-scope high-risk systems where the firm is a provider or deployer.

## 18. Research Basis
> [Bank of England/PRA/FCA, "Artificial Intelligence and Machine Learning," Discussion Paper DP5/22, Oct 2022] frames the core supervisory question of whether SMCR and existing accountability frameworks in fact extend to AI systems in practice, not merely in policy — the empirical gap this IRQ tests. [ISO/IEC 42001:2023, clauses 5 and 8] establishes leadership/role-assignment requirements for AI management systems as accepted management-system practice, the closest available standards analogue (no peer-reviewed empirical literature on AI ownership genuineness specifically was identified; this control area is governance/audit practice rather than a research literature, consistent with this domain's evidentiary profile).
>
> **[FAIAS Incident Register, row 65, "Uber Advanced Technologies Group Tempe crash", 2019]** — the National Transportation Safety Board found that the automated-driving developer "did not have a safety division or a dedicated safety manager responsible for risk assessment and mitigation"; the head of operations, "lacking experience in safety management", held the role as an additional responsibility. Accountability existed in name without time, expertise or capacity. The developer is not a financial-services firm; the point that carries across is an owner named without the capacity to act.
>
> **[FAIAS Incident Register, row 66, "ANAO audit of AI governance at the Australian Taxation Office", 2025]** — carried as an audit finding of control gaps, not a harm event: the Australian National Audit Office found that "Key roles and responsibilities with respect to AI are not always clearly defined, including enterprise-wide responsibilities and accountabilities" at the Australian Taxation Office, which appointed its Chief Data Officer as accountable official in November 2024. The match to this question is partial: the audit records roles left undefined, not an owner named without capacity.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-002 (I.1: inventory completeness — the ownership object must first exist to be owned)
  - IRQ-HUM-005 (D.3: suspension authority — depends on a genuinely accountable, empowered owner)
  - IRQ-HUM-006 (D.4: decision-level accountability — individual decisions vs system-level ownership, distinct but linked)
  - IRQ-GOV-008 (I.3: monitoring signals must reach an accountable body — the owner is that body's anchor)
  - IRQ-TPR-001 (F.1: provider due diligence — embedded/third-party AI ownership gap shares this root cause)
```

## 20. References
```
[1] Bank of England/PRA/FCA, 2022. "Artificial Intelligence and Machine Learning." Discussion
    Paper DP5/22. Published October 2022.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] Bank of England/PRA, 2024. "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI." 22 April 2024.
[4] FCA, 2024. "AI Update." April 2024.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L, 12 July 2024. Art. 9, Art. 26.
[6] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management system."
    Clauses 5, 8, 9.
[7] NIST, 2023. "AI Risk Management Framework (AI RMF 1.0)." Govern function. January 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.1 (Governance domain, Inventory & Ownership)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Governance SMEs assume a populated "owner" field is sufficient
  evidence of accountability; the genuineness/seniority/SM&CR-mapping gap, especially for
  embedded third-party AI, is easy to overlook without a dedicated interview-based audit.
✓ Test 2 (Plausible Harm): Grounded in the PRA/FCA's own stated supervisory concern (DP5/22)
  that SMCR accountability must be shown to extend to AI in practice; absent ownership
  degrades every downstream escalation and incident-response control.
✓ Test 3 (Testable): Fully testable via inventory sampling, document tracing and structured
  interview against governance records; no production system access required. ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome gates whether the firm's SMCR accountability claims for
  AI are supportable, and determines remediation priority for embedded/third-party AI ownership.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.3 (2026-10-09): Field 17 — the SS1/23 sentence names the Bank of England and PRA letter of 22 April 2024, in place of the PRA's April 2024 mapping. Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 17 and 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citations added in the reserved form (row 65, Uber Advanced Technologies Group, for an owner named without capacity; row 66, the Australian National Audit Office audit of the Australian Taxation Office, carried as an audit finding of control gaps and not a harm event, and matched in part). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Field 9 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Field 9 Expected Controls — the Bank of England and PRA letter of 22 April 2024 cited by its title, The Bank and the PRA's response to DSIT/HMT: update on our approach to AI, with the Bank of England and the PRA as issuers (it was cited as a PRA/FCA document under another title). Field 17 Regulatory Basis — the same. Field 20 References — the same. No change to controls, test, ★ rating or risk profile.
```

---
---

