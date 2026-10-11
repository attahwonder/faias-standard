# CANVAS: IRQ-GOV-005

## 1. IRQ ID & Title
**IRQ-GOV-005: Policy Suite Silent on GenAI/Agentic-Specific Risks, Covering Only Legacy Model Risk**

Register question: "Do firm policies address GenAI/agentic specifics — acceptable use, data entry restrictions, output reliance, agent permissions — or only legacy model risk?"

## 2. Business Activities Affected
- **Every business unit using GenAI or agentic tools day-to-day:** without a current acceptable-use policy, staff have no authoritative guidance on what is and is not permitted (e.g., entering client-confidential data into a public LLM interface, relying on unverified generated output for a customer decision).
- **Data handling across the firm:** legacy data policies were written for structured data and traditional systems; they do not anticipate free-text prompts as a data egress channel or generated outputs as a new data-creation event.
- **Agentic deployments specifically:** legacy policy frameworks have no concept of "agent permissions" as a governed object, leaving delegation of authority to an autonomous system unaddressed by any existing policy.

## 3. AI Behaviour(s)
- Accepts free-text and file-based input from users, which may include client-confidential or personal data entered without users appreciating it constitutes a data-handling event under existing policy.
- Generates outputs that users may rely upon directly, at varying levels of verification, in the absence of policy guidance on required reliance behaviour.
- Where agentic, is granted permissions/credentials to act — a governed object with no legacy policy analogue.

## 4. Failure Mode
> The firm's policy suite (acceptable use, data handling, model risk, third-party risk) was written for legacy deterministic/statistical models and does not address GenAI/agentic-specific behaviours — free-text data entry as a data-handling event, generated-output reliance, and agent permission delegation — leaving staff without authoritative guidance and leaving these risk areas ungoverned by any policy at all.

## 5. Potential Consequences
- **Customer:** Staff relying on unverified generated output for customer decisions, in the absence of any policy requiring verification, produces decisions with no documented basis for having been checked.
- **Institution:** Client-confidential or personal data entered into GenAI interfaces without policy-driven restriction creates data protection exposure the firm cannot demonstrate it managed; agent permission delegation with no policy framework creates ungoverned operational risk.
- **Regulator/market:** A policy suite silent on GenAI/agentic risk is a direct, easily-identified supervisory finding — evidence the firm has not adapted its control framework to the technology actually in use, undermining confidence in the broader governance programme (echoing the PRA/FCA's DP5/22 question of whether existing frameworks in fact extend to AI).

## 6. Failure Chain
```
Firm adopts GenAI/agentic tools while policy suite remains legacy (written for static
predictive models and structured data)
  ↓ (IRQ-GOV-005 — THIS IRQ: no acceptable-use, data-entry, output-reliance or agent-
  permission policy exists to fill the gap)
Staff have no authoritative guidance; behaviour defaults to individual judgement
  ↓ (IRQ-DAT-002: personal/confidential data enters GenAI corpora without documented basis)
Client-confidential data entered into a public/uncontrolled GenAI interface, or generated
output relied upon for a customer decision without verification
  ↓ (IRQ-SEC-008: unsanctioned tool use compounds data exposure risk)
Data exposure or unverified-output-driven customer harm occurs
  ↓
Incident investigation finds no policy existed to have governed the behaviour →
firm cannot demonstrate a reasonable control framework was in place → regulatory finding

Control Breakpoints:
  • IRQ-GOV-005: policy suite explicitly extended to GenAI/agentic-specific risks
  • IRQ-DAT-002: lawful basis and minimisation controls for personal data in GenAI corpora
  • IRQ-GOV-003: technical enforcement of acceptable-use policy, not policy text alone
  • IRQ-HUM-002: review/reliance behaviour trained per output-reliance policy
```

## 7. Why a Domain Expert May Miss It
- Policy suites are reviewed for existence and currency against a checklist of traditional headings (data protection, model risk, third-party risk, information security); a reviewer confirming those headings exist can miss that none of them actually addresses GenAI-specific behaviour within their scope.
- Legacy data-handling policy already prohibits "sharing confidential data externally"; SMEs may assume this covers entering data into a GenAI prompt, without recognising a prompt to a hosted model is a distinct data-egress channel the policy drafters never contemplated.
- "Model risk policy" sounds like it should cover GenAI by name, but if it was last substantively revised before GenAI adoption, its definitions, thresholds and examples may all implicitly assume deterministic/statistical models, silently excluding GenAI in practice even where not excluded in principle.
- Agent permissions have no legacy governed-object analogue at all (no traditional model "acts" with delegated authority), so a policy-gap audit built around updating existing categories may simply never generate a category for it.

## 8. Assurance Objective
**AO-GOV-005:** The firm's policy suite shall explicitly address GenAI- and agentic-specific risks — acceptable use, data entry restrictions, output reliance, and agent permissions — with no material gap left to legacy model-risk policy silently covering by extension.

## 9. Expected Controls (Traced)
- **Dedicated GenAI acceptable-use policy covering data entry restrictions, permitted use cases and prohibited practices** — [FCA, "AI Update," Apr 2024, confirming existing SYSC/Consumer Duty framework applies but requiring firm-level policy translation; ISO/IEC 42001:2023, clause 5.2 (policy)] — a current, GenAI-specific policy document, not solely inference from legacy policy headings.
- **Output-reliance policy defining required verification/human-review behaviour before generated content is relied upon in customer or material decisions** — [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), use and compensating-controls principle, extended to generative outputs] — Emerging Practice: SS1/23 was not written for generative model outputs specifically; applying its use-principle logic to output-reliance policy is a firm-level extension, not yet standard.
- **Agent permission and delegation policy defining approval, scoping and revocation of autonomous action authority** — [ISO/IEC 42001:2023, clause 8 (operation)] — Emerging Practice: no established regulatory standard specifically addresses agentic permission-delegation policy; this control area is genuinely nascent, and is documented as such rather than papered over.
- **Data-entry classification extending existing data protection policy to explicitly name GenAI prompts/uploads as a data-handling event** — [UK GDPR Art. 5(1)(f) and Art. 32; linked IRQ-DAT-002] — closes the gap between legacy data policy scope and the new channel.
- **Policy review cadence tied to AI capability/tooling change, not solely annual calendar review** — [ISO/IEC 42001:2023, clause 9 (performance evaluation) and clause 10 (improvement)] — ensures policy currency keeps pace with a fast-moving technology, rather than becoming stale between annual cycles.

## 10. Expected Evidence (Tagged L1–L5)
- Current policy suite documents (acceptable use, data protection, model risk, third-party risk) — **L2**.
- Gap-analysis mapping each GenAI/agentic risk area (acceptable use, data entry, output reliance, agent permissions) against the policy suite, identifying explicit coverage vs silent gaps — **L2/L3**.
- Staff attestation/training records confirming policy has been communicated and acknowledged — **L2**.
- Internal audit or legal/compliance review confirming policy suite substantively addresses GenAI/agentic risk (not merely mentions the term "AI") — **L4**.
- Sample of actual staff usage behaviour (e.g., help-desk queries, escalations, incident reports) tested against policy for whether guidance existed to have prevented the observed behaviour — **L3/L5**.
- Record of policy update following a specific GenAI/agentic capability or tooling change, evidencing the review-cadence control is live — **L5**.

## 11. Independent Test
> Obtain the current policy suite and independently map it against a defined set of GenAI/agentic risk areas (acceptable use of GenAI tools, data entry restrictions for prompts/uploads, output-reliance/verification requirements, agent permission and delegation). For each area, classify coverage as: explicit and current, inferred from legacy policy only, or absent. Interview a sample of business users on their understanding of what is and is not permitted, to test whether policy (where it exists) is actually known and actionable, not merely documented. Cross-check a sample of incident/help-desk records for cases where the absence of clear policy contributed to an issue. Methodology follows standard policy gap-analysis and compliance-testing practice, extended to an AI-specific risk taxonomy with no AI-specific benchmark for "adequate" GenAI policy coverage. Conducted against policy documents, interviews and records only. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established gap-analysis and compliance-testing methodology; no industry-standard checklist defines the complete set of GenAI/agentic policy areas a firm must cover, so the risk-area taxonomy itself rests on professional judgement, informed by FCA/PRA and ISO 42001 sources).

## 12. Pass Indicators
- All four risk areas (acceptable use, data entry, output reliance, agent permissions) are explicitly and currently addressed in named policy documents, not inferred from legacy headings.
- Staff interviews confirm actionable, correct understanding of GenAI-specific policy requirements in ≥90% of the sample.
- No incident/help-desk record in the sample identifies absence of policy as a contributing factor.
- Policy has demonstrably been updated in response to a specific GenAI/agentic capability change within the last review cycle.
- Agent permission/delegation policy exists with defined approval, scoping and revocation processes, even where labelled Emerging Practice.

## 13. Fail Indicators
- One or more risk areas (particularly agent permissions) have no policy coverage at all — silent gap.
- Legacy model-risk or data-protection policy is asserted to "cover" GenAI by extension, with no substantive revision demonstrating the drafters actually considered GenAI-specific behaviour.
- Staff interviews reveal inconsistent or incorrect understanding of what is permitted, indicating policy (even if it technically exists) is not functioning as guidance.
- Incident/help-desk records show cases where policy silence contributed to a data-handling or reliance issue.
- Policy suite has not been substantively updated since before GenAI/agentic tools were adopted.

## 14. Reporting Language
**Pass:** "Gap-analysis testing confirms the policy suite explicitly and currently addresses all four GenAI/agentic risk areas — acceptable use, data entry, output reliance and agent permissions. Staff interviews corroborate actionable understanding, and no incident record in the sample identifies policy silence as a contributing factor. Conclusions rest on ★3 methodology — established gap-analysis practice with no industry-standard GenAI policy checklist — and should be read as professional assessment."
**Fail:** "Gap-analysis testing found that [n] of 4 GenAI/agentic risk areas — most materially, [named area] — have no explicit policy coverage; legacy model-risk and data-protection policy is being relied upon by extension without substantive revision for GenAI-specific behaviour. Staff interviews found inconsistent understanding of what is permitted. Data entry and output-reliance behaviour in this gap is currently ungoverned by any authoritative guidance; policy development is required before further reliance can be assured."
**Partial:** "Acceptable-use and data-entry policy is current and explicit, but output-reliance and agent-permission policy remain silent gaps, affecting [describe scope]. The assurance objective is not yet met for the ungoverned areas; remediation should close the policy gap within [n] days, prioritising agent-permission policy given active agentic deployment."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a policy gap is a governance-foundation issue; realised severity depends on what
              staff do in the absence of guidance)
  Likelihood: 2 (plausible where policy has not been substantively revised since GenAI adoption;
              less likely once a current, mapped policy suite exists)
  Detectability: 2 (found via periodic gap-analysis or internal audit; not visible from routine
              operation until an incident occurs)
  Recoverability: 1 (reversible by drafting and communicating the missing policy, though staff
              behaviour during the gap period cannot be retrospectively governed)
  Novelty: 2 (a governance-literate domain expert with AI context would likely think to check
              for GenAI-specific policy coverage; the gap is more a matter of policy maintenance
              lagging technology adoption than a purely novel AI-specific blind spot)

Interpretation: acceptable residual risk once a current, explicitly-mapped policy suite exists;
the material concern is the foundational nature of the gap — every other governance control in
this file (approval, tiering, escalation, accountability) assumes policy exists to define what
"acceptable" and "escalate" mean, and a silent policy gap undermines that assumption everywhere.

If controls are absent or degraded:
  Severity: 3 (ungoverned data entry and output reliance can produce data protection breaches
              and unverified customer decisions across the full population of staff using the tool)
  Likelihood: 3 (foreseeable and common — policy maintenance lagging fast-moving technology
              adoption is a routine organisational failure mode, not a rare event)
  Detectability: 3 (requires a dedicated gap-analysis to surface systematically; individual
              instances surface only via incident)
  Recoverability: 2 (policy can be drafted quickly once the gap is identified, but cannot
              retrospectively govern behaviour that already occurred during the gap period)
  Novelty: 2
Residual risk: High while the policy gap persists; foundational because it undermines the
premise of every downstream governance control.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | A policy gap does not itself cause harm; realised severity is inherited from the ungoverned staff behaviour it permits (data exposure, unverified reliance). |
| **Likelihood** | 3 | Probable wherever policy has not been substantively revised since GenAI/agentic adoption — a common and foreseeable maintenance lag rather than a rare failure. |
| **Detectability** | 3 | Requires a dedicated gap-analysis to surface systematically; the gap is otherwise invisible until an incident traces back to absent guidance. |
| **Recoverability** | 2 | New policy can be drafted quickly, but behaviour occurring during the gap period (data already entered, decisions already relied upon) cannot be retrospectively governed. |
| **Novelty** | 2 | Less AI-specific than other GOV IRQs — this is fundamentally a policy-maintenance discipline familiar to any governance SME, applied to a new technology; the AI-specific element is knowing which four risk areas to check for. |

## 17. Regulatory Basis
> [FCA, "AI Update," Apr 2024] confirms the FCA expects existing SYSC and Consumer Duty obligations to be translated into firm-level policy for AI use, without prescribing the policy content itself, leaving policy-suite adequacy a firm responsibility this IRQ tests. [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023)] establishes model use principles that extend to AI/ML by the Bank of England and PRA letter of 22 April 2024, implying output-reliance policy should exist for generative model use. [ISO/IEC 42001:2023, clause 5.2] requires a documented AI policy as a certifiable management-system requirement. [UK GDPR Art. 5(1)(f) and Art. 32] underlies the data-entry policy gap specifically, where GenAI prompts constitute a data processing/egress channel.

## 18. Research Basis
> No peer-reviewed academic literature specifically evaluates financial-services GenAI/agentic policy-suite adequacy; this control area is compliance/governance practice rather than a research literature, consistent with this domain's evidentiary profile. [FCA "AI Update" (2024)] and [ISO/IEC 42001:2023] are treated as the most credible available reference points for the expected policy scope.
>
> **[FAIAS Incident Register, row 67, "Victoria's Department of Families, Fairness and Housing", 2024]** — the Information Commissioner records that at the time of the incident "there were no specific departmental rules in place about when and how these tools should or should not be used" (para 92), the department's guidance following on 25 October 2023 (para 98): staff had no departmental rule on the use of such tools until then. The department is a public-sector child protection body, not a financial-services firm.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-002 (A.1: personal data in training/fine-tuning without lawful basis — the
    data-entry policy gap's downstream consequence)
  - IRQ-GOV-003 (I.2: technical enforcement of conditions of use — policy alone is insufficient
    without this companion control)
  - IRQ-TPR-002 (F.1: contractual rights — policy suite should align with what contracts permit)
  - IRQ-HUM-002 (D.1: automation bias/approval theatre — output-reliance policy shapes review behaviour)
  - IRQ-SEC-008 (E.2: unsanctioned tool data egress — technical backstop where acceptable-use
    policy is silent or unenforced)
```

## 20. References
```
[1] FCA, 2024. "AI Update." April 2024.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management system."
    Clauses 5.2, 8, 9, 10.
[4] UK, 2018 (as amended). "UK General Data Protection Regulation." Art. 5(1)(f), Art. 32.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.2 (Governance domain, Approval, Tiering & Policy)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): A policy-suite review against a checklist of traditional headings
  can confirm those headings exist without noticing none of them substantively addresses
  GenAI-specific behaviour; agent permissions have no legacy governed-object analogue at all.
✓ Test 2 (Plausible Harm): Grounded in the FCA's own confirmation that translation of existing
  obligations into firm-level AI policy is expected, and in UK GDPR's data-egress framing of
  prompt-based data entry; a silent policy gap leaves real staff behaviour ungoverned.
✓ Test 3 (Testable): Testable via structured gap-analysis, staff interview and incident-record
  cross-check against policy documents. ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome determines whether staff have authoritative guidance for
  GenAI/agentic use, and is foundational to every other governance control that assumes policy
  defines acceptable behaviour and escalation triggers.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.3 (2026-10-09): Field 17 — the SS1/23 sentence names the Bank of England and PRA letter of 22 April 2024, in place of the PRA's April 2024 mapping. Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 67, the Information Commissioner's investigation of a Victorian child protection department, a public-sector setting). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
```

---
---

