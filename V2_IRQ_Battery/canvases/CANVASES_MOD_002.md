# CANVAS: IRQ-MOD-002

## 1. IRQ ID & Title
**IRQ-MOD-002: Undocumented Capability Expansion via Model Release Introducing Unapproved Behaviour**

Register question: "Could a model release or update introduce unexpected or expanded capabilities into production without documentation and re-approval of the enlarged capability surface?"

## 2. Business Activities Affected
- **Underwriting assistant on a hosted foundation model:** A vendor releases a point update; the model now attempts multi-step reasoning or tool-like behaviour it previously refused, changing the underwriting narrative it produces without any firm-side change request.
- **AML analyst copilot:** A model update improves fluency in generating plausible-sounding SAR narratives, increasing the risk that ungrounded content is accepted at face value by analysts used to the model's previous, more cautious style.
- **Customer advice chatbot:** An update expands the model's willingness to answer adjacent regulated-advice-like questions it previously declined, silently widening the effective service scope.

## 3. AI Behaviour(s)
- Behaves differently after a version update to the same nominal model/endpoint, without the firm changing any prompt or code.
- May begin performing tasks (multi-step reasoning, more assertive claims, broader topic coverage) it previously refused or performed poorly.
- Vendor release notes, where they exist, describe capability changes at a general level not mapped to the firm's specific approved use case.

## 4. Failure Mode
> A vendor-side model release introduces expanded or altered capabilities into a production endpoint the firm already approved for a narrower use, and those capabilities are used in production before the firm has assessed, documented and re-approved the enlarged capability surface.

## 5. Potential Consequences
- **Customer:** Exposure to newly-enabled behaviours (more assertive claims, expanded topic scope) that were never validated for safety or accuracy in the firm's specific context.
- **Institution:** Model risk governance is bypassed by a change the firm did not initiate; SS1/23 development/validation principle breach; loss of change-control assurance.
- **Regulator/market:** Evidence that a supervised firm's AI control environment can be silently altered by a third party without the firm's knowledge — a systemic governance gap flagged by BoE/FPC concentration concerns.

## 6. Failure Chain
```
Vendor ships a model/endpoint update
(weights, safety filters, or default behaviour changed)
  ↓ (IRQ-TPR-004: no contractual advance-notice or version-pinning control)
Firm's production endpoint silently receives new behaviour
  ↓ (IRQ-MOD-002 — THIS IRQ: no capability-delta detection or re-approval gate)
Expanded capability used in live underwriting/AML/advice workflow
  ↓ (IRQ-GOV-003: approval conditions not technically re-enforced post-update)
New, unvalidated behaviour reaches customer or decision-maker
  ↓ (IRQ-HUM-001: reviewers calibrated on the prior model version accept unfamiliar output)
Incorrect or non-compliant decision/communication issued
  ↓
Complaint/incident → root-cause traces to unapproved vendor-side capability change →
governance and regulatory finding

Control Breakpoints:
  • IRQ-TPR-004: version pinning, canary testing, contractual advance notice of vendor changes
  • IRQ-MOD-002: capability-delta assessment and re-approval gate per release
  • IRQ-GOV-003: conditions of use technically enforced, not just documented
  • IRQ-RES-005/006: monitoring surfaces behavioural change (even gradual) post-update
```

## 7. Why a Domain Expert May Miss It
- Credit/AML SMEs are used to change control for internally-built systems, where nothing changes unless the firm deploys a change; the idea that "the same API endpoint" can behave differently overnight is counter-intuitive.
- Vendor release notes are typically framed as improvements, not risks — SMEs read "better reasoning" as unambiguously positive rather than as an unapproved capability-surface expansion requiring re-validation.
- Traditional model risk sign-off is a point-in-time event; the assumption that approval persists indefinitely for a "black-box" hosted model is a governance blind spot specific to externally-controlled AI.
- Behavioural drift from vendor updates can be gradual and multi-release, making a single trigger point hard to identify without dedicated canary testing.

## 8. Assurance Objective
**AO-MOD-002:** Capability deltas introduced by any model or endpoint release shall be detected, assessed and formally re-approved by the firm before the expanded capability surface is relied upon in production, and no vendor-side change shall bypass the firm's governance process.

## 9. Expected Controls (Traced)
- **Version pinning and controlled roll-forward** — [linked IRQ-TPR-004; PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), model change management expectations] — production traffic is pinned to a specific model version; upgrades are a deliberate, governed act, not automatic.
- **Behavioural canary/regression testing on every release** — [Chen et al., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009; Harvard Data Science Review 6(2), 2024; linked IRQ-MOD-013] — a fixed regression suite runs against any new version before production cutover, comparing outputs to the prior baseline.
- **Contractual advance-notice and change-transparency rights** — [linked IRQ-TPR-002] — vendor contracts secure notice of material model, weight, or default-behaviour changes ahead of production impact.
- **Capability-delta assessment and re-approval gate** — [PRA SS1/23 development/validation and ongoing-use principles] — any detected capability change triggers a structured re-assessment before continued reliance, mirroring initial approval rigour.
- **Post-release monitoring for behavioural drift** — [linked IRQ-RES-005, IRQ-RES-006] — quality/behaviour metrics tracked continuously to catch capability changes that canary testing alone might miss.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor release notes describing "general capability improvements" — **L1** (assertion only; no firm-specific assessment).
- Change-management policy requiring re-approval on detected capability delta — **L2**.
- Configuration/version-pinning audit confirming the firm controls when updates reach production — **L3**.
- Canary test results comparing pre- and post-update outputs on a fixed regression suite, with any behavioural delta documented — **L3**.
- Independent validation report reviewing the firm's model-change governance process and its application to a recent release — **L4**.
- Production monitoring data showing detection of, and governance response to, an actual vendor-side change in the last 12 months — **L5**.

## 11. Independent Test
> In a non-production environment, run a fixed regression suite of representative underwriting/AML/advice prompts against both the currently pinned model version and the latest available vendor version, within the provider's published usage terms and under the firm's own contract (METHODOLOGY_STANDARDS.md §3), or, where the vendor does not permit version selection, against captured historical outputs for the same prompts. Measure: (1) rate and materiality of output divergence; (2) any newly-enabled behaviour (task completion the prior version refused or could not perform); (3) whether the firm's canary/regression process would have caught the divergence pre-cutover; (4) whether a re-approval gate exists and would have been triggered. Methodology informed by longitudinal drift measurement (Chen et al., 2023). Test executed entirely in staging using historical output logs and non-production API calls. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (documented that hosted models drift over time; test design and materiality thresholds are institution-specific and rely on professional judgement; no standard benchmark for capability-delta detection exists).

## 12. Pass Indicators
- Production traffic is version-pinned; roll-forward is a deliberate, logged, governed act.
- A canary/regression suite runs on every release before cutover, with documented pass/fail criteria and results retained.
- Contractual advance-notice rights exist and have been exercised at least once (evidenced, not merely stated).
- A capability-delta re-approval gate exists in policy and has been demonstrably exercised for at least one past release.
- Post-release monitoring shows no undetected material behavioural drift over the last 12 months, or drift was detected and governed.

## 13. Fail Indicators
- Production traffic auto-updates to new vendor versions with no pinning, canary testing, or notice.
- No regression suite exists, or it covers only functional correctness and not behavioural/safety dimensions.
- Contractual terms are silent on advance notice of model changes.
- No capability-delta re-approval process exists; approval is treated as a one-time event regardless of subsequent vendor changes.
- Historical evidence shows a vendor-side change reached production and was discovered only via customer complaint or anomalous output pattern.

## 14. Reporting Language
**Pass:** "Model version pinning, pre-cutover canary testing and contractual advance-notice rights are operational and evidenced. A capability-delta re-approval gate has been exercised for the most recent vendor release with no undetected material behavioural drift in the last 12 months. Conclusions rest on ★2 methodology — institution-specific test design with no standard benchmark — and should be refreshed at each release cycle."

**Fail:** "Production traffic auto-updates to new vendor model versions with no version pinning, canary testing or contractual notice. No capability-delta re-approval process exists. This means vendor-side changes can silently alter production AI behaviour, bypassing the firm's model risk governance entirely; remediation (version pinning, regression testing, contractual rights) is required before continued reliance can be assured."

**Partial:** "Version pinning exists for [x]% of production endpoints but canary regression testing is not yet applied to [the remainder / a specific business line]. The assurance objective is not fully met until behavioural regression coverage is equivalent across all endpoints; interim reliance should be restricted to pinned, tested endpoints."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (single-line disruption or delayed detection; moderate operational impact)
  Likelihood: 2 (plausible if pinning/canary controls lapse; requires vendor to ship a
              material change without prior firm assessment)
  Detectability: 2 (canary testing and post-release monitoring surface changes within days)
  Recoverability: 2 (rollback to pinned prior version is generally straightforward)
  Novelty: 3 (the concept of an externally-controlled "black box" changing behaviour without
              any firm-side action is outside traditional change-management intuition)

Interpretation: acceptable residual risk with pinning, canary testing and contractual rights
in place; highest concern is Novelty — governance teams assume change control applies only
to firm-initiated changes.

If controls are absent or degraded:
  Severity: 4 (systemic, undetected behavioural change across an entire production book)
  Likelihood: 4 (vendors release frequently; without pinning, every release is an unassessed
              change)
  Detectability: 4 (silent; discovered only via complaint, anomaly, or forensic review)
  Recoverability: 3 (requires identifying the exposure window and affected decisions
              retrospectively)
  Novelty: 3
Residual risk: Critical. Deployment gate should not be passed without pinning and canary
testing.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Silently expanded capability can affect an entire book of underwriting/AML/advice interactions before detection; regulatory notice risk under SS1/23. |
| **Likelihood** | 2 | Requires a material vendor-side change to reach production undetected; plausible where pinning/canary controls are absent, which is common for hosted-API integrations. |
| **Detectability** | 3 | Without canary testing or monitoring, a capability change is silent — the endpoint identity is unchanged, so nothing prompts investigation. |
| **Recoverability** | 2 | Rollback to a pinned prior version is usually feasible once detected; the harder cost is identifying affected decisions in the interim. |
| **Novelty** | 3 | The assumption that model behaviour changes only when the firm changes something is deeply embedded traditional change-management thinking; AI-specific vendor-side drift is easily missed. |

## 17. Regulatory Basis
> [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024, Principle 3/4 — a model must remain validated for its intended use, which is undermined by unapproved capability change] — the closest binding UK anchor. [Bank of England FPC, "Financial Stability in Focus: Artificial intelligence in the financial system", Apr 2025] — flags vendor/model concentration and correlated behavioural risk at a systemic level, supporting firm-level version-control expectations. No regulation names "capability-delta re-approval" explicitly; this IRQ operationalises SS1/23's ongoing-validation principle for externally-hosted models. (verified 29 Jul 2026)

## 18. Research Basis
> [Chen, L., Zaharia, M., Zou, J., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009; Harvard Data Science Review 6(2), 2024] — empirically demonstrates the same nominally-versioned API endpoint drifting materially in accuracy and behaviour across months, directly evidencing the mechanism this IRQ addresses. [Incident: xAI Grok "MechaHitler" episode, Jul 2025 — on xAI's account, an upstream code-path update that unexpectedly incorporated deprecated instructions into the production bot's behaviour for 16 hours, publicly documented] — illustrates that a change reaching production upstream of an unchanged model can alter a deployed system's behaviour materially: a real, recent, high-severity occurrence. xAI states that changes to the bot are evaluated and tested before release and does not say whether this update was.
>
> **[FAIAS Incident Register, row 24, "xAI Grok system-prompt change", 2025]** — the register entry for the incident named immediately above: on xAI's account, an upstream code-path update that unexpectedly incorporated deprecated instructions into the production bot's behaviour for 16 hours, the register's transferable reading being that prompt and configuration changes are model changes and require the same release governance. Recorded as the register linkage for the citation above; it introduces no source, finding or date this field did not already carry.
>
> **Release-driven-change methodology addition (v1.2.0).** [Chen, Y. (Alibaba Group), Zhang, W. (Cheung Kong Graduate School of Business), 2026, "UpgradeBench", arXiv:2608.20918v1, 21 August 2026] is a 33-episode longitudinal benchmark of what happens to a fine-tuned specialist when the base model is upgraded, across four consecutive Qwen releases plus documented OLMo checkpoints, with released artefacts: "We release per-example predictions, cost logs, split manifests, and the evaluation harness". It is the first released benchmark addressing the decision this IRQ governs — whether to freeze, port, refresh or retrain after an announced release — and it is therefore the nearest published methodology to the capability-delta assessment tested in §11. **Scope, stated precisely:** the paper concerns the migration decision after a *disclosed* release, not the detection of an *undisclosed* provider-side change; it is open-weight (Qwen/OLMo) rather than hosted-frontier-API; and it measures which migration strategy minimises regret on general machine-learning tasks (text-to-SQL, intent classification), not whether a vendor release has introduced unapproved capability into a financial-services decision system. Those are adjacent questions, not the same one. It was added at v1.2.0 as a secondary reference at IRQ-TPR-004. It is not a source on silent vendor-side drift: UpgradeBench is a single v1 preprint with no peer-review statement, and it concerns a *disclosed* release. The `[UNVERIFIED — no confirmed peer-reviewed source specifically on silent vendor-side LLM drift …]` tag that IRQ-TPR-004 carried at v1.2.0 has since been removed on two other, peer-reviewed studies cited at its field 18. Whether a released longitudinal benchmark falsifies this canvas's ★2 clause "no standard benchmark for capability-delta detection exists" is an open question; **★2 is unchanged.**
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)
>
> **URO-3: UpgradeBench, arXiv:2608.20918v1, 21 August 2026 — whether this canvas's research basis should carry a named benchmark for the post-release re-approval decision, and whether the rating moves — resolve by 2027-03-11.** The ★ above stands untouched while this observation is open (§6A.2).

## 19. Related IRQs
```
  - IRQ-TPR-004 (F.2: silent provider-side change detection — the upstream control this IRQ depends on)
  - IRQ-MOD-013 (B.6: prompt/config change control — the firm-side analogue of this vendor-side risk)
  - IRQ-GOV-003 (I.2: technical enforcement of approval conditions post-update)
  - IRQ-HUM-001 (D.1: reviewers calibrated on the prior model version may accept unfamiliar output — the human-review step in this IRQ's failure chain)
  - IRQ-MOD-001 (B.1: capability envelope definition — this IRQ concerns unapproved *expansion* of that envelope)
  - IRQ-RES-005 / IRQ-RES-006 (G.3: monitoring for behavioural drift, incl. gradual decay)
```

## 20. References
```
[1] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over Time?"
    arXiv:2307.09009. Published in Harvard Data Science Review 6(2), 12 March 2024,
    https://doi.org/10.1162/99608f92.5317da47.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] Bank of England, Financial Policy Committee, 2025. "Financial Stability in Focus:
    Artificial intelligence in the financial system." April 2025.
[4] The Guardian, 2025. "Musk's AI firm forced to delete posts praising Hitler from Grok chatbot."
    9 July 2025. https://www.theguardian.com/technology/2025/jul/09/grok-ai-praised-hitler-antisemitism-x-ntwnfb
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.1 (Model domain, Capability Uncertainty)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional change management assumes nothing changes unless the
  firm changes it; vendor-side silent capability drift on a hosted model is AI-specific and
  counter-intuitive.
✓ Test 2 (Plausible Harm): Empirically documented (Chen et al., 2023) and illustrated by a
  real, recent, high-severity incident (xAI Grok, Jul 2025).
✓ Test 3 (Testable): Fully testable via canary regression comparison in staging; no
  production access required.
✓ Test 4 (Decision-Relevant): Outcome gates whether version pinning, canary testing and
  contractual notice rights are adequate before continued reliance on a hosted model.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-12): Field 18 — UpgradeBench (Chen & Zhang, arXiv:2608.20918, 21 Aug 2026; harness, per-example predictions, cost logs and split manifests released) added as the nearest published methodology for release-driven capability change, with its scope limits stated (disclosed releases, open-weight models, general-ML tasks) and an explicit statement that it does not clear IRQ-TPR-004's UNVERIFIED tag on silent provider-side drift. ★2 unchanged; the ★ question held for the owner. §20 reference [3] (erratum, 14 September 2026): the BoE FPC title corrected to "Artificial intelligence in the financial system", the title §17 already carried and the v1.1.1 closure verified.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form (row 24, xAI Grok system-prompt change) beside the existing free-text citation of the same incident, as a register linkage. Erratum in the same field: the free-text citation described the episode as an un-gated system-prompt change that removed behavioural constraints in production and read it as a change reaching production without release governance; on xAI's own account of 12 July 2025 an upstream code-path update unexpectedly incorporated deprecated instructions into the production bot's behaviour for 16 hours, and xAI does not say whether that update was tested before release. Both citations now carry that account. Field 20 — erratum: reference [4]'s title corrected to the article's headline. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 — wording only: a pending question is now recorded as an open question. Research Basis unchanged; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 19 Related IRQs — IRQ-HUM-001 added: the failure chain names it, and field 19 now lists every IRQ the chain names. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Fields 9, 18 and 20 — the Chen, Zaharia and Zou citation (arXiv:2307.09009) now also gives its publication in Harvard Data Science Review 6(2), 2024. The UpgradeBench note no longer describes the silent-drift UNVERIFIED tag at IRQ-TPR-004 as standing; it says that UpgradeBench is not a source on silent vendor-side drift and that the tag has been removed there. Research-basis review date moved. ★2 unchanged.
```

---
---

