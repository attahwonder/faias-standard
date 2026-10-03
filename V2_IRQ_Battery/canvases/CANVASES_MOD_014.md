# CANVAS: IRQ-MOD-014

## 1. IRQ ID & Title
**IRQ-MOD-014: Unmeasured Decision-Flip Rate Under Materially Identical Inputs at Pinned Configuration**

Register question: "At a pinned model version, prompt/system configuration and decoding parameters, do materially identical inputs — exact repeat runs, and inputs subject only to immaterial perturbation — produce different consequential decisions or outputs; is the resulting decision-flip rate measured and held within a defined bound; and is the decision-extraction logic that turns model output into a decision tested separately from the underlying generation?"

**Applicability:** Y / Y / N — predictive-stack applicability is N by default (a fixed classical/statistical model is deterministic at inference), flipping to **Y** where a predictive stack itself samples at inference (e.g. randomised subsampling, ensemble sampling). Confirmed at authoring, 31 Jul 2026; applicability is confirmed at scoping, not assumed.

## 2. Business Activities Affected
- **Lending/underwriting decisioning:** at pinned model/prompt configuration, identical applicant data submitted twice (e.g. a retried request after a timeout) can return "approve" on one run and "decline" on the next, with nothing in the case file to explain the divergence.
- **AML disposition:** a transaction-narrative model at pinned configuration flags an alert as "escalate" on one run and "no further action" on a re-run of the identical case, with a separate extraction layer converting free text into the binary disposition.
- **Claims triage and customer communications:** repeat generation of a customer-facing decision letter for the identical claim can flip the stated outcome or its framing between runs, with no record of which run was relied upon.

## 3. AI Behaviour(s)
- Samples tokens stochastically at inference (temperature/top-p/top-k decoding) even when model version, prompt, system configuration and input are held fixed, so repeat runs of an identical input are not guaranteed to produce an identical output.
- Downstream systems parse free-text or variably-structured model output into a discrete decision (approve/decline, escalate/clear) via separate extraction logic (regex, classifier, schema parse), which can itself flip the extracted decision even where the underlying generation is materially unchanged.
- Immaterial input perturbation (whitespace, field ordering, a non-substantive rounding difference upstream) can also change the output at a rate not predictable from the size of the perturbation.

## 4. Failure Mode
> At a pinned model version, prompt/system configuration and decoding parameters, materially identical or immaterially-perturbed inputs produce a different consequential decision on repeat runs, and neither the generation-level flip rate nor the separate contribution of decision-extraction logic is measured or bounded.

## 5. Potential Consequences
- **Customer:** two customers in materially identical circumstances — or the same customer on a retried request — receive different outcomes, with no record of which run was "correct" and no basis to explain the divergence if challenged.
- **Institution:** change-control and QA processes that treat a single test-suite pass as durable evidence give false assurance — nothing changed, yet the decision was never guaranteed to be stable in the first place; unequal-treatment claims are difficult to rebut without a measured flip rate.
- **Regulator/market:** an inability to demonstrate consistent treatment of like cases is a direct challenge to Consumer Duty fair-treatment expectations, and directly undermines any capability claim describing the system's behaviour as "consistent" or produced "consistently".

## 6. Failure Chain
```
Model deployed with stochastic decoding at inference (temperature > 0)
  ↓ (IRQ-MOD-014 — THIS IRQ: no repeat-run flip-rate measurement at pinned configuration)
Identical or near-identical input run twice returns different free-text output
  ↓ (IRQ-MOD-014 — decision-extraction logic not separately validated)
Decision-extraction layer converts the divergent output into a different discrete decision
  ↓ (IRQ-MOD-006: confidence signal, if any, does not flag the instability)
No escalation triggered; whichever run happened to execute is treated as the decision
  ↓ (IRQ-CON-001: subgroup/consistency testing does not include repeat-run stability)
Two materially identical cases receive different outcomes, undetected
  ↓
Customer complaint or internal audit discovers the divergence → unequal-treatment finding
→ Consumer Duty/fair-treatment exposure; unsupported "consistently" claim

Control Breakpoints:
  • IRQ-MOD-014: pinned-configuration repeat-run protocol with measured, bounded flip rate
  • IRQ-MOD-014: decision-extraction logic tested independently of generation
  • IRQ-MOD-006: confidence/consistency signal escalates where instability is detected
  • IRQ-CON-001: fairness/consistency testing extended to include repeat-run stability
```

## 7. Why a Domain Expert May Miss It
- Change-control practice tests "did the change break anything" against a single pass of a fixed test suite; it does not ask whether the pre-change system was ever stable to begin with, so a clean pass is mistaken for durable proof of stability.
- Traditional (non-generative) decisioning models are deterministic at inference — the same input always returns the same output — so "run it again and check" sits outside an SME's mental model of what needs testing for an AI system.
- Decision-extraction logic (the code or prompt that turns free text into "approve"/"decline") is often treated as trivial plumbing, not as a component that itself requires independent validation.
- The word "consistently" appears in capability claims and governance papers without anyone having actually re-run the same case twice to check.

## 8. Assurance Objective
**AO-MOD-014:** Run-to-run and near-identical-input decision stability shall be measured at pinned model configuration, held within a defined and documented tolerance, and the decision-extraction logic that converts model output into a decision shall be validated independently of the underlying generation.

## 9. Expected Controls (Traced)
- **Pinned-configuration repeat-run protocol before approval and after material change** — [Emerging Practice; no published FS-specific methodology identified] — the same representative consequential inputs are run n times at fixed model version/prompt/decoding parameters and the outcome distribution recorded.
- **Measured, bounded flip rate against a stated tolerance** — [linked IRQ-GOV-006 risk appetite] — a documented, governance-approved maximum acceptable flip rate for consequential decisions, analogous to existing tolerance-setting practice in IRQ-MOD-004.
- **Decision-extraction logic tested as its own component** — [Emerging Practice] — extraction-layer behaviour (parsing, classification, schema validation) is tested by holding generation fixed and varying only extraction inputs, isolating extraction-driven flips from generation-driven flips.
- **Immaterial-perturbation testing** — [linked IRQ-CON-001 fairness/consistency testing] — inputs that should be decision-irrelevant (formatting, field order, immaterial rounding) are varied and the decision checked for stability.
- **Predictive-stack exception check at scoping** — [applicability note, this IRQ] — where a nominally predictive component samples at inference, applicability is confirmed Y rather than assumed N.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor or developer assertion that the system is "reliable" or "consistent" with no repeat-run evidence — **L1** (assertion only; flag).
- Design documentation defining the repeat-run test protocol, sample size and the tolerance threshold to be applied — **L2**.
- Staging test results: flip rate measured across n repeat runs on a representative sample of consequential inputs at pinned configuration, decomposed into generation-level and extraction-level contribution — **L3**.
- Independent validation report assessing the repeat-run methodology and findings, performed by a function independent of development — **L4**.
- Production monitoring data comparing logged outcomes for near-duplicate case resubmissions (e.g. retries) against the staging-measured flip rate — **L5**.

## 11. Independent Test
> In a non-production environment, select a representative sample of consequential inputs at pinned model version, prompt/system configuration and decoding parameters. Run each input n times (n sized to the tester's judgement; no standard sample size exists) and record the discrete decision produced by the full pipeline including extraction logic; compute the flip rate. Repeat with a second, extraction-only test: hold a fixed generated output constant and vary only extraction-layer inputs (e.g. edge-case phrasing, formatting) to isolate the extraction layer's own contribution to instability. Separately, apply immaterial input perturbations (whitespace, field order, non-substantive rounding) to a further sample and measure decision stability. Executed entirely on synthetic/anonymised or historical non-live data in staging. **None established as a methodology — stated plainly; no published or FAIAS-standard protocol for decision-flip-rate testing was identified.** Test design, sample size and tolerance-setting are bespoke and professional-judgement-led. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the underlying phenomenon — stochastic sampling instability and extraction-layer brittleness — is well understood mechanically, but no published assurance methodology, benchmark or FS precedent exists for measuring or bounding it; test design rests entirely on tester judgement). **Field-maturity caveat:** the phenomenon is documented; the assurance methodology is not — this ★2 reflects that gap directly, not a defect in test execution.

## 12. Pass Indicators
- Measured flip rate at pinned configuration is at or below the governance-approved tolerance for consequential decisions.
- Extraction-layer contribution to the flip rate is separately measured and is not the dominant source of instability, or is itself remediated (e.g. deterministic parsing, schema validation with fallback).
- Immaterial-perturbation testing shows no material decision change from decision-irrelevant input variation.
- Repeat-run testing is repeated after any material model, prompt or configuration change, not treated as a one-off approval artefact.

## 13. Fail Indicators
- No repeat-run testing has ever been performed; stability is asserted rather than measured.
- Measured flip rate on consequential decisions is non-trivial and no governance-approved tolerance exists against which to judge it.
- Extraction logic has never been tested independently of generation; flips cannot be attributed to generation vs extraction.
- Immaterial input perturbation (formatting, field order) changes the decision at a material rate.

## 14. Reporting Language
**Pass:** "Decision-flip rate at pinned model configuration has been measured across a representative sample of consequential inputs and is within the governance-approved tolerance; decision-extraction logic has been separately validated and is not a material source of instability. Conclusions rest on ★2 methodology — no established testing methodology exists for this failure mode; test design is bespoke and professional-judgement-led — and should be repeated on material change."

**Fail:** "No repeat-run stability testing has been performed on this system; claims that the system behaves 'consistently' are unsupported by measurement. Independent staging testing found a flip rate of [x]% on materially identical consequential inputs at pinned configuration, with no governance-approved tolerance in place to judge whether this is acceptable. This is a foundational assurance gap for any consequential AI decision system; deployment should not proceed on the strength of a 'consistency' claim until flip-rate measurement and an approved tolerance are in place."

**Partial:** "Repeat-run flip-rate testing has been performed for [use case A] but not for [use case B] sharing the same underlying model and configuration. The assurance objective is not met for use case B; deployment should be restricted to measured use cases pending equivalent testing."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (materially identical cases can receive different consequential outcomes;
              unequal-treatment and Consumer Duty exposure)
  Likelihood: 2 (repeat-run measurement and bounded tolerance should catch and constrain
              instability before it becomes systemic)
  Detectability: 2 (repeat-run testing and production resubmission monitoring surface
              instability directly when performed)
  Recoverability: 2 (affected cases identifiable via logs where flip rate is monitored;
              re-decisioning feasible)
  Novelty: 4 (traditional decisioning models are deterministic; that a pinned-configuration
              AI system may not return the same answer to the same question is genuinely
              counter-intuitive and outside conventional change-control testing)

Interpretation: acceptable residual risk with repeat-run measurement and a bounded tolerance
in place; highest concern is Novelty — the failure mode contradicts the deterministic
assumption baked into conventional model risk practice.

If controls are absent or degraded:
  Severity: 3 (unequal treatment across a population of materially identical cases, with no
              record permitting the divergence to be explained or defended)
  Likelihood: 4 (stochastic sampling at inference is the default configuration for most
              deployed generative systems; instability is the base case, not an edge case)
  Detectability: 4 (silent; nothing in change control or a single test-suite pass signals
              the absence of stability testing)
  Recoverability: 3 (requires retrospective identification of affected case pairs, which may
              not be possible without prior repeat-run logging)
  Novelty: 4
Residual risk: High. Should gate approval of any consequential-decision deployment pending
flip-rate measurement, particularly given CLM-04's unevidenced "consistently" claim.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Materially identical cases can receive different consequential outcomes; unequal-treatment and Consumer Duty exposure. |
| **Likelihood** | 3 | Stochastic sampling at inference is the default configuration for deployed generative systems; instability absent measurement is probable, not rare. |
| **Detectability** | 3 | Without repeat-run testing or resubmission monitoring, instability is invisible to conventional single-pass QA and change control. |
| **Recoverability** | 2 | Affected cases are identifiable via logs where flip rate is monitored, and re-decisioning is feasible. |
| **Novelty** | 4 | Traditional decisioning models are deterministic; that a pinned-configuration AI system may not return the same answer to the same question sits outside conventional change-control intuition. |

## 17. Regulatory Basis
> [FCA, PRIN 2A Consumer Duty, in force 31 July 2023, consumer understanding outcome (PRIN 2A.5) and cross-cutting obligations (PRIN 2A.2)] — materially identical customers receiving different outcomes with no evidenced basis is difficult to reconcile with fair-treatment expectations. [PRA SS1/23, May 2023, effective 17 May 2024, Principle 3 (model development, implementation and use)] — development and use principles presuppose that a model's behaviour at a given configuration is understood and controlled; unmeasured decision instability is a gap in that understanding. No regulation names "decision-flip rate" or "output stability testing" explicitly; this IRQ operationalises the above general principles for an AI-specific stochastic-sampling failure mode. (verified 31 Jul 2026)

## 18. Research Basis
> **None established.** No published research anchor establishing a decision-flip-rate or output-stability-testing methodology for consequential FS decisions was identified in the verified corpus at time of drafting (31 Jul 2026). This is a stated gap, not an oversight: stochastic token sampling at inference (temperature/top-p decoding) is well documented in general model-provider technical documentation, and the resulting run-to-run variability of generations is widely acknowledged informally, but no peer-reviewed methodology, published incident analysis, or FS-specific assurance precedent for measuring or bounding decision-flip rate — or for testing decision-extraction logic independently of generation — was located. No anchor is manufactured to fill this gap. The Independent Test above is designed from first principles accordingly and is rated ★2 on that basis.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-MOD-006 (B.3: confidence calibration — a well-calibrated confidence signal would be
    expected to reflect, not mask, run-to-run instability; overlapping but distinct construct)
  - IRQ-MOD-013 (B.6: model updates & configuration — a pinned configuration is the baseline
    against which this IRQ measures stability; MOD-013 covers what happens when the pin moves)
  - IRQ-DAT-008 (A.3: retrieval determinism and precedence — a related stability concern at
    the retrieval layer rather than the generation/extraction layer)
  - IRQ-CON-001 (H.1: subgroup/intersectional fairness testing — repeat-run stability is a
    precondition for any fairness metric to be meaningful; an unstable decision cannot be
    reliably attributed to a protected characteristic or anything else)
```

## 20. References
```
[1] FCA, 2022. "PS22/9: A New Consumer Duty." PRIN 2A in force 31 July 2023.
[2] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
```
No research reference is listed — none established; see Field 18.

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.7 (Model domain, Output Stability & Determinism) — new subdomain
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Conventional change control and QA treat a single test-suite pass
  as durable evidence of stability, and traditional deterministic decisioning models offer no
  intuition that a pinned-configuration AI system may answer the same question differently on
  repeat runs.
✓ Test 2 (Plausible Harm): Grounded in the well-documented mechanical fact of stochastic
  token sampling at inference and in CLM-04's unevidenced "consistently" claim; no published
  research anchor exists for the assurance methodology itself — stated as a gap, not
  manufactured.
✓ Test 3 (Testable): Fully testable in staging via pinned-configuration repeat-run protocol
  and extraction-layer isolation testing; no production data required.
✓ Test 4 (Decision-Relevant): Outcome directly closes the evidence gap behind CLM-04
  (Critical) and gates approval of consequential-decision deployments on a measured,
  bounded flip rate.

Change Log:
- v1.0 (2026-08-01): Initial publication (v1.0.3 batch); four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

