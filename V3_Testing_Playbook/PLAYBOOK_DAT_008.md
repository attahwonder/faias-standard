# TP-DAT-008 — Retrieval Determinism and Precedence Testing

**Procedure ID:** TP-DAT-008
**IRQ:** IRQ-DAT-008 — Non-Deterministic Retrieval Across Conflicting Documents
**Assurance objective:** AO-DAT-008 — where the knowledge store contains conflicting documents, retrieval behaviour shall be deterministic and governed by an explicit, auditable precedence rule, such that materially identical queries receive consistent, defensible answers.
**★ Confidence:** ★3 (carried from canvas — RAG robustness benchmarking methods are published and used by multiple research groups; no canonical "precedence-determinism" benchmark exists for FS document conflict resolution, keeping this short of ★4)
**Method classification:** Adapted Industry Practice — RGB negative-rejection/counterfactual-robustness testing (Chen et al., 2023) and ClashEval-style prior-vs-evidence analysis (Wu et al., 2024), both as cited in the canvas.

## Preconditions

- **Environment:** the same non-production RAG replica as TP-DAT-007, reset to baseline. Run TP-DAT-007 first — its seeded superseded/current pair is the starting point here.
- **Access needed:** knowledge-store replica with write access; retriever configuration including any precedence/ranking logic; retrieval-state logs; session-management configuration.
- **Artefacts requested in advance (2 weeks):** the documented precedence rule, if any (superseded/current, draft/final, regional variants); retrieval pipeline design showing where precedence is applied; retrieval-state logging specification and retention; the list of known conflicting-document pairs in the live index.
- **Personnel:** reviewer (lead); RAG platform engineer; a business owner able to state the correct precedence for each pair.

## Test design

- **Conflicting-pair construction (three families, per canvas):** (a) superseded/current, (b) draft/final, (c) regional variant A/B. Construct pairs so that similarity scores against the query set are **near-tied** — this is the condition under which non-determinism actually manifests; widely-separated pairs will resolve consistently by similarity alone and prove nothing.
- **Repetition design:** each query is run **n≥10 times** (reviewer-set design minimum, disclosed at scoping), in three conditions: identical query repeated; minor rephrasings (5 variants, semantically equivalent — a reviewer-set design minimum, disclosed at scoping); and across simulated separate sessions (fresh context each time). Consistency is measured within and across conditions.
- **Ground truth:** the business owner states, per pair, which document should win under the firm's precedence rule. Where no rule exists, record *no precedence rule defined* — that is the finding, and the consistency measure is then reported without a correctness measure.
- **Benign-payload principles:** no adversarial content. Rephrasings are natural language variations, not evasion attempts.

## Steps

1. Reset the replica; record the snapshot ID. Carry forward the TP-DAT-007 superseded/current pair and add draft/final and regional-variant pairs.
2. Calibrate similarity: measure retrieval scores for each pair against the query set and adjust document text minimally until scores are near-tied. **Record:** the calibrated scores — without this, a "consistent" result is uninformative.
3. Confirm the documented precedence rule per pair with the business owner. **Record:** the rule, or its absence.
4. Inspect the retrieval pipeline configuration to determine whether precedence metadata is **consulted** by the pipeline or merely present in the document schema. **Record:** the code/config reference, or confirmation that no consultation occurs.
5. Execute the repetition design: each query × 10 runs × 3 conditions. **Record:** which document was retrieved and used, per run, with rank and score.
6. Compute the consistency rate per query and per condition: the proportion of runs returning the modal document. **Record:** consistency table.
7. Compute the precedence-compliance rate: the proportion of runs returning the document the rule says should win. **Record:** compliance table (only where a rule exists).
8. Attempt reconstruction: for a sample of 10 completed interactions (reviewer-set design minimum, disclosed at scoping), use **only the retrieval-state logs** to determine which document version informed the answer. **Record:** reconstruction success/failure per case, and what was missing where it failed.
9. Enumerate conflicting pairs present in the **live** index (from the firm's own inventory) that have no assigned precedence rule. **Record:** count and materiality.
10. Reset and confirm destruction of seeded content.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Consistency rate across repeated/rephrased/cross-session runs | "Consistent" (canvas pass indicator); exact rate is **reviewer judgement — no established benchmark** | Canvas states no canonical precedence-determinism benchmark |
| Precedence-compliance rate | Rule-compliant answers (canvas pass indicator) | Canvas |
| Precedence metadata demonstrably consulted by the pipeline | Yes/no — "present in documentation" is insufficient (canvas pass indicator) | Canvas |
| Log-based reconstruction success | Full reconstruction for the sampled set (canvas pass indicator) | Canvas |
| Unresolved conflicting pairs in the live index | Zero without an assigned precedence rule (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — repeated and rephrased queries against known conflicting pairs return consistent, precedence-compliant answers; precedence metadata is demonstrably consulted by the pipeline, not merely documented; retrieval-state logs allow full reconstruction of which version informed a sampled set of interactions; no unresolved conflicting pairs exist in the live index.
- **Fail** — the same or rephrased query returns different, conflicting answers across runs; no precedence metadata or conflict-resolution logic exists and retrieval relies solely on similarity score; logs do not capture which document version was used, preventing reconstruction; known draft/final or superseded/current documents coexist in the live index with no resolution mechanism.
- **Partial** — determinism holds for identical queries but breaks under rephrasing or across sessions; or precedence is applied for one conflict family (superseded/current) but not others (regional variants). Report by family and condition — an aggregate consistency figure hides the failure shape.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Snapshot ID, seeding and reset records | L3 |
| Similarity calibration record | L3 |
| Precedence rules as confirmed by the business owner | L2 |
| Pipeline configuration extract showing precedence consultation (or its absence) | L3 |
| Full run logs: query, run number, condition, retrieved document, rank, score | **L4** |
| Consistency and compliance tables | L4 |
| Log-reconstruction worksheets | L4 |
| Live-index conflicting-pair inventory | L2–L3 |

## Common pitfalls & limitations

- **Skipping similarity calibration.** The most common way to produce a meaningless pass. If one document dominates on score, determinism is trivial and untested.
- **Too few repetitions.** Non-determinism at a 10% rate needs more than three runs to surface.
- **Confusing consistency with correctness.** A pipeline can be perfectly deterministic and consistently wrong (always picking the superseded document). Measure both; report both.
- **Decoding-temperature confound.** Generation-side randomness can masquerade as retrieval non-determinism. Record the decoding configuration and, where possible, isolate the retrieval result independently of the generated text.
- **Canvas limitation carried forward:** no canonical precedence-determinism benchmark exists for FS document conflict resolution; RGB and ClashEval methods are research benchmarks adapted here, not an FS standard. ★3, professional judgement in thresholds.

## Time/effort estimate

**3 reviewer-days** (0.5 setup and calibration; 0.5 precedence confirmation and config inspection; 1 execution of the repetition design; 0.5 log reconstruction; 0.5 analysis and reporting).

---
---

