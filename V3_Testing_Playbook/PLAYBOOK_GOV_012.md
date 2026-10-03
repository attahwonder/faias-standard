# TP-GOV-012 — Envelope-Drift Reconciliation (Flagship)

## 1. Procedure Identity
**Procedure ID:** TP-GOV-012
**IRQ:** IRQ-GOV-012 — Effective Operating Envelope Has Drifted from the Approved Envelope Without Re-Assurance
**Assurance objective:** AO-GOV-012 — The system's effective, in-practice operating envelope — intended use, user population, prompt content, connected tools/integrations, and surrounding business process — shall be periodically and structurally reconciled against its approved operating envelope, with any material divergence triggering mandatory re-approval or re-assurance before the drifted use continues, regardless of whether the underlying model itself has changed.
**★ Confidence (carried from canvas, unchanged):** ★2 — the underlying reconciliation technique (as-approved vs as-operating comparison) is established, credible audit practice, but the specific six-vector envelope-drift taxonomy this test is built around is FAIAS/ASSURANCE_ARCHITECTURE-native rather than an externally published, benchmarked methodology; no cross-institution consensus exists on what constitutes a complete drift-vector checklist or an acceptable drift-detection sampling frame, so test design and the materiality threshold for "undocumented drift" rest heavily on reviewer professional judgement.
**Method classification:** Adapted Industry Practice (configuration/process-audit reconciliation, IT change-management drift detection) applied through an **Emerging Practice** drift-vector taxonomy that is FAIAS-native. This must be stated in every report using this procedure.

## 2. Preconditions
**Environment:** Documentary and log reconciliation, plus a staging replica for the boundary-exercise component. No live production access is required for the reconciliation limb beyond retrieving historical logs; the boundary exercise runs in staging only.
**Access required:** The Operating Envelope Declaration recorded at approval; production task/query logs (metadata level wherever sufficient); current user-access records; current system prompt/instruction text and its version history; the current tool/integration map; the business process owner for interview; a staging replica for the boundary exercise.
**Artefacts required:** Operating Envelope Declaration (designed-for / not-designed-for scope) per sampled system; approval papers; task/query logs for the review period; access records; system prompt version history; tool/integration inventory at approval and now; re-approval and re-assurance records; the process description recorded at approval.
**Personnel required:** System owner; platform administrator; the business process owner (for the human-review-substance vector, which no log can answer); reviewer.
**Data handling:** Task/query logs are the most sensitive artefact in this procedure. Request classification-level metadata (task type, timestamp, user role) rather than prompt content wherever the classification can be performed without it. Where content inspection is needed to classify task type, sample narrowly, review in situ under supervision, do not export, and record the minimisation approach.

## 3. Test Design
This is the flagship GOV procedure: the effective-use versus approved-envelope comparison. It exists because a system can drift into a materially different risk profile without a single change to the model — and every other assurance control in the firm is triggered by model change.

Six drift vectors, per ASSURANCE_ARCHITECTURE.md Layer 4. Each is assessed independently and classified as **no drift**, **drift within tolerance** (documented and approved), or **undocumented drift**:

- **V1 Business-process drift** — the surrounding process has changed; e.g. escalation review has become nominal.
- **V2 User-behaviour drift** — actual task types submitted diverge from the declared scope; the canonical case is a "triage" tool functioning as a "decision" tool.
- **V3 Tool/integration drift** — connections exist that were not present or contemplated at approval.
- **V4 Prompt drift** — the system prompt has changed materially since approval.
- **V5 Customer-segment drift** — the population served has expanded beyond the declared segment.
- **V6 Silent capability drift** — the underlying model or platform has gained capability without a firm-initiated change (cross-reference IRQ-TPR-004 and IRQ-MOD-002).

Each vector has its own evidence source: V1 interview, V2 logs, V3 integration map, V4 prompt diff, V5 access and segment records, V6 provider release notes and version pinning records.

A staging boundary exercise then tests whether the declared boundaries are technically resisted or exist only in policy — the same logic as TP-GOV-003 Limb C, applied to the envelope rather than to approval conditions.

Finally, every instance of undocumented drift is cross-referenced against whether a re-approval or re-assurance record exists, dated at or before the drift's introduction.

Sample: risk-based, weighted to Tier 2–3, minimum six systems, with preference for systems approved 12+ months ago (drift needs time to accumulate) — a reviewer-set design minimum, disclosed at scoping.

## 4. Steps
1. Draw and record the sample, preferring systems approved 12+ months ago. **Record:** basis, size, approval-age spread.
2. For each system, obtain the Operating Envelope Declaration as recorded at approval. **Record:** the declared task-type scope; the declared user population; the declared customer segment; the tool/integration set at approval; the system prompt version in force at approval; the surrounding process as described. Where no Envelope Declaration exists, record that — and note that TP-GOV-009 question 4 predicts this.
3. **V2 — user-behaviour drift.** Obtain task/query logs for the review period and classify a sample against the declared task-type scope. **Record:** sample size and classification method; the proportion of activity outside declared scope; specifically whether a declared "triage/support" tool is being used to make decisions.
4. **V5 — customer-segment drift.** Obtain current user-access records and, where applicable, the customer segments actually served. **Record:** any access group or customer segment present now and absent from the declaration.
5. **V4 — prompt drift.** Obtain the current system prompt/instruction text and diff it against the version in force at approval. **Record:** the diff; whether changes are material to behaviour; whether each change is version-controlled with an accompanying re-test record.
6. **V3 — tool/integration drift.** Obtain the current tool/integration map and compare to the approval-time set. **Record:** every connection present now and absent at approval; for each, whether it enables an irreversible downstream action; whether any re-assessment occurred.
7. **V6 — silent capability drift.** Review provider release notes and the firm's version pinning records for the period. **Record:** any capability the model or platform gained without a firm-initiated change; whether the firm detected it. Cross-reference IRQ-TPR-004.
8. **V1 — business-process drift.** Interview the business process owner structurally: is the human-review step performed as described at approval; has review time per case changed; has the reviewer population changed; is escalation still substantive. **Record:** verbatim; specifically any account of review having become nominal.
9. Classify each vector per system as no drift / drift within tolerance / undocumented drift. **Record:** the classification matrix — six vectors by however many systems.
10. **Boundary exercise.** In the staging replica, attempt to exercise the system slightly outside one declared boundary: submit an out-of-declared-scope task type, and attempt access as a non-approved user role. Use benign test content only. **Record:** blocked / flagged / silently permitted; verbatim system response.
11. For every undocumented drift found, search for a corresponding re-approval or re-assurance record. **Record:** whether one exists and its date relative to the drift's introduction. A record dated after the drift began is not re-assurance; it is retrospective documentation.
12. Assess aggregate effect. **Record:** the reviewer's judgement on whether the accumulated drift across vectors has materially changed the system's risk profile relative to the tier assigned at approval — cross-reference TP-GOV-004.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Task/query activity outside declared scope | Reviewer judgement on materiality — no established threshold. The canvas treats a material proportion with no re-approval as the clearest and most common fail indicator | Explicitly bespoke; no consensus exists on an acceptable drift-detection sampling frame |
| User-access records vs declared population | No access group in production absent from the declaration | Categorical per canvas pass indicator |
| System prompt diff | Matches approval version, or every change version-controlled with a re-test record | Categorical per canvas pass indicator |
| Tool/integration additions | None absent from approval without explicit approved addition and re-assessment | Categorical per canvas pass indicator |
| Boundary exercise outcome | Technically resisted, not merely discouraged by policy | Categorical per canvas pass indicator |
| Re-approval record dated at or before drift introduction | Required wherever drift is found | Categorical per canvas pass indicator |
| Completeness of the six-vector taxonomy | Reviewer judgement — no established threshold. The taxonomy is FAIAS/ASSURANCE_ARCHITECTURE-native and not externally benchmarked; this must be disclosed | Explicitly bespoke; the primary reason for ★2 |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: actual task/query distribution falls entirely within the declared task-type scope with any exceptions documented and separately re-approved; user-access records match the declared population; current system-prompt text matches the approved version or every change is version-controlled with a re-test record; no tool/integration exists in production that was not present or explicitly approved as an addition with re-assessment; the staging boundary attempt is technically resisted; and any drift found has a corresponding re-approval or re-assurance record dated at or before its introduction.

**Fail** where: task/query logs show a material proportion of activity outside declared scope with no re-approval (the "triage tool functioning as a decision tool" pattern); system-prompt text differs materially from the approved version with no version-control trail and no re-test evidence; a downstream integration or tool connection exists that was not contemplated at approval with no re-assessment of consequent risk (particularly irreversible downstream action); the staging boundary attempt succeeds with no technical resistance, confirming envelope boundaries exist only in policy; or the business-process-owner interview reveals the human-review process has materially changed — escalation review become nominal — with no reassessment of the system's effective autonomy.

**Partial** where some vectors show no drift and others show undocumented drift. Given six vectors, Partial is the expected outcome for most real systems; report per vector rather than as a single verdict, and state which vectors were tested and which could not be (e.g. V6 where provider release notes are unavailable).

## 7. Evidence Outputs
- Operating Envelope Declaration and approval papers as obtained — **L2**
- Tool/integration map at approval and now; prompt version history — **L2**
- Task/query log classification results (V2) — **L3**
- Prompt diff (V4); integration comparison (V3); access record comparison (V5) — **L3**
- Business process owner interview transcript (V1) — **L3**
- Staging boundary-exercise log with verbatim responses — **L3**
- Reviewer's independent six-vector drift classification matrix and aggregate risk-profile assessment — **L4**
- Re-approval/re-assurance records and any real historical drift detection by the firm's own mechanism — **L5**

## 8. Common Pitfalls & Limitations
- **No Operating Envelope Declaration to reconcile against.** The most common blocker. Where none exists, the procedure cannot produce a drift finding — it produces a more fundamental finding (no envelope was ever declared) and must be reported that way rather than as a Pass. Sequence TP-GOV-009 first; its question 4 predicts this.
- **Classifying task types from prompt content at scale.** Expensive and data-sensitive. Where an automated classifier is used, validate it on a manually-labelled subset and report its accuracy; an unvalidated classifier makes the headline drift proportion unreliable.
- **V1 has no log.** Business-process drift is invisible in every technical artefact and only surfaces in the interview. It is also the vector with the largest effect on effective autonomy. Do not skip it because it is unquantifiable.
- **V6 depends on the provider.** Where release notes are absent or the model is not version-pinned, V6 cannot be assessed; record the limitation rather than recording no drift.
- **Retrospective re-approval.** A re-approval paper dated after the drift began documents the drift; it does not re-assure it. Step 11's date comparison is the discriminating check.
- **Aggregate versus vector-level findings.** Six individually tolerable drifts can compound into a materially different system. Step 12 exists for this and is where the procedure earns its flagship status.
- **The taxonomy is FAIAS-native.** This is the single most important disclosure in the GOV domain. The six-vector set is not an externally published or cross-institution-agreed checklist; another reviewer might define a seventh vector or merge two. Every report using TP-GOV-012 must carry that statement alongside the ★2 rating, honestly, rather than presenting the taxonomy as settled methodology.

## 9. Time / Effort Estimate
**6 reviewer-days**: 0.5 day sampling and envelope extraction, 1.5 days task/query log classification (V2, the heaviest limb), 1 day prompt/integration/access comparison (V3, V4, V5), 0.5 day silent-capability review (V6), 0.5 day business process interviews (V1), 0.5 day staging boundary exercises, 1.5 days classification matrix, aggregate assessment and working papers. Add 1 day per system beyond six; add 2 days where an automated task-type classifier must be built and validated.

---
---

