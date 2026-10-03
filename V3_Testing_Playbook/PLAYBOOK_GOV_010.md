# TP-GOV-010 — Decision Reconstruction Walkthrough

## 1. Procedure Identity
**Procedure ID:** TP-GOV-010
**IRQ:** IRQ-GOV-010 — Retained Records Insufficient to Reconstruct a Consequential AI-Influenced Decision
**Assurance objective:** AO-GOV-010 — Retained records for every consequential AI-influenced decision shall span inputs, outputs, model/prompt version, agent traces (where applicable) and the human decision-maker's action, cross-linked and retained for a period sufficient to support audit, complaint and regulatory reconstruction, and this reconstructability shall be demonstrated by test, not assumed from the existence of individual logs.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established record-reconstruction and evidentiary-sufficiency testing methodology adapted from internal audit practice; no AI-specific benchmark defines the precise artefact set or completeness threshold required, though the EU AI Act Art. 12 traceability requirement provides an external reference point for in-scope systems, so professional judgement determines adequacy for the remainder.
**Method classification:** Adapted Industry Practice — internal-audit evidentiary-sufficiency and record-reconstruction testing, extended to the AI-specific artefact set.

## 2. Preconditions
**Environment:** Retained record retrieval. No live production system access required beyond retrieving historical records through normal retrieval channels — and the retrieval channel is itself part of what is being tested.
**Access required:** The ability to request historical records exactly as a complaint handler, auditor or regulator would; read access to retention schedules per artefact type; read access to the decision population from which the sample is drawn.
**Artefacts required:** Retention schedules by artefact type; the decision population for the review period; historical complaint, audit or regulatory requests and the record sets produced in response; log architecture documentation showing where each artefact type is stored.
**Personnel required:** Records/retrieval function; the log owner for each artefact type (frequently different teams own prompt logs, model version metadata and human-action records — the fragmentation is the risk); reviewer.
**Data handling:** Reconstructed decisions contain full customer records including prompt content. Review in situ under the firm's supervision wherever possible; where extraction is necessary, minimise to the fields needed for the completeness assessment, restrict to the review team, and delete at engagement close. Record the data-minimisation approach in the working papers.

## 3. Test Design
A sample of historical consequential decisions is selected and full reconstruction is attempted using **only the retained record set**, requested through normal retrieval channels. Five artefacts must be recovered per decision:

1. The exact input.
2. The exact output.
3. The model and prompt version in effect at the time.
4. The complete agent trajectory including abandoned branches (where applicable).
5. The specific human reviewer's action and rationale.

Each attempt is scored complete / partially complete (naming the missing artefact type) / not reconstructable.

The sample must span system types — static predictive, generative assistant, agentic — because the missing artefact differs by type. Static predictive decisions usually fail on model version; generative on prompt version; agentic on abandoned branches and intermediate tool calls.

A second limb tests **retention alignment**: whether retention periods differ across artefact types for the same decision, such that one component has been purged while another remains. This is the silent failure that turns a complete-looking record set into an incomplete one at month 13.

Sample: minimum 12 decisions, risk-based, spanning the three system types and spanning the age range of the retention period — including at least three decisions close to the retention boundary, where purge misalignment appears (reviewer-set design minimum, disclosed at scoping).

## 4. Steps
1. Obtain the retention schedules by artefact type. **Record:** the retention period for each of the five artefact types, per system; any misalignment visible on paper before testing.
2. Draw and record the sample. **Record:** basis; system type spread; age spread including near-retention-boundary cases.
3. For each sampled decision, submit a retrieval request through normal channels — the same route a complaint handler would use. **Record:** the request, the channel, and the elapsed time to receive the record set.
4. Attempt reconstruction using only what was returned. **Record:** per decision, which of the five artefacts were recovered; the score (complete / partial / not reconstructable); and for partials, the specific missing artefact type.
5. For any artefact not returned, establish whether it exists but was not returned (a retrieval failure) or does not exist (a retention failure). **Record:** the distinction — it drives entirely different remediation.
6. Assess whether reconstruction required inference. **Record:** any case where the reviewer had to infer (e.g. "the model version was probably X based on deployment date") rather than read direct evidence. Inference is not reconstruction.
7. **Agentic limb.** For agentic decisions, check specifically whether abandoned branches and failed tool calls are present in the retained trace. **Record:** present / absent; the canvas names systematic absence of abandoned branches as a fail indicator.
8. **Retention alignment limb.** For the near-boundary decisions, check whether any artefact type has been purged ahead of the others. **Record:** any premature purge found and which artefact.
9. Check version metadata capture. **Record:** whether model/prompt version is captured and linked at generation time, or reconstructed retrospectively from indirect evidence such as deployment dates.
10. Review historical complaint, audit or regulatory requests. **Record:** at least one instance where the requesting party judged the record set complete — or any instance where it was judged incomplete and whether the underlying gap was remediated.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Full reconstruction rate | 100% of sampled decisions across all five artefact types | Categorical per canvas pass indicator |
| Retention alignment across artefact types | Aligned and consistently applied for the same decision; no premature purge | Categorical per canvas pass indicator |
| Version metadata capture | Captured and linked at generation time, not reconstructed retrospectively | Categorical per canvas pass indicator |
| Agentic trace completeness | Abandoned branches and intermediate tool calls present | Categorical per canvas pass indicator |
| Reconstruction requiring inference | Zero — inference is a fail indicator | Categorical per canvas |
| Adequacy of the five-artefact set itself | Reviewer judgement — no AI-specific benchmark defines the required artefact set; EU AI Act Art. 12 provides an external reference for in-scope systems only | Explicitly bespoke for out-of-scope systems |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: 100% of sampled decisions are fully reconstructable from retained records alone across all artefact types; no premature purge is identified and retention periods are aligned; model/prompt version metadata is captured and linked at generation time; agentic traces include abandoned branches and intermediate tool calls; and at least one real historical complaint, audit or regulatory request evidences a record set judged complete by the requesting party.

**Fail** where: a material proportion of sampled decisions cannot be fully reconstructed (commonly model/prompt version metadata or agentic intermediate traces missing); retention periods differ across artefact types such that one component is purged while another remains; reconstruction requires inference rather than direct evidence; a real historical request found the record set incomplete with no remediation since; or abandoned agentic branches and failed tool calls are systematically absent.

**Partial** where static predictive and generative decisions reconstruct fully but agentic ones do not, or where all artefacts exist but retrieval through normal channels failed and required specialist intervention — a real-world reconstructability failure even though the data exists.

## 7. Evidence Outputs
- Retention schedules by artefact type — **L2**
- Retrieval requests as submitted and record sets as returned — **L3**
- Per-decision reconstruction scoring with named missing artefacts — **L3**
- Retention alignment analysis at the near-boundary sample — **L3**
- Reviewer's independent evidentiary-sufficiency assessment — **L4**
- Historical complaint/audit/regulatory request outcomes on record completeness — **L5**

## 8. Common Pitfalls & Limitations
- **Requesting records through a privileged channel.** If the reviewer asks the log owner directly, the test measures the log's contents, not the firm's reconstructability. Use normal retrieval channels.
- **Accepting inference as reconstruction.** Step 6 exists because "probably version X" will not survive a regulatory challenge.
- **Sampling only recent decisions.** The retention-alignment failure only appears near the boundary. Age spread is mandatory.
- **Omitting abandoned branches.** Firms retain the successful path; the canvas names the abandoned branches as the systematic gap.
- **Data-handling exposure.** This procedure touches the most sensitive data of any in the GOV set. Minimise, review in situ, and document the approach.

## 9. Time / Effort Estimate
**5 reviewer-days**: 0.5 day retention schedule review and sampling, 1 day retrieval requests and waiting (elapsed time may exceed effort), 2 days reconstruction attempts across 12 decisions, 0.5 day retention alignment analysis, 1 day working papers.

---
---

