# TP-GOV-009 — Documentation Answerability Test

## 1. Procedure Identity
**Procedure ID:** TP-GOV-009
**IRQ:** IRQ-GOV-009 — Documentation Below Review-Grade Standard for Independent Review or Regulatory Response
**Assurance objective:** AO-GOV-009 — Documentation shall exist for every AI system at a standard of specificity and currency sufficient to enable effective independent review by a party without prior system knowledge, and shall be maintained current through the system's change-control process.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established documentation-adequacy and readability-testing methodology; the specific field set and answerability threshold for AI system documentation has no AI-specific benchmark, so the key-question set and pass threshold rest on reviewer professional judgement, informed by the EU AI Act Annex IV structure as an external reference.
**Method classification:** Adapted Industry Practice — documentation-adequacy and readability testing, extended to an AI-specific field set.

## 2. Preconditions
**Environment:** Documentation review. No system access required — indeed, system access would defeat the procedure, since the test is whether documentation *alone* suffices.
**Access required:** Current system/model cards, data statements and intended-use/limitation statements for sampled systems; change-control logs for the same systems; documentation version history.
**Artefacts required:** The documentation set per sampled system; change-control log; version history; the firm's own documentation standard or template, if any; EU AI Act Annex IV structure as the external reference for field-set completeness.
**Personnel required:** A **naive reviewer** — someone with general AI assurance competence but no prior knowledge of the specific systems. This is a hard requirement: using a reviewer who has already worked on the system invalidates the procedure. The lead reviewer administers and scores; the naive reviewer answers.
**Data handling:** Documentation may reference confidential architecture and vendor terms. Handle under engagement confidentiality.

## 3. Test Design
A fixed key-question set is answered by a naive reviewer using only the documentation provided, under a defined time limit. Each question is scored answerable / partially answerable / unanswerable. The time limit matters: documentation that yields an answer after two hours of cross-referencing is not review-grade, because a regulator or an independent reviewer will not have two hours per question.

Key-question set (fixed before fieldwork, informed by the EU AI Act Annex IV structure as an external reference and recorded as reviewer-defined):
1. What is this system's approved intended use?
2. What are its documented known limitations?
3. What evaluation evidence underpins its approval?
4. Has the approved operating envelope been stated explicitly?
5. What data feeds it, and what is that data's provenance?
6. Who is accountable for it?

Time limit: 30 minutes per system across all six questions. Record the limit as a reviewer-set parameter.

A separate currency limb cross-checks documentation version dates against the change-control log, since documentation can be perfectly answerable and describe a system that no longer exists.

Sample: risk-based, weighted to Tier 2–3, minimum six systems, including at least one where the model is third-party-supplied (vendor boilerplate documentation is the characteristic weakness) — a reviewer-set design minimum, disclosed at scoping.

## 4. Steps
1. Draw and record the sample. **Record:** basis, size, weighting, third-party inclusion.
2. Fix and record the key-question set, the scoring rubric and the time limit, before fieldwork. **Record:** all three, and the statement that the field set is reviewer-defined informed by Annex IV.
3. Obtain the complete documentation set per sampled system exactly as it would be provided to an external reviewer. **Record:** what was provided; anything the firm added on request (an addition on request is itself a finding — it means the standing documentation was insufficient).
4. Brief the naive reviewer on the questions and the time limit only. **Record:** confirmation that the naive reviewer has no prior system knowledge.
5. Administer the test per system. **Record:** per-question answers, the score (answerable / partial / unanswerable), and the documentation section relied upon.
6. Compute the answerability rate per system and across the sample. **Record:** rates and counts.
7. Assess documentation specificity. **Record:** for each system, whether intended-use and limitation statements are deployment-specific or generic ("use responsibly"); whether the model card is firm-authored or vendor boilerplate.
8. **Currency limb.** Cross-check documentation version dates against the change-control log. **Record:** any material change (model update, prompt change) with no corresponding documentation update.
9. Check data statement cross-referencing. **Record:** whether data statements cross-reference provenance evidence (cross-reference IRQ-DAT-001) or assert provenance separately and unsupported.
10. Check version history retrievability. **Record:** whether prior documentation states can be retrieved, or only the current version — the latter prevents reconstructing what was known at the time of a past decision.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Key-question answerability | ≥90% of key questions answerable from documentation alone across the sample | Per canvas pass indicator — a FAIAS-set rate; no AI-specific benchmark exists |
| Documentation firm-specific vs vendor boilerplate | Firm-specific for all sampled systems | Categorical per canvas pass indicator |
| Version-date alignment with change-control log | No material change without a corresponding documentation update | Categorical per canvas pass indicator |
| Data statement cross-referencing to provenance evidence | Present | Categorical per canvas pass indicator |
| Version history retrievable | Prior states retrievable, not only current | Categorical per canvas pass indicator |
| Time limit and question-set adequacy | Reviewer judgement — no established threshold; both are reviewer-set parameters informed by Annex IV | Explicitly bespoke |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: ≥90% of key questions are answerable from documentation alone with no reliance on the development team's tacit knowledge; documentation is firm-specific with deployment-specific intended-use and limitation statements; version dates align with the change-control log; data statements cross-reference provenance evidence; and version history is retrievable.

**Fail** where: key questions are unanswerable for a material proportion of the sample, requiring contact with the development team; documentation is substantially vendor boilerplate with no firm-specific content; version dates predate known material changes; intended-use and limitation statements are generic rather than deployment-specific; or no version history exists.

**Partial** where questions 1, 2 and 6 are answerable but 3 and 4 (evaluation evidence and operating envelope) are not — extremely common, and directly weakening TP-GOV-012, which needs a stated envelope to reconcile against.

## 7. Evidence Outputs
- Documentation set as provided — **L2**
- Key-question set, rubric and time limit, recorded pre-fieldwork — **L2**
- Naive-reviewer answer sheets with per-question scores and cited sections — **L3**
- Currency cross-check against change-control log — **L3**
- Reviewer's independent documentation-adequacy assessment — **L4**

## 8. Common Pitfalls & Limitations
- **Using a non-naive reviewer.** The single invalidating error. Confirm and record naivety at step 4.
- **Accepting supplementary material provided on request.** Note it as a finding; the test is what stands without prompting.
- **No time limit.** Without one, almost any documentation eventually yields an answer, and the procedure loses its discriminating power.
- **Answerable but wrong.** The naive reviewer's answer should be checked for accuracy against the system owner afterwards; documentation that confidently states something untrue is worse than documentation that is silent.
- **Feeding TP-GOV-012.** Where question 4 (operating envelope) is unanswerable, TP-GOV-012 has no baseline to reconcile against. Sequence GOV-009 before GOV-012 and flag the dependency.

## 9. Time / Effort Estimate
**3 reviewer-days**: 0.5 day sampling and question-set design, 1 day naive-reviewer administration across the sample (30 minutes per system plus setup), 0.5 day accuracy verification with owners, 0.5 day currency cross-check, 0.5 day working papers. Note this requires two reviewers for part of the work.

---
---

