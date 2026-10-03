# TP-MOD-015 — LLM-as-Judge Validation: Human-Agreement, Bias-Probe and Correlated-Error Testing

**Procedure ID:** TP-MOD-015
**IRQ:** IRQ-MOD-015 — Unvalidated LLM-as-Judge Producing Unsound Evaluation Evidence
**Assurance objective:** AO-MOD-015 — where a language model is used as judge or evaluator to generate the institution's own evaluation evidence, that judge shall be independently validated for known bias classes and human-judgement agreement, its version shall be pinned so evaluation evidence remains comparable over time, and correlated-error risk shall be assessed and compensated for where judge and assessed system share a model family.
**★ Confidence:** ★3 (carried from canvas — see canvas §11. Summary: a credible, peer-reviewed and widely-cited evaluation methodology exists with a defined bias taxonomy and human-agreement validation approach; no agreed industry or FAIAS-standard acceptance threshold exists, so pass/fail judgement on the measured results remains a professional-judgement call.)
**Method classification:** Adapted Industry Practice — the LLM-as-judge validation methodology of Zheng et al. (2023), *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena*, arXiv:2306.05685, NeurIPS 2023 Datasets and Benchmarks Track, as cited in the canvas: human-agreement study, order-swap and length-matched bias probes, and self-enhancement-bias screening. The canvas states plainly that **the paper supplies a measurement method, not a pass/fail bar**, and that **no FAIAS-standard acceptance threshold exists for judge/human agreement or for the magnitude of tolerable bias — stated, not implied**; the firm sets and documents its own thresholds.

## Preconditions

- **Environment:** non-production staging, on synthetic, anonymised or historical non-live data. The sample under test is **the outputs the judge is used to evaluate**, not production customer data.
- **Access needed:** the judge model and its pinned version identifier; the evaluation criteria and judging prompt the judge is given; a representative sample of judge-scored outputs with the judge's verdicts; the identity and version of the system under assessment, so that shared-model-family correlation can be established; the ability to substitute a cross-family judge on a subsample, or human raters for the same subsample; the version-pinning configuration and any re-validation trigger.
- **Artefacts requested in advance (3 weeks — human rater availability drives the lead time):** the design documentation specifying the judge model, its pinned version, the bias-testing methodology to be applied and the human-agreement sample size; any existing human-agreement or bias-probe results; the judge's version-change history and any provider-side update notices; the independent validation report covering the judge, where one exists; the inventory of evaluation use cases relying on the judge, and the outputs its verdicts fed into — approval papers, monitoring dashboards, vendor comparisons.
- **Personnel:** reviewer (lead); **human raters drawn from the domain, independent of the team that selected the judge and independent of the development team for the system under assessment**; the evaluation function that operates the judge; the independent validation function; the vendor-management contact for provider-side judge update terms.
- **Shared asset:** the domain's independent evaluator pool, whose documented independence from any reward model used in fine-tuning is established once and relied on throughout. Where that pool has been briefed for TP-MOD-004 or TP-MOD-008, brief it once more rather than recruiting separately — **but note that this procedure requires a wider independence condition than the pool's existing one: independence must also run to the team that selected the judge.**
- **Dependency:** run alongside TP-MOD-011 where both are in scope. The canvas names this IRQ as the evaluator-side twin of TP-MOD-011's benchmark-side contamination question, and a single reviewer holding both produces a materially stronger combined finding on evaluation-evidence integrity.

## Test design

- **Limb 1 — human-agreement study.** A representative sample of judge-scored outputs is independently re-scored by human raters **using the same criteria the judge was given**, and agreement between judge and human verdicts is computed. Re-scoring against improved or clarified criteria measures the reviewer's clarification, not the judge's agreement.
- **Limb 2 — position-bias probe.** Order-swapped subsets: an identical candidate pair presented in reversed order. A verdict that shifts with presentation order is position bias.
- **Limb 3 — verbosity-bias probe.** Length-matched subsets, verbosity controlled, testing whether the judge favours longer answers independent of quality.
- **Limb 4 — correlated-error check.** Where the judge model and the system under assessment share a model family, either a cross-family judge is substituted on a subsample, or a human spot-check is applied to that subsample, and the results compared. This is the self-enhancement-bias limb, per the canvas's citation.
- **Limb 5 — version pinning.** The judge model's pinned version is recorded alongside all results, and the version-change history is reviewed for any provider-side update, and for whether that update triggered and completed re-validation before continued reliance. The control is mirrored from IRQ-TPR-004 and applied to the evaluator rather than the deployed model, per the canvas.
- **Sample discipline.** The human-agreement sample size is fixed and recorded before any scoring. The canvas prescribes no size, so the size and its rationale are documented as tester judgement.
- **Threshold discipline.** The firm sets and documents its own human-agreement and bias-tolerance thresholds. **FAIAS prescribes none**, since none is established in the field, and the canvas states this rather than implying it. Where the firm has no documented threshold, the measurements stand and the missing threshold is reported as a separate finding; the reviewer does not invent one.
- **Benign-payload principles:** not applicable. The governing safety rules are data handling — the sample is evaluation output, not production customer data — and rater independence, which is a design condition rather than a courtesy.

## Steps

1. Establish where the judge is relied upon: approval evidence, production monitoring, vendor and model selection. **Record:** the evaluation use-case inventory — the conclusion's blast radius, which bounds the consequence of every adverse finding below.
2. Record the judge model and its pinned version, the evaluation criteria as given to the judge, and the system under assessment with its model family. **Record:** the identifiers, the configuration, and whether judge and assessed system share a family.
3. Establish whether any human-agreement study or bias-probe testing has previously been performed. **Record:** the evidence, or the fact that judge verdicts are relied upon with no independent corroboration.
4. Obtain the firm's documented human-agreement and bias-tolerance thresholds. **Record:** the thresholds and their approval route, or the fact that none exist.
5. Draw and record the representative sample of judge-scored outputs, fix the rating rubric — which is the judge's own criteria — and construct the bias-probe subsets, all before any rater sees a case.
6. Brief the human raters on the criteria **as given to the judge**, without clarification. **Record:** the briefing content and any questions raised, which are themselves evidence of criteria ambiguity.
7. Have raters independently re-score the sample. Compute agreement between judge and human verdicts. **Record:** per-item judge and human verdicts, the agreement measure and the method used to compute it, and inter-rater agreement among the humans as the interpretive floor.
8. Run the order-swapped position-bias probe. **Record:** the proportion of pairs on which the verdict shifts with presentation order.
9. Run the length-matched verbosity-bias probe. **Record:** the direction and magnitude of any length preference independent of quality.
10. Where judge and assessed system share a model family, run the correlated-error limb — cross-family judge or human spot-check on a subsample — and compare against the primary judge's verdicts. **Record:** which compensating route was used and the divergence, or that no shared family exists and the limb does not apply.
11. Compare all results against the firm's documented thresholds. **Record:** the comparison and its basis, or that no threshold exists.
12. Review the judge's version-pinning configuration and version-change history. **Record:** every provider-side update in the reliance period, and whether each triggered and completed re-validation before continued reliance.
13. Review independent validation coverage: was the judge-validation methodology and its findings assessed by a function independent of the team that selected the judge? **Record:** the report, or its absence.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Judge/human agreement rate | Against **the firm's own documented and approved threshold** (canvas pass indicator). **No FAIAS-standard acceptance threshold exists — stated, not implied**; where the firm has none, report the measurement and the missing threshold separately | Canvas; Zheng et al. (2023) as cited — the paper supplies a measurement method, not a pass/fail bar |
| Position bias — verdict shift under order-swapped presentation | **No material position bias** (canvas pass indicator); materiality against the firm's documented tolerance, and **reviewer judgement where none exists — no established threshold** | Canvas; Zheng et al. (2023) |
| Verbosity bias — length preference on length-matched pairs | **No material verbosity bias** (canvas pass indicator); same threshold basis | Canvas; Zheng et al. (2023) |
| Judge version pinning and re-validation on provider-side change | Pinned and recorded; any provider-side update triggered and completed re-validation before continued reliance (canvas pass indicator) | Canvas; control mirrored from IRQ-TPR-004 per canvas |
| Correlated error where judge and assessed system share a model family | Compensating cross-family or human-spot-check step applied, showing **no material correlated-error divergence** (canvas pass indicator); absence of any compensating step with no correlated-error assessment is a canvas fail indicator | Canvas; Zheng et al. (2023) self-enhancement-bias finding |
| Inter-rater agreement among the human raters | Reported alongside the judge/human agreement rate; where the humans do not agree with each other, the judge's disagreement with them is uninterpretable | ASSURANCE_MODEL.md §7A; canvas §9 — and MOD domain convention on blind scoring and agreement |

## Interpretation

- **Pass** — the human-agreement study shows judge verdicts aligning with human raters at a rate the firm has documented and approved as its own threshold; order-swap and length-matched probes show no material position or verbosity bias; the judge version is pinned and recorded, and any provider-side update triggered and completed re-validation before continued reliance; and where judge and assessed system share a model family, a compensating cross-family or human-spot-check step has been applied and shows no material correlated-error divergence.
- **Fail** — no human-agreement study has been performed and judge verdicts are relied upon as evaluation evidence with no independent corroboration; **or** order-swap or length-matched testing reveals material position or verbosity bias; **or** the judge version is unpinned, or a provider-side update occurred with no re-validation, so evaluation evidence is no longer comparable over time without anyone having noticed; **or** judge and assessed system share a model family with no compensating step and no correlated-error assessment.
- **Partial** — the canvas's own shape: a human-agreement study exists for one evaluation use case, but the same judge is relied upon for another without equivalent bias-probe testing or correlated-error assessment. The assurance objective is not met for the second use case pending equivalent validation. Report which downstream conclusions rest on which.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Vendor or internal assertion that the judge model is reliable, with no bias testing or human-agreement study | **L1** (assertion only; flag) |
| Design documentation specifying the judge model, its pinned version, the bias-testing methodology and the human-agreement sample size | L2 |
| Evaluation use-case inventory: every downstream conclusion resting on the judge's output | L2 |
| Sampling design, fixed rubric and rater briefing pack with the question log | L3 |
| Human-agreement study results: judge-versus-human agreement on a representative sample, with inter-rater agreement reported alongside | **L3** |
| Order-swap position-bias probe results | L3 |
| Length-matched verbosity-bias probe results | L3 |
| Correlated-error comparison (cross-family judge or human spot-check) where model families are shared | L3 |
| Judge version-pinning record and version-change history with re-validation evidence | L3 |
| Independent validation report assessing the judge-validation methodology and findings, performed by a function independent of the development team that selected the judge | **L4** |
| Production monitoring evidence that judge version pinning is enforced and that re-validation was triggered and completed following a provider-side judge update | L5 |

## Common pitfalls & limitations

- **Treating the judge as neutral infrastructure.** This is the canvas's blind-spot finding: the evaluator is another AI system with its own documented failure modes, not a tool that checks the AI. A fluent, well-formatted verdict looks identical whether sound or biased.
- **Re-scoring against different criteria than the judge used.** The human raters must apply the criteria the judge was given. Improving or clarifying them at briefing measures the reviewer's clarification, not the judge's agreement.
- **Reporting judge/human agreement without inter-rater agreement.** If the humans do not agree with each other, the judge's disagreement with them is uninterpretable. Report both.
- **Recruiting raters connected to the judge's selection.** Independence must run to the team that chose the judge, not only to the development team for the system under assessment — a wider condition than the domain's existing evaluator-pool independence.
- **Skipping the correlated-error limb because the families "look different", or because the family question was never asked.** Establish the model families first, from the model identifiers rather than the product name — a specialist vendor's judge may itself sit on a frontier family already in use as the assessed system.
- **Accepting a pinned version on paper.** The evidence is enforcement plus a re-validation trail after an actual provider update, not a configuration screenshot. Version pinning without a re-validation trigger is half a control.
- **Inventing an acceptance threshold.** The methodology supplies measurement, not a bar. Where the firm has set none, report the measurements and the missing threshold separately.
- **Canvas limitation carried forward:** a credible, peer-reviewed and widely-cited methodology exists, but no agreed industry or FAIAS-standard acceptance threshold for judge/human agreement or for the magnitude of tolerable bias. ★3 — threshold-setting and materiality remain reviewer professional judgement, and reporting must say so.
- **Consequence bounding.** Where an adverse finding is made, the affected population is every downstream conclusion drawn from this judge's output, not only the system currently under review. Step 1 exists so that the report can say how far the finding reaches.

## Time/effort estimate

**5 reviewer-days** (0.5 use-case inventory, judge/version/model-family identification and prior-evidence review; 0.5 sampling design, rubric fixing and probe-subset construction; 0.5 rater briefing; 1 agreement computation and analysis, including inter-rater agreement; 1 position- and verbosity-bias probe execution; 0.5 correlated-error limb; 0.5 version-history and independent-validation review; 0.5 reporting). Human rater effort is costed separately as non-reviewer support, typically 1–3 person-days per rater.

---
---

