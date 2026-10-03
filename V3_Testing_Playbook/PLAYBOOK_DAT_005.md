# TP-DAT-005 — Representativeness Comparison Against the Current Book

**Procedure ID:** TP-DAT-005
**IRQ:** IRQ-DAT-005 — Training Data Under-Representing the Current Customer Book
**Assurance objective:** AO-DAT-005 — the firm shall assess and document the representativeness of training and reference data against its current customer book, product set and market conditions, at build and at defined refresh intervals, with material gaps disclosed.
**★ Confidence:** ★3 (carried from canvas — published, multiply-used statistical shift-detection methods per Rabanser et al. 2019 and Koh et al. 2021; segment definition and materiality thresholds require professional judgement, so short of ★4)
**Method classification:** Established/Adapted — distribution-comparison methodology (population stability index, two-sample tests) applied to a training-vs-book comparison.

## Preconditions

- **Environment:** non-production analytical environment. The "current book" input is a **statistical composition snapshot** — counts and proportions by segment, product, vintage and geography — not a customer-level extract. This keeps the procedure within the non-production rule.
- **Access needed:** training/reference dataset composition; current book composition snapshot; segment and product taxonomies; held-out samples matching underrepresented segments (anonymised or synthetic); staging model for segment-stratified evaluation.
- **Artefacts requested in advance (2 weeks):** representativeness assessments performed at build and at each refresh; the defined refresh cadence; segment-stratified validation results, if any; gap analyses for any product/segment extension of an existing model; the firm's documented PSI or equivalent threshold.
- **Personnel:** reviewer (lead); MI/analytics contact to produce the book composition snapshot; model owner for stratified evaluation.

## Test design

- **Comparison dimensions:** segment, product, vintage (time of origination), geography — as specified in the canvas. Add any dimension the firm's own risk taxonomy treats as material.
- **Sampling approach:** full-population composition comparison where possible (this is a distributional comparison, not a sample-based one). Where the training set is too large to profile fully, use a documented random sample with recorded seed.
- **Case categories:** deliberately include (a) segments that have grown materially since the training vintage, (b) products launched after the training vintage, and (c) geographies added since. These are where the gap concentrates.
- **Stratified evaluation:** for each segment failing the distributional check, evaluate model performance on a held-out sample matched to that segment and compare against aggregate reported performance.
- **Benign-payload principles:** not applicable; the safety rule is that no customer-level data leaves the analytical environment and the book snapshot is aggregate-only.

## Steps

1. Obtain and validate the current book composition snapshot (completeness, as-at date). **Record:** as-at date, total volumes, dimension coverage.
2. Profile the training/reference dataset on the same dimensions using the same taxonomy. Reconcile taxonomy mismatches explicitly — a mismatch is itself a finding. **Record:** profile tables, taxonomy reconciliation notes.
3. Compute distributional comparison statistics per dimension: population stability index per category, plus a two-sample test where the dimension is continuous (per Rabanser et al., 2019, as cited in the canvas). **Record:** per-dimension, per-category statistics.
4. Compare each statistic against the firm's documented threshold. Where no threshold is documented, record *no threshold defined* — a finding against the objective's "material gaps disclosed" clause — and report the raw statistics without a pass/fail claim.
5. Identify all segments/products/geographies present materially in the book but thin or absent in training. **Record:** the gap list, ranked by book volume.
6. For the top gaps, run segment-stratified evaluation on matched held-out samples. Compare against aggregate reported performance. **Record:** per-segment performance versus aggregate, and the gap.
7. Review representativeness assessments on file: were they performed at build, and at the stated refresh cadence? **Record:** assessment dates versus cadence, and any missed refresh.
8. For each documented extension of an existing model to a new product or segment, check for a preceding gap analysis. **Record:** extension events with and without gap analysis.
9. Check whether validation reporting presents segment-stratified results **alongside** aggregate accuracy, not instead of it. **Record:** reporting format.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| PSI per category | Against the firm's own documented threshold | Firm-defined; **reviewer judgement — no established FS threshold** if undocumented |
| Two-sample test outcomes | Report statistic and significance; materiality is **reviewer judgement** | Rabanser et al. (2019) methodology as cited in canvas |
| Segment-stratified performance versus aggregate | "No material degradation invisible in aggregate KPIs" (canvas fail indicator); materiality **reviewer judgement** | Canvas |
| Refresh cadence adherence | Against the firm's own defined cadence | Canvas pass indicator |
| Extensions preceded by gap analysis | 100% (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — representativeness assessment on file at build and refreshed on cadence; no segment shows a material distributional gap without a corresponding validated performance check; segment-stratified results reported alongside aggregate; extensions preceded by explicit gap analysis.
- **Fail** — no representativeness comparison exists and reporting is aggregate-only; a materially grown or new segment is thin or absent in training with no gap analysis; stratified performance shows material degradation for an underrepresented segment invisible in aggregate KPIs; a model was extended to a new product without a documented check.
- **Partial** — assessment exists at build but refresh has lapsed; or gaps are identified but not disclosed in the reporting that decision-makers actually see. State the affected book volume as a proportion.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Book composition snapshot (aggregate) and training profile tables | L3 |
| Taxonomy reconciliation notes | L3 |
| PSI/two-sample computation workbook | **L4** (independent comparison) |
| Gap list with book volumes | L4 |
| Segment-stratified evaluation results | L4 |
| Firm's own representativeness assessments and refresh records | L2–L3 |
| Production outcome data by segment, where held | L5 |

## Common pitfalls & limitations

- **Taxonomy drift.** Training-era segment definitions frequently differ from current MI definitions; comparing them naively manufactures a gap or hides one. Reconcile explicitly and record.
- **PSI thresholds are conventions, not standards.** Common industry figures are heuristics; the canvas ★3 rating is explicitly held short of ★4 because materiality thresholds require professional judgement. Do not present a PSI cut-off as an external requirement.
- **Aggregate performance masking.** The whole point of step 6 — do not stop at the distributional comparison, which shows exposure, not harm.
- **Vintage confounding.** A gap on the vintage dimension may reflect a deliberate, defensible recency policy rather than neglect; ask before scoring.
- **Book snapshot quality.** If the firm cannot produce a reliable composition snapshot, that is a finding in its own right and blocks the procedure.

## Time/effort estimate

**3 reviewer-days** (0.5 snapshot validation and profiling; 1 statistical comparison; 1 stratified evaluation and analysis; 0.5 reporting).

---
---

