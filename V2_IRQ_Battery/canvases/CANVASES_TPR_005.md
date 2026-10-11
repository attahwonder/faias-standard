# CANVAS: IRQ-TPR-005

## 1. IRQ ID & Title
**IRQ-TPR-005: Unverified Open-Source Model Provenance**

Register question: "For open-source models, is provenance verified — publisher authenticity, weight integrity, licence terms, and screening for known backdoors or unsafe fine-tunes?"

## 2. Business Activities Affected
- **Internally hosted AI capabilities:** Firms deploying open-weight models (for cost, data-residency or customisation reasons) inherit whatever integrity and safety properties the published weights actually carry, not what the model card claims.
- **Fine-tuned derivative models:** A firm fine-tuning an open-source base model inherits any backdoor, bias or licence encumbrance present in the base weights.
- **Any downstream decisioning process** built on an internally hosted open-source model carries this provenance risk forward invisibly.

## 3. AI Behaviour(s)
- Firm downloads model weights from a public repository (e.g. a model hub) and deploys them, with the model's behaviour determined by whatever training and modification the weights actually underwent — potentially including undisclosed fine-tuning by an intermediate party.
- Model executes locally with full access to firm infrastructure and data, unlike a hosted API where the provider retains operational control.
- Serialisation/loading process may itself execute arbitrary code if the artefact format is unsafe (pickle-based formats).

## 4. Failure Mode
> An open-source model is deployed into the firm's environment without verified publisher authenticity, weight integrity, licence clarity, or screening for backdoors and unsafe fine-tunes, so the firm cannot establish that the model it is running is the model it believes it downloaded, safe to execute, or lawfully licensed for its intended use.

## 5. Potential Consequences
- **Institution:** Deployment of a model artefact containing a backdoor or malicious fine-tune that behaves normally under testing but triggers harmful behaviour on specific inputs; licence breach exposure if terms are incompatible with commercial FS use.
- **Customer:** Undetected behavioural anomalies from an unsafe fine-tune propagate into customer-facing decisions.
- **Security:** Malicious serialisation formats can achieve remote code execution on load, a direct infrastructure compromise vector distinct from model behavioural risk.

## 6. Failure Chain
```
Open-source model selected for cost/customisation/data-residency
reasons; intake process treats it as "just a file download"
  ↓ (IRQ-DAT-001: lineage/provenance not captured at intake)
Weights loaded without publisher authenticity check, integrity hash
verification, or safe-serialisation-format screening
  ↓ (IRQ-SEC-009: artefact supply-chain integrity not enforced)
Model deployed; either (a) unsafe serialisation format executes
malicious code on load, or (b) an undisclosed backdoor/unsafe
fine-tune produces anomalous behaviour on trigger inputs
  ↓
Infrastructure compromise, or a downstream decision is corrupted by
model behaviour the firm never tested for

Control Breakpoints:
  • IRQ-TPR-005: provenance and integrity verification gate at intake
  • IRQ-SEC-009: artefact signing, scanning, trusted registry use
  • IRQ-DAT-001: lineage capture extended to open-source model intake
```

## 7. Why a Domain Expert May Miss It
- "Open source" is often equated with "transparent and therefore trustworthy" by non-specialists, when in fact open weights can be silently modified, backdoored, or falsely attributed to a reputable publisher without any of the code-review norms of open-source software.
- Traditional software supply-chain security (dependency scanning, SBOM) does not natively cover model weight files; security teams may screen the surrounding code but not the weights themselves.
- Model licences (e.g. research-only, non-commercial, or "responsible AI" use restrictions) are often overlooked by technical teams focused on technical integration, not legal review.
- Unsafe serialisation formats (pickle-based) are a known but non-obvious code-execution risk that a data scientist loading a model file may not recognise as a security event, distinct from data science risk.

## 8. Assurance Objective
**AO-TPR-005:** The firm shall verify publisher authenticity, weight integrity, licence compatibility and freedom from known backdoors or unsafe fine-tunes for every open-source model before deployment, and shall use safe serialisation/loading practices.

## 9. Expected Controls (Traced)
- **Artefact integrity verification (signing, hashing, trusted registries)** — [linked IRQ-SEC-009] — [OWASP Machine Learning Security Top 10, ML06:2023 ML Supply Chain Attacks] — verify artefact provenance and integrity before deployment.
- **Safe serialisation format enforcement** — [OWASP Top 10 for LLM Applications 2025, LLM03:2025 Supply Chain — unsafe model serialisation formats] — avoid unsafe pickle-based formats in favour of safetensors or equivalent; scan artefacts before loading.
- **Licence compatibility review** — [linked IRQ-DAT-001] — legal review of model licence terms against intended commercial FS use prior to deployment.
- **Publisher authenticity verification** — Emerging Practice, informed by model hub verified-publisher features and cryptographic signing where available — no single FS regulatory standard mandates this specifically.
- **Backdoor/unsafe fine-tune screening** — Emerging Practice — behavioural red-teaming against known trigger-pattern classes; research area is active but no agreed FS-sector benchmark exists.

## 10. Expected Evidence (Tagged L1–L5)
- Model hub listing showing "verified" badge, accepted without further check — **L1**.
- Firm's open-source model intake policy specifying required provenance/integrity/licence checks — **L2**.
- Sampled intake file for a deployed open-source model, evidencing hash verification, licence review and serialisation-format screening — **L3**.
- Security assessment/red-team report on the deployed model, including backdoor-trigger screening results — **L4**.
- Artefact registry log showing integrity verification status for all open-source models in production over the last 12 months — **L5**.

## 11. Independent Test
> For a sample of deployed open-source models, independently verify: (a) publisher authenticity against the claimed source, (b) weight file hash against a known-good reference where available, (c) serialisation format safety, (d) licence terms against intended use. Where feasible, run a bounded behavioural probe for known trigger-pattern backdoor classes on a non-production instance. Test executed in isolated staging environment. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (OWASP ML Top 10 provides a structured checklist for supply-chain and deserialisation risk — ★3 for that component; backdoor/unsafe-fine-tune behavioural screening remains bespoke research-grade testing — ★1–2 — blended rating reflects the weaker component dominating overall confidence).

## 12. Pass Indicators
- All sampled open-source models show verified publisher authenticity and matching integrity hashes.
- No unsafe (pickle-based) serialisation formats found in production without a mitigating scan step.
- Licence terms are documented and confirmed compatible with commercial FS use for every deployed model.
- Backdoor/trigger screening finds no anomalous behaviour on the tested probe set.

## 13. Fail Indicators
- Deployed models lack any integrity verification; provenance rests solely on the download source's reputation.
- Unsafe serialisation formats are loaded without scanning.
- Licence terms are undocumented or incompatible with intended commercial use.
- No screening for backdoor/trigger behaviour has ever been performed on deployed open-source models.

## 14. Reporting Language
**Pass:** "Sampled open-source models show verified publisher authenticity, matching integrity hashes, safe serialisation handling, and documented licence compatibility. Behavioural trigger-pattern screening found no anomalies on the tested probe set. Supply-chain component of this assessment rests on ★3 (OWASP ML Top 10-anchored); backdoor-screening component rests on ★1–2 (bespoke, no agreed benchmark) — treat backdoor-freedom findings as indicative, not conclusive."

**Fail:** "Sampled open-source models were deployed with no integrity verification, and at least one uses an unsafe serialisation format loaded without scanning. Licence terms have not been reviewed against intended commercial use. This is a critical supply-chain gap combining security (code execution risk) and legal (licence breach) exposure."

**Partial:** "Provenance and integrity verification are applied to newly onboarded open-source models under the current policy but not retrospectively to models deployed before the policy existed. Remediation plan should prioritise retrospective verification for production-critical legacy models."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (typically bounded to the specific model's workflow; escalates sharply if a code-execution vulnerability is present)
  Likelihood: 2 (plausible given the pace of open-source model adoption versus security screening maturity)
  Detectability: 3 (integrity verification, if run, is near-real-time; absent that, detection is incident-driven)
  Recoverability: 2 (model can be replaced/patched once an issue is found; infrastructure compromise, if it occurred, is more severe)
  Novelty: 3 (security teams familiar with software supply chain may not extend the same rigour to model weight files)

If controls are absent or degraded:
  Severity: 4 (unsafe serialisation format could yield direct infrastructure compromise; backdoored model could systematically corrupt decisions)
  Likelihood: 2 (requires either a genuinely malicious/compromised artefact or an unsafe format in the specific model chosen — not universal, but rising with adoption)
  Detectability: 4 (silent by design; a well-crafted backdoor triggers only on specific inputs and evades normal testing)
  Recoverability: 3 (infrastructure compromise or systematic decision corruption requires forensic investigation and remediation over weeks)
  Novelty: 4 (fully outside traditional model risk and even most software security review scope)

Residual risk interpretation: The security (code-execution) tail risk is the most severe element of this IRQ; even where behavioural backdoor risk is judged low-probability, serialisation-format screening should be treated as a hard gate, not a discretionary check.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Code-execution/infrastructure-compromise tail risk from unsafe serialisation is materially severe if realised |
| **Likelihood** | 2 | Plausible given open-source adoption pace outstripping security screening maturity in many firms |
| **Detectability** | 3 | Integrity checks give near-real-time detection when run; absent that, silent until incident |
| **Recoverability** | 2 | Model-level issues are replaceable; infrastructure compromise is more severe but still recoverable within a defined incident response |
| **Novelty** | 3 | Requires AI-specific supply-chain security knowledge (serialisation format risk) beyond generic software security training |

## 17. Regulatory Basis
> No FS-specific regulation directly addresses open-source model artefact integrity; this IRQ is grounded in general ICT/cyber risk management obligations ([Regulation (EU) 2022/2554, DORA, Art. 6 (ICT risk management framework) and Art. 9 (protection and prevention)] ICT risk management, extended to AI artefact supply chain) and general model risk management documentation expectations ([PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023)]) [UNVERIFIED — DORA Arts. 6 and 9 and SS1/23 do not reference open-weight model artefacts specifically; applicability is FAIAS's interpretive extension] (verified 29 Jul 2026; DORA articles re-read 8 Oct 2026; PRA SS1/23 cited as its April 2026 version).

## 18. Research Basis
> [OWASP Machine Learning Security Top 10, 2023, ML06:2023 ML Supply Chain Attacks; OWASP Top 10 for LLM Applications 2025, LLM03:2025 Supply Chain — unsafe model serialisation] document the artefact-integrity and unsafe-serialisation risks directly (entry names corrected against owasp.org, 3 October 2026). [UNVERIFIED — this remains an active, young research area; no single canonical peer-reviewed paper on backdoored open-source LLM fine-tunes was confirmed as a settled reference at time of search] (verified 29 Jul 2026).
>
> [Nikolic, I., Baluta, T., Saxena, P., 2025, "Model Provenance Testing for Large Language Models", Advances in Neural Information Processing Systems 38 (NeurIPS 2025), arXiv:2502.00706] is a peer-reviewed method for the lineage of a model. Using only black-box access, it tests whether one model is derived from another by comparing the similarity of their outputs against a baseline set by unrelated models. It reports 90–95% precision and 80–90% recall on two benchmarks of over 600 models from 30 million to 4 billion parameters. It addresses lineage, not weight integrity or backdoors, so the statement above that no settled reference on backdoored open-source fine-tunes was confirmed stands. The paper states that the implementation and the two benchmarks are at github.com/ivicanikolicsg/model_provenance_testing. No ★ change follows from this addition.
>
> **[FAIAS Incident Register, row 82, "JFrog malicious Hugging Face models", 2024]** — researchers report "around 100 instances" of malicious models on a public hub, including pickle models whose loading gives the attacker a shell, so a claim that a downloaded model is the model the firm believes it is, and is safe to execute, could not be made without checks. The researchers name no victim organisation. Carried as a secondary row: the source is the researchers' own disclosure.
>
> **[FAIAS Incident Register, row 88, "ReversingLabs nullifAI Hugging Face models", 2025]** — researchers found two Hugging Face models carrying reverse-shell payloads that the hub's own security scanning did not flag as unsafe; they were reported on 20 January 2025 and removed in less than 24 hours, the researchers call them closer to a proof of concept, and no victim is recorded. A hub's "not flagged" status was not a screening control for a firm that deployed open-source models. Carried as a secondary row: the source is the researchers' own disclosure, and no statement from the hub's operator was read.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-SEC-009 (E.3 Supply Chain & Tool Security: artefact integrity enforcement)
  - IRQ-DAT-001 (A.1 Training Data Provenance: lineage capture extended to open-source intake)
  - IRQ-TPR-001 (F.1 Due Diligence: publisher authenticity is a diligence dimension)
```

## 20. References
```
[1] OWASP Foundation, 2023. "OWASP Machine Learning Security Top 10."
    Latest release v0.3 (pre-release, 29 September 2023).
    URL: https://owasp.github.io/www-project-machine-learning-security-top-10/docs/
    Accessed: 2026-07-29

[2] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 6 and Art. 9.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[3] Nikolic, I., Baluta, T., Saxena, P., 2025. "Model Provenance Testing for Large Language Models." Advances in Neural Information Processing Systems 38 (NeurIPS 2025). arXiv:2502.00706. Code and benchmarks stated in the paper: github.com/ivicanikolicsg/model_provenance_testing.
    Published: 2025
    URL: https://arxiv.org/abs/2502.00706
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.3 (Third Party domain, Dependencies, Concentration & Data Handling)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): "Open source" is conflated with "trustworthy" absent code-review norms extending to model weights.
✓ Test 2 (Plausible Harm): Grounded in OWASP ML Top 10 documented supply-chain and deserialisation attack classes.
✓ Test 3 (Testable): Answerable via integrity verification and bounded behavioural probing.
✓ Test 4 (Decision-Relevant): Outcome gates whether an open-source model may be deployed.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 17 and 20 — DORA cited at Art. 6 (ICT risk management framework) and Art. 9 (protection and prevention), in place of Art. 9 alone, at field 17 and at reference [2]; the dated note at field 17 states what its date covers. Reference [1] names the latest release of the OWASP Machine Learning Security Top 10, v0.3 (pre-release, 29 September 2023), in place of "v0.4 (or latest)". No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citations added in the reserved form (row 82, JFrog disclosure of malicious Hugging Face models, carried as a secondary row; row 88, ReversingLabs nullifAI models, carried as a secondary row, closer to a proof of concept, with no victim recorded). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — Nikolic et al. (NeurIPS 2025) cited as a method for testing the lineage of a model, with its limit stated (lineage, not weight integrity or backdoors); the UNVERIFIED marker stands. Field 20 References — entry [3] added. Research-basis review date moved. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
```

---
---

