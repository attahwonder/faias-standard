# TP-DAT-003 — Independent Re-Annotation and Label-Quality Measurement

**Procedure ID:** TP-DAT-003
**IRQ:** IRQ-DAT-003 — Insufficient Ground-Truth Label Quality for Fine-Tuning and Validation
**Assurance objective:** AO-DAT-003 — ground-truth labels used for model fine-tuning or validation shall have measured inter-annotator agreement and bounded error rates, disclosed alongside any model performance claim that depends on them.
**★ Confidence:** ★2 (carried from canvas — research-grounded general method exists; sample size, adjudication protocol and segment stratification are bespoke to the firm; no cross-institution consensus benchmark for FS label-quality thresholds)
**Method classification:** Emerging Practice / bespoke, anchored on general annotation-quality practice and ISO/IEC TS 4213:2022 statistical assessment methods. The canvas explicitly records that **no FS-specific peer-reviewed study of inter-annotator agreement practice in credit/insurance labelling was located** — this procedure is structured honestly as bespoke rather than presented as a standard.

## Preconditions

- **Environment:** non-production. Labelled examples are extracted to an isolated review workspace; annotators see case content but not the original labels.
- **Access needed:** the labelled training/validation datasets underpinning a current model approval; the labelling guidelines actually issued to annotators; segment metadata sufficient to stratify (where lawfully available for this purpose); vendor annotation contracts.
- **Artefacts requested in advance (3 weeks — annotator recruitment drives the lead time):** labelling guidelines and any version history; any existing IAA statistics; annotation vendor scorecards; the model documentation containing the accuracy claim under test; annotator training materials.
- **Personnel:** reviewer (lead); **two or more independent annotators** who are competent in the domain but were not involved in the original labelling and have not seen the original labels — recruitment is the critical-path constraint; an adjudicator (senior domain practitioner, independent of both); privacy sign-off for any segment stratification.

## Test design

- **Sampling approach:** stratified random sample from the labelled set. Stratify by (a) customer segment where feasible and lawful, (b) label class (including minority classes, deliberately over-sampled), and (c) labelling batch/annotator cohort where that metadata exists — batch effects are a common hidden driver of label noise. Indicative n=200–400 examples; the canvas gives no prescribed size, and the reviewer must document the rationale (precision needed on kappa versus annotator cost).
- **Blinding:** annotators receive case content and the documented guidelines only. Original labels are withheld and held by the reviewer.
- **Adjudication protocol:** define before execution — where the two independent annotators disagree, the adjudicator assigns a resolved label without seeing the original; only then is the original revealed for comparison.
- **Controls:** include a small set of examples with unambiguous labels agreed in advance as an annotator-competence check. If an annotator fails these, their results are excluded and recorded.
- **Benign-payload principles:** not applicable (no adversarial content). The relevant safety rule is data handling — anonymised or synthetic case content only, and no export of identifiers to annotators.

## Steps

1. Review the labelling guidelines and any existing IAA statistics. **Record:** whether IAA was ever computed, by whom, on which dataset version, and whether it is disclosed alongside the model's accuracy claim.
2. Construct the stratified sample and document the strata, sizes and rationale. Withhold original labels. **Record:** sampling design and the sealed original-label file.
3. Brief annotators on the guidelines *as written* — do not clarify ambiguities, since guideline ambiguity is part of what is being measured. **Record:** briefing content and any questions asked (questions are themselves evidence of guideline weakness).
4. Run the competence-check subset. Exclude and record any annotator failing it.
5. Have each annotator independently label the full sample. **Record:** per-annotator labels, time taken, and any items flagged unlabelable.
6. Compute inter-annotator agreement between the independent annotators (Cohen's kappa for two, Fleiss' kappa for more). **Record:** overall kappa and kappa by stratum.
7. Run adjudication on all disagreements. **Record:** adjudicated labels and the adjudication rationale for a sample of cases.
8. Unseal the original labels. Compute agreement between adjudicated labels and originals, overall and by stratum. **Record:** agreement rates, and the direction of systematic disagreement where one exists (e.g. originals consistently harsher for one segment).
9. Compute a label-quality-adjusted view of the model's reported accuracy: re-score the model's outputs on the sampled examples against adjudicated labels rather than original labels. **Record:** reported accuracy vs adjusted accuracy, and the gap.
10. Inspect vendor annotation contracts for a quality-disclosure obligation. **Record:** clause reference or absence.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Inter-annotator kappa | Against the firm's documented, justified threshold; canvas illustrates kappa ≥ 0.6 as an example only | Firm-defined; **no FS-specific consensus threshold exists** — the canvas is explicit |
| Original-vs-adjudicated agreement | **Reviewer judgement — no established threshold**; "no material discrepancy" is the canvas pass indicator | Canvas |
| Stratified kappa by customer segment | No segment materially lower than others — materiality is **reviewer judgement** | Canvas pass indicator; segment-stratified IAA is labelled Emerging Practice in the canvas controls |
| Reported vs label-quality-adjusted accuracy | Report the gap; no threshold | Bespoke |

## Interpretation

- **Pass** — IAA exists and meets a documented, justified threshold for every labelled set feeding fine-tuning or validation; re-annotation shows no material discrepancy; no segment shows materially lower reliability; model documentation discloses label quality alongside accuracy.
- **Fail** — no IAA statistic for labels underpinning a current approval; independent re-annotation reveals a materially different label distribution; a segment shows systematically lower agreement and this was unflagged in validation; vendor contracts contain no quality-disclosure obligation and no data is available to test it.
- **Partial** — canvas shape: measurement exists for the primary training set but not a supplementary set (new product line, minority segment). Report the proportion of fine-tuning examples uncovered. Also partial where kappa is adequate overall but the reviewer's stratified view is under-powered — state that the segment question is unresolved rather than passed.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Sampling design, strata, sealed original-label file | L3 |
| Annotator briefing pack and question log | L3 |
| Per-annotator label sheets and competence-check results | L3 |
| Kappa computations (overall and stratified) with working | **L4** (independent re-annotation audit performed by a party independent of the original labelling) |
| Adjudication record with rationale samples | L4 |
| Reported-vs-adjusted accuracy comparison | L4 |
| Vendor contract clause extracts; existing firm IAA statistics | L2 |
| Vendor rolling-IAA scorecards, where an ongoing pipeline exists | L5 |

## Common pitfalls & limitations

- **Annotator contamination.** Any exposure to original labels destroys the test. Enforce the seal procedurally, not by trust.
- **Clarifying the guidelines during briefing.** Tempting and fatal — it measures the reviewer's clarification, not the guideline the original annotators used.
- **Under-powered stratification.** Segment-level kappa on 15 examples is noise. Either power the strata or report the segment question as unresolved.
- **Canvas limitation carried forward:** segment-stratified IAA is labelled **Emerging Practice** in the canvas's own control list — there is no published FS standard for it. ISO/IEC TS 4213:2022 is a general, non-FS statistical-assessment reference, not a label-quality benchmark.
- **Kappa is sensitive to class prevalence.** A high kappa on a balanced sample may not transfer to a skewed production distribution; report prevalence alongside.
- **Cost and lead time.** Independent domain-competent annotators are scarce; this is the procedure most likely to slip.

## Time/effort estimate

**5 reviewer-days** for the reviewer (1 design and recruitment coordination; 0.5 briefing; 1.5 adjudication supervision and scoring; 1 statistical analysis; 1 reporting), plus annotator effort costed separately (typically 2–4 person-days per annotator).

---
---

