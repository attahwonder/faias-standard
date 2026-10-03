# CANVAS: IRQ-MOD-015

## 1. IRQ ID & Title
**IRQ-MOD-015: Unvalidated LLM-as-Judge Producing Unsound Evaluation Evidence**

Register question: "Where a language model is used as a judge or evaluator to generate the institution's own evaluation evidence, has the judge itself been validated — known bias classes (position, verbosity, self-enhancement) tested; agreement with human judgement measured; judge version pinned so evaluation evidence stays comparable; and correlated error assessed where judge and assessed system share a model family?"

**Applicability:** Y / Y / N.

## 2. Business Activities Affected
- **Model validation/pilot evidence:** an LLM judge scores a candidate system's outputs for accuracy, tone or policy compliance as part of the firm's own approval evidence base (feeds IRQ-MOD-004, IRQ-GOV-007).
- **Ongoing production monitoring:** an LLM judge grades a sample of live outputs for quality drift, feeding governance dashboards without independent human corroboration.
- **Vendor/model selection:** comparative LLM-judge scoring is used to choose between candidate models or prompt configurations, directly informing procurement.

## 3. AI Behaviour(s)
- A second language model ("the judge") is prompted to score, rank or classify the outputs of the system under evaluation, generating a verdict presented as evaluation evidence.
- The judge model exhibits documented bias classes — position bias (verdict shifts with the order candidate answers are presented), verbosity bias (favouring longer answers regardless of quality), and self-enhancement bias (rating outputs from its own model family more favourably).
- Judge behaviour can change silently when the underlying judge model is updated by the provider, without the firm's evaluation criteria having changed.

## 4. Failure Mode
> A language model used as judge or evaluator to generate the institution's own evaluation evidence has not itself been validated — its known bias classes untested, its agreement with human judgement unmeasured, its version unpinned, and any correlated-error risk with the system it assesses unscreened — so the evaluation evidence it produces is unsound at the point of generation, and every downstream conclusion drawn from it inherits that unsoundness.

## 5. Potential Consequences
- **Customer:** a system is approved, or a quality problem goes undetected, because the evaluation evidence behind the decision was itself unreliable — the harm surfaces wherever the underlying capability, accuracy or safety claim was wrong.
- **Institution:** the firm's evaluation function is undermined at its root; any conclusion drawn from LLM-judge scoring (approval decisions, monitoring dashboards, vendor comparisons) is unsupportable if challenged, and silent judge-version drift can move scores with no corresponding change in the assessed system.
- **Regulator/market:** an independent validation record shown to rest on an unvalidated evaluator is a direct SS1/23 independent-validation gap — an evidence-integrity failure one layer upstream of the more familiar contaminated-benchmark problem (IRQ-MOD-011).

## 6. Failure Chain
```
Firm adopts LLM-as-judge to generate evaluation evidence (accuracy, tone, compliance scoring)
  ↓ (IRQ-MOD-015 — THIS IRQ: judge itself not validated — bias classes untested,
     human-agreement unmeasured, version unpinned, correlated error unscreened)
Judge produces scores affected by position, verbosity or self-enhancement bias, or by an
unannounced provider-side judge update
  ↓ (IRQ-GOV-007: independent validation accepts the judge's scores as sufficient evidence
     without independent human corroboration)
System approved, or quality drift missed, on the strength of unsound evaluation evidence
  ↓ (IRQ-MOD-011: the same evidence-integrity blind spot as benchmark contamination, one
     layer upstream — at the evaluator rather than the benchmark)
Wrong approval decision or undetected quality/safety regression persists in production
  ↓
Retrospective discovery (e.g. human re-scoring disagrees materially) → governance finding
that the evaluation basis itself was never validated → re-evaluation required

Control Breakpoints:
  • IRQ-MOD-015: human-agreement study, bias-class testing, version pinning and
    correlated-error screening performed before judge output is relied upon
  • IRQ-GOV-007: independent validation requires human corroboration where judge validity
    is untested
  • IRQ-MOD-011: evidence-integrity discipline extended from benchmark contamination to
    evaluator validity
```

## 7. Why a Domain Expert May Miss It
- The evaluator is naturally treated as neutral infrastructure — "the tool that checks the AI" — rather than as another AI system with its own failure modes requiring independent validation, an assumption that does not hold for LLM judges.
- FS model risk practice is accustomed to a human reviewer or a fixed statistical metric as the source of validation evidence; substituting a second LLM for that role is a recent practice that has outpaced governance awareness of its own limitations.
- Documented bias classes (position, verbosity, self-enhancement) are specialist AI-evaluation research findings, not intuitive to a reviewer assessing evaluation methodology through a traditional QA lens.
- A judge model silently changing behaviour when the provider updates it — with no corresponding change in the firm's evaluation criteria or the system being assessed — is a dependency risk unfamiliar outside AI-specific practice.

## 8. Assurance Objective
**AO-MOD-015:** Where a language model is used as judge or evaluator to generate the institution's own evaluation evidence, that judge shall be independently validated for known bias classes and human-judgement agreement, its version shall be pinned so evaluation evidence remains comparable over time, and correlated-error risk shall be assessed and compensated for where judge and assessed system share a model family.

## 9. Expected Controls (Traced)
- **Human-agreement study** — [Zheng et al., 2023, "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena", arXiv:2306.05685, NeurIPS 2023 Datasets and Benchmarks Track] — a stated sample of judge verdicts is re-scored by human raters and agreement measured, following the paper's validation approach.
- **Inter-rater agreement among the human raters** — [ASSURANCE_MODEL.md §7A; Hallgren, K.A., 2012, *Tutorials in Quantitative Methods for Psychology* 8(1), p.24] — where more than one human rater re-scores the judge-scored sample, agreement among the human raters themselves is computed, chance-corrected where the design allows, and reported alongside the judge/human agreement; where the raters do not agree with each other, the judge's disagreement with them is uninterpretable. A single rater's verdict is not treated as ground truth without this check. No threshold is prescribed (§7A).
- **Known bias-class testing** — [Zheng et al., 2023, arXiv:2306.05685] — position bias tested via order-swapped candidate pairs; verbosity bias tested via length-matched pairs; self-enhancement bias tested or documented where judge and assessed system share a model family.
- **Judge version pinning with re-validation on change** — [linked IRQ-TPR-004, control mirrored and applied to the evaluator rather than the deployed model] — the judge model version is fixed and recorded; any provider-side judge update triggers re-validation before continued reliance, so evaluation evidence remains comparable over time.
- **Correlated-error compensating control** — [Zheng et al., 2023, arXiv:2306.05685, self-enhancement bias finding] — where the judge and the assessed system share a model family, a cross-family judge or human spot-check is used as a compensating step.
- **No FAIAS-standard acceptance threshold imposed** — [this IRQ; stated, not implied] — the firm sets and documents its own human-agreement/bias-tolerance thresholds; FAIAS does not prescribe one, since none is established in the field.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor or internal assertion that "the judge model is reliable" with no bias testing or human-agreement study — **L1** (assertion only; flag).
- Design documentation specifying the judge model, its pinned version, the bias-testing methodology to be applied and the human-agreement sample size — **L2**.
- Staging test results: human-agreement study comparing judge verdicts to human raters on a representative sample; order-swap and length-matched bias-probe results — **L3**.
- Independent validation report assessing the judge-validation methodology and findings, performed by a function independent of the development team that selected the judge — **L4**.
- Production monitoring evidence that judge version pinning is enforced and that a re-validation was triggered and completed following any provider-side judge update — **L5**.
- **Worked example — first-party disclosure, 9 September 2026 (Anthropic, "An alignment assessment of recent cybersecurity incidents").** The assessment describes a two-stage retrospective screen of "roughly 481 million transcripts" in which a "second-stage scan **using Claude**" reviewed the 9.2 million transcripts the first stage escalated (§Introduction) — an LLM-graded evaluation stage at a scale no worked example in this canvas previously reached. Separately, and **attaching to the LLM graders in the assessment's own analysis pipeline rather than to that retrospective scan**, §Methods records as a general limitation that the authors "relied heavily on LLM-based graders to classify model outputs" and that "it is possible some classifiers are misdesigned or miscalibrated". A reviewer should expect the firm's own evaluation record to state, at this level of specificity, which stages were LLM-graded and what validation each grader received — **L2/L3 where the firm states it; L1 where the scale is disclosed but the grader validation is not**.
- **Worked example — evaluation-harness grader change, 2 September 2026 (UK AISI, `inspect_ai` CHANGELOG, release "0.3.262 (02 September 2026)", first item, flagged breaking).** Model-graded scorers with a panel of graders now require a strict majority: "samples with no majority grade (even-split ties, three-way splits, or ties after a grader returns no parseable grade) come back unscored" and leave the metric denominator, rather than the most common grade winning with ties broken by grader order. This is a live instance of the provider/tool-side scoring change this canvas's version-pinning control exists to catch, and it supplies a named, tool-implemented compensating control — grader-panel strict majority rather than order-based tie-break. Expected evidence: the firm's pinned harness version, and a re-baseline of any score compared across the v0.3.261 → v0.3.262 boundary (both numerator and denominator change) — **L3**.
- **Dated worked example, added at the September 2026 refresh — what AI-delegated analysis cost a published independent investigation.** In the one published independent investigation of an evaluation-containment incident, the investigators record that they "had to heavily delegate our analysis to AI agents; these agents had significantly worse judgment and reliability than human researchers", and that "it was challenging to spot check their work"; they further record that "a small amount of communication and activity related to this attack was not captured in the datasets we used for our final analysis", the preceding sentence stating that "that agent activity can itself modify or delete relevant data" [METR, *Brief independent investigation of agents' behavior, reasoning and collaboration in the OpenAI / Hugging Face hacking incident*, 26 August 2026, §"Limitations due to the scale and complexity of this incident"]. The bearing on this IRQ is direct and uncomfortable: where a firm's own evaluation evidence is produced with model assistance at scale, the limitation the investigators state of themselves is the limitation a reviewer must assume of the firm — and it is a limitation of **judgement and reliability relative to a human rater**, which is precisely what §11's human-agreement study measures. A firm that has not measured it has not established it.

## 11. Independent Test
> In a non-production environment, take a representative sample of the firm's judge-scored outputs (the outputs the judge is used to evaluate, not production customer data) and have human raters independently re-score the same sample using the same criteria; compute agreement between judge and human verdicts. Where more than one human rater is used, compute and report inter-rater agreement among the raters themselves alongside the judge/human figure, as the interpretive floor for it. Construct order-swapped subsets (identical candidate pair, presentation order reversed) to test for position bias, and length-matched subsets (verbosity controlled) to test for verbosity bias. Where the judge model and the system under assessment share a model family, either substitute a cross-family judge on a subsample or apply a human spot-check to that subsample and compare results. Record the judge model's pinned version alongside all results. Executed entirely on synthetic/anonymised or historical non-live data in staging. Methodology follows Zheng et al. (2023); **no FAIAS-standard acceptance threshold exists for judge/human agreement or bias-probe results — stated, not implied.** — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, peer-reviewed and widely-cited evaluation methodology exists with a defined bias taxonomy and human-agreement validation approach; no agreed industry or FAIAS-standard acceptance threshold exists, so pass/fail judgement on the measured results remains a professional-judgement call).

## 12. Pass Indicators
- Human-agreement study shows the judge's verdicts align with human raters at a rate the firm has documented and approved as its own threshold.
- Where more than one human rater is used, inter-rater agreement among them is reported and is sufficient to make the judge/human comparison interpretable.
- Order-swap and length-matched bias-probe testing shows no material position or verbosity bias in the judge's verdicts.
- Judge model version is pinned and recorded; any provider-side update to the judge triggered and completed re-validation before continued reliance.
- Where judge and assessed system share a model family, a compensating cross-family or human-spot-check step has been applied and shows no material correlated-error divergence.

## 13. Fail Indicators
- No human-agreement study has been performed; judge verdicts are relied upon as evaluation evidence with no independent corroboration.
- Judge/human agreement is reported with no corresponding inter-rater agreement among the human raters, so the reliability of the comparison's own reference standard is unknown.
- Order-swap or length-matched testing reveals material position or verbosity bias in judge verdicts.
- Judge model version is unpinned, or a provider-side judge update occurred with no re-validation, so evaluation evidence is no longer comparable over time without anyone having noticed.
- Judge and assessed system share a model family with no compensating step, and no correlated-error assessment has been performed.

## 14. Reporting Language
**Pass:** "The LLM judge used to generate this system's evaluation evidence has been independently validated: a human-agreement study, position- and verbosity-bias probes, and a correlated-error check (given shared model family) were performed, with results meeting the firm's own documented threshold. Judge version is pinned and re-validation is triggered on change. Conclusions rest on ★3 methodology — a credible, peer-reviewed evaluation approach with no agreed acceptance threshold, requiring the firm's own documented tolerance."

**Fail:** "The evaluation evidence for this system rests on an LLM judge that has not been independently validated: no human-agreement study exists, and bias-probe testing was not performed. [Where performed:] Independent testing found [material/no] position or verbosity bias, and judge/human agreement of [x]%, with no documented threshold against which to judge sufficiency. This is a foundational evidence-integrity gap: every downstream conclusion drawn from this evaluation evidence is unsupported until the judge itself is validated."

**Partial:** "A human-agreement study exists for [evaluation use case A] but the same judge is relied upon for [use case B] without equivalent bias-probe testing or correlated-error assessment. The assurance objective is not met for use case B pending equivalent validation."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (unsound evaluation evidence can underpin an unsound approval or monitoring
              decision for any system the judge assesses; regulatory notice risk if the
              gap is discovered externally)
  Likelihood: 2 (human-agreement study, bias-probe testing and version pinning should catch
              material judge unreliability before or shortly after adoption)
  Detectability: 2 (a defined, published methodology exists (Zheng et al.) and surfaces the
              issue directly when applied)
  Recoverability: 2 (re-validation of the judge and, where needed, re-scoring of affected
              evaluation evidence is a defined, resourced process)
  Novelty: 4 (treating a second AI system as neutral evaluation infrastructure, rather than
              as a system with its own bias classes requiring validation, is an assumption
              essentially unknown outside AI-evaluation research)

Interpretation: acceptable residual risk with human-agreement, bias-probe and version-pinning
controls in place; highest concern is Novelty, since the judge's fluency and apparent
objectivity are maximally reassuring on their face.

If controls are absent or degraded:
  Severity: 4 (the firm's evaluation evidence base for any system assessed by the judge is
              unsound at source, with no bound on how many downstream conclusions are
              affected)
  Likelihood: 3 (documented bias classes are near-universal properties of current LLM judges
              absent specific mitigation, not a rare edge case)
  Detectability: 4 (invisible without a specialist human-agreement/bias-probe study; a
              confident, well-formatted judge verdict looks identical whether sound or
              biased)
  Recoverability: 3 (requires re-validating the judge and potentially re-running the affected
              evaluation programme retrospectively)
  Novelty: 4
Residual risk: High to Critical depending on the materiality of the systems approved or
monitored on the strength of the unvalidated judge's output.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unsound evaluation evidence can underpin unsound approval or monitoring decisions across every system the judge assesses. |
| **Likelihood** | 3 | Documented bias classes (position, verbosity, self-enhancement) are near-universal properties of LLM judges absent specific mitigation. |
| **Detectability** | 4 | A confident, fluent judge verdict looks identical whether sound or biased; only a specialist human-agreement/bias-probe study reveals the difference. |
| **Recoverability** | 2 | Once identified, judge re-validation and re-scoring of affected evaluation evidence is a defined, resourced process. |
| **Novelty** | 4 | Treating a second AI system as neutral evaluation infrastructure rather than as a system requiring its own validation is an assumption specific to AI-evaluation practice, unfamiliar to traditional model risk review. |

## 17. Regulatory Basis
> [PRA SS1/23, May 2023, effective 17 May 2024, Principle 4 (independent model validation) — validation must be performed by a party independent of development, using evidence adequate to the model's risk] — directly engaged where the "independent" evidence is itself generated by an unvalidated AI judge. No regulation names "LLM-as-judge validation" explicitly; this IRQ operationalises SS1/23's independent-validation principle for an evidence-integrity failure specific to using a language model as an evaluator. (verified 31 Jul 2026)

## 18. Research Basis
> [Zheng, L., Chiang, W-L., Sheng, Y., et al., 2023, "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena", arXiv:2306.05685, **NeurIPS 2023 Datasets and Benchmarks Track**] — the primary anchor for this IRQ: identifies and empirically demonstrates position bias, verbosity bias and self-enhancement bias in LLM judges, and validates a human-agreement methodology (comparing judge verdicts to human preference labels) as the corrective approach. **No FAIAS-standard acceptance threshold exists for judge/human agreement or for the magnitude of tolerable bias — stated, not implied; the paper supplies a measurement method, not a pass/fail bar.**
>
> **Construct-validity addition (v1.2.0) — the anchor is directly contested.** [Chen, J., Chen, W., Lin, Z., Vong, C.M., 2026, "A Judge Should Know What Changed: Construct Validity for LLM-as-a-Judge Evaluation", arXiv:2608.24419, 25 August 2026; artefact availability stated in the paper at l.1294] formalises evaluator construct validity as a two-dimensional profile: "invariance S, the probability that a verdict is unchanged under construct-preserving edits, and construct sensitivity R, the probability that it changes under minimal construct-changing edits" [arXiv abstract page (listing), fetched 2026-09-12; this wording is the submitted abstract's and differs from the PDF's own abstract]. Across 7 judges and 4 domains the paper reports that "At matched invariance S ≥ 0.90 judges sit at S = 0.945 against R = 0.319" [PDF p.1] — a judge can be highly stable under surface perturbation while rarely changing its verdict when the thing being measured actually changes. The paper also audits the validation sets themselves and finds that a surface-only predictor "reproduces 55%–67% of their labels, including 67.4% of MT-Bench’s human votes" [PDF l.47]. **Why this is not merely corroborative:** Zheng et al. (2023) / MT-Bench is this IRQ's sole §18 and §20 anchor, and the order-swap and length-matched probes in §11 are precisely the "robustness to surface perturbations" the paper says is insufficient; §11 contains **no construct-sensitivity probe at all**. The missing R axis, and the standing of the validation set itself, are recorded here as an open question on the ★3 basis and on §11's completeness — **held for the owner's ruling; the ★3 rating and §11 are unchanged by this addition.**
>
> **Judge/human-agreement addition (v1.2.0).** [Baig, H., Joren, H., Benton, J., 2026, "TASTE", Anthropic Alignment Science, 28 August 2026] is a second, independent human-agreement measurement on a complex analytical-judgement task (92 proposal pairs): "Fable 5 achieves 60% whereas we estimate researcher performance at 77%", with two frontier models performing near chance. It is closer in kind to structured financial-services analytical review than MT-Bench's chatbot-response setting, and it corroborates rather than upgrades the Zheng et al. anchor. **Limits, stated:** single-lab benchmark; access by request; no public code or data release located; 77% is the benchmark's estimated human-agreement ceiling, not an independent human score on a settled scale.
>
> **Scope note (v1.2.0), stated not implied.** This IRQ is **not** broadened to deterministic-grader gaming. Its register question and its §11 procedure address a *language model used as judge or evaluator* and the bias classes documented for that case. A system under test reasoning about, and metagaming, a deterministic code-based grader is a different failure mode that §11 does not exercise; it is routed to IRQ-MOD-008 ("evaluator exploitation"). Inference-time metagaming of a deterministic grader is recorded as an **absence** in this battery rather than folded into this IRQ.
>
> **Research basis last reviewed:** 12 September 2026 · **review cadence:** Fast (6 months)
>
> **URO-5: Chen et al., "A Judge Should Know What Changed", arXiv:2608.24419v1, 25 August 2026 — whether §11's judge/human agreement limb is sufficient, given judges averaging S = 0.945 at R = 0.319, a direct challenge to Zheng et al. (2023), this canvas's sole anchor — resolve by 2027-03-11.** The ★3 above stands untouched while this observation is open (§6A.2).

## 19. Related IRQs
```
  - IRQ-GOV-007 (I.3: independent validation must use firm-relevant evidence; an unvalidated
    judge is a direct gap in that independence)
  - IRQ-DAT-003 (A.1: human annotator quality — the human-annotation counterpart of evaluator
    validity; no conflict, as DAT-003 addresses human raters and this IRQ addresses AI judges)
  - IRQ-MOD-011 (B.5: contaminated evaluation evidence — the same evidence-integrity concern
    applied to the benchmark rather than the evaluator; this IRQ is the evaluator-side twin)
  - IRQ-MOD-016 (B.5: external validity of the setting that produced the evaluation
    evidence — the setting-side member of the same family. Where a firm uses a
    language model to score its own traces for test-awareness indication, that
    judge's validity is this IRQ's question and not IRQ-MOD-016's)
```

## 20. References
```
[1] Zheng, L., Chiang, W-L., Sheng, Y., et al., 2023. "Judging LLM-as-a-Judge with MT-Bench
    and Chatbot Arena." NeurIPS 2023 Datasets and Benchmarks Track. arXiv:2306.05685.
[2] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.5 (Model domain, Distribution Shift & Evaluation Integrity)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): The judge model is naturally treated as neutral evaluation
  infrastructure rather than as an AI system with its own documented bias classes requiring
  independent validation.
✓ Test 2 (Plausible Harm): Grounded in Zheng et al. (2023), a widely-cited, peer-reviewed
  benchmark paper empirically demonstrating position, verbosity and self-enhancement bias in
  LLM judges.
✓ Test 3 (Testable): Fully testable in staging via human-agreement study, order-swap and
  length-matched bias probes, and correlated-error screening; no production data required.
✓ Test 4 (Decision-Relevant): Outcome determines whether the firm's own evaluation evidence
  — the basis for every downstream approval, monitoring and vendor-selection decision that
  relies on it — is sound.

Change Log:
- v1.0 (2026-08-01): Initial publication (v1.0.3 batch); four tests passed.
- v1.2.0 (2026-09-12): Field 10 — three dated worked examples added (Anthropic alignment assessment, 9 Sep 2026, the 481m/9.2m LLM-graded stage with the §Methods grader caveat correctly scoped to the analysis pipeline; UK AISI inspect_ai v0.3.262, 2 Sep 2026, strict-majority grader panel as a named compensating control; METR's independent investigation of the OpenAI/Hugging Face incident, 26 Aug 2026, on the cost of AI-delegated analysis — "significantly worse judgment and reliability than human researchers"). Field 18 — Chen, Chen, Lin & Vong (arXiv:2608.24419) added as a direct challenge to the Zheng et al. 2023 anchor (invariance/sensitivity profile; S = 0.945 against R = 0.319; 67.4% of MT-Bench's human votes reproduced by a surface-only predictor), and TASTE (28 Aug 2026) as a second human-agreement data point; scope note recorded that this IRQ is not broadened to deterministic-grader gaming. Fields 9, 11, 12 and 13 — inter-rater agreement among the human raters added as an expected control, as a step in the independent test, and as a pass and a fail indicator, so that the reference standard against which the judge is compared is itself reported. Related IRQs — the reciprocal entry to IRQ-MOD-016 added. ★3 unchanged; the ★ basis and the absence of a construct-sensitivity probe in §11 are open questions held for the owner.
- v1.2.1 (2026-09-19): Field 10 — erratum. The METR worked example called its fourth quotation the fuller sentence of the third; the quoted words end the sentence before it, and it now says so. ★3 unchanged.
```

---
---

