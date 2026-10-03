# TP-TPR-006 — Embedding Model / Vector Database Dependency and Exit Review

**IRQ:** IRQ-TPR-006 — Hidden Embedding/Vector Database Lock-In and Index Invalidation Risk.
**Assurance objective:** AO-TPR-006 — the firm shall document and test the dependency between embedding-model version and vector index validity, ensure index re-generation is triggered on embedding-model change, and maintain a viable rebuild and export/exit path for its vector database dependency.
**Confidence:** ★2 (carried unchanged). Method class: Mixed — information-retrieval evaluation metrics are well established (that component alone would rate ★4), but the specific embedding-version-mismatch scenario and vector-database export testing are bespoke, FS-specific applications with no agreed benchmark. **The weaker, novel component governs the blended rating.**

### Preconditions
- Isolated staging environment with the vector database and embedding pipeline reproduced, and the ability to change the query-time embedding model independently of the stored index.
- A **fixed query set** with relevance judgements, or a synthetic corpus with known relevant documents per query — required for precision@k measurement. Where the firm has neither, one must be constructed with an SME, and the construction effort should be scoped before committing to a date.
- Synthetic corpus preferred; anonymised data only where a synthetic corpus is not available.
- The **dependency map** documenting embedding model version, index format and vendor export capability, where one exists.
- Access to the re-indexing trigger implementation, to determine whether it fires on embedding-model change events.
- Vendor-documented export mechanisms for the vector database, and permission to exercise them against the staging instance.
- Production retrieval-quality monitoring data over the last 90 days, where it exists.
- Personnel: lead reviewer; technical reviewer for the retrieval experiment; firm platform engineer; SME for relevance judgements.

### Test design
**Mismatch limb (technical).** The query-time embedding model is intentionally updated while the stored index is left un-regenerated. The fixed query set is run and **precision@k** measured against the pre-change baseline. The measurement itself uses standard IR methodology; what is bespoke is the scenario.

The critical observation is not the size of the degradation but whether the mismatch state is **reachable and undetected**: does any monitoring or alert fire? A system that degrades noisily is manageable; one that degrades silently is the risk this IRQ names.

**Trigger-design limb.** Independently of the experiment, inspect whether re-indexing triggers actually fire on embedding-model change events in the current architecture — in code and configuration, not in the design document. The question is whether an undetected mismatch state is reachable at all.

**Export limb.** Attempt a **full data export** from the vector database using **only documented vendor mechanisms** — not a database-level dump, not vendor professional services. Record success, elapsed time, and completeness (are vectors, metadata, and index configuration all recoverable, or only some?). Partial export is the common result and is the substance of the lock-in finding.

**Monitoring limb.** Establish whether retrieval-quality monitoring exists in production with defined relevance thresholds, and review 90 days of data where available.

**Dependency-map limb.** Establish whether a dependency map exists linking embedding model version to index validity, whether it is current, and whether it is reviewed at least annually or on material architecture change.

### Steps
1. Obtain the dependency map, architecture documentation and vendor export documentation. Record what exists.
2. Establish or construct the fixed query set with relevance judgements; record the construction basis.
3. Run the baseline: current embedding model, current index, fixed query set. Record precision@k and the retrieved sets.
4. **Mismatch experiment:** update the query-time embedding model, leave the index un-regenerated, re-run the query set. Record precision@k and the delta.
5. Record whether any monitoring, alert or error surfaced during the mismatch state — and specifically whether the system reported an error or simply returned worse results silently.
6. **Trigger-design limb:** inspect the re-indexing trigger implementation. Determine whether it fires on embedding-model change events, what event source it listens to, and whether any path exists by which the embedding model can change without triggering re-indexing. Record file/config references.
7. Restore the environment to a consistent state and confirm baseline precision@k is recovered.
8. **Export limb:** attempt full export using only documented vendor mechanisms. Record success/failure, elapsed time, completeness by component (vectors, metadata, index configuration), and whether vendor professional services would be required.
9. **Monitoring limb:** establish whether production retrieval-quality monitoring exists, what thresholds are defined, and review 90 days of data including any re-indexing events and their impact.
10. **Dependency-map limb:** assess currency and review cadence.
11. Report per limb.

### Observations & measures
- **Precision@k baseline and mismatch delta.** Standard IR metric; the measurement is well-founded, the scenario is not benchmarked. **No established threshold for what degradation is acceptable — reviewer judgement**, because the operative question is detectability rather than magnitude.
- **Silent-degradation finding** (binary): the mismatch state produced degraded retrieval with **no** monitoring or alert firing / degradation was detected. Canvas Fail condition: a mismatch state that produces degraded but undetected retrieval with no alert.
- **Trigger reachability** (binary, from code): no undetected mismatch state is reachable in the tested architecture / a path exists by which the embedding model can change without triggering re-indexing. Canvas threshold: re-indexing triggers fire correctly and no undetected mismatch state is reachable.
- **Export outcome** (categorical): full export succeeds via documented mechanisms within a reasonable timeframe / partial export only / not possible without vendor professional services. Canvas Fail condition: export not possible via any documented mechanism, or requires vendor professional services with no defined SLA. "Reasonable timeframe" is not defined by any cited source — **reviewer judgement**, and should be assessed against the firm's own exit and continuity requirements where those exist.
- **Export completeness** by component — vectors / metadata / index configuration.
- **Production monitoring** (binary): retrieval-quality monitoring in place with defined relevance thresholds / absent. Canvas Fail condition: absent, with customer complaint the only signal.
- **Dependency map** (categorical): current and reviewed at least annually or on material architecture change / exists but stale / absent. Canvas Fail condition: absent.

### Interpretation
- **Pass** — the staging test confirms re-indexing triggers fire correctly on embedding-model version change and no undetected mismatch state is reachable in the tested architecture; retrieval-quality monitoring is in place in production with defined relevance thresholds; full data export from the vector database succeeds via documented vendor mechanisms within a reasonable timeframe; the dependency map is current and reviewed at least annually or on material architecture change.
- **Fail** — the staging test demonstrates a mismatch state producing degraded but undetected retrieval with no monitoring or alert firing; **or** no retrieval-quality monitoring exists in production and the only signal of a problem is customer complaint; **or** data export is not possible via any documented mechanism, or requires vendor professional services with no defined SLA; **or** no dependency map exists linking embedding model version to index validity.
- **Partial** — triggers fire correctly and monitoring exists, but export is only partially successful (vectors recoverable, index configuration not), or the dependency map exists but has not been reviewed since a material architecture change. Quantify what is recoverable and what is not.

### Evidence outputs
- E1 Assertion that retrieval is working fine, based on absence of error logs — **L1** (explicitly labelled).
- E2 Dependency map documenting embedding model version, index format and vendor export capability — **L2**.
- E3 Fixed query set and relevance judgement construction record — **L3**.
- E4 Baseline precision@k results — **L3**.
- E5 Mismatch experiment results with delta and the silent-degradation finding — **L3**.
- E6 Re-indexing trigger implementation inspection note with file/config references — **L3**.
- E7 Environment restoration confirmation — **L3**.
- E8 Export attempt record: mechanism used, elapsed time, completeness by component — **L3**.
- E9 Production retrieval-quality monitoring configuration and 90 days of data including re-indexing events — **L5**.
- E10 Dependency map currency and review cadence assessment — **L2/L3**.
- E11 Independent review confirming re-indexing triggers actually fire on embedding-model change events in the current architecture, where held — **L4**.

### Common pitfalls & limitations
- **No relevance judgements.** Precision@k without them is not measurable. Construct them with an SME or do not claim the metric.
- **Measuring degradation magnitude and stopping there.** The finding is detectability. A large silent degradation and a small silent degradation are the same class of problem.
- **Testing the trigger by observation only.** Observing that re-indexing happened once does not establish that no path exists by which it would not. Read the trigger implementation.
- **Export attempted by the platform engineer with database-level access.** The test is whether **documented vendor mechanisms** suffice — that is what would be available in an exit scenario. A `pg_dump`-equivalent is not an exit path if the vendor's managed service does not expose it.
- **Leaving the staging index in a mismatched state.** Step 7 restores it; confirm the baseline is recovered.
- **Anonymised production data where a synthetic corpus was available.** Prefer synthetic; use anonymised only where necessary, and record the choice.
- **Averaging the rating.** IR metrics are mature; this scenario is not. The weaker component governs.

### Time/effort estimate
**3.5 reviewer-days** — 0.5 documentation review; 0.75 query set and relevance judgement construction with SME (more where none exists); 0.5 baseline and mismatch experiment; 0.5 trigger implementation inspection; 0.5 export attempt; 0.25 monitoring data review; 0.5 write-up.

---
---

