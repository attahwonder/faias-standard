# TP-MOD-013 — Prompt and Decoding-Parameter Change-Control Testing

**Procedure ID:** TP-MOD-013
**IRQ:** IRQ-MOD-013 — Uncontrolled Prompt/Decoding-Parameter Change Materially Altering Behaviour
**Assurance objective:** AO-MOD-013 — prompt templates, system prompts and decoding parameters shall be version-controlled and subject to a fixed behavioural regression test before any change reaches production, with the same change-approval discipline applied to code.
**★ Confidence:** ★2 (carried from canvas — the mechanism (small prompt changes causing material behavioural shifts) is well evidenced by both research and public incident; the specific test of whether the firm's deployment pathway structurally enforces version control is bespoke to the institution's tooling and requires professional judgement to design comprehensively)
**Method classification:** Adapted Industry Practice — longitudinal drift-measurement practice (Chen et al., 2023, as cited in the canvas) applied to firm-controlled configuration rather than vendor-controlled model versions; the pathway-enforcement component is **bespoke**.

## Preconditions

- **Environment:** staging with **non-production deployment pathways** available for exercise. Any pathway that can only be exercised against production is out of scope and must be recorded as untested rather than attempted.
- **Access needed:** every deployment pathway for prompt/parameter change available to product and operations staff — including informal ones (vendor console, shared prompt-editing document, feature-flag interface, CMS); the regression suite; change-approval records; rollback tooling.
- **Artefacts requested in advance (2 weeks):** the documented change process for prompts and decoding parameters; the fixed regression suite and its promotion-blocking criteria; change-approval records for prompt/parameter changes over the review period, comparable with code-change records; rollback procedure and recovery objective; historical incidents involving a prompt or parameter change.
- **Personnel:** reviewer (lead); platform engineer; **a product or operations person who actually edits prompts** — this interview is essential, because the informal pathway is by definition undocumented and only the practitioner knows it exists; change-control owner.

## Test design

- **Component 1 — pathway enumeration and bypass testing.** Enumerate every route by which prompt text or a decoding parameter can reach the running system, from interviews and configuration, not from the documented process. For each route, attempt (in staging) to deploy a change and observe whether version control, regression testing and approval are **structurally enforced** or bypassable. Enumeration completeness is the procedure's critical variable — an unenumerated pathway is an untested pathway.
- **Component 2 — behavioural-divergence measurement.** Take a historical prompt change (preferred) or a constructed representative change, and run the firm's fixed regression suite against both versions on a representative task sample. Measure divergence in accuracy, refusal rate, and tone/content shift. The reviewer, having run TP-MOD-001 to 009, is well placed to select a change that is plausible and behaviourally meaningful rather than trivial.
- **Component 3 — rollback exercise.** Execute a rollback to the prior version in staging and measure elapsed time against the firm's recovery objective.
- **Benign-payload principles:** the test change is a benign, realistic edit (a rewording, a threshold adjustment) — never a change that weakens a safety instruction or removes a guardrail, even in staging. The point is to test the *control pathway*, not to demonstrate that a safety instruction can be removed.

## Steps

1. Interview the product/operations prompt editor: how do prompt changes actually get made, including any quick route used under time pressure? **Record:** the pathways described, verbatim where possible.
2. Enumerate pathways from configuration and tooling independently. **Record:** the union of interview-derived and configuration-derived pathways, flagging any not in the documented process.
3. For each pathway, in staging, attempt a benign prompt change and observe whether version control, regression testing and approval are enforced. **Record:** per-pathway outcome: enforced / partially enforced / bypassable.
4. Select the behavioural test change (historical preferred). **Record:** the change and the rationale for its representativeness.
5. Fix and record the decoding configuration and repetition count. Establish the within-version variance as the noise floor.
6. Run the firm's fixed regression suite against the pre-change prompt version. **Record:** results.
7. Run it against the post-change version. **Record:** results.
8. Measure divergence on the three dimensions — accuracy, refusal rate, tone/content shift — adjusted for the noise floor. **Record:** the divergence profile.
9. Determine whether the firm's own promotion criteria would have **blocked** this change. **Record:** the criteria and the outcome under them. A regression suite that runs but blocks nothing is not a control.
10. Execute a rollback to the prior version. **Record:** elapsed time versus the recovery objective, and whether rollback was clean.
11. Compare change-approval records for prompt/parameter changes against those for code changes over the review period. **Record:** the comparison — the objective requires equivalent rigour.
12. Review any historical incident involving a prompt or parameter change. **Record:** how it was detected — monitoring, regression testing, or complaint.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Deployment pathways enforcing version control | **Every** pathway; no informal bypass path (canvas pass indicator) | Canvas |
| Regression suite runs automatically on every change | Automatic, with material divergence blocking promotion (canvas pass indicator) | Canvas |
| Behavioural divergence from the test change | Report against the noise floor; materiality is **reviewer judgement — no established threshold** | Canvas: mechanism evidenced, thresholds bespoke |
| Change-approval rigour versus code changes | Equivalent (canvas pass indicator) | Canvas |
| Rollback within the recovery objective | Demonstrated, not asserted (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — every available deployment pathway for prompt/parameter changes enforces version control with no informal bypass; a fixed regression suite runs automatically on every change with material divergence blocking promotion; change-approval records exist at the same rigour as for code; rollback to a known-good version has been demonstrated within the defined recovery objective.
- **Fail** — a bypass pathway exists (vendor console, shared prompt-editing document) allowing changes to reach production without version control or regression testing; no fixed regression suite exists and testing is ad hoc and undocumented; historical evidence shows a prompt or parameter change reached production and caused a detectable behavioural shift before being caught, or was never caught and surfaced only via complaint; rollback is not demonstrated or not achievable within a defined time bound.
- **Partial** — the primary pathway is fully governed while a secondary one is not; or the regression suite runs but has no promotion-blocking criteria, so it informs without controlling. Report per pathway — an average across pathways is meaningless when a single bypass defeats the control.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Interview note with the prompt editor (pathways as described) | L2, elevated to L3 where the pathway is then verified in configuration |
| Independent pathway enumeration | **L4** |
| Per-pathway bypass test results | L4 |
| Test change definition and rationale | L3 |
| Noise-floor measurement | L3 |
| Regression suite results, pre- and post-change | **L4** |
| Divergence profile (accuracy, refusal rate, tone/content) | L4 |
| Promotion-criteria evaluation | L3 |
| Rollback exercise record with elapsed time | L4 |
| Change-approval record comparison (prompt versus code) | L2–L3 |
| Historical incident record | L5 |

## Common pitfalls & limitations

- **Enumerating pathways from documentation.** The documented pathway is the governed one by definition; the finding is always in the undocumented route. Step 1 is the procedure.
- **Choosing a trivial test change.** A cosmetic edit that changes nothing demonstrates nothing. Use a historical change, or one the reviewer has reason to believe is behaviourally load-bearing.
- **Weakening a safety instruction as the test change.** Never — even in staging. Test the pathway, not the guardrail.
- **Canvas limitation carried forward:** the pathway-enforcement test is bespoke to the institution's tooling and requires professional judgement to design comprehensively; completeness of enumeration cannot be proven. ★2 — professional assessment, and state that unenumerated pathways may exist.
- **Staging pathways may differ from production pathways.** Where a pathway exists in production but not in staging, it cannot be tested here; record it as untested rather than passed.

## Time/effort estimate

**3 reviewer-days** (0.5 interviews and pathway enumeration; 0.5 bypass testing; 0.5 regression execution; 0.5 divergence analysis; 0.5 rollback exercise; 0.5 change-record comparison and reporting).

---
---

