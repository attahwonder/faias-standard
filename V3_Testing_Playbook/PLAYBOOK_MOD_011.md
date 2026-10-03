# TP-MOD-011 — Benchmark Contamination Probing and Held-Out Corroboration

**Procedure ID:** TP-MOD-011
**IRQ:** IRQ-MOD-011 — Contaminated Evaluation Evidence Underpinning Model Approval
**Assurance objective:** AO-MOD-011 — approval shall rely on held-out, contamination-checked, firm-relevant evaluation evidence; vendor-reported or public-benchmark scores shall not be accepted as sufficient evidence of capability or safety without an independent contamination check and, where feasible, corroboration on genuinely held-out firm-relevant data.
**★ Confidence:** ★3 (carried from canvas — credible, peer-reviewed contamination-detection methods with growing consensus (Sainz et al., 2023; Golchin & Surdeanu, 2023), with comparator evidence from Zhang et al., 2024 (GSM1k) showing material score drops on decontaminated recreations; no single canonical contamination test applies universally across benchmark types, so method selection and threshold-setting require professional judgement)
**Method classification:** Adapted Industry Practice — guided-prompting contamination probing per the cited methods, plus independent held-out corroboration.

## Preconditions

- **Environment:** staging / non-production API access to the model under approval. Internal historical data used for the held-out set must be verified as **not publicly scraped**, and must be anonymised.
- **Access needed:** the model's approval papers and every benchmark cited in them; non-production API access; internal historical case files suitable for constructing a held-out set; model-selection decision records.
- **Artefacts requested in advance (2 weeks):** approval papers with all cited evaluation evidence and its provenance (vendor-reported, public leaderboard, firm-executed); any contamination check performed and its result; the model-selection rationale; the internal case corpus and confirmation of its non-public status.
- **Personnel:** reviewer (lead); domain SME to construct and validate the firm-relevant held-out set; model platform engineer.

## Test design

- **Component 1 — guided-prompting contamination probe:** for each benchmark cited in the approval papers, present the model with a **partial excerpt** of a benchmark item and measure whether it reproduces the exact remainder at a rate exceeding chance. Compare against a **comparably-structured but demonstrably novel item** — the novel comparator is what converts a raw reproduction rate into evidence of memorisation rather than of general competence. n≥50 benchmark items and n≥50 matched novel comparators per benchmark (reviewer-set design minimum, disclosed at scoping).
- **Component 2 — held-out firm-relevant corroboration:** construct or source a small evaluation set from internal historical case files covering the **same claimed capability** as the cited benchmark, verified not to be publicly scraped. n≥50 (reviewer-set design minimum, disclosed at scoping). Compare performance against the cited benchmark score.
- **Matching discipline:** the novel comparator items must match the benchmark items in structure, length and difficulty as closely as the reviewer can achieve; a poorly-matched comparator is the main way this procedure produces a false contamination signal.
- **Repetition and decoding:** low-temperature or greedy decoding for the reproduction probe, fixed and recorded; reproduction is a memorisation test, and high-temperature sampling obscures it.
- **Benign-payload principles:** not applicable; probes are benchmark excerpts. The safety rule is data handling — internal historical case files must be anonymised and must not be published or transmitted to a third-party endpoint in identifiable form.

## Steps

1. Enumerate every piece of evaluation evidence cited in the approval papers, with its provenance. **Record:** the inventory, classifying each as vendor-reported, public benchmark, or firm-executed.
2. Determine whether any contamination check was performed and recorded. **Record:** the check and result, or its absence — absence alone is a canvas fail indicator.
3. Select benchmark items and construct matched novel comparators. **Record:** item selection, matching rationale, and SME validation of comparability.
4. Fix and record the decoding configuration (low temperature or greedy) and attempt count.
5. Run the guided-prompting probe on benchmark items. **Record:** per-item reproduction outcome, scored on a defined match criterion (exact, near-exact, unrelated).
6. Run the identical probe on the novel comparators. **Record:** per-item outcomes.
7. Compare reproduction rates: benchmark versus novel comparator. **Record:** the differential — this is the contamination signal, not the raw benchmark rate.
8. With the SME, construct the held-out firm-relevant evaluation set from internal historical cases, verifying non-public status. **Record:** construction method and the non-public verification.
9. Run the model on the held-out set and score against ground truth. **Record:** performance.
10. Compare held-out performance against the cited benchmark score for the same claimed capability. **Record:** the gap, and whether any reconciliation or re-approval occurred where a gap was previously known.
11. Review model-selection records: did selection rest on public leaderboard position alone? **Record:** the rationale as documented.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Reproduction-rate differential (benchmark vs matched novel comparator) | At or near chance for held-out comparators (canvas pass indicator); the differential threshold is **reviewer judgement — no canonical contamination test applies universally** | Canvas ★3 caveat |
| Held-out firm-relevant performance versus cited benchmark score | Materially lower performance without reconciliation is a fail indicator | Canvas; comparator evidence from the GSM1k finding cited in the canvas |
| Contamination check recorded in approval documentation | Present, with the result, not merely the raw score (canvas pass indicator) | Canvas |
| At least one independent, firm-relevant held-out evaluation in approval evidence | Present (canvas pass indicator) | Canvas |
| Model selection resting on leaderboard position alone | Fail indicator | Canvas |

## Interpretation

- **Pass** — contamination probes on cited benchmarks show no material evidence of memorisation, with reproduction at or near chance for held-out comparators; approval evidence includes at least one independent, firm-relevant held-out evaluation corroborating the cited benchmark's implied capability level; documentation records the contamination check and its result rather than citing the raw score alone; where a contamination risk was identified, the approval decision was revisited and re-tested.
- **Fail** — approval papers cite a vendor or public benchmark score with no contamination check of any kind; guided-prompting probes show material memorisation on the cited benchmark; independent firm-relevant held-out testing shows materially lower performance than the cited score with no reconciliation or re-approval; model-selection decisions rest on public leaderboard position alone.
- **Partial** — no memorisation is detected but no firm-relevant held-out corroboration exists either, so the approval still rests on an uncorroborated external score; or corroboration exists for one claimed capability and not others. Report which capability claims are corroborated and which are not.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Evaluation-evidence inventory with provenance classification | L3 |
| Existing contamination check record, where one exists | L2–L3 |
| Benchmark item and novel comparator sets with matching rationale and SME validation | L3 |
| Decoding configuration and probe manifest | L3 |
| Per-item reproduction results for both sets | **L4** |
| Reproduction-differential analysis | L4 |
| Held-out firm-relevant set construction record and non-public verification | L3 |
| Held-out performance results and benchmark comparison | L4 |
| Model-selection decision records | L2 |

## Common pitfalls & limitations

- **Poorly matched comparators.** The single largest source of false contamination signals. Match structure, length and difficulty, and have the SME validate.
- **High-temperature probing.** Obscures memorisation. Use greedy or low-temperature decoding.
- **Held-out data that is not actually held out.** Internal case files derived from public sources, or previously published, defeat the corroboration. Verify explicitly (step 8).
- **Canvas limitation carried forward:** no single canonical contamination test applies universally across benchmark types; method selection and threshold-setting require professional judgement. ★3 — credible method, judgement-set thresholds.
- **Absence of reproduction does not prove absence of contamination** — paraphrased or transformed benchmark content in training will not reproduce verbatim yet still inflates scores. State this.
- **Sending internal case content to a third-party endpoint** is a data-governance decision in its own right; obtain approval and use anonymised content.

## Time/effort estimate

**4 reviewer-days** (0.5 evidence inventory; 1 comparator construction and validation; 0.5 probe execution; 1 held-out set construction with SME and execution; 0.5 analysis; 0.5 reporting).

---
---

