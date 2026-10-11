# CANVAS: IRQ-SEC-009

## 1. IRQ ID & Title
**IRQ-SEC-009: Model Artefact Supply-Chain Tampering and Deserialisation Exploits**

Register question: "Is the model artefact supply chain — weights, checkpoints, serialisation formats, dependencies — protected against tampering and known deserialisation exploits?"

## 2. Business Activities Affected
- **Any deployment using downloaded or third-party-distributed model weights:** Open-source or partner-provided model checkpoints introduce a software-supply-chain-style trust dependency distinct from API-consumed models.
- **Internal ML platform/MLOps pipelines:** Model artefacts moving through training, evaluation, and deployment pipelines are handled by tooling (serialisation libraries, package dependencies) with their own known vulnerability classes.
- **Any FS deployment using pickled/serialised Python model formats:** A specific, well-documented deserialisation exploit class applies wherever legacy or unsanitised serialisation formats are used to load model artefacts.

## 3. AI Behaviour(s)
- Model weights and checkpoints are loaded from storage into a runtime environment at deployment/inference time, via a serialisation/deserialisation process.
- Model artefacts and their dependencies (tokenizers, adapter weights, associated libraries) are typically sourced from external registries or repositories, with varying levels of provenance verification.
- The loading process itself, not just the model's learned behaviour, can be a point of code execution if the artefact or its format is malicious.

## 4. Failure Mode
> A tampered model artefact — malicious weights, a poisoned checkpoint, or a deserialisation payload embedded in a model file format (e.g. unsafe pickle) — is loaded into a production or pre-production environment, resulting in unauthorised code execution, backdoored model behaviour, or both.

## 5. Potential Consequences
- **Institution:** Unauthorised code execution on infrastructure loading the artefact — a conventional cybersecurity incident with AI-specific entry point; backdoored model behaviour that activates on specific, attacker-known triggers, evading normal evaluation.
- **Customer:** Downstream harm from either the direct compromise (lateral movement into customer-data systems) or from backdoored model behaviour affecting decisions.
- **Market/regulator:** A model-artefact-borne compromise is a textbook software-supply-chain incident applied to a new asset class; regulators increasingly expect AI artefact integrity to be treated with the same rigour as software supply chain (SBOM-equivalent expectations).

## 6. Failure Chain
```
Adversary compromises an upstream model registry, repository, or a specific
checkpoint distribution channel (or crafts a malicious file exploiting a
known deserialisation vulnerability)
  ↓ (IRQ-TPR-005: open-source/third-party provenance not verified before intake)
Tampered artefact is downloaded/ingested into the firm's ML pipeline
  ↓ (IRQ-SEC-009 — THIS IRQ: no artefact integrity verification — signing,
     scanning, safe-format enforcement — at intake or load time)
Artefact is loaded at training, evaluation, or inference time
  ↓ (deserialisation exploit executes, or backdoored weights activate on trigger)
Unauthorised code execution on infrastructure, or backdoored model behaviour
enters production undetected
  ↓
Cybersecurity incident (lateral movement, data compromise) and/or systematically
wrong model outputs on attacker-known triggers → discovered via incident
response or, for backdoors, potentially not at all without targeted testing

Control Breakpoints:
  • IRQ-TPR-005: provenance verification before any artefact intake
  • IRQ-SEC-009: artefact signing, integrity scanning, safe-format enforcement
    (e.g. safetensors over unsafe pickle), trusted-registry-only sourcing
  • IRQ-GOV-007: independent validation should include backdoor/trigger testing
    for externally-sourced checkpoints
```

## 7. Why a Domain Expert May Miss It
- ML platform teams often come from a data-science rather than a security-engineering background, and may not apply standard software-supply-chain discipline (artefact signing, SBOM, trusted registries) to model weights, treating them as data rather than as executable-adjacent artefacts.
- The specific deserialisation exploit class (arising from certain Python serialisation formats commonly used to distribute model checkpoints) is a well-documented but specialist vulnerability that a general security reviewer without ML-pipeline familiarity may not know to check for.
- Backdoored model behaviour that only activates on attacker-known triggers is, by construction, invisible to normal evaluation and testing — the model performs correctly on every benchmark and business test case except the ones the attacker chose.
- Open-source model adoption in FS is often driven by cost/capability considerations with security review treated as a standard vendor-diligence checkbox rather than an artefact-specific integrity verification exercise.

## 8. Assurance Objective
**AO-SEC-009:** Model artefacts (weights, checkpoints, serialisation formats, and their dependencies) shall be integrity-verified — via signing, scanning, safe-format enforcement, and trusted-source sourcing — before being loaded into any training, evaluation, or production environment.

## 9. Expected Controls (Traced)
- **Artefact signing and provenance verification** — [linked IRQ-TPR-005; NIST, SP 800-53 supply-chain-risk-management control family, applied by analogy to AI artefacts] — cryptographic signing and chain-of-custody verification before artefact intake, treating model weights with the same rigour as software supply chain.
- **Safe serialisation format enforcement** — [OWASP Top 10 for LLM Applications 2025, LLM03 Supply Chain] — mandated use of safe formats (e.g. safetensors) over formats with known deserialisation exploit history (e.g. unsafe pickle), across the artefact pipeline.
- **Trusted-registry-only sourcing** — [linked IRQ-TPR-005] — model artefacts sourced only from registries with published integrity/scanning practices, not arbitrary third-party distribution channels.
- **Integrity scanning at intake** — [MITRE ATLAS, technique category covering ML supply-chain compromise; NIST AI 100-2 E2025, poisoning taxonomy] — automated scanning for known malicious patterns and unexpected file structure at every artefact intake point.
- **Backdoor/trigger testing for externally-sourced checkpoints** — [linked IRQ-GOV-007; Emerging Practice] — no FS-sector-standard backdoor-detection benchmark yet exists; independent validation should include targeted adversarial probing for anomalous, trigger-conditioned behaviour on any externally-sourced model, marked as Emerging Practice given the immaturity of detection methodology.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor/registry claim that "artefacts are scanned for malware" with no detail — **L1**.
- Documentation of the artefact intake pipeline: signing, scanning, format enforcement, registry sourcing policy — **L2**.
- Code/pipeline inspection confirming signing/scanning is actually enforced (i.e. cannot be bypassed) and that unsafe serialisation formats are rejected — **L3**.
- Staging test: attempt to load a benign test artefact using an unsafe format or lacking a valid signature, confirm rejection — **L3**.
- Independent security assessment of the ML artefact supply chain — **L4**.
- Operational evidence (comparable deployment) of intake-scanning rejections or any confirmed incident — **L5**.

## 11. Independent Test
> In an isolated non-production environment: (1) attempt to load a benign, clearly-marked test artefact packaged in an unsafe serialisation format, and confirm the pipeline rejects or safely handles it without code execution; (2) attempt to load an artefact with a tampered or missing signature, and confirm rejection; (3) attempt to source an artefact from outside the approved trusted-registry list, and confirm the intake process blocks it. Where feasible, run a basic backdoor-probing test on a sample externally-sourced checkpoint (targeted adversarial input search for anomalous trigger-conditioned behaviour), acknowledging this sub-test is Emerging Practice. Methodology per OWASP LLM03:2025 (Supply Chain) and general software-supply-chain-security testing analogues (NIST SP 800-53 SR control family). No production infrastructure or real malicious payloads used; benign test artefacts only. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the format/signing/registry-enforcement sub-tests draw on mature general software-supply-chain security practice, giving reasonable confidence, but the backdoor-detection sub-test has no established methodology or benchmark specific to AI model artefacts — overall rating reflects this weaker element, per the instruction to rate honestly rather than average optimistically).

## 12. Pass Indicators
- Unsafe-format, unsigned, and untrusted-registry artefacts are all demonstrably rejected by the intake pipeline in staging.
- Artefact signing/scanning is enforced at a pipeline stage that cannot be bypassed by a direct file-system load.
- All currently deployed model artefacts confirmed sourced from the approved trusted-registry list with valid provenance records.
- Where backdoor-probing was attempted, no anomalous trigger-conditioned behaviour found (with the caveat that absence of evidence is not strong evidence given methodology immaturity).

## 13. Fail Indicators
- Any unsafe-format, unsigned, or untrusted-source artefact is successfully loaded in staging without rejection.
- Signing/scanning exists only for the primary deployment path, with an unscanned side-loading route available (e.g. direct file-system access for data scientists).
- No inventory exists of the provenance of currently deployed model artefacts.
- Backdoor-probing capability does not exist at all, and no compensating control (e.g. behavioural monitoring in production) is in place for externally-sourced checkpoints.

## 14. Reporting Language
**Pass:** "Artefact intake pipeline testing confirms rejection of unsafe-format, unsigned, and untrusted-source model artefacts, with enforcement verified to apply to all load paths. All currently deployed artefacts are confirmed sourced from the approved trusted registry with valid provenance. Testing rated ★2 overall — the format/signing/registry controls are well-evidenced against mature supply-chain-security practice, but the backdoor-probing sub-test remains Emerging Practice with no established benchmark; this caveat should accompany any pass conclusion."

**Fail:** "Testing found that [an unsafe-format / unsigned / untrusted-source] artefact was successfully loaded without rejection via [the identified path]. This represents an active model-supply-chain compromise vector requiring immediate remediation of the intake pipeline before further model deployment."

**Partial:** "Signing and format enforcement are applied to the primary deployment pipeline, but a side-loading route exists for data scientists conducting ad hoc experimentation that bypasses these controls. The assurance objective is not met until this path is either closed or brought under equivalent controls."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (unauthorised code execution or backdoored model behaviour; potential
              cybersecurity incident with AI-specific entry point)
  Likelihood: 2 (plausible but requires either registry compromise or a bypassed intake
              control; mitigated by signing/scanning/format enforcement)
  Detectability: 3 (format/signature rejection is real-time detectable; backdoored behaviour
              is much harder to detect without dedicated probing)
  Recoverability: 2 (rollback to a known-good artefact version; moderate cost)
  Novelty: 3 (requires treating model weights as a supply-chain artefact class, a framing
              still uncommon among data-science-led ML platform teams)

Interpretation: acceptable for the format/signing/registry sub-controls, which rest on mature
practice; residual concern is concentrated in backdoor detection, which remains genuinely
immature (Emerging Practice) — this should be flagged as an accepted, monitored gap rather
than a false assurance of complete coverage.

If controls are absent or degraded:
  Severity: 4 (code execution on ML infrastructure; backdoored behaviour affecting all
              downstream decisions, potentially undetected indefinitely)
  Likelihood: 3 (deserialisation exploits are well-documented and have been exploited in the
              wild against ML pipelines generally)
  Detectability: 4 (backdoored behaviour is silent by construction — evaluates correctly on
              every test except the attacker's chosen trigger)
  Recoverability: 4 (full artefact provenance audit required across all deployed models;
              potentially years-long if backdoor discovery is delayed)
  Novelty: 3
Residual risk: Critical absent basic signing/scanning/format controls, given the
silent-by-construction nature of a successful backdoor.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unauthorised code execution or backdoored model behaviour; potential for a conventional cybersecurity incident via an AI-specific entry point. |
| **Likelihood** | 2 | Plausible if controls absent but requires either upstream registry compromise or a bypassed intake path; well-mitigated by mature supply-chain-security practice applied to this artefact class. |
| **Detectability** | 3 | Format/signature violations are readily detectable in real time; backdoored behaviour is materially harder and rests on immature (Emerging Practice) detection methodology. |
| **Recoverability** | 2 | Rollback to a known-good artefact version is generally feasible and fast once the compromise is identified. |
| **Novelty** | 3 | Requires reframing model weights as a supply-chain artefact class subject to the same rigour as software dependencies — a framing gap common among data-science-led ML platform teams, though increasingly documented (OWASP 2025, LLM03). |

## 17. Regulatory Basis
> No regulation names model-artefact supply-chain integrity explicitly for AI. [DSIT, AI Cyber Security Code of Practice, Jan 2025] — secure-development principles extend to artefact supply-chain integrity. [PRA SS1/23 Model Risk Management, April 2026 (16 April 2026, updating 17 May 2023)] and [FCA/PRA operational resilience regime] — model artefact integrity sits within sound model development and operational resilience practice where in scope. General software-supply-chain-security regulatory direction (e.g. UK NCSC guidance on supply chain security) applies by analogy; no AI-artefact-specific rule yet exists. [UNVERIFIED — NCSC's Machine learning principles, 2.1 "Secure your supply chain" (Version 2.0, published 22 May 2024), address the supply chain of machine learning models, including a tampered model uploaded to a public model hub and exploits of the model serialisation process; no standalone NCSC publication on AI-model-artefact supply-chain integrity was located, and that principle sits within the wider Machine learning principles collection. Re-checked at the September 2026 refresh against NCSC's frontier-AI hub and its April–August 2026 frontier and agentic-AI blog set, including "Managing the cyber risk of agentic AI" (20 August 2026; page metadata: modified 24 August 2026): that set addresses agent containment, identity, network and compute isolation and emergency shutdown, and carries **nothing** on model-artefact integrity, so the absence of a standalone publication stands on a wider and more recent search than before. NCSC's Machine learning principles 2.1, NCSC's general supply-chain-security guidance and the DSIT AI Cyber Security Code of Practice (January 2025) remain the closest applicable sources] (re-verified 11 September 2026; NCSC Machine learning principles 2.1 read 7 October 2026).

## 18. Research Basis
> [OWASP Foundation, 2025, "Top 10 for LLM Applications 2025", LLM03 Supply Chain] — direct classification of model, dataset, and dependency supply-chain risk with mitigation guidance. [Carlini, N., et al., 2023, "Poisoning Web-Scale Training Datasets is Practical", arXiv:2302.10149] — establishes the general practicality and low cost of supply-chain-style poisoning attacks, supporting plausibility of artefact-level compromise. [MITRE ATLAS, ongoing, ML-supply-chain-compromise technique category] — adversary technique catalogue applicable to artefact tampering.
>
> [Zhao, J., Wang, S., Zhao, Y., et al., 2024, "Models Are Codes: Towards Measuring Malicious Code Poisoning Attacks on Pre-trained Model Hubs", Proceedings of the 39th IEEE/ACM International Conference on Automated Software Engineering (ASE '24), pp. 2087–2098, https://doi.org/10.1145/3691620.3695271] studies malicious code in model and dataset artefacts on Hugging Face. It describes MalHug, a pipeline that extracts dataset loading scripts, deserialises models, runs taint analysis and applies pattern matching to detect and classify malicious artefacts. The authors report running it for over three months, in collaboration with a financial technology company, on a mirror of the hub: it monitored more than 705,000 models and 176,000 datasets and found 91 malicious models and 9 malicious dataset loading scripts. It scans artefacts that are already on a hub. It does not test whether a firm's own intake process rejects an unsafe artefact, which is the test in field 11, so it informs the threat picture and the choice of scanning method and not that test. The repository that the paper names, github.com/security-pride/MalHug, holds a table that describes the detected artefacts and a README; no pipeline code is released in it, and the source files of the artefacts are on Zenodo. No ★ change follows from this addition.
>
> **[FAIAS Incident Register, row 82, "JFrog malicious Hugging Face models", 2024]** — researchers report "around 100 instances" of malicious machine-learning models on Hugging Face, among them pickle models whose loading gives the attacker a shell on the user's machine; one PyTorch model carried a reverse-shell payload. Tampered model artefacts with a deserialisation payload were available to load from a public hub; the researchers name no victim organisation, and users reported one further model as dangerously malicious, after which the hub blocked it. Carried as a secondary row: the source is the researchers' own disclosure, and no statement from the hub's operator was read.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-TPR-005 (F.3: open-source provenance verification — the upstream diligence control)
  - IRQ-DAT-006 (A.2: general data poisoning — the training-data-side analogue of artefact
    tampering)
  - IRQ-SEC-010 (E.3: MCP/tool-server supply-chain compromise — the tooling-layer analogue)
  - IRQ-GOV-007 (I.3: independent validation should include backdoor/trigger testing for
    externally-sourced checkpoints)
  - IRQ-RES-004 (G.2: rollback to a known-good artefact version as recovery mechanism)
```

## 20. References
```
[1] OWASP Foundation, 2025. "OWASP Top 10 for LLM Applications 2025." LLM03:2025 Supply
    Chain.
[2] Carlini, N., et al., 2023. "Poisoning Web-Scale Training Datasets is Practical."
    arXiv:2302.10149.
[3] MITRE, ongoing. "ATLAS." atlas.mitre.org. Accessed 2026-07-29.
[4] DSIT, 2025. "AI Cyber Security Code of Practice." January 2025.
[5] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023).
[6] Zhao, J., Wang, S., Zhao, Y., et al., 2024. "Models Are Codes: Towards Measuring Malicious
    Code Poisoning Attacks on Pre-trained Model Hubs." Proc. 39th IEEE/ACM International
    Conference on Automated Software Engineering (ASE '24), pp. 2087–2098.
    https://doi.org/10.1145/3691620.3695271. Result data only, no pipeline code:
    github.com/security-pride/MalHug.
[7] NCSC, 2024. "Machine learning principles," 2.1 "Secure your supply chain." Version 2.0, 22 May 2024.
    https://www.ncsc.gov.uk/collection/machine-learning-principles/secure-development/secure-supply-chain
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.3 (Security domain, Supply Chain & Tool Security)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Data-science-led ML platform teams often do not apply
  software-supply-chain discipline (signing, SBOM, trusted registries) to model weights,
  and the specific deserialisation exploit class is specialist knowledge.
✓ Test 2 (Plausible Harm): Grounded in OWASP LLM03:2025 classification, general
  supply-chain-poisoning research (Carlini et al. 2023), and MITRE ATLAS technique catalogue.
✓ Test 3 (Testable): Testable via staging artefact-intake rejection tests; ★2 methodology,
  honestly rated given the immaturity of backdoor-detection testing specifically.
✓ Test 4 (Decision-Relevant): Outcome gates whether an open-source or externally-sourced
  model may be loaded into any environment, and informs required intake-pipeline controls.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-12): Regulatory Basis — erratum: the NCSC absence marker re-based to
  11 Sep 2026 against NCSC's frontier-AI hub and its Apr-Aug 2026 frontier and
  agentic-AI blog set. The absence stands on the wider search; the SEC-009 gap is not
  closed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 82, JFrog disclosure of malicious Hugging Face models, carried as a secondary row on the researchers' own disclosure, with no victim recorded). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — MalHug (ASE 2024) cited with its limits stated (hub scanning, not an intake test; no pipeline code released). Field 20 References — entry [6] added. Research-basis review date moved. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 15 — controls-absent Recoverability scored 4 in place of 3. The line allows years-long recovery if discovery is delayed, which ASSURANCE_MODEL.md §7 scores 4 (irreversible or years-long recovery). Field 16, the other axes, the ★ rating and the research basis are unchanged.
- v1.3.3 (2026-10-09): Field 17 Regulatory Basis — the NCSC absence marker narrowed: NCSC Machine learning principles 2.1, Secure your supply chain (Version 2.0, published 22 May 2024), is cited as NCSC guidance on the machine learning model supply chain, and the absence claim is limited to a standalone NCSC publication on model-artefact supply-chain integrity. Field 20 References — entry [7] added. No change to controls, test, ★ rating or risk profile.
```

---
---

