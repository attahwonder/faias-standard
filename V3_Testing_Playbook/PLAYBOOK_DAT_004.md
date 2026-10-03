# TP-DAT-004 — Synthetic-Data Provenance and Fidelity Testing

**Procedure ID:** TP-DAT-004
**IRQ:** IRQ-DAT-004 — Undeclared or Unvalidated Synthetic Data Concealing Rare Events and Subgroups
**Assurance objective:** AO-DAT-004 — synthetic data used in training, fine-tuning or validation corpora shall be identifiable as such, with generation method and proportion documented, and shall be validated to demonstrate preservation of rare events, minority-subgroup characteristics and real-world complexity before use.
**★ Confidence:** ★2 (carried from canvas — research base strong but developed for recursive generative-model collapse, not FS tabular/text fine-tuning augmentation; test design requires significant adaptation and professional judgement)
**Method classification:** Adapted Industry Practice bordering on Emerging Practice — collapse-detection approaches from Shumailov et al. (2024) and Alemohammad et al. (2023) adapted to a discriminative FS use case. The canvas states plainly that this literature was developed for a different setting; the adaptation is documented, not concealed.

## Preconditions

- **Environment:** non-production analytical environment with access to the synthetic augmentation set and a held-out **real** reference sample covering the same classes. Real reference data must be anonymised or approved historical non-live data.
- **Access needed:** the augmentation set with any provenance tags; the generator configuration/method documentation; the blended training corpus; a held-out real rare-event sample; model artefacts sufficient to run holdout evaluation in staging.
- **Artefacts requested in advance (2 weeks):** synthetic data generation methodology document (generator type, target classes, proportion); data registry entries showing real/synthetic tagging; the augmentation strategy (accumulation vs replacement); existing fidelity validation results, if any; validation reports stating what proportion of the test set was synthetic.
- **Personnel:** reviewer (lead, statistically literate); data scientist who owns the generator (for configuration facts only); model owner for holdout evaluation execution.

## Test design

- **Provenance component:** an inventory reconciliation — every record in the blended corpus should carry a real/synthetic tag traceable to a documented generation method and proportion.
- **Fidelity component:** compare the synthetic set against the real reference on three families of statistics: (a) **distributional tails** — extreme-quantile behaviour of key features, tail mass, maximum/minimum ranges; (b) **subgroup diversity** — within-segment variance and distinct-pattern counts for minority segments; (c) **rare-event feature combinations** — the joint combinations that define the rare event, counted and compared, since mode collapse typically shows as missing *combinations* rather than missing marginals.
- **Sampling approach:** match on class. For each rare class, draw the full synthetic set (usually small) and a real reference sample of comparable or larger size. Where real rare examples are too few for stable statistics, say so — under-powered comparison is a finding about data scarcity, not a pass.
- **Performance component:** evaluate model performance separately on a real rare-event holdout and a synthetic rare-event holdout. The gap is the headline measure.
- **Benign-payload principles:** not applicable. Safety rule: real reference data is anonymised; no re-identification attempts; synthetic records are never promoted out of the test environment as if real.

## Steps

1. Reconcile the blended corpus against provenance tags. **Record:** proportion tagged, proportion untagged, and whether the synthetic proportion is documented anywhere.
2. Review the generation methodology document. **Record:** generator type, target classes, generation date, and whether the strategy accumulates alongside real data or replaces it.
3. Define the fidelity statistic set and the materiality convention **before** computing anything (which features, which quantiles, which segments). **Record:** the pre-registered statistic list, dated.
4. Compute tail statistics for synthetic vs real reference on each selected feature. **Record:** paired statistics, and the direction of any compression.
5. Compute within-segment diversity for each minority segment: variance, distinct-pattern count, and the ratio of synthetic to real diversity. **Record:** per-segment table.
6. Enumerate rare-event feature combinations present in the real reference and check presence in the synthetic set. **Record:** combinations present in real but absent in synthetic (the mode-collapse signature).
7. Run the model on the real rare-event holdout and the synthetic rare-event holdout separately. **Record:** per-holdout performance and the gap.
8. Inspect validation reports for disclosure of the synthetic proportion of the test set. **Record:** disclosed / not disclosed.
9. Where the augmentation strategy replaces rather than accumulates real data, record this against the canvas's accumulation control (Gerstgrasser et al., 2024, as cited in the canvas).

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Proportion of records with provenance tags | 100% (canvas pass indicator) | Canvas / EU AI Act Art. 10 data governance |
| Tail-distribution loss (synthetic vs real) | "No material loss" — materiality is **reviewer judgement, no established threshold** | Canvas states no FS benchmark; collapse literature gives direction, not thresholds |
| Within-segment diversity ratio | **Reviewer judgement — no established threshold** | Canvas |
| Rare-combination coverage | Report count of real combinations absent from synthetic; **no established threshold** | Bespoke |
| Real vs synthetic rare-event holdout performance gap | "Not materially worse" (canvas pass indicator); materiality **reviewer judgement** | Canvas |

## Interpretation

- **Pass** — all synthetic records tagged and traceable to a documented method and proportion; no material tail or subgroup-diversity loss versus the real reference; real rare-event holdout performance not materially worse than synthetic; augmentation accumulates rather than replaces.
- **Fail** — synthetic and real blended with no provenance tag and unknown proportion; fidelity testing shows synthetic tail cases systematically easier or more homogeneous (mode collapse); validation metrics reported without disclosing the synthetic proportion of the test set; minority-segment augmentation reduces rather than preserves within-segment diversity.
- **Partial** — canvas shape: tagging exists for the primary training set but fidelity validation has not reached the minority-segment augmentation subset. Report the percentage of that segment's training examples affected. Also partial where the real reference is too thin for a powered comparison — that is an unresolved question, not a pass.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Provenance reconciliation table | L3 |
| Generation methodology document | L2 |
| Pre-registered statistic list (dated) | L3 |
| Fidelity computation workbooks (tails, diversity, combinations) | **L4** (independent audit of fidelity) |
| Real vs synthetic holdout performance comparison | L4 |
| Validation-report disclosure check | L2 |
| Post-deployment rare-event outcome monitoring, where the firm holds it | L5 |

## Common pitfalls & limitations

- **Comparing marginals only.** Mode collapse frequently preserves marginal distributions while destroying joint structure. The combination enumeration in step 6 is the load-bearing measure.
- **Post-hoc statistic selection.** Choosing statistics after seeing results turns this into advocacy. Pre-register in step 3.
- **Thin real reference.** The exact classes most in need of augmentation are the ones with least real data to compare against — an inherent limitation of the procedure, and one to state rather than paper over.
- **Canvas limitation carried forward:** the model-collapse literature (Shumailov 2024, Alemohammad 2023, Gerstgrasser 2024, Dohmatob 2024) addresses recursive generative-model training, not FS tabular fine-tuning augmentation. The analogy is credible but adapted — hence ★2, and hence conclusions are professional assessment, not standardised evidence (METHODOLOGY_STANDARDS §3c).
- **Fidelity is not utility.** A synthetic set can be statistically faithful and still unhelpful, or divergent and still useful. Report fidelity as a risk indicator, not a quality verdict.

## Time/effort estimate

**4 reviewer-days** (0.5 provenance reconciliation; 0.5 pre-registration and design; 1.5 statistical computation; 1 holdout evaluation and analysis; 0.5 reporting).

---
---

