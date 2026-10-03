# CANVAS: IRQ-TPR-004

## 1. IRQ ID & Title
**IRQ-TPR-004: Undetected Silent Provider-Side Model Change**

Register question: "Would a silent provider-side change to model weights, safety filters or defaults be detected by the firm before it affects customers or controls, with rollback and re-approval paths available?"

## 2. Business Activities Affected
- **Any workflow dependent on a hosted/API foundation model:** credit narrative generation, customer chat, claims summarisation and AML alert triage all rely on the deployed model behaving as approved; a provider-side update changes that behaviour without the firm's knowledge or consent.
- **Model risk approval integrity:** The approval granted at go-live is only valid for the model version tested; unversioned reliance means the approval basis silently decays.
- **Regulatory reporting/MI:** Behavioural change can shift output distributions (e.g. approval rates, sentiment) in ways that distort MI the firm reports internally or to regulators.

## 3. AI Behaviour(s)
- Firm calls a hosted model or API by name/endpoint (e.g. a model family) rather than a pinned, immutable version, or the provider updates the "latest" alias, safety filter defaults, or system prompt without notice.
- Model output distribution, refusal behaviour, tone or accuracy shifts following the change; the shift may be subtle (slow-decay) or abrupt.
- Firm's downstream systems consume the changed output identically to before, with no behavioural comparison against a baseline.

## 4. Failure Mode
> A foundation model or API provider changes model weights, safety filters or default behaviour without firm-visible notice, and the firm has no canary/behavioural monitoring or version-pinning mechanism capable of detecting the change before it affects customers or controls — nor a rollback and re-approval path to respond once detected.

## 5. Potential Consequences
- **Customer:** Behavioural drift changes decision outcomes (approval rates, tone, accuracy) for customers without any corresponding change control or re-testing.
- **Institution:** Model risk approval basis is invalidated retroactively; the firm cannot demonstrate the model in production matches the model that was approved.
- **Regulator/market:** Governance-bypass finding — a material model change occurred outside the firm's change management and re-approval process; DORA/EBA outsourcing change-management expectations breached.

## 6. Failure Chain
```
Model accessed via non-pinned endpoint or "latest" alias; contract
lacks change-notification clause (IRQ-TPR-002 gap)
  ↓ (IRQ-MOD-002: capability delta introduced without documentation/re-approval)
Provider updates weights, safety filter defaults, or backend routing
  ↓ (IRQ-RES-005: no behavioural canary/monitoring detects the shift)
Model output distribution shifts (accuracy, tone, refusal rate,
approval rate) in production, undetected
  ↓ (IRQ-MOD-013: no version-controlled regression testing catches the change)
Customers experience altered outcomes; internal MI silently reflects
the new, unapproved behaviour as if it were the approved baseline
  ↓
Discovery (via incident, customer complaint pattern, or rare manual
comparison) triggers retrospective governance failure investigation

Control Breakpoints:
  • IRQ-TPR-002: contractual notification rights create an external trigger
  • IRQ-TPR-004: version pinning and canary testing create a technical trigger
  • IRQ-RES-005/006: continuous behavioural monitoring detects drift, including slow decay
  • IRQ-MOD-013: regression testing against version-controlled baselines
```

## 7. Why a Domain Expert May Miss It
- Traditional software change management assumes the firm controls deployment timing; hosted/API AI models can change server-side at the provider's discretion, a concept unfamiliar to change-management SMEs used to on-premise or firm-controlled release cycles.
- "The API contract hasn't changed" is treated as evidence of stability, when the model behind an unchanged API can be silently swapped.
- Version pinning is available from most major providers but requires deliberate technical choice; teams optimising for "always get the latest, best model" default into exposure without recognising the governance trade-off.
- Slow-decay drift (per RES-006) is especially easy to miss because no single incident triggers investigation — the change is gradual and invisible against normal performance variance.

## 8. Assurance Objective
**AO-TPR-004:** The firm shall detect material provider-side changes to model weights, safety filters or defaults before they affect customers or controls, through version pinning and behavioural canary testing, and shall have a tested rollback and re-approval path available on detection.

## 9. Expected Controls (Traced)
- **Version pinning to immutable model identifiers** — Emerging Practice, informed by standard software supply-chain integrity principles (cf. [ISO/IEC 5338:2023] lifecycle configuration management) — avoid "latest"-alias endpoints for production-critical use cases where the provider offers pinning.
- **Behavioural canary/regression testing against a fixed benchmark set** — [linked IRQ-RES-005, IRQ-MOD-013] — periodic re-run of a fixed evaluation set against the live endpoint; alert on distributional deviation.
- **ICT change management for third-party services** — [Regulation (EU) 2022/2554, DORA, Art. 9(4)(e) ICT change management] — changes affecting critical ICT services must be identified and managed, including where the change originates with a third party.
- **Contractual advance notice of model changes** — [linked IRQ-TPR-002] — external trigger complementing technical canary detection.
- **Rollback and re-approval path** — [linked IRQ-RES-004, IRQ-MOD-013] — a tested mechanism to revert to a known-good configuration and re-trigger governance approval on detected drift.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the model hasn't changed since approval" with no supporting test evidence — **L1**.
- Design specification for version pinning and canary testing (benchmark set, cadence, alert thresholds) — **L2**.
- Staging/production canary test results over a defined period, showing baseline comparison and any deviations flagged — **L3**.
- Independent audit confirming canary testing is operating as designed across the critical-model population — **L4**.
- Production monitoring log of canary test runs over the last 12 months, with any detected provider-side changes and the resulting rollback/re-approval actions taken — **L5**.

**Dated worked example, added at the September 2026 refresh — first-party evidence of what happens upstream of the firm's endpoint.** A frontier lab's September 2026 threat report discloses that since its first disclosure in February it has "identified and disrupted additional distillation attacks against Claude from seven labs based in China", the largest attributed to operators affiliated with one named lab, whose "CoT distillation pipeline injected a fixed prompt into each request that forced" reasoning traces into a fixed form, the harvested transcripts being "used to distill Claude's capabilities" into that lab's own model line, with the campaign peaking at nearly three million exchanges per day [Anthropic, *Detecting and countering misuse of AI: September 2026*, 10 September 2026, §"Illicit distillation", printed pp. 143–147]. Beside it, a joint advisory of the US National Security Agency, Federal Bureau of Investigation and Cybersecurity and Infrastructure Security Agency addresses the same provider-side conduct [NSA/FBI/CISA, AA26-251A, 8 September 2026]. The relevance to this IRQ is directional and specific: a provider under sustained extraction pressure is a provider with a live incentive to change sampling, reasoning exposure, rate limits or output format **without announcing it**, and a canary set that fixes only accuracy and tone will not see a change in what the endpoint discloses of its own reasoning. A reviewer should ask what the provider has changed in response to extraction pressure, and whether the firm's canary design would detect it.

## 11. Independent Test
> In a non-production environment, run a fixed benchmark prompt set against the current live endpoint, within the provider's published usage terms and under the firm's own contract (METHODOLOGY_STANDARDS.md §3), and compare output distribution (accuracy, tone, refusal rate, structured-output conformance) against the archived baseline from the last approved version. Where the provider has published a model update in the review window, verify whether the firm's canary process independently detected the change and whether re-approval was triggered. No production customer data used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (research and industry practice recognise the risk of vendor-side drift; no standardised, benchmarked FS methodology exists for "silent drift detection" — largely bespoke canary design and professional judgement in threshold-setting).

## 12. Pass Indicators
- Canary testing runs on a defined cadence with documented baseline comparison; deviations trigger a defined alert and investigation.
- Version pinning is used for all production-critical model calls where the provider supports it.
- At least one instance in the review period demonstrates the canary process detecting a real provider-side change, followed by rollback/re-approval.
- Rollback path is tested (not merely documented) within a defined recovery time objective.

## 13. Fail Indicators
- No canary testing exists; the firm has no mechanism to detect provider-side change other than customer complaint or incident.
- Production calls use "latest"-alias endpoints with no version pinning available or used.
- A known provider model update occurred in the review period with no corresponding internal detection or re-approval record.
- Rollback path is undocumented or untested; no defined recovery time objective exists.

## 14. Reporting Language
**Pass:** "Version pinning is applied to production-critical model calls, and canary testing on a fixed benchmark set has demonstrated the ability to detect provider-side behavioural change, triggering rollback and re-approval within the review period. Conclusions rest on ★2 methodology — bespoke canary design, professional-judgement-driven — and should be interpreted as a point-in-time capability demonstration, not a guarantee against undetected future drift."

**Fail:** "No canary testing or version pinning is in place; the firm has no mechanism to detect provider-side model changes before they reach customers. A known provider model update in the review window produced no corresponding internal governance action. This is a critical gap: the firm cannot evidence that the model in production matches the model it approved."

**Partial:** "Canary testing exists for the flagship production model but not for secondary/embedded uses of the same provider (e.g. internal tooling); version pinning is inconsistently applied. Remediation should extend canary coverage to all production-critical endpoints."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (behavioural shift typically gradual and bounded; escalates if it affects a high-materiality decision workflow)
  Likelihood: 2 (providers do update models periodically; canary testing catches material shifts before customer impact)
  Detectability: 2 (canary testing provides near-real-time detection when operating)
  Recoverability: 2 (rollback to a pinned prior version is achievable within hours if rehearsed)
  Novelty: 4 (domain expert very likely to miss; server-side model change is an AI-specific supply-chain concept absent from traditional change management)

If controls are absent or degraded:
  Severity: 3 (multiple customers affected by an undetected, unapproved behavioural shift in a material decision workflow)
  Likelihood: 3 (probable — major providers update models on a regular cadence; without pinning/canary, exposure is continuous)
  Detectability: 4 (silent by nature, especially for gradual/slow-decay drift; discovered only via incident or rare manual audit)
  Recoverability: 3 (rollback untested means recovery time is unpredictable, likely days; re-approval process may itself be undefined)
  Novelty: 4 (fully outside traditional change-management training)

Residual risk interpretation: This is one of the highest-novelty, highest-detectability-risk IRQs in the domain; canary testing maturity should be prioritised even though it is currently only ★2-rated methodology.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Typically a gradual, bounded shift unless the affected workflow is high-materiality |
| **Likelihood** | 2 | Real and periodic given provider release cadences, mitigated where canary testing is active |
| **Detectability** | 4 | Silent by design absent active canary testing; slow-decay variant is especially hard to catch |
| **Recoverability** | 2 | Fast if version pinning/rollback is rehearsed; slow and uncertain otherwise |
| **Novelty** | 4 | Server-side, provider-controlled model change is unfamiliar territory for traditional change management |

## 17. Regulatory Basis
> [Regulation (EU) 2022/2554, DORA, Art. 6 (ICT risk management framework) and Art. 9(4)(e) (ICT change management)] require an ICT risk management framework including change management covering ICT services, extending in principle to third-party model changes. No FS regulator has published AI-specific guidance mandating canary/drift-detection testing for hosted models; this IRQ addresses a governance-continuity risk under general model risk management expectations ([PRA SS1/23, Principle 4 (independent model validation, including ongoing monitoring)] applied to vendor-hosted models — the PRA states the principles apply to models whether developed in-house or externally, including vendor models; only the application to hosted-model drift specifically is FAIAS's interpretive extension) [UNVERIFIED — sub-clause pinpoint not confirmed against primary text] (verified 29 Jul 2026).

## 18. Research Basis
> The risk of silent vendor-side model drift is documented in industry and academic commentary on "model versioning" and "LLM behavioural drift" [UNVERIFIED — no confirmed peer-reviewed source specifically on silent vendor-side LLM drift was located after search; closest related work is general LLM-evaluation/benchmark-drift literature, not a named study of this exact phenomenon] (verified 29 Jul 2026). This IRQ is grounded in the general software supply-chain integrity principle (unpinned dependencies introduce undetected behavioural change) applied to hosted AI models, and in BoE FPC's concentration/monitoring framing of AI/cloud provider dependency (Financial Stability in Focus, April 2025).
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)
>
> **URO-3 (secondary): UpgradeBench, arXiv:2608.20918v1, 21 August 2026 — whether released-benchmark evidence bears on this canvas's question; it does not clear the `[UNVERIFIED — no confirmed peer-reviewed source]` tag, which requires a confirmed peer-reviewed source on silent provider-side change — resolve by 2027-03-11.** Primary home is IRQ-MOD-002. The ★ above stands untouched (§6A.2).

## 19. Related IRQs
```
Related IRQs:
  - IRQ-MOD-002 (B.1 Capability Uncertainty: capability deltas require re-approval)
  - IRQ-MOD-013 (B.6 Model Updates & Configuration: version-controlled regression testing)
  - IRQ-RES-005 (G.3 Monitoring & Alerting: continuous behavioural monitoring)
  - IRQ-RES-006 (G.3 Monitoring & Alerting: slow-decay detection specifically)
  - IRQ-TPR-002 (F.1 Contracts & Licensing: contractual notification as external trigger)
  - IRQ-TPR-001 (F.1 Due Diligence: which access tier a provider or its sub-provider operates on is a diligence fact bearing on what a silent change could consist of)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Arts. 6 and 9(4)(e).
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] Prudential Regulation Authority, 2023. "SS1/23 — Model risk management principles for banks."
    Published: May 2023
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss

[3] Bank of England, Financial Policy Committee, 2025. "Financial Stability in Focus: Artificial intelligence in the financial system."
    Published: April 2025
    URL: https://www.bankofengland.co.uk/financial-stability-in-focus/2025/april-2025
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.2 (Third Party domain, Model Change Management)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Traditional change management assumes firm-controlled deployment timing; provider-side change is invisible to that mental model.
✓ Test 2 (Plausible Harm): Grounded in DORA change-management obligations and BoE FPC's AI/cloud concentration monitoring framing.
✓ Test 3 (Testable): Answerable via canary benchmark comparison against archived baseline.
✓ Test 4 (Decision-Relevant): Outcome gates whether continued reliance on unpinned endpoints is acceptable.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Expected Evidence — dated worked example added on provider-side extraction pressure (illicit-distillation disclosure naming seven China-based labs and one named campaign, 10 Sep 2026) with the NSA/FBI/CISA advisory AA26-251A (8 Sep 2026) beside it. Related IRQs — TPR-001 added. Research Basis — the URO-3 (secondary) flag recorded against UpgradeBench (arXiv:2608.20918v1, 21 August 2026), whose primary home is IRQ-MOD-002; the ★ above stands untouched under §6A.2 and the silent-drift UNVERIFIED marker is not discharged. ★2 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

