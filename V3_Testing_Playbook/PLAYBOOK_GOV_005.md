# TP-GOV-005 — Policy Suite Gap Analysis

## 1. Procedure Identity
**Procedure ID:** TP-GOV-005
**IRQ:** IRQ-GOV-005 — Policy Suite Silent on GenAI/Agentic-Specific Risks, Covering Only Legacy Model Risk
**Assurance objective:** AO-GOV-005 — The firm's policy suite shall explicitly address GenAI- and agentic-specific risks — acceptable use, data entry restrictions, output reliance, and agent permissions — with no material gap left to legacy model-risk policy silently covering by extension.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established gap-analysis and compliance-testing methodology; no industry-standard checklist defines the complete set of GenAI/agentic policy areas a firm must cover, so the risk-area taxonomy itself rests on professional judgement, informed by FCA/PRA and ISO 42001 sources.
**Method classification:** Adapted Industry Practice — policy gap analysis and compliance testing, extended to an AI-specific risk taxonomy.

## 2. Preconditions
**Environment:** Documents, interviews and records. No system access required.
**Access required:** The complete current policy suite (not only the AI policy — data protection, information security, outsourcing, model risk, conduct and HR policies all carry relevant provisions); policy version history; incident and help-desk records for the review period; access to a sample of business users for interview.
**Artefacts required:** Full policy suite with version dates; policy change history; incident/help-desk records; any GenAI-specific guidance issued outside the formal policy suite (intranet pages, all-staff emails — these frequently carry the real operating rules and their informality is itself a finding); agent permission/delegation process documentation.
**Personnel required:** Policy owner(s); a sample of business users across functions using AI tools; the help-desk or incident function; reviewer.
**Data handling:** Incident and help-desk records may contain personal data about staff and customers. Request redacted extracts categorised by issue type where possible.

## 3. Test Design
The four risk areas named in the assurance objective form the assessment frame, and the canvas is explicit that this taxonomy is the reviewer's professional judgement informed by FCA/PRA and ISO 42001 sources rather than an industry-standard checklist. State that in the report.

For each area, coverage is classified into exactly three states:
- **Explicit and current** — addressed in a named policy document with content demonstrating the drafters considered GenAI/agentic behaviour specifically.
- **Inferred from legacy policy only** — a legacy model-risk or data-protection policy is asserted to cover it by extension, with no substantive GenAI-specific revision.
- **Absent** — no coverage.

The middle state is the one this procedure exists to expose, and it requires reading the policy text, not the policy index. A model risk policy that says "all models must be validated" nominally covers a GenAI assistant while providing no usable guidance on prompt data entry.

Two corroborating limbs: user interviews (does the policy function as guidance, or merely exist?) and incident records (has policy silence contributed to a real issue?).

## 4. Steps
1. Obtain the complete policy suite and record its scope. **Record:** documents in scope; version dates; date of last substantive revision for each.
2. Record the four-area taxonomy and its derivation, labelling it as reviewer-defined and informed by FCA/PRA and ISO 42001 sources. **Record:** the taxonomy statement, to appear in the report.
3. For each of the four areas, read the relevant policy text and classify coverage into the three states. **Record:** classification per area, with the specific policy clause relied upon, or its absence.
4. For each area classified "inferred from legacy policy only", assess whether the legacy text demonstrably contemplates GenAI behaviour. **Record:** the reasoning and the specific text.
5. Assess the agent permission/delegation area specifically. **Record:** whether approval, scoping and revocation processes exist; whether they are labelled Emerging Practice (acceptable per the canvas) or absent (not).
6. Search for GenAI guidance issued outside the formal policy suite. **Record:** any found, and whether its content is more current or more specific than the formal policy — a common and reportable pattern.
7. Interview a sample of business users. Ask what they believe is and is not permitted regarding: entering customer data into a prompt; relying on an AI output without verification; connecting an AI tool to another system. **Record:** verbatim responses; whether answers are consistent across users and correct against policy.
8. Score interviews against a rubric fixed before fieldwork. **Record:** rubric and per-user scores.
9. Review incident and help-desk records for the period. **Record:** any case where absence of clear policy contributed to a data-handling or reliance issue.
10. Review policy change history. **Record:** whether the suite has been substantively updated in response to a specific GenAI/agentic capability change within the last review cycle, or whether it predates GenAI adoption.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Coverage of the four risk areas | All four explicit and current in named policy documents | Categorical per canvas pass indicator |
| User understanding | ≥90% of the interview sample demonstrate actionable, correct understanding | Per canvas pass indicator — a FAIAS-set rate, not an external standard |
| Incident records citing policy absence | Zero in the sample | Categorical per canvas pass indicator |
| Policy updated for a specific GenAI capability change in the last cycle | ≥1 demonstrable update | Categorical per canvas pass indicator |
| Agent permission/delegation policy | Present with approval, scoping and revocation processes; Emerging Practice labelling acceptable | Categorical per canvas pass indicator |
| Completeness of the risk-area taxonomy itself | Reviewer judgement — no established threshold. No industry-standard checklist exists; the taxonomy is reviewer-defined | Explicitly bespoke |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: all four risk areas are explicitly and currently addressed in named policy documents rather than inferred from legacy headings; staff interviews confirm actionable correct understanding in ≥90% of the sample; no incident record identifies policy absence as a contributing factor; policy has demonstrably been updated in response to a specific GenAI/agentic capability change within the last cycle; and agent permission/delegation policy exists with defined approval, scoping and revocation processes.

**Fail** where: one or more risk areas (particularly agent permissions) have no coverage at all; legacy policy is asserted to cover GenAI by extension with no substantive revision; staff interviews reveal inconsistent or incorrect understanding indicating policy is not functioning as guidance; incident records show policy silence contributing to a data-handling or reliance issue; or the suite has not been substantively updated since before GenAI/agentic tools were adopted.

**Partial** where three areas are explicit and agent permissions is absent — the near-universal pattern, since agent delegation policy is the newest of the four.

## 7. Evidence Outputs
- Policy suite extract with version dates — **L2**
- Coverage classification matrix across the four areas with cited clauses — **L3**
- User interview transcripts with rubric scores — **L3**
- Reviewer's independent gap assessment, including the taxonomy derivation statement — **L4**
- Incident/help-desk records evidencing real consequences of policy silence — **L5**

## 8. Common Pitfalls & Limitations
- **Reviewing the policy index rather than the text.** The "inferred from legacy only" state is invisible from an index.
- **Reviewing only the AI policy.** Data entry restrictions typically live in the information security or data protection policy; missing this produces false gap findings.
- **Ignoring informal guidance.** Where the real rules live on an intranet page, the formal suite is failing even if staff behave correctly — and the informality is a finding in its own right.
- **Interviewing policy owners instead of users.** The policy owner knows what the policy says. The user demonstrates whether it functions.
- **Presenting the four-area taxonomy as a standard.** It is not. Step 2's statement must reach the report.

## 9. Time / Effort Estimate
**3 reviewer-days**: 1 day policy text review and classification, 0.5 day informal guidance search, 1 day user interviews, 0.5 day incident record review and working papers.

---
---

