# TP-DAT-012 — Retrieval, Embedding and Corpus Drift Simulation

**Procedure ID:** TP-DAT-012
**IRQ:** IRQ-DAT-012 — Unmanaged Retrieval, Embedding and Document Drift
**Assurance objective:** AO-DAT-012 — retrieval, embedding and document-corpus drift shall be managed through defined re-indexing and re-validation triggers, such that embedding-model changes or corpus composition shifts do not silently degrade retrieval quality.
**★ Confidence:** ★2 (carried from canvas — RAG evaluation tooling such as RAGAS is published and used by multiple groups, but retrieval/embedding drift specifically as a monitored, benchmarked phenomenon is newer and less standardised than generation-quality evaluation; the mixed-geometry and corpus-drift test designs are largely bespoke)
**Method classification:** Adapted Industry Practice / Emerging — RAGAS-style faithfulness and relevance metrics (Es et al., 2023) and RGB robustness benchmarking (Chen et al., 2023), both as cited in the canvas, applied to a drift scenario for which no benchmark exists.

## Preconditions

- **Environment:** non-production replica of the retrieval pipeline with the ability to re-embed a subset of the corpus with a different embedding-model version, and to add documents in bulk. Reset to baseline before and after.
- **Access needed:** corpus replica; embedding pipeline with at least two model versions available; vector index; retrieval-quality metrics; version-pinning configuration; re-indexing procedure documentation.
- **Artefacts requested in advance (2 weeks):** embedding-model version and pinning configuration; re-indexing trigger policy; retrieval-quality monitoring design (what is measured, independently of generation quality); corpus change history and volume; any canary testing for vendor-side embedding updates; historical re-indexing event records.
- **Personnel:** reviewer (lead); RAG platform engineer; vendor management contact for embedding-provider terms.

## Test design

- **Scenario (a) — mixed-geometry index:** re-embed a defined subset of the corpus (e.g. 20%) with a different embedding-model version, leaving the remainder on the original vectors. This reproduces the realistic failure of a partial or interrupted re-index. Measure retrieval precision and recall on the shared query set against the pre-change baseline.
- **Scenario (b) — corpus composition drift:** add a substantial volume of topically-skewed new documents (e.g. doubling the corpus with content concentrated in one product area) and re-measure retrieval relevance for **existing** query types. The mechanism is competition — new documents crowd out previously well-retrieved ones.
- **Query set:** reuse the TP-DAT-007 representative query set with ground-truth relevant documents annotated, so precision and recall are computable.
- **Baseline:** measure the clean, single-geometry, pre-drift baseline first. Without it, the degradation measures are meaningless.
- **Detection question (the real point):** for each scenario, determine whether the firm's **existing monitoring** would have surfaced the degradation, independently of any generation-fluency signal.
- **Benign-payload principles:** not applicable; added documents are benign synthetic or genuine firm content.

## Steps

1. Reset the replica; record the snapshot ID and corpus baseline (document count, embedding-model version).
2. Annotate ground-truth relevant documents for each query in the shared query set. **Record:** the annotated query set (reusable).
3. Measure the clean baseline: retrieval precision, recall and rank quality per query; plus RAGAS-style faithfulness/relevance on the generated responses. **Record:** the full baseline table.
4. Execute scenario (a): re-embed the defined subset with the alternate embedding-model version. **Record:** which documents, which versions, the resulting index state.
5. Re-measure precision, recall and rank quality on the same query set. **Record:** post-change table and the delta versus baseline, broken down by whether the ground-truth document was in the re-embedded subset.
6. Determine whether the firm's existing retrieval-quality monitoring raised any signal. **Record:** monitoring output, and specifically whether any signal exists that is independent of generation fluency.
7. Reset to baseline. Execute scenario (b): add the topically-skewed document volume. **Record:** volume added, topic concentration.
8. Re-measure retrieval relevance for the **pre-existing** query types. **Record:** delta versus baseline, with attention to rank displacement rather than outright loss.
9. Determine whether any re-validation trigger fired for the corpus change, and at what volume threshold, if any. **Record:** trigger policy and observed behaviour.
10. Review version pinning and vendor-update detection: is the embedding-model version pinned, and would a vendor-side update be detected (canary testing, version assertion)? **Record:** configuration evidence.
11. Review any historical re-indexing event for completeness and timeliness. **Record:** event record.
12. Reset the replica; confirm restoration.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Mixed-geometry index present in production | None — embedding changes should trigger full re-indexing before live use (canvas pass indicator) | Canvas |
| Retrieval precision/recall delta under scenario (a) | Within the firm's documented tolerance; **reviewer judgement — no established threshold** if undocumented | Canvas |
| Retrieval relevance delta under scenario (b) | Within the firm's documented tolerance versus pre-drift baseline (canvas pass indicator) | Canvas |
| Retrieval-quality metric monitored independently of generation fluency | Present (canvas pass indicator) | Canvas |
| Re-validation trigger on corpus change | Fires regardless of scale (canvas fail indicator: "corpus changes occur with no re-validation trigger, regardless of scale") | Canvas |
| Vendor-side embedding update detection | Version pinning or canary testing present (canvas fail indicator) | Canvas |

## Interpretation

- **Pass** — no mixed-geometry index exists in production and embedding-model changes trigger full re-indexing before live retrieval; simulated corpus drift keeps retrieval precision/recall within documented tolerance; retrieval-quality metrics are monitored directly and independently of generation-fluency signals; any historical re-indexing event was complete and timely.
- **Fail** — the simulated embedding-model change produces a mixed-geometry index with measurable retrieval degradation undetected by current monitoring; no retrieval-quality metric independent of generation output, so degraded retrieval is invisible until complaints emerge; corpus changes occur with no re-validation trigger at any scale; vendor-side embedding updates are undetected (no pinning, no canary).
- **Partial** — degradation is detected but only after a long lag; or monitoring exists for scenario (b) but not (a); or pinning exists for the primary embedding model but not for a secondary/reranking model. Report by scenario.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Snapshot IDs, corpus baseline record, reset confirmations | L3 |
| Annotated query set with ground-truth relevance (reusable artefact) | L3 |
| Baseline and post-change precision/recall/rank tables | **L4** |
| Mixed-geometry index configuration record | L3 |
| Monitoring output during each scenario | L3–L4 |
| Re-validation trigger policy and observed behaviour | L2–L3 |
| Version pinning / canary configuration evidence | L3 |
| Historical re-indexing event record | L5 where drawn from production history |

## Common pitfalls & limitations

- **No clean baseline.** The most common way to waste this procedure. Measure step 3 before touching anything.
- **Confounding retrieval and generation.** A fluent answer can mask a degraded retrieval, and a poor answer can come from a good retrieval. Measure retrieval metrics directly (that is precisely the canvas fail indicator).
- **Unrepresentative corpus scale.** Rank displacement effects depend heavily on corpus size; a small replica understates scenario (b). Record scale and state the limitation.
- **Canvas limitation carried forward:** retrieval/embedding drift as a monitored, benchmarked phenomenon is newer and less standardised than generation-quality evaluation; the mixed-geometry and corpus-drift designs are largely bespoke. ★2 — report as professional assessment per METHODOLOGY_STANDARDS §3c.
- **Access to a second embedding-model version** may be unavailable (hosted, single-version providers). Where scenario (a) cannot run, record it as untested and note that vendor-side update detection (step 10) becomes the only available control evidence — a weaker position, and one to state.

## Time/effort estimate

**4 reviewer-days** (0.5 setup and baseline; 0.5 query-set annotation; 1 scenario (a); 1 scenario (b); 0.5 pinning/monitoring review; 0.5 analysis and reporting).

---
---

