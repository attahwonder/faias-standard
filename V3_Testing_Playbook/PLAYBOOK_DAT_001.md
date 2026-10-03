# TP-DAT-001 — Lineage Reconstruction

**Procedure ID:** TP-DAT-001
**IRQ:** IRQ-DAT-001 — Untraceable Training and Grounding Data Lineage
**Assurance objective:** AO-DAT-001 — the firm shall be able to reconstruct, for any training, fine-tuning or grounding dataset in current use, its lawful origin, licence status, copyright position and complete transformation history, on demand and within a defined timeframe.
**★ Confidence:** ★3 (carried from canvas — credible standards-based method per ISO/IEC 5338:2023 lifecycle documentation expectations; no agreed pass/fail benchmark for lineage reconstruction success rate in FS)
**Method classification:** Adapted Industry Practice (ISO/IEC 5338:2023 lifecycle documentation expectations adapted to a sample-based reconstruction audit)

## Preconditions

- **Environment:** Read-only access to a mirror or export of the firm's data lineage/registry system. No production write access. This procedure is documentary and does not execute models.
- **Access needed:** Registry read access; data-catalogue search; model-approval document repository; vendor contract repository (for vendor-supplied fine-tuned models).
- **Artefacts requested in advance (2 weeks):** dataset inventory for all models in current use or in-development; registry schema documentation; licence/copyright clearance workflow description; the most recent independent validation report for at least one approved model; vendor contracts covering any externally fine-tuned model.
- **Personnel:** reviewer (lead); data-governance owner (available for access, *not* for supplying lineage facts verbally — see step 4); MRM/independent validation contact for one interview.

## Test design

- **Sampling approach:** stratified random sample across five source strata — internal, licensed/commercial feed, web-scraped, vendor-supplied, synthetic. Target n=20 datasets minimum (canvas evidence item specifies a 20-dataset trace), allocated proportionally to the estate with a floor of 3 per stratum where the stratum exists (reviewer-set design minimum, disclosed at scoping). Where a stratum has fewer than 3 datasets, take all.
- **Case categories:** within each stratum, deliberately include (a) the oldest dataset still feeding a live model, (b) the most recently ingested, and (c) one that has undergone at least one documented transformation or merge. These three categories are where lineage most commonly breaks.
- **Controls:** a "known-good" dataset nominated by the firm is included unlabelled in the sample as a positive control — if the reviewer cannot reconstruct even the firm's exemplar, the failure is in the reconstruction protocol, not the registry.
- **Benign-payload principles:** not applicable — no payloads, no model execution. The only safety rule is that no dataset content is extracted; the reviewer works with metadata only.

## Steps

1. Obtain the dataset inventory and confirm its completeness against the model inventory (every model in scope should map to at least one dataset). **Record:** inventory date, count of models, count of datasets, any model with no mapped dataset.
2. Construct the stratified sampling frame and draw the sample using a documented random method (record seed or draw method). **Record:** sampling frame, stratum counts, drawn sample IDs, positive-control ID (held separately, not disclosed to the firm).
3. Define the reconstruction scoring rubric before looking at any record. Four elements per dataset: **origin** (identifiable original source), **licence terms** (specific terms, not "licensed"), **copyright position** (a determination, not a blank), **transformation history** (every step from ingestion to current use). Score each element 2 (fully evidenced in the registry), 1 (partially evidenced or requires inference), 0 (absent). **Record:** the rubric, signed and dated before execution.
4. For each sampled dataset, attempt reconstruction **using only the registry and formal documentation**. Do not ask staff for facts. Where a registry field points to an external document, follow the pointer once; if the pointer is dead, score the element 0. **Record:** per-element scores, the evidence reference relied upon, and elapsed time-to-reconstruct in minutes.
5. Where an element scores 0 or 1, record the specific failure mode: field absent, field present but empty, field populated with an assertion ("licensed"), pointer to a document that does not exist, or knowledge held only informally.
6. Compare time-to-reconstruct against the firm's documented SLA for lineage response, if one exists. If none exists, record *no SLA defined* — this is itself a finding against AO-DAT-001's "within a defined timeframe" clause.
7. Interview the independent validation contact on one specific approved model: establish whether lineage evidence was **inspected** or **asserted** at validation. Ask for the specific artefact inspected. **Record:** the artefact named, and whether the reviewer can locate it.
8. For any vendor-supplied fine-tuned model in the sample, inspect the contract for an inspection right or equivalent attestation obligation. **Record:** clause reference or its absence.
9. Reconcile: compute the reconstruction success rate (datasets scoring 2 on all four elements / total sampled), per stratum and overall. Verify the positive control reconstructed successfully.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Full reconstruction success rate | ≥95% (canvas pass indicator) | Canvas-defined; not an external benchmark — the canvas states no published FS benchmark exists |
| Time-to-reconstruct per dataset | Against the firm's own documented SLA | Firm-defined; **reviewer judgement — no established threshold** if no SLA exists |
| Datasets in active use with no licence/copyright determination | Zero (canvas pass indicator) | Canvas-defined, traced to EU AI Act Art. 10 and PRA SS1/23 |
| Per-stratum reconstruction rate | **Reviewer judgement — no established threshold**; report the profile, do not average away a failing stratum | Canvas fail indicators are stratum-sensitive (vendor-supplied specifically called out) |

Also capture: count of L1-only evidence encounters (assertions offered in place of records); count of dead pointers; whether independent validation named an inspectable artefact.

## Interpretation

- **Pass** — ≥95% full reconstruction from the registry alone within the defined SLA; no active dataset lacking a licence/copyright determination; validation demonstrably inspected lineage; vendor/open-source intake shows pre-use provenance checks.
- **Fail** — reconstruction depends on staff memory or ad hoc correspondence; registry incomplete or absent; production-pipeline datasets with no licence determination; validation sign-off citing "provenance confirmed" with no underlying trail (L1 only); vendor fine-tuned models with no inspection mechanism.
- **Partial** — the canvas anticipates the common shape: internal data well-evidenced, vendor-supplied corpora absent. Report as partial with the affected percentage of the model estate stated, and note that the objective is unmet until vendor inspection rights or evidenced attestation exist. A stratum-level failure inside an overall ≥95% rate is a partial, not a pass.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Scoring rubric (pre-dated), sampling frame and draw record | L3 (demonstration of method) |
| Per-dataset reconstruction worksheets with evidence references and timings | L3 |
| Registry extracts / screenshots supporting each score | L2–L3 |
| Reviewer's independent reconstruction report with success rates by stratum | **L4** (independent evidence — this is an independent assessment, not the firm's own record) |
| Vendor contract clause extracts | L2 |
| Interview note with the validation contact | L2 (assertion-based unless the named artefact is produced, in which case L3) |

## Common pitfalls & limitations

- **Accepting verbal reconstruction.** The single most common protocol failure. If a data engineer explains the lineage, the test has measured the engineer, not the registry. Enforce the documentation-only rule.
- **Scoring "licensed" as a licence determination.** It is an assertion (L1). The rubric must require specific terms.
- **Canvas limitation carried forward:** no FS-specific empirical study of lineage reconstruction success rates exists (canvas Research Basis flags this as an evidence gap, not an omission). The ≥95% figure is a canvas-set expectation, not an industry benchmark — say so in reporting.
- **Sample size.** n=20 supports a qualitative finding, not a statistically precise estate-wide rate. Do not report a confidence interval.
- **Blended/web-scale sources** may be genuinely unreconstructable by design rather than by neglect; distinguish the two in reporting, because the remediation differs.

## Time/effort estimate

**3 reviewer-days** (0.5 preparation and sampling; 1.5 reconstruction; 0.5 interviews and contract review; 0.5 analysis and reporting).

---
---

