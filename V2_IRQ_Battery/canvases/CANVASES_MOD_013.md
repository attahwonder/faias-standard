# CANVAS: IRQ-MOD-013

## 1. IRQ ID & Title
**IRQ-MOD-013: Uncontrolled Prompt/Decoding-Parameter Change Materially Altering Behaviour**

Register question: "Are prompt templates, system prompts and decoding parameters version-controlled and regression-tested, given that small changes materially alter behaviour without any code change?"

## 2. Business Activities Affected
- **Underwriting assistant system prompt:** A small wording change to the system prompt (e.g. adjusting tone guidance, adding an example) can materially shift the model's decision recommendations or explanation style without any application code changing.
- **AML analyst copilot decoding parameters:** Adjusting temperature or sampling parameters to "make responses more natural" can measurably change the consistency and reliability of investigation narratives.
- **Customer-facing chatbot prompt template:** An informal prompt edit made to fix one complaint can silently change refusal behaviour or factual accuracy across the entire customer base.

## 3. AI Behaviour(s)
- Behaviour is materially shaped by the system prompt, prompt template and decoding parameters (temperature, top-p, etc.), which are typically stored as configuration or plain text rather than compiled code.
- The same underlying model can behave very differently under different prompt/parameter settings, without any model version change.
- Prompt and parameter edits are often made by product, prompt-engineering, or operations staff outside the formal software change-management process, since they "aren't code."

## 4. Failure Mode
> A prompt template, system prompt, or decoding parameter is changed without version control or regression testing, materially altering production model behaviour in a way that is not detected, documented, or re-approved before it reaches customers or decision-makers.

## 5. Potential Consequences
- **Customer:** An untested prompt edit degrades accuracy, changes refusal boundaries, or alters the tone/content of customer-facing communications, with no governance visibility into the change.
- **Institution:** Loss of the ability to reproduce, audit, or roll back to a known-good behavioural state; any incident investigation is hampered because the "version" that produced a given historical output cannot be reconstructed.
- **Regulator/market:** A change-control gap that would be unthinkable for application code is routine for prompts, undermining the credibility of the firm's broader AI governance claims (cf. xAI Grok "MechaHitler" incident, a real-world instance of an instruction change materially altering production behaviour before it was detected, although xAI does not say whether the change was tested before release).

## 6. Failure Chain
```
Prompt template, system prompt, or decoding parameter is edited
(e.g. to fix a specific complaint, improve tone, or "make it more natural")
  ↓ (IRQ-MOD-013 — THIS IRQ: no version control or regression test applied to the change)
Change deploys directly to production, often without any code review, since prompts
are treated as configuration rather than controlled artefacts
  ↓ (IRQ-AGT-009: for agentic systems, downstream behaviour depending on this prompt/
     reasoning-scaffold state compounds the effect)
Model behaviour materially shifts (accuracy, refusal boundaries, tone, factual
grounding) across the full customer/decision-maker base using that prompt
  ↓ (IRQ-GOV-003: approval conditions of use are not re-enforced because the change was not
     recognised as one requiring governance)
Degraded or non-compliant behaviour reaches customers before detection
  ↓
Incident/complaint pattern → investigation cannot reconstruct which prompt version
produced a given historical output → governance finding of an uncontrolled
behaviour-bearing change

Control Breakpoints:
  • IRQ-MOD-013: prompts and decoding parameters version-controlled as configuration,
    subject to the same change discipline as code
  • IRQ-MOD-013: fixed behavioural regression suite run on every prompt/parameter change
    before production deployment
  • IRQ-GOV-003: prompt/parameter changes recognised as changes requiring approval-condition
    re-enforcement
  • IRQ-RES-004: rollback to a known-good prompt/parameter version within recovery objectives
```

## 7. Why a Domain Expert May Miss It
- Traditional change management is built around code and infrastructure; a prompt is plain text, often edited in a web UI or spreadsheet, and does not intuitively register as "a system change" requiring the same rigour as a code deployment.
- The magnitude of behavioural change from a small prompt edit is genuinely counter-intuitive to non-AI-specialists — a single added sentence or example can shift refusal boundaries or accuracy more than many code changes would.
- Prompt engineering is often performed by product or operations staff without software engineering change-control training or tooling access, creating an organisational, not just technical, gap.
- The xAI Grok "MechaHitler" incident (Jul 2025) — a real, recent, public, high-severity example of a change to a production bot's instructions altering its behaviour (on xAI's account, an upstream code-path update that unexpectedly incorporated deprecated instructions for 16 hours) — demonstrates this is not a theoretical risk, yet remains widely under-appreciated as a governance priority in FS.

## 8. Assurance Objective
**AO-MOD-013:** Prompt templates, system prompts and decoding parameters shall be version-controlled and subject to a fixed behavioural regression test before any change reaches production, with the same change-approval discipline applied to code.

## 9. Expected Controls (Traced)
- **Version control of prompts and decoding parameters as configuration artefacts** — [linked IRQ-AGT-009; general software configuration-management practice extended to AI-specific artefacts] — every prompt template and parameter set is stored, versioned, and attributable to a specific change and approver, exactly as code would be.
- **Fixed behavioural regression suite on every change** — [informed by longitudinal behavioural-drift measurement methodology, Chen et al., 2023, arXiv:2307.09009; Harvard Data Science Review 6(2), 2024] — a representative test set is run against both the prior and proposed prompt/parameter version before deployment, with material divergence blocking automatic promotion.
- **Change approval requiring the same rigour as code deployment** — [linked IRQ-GOV-003; PRA SS1/23 change-management expectations by analogy] — prompt/parameter changes go through the same review and sign-off process as application code changes, not an informal or bypassed path.
- **Rollback capability to a known-good prompt/parameter version** — [linked IRQ-RES-004] — the firm can revert to a previous version within defined recovery objectives if a change proves harmful.
- **Post-deployment monitoring for behavioural change correlated with a recent prompt/parameter edit** — [linked IRQ-RES-005, IRQ-RES-006] — monitoring is capable of attributing a detected behavioural shift to a specific configuration change, supporting rapid root-cause diagnosis.

## 10. Expected Evidence (Tagged L1–L5)
- Informal assertion that "prompts are managed carefully" — **L1** (assertion only; flag).
- Version-control system (e.g. git-based) log showing prompt/parameter changes with author, timestamp and approval record — **L2**.
- Staging regression test results comparing prior and proposed prompt/parameter versions on a fixed test set, with pass/fail criteria applied — **L3**.
- Independent validation/audit confirming prompt/parameter changes cannot bypass version control or regression testing in the production deployment pipeline — **L4**.
- Production incident/change history showing at least one prompt/parameter change that was caught by regression testing before reaching customers, or rolled back after detection — **L5**.

## 11. Independent Test
> In a non-production environment, attempt to deploy a prompt or decoding-parameter change through whatever pathway is actually available to product/operations staff (not only the "official" documented pathway) and observe whether version control, regression testing and approval are structurally enforced or can be bypassed. Separately, take a historical prompt change (or a constructed representative change) and run the firm's fixed regression suite against both the pre- and post-change prompt versions on a representative task sample, measuring behavioural divergence (accuracy, refusal-rate, tone/content shift). Confirm whether a rollback to the prior version can be executed within the firm's defined recovery objective. Methodology informed by longitudinal drift-measurement practice (Chen et al., 2023) applied to firm-controlled configuration rather than vendor-controlled model versions. Executed entirely in staging with non-production deployment pathways. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the mechanism — small prompt changes causing material behavioural shifts — is well-evidenced by both research and public incident; the specific test of whether the firm's deployment pathway structurally enforces version control is bespoke to the institution's tooling and requires professional judgement to design comprehensively).

## 12. Pass Indicators
- Every available deployment pathway for prompt/parameter changes enforces version control; no informal bypass path exists.
- A fixed regression suite runs automatically on every prompt/parameter change, with material divergence blocking promotion to production.
- Change approval records exist for prompt/parameter changes at the same rigour as code changes.
- Rollback to a known-good version has been demonstrated within the firm's defined recovery objective.

## 13. Fail Indicators
- A bypass pathway exists (e.g. a vendor console, a shared prompt-editing document) that allows prompt/parameter changes to reach production without version control or regression testing.
- No fixed regression suite exists for prompt/parameter changes; testing, if any, is ad hoc and undocumented.
- Historical evidence shows a prompt/parameter change reached production and caused a detectable behavioural shift before being caught (or was never caught, only discovered via complaint).
- Rollback to a prior prompt/parameter version is not demonstrated or is not achievable within a defined time bound.

## 14. Reporting Language
**Pass:** "Prompt templates and decoding parameters are version-controlled with no available bypass pathway; a fixed regression suite runs on every change, and rollback to a known-good version has been demonstrated within the firm's recovery objective. Conclusions rest on ★2 methodology — well-evidenced general mechanism, institution-specific pathway testing — and should be re-verified whenever the deployment tooling changes."

**Fail:** "Testing found that prompt changes can reach production via [a vendor console / an undocumented pathway] with no version control or regression testing applied. A constructed test change produced a [x] percentage-point shift in [accuracy/refusal rate/tone] against the fixed regression suite, illustrating the scale of undetected risk this bypass permits. This is a foundational change-management gap for a behaviour-bearing artefact; the bypass pathway should be closed and regression testing made mandatory before further prompt changes are permitted."

**Partial:** "Version control and regression testing are enforced for the primary prompt-deployment pathway but not for [a secondary tool/console] used by [a specific team]. The assurance objective is not fully met until coverage is equivalent across all pathways; use of the secondary pathway should be restricted pending remediation."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a well-governed prompt change process bounds the blast radius of any single
              edit; residual risk is a control lapse, not a structural gap)
  Likelihood: 2 (plausible only if version control or regression testing is bypassed or
              lapses, which controls should prevent)
  Detectability: 2 (regression testing and change-attributed monitoring surface issues before
              or shortly after deployment)
  Recoverability: 2 (rollback to a known-good version is a defined, rapid remediation)
  Novelty: 3 (that a prompt edit is a behaviour-bearing change requiring code-equivalent
              rigour is not obvious to teams trained in traditional software change control,
              where text/configuration edits are often treated as lower-risk than code)

Interpretation: acceptable residual risk with version control, regression testing and
rollback capability in place; highest concern is Novelty — the organisational habit of
treating prompts as "just text" rather than as controlled, behaviour-bearing artefacts.

If controls are absent or degraded:
  Severity: 3 (an uncontrolled prompt/parameter change can materially alter behaviour across
              the entire customer/decision-maker base using that prompt, with no attribution
              trail — the scale of such an alteration illustrated at high severity by the
              xAI Grok incident, although xAI does not say whether the change was tested
              before release)
  Likelihood: 4 (prompt edits are frequent, low-friction, and commonly made outside formal
              change control by design of most prompt-management tooling)
  Detectability: 4 (without regression testing, a behavioural shift is discovered only via
              complaint or anomaly, with no attribution to the specific change that caused it)
  Recoverability: 2 (rollback itself is usually straightforward once the causal change is
              identified; the harder problem is identification, which is captured above under
              Detectability)
  Novelty: 3
Residual risk: Critical. Deployment gate should not be passed without version control and
regression testing on prompt/parameter changes.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | An uncontrolled prompt change can materially alter behaviour across the entire customer/decision-maker base using that prompt; the scale of such an alteration is illustrated at high severity by a real public incident (xAI Grok, Jul 2025), although xAI does not say whether the change was tested before release. |
| **Likelihood** | 3 | Prompt/parameter edits are frequent and low-friction; many prompt-management tools do not enforce change control by default, making bypass the path of least resistance absent deliberate governance. |
| **Detectability** | 3 | Without regression testing and change-attributed monitoring, a behavioural shift is discovered only via complaint or anomaly, with no attribution trail to the causal change. |
| **Recoverability** | 2 | Rollback is usually straightforward once the causal change is identified; the harder cost is the identification step itself. |
| **Novelty** | 3 | Treating a prompt edit as a behaviour-bearing change requiring code-equivalent change control is not obvious to teams trained in traditional software change management, where text edits are typically deprioritised relative to code. |

## 17. Regulatory Basis
> [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024, Principle 3 (model development, implementation and use) and Principle 4 (independent model validation — review of model changes and periodic revalidation)] — a prompt or decoding-parameter change that materially alters model behaviour is, in substance, a model change and falls within SS1/23's change-management expectations even though it involves no code deployment. No regulation names "prompt version control" explicitly; this IRQ operationalises SS1/23's change-management principle for a configuration artefact specific to generative AI. (verified 29 Jul 2026)

## 18. Research Basis
> [Chen, L., Zaharia, M., Zou, J., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009; Harvard Data Science Review 6(2), 2024] — demonstrates that behavioural drift across nominal versions is measurable and material, supporting the regression-testing methodology used in this IRQ's independent test, applied here to firm-controlled prompt/parameter changes rather than vendor-controlled model versions. [Incident: xAI Grok "MechaHitler" episode, Jul 2025 — on xAI's account, an upstream code-path update that unexpectedly incorporated deprecated instructions into the production bot's behaviour for 16 hours, publicly documented and widely reported] — direct, recent, high-severity real-world evidence that a change to a production system's instructions can materially alter its behaviour before it is detected. xAI states that changes to the bot are evaluated and tested before release and does not say whether this update was, so the incident does not evidence a change made outside a change-control process.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-AGT-009 (C.6: the agent-specific hazard of behaviour depending on undocumented prompt/
    reasoning-scaffold state across a multi-step workflow — this IRQ is the general
    generative-system change-control discipline both draw on)
  - IRQ-MOD-002 (B.1: vendor-side capability change — the externally-originated counterpart
    to this firm-side configuration-change risk)
  - IRQ-GOV-003 (I.2: conditions of use must be technically re-enforced after any
    behaviour-bearing configuration change)
  - IRQ-RES-004 (G.2: rollback of prompts/config as part of full behavioural-component
    rollback capability)
  - IRQ-GOV-012 (I.2: operating-envelope drift reconciliation, which prompt changes can
    silently cause)
```

## 20. References
```
[1] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over Time?"
    arXiv:2307.09009. Published in Harvard Data Science Review 6(2), 12 March 2024,
    https://doi.org/10.1162/99608f92.5317da47.
[2] The Guardian, 2025. "Musk's AI firm forced to delete posts praising Hitler from Grok chatbot."
    9 July 2025. https://www.theguardian.com/technology/2025/jul/09/grok-ai-praised-hitler-antisemitism-x-ntwnfb
[3] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.6 (Model domain, Model Updates & Configuration)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional change management treats text/configuration edits as
  lower-risk than code; that a single prompt sentence can shift refusal boundaries or
  accuracy more than many code changes is genuinely counter-intuitive.
✓ Test 2 (Plausible Harm): Grounded in longitudinal behavioural-drift research (Chen et al.,
  2023) and a real, recent, high-severity public incident (xAI Grok, Jul 2025).
✓ Test 3 (Testable): Fully testable in staging via deployment-pathway probing and fixed
  regression suites on constructed prompt changes; no production access required.
✓ Test 4 (Decision-Relevant): Outcome gates whether prompt/parameter changes may bypass
  formal change control, and sets the mandatory regression-testing condition of use.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.1 (2026-09-19): Fields 5, 7, 15, 16 and 18 — erratum: the xAI Grok episode of July 2025 was described as an un-gated system-prompt change that removed behavioural constraints in production and, in the research basis, as this failure mode occurring outside a change-control process. On xAI's own account of 12 July 2025 an upstream code-path update unexpectedly incorporated deprecated instructions into the production bot's behaviour for 16 hours; xAI states that changes to the bot are evaluated and tested before release and does not say whether this update was. Fields 5, 7 and 18 now carry that account; Residual Judgement (Field 15) and Risk Weighting Profile (Field 16), which offered the episode as the illustration of an uncontrolled change with no attribution trail, now cite it for the scale of the behavioural alteration only, with the same caveat; none of the five calls the change un-gated or says it was made outside change control. Field 20 — erratum: reference [2]'s title corrected to the article's headline. Research-basis review date moved. No change to controls, test, ★2 or any five-axis rating.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Fields 9, 18 and 20 — the Chen, Zaharia and Zou citation (arXiv:2307.09009) now also gives its publication in Harvard Data Science Review 6(2), 2024. Research-basis review date moved. No change to the ★ rating or the risk profile.
```

---
---
