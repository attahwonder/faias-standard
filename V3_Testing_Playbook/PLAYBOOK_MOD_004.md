# TP-MOD-004 — Task-Representative Hallucination Measurement

**Procedure ID:** TP-MOD-004
**IRQ:** IRQ-MOD-004 — Unmeasured Hallucination Rate Against Task-Representative FS Tolerance
**Assurance objective:** AO-MOD-004 — the frequency and severity of hallucinated facts, figures and citations shall be measured on tasks representative of the intended FS use, and a documented tolerance threshold shall be established and approved before deployment.
**★ Confidence:** ★3 (carried from canvas — credible, peer-reviewed measurement methods with multiple independent research groups (Min et al., 2023; Manakul et al., 2023); no single canonical hallucination-rate benchmark exists for FS-specific tasks, so test design and severity classification rest on professional judgement)
**Method classification:** Adapted Industry Practice — atomic-fact decomposition and verification (FActScore-style, Min et al., 2023) and sampling-consistency checking (SelfCheckGPT-style, Manakul et al., 2023), adapted to FS task types.

## Preconditions

- **Environment:** staging pipeline. Cases are synthetic/anonymised or historical non-live.
- **Access needed:** staging pipeline; the source documents constituting ground truth; the governance record of any approved tolerance threshold; production QA/complaint data (aggregate) for the comparison step.
- **Artefacts requested in advance (2 weeks):** the documented hallucination tolerance threshold and its approval record; any existing hallucination measurement and its methodology; the source-document corpus supporting ground truth; production QA sampling and complaint categorisation.
- **Personnel:** reviewer (lead); two independent evaluators for atomic-fact verification and severity classification (drawn from the shared evaluator pool, independent of any fine-tuning reward signal); domain SME to define the cosmetic/material severity boundary.

## Test design

- **Sample:** n≥150 (canvas figure) of the firm's actual task type — customer-facing product queries, claims summaries or AML narrative drafts — each with verifiable ground truth drawn from source documents. Representativeness is the point: a generic benchmark score is explicitly a fail indicator.
- **Stratification:** across task subtypes and, where relevant, across evidence-completeness conditions, so the measured rate is not dominated by the easiest subtype.
- **Atomic-fact decomposition:** each output is decomposed into atomic factual assertions; each assertion is verified against source documents as **supported / contradicted / unverifiable**. Two evaluators decompose and verify independently on an overlap subsample to establish agreement.
- **Severity classification (defined before scoring):** **cosmetic** (does not affect any decision or customer understanding) versus **material/decision-relevant** (fabricated policy terms, invented case facts, wrong figures, fabricated citations). The SME sets the boundary; the reviewer applies it.
- **Consistency cross-check:** where model-internal probabilities are unavailable (hosted API), generate k independent completions per case and compare for factual consistency (SelfCheckGPT-style), giving a second, model-agnostic signal.
- **Benign-payload principles:** ordinary business queries; no adversarial elicitation. The test measures baseline behaviour, not worst-case adversarial behaviour.

## Steps

1. Confirm whether a documented, governance-approved tolerance threshold exists and when it was approved relative to deployment. **Record:** the threshold, the approval record and its date, or *no approved threshold* — which is itself a canvas fail indicator regardless of the measured rate.
2. Assemble the n≥150 stratified sample with ground truth traced to source documents. **Record:** sample composition, source-document mapping.
3. Define the severity rubric with the SME and date it before any scoring. **Record:** the rubric.
4. Fix and record the decoding configuration; set k for the consistency check.
5. Run the pipeline on all cases, generating one primary output plus k independent completions per case. **Record:** all outputs.
6. Decompose primary outputs into atomic assertions and verify each against source documents. **Record:** per-assertion verdicts, per-case counts.
7. Establish evaluator agreement on the overlap subsample. **Record:** agreement rate — a low rate means the severity rubric is under-specified and must be tightened before the headline figure is reported.
8. Classify every unsupported assertion by severity. **Record:** cosmetic and material counts, and the material-hallucination rate.
9. Run the consistency check: compare the k completions per case for factual divergence. **Record:** consistency scores, and their correlation with the verification results (agreement between the two signals strengthens the finding; divergence should be reported, not smoothed).
10. Compare the measured rate against the approved tolerance. **Record:** the comparison, or note that no threshold exists to compare against.
11. Compare against production QA and complaint data for hallucination-driven harm. **Record:** whether production experience is consistent with the staging-measured rate.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Overall hallucination rate (assertions unsupported / total) | At or below the approved tolerance (canvas pass indicator) | Firm-approved; **no canonical FS benchmark** exists (canvas ★3 caveat) |
| Material/decision-relevant hallucination rate | At or near zero (canvas pass indicator) | Canvas |
| Cosmetic versus material distribution | Only cosmetic errors at any meaningful rate (canvas pass indicator) | Canvas |
| Evaluator agreement on severity | **Reviewer judgement — no established threshold**; report it as a quality measure of the finding itself | Bespoke |
| Consistency-check divergence | Report; corroborative signal, **no established threshold** | Manakul et al. (2023) as cited |
| Production monitoring divergence from staging rate | No material divergence (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — the measured rate on the task-representative sample is at or below the approved tolerance with material/decision-relevant hallucinations at or near zero; severity classification distinguishes cosmetic from material and only cosmetic errors occur at any meaningful rate; the tolerance threshold was documented and formally approved before deployment; production monitoring shows no material divergence from the staging rate.
- **Fail** — no task-representative measurement was performed and only a generic or vendor-reported benchmark score is cited; material hallucinations occur at a non-trivial rate (fabricated policy terms, invented case facts); no documented, governance-approved tolerance threshold exists, meaning "acceptable" hallucination risk was never explicitly decided; production complaint or QA data reveals hallucination-driven customer harm that no staging measurement anticipated.
- **Partial** — a rate is measured and acceptable but no threshold was ever approved (measurement without a decision); or measurement covers one task subtype and not others. Note that an unapproved threshold is a governance fail even where the measured rate is good — the canvas treats these as separate indicators.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Tolerance threshold and its approval record | L2 |
| Sample composition and source-document ground-truth mapping | L3 |
| Severity rubric (dated pre-scoring) | L3 |
| Full outputs including the k consistency completions | **L4** |
| Atomic-assertion verification sheets, both evaluators | L4 |
| Evaluator agreement computation | L4 |
| Severity classification and rate computation | L4 |
| Consistency-check results | L4 |
| Production QA/complaint comparison | L5 |

## Common pitfalls & limitations

- **Citing a vendor benchmark instead of measuring.** Explicitly a fail indicator, and the most common state found.
- **Severity rubric written after seeing results.** Pre-date it (step 3) or the headline rate is unfalsifiable.
- **Single evaluator.** Hallucination severity judgements vary substantially between people; the agreement measure in step 7 is what makes the rate credible.
- **Unverifiable-but-true assertions.** These are not hallucinations; the three-way verdict (supported/contradicted/unverifiable) prevents mis-scoring them, but the unverifiable bucket must be reported separately, not folded into either side.
- **Canvas limitation carried forward:** no single canonical hallucination-rate benchmark exists for FS-specific tasks; test design and severity classification rest on professional judgement. ★3 — credible method, firm-set thresholds.
- **The rate is conditional on the sample.** It describes this task type at this evidence completeness, not the system in general.

## Time/effort estimate

**6 reviewer-days** (0.5 threshold and artefact review; 1 sample assembly and ground-truth mapping; 0.5 rubric definition; 0.5 execution; 2 atomic-fact verification and severity scoring; 0.5 consistency analysis; 0.5 production comparison; 0.5 reporting). The verification stage dominates and is the least compressible.

---
---

