# TP-GOV-001 — Accountable Ownership Trace

## 1. Procedure Identity
**Procedure ID:** TP-GOV-001
**IRQ:** IRQ-GOV-001 — Absent or Nominal Accountable Ownership of AI Systems Across Their Lifecycle
**Assurance objective:** AO-GOV-001 — Every AI system in scope shall have a single named, sufficiently senior, SM&CR-mapped accountable owner across its full lifecycle, including where AI capability is delivered by or embedded within a third party.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established audit-sampling methodology; no AI-specific standard defines "genuine" versus "nominal" ownership, so the genuineness judgement rests on reviewer professional assessment — state this caveat in reporting.
**Method classification:** Adapted Industry Practice — internal-audit reconciliation and control testing (walkthrough, sample tracing, interview) as applied to model governance under SS1/23, extended to an AI-specific ownership object.

## 2. Preconditions
**Environment:** Governance records and interviews only. No production system access required.
**Access required:** Read access to the AI inventory; approval papers for sampled systems; SM&CR Statements of Responsibilities or equivalent senior accountability records; change-control and escalation records for the last 12 months; contracts or service schedules for embedded/third-party AI.
**Artefacts required:** AI inventory with owner field; approval papers; SM&CR mapping; the firm's documented seniority threshold for AI system ownership; ownership review/reconfirmation records; the last 12 months of governance decisions per sampled system.
**Personnel required:** The named owner of each sampled system (for interview); the governance/model risk function; HR or the SMCR administration function for Statement of Responsibilities verification; reviewer.
**Data handling:** Statements of Responsibilities are personal data about identified individuals; handle under engagement confidentiality, restrict to the review team, and report findings by role and system rather than by name in wider circulation.

## 3. Test Design
The procedure tests four attributes per sampled system, of which only the first is documentary:

- **Recorded** — is an owner named at or before go-live?
- **Mapped** — is that individual traceable to an SM&CR Statement of Responsibilities or equivalent senior accountability record?
- **Empowered** — does ownership sit at a level with authority to restrict or suspend the system?
- **Genuine** — has the owner actually exercised ownership (at least one substantive decision in 12 months) and can they describe the system's approved envelope and known limitations without preparation?

The fourth attribute is what distinguishes this procedure from a register review, and it is the reason the canvas carries a professional-judgement caveat: no standard defines the boundary between genuine and nominal ownership. The reviewer's approach is to make the judgement explicit and evidenced — a named owner who cannot describe their system's limitations in interview is recorded as such, verbatim, and the reader draws the conclusion alongside the reviewer.

Sample: risk-based, weighted to Tier 2–3, minimum eight systems, and **must include at least two embedded or third-party-delivered AI systems** (reviewer-set design minimum, disclosed at scoping), since the canvas identifies these as where ownership most often does not exist at all.

## 4. Steps
1. Draw and record the sample. **Record:** sample basis, size, tier weighting, and the specific inclusion of embedded/third-party systems.
2. For each sampled system, obtain the approval paper and the inventory record. **Record:** the named owner at approval; the named owner now; whether these differ and whether any handover was documented.
3. Obtain the firm's documented seniority threshold for AI system ownership. **Record:** the threshold; where none exists, record that absence.
4. Verify each named owner against SM&CR Statements of Responsibilities or equivalent. **Record:** mapped / not mapped; the specific SMF or responsibility line where mapped.
5. Assess authority level. **Record:** the owner's grade/role; whether that role holds authority to restrict or suspend the system, verified against the firm's own delegation framework rather than assumed.
6. Search the last 12 months of governance and change records for substantive ownership decisions by the named owner for that system. **Record:** each decision found (approval, restriction, escalation, change sign-off) with date; or the absence of any.
7. **Interview each named owner, unprepared.** Ask them to describe: the system's approved intended use; its known limitations; the escalation route if it misbehaves; whether they consider themselves accountable for it. **Record:** verbatim responses; whether the owner was aware they held the role.
8. Score each interview against a rubric fixed before fieldwork (correct / partially correct / cannot describe) on each of the four questions. **Record:** rubric and scores.
9. For embedded/third-party systems specifically, examine whether an *internal* owner exists. **Record:** whether the owner field names an internal individual, a vendor, or is empty.
10. Review ownership record currency. **Record:** date of last ownership review or reconfirmation; whether material system changes have occurred since without ownership review.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Systems with a named owner recorded at or before go-live | 100% of sample, meeting the firm's documented seniority threshold | Categorical per canvas pass indicator |
| Owners traceable to SM&CR or equivalent | 100% of sample | Categorical per canvas pass indicator |
| Owners correctly describing envelope, limitations and escalation route | ≥90% of interviews | Per canvas pass indicator — a FAIAS-set rate, not an external standard |
| Substantive ownership decisions in last 12 months | ≥1 per sampled system | Categorical per canvas pass indicator |
| Embedded/third-party systems with an internal owner | 100%; "the vendor" recorded as owner is a fail indicator | Categorical per canvas |
| Genuine vs nominal ownership | Reviewer judgement — no established threshold. The canvas is explicit that no AI-specific standard defines this; the judgement must be stated as professional assessment with the interview evidence attached | Explicitly bespoke; the reason for the ★3 caveat |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where all six measures above are met across the sample, including embedded/third-party systems having identified internal owners.

**Fail** where: the owner field is populated but the named individual cannot describe the system, is unaware they are the owner, or has never made a decision about it; no SM&CR or equivalent mapping exists; systems (particularly embedded/third-party) are found with no owner or with "the vendor" recorded as owner; ownership sits at a level with no authority to restrict or suspend; or the ownership record is stale with no reconfirmation since go-live despite material change.

**Partial** where directly-procured systems have genuine, mapped, empowered ownership but embedded/third-party AI does not — the characteristic pattern.

## 7. Evidence Outputs
- AI inventory extract, approval papers and SM&CR mapping as obtained — **L2**
- Sample selection record with basis and weighting — **L2**
- Ownership trace matrix across the four attributes — **L3**
- Interview transcripts with rubric scores — **L3**
- Reviewer's independent genuineness assessment with supporting verbatim evidence — **L4**
- Governance decision records evidencing real ownership actions taken — **L5**

## 8. Common Pitfalls & Limitations
- **Interviewing prepared owners.** If the owner is sent the questions in advance, the procedure measures their briefing, not their ownership. Interviews are unannounced in content.
- **Accepting a role title as authority.** Verify against the delegation framework; a "Head of" title does not necessarily carry suspension authority.
- **Sampling only directly-procured systems.** The embedded/third-party inclusion is mandatory, not optional.
- **Judging genuineness implicitly.** The canvas requires the caveat to be stated. Attach the evidence and label the judgement.
- **Handover gaps.** Where the approval owner and current owner differ with no documented handover, the accountability chain is broken even if both individuals are senior and capable.

## 9. Time / Effort Estimate
**3 reviewer-days**: 0.5 day sampling and record extraction, 1 day trace and SM&CR verification, 1 day interviews (typically 30–45 minutes each across eight systems), 0.5 day analysis and working papers.

---
---

