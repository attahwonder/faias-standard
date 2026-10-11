# TP-MOD-014 — Pinned-Configuration Decision-Flip Rate and Extraction-Layer Isolation Testing

**Procedure ID:** TP-MOD-014
**IRQ:** IRQ-MOD-014 — Unmeasured Decision-Flip Rate Under Materially Identical Inputs at Pinned Configuration
**Assurance objective:** AO-MOD-014 — run-to-run and near-identical-input decision stability shall be measured at pinned model configuration, held within a defined and documented tolerance, and the decision-extraction logic that converts model output into a decision shall be validated independently of the underlying generation.
**★ Confidence:** ★2 (carried from canvas — see canvas §11. Summary: the underlying phenomenon — stochastic sampling instability and extraction-layer brittleness — is well understood mechanically, and two published methods, both workshop papers, cover the repeat-run limb only; no FS-specific published method, benchmark or precedent was located for the extraction-layer or perturbation limbs, or for bounding the flip rate against a governance-approved tolerance; test design rests largely on tester judgement. Field-maturity caveat carried with the rating: **the phenomenon is documented; two published methods cover the repeat-run limb, and no FS-specific assurance methodology was located for the other limbs — this ★2 reflects that gap directly, not a defect in test execution.**)
**Method classification:** Emerging Practice / bespoke. The canvas records two published repeat-run methods, both workshop papers (Atıl et al., 2025; Khatchadourian and Franco, 2025), for the repeat-run limb only, with their limits. No FS-specific published method was located for testing decision-extraction logic independently of generation or for immaterial-perturbation testing; no published method, peer-reviewed methodology, published incident analysis or FS-specific assurance precedent was located for bounding decision-flip rate against a governance-approved tolerance; and no anchor is manufactured to fill the gap. Two of the five expected controls — the pinned-configuration repeat-run protocol and the decision-extraction component test — are marked Emerging Practice in the canvas's own control list. Test design, sample size and tolerance-setting are bespoke and professional-judgement-led.

## Preconditions

- **Applicability confirmed at scoping, not assumed.** The canvas records applicability as Y / Y / N: predictive-stack applicability is **N by default**, because a fixed classical or statistical model is deterministic at inference, and flips to **Y** where a predictive stack itself samples at inference (randomised subsampling, ensemble sampling). The reviewer records the determination and its basis before the procedure runs.
- **Environment:** staging replica of the full deployed pipeline — prompt templates, model endpoint and the decision-extraction layer (parsing, classification, schema validation) — **not a bare model endpoint**; the extraction layer is half the object of study. Executed entirely on synthetic, anonymised or historical non-live case data approved for test use. No production traffic, no live customer data, no production retraining or configuration change.
- **Access needed:** the ability to pin and hold model version, prompt and system configuration, and decoding parameters (temperature, top-p, top-k, seed where available) across a run series; the extraction layer's code or configuration, and the ability to hold a generated output fixed and feed it to the extraction layer independently; historical change records for model, prompt and configuration.
- **Artefacts requested in advance (2 weeks):** the documented decoding configuration as deployed; the decision-extraction logic and any specification of it; any existing repeat-run or stability test results, with the documented protocol and sample size where they exist; the governance-approved tolerance for decision-flip rate on consequential decisions, or confirmation that none exists; the independent validation report covering stability, where one exists; change-control records for the review period; production logging of near-duplicate case resubmissions (for example, retried requests) where retained.
- **Personnel:** reviewer (lead); platform or ML engineer to pin configuration and run the repetition series; **the owner of the decision-extraction component**, who is frequently not the model owner and is often not identified until asked; the governance owner able to confirm whether a flip-rate tolerance has ever been approved.

## Test design

- **Three distinct tests, deliberately not blended.** The canvas requires generation-level and extraction-level contributions to instability to be separately measurable; a single blended flip rate does not satisfy the assurance objective and cannot support attribution.
  1. **Full-pipeline repeat-run.** A representative sample of consequential inputs is run n times at pinned model version, prompt and system configuration, and decoding parameters. The **discrete decision produced by the full pipeline including extraction logic** is recorded per run and the flip rate computed. This figure is the blended rate — it is not yet attributable.
  2. **Extraction-only isolation.** A fixed generated output is held constant and only extraction-layer inputs are varied — edge-case phrasing, formatting — to isolate the extraction layer's own contribution to instability, independent of generation.
  3. **Immaterial-input perturbation.** Inputs that should be decision-irrelevant — whitespace, field ordering, non-substantive rounding — are varied on a further sample and decision stability measured.
- **Sample and repetition count.** The canvas states plainly that **no standard sample size exists**; n is sized to the tester's judgement, and the size and its rationale are fixed and recorded before execution. The consequential-decision sample is drawn to be representative of the decision types the system actually makes, not of the easiest cases to run.
- **Tolerance.** The threshold is the firm's own governance-approved maximum acceptable flip rate for consequential decisions (linked IRQ-GOV-006 risk appetite, per the canvas). FAIAS sets no figure. Where no tolerance exists, that absence is a canvas fail condition in its own right, distinct from any measured rate, and both are reported. The reviewer does not invent one.
- **Configuration discipline.** The pinned configuration is recorded before the first run and held fixed throughout. Any change mid-procedure invalidates the measurement; re-pin and restart.
- **Benign-payload principles:** not applicable. The governing safety rule is the domain's determinism discipline — record the decoding configuration for every run and hold it fixed within a test. Failing to do so makes the result uninterpretable and is the domain's most common source of wasted execution.

## Steps

1. Confirm and record the applicability determination, including the predictive-stack exception check where a nominally predictive component samples at inference. **Record:** the determination and its basis.
2. Obtain the documented decoding configuration and pin it. **Record:** model version, prompt and system-configuration identifiers, temperature, top-p, top-k, seed availability, and the repetition count n with the reasoning for it.
3. Establish whether any repeat-run testing has ever been performed. **Record:** the evidence, or the fact that stability is asserted rather than measured.
4. Obtain the governance-approved flip-rate tolerance. **Record:** the tolerance and its approval route, or its documented absence.
5. Draw and record the representative consequential-input sample. **Record:** the sampling basis and the decision types covered, fixed before any run.
6. Execute the full-pipeline repeat-run series. **Record:** the discrete decision per run per input, and the computed full-pipeline flip rate.
7. Execute the extraction-only isolation test on a fixed generated output. **Record:** extraction-layer flips under varied edge-case phrasing and formatting.
8. Decompose the measured flip rate into generation-level and extraction-level contribution. **Record:** the decomposition — an undecomposed rate does not meet the assurance objective, and flips otherwise cannot be attributed.
9. Execute the immaterial-perturbation series on a further sample. **Record:** decision changes arising from whitespace, field ordering and non-substantive rounding, and the rate at which they occur, per perturbation class.
10. Compare all three measured rates against the governance-approved tolerance where one exists. **Record:** the comparison, or the fact that no tolerance exists against which to judge the result.
11. Establish whether repeat-run testing is repeated after material model, prompt or configuration change, or was treated as a one-off approval artefact. **Record:** the change-triggered retest policy and the change records evidencing it operating.
12. Where retained, compare production logs for near-duplicate case resubmissions against the staging-measured flip rate. **Record:** the comparison, or the fact that resubmission logging does not permit it.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Full-pipeline decision-flip rate at pinned configuration on consequential inputs | At or below the **governance-approved tolerance** (canvas pass indicator). FAIAS sets no figure; where no tolerance exists, the absence is itself a canvas fail indicator and the reviewer does not set one | Canvas; linked IRQ-GOV-006 per canvas |
| Extraction-layer contribution to the flip rate | Separately measured, and not the dominant source of instability — or itself remediated, for example by deterministic parsing or schema validation with fallback (canvas pass indicator) | Canvas |
| Decision change under immaterial input perturbation (whitespace, field order, non-substantive rounding) | **No material decision change** (canvas pass indicator); materiality is **reviewer judgement — no established threshold** | Canvas |
| Repeat-run testing repeated after material model, prompt or configuration change | Repeated, not treated as a one-off approval artefact (canvas pass indicator) | Canvas |
| Attribution of flips to generation versus extraction | Attributable. Where extraction has never been tested independently of generation, flips cannot be attributed and this is a canvas fail indicator regardless of the measured rate | Canvas |
| Resubmission monitoring against the staging-measured rate | Compared where production resubmission logging exists | Canvas evidence level L5 |

## Interpretation

- **Pass** — the measured flip rate at pinned configuration is at or below the governance-approved tolerance for consequential decisions; the extraction-layer contribution is separately measured and is not the dominant source of instability, or has itself been remediated; immaterial-perturbation testing shows no material decision change; and repeat-run testing is repeated on material model, prompt or configuration change rather than held as a one-off approval artefact.
- **Fail** — no repeat-run testing has ever been performed and stability is asserted rather than measured; **or** the measured flip rate on consequential decisions is non-trivial and no governance-approved tolerance exists against which to judge it; **or** extraction logic has never been tested independently of generation, so flips cannot be attributed; **or** immaterial input perturbation changes the decision at a material rate.
- **Partial** — the canvas's own shape: repeat-run flip-rate testing has been performed for one use case but not for another sharing the same underlying model and configuration. The assurance objective is not met for the untested use case, and deployment should be reported as supported only for the measured ones pending equivalent testing.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Vendor or developer assertion that the system is "reliable" or "consistent", with no repeat-run evidence | **L1** (assertion only; flag) |
| Design documentation defining the repeat-run protocol, sample size and the tolerance threshold to be applied | L2 |
| Applicability determination record, including the predictive-stack exception check | L2 |
| Pinned-configuration record: versions, decoding parameters, repetition count and its basis | L3 |
| Staging test results: flip rate across n repeat runs on a representative consequential sample at pinned configuration, **decomposed into generation-level and extraction-level contribution** | **L3** |
| Extraction-only isolation results on a held-constant generated output | L3 |
| Immaterial-perturbation stability results | L3 |
| Independent validation report assessing the repeat-run methodology and findings, performed by a function independent of development | **L4** |
| Production monitoring data comparing logged outcomes for near-duplicate case resubmissions against the staging-measured flip rate | L5 |

## Common pitfalls & limitations

- **Reporting a blended flip rate.** An undecomposed figure cannot distinguish a stochastic generation problem from a brittle regex, and the remediations are entirely different. Step 8 is the procedure's analytical core.
- **Treating a single clean test-suite pass as durable evidence of stability.** The canvas's blind-spot finding is precisely this: change control asks whether a change broke anything, never whether the pre-change system was stable to begin with.
- **Treating the extraction layer as plumbing.** It is a component that turns free text into "approve" or "decline" and it can flip that decision on its own, even where generation is materially unchanged. It requires independent validation, and identifying its owner is often the first thing this procedure surfaces.
- **Assuming determinism from traditional-model experience.** Traditional decisioning models are deterministic at inference, so "run it again and check" sits outside conventional intuition — which is precisely why the measurement is missing. The applicability exception exists because a nominally predictive stack that samples at inference is in scope: confirm it, do not default it to N.
- **Inventing a tolerance.** Where the firm has approved none, report the measurement and the missing tolerance as two separate findings. Substituting the reviewer's own figure is not available: FAIAS has no basis to set one.
- **Letting the pin move mid-procedure.** Any configuration change during execution invalidates the measurement; re-pin and restart.
- **An unsupported "consistently" claim.** Where governance papers or capability descriptions state that the system behaves consistently, and no repeat-run measurement exists, the claim is unsupported by measurement and is reported as such — the canvas's own fail language.
- **Canvas limitation carried forward:** published repeat-run methods exist as two workshop papers (Atıl et al., 2025; Khatchadourian and Franco, 2025), with the limits stated in the canvas (Field 18); no FAIAS-standard protocol for decision-flip-rate testing exists, and no FS-specific published method was located for extraction-layer isolation or immaterial-perturbation testing. Test design, sample size and tolerance-setting remain bespoke and professional-judgement-led. ★2 — the rating reflects the state of the methodology, not the quality of the execution. Report as professional assessment per METHODOLOGY_STANDARDS §3c.

## Time/effort estimate

**4 reviewer-days** (0.25 applicability determination and configuration pinning; 0.25 tolerance and prior-testing review; 0.5 sample construction and protocol fixing; 1 full-pipeline repeat-run execution; 0.75 extraction-only isolation and decomposition; 0.5 immaterial-perturbation series; 0.25 change-control and production-resubmission comparison; 0.5 reporting). Excludes compute wall-time for the repetition series and non-reviewer engineering support, costed separately.

---
---

