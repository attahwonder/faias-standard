# CANVAS: IRQ-MOD-011

## 1. IRQ ID & Title
**IRQ-MOD-011: Contaminated Evaluation Evidence Underpinning Model Approval**

Register question: "Could the evaluation evidence supporting approval be contaminated — benchmark items present in training data, or vendor-reported scores on leaked public benchmarks?"

## 2. Business Activities Affected
- **Any AI-assisted lending, AML or claims decision approved on the strength of a capability benchmark:** If the approval evidence rests on a contaminated benchmark, every downstream reliance on "the model was validated to X% accuracy" is unsound.
- **Model selection/procurement:** Choosing between competing vendor models based on public leaderboard performance is directly undermined if those scores reflect benchmark leakage rather than genuine capability.
- **Ongoing governance reporting:** Board/committee papers citing a capability score as evidence of safety inherit the contamination risk silently.

## 3. AI Behaviour(s)
- Performs well on evaluation items that were present, in whole or in near-duplicate form, within its training data — appearing to demonstrate genuine capability while actually demonstrating memorisation.
- Vendor-reported scores are typically obtained on public benchmarks whose test items may have entered the training corpus of that or a related model, without the vendor necessarily being aware.
- Performance on a contaminated benchmark and a genuinely held-out, firm-relevant test can diverge sharply.

## 4. Failure Mode
> The evaluation evidence used to approve the model for deployment is contaminated — benchmark items were present in the model's training data or the vendor-reported score derives from a leaked public benchmark — so the approval decision rests on a capability claim that has not actually been demonstrated on held-out, firm-relevant data.

## 5. Potential Consequences
- **Customer:** Reliance on a model approved for a capability level it does not actually possess in the firm's real task context, leading to wrong decisions the approval process believed it had ruled out.
- **Institution:** The entire model risk approval record for the system is unsound if it traces back to contaminated evidence; retrospective re-approval is required once discovered.
- **Regulator/market:** A supervisory finding that "independent validation" in fact relied on vendor or public benchmark claims that were never checked for contamination — a direct SS1/23 independent-validation failure.

## 6. Failure Chain
```
Vendor reports a capability/safety benchmark score, or an internal team cites a
public benchmark result, as evidence for approval
  ↓ (IRQ-MOD-011 — THIS IRQ: no contamination check performed on the benchmark or the
     model's training-data relationship to it)
Benchmark items were in fact present (or near-duplicated) in the model's training
corpus, inflating the reported score relative to genuine capability
  ↓ (IRQ-GOV-007: independent validation accepts the vendor/public score without an
     independent, firm-relevant, held-out test)
Model is approved for deployment on the strength of the inflated score
  ↓ (IRQ-MOD-004/IRQ-MOD-010: hallucination rate and shift robustness were never
     separately, genuinely measured because the contaminated score was treated as sufficient)
Model underperforms in production relative to the approval basis
  ↓
Wrong decisions accumulate; retrospective discovery that the approval evidence was
contaminated → governance finding that the entire approval chain must be re-run

Control Breakpoints:
  • IRQ-GOV-007: independent validation uses firm-relevant, held-out evaluations, not vendor/
    public benchmark claims alone
  • IRQ-MOD-011: explicit contamination-detection testing (e.g. guided-prompting probes,
    temporally-fresh benchmark construction) before approval
  • IRQ-MOD-004: hallucination/accuracy re-measured on genuinely held-out, firm-relevant data
  • IRQ-GOV-009: documentation records the contamination check performed and its result
```

## 7. Why a Domain Expert May Miss It
- FS SMEs are accustomed to trusting published performance figures (credit-bureau scorecards, actuarial tables) that are not vulnerable to this failure mode; the idea that a benchmark score can be inflated because the model "saw the answers during training" is specific to how LLMs are trained on scraped internet-scale corpora.
- A high, well-publicised benchmark score is reassuring and often used directly in board papers as evidence of safety — the incentive to interrogate it further is weak, especially where the vendor is a reputable frontier lab.
- Contamination detection is a specialist technical exercise (guided-prompting, temporal analysis, near-duplicate detection) unfamiliar to model risk teams whose training is in statistical/credit-risk model validation, not LLM evaluation methodology.
- Public benchmarks are widely treated as a neutral "ground truth" for capability; the fact that widely-used benchmarks (e.g. GSM8K) have been shown to be substantially contaminated in frontier models is not widely known outside AI research circles.

## 8. Assurance Objective
**AO-MOD-011:** Approval shall rely on held-out, contamination-checked, firm-relevant evaluation evidence; vendor-reported or public-benchmark scores shall not be accepted as sufficient evidence of capability or safety without an independent contamination check and, where feasible, corroboration on genuinely held-out firm-relevant data.

## 9. Expected Controls (Traced)
- **Contamination detection on cited benchmarks** — [Sainz et al., 2023, "NLP Evaluation in Trouble: On the Need to Measure LLM Data Contamination for Each Benchmark", arXiv:2310.18018; Golchin & Surdeanu, 2023, "Time Travel in LLMs: Tracing Data Contamination in Large Language Models", arXiv:2308.08493] — guided-prompting or similar probes applied to any benchmark cited in the approval papers, to test whether the model shows evidence of having memorised specific items.
- **Temporally-fresh or continuously-refreshed benchmark use where available** — [White et al., 2024, "LiveBench: A Challenging, Contamination-Free LLM Benchmark", arXiv:2406.19314] — preferring evaluation sources designed to resist contamination by construction.
- **Independent, firm-relevant, held-out evaluation** — [linked IRQ-GOV-007; PRA SS1/23 independent-validation principle] — the firm constructs or commissions test items drawn from its own task domain, verified not to overlap with any publicly scraped or vendor-provided data.
- **Caution on leaderboard-based model selection** — [Singh et al., 2025, "The Leaderboard Illusion", arXiv:2504.20879; Cohere/C4AI, "Elo Uncovered", arXiv:2311.17295] — public leaderboard rankings are treated as directional signal only, not sufficient approval evidence, given documented instability and asymmetric testing access.
- **Documentation of the contamination check and its outcome** — [linked IRQ-GOV-009] — the approval record explicitly states what contamination testing was performed and what it found, rather than citing the raw benchmark score alone.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor-reported benchmark score cited in the approval paper with no contamination check — **L1** (assertion only; flag explicitly as unverified).
- Documentation of the contamination-detection methodology applied (guided-prompting, temporal analysis) and its result — **L2**.
- Staging test results: independent, firm-relevant held-out evaluation performed alongside or instead of the cited benchmark, with results compared — **L3**.
- Independent validation report explicitly addressing contamination risk in the approval evidence — **L4**.
- Historical record of a contamination check that changed an approval decision or triggered re-testing — **L5**.

## 11. Independent Test
> In a non-production environment, take the specific benchmark(s) cited in the model's approval papers and apply a guided-prompting contamination probe: prompt the model to complete a benchmark item given only a partial excerpt, and measure whether it reproduces the exact remainder at a rate exceeding chance (indicating memorisation) versus a comparably-structured but demonstrably novel item. Separately, construct or source a small held-out, firm-relevant test set (e.g. from internal historical case files, verified not to be publicly scraped) covering the same claimed capability, and compare performance against the cited benchmark score. Methodology per Sainz et al. (2023) and Golchin & Surdeanu (2023); comparator evidence from Zhang et al., 2024, GSM1k, arXiv:2405.00332, showing material score drops on decontaminated recreations of a widely-used benchmark. Executed entirely with non-production API calls and internal historical data. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, peer-reviewed contamination-detection methods exist with growing consensus; no single canonical contamination test applies universally across all benchmark types, so method selection and threshold-setting require professional judgement).

## 12. Pass Indicators
- Contamination probes on cited benchmarks show no material evidence of memorisation (reproduction rate at or near chance for held-out comparators).
- Approval evidence includes at least one independent, firm-relevant, held-out evaluation corroborating the cited benchmark's implied capability level.
- Documentation explicitly records the contamination check performed and its result, rather than citing the raw score alone.
- Where a contamination risk was identified, the approval decision was revisited and re-tested, not carried forward unchanged.

## 13. Fail Indicators
- Approval papers cite a vendor or public benchmark score with no contamination check of any kind.
- Guided-prompting or similar probes show material evidence of memorisation on the cited benchmark.
- Independent, firm-relevant held-out testing (where performed) shows materially lower performance than the cited benchmark score, with no reconciliation or re-approval.
- Model selection decisions rely on public leaderboard position alone, with no independent corroboration.

## 14. Reporting Language
**Pass:** "The benchmark(s) cited in this model's approval papers have been tested for contamination using guided-prompting probes, with no material evidence of memorisation; an independent, firm-relevant held-out evaluation corroborates the claimed capability level. Conclusions rest on ★3 methodology — credible, growing-consensus contamination-detection methods, professional-judgement-led threshold-setting — and should be repeated for any benchmark cited in future re-approvals."

**Fail:** "The model's approval rested solely on a vendor-reported benchmark score with no contamination check. Independent testing found [material/no] evidence of memorisation on that benchmark, and an independent held-out evaluation on firm-relevant data produced a materially lower result than the cited score ([x]% vs [y]%). The original approval basis is unsound; re-approval using contamination-checked, firm-relevant evaluation evidence is required before continued reliance."

**Partial:** "A contamination check has been performed on the primary benchmark cited for [capability A] but not for a second benchmark cited for [capability B] used in the same approval paper. The assurance objective is not fully met; the outstanding benchmark should be checked before the approval is treated as complete."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (an unsound approval basis for a system used in material FS decisions;
              regulatory notice risk if discovered by a supervisor rather than the firm)
  Likelihood: 2 (contamination checking and independent held-out evaluation should catch
              the issue before or shortly after approval)
  Detectability: 2 (guided-prompting probes and held-out comparison are a defined, if
              specialist, test that surfaces the issue directly when performed)
  Recoverability: 2 (re-approval using corrected evidence is a defined, resourced process)
  Novelty: 4 (that a benchmark score can be inflated by training-data memorisation, rather
              than reflecting genuine capability, is a mechanism essentially unknown outside
              AI research and very likely to be missed by a traditional model risk reviewer)

Interpretation: acceptable residual risk with contamination checking embedded in the approval
process; highest concern is Novelty, since the failure mode is invisible without a specialist
probe and a high benchmark score is maximally reassuring on its face.

If controls are absent or degraded:
  Severity: 3 (the firm's approval record for a material FS system is built on unverified,
              potentially inflated evidence, though the model may still perform adequately
              in practice — severity is bounded by whether contamination in fact occurred)
  Likelihood: 3 (documented that widely-used public benchmarks show material contamination
              in frontier models; likelihood of some contamination is high where public
              benchmarks are cited without checking)
  Detectability: 4 (invisible without a specialist contamination probe; a high score looks
              identical whether genuine or memorised)
  Recoverability: 3 (requires re-running the entire approval evidence base with
              contamination-checked, firm-relevant evaluations)
  Novelty: 4
Residual risk: High to Critical depending on the materiality of the system approved on the
contaminated evidence.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | An unsound approval basis undermines the entire governance record for a system used in material FS decisions; regulatory notice risk if discovered externally. |
| **Likelihood** | 3 | Documented, material contamination exists in widely-used public benchmarks for frontier models; likelihood is high wherever such benchmarks are cited without an independent check. |
| **Detectability** | 4 | A high benchmark score looks identical whether it reflects genuine capability or training-data memorisation; only a specialist contamination probe reveals the difference. |
| **Recoverability** | 2 | Once identified, re-approval using contamination-checked, firm-relevant evaluation evidence is a defined and resourced process. |
| **Novelty** | 4 | Benchmark contamination via training-data memorisation is a mechanism specific to how LLMs are trained on scraped corpora, essentially unknown to traditional model risk practice. |

## 17. Regulatory Basis
> [PRA SS1/23, May 2023, effective 17 May 2024, Principle 4 (independent model validation) — validation must be performed by a party independent of development, using evidence adequate to the model's risk] — directly engaged: reliance on unchecked vendor/public benchmark claims fails the independence and adequacy test. [FCA, AI Update, Apr 2024] — signals that AI risk is assessed through existing governance and validation frameworks, which this IRQ interprets to require contamination-aware evaluation practice. No regulation names "benchmark contamination" explicitly; this IRQ operationalises SS1/23's independent-validation principle for an LLM-specific evidence-integrity failure. (verified 29 Jul 2026)

## 18. Research Basis
> [Sainz, O., et al., 2023, "NLP Evaluation in Trouble: On the Need to Measure LLM Data Contamination for Each Benchmark", EMNLP Findings, arXiv:2310.18018] — names and documents the contamination problem for the LLM era. [Golchin, S., Surdeanu, M., 2023, "Time Travel in LLMs: Tracing Data Contamination in Large Language Models", arXiv:2308.08493] — practical guided-prompting contamination-detection technique used in this IRQ's independent test. [Zhang, H., et al. (Scale AI), 2024, "A Careful Examination of Large Language Model Performance on Grade School Arithmetic" (GSM1k), arXiv:2405.00332] — hard empirical evidence of accuracy drops of up to 13% (arXiv v1; up to 8% in v4) on an uncontaminated recreation of a widely-cited benchmark. [White, C., et al., 2024, "LiveBench: A Challenging, Contamination-Free LLM Benchmark", arXiv:2406.19314] — a continuously-refreshed benchmark design resisting contamination by construction. [Singh, S., et al., 2025, "The Leaderboard Illusion", arXiv:2504.20879] — documents private testing/data asymmetries distorting public leaderboard rankings such as Chatbot Arena.
>
> **Structural-prevention addition (v1.2.0) — a published protocol, not yet an adopted one.** [Google DeepMind, "Piloting the world's first double-blind AI evaluations", 27 August 2026, with MLCommons, "The key to trustworthy AI evaluation is secrecy by design"; technical report published] describes a confidential-computing protocol in which "the evaluator cannot see the Gemini model weights, and Google cannot see the evaluator’s test prompts", implemented using Confidential Space within Google Cloud's confidential-computing portfolio. Every contamination control in §9 above detects or avoids contamination after or around the fact; this prevents it by construction, and is therefore a distinct control category rather than a further instance of the existing ones. Partners named at the primary: the Singapore AI Safety Institute, OpenMined, AVERI and MLCommons, with AVERI as the auditor and MLCommons as the instrument maker. MLCommons states it provided "a reserved subset of the AILuminate™ safety benchmark prompts … ensuring that no GDM model had ever been exposed to this specific evaluation set before", and calls the exercise a proof of concept. **Limits, stated, and they are why nothing moves:** one joint pilot rather than adoption of the same method by unconnected parties; one relatively small model (Gemini Flash Lite); a non-financial-services benchmark; and the technical report itself unfetched at the date of this entry. **★3 is unchanged and any upgrade is held pending a second independent adopter or a financial-services pilot.**
>
> **Evaluation-awareness addition (v1.2.0) — a second, non-contamination route to the same invalid conclusion.** [Heidari, Memarian & Rabusseau, 2026, "Evaluation Awareness in Language Models: Representation, Verbalization, and Control", arXiv:2608.21766, 22 August 2026; code release stated in the printed abstract] reports that "evaluation awareness is linearly decodable from the residual streams of every model (best AUROC ≥ 0.7)" across six models, only partly aligned with what the model verbalises, causally steerable, present already in base models and amplified through supervised fine-tuning. **Why it is recorded against this canvas's construct:** contamination invalidates evaluation evidence because the model has seen the *items*; evaluation awareness can invalidate it without the model having seen anything, because the model conditions its behaviour on recognising the *setting*. A contamination probe — guided prompting, temporal analysis, a held-out firm-relevant set — will not detect it, so a clean contamination result is not a finding of sound evaluation evidence. **Limits, stated:** a white-box method requiring activation access, which a deployer reviewing a hosted model does not have; a single arXiv preprint, not peer-reviewed; six general-capability models with no financial-services setting. **No ★ or severity change arises; the boundary between this canvas and the new evaluation-validity question is set by the owner's ruling on deliberate gap 2, not here.**
>
> **Research basis last reviewed:** 12 September 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-MOD-004 (B.2: hallucination rate must be measured on genuinely held-out,
    firm-relevant data, not a contaminated benchmark)
  - IRQ-MOD-010 (B.5: distribution-shift robustness assessment depends on the same
    evidence-integrity discipline)
  - IRQ-GOV-007 (I.3: independent validation must use firm-relevant evaluations rather than
    vendor/public benchmark claims — the governance-side counterpart of this IRQ)
  - IRQ-TPR-001 (F.1: provider due diligence should include scrutiny of vendor-reported
    safety evaluation claims)
  - IRQ-MOD-012 (B.5: model collapse from recursive synthetic data — a related evaluation/
    training-data-integrity concern)
  - IRQ-MOD-016 (B.5: external validity of the evaluation setting — the adjacent
    evidence-integrity question. This IRQ asks what the evidence contains;
    IRQ-MOD-016 asks what setting produced it. A publisher treating
    evaluation-aware behaviour as equivalent to a contaminated evaluation is
    why the two are cross-linked rather than merged)
```

## 20. References
```
[1] Sainz, O., Campos, J.A., García-Ferrero, I., et al., 2023. "NLP Evaluation in Trouble:
    On the Need to Measure LLM Data Contamination for Each Benchmark." EMNLP Findings 2023.
    arXiv:2310.18018.
[2] Golchin, S., Surdeanu, M., 2023. "Time Travel in LLMs: Tracing Data Contamination in
    Large Language Models." arXiv:2308.08493.
[3] Zhang, H., et al. (Scale AI), 2024. "A Careful Examination of Large Language Model
    Performance on Grade School Arithmetic." arXiv:2405.00332.
[4] White, C., Dooley, S., Roberts, M., et al., 2024. "LiveBench: A Challenging,
    Contamination-Free LLM Benchmark." arXiv:2406.19314.
[5] Singh, S., et al., 2025. "The Leaderboard Illusion." arXiv:2504.20879.
[6] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[7] FCA, 2024. "AI Update." April 2024.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.5 (Model domain, Distribution Shift & Evaluation Integrity)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional model risk practice trusts published performance
  figures; that a benchmark score can be inflated by training-data memorisation is a
  mechanism specific to LLM training on scraped corpora, unknown outside AI research.
✓ Test 2 (Plausible Harm): Grounded in peer-reviewed contamination research (Sainz et al.,
  Golchin & Surdeanu) with hard empirical evidence of score inflation (Zhang et al., GSM1k)
  and leaderboard distortion (Singh et al.).
✓ Test 3 (Testable): Fully testable via guided-prompting probes and held-out comparison using
  non-production API calls; no production data required.
✓ Test 4 (Decision-Relevant): Outcome directly determines whether the model's original
  approval basis is sound or requires re-approval.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-12): Field 18 — the DeepMind–MLCommons confidential-computing double-blind evaluation protocol (27 Aug 2026) added as a structural-prevention control category distinct from the detect-and-avoid controls in §9, with its limits stated (one non-FS pilot, one small model, technical report unreached) and ★3 held pending a second independent adopter; and arXiv:2608.21766 (Heidari, Memarian & Rabusseau, 22 Aug 2026, code release stated in the printed abstract) added as a second, non-contamination route to invalid evaluation evidence, with its white-box access limit stated. Related IRQs — the reciprocal entry to IRQ-MOD-016 added, separating the two questions: this IRQ asks whether the evaluation result is trustworthy, IRQ-MOD-016 asks what setting produced it. ★3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

