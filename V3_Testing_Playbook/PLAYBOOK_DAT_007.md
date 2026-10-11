# TP-DAT-007 — RAG Currency and Curation Testing

**Procedure ID:** TP-DAT-007
**IRQ:** IRQ-DAT-007 — Uncurated RAG Ingestion Allowing Stale Content to Override Current Policy
**Assurance objective:** AO-DAT-007 — all content entering the RAG knowledge store shall pass curation controls (currency verification, deduplication, assigned content owner) before being retrievable, such that stale or superseded content cannot be presented as current.
**★ Confidence:** ★3 (carried from canvas — RAG failure-point taxonomies and faithfulness-evaluation tooling are published and used by multiple independent groups; no canonical "currency-check adequacy" benchmark exists for FS knowledge stores, keeping this short of ★4)
**Method classification:** Adapted Industry Practice — RAGAS-style faithfulness evaluation (Es et al., 2023) and, for RAG failure in general, Barnett et al. (2024), whose seven failure points do not include superseded or stale documents; the seeded-supersession design is the canvas's own. Both sources as cited in the canvas.

## Preconditions

- **Environment:** non-production replica of the RAG knowledge store, retriever and generation pipeline, resettable to a known baseline. No production index, no live customer traffic.
- **Access needed:** knowledge-store replica with write access for seeding; retriever configuration; generation pipeline; document metadata schema; the authoritative source repository for policy/product documents (read-only).
- **Artefacts requested in advance (2 weeks):** ingestion/curation procedure for the knowledge store; metadata schema (owner, review date, currency, version); deduplication mechanism description; reconciliation schedule against the source repository; the current and superseded versions of at least three policy/product documents.
- **Personnel:** reviewer (lead); RAG platform engineer (seeding and reset); a business content owner to confirm which version is genuinely current.

## Test design

- **Scenario construction:** for each of at least three document families (reviewer-set design minimum, disclosed at scoping), seed **both** the superseded version and its current replacement — the state that arises from an incomplete update, which is the realistic failure condition rather than a contrived one. Vary the pairs: (a) a policy with materially changed terms, (b) a product document with a changed rate/limit, (c) a document where the change is subtle (wording, not numbers).
- **Query set:** 30–50 representative customer-facing and colleague-facing queries per document family (reviewer-set design minimum, disclosed at scoping), drawn from real query patterns where available, otherwise constructed with the business owner. This query set is designed for reuse in TP-DAT-008, 009 and 012.
- **Metadata condition:** run each scenario twice — once with the currency/ownership metadata present as the firm's control intends, and once with it absent — to establish whether the metadata would have made a difference had the ingestion control been active.
- **Benign-payload principles:** no adversarial payloads. Seeded documents are genuine (or realistic synthetic) firm documents; no injected instructions (that is IRQ-SEC-003's territory, tested separately).

## Steps

1. Reset the replica to a known baseline and record the snapshot ID.
2. Audit metadata completeness across the replica corpus: proportion of documents with an assigned owner, a review date and a currency indicator. **Record:** completeness by field and by document type.
3. Seed the superseded/current pairs. **Record:** document IDs, versions, seeding timestamps, and which is authoritative per the business owner.
4. Run the query set. For each query, capture: which document(s) the retriever surfaced and at what rank; whether the response reflects current or superseded terms; whether any disambiguation or currency signal appears in the output. **Record:** full prompt, retrieved passages, generated response, and rank order.
5. Score each response against ground truth (the current document's terms) on a three-way scale: **current**, **stale**, **conflated/ambiguous**. Score independently of the retrieval result, then compare — a correct answer from a stale retrieval is still a control failure.
6. Repeat with metadata absent. **Record:** the difference in outcomes, which isolates the metadata control's contribution.
7. Test deduplication: upload a near-duplicate of an existing document (same content, different filename/format) and observe whether it becomes independently retrievable. **Record:** outcome.
8. Reconcile a sample of replica documents against the authoritative source repository. **Record:** divergences found, and whether the firm's own scheduled reconciliation would have caught them.
9. Apply a faithfulness check on a sample of responses (RAGAS-style, per Es et al., 2023): does each assertion in the response entail from the retrieved passage? **Record:** faithfulness scoring sheet.
10. Reset the replica and record destruction of seeded content.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Documents lacking owner / review date / currency metadata | Zero (canvas pass indicator) | Canvas |
| Stale-document retrieval rate | Stale documents excluded or clearly flagged/deprioritised versus current (canvas pass indicator); exact rate threshold is **reviewer judgement — no established benchmark** | Canvas states no canonical currency-check benchmark exists |
| Responses reflecting superseded terms | Any occurrence is a fail indicator | Canvas |
| Deduplication effectiveness | Duplicates caught before independent retrievability (canvas pass indicator) | Canvas |
| Source-repository divergence found by scheduled reconciliation | No undetected divergence (canvas pass indicator) | Canvas |
| Faithfulness score | Report; **reviewer judgement — no established FS threshold** | RAGAS-style evaluation per canvas |

## Interpretation

- **Pass** — no document lacks a currency check, owner and review date; stale documents excluded or clearly deprioritised in both retrieval and generation; deduplication catches superseded uploads; periodic reconciliation finds no undetected divergence.
- **Fail** — documents retrievable with no owner, review date or currency metadata; a stale document retrieved and presented as current with the response reflecting superseded terms; no deduplication mechanism, with divergent versions of the same policy independently retrievable; no scheduled reconciliation, drift discovered only via complaint or incident.
- **Partial** — metadata complete for the primary document set but absent for a secondary source (attachments, historic uploads, a migrated corpus); or stale documents deprioritised but still occasionally surfaced without a currency flag. Report the affected document population.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Baseline snapshot ID, seeding log, reset confirmation | L3 |
| Metadata completeness audit | L3 |
| Full prompt/response/retrieval logs for every query | **L4** (independent staging test execution) |
| Three-way scoring sheet (current/stale/conflated) with scorer notes | L4 |
| With/without-metadata comparison | L4 |
| Deduplication test record | L4 |
| Source-repository reconciliation extract | L3 |
| Faithfulness scoring sheet | L4 |
| Ingestion/curation procedure documentation | L2 |

## Common pitfalls & limitations

- **Testing with only obviously-different document pairs.** The subtle-wording pair is where real currency failures hide; include it.
- **Scoring retrieval instead of outcome.** Both matter and they can diverge — record separately (step 5).
- **Staging corpus unrepresentative of production.** A 500-document replica of a 500,000-document index does not exercise retrieval competition realistically. Record corpus size and state the limitation.
- **Canvas limitation carried forward:** no single canonical "currency-check adequacy" benchmark exists for FS knowledge stores — this is why the canvas holds the rating at ★3 rather than ★4. Thresholds are firm-set and the reviewer's scoring judgement is material.
- **Contamination with SEC-003 testing.** If injection payloads from the security testing remain in the replica, results here are confounded. Reset between procedures.

## Time/effort estimate

**3 reviewer-days** (0.5 setup and metadata audit; 0.5 query-set construction with the business owner; 1 execution across both metadata conditions; 0.5 faithfulness and reconciliation checks; 0.5 analysis and reporting).

---
---

