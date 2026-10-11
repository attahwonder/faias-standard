# CANVAS: IRQ-DAT-006

## 1. IRQ ID & Title
**IRQ-DAT-006: Undetected Tampering Through Ingestion, Labelling and Curation Pipelines**

Register question: "Could a poisoned or tampered record introduced through data ingestion, labelling or curation pipelines persist undetected into training data or the knowledge store?"

## 2. Business Activities Affected
- **Fraud/AML model retraining:** Ingestion pipelines pulling from internal case systems, vendor feeds and analyst annotations are all points where a manipulated record (e.g. mislabelled fraud case) can enter and persist.
- **RAG knowledge-store population:** Document ingestion into policy/product knowledge stores is a supply-chain step where a tampered or malicious document can enter without integrity checking.
- **Any fine-tuning pipeline sourcing from crowdsourced, outsourced or multi-party contributed data:** Instruction-tuning or labelling contributions from external or lightly-vetted contributors are a documented backdoor vector.

## 3. AI Behaviour(s)
- Ingests records from upstream systems, feeds and annotation workflows, trusting that curation steps have already filtered for integrity.
- Trains or grounds on whatever passes through ingestion, with no innate ability to detect that a specific record was deliberately or accidentally tampered with.
- Can encode a backdoor or persistent bias from a small number of poisoned records without visible degradation in aggregate metrics.

## 4. Failure Mode
> A poisoned, tampered or maliciously crafted record enters the data supply chain via ingestion, labelling or curation and persists undetected into training data or the knowledge store, because no integrity screening, anomaly detection or source vetting intercepts it.

## 5. Potential Consequences
- **Institution:** A backdoored model exhibits attacker-chosen behaviour under a specific trigger condition, undetectable through normal validation; discovered only via incident or targeted red-team.
- **Customer:** Specific customers or transaction patterns matching the poison trigger receive manipulated decisions (e.g. fraud model trained to systematically miss a specific typology).
- **Regulator:** Supply-chain integrity failure under EU AI Act Art. 10 and PRA SS1/23 data-governance expectations; potential AML/CTF control failure if the poisoned model is transaction-monitoring-facing.

## 6. Failure Chain
```
Data enters via ingestion, labelling or curation pipeline from an
internal, crowdsourced, vendor or web-sourced contributor
  ↓ (IRQ-DAT-006 — THIS IRQ: no integrity screening, checksum or anomaly
     detection intercepts a tampered/poisoned record)
Poisoned record enters training data or knowledge store undetected
  ↓ (IRQ-DAT-001: lineage capture would have flagged an unvetted source,
     but is itself absent or bypassed)
Model trains on or retrieves the poisoned content; backdoor or bias
encoded, invisible in aggregate validation metrics
  ↓ (IRQ-MOD-011: evaluation does not specifically test for backdoor triggers)
Attacker (or accidental trigger condition) activates the poisoned
behaviour in production
  ↓
Manipulated decision, missed AML typology, or systematic bias
→ financial loss, regulatory breach, reputational damage

Control Breakpoints:
  • IRQ-DAT-006: integrity screening (checksums, anomaly detection, source vetting) at intake
  • IRQ-DAT-001: lineage capture flags unvetted/unknown sources
  • IRQ-MOD-011: evaluation specifically includes backdoor/trigger-condition testing
```

## 7. Why a Domain Expert May Miss It
- FS data-quality teams check for completeness, format and business-rule validity, not for deliberately crafted adversarial content designed to look statistically normal.
- The scale finding that poisoning requires only a small, near-constant number of documents regardless of model size (Souly et al., 2025) overturns the intuitive "dilution" assumption that large training sets are naturally protected — an assumption most SMEs still hold.
- Backdoors can survive standard safety/fine-tuning processes (Hubinger et al., "Sleeper Agents"), so "we retrained/fine-tuned since" is not the reassurance it intuitively seems.
- Crowdsourced or outsourced labelling is a normal, budget-driven practice; the security implications of who contributes labels are rarely part of the vendor-selection conversation.

## 8. Assurance Objective
**AO-DAT-006:** Data entering the training or knowledge-store supply chain via ingestion, labelling or curation shall pass integrity screening (source vetting, anomaly detection, checksum/consistency checks) before being incorporated, such that tampered or poisoned records cannot persist undetected.

## 9. Expected Controls (Traced)
- **Source vetting and access control on ingestion pipelines** — [NIST AI 100-2 E2025, adversarial ML taxonomy, poisoning mitigations] — only vetted, access-controlled sources feed training or knowledge-store pipelines.
- **Statistical anomaly detection on incoming records** — [Carlini et al., 2023, "Poisoning Web-Scale Training Datasets is Practical"] — outlier/anomaly screening applied to detect statistically unusual records consistent with poisoning patterns.
- **Checksum and provenance consistency checks** — [linked IRQ-DAT-001] — records without a traceable, consistent source are quarantined pending review.
- **Backdoor/trigger-condition testing at evaluation** — [Hubinger et al., 2024, "Sleeper Agents", arXiv:2401.05566; Gu et al., 2017, "BadNets"] — evaluation specifically probes for anomalous trigger-conditioned behaviour, not just aggregate accuracy.
- **Minimum poison-resistance awareness in scaling assumptions** — [Souly et al., 2025, "Poisoning Attacks on LLMs Require a Near-constant Number of Poison Samples", arXiv:2510.07192] — data-governance policy explicitly rejects the assumption that larger training sets dilute poisoning risk.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "our data pipeline is secure" with no detail — **L1**.
- Ingestion pipeline architecture documentation showing where (if anywhere) integrity screening is applied — **L2**.
- Code/config inspection confirming anomaly detection and source vetting actually execute before data reaches training/knowledge-store — **L3**.
- Staging test results: seeded poisoned records injected into a test ingestion pipeline; detection rate measured — **L3**.
- Independent security assessment of the data supply chain, covering ingestion, labelling and curation stages — **L4**.
- Production incident/anomaly logs showing screening has been triggered and investigated over a defined period — **L5**.

## 11. Independent Test
> In an isolated non-production ingestion pipeline, seed a set of tampered/poisoned records (label-flipped examples per Wan et al., 2023 instruction-tuning poisoning patterns; anomalous outlier records; trigger-phrase-bearing documents per BadNets-style patterns) alongside clean data. Measure: (1) detection/quarantine rate by the anomaly-detection and source-vetting controls; (2) whether any poisoned record reaches the training/knowledge-store stage undetected; (3) if a model is trained on a partially-undetected poison set, whether post-training evaluation with trigger-condition probing surfaces the backdoor. Methodology draws on Wan et al. (2023), Gu et al. (2017, BadNets) and Souly et al. (2025) poison-sample-count findings. No production data or systems used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (research base is credible and well-published, but poisoning-detection test design is institution-specific and evolves with attack sophistication; no cross-institution consensus benchmark exists for FS data-pipeline poison detection).

## 12. Pass Indicators
- 100% of seeded poisoned/tampered records in the staging test are quarantined or flagged before reaching training/knowledge-store status.
- Anomaly detection and source vetting are demonstrably invoked on every ingestion path, not only the primary one.
- Trigger-condition evaluation testing finds no anomalous conditioned behaviour in the resulting model.
- Crowdsourced/outsourced labelling contributors are vetted and their contribution volume/pattern monitored for anomalies.

## 13. Fail Indicators
- Any seeded poisoned record reaches the training set or knowledge store undetected in staging testing.
- Anomaly detection exists on the primary ingestion path but not on secondary paths (vendor feeds, crowdsourced labelling, ad hoc bulk uploads).
- Evaluation testing covers only aggregate accuracy, with no trigger-condition or backdoor-specific probing.
- Data governance assumes "our training set is too large to poison meaningfully" — contradicted by the near-constant poison-sample-count finding.

## 14. Reporting Language
**Pass:** "Integrity screening on the data ingestion pipeline detected [x]% of seeded poisoned records in staging testing, with none reaching the training set or knowledge store undetected. Trigger-condition evaluation of the resulting model found no anomalous conditioned behaviour. This is ★2 professional-judgement testing given the absence of a cross-institution benchmark; screening effectiveness should be re-tested as poisoning techniques evolve."

**Fail:** "Staging testing demonstrated that seeded poisoned records reached the training data/knowledge store undetected via [ingestion path], because no anomaly detection or source vetting is applied there. Given research evidence that a near-constant, small number of poisoned documents can backdoor a model regardless of overall training-set size, this represents a credible route to undetected manipulated model behaviour requiring immediate remediation."

**Partial:** "Integrity screening is effective on the primary internal ingestion path but absent from the crowdsourced/vendor-labelling path, through which [x]% of new training records arrive. The assurance objective is not met until coverage is equivalent across all ingestion paths."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (attacker-chosen trigger-conditioned behaviour affecting a subset of decisions;
              regulatory breach risk if AML/fraud detection is the affected system)
  Likelihood: 2 (requires an adversary with write/contribution access to an ingestion path;
                 plausible given crowdsourced/vendor labelling is common)
  Detectability: 3 (backdoors are specifically designed to be invisible to aggregate metrics;
                    requires deliberate trigger-condition testing)
  Recoverability: 2 (remediable via retraining on cleaned data once identified)
  Novelty: 4 (poisoning-resistance requires AI-security-specific knowledge; "large datasets
              are naturally robust" is a false but intuitive assumption)

If controls are absent or degraded:
  Severity: 4 (systematic manipulated behaviour in a materially important model, e.g. AML/fraud)
  Likelihood: 3 (documented low-cost feasibility: ~$60 for web-scale poisoning per Carlini et al.;
                 ~100-250 examples for instruction-tuning/backdoor per Wan et al./Souly et al.)
  Detectability: 4 (silent by design; discovered only through targeted red-team or incident)
  Recoverability: 3 (full retraining, forensic investigation of affected decisions, incident response)
  Novelty: 4
Residual risk: Critical for materially important models (fraud/AML/credit) without integrity screening.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Attacker-chosen conditioned behaviour can affect materially important decisioning (AML/fraud/credit) for a subset of cases. |
| **Likelihood** | 3 | Documented low-cost feasibility (near-constant poison-sample counts; ~$60 web-scale poisoning); crowdsourced/vendor labelling is common practice. |
| **Detectability** | 4 | Poisoning is specifically designed to evade aggregate metrics; only targeted trigger-condition testing surfaces it. |
| **Recoverability** | 2 | Remediable via retraining on cleaned/re-vetted data once identified. |
| **Novelty** | 4 | The "large training sets dilute poison" intuition is false and well-documented as false — a genuine AI-security blind spot for FS SMEs. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(f), data governance and Art. 15(5), cybersecurity resilience against data poisoning] requires examination of data for possible biases and appropriate measures against attempts to alter use, behaviour or performance including data poisoning. [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), Principle 3] data-governance expectations extend to supply-chain integrity of model-feeding data. [NIST AI 100-2 E2025, "Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations"] provides the authoritative taxonomy for poisoning attacks referenced above. (verified 29 Jul 2026)

## 18. Research Basis
> [Gu, T., Dolan-Gavitt, B., Garg, S., 2017, "BadNets: Identifying Vulnerabilities in the Machine Learning Model Supply Chain", arXiv:1708.06733] — foundational backdoor demonstration. [Carlini, N., et al., 2023, "Poisoning Web-Scale Training Datasets is Practical", arXiv:2302.10149] — web-scale datasets poisonable for ~$60 via split-view/frontrunning. [Wan, A., et al., 2023, "Poisoning Language Models During Instruction Tuning", arXiv:2305.00944] — ~100 poisoned examples manipulate instruction-tuned behaviour. [Hubinger, E., et al., 2024, "Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training", arXiv:2401.05566] — backdoors survive standard safety fine-tuning, especially in larger models. [Souly, A., et al. (UK AI Security Institute, Anthropic, Alan Turing Institute), 2025, "Poisoning Attacks on LLMs Require a Near-constant Number of Poison Samples", arXiv:2510.07192] — overturns the dilution-by-scale assumption. Two published benchmarks of backdoor attacks and defences and one evaluation programme for trojan detectors are cited as related work; none is specific to financial services. [Wu, B., et al., 2022, "BackdoorBench: A Comprehensive Benchmark of Backdoor Learning," NeurIPS 2022 Datasets and Benchmarks Track, arXiv:2206.12654] — evaluates 8 attacks against 9 defences at 5 poisoning ratios, on 5 models and 4 datasets (CIFAR-10, CIFAR-100, GTSRB and Tiny ImageNet), under one standardised protocol; code and evaluations are public. Two of its defences, activation clustering and spectral signatures, identify poisoned training samples from the feature representations of a model already trained on them; the benchmark does not test a firm's ingestion, labelling or curation pipeline. [Li, Y., et al., 2025, "BackdoorLLM: A Comprehensive Benchmark for Backdoor Attacks and Defenses on Large Language Models," NeurIPS 2025 Datasets and Benchmarks Track (poster), arXiv:2408.12798] — covers four attack modalities on text-generation models (data poisoning, weight poisoning, hidden-state manipulation and chain-of-thought hijacking) and seven mitigation techniques; code and datasets are public. Its mitigation techniques, such as fine-tuning, quantisation, pruning, decoding-time defences, CleanGen, CROW and a response-level judge, act on the trained model or at inference time, not on a record before it enters a training set or knowledge store. [National Institute of Standards and Technology, TrojAI, "Overview," pages.nist.gov/trojai] — evaluates submitted detectors on how accurately they identify whether a trained model carries a trojan, using sequestered data, in leaderboard rounds from June 2020 to October 2024; the competition is closed and its evaluation server is offline. It bears on step (3) of the test in field 11 only.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-001 (A.1: lineage capture — would flag unvetted sources)
  - IRQ-DAT-007 (A.3: RAG ingestion curation — the retrieval-store analogue)
  - IRQ-SEC-005 (E.1: inference-time RAG poisoning — the adversarial-injection variant, SEC-homed)
  - IRQ-SEC-009 (E.3: model artefact supply-chain integrity — the weights/checkpoint analogue)
  - IRQ-MOD-011 (B.5: evaluation integrity must include trigger-condition testing)
```

## 20. References
```
[1] Gu, T., Dolan-Gavitt, B., Garg, S., 2017. "BadNets: Identifying Vulnerabilities in the
    Machine Learning Model Supply Chain." arXiv:1708.06733.
[2] Carlini, N., et al., 2023. "Poisoning Web-Scale Training Datasets is Practical." arXiv:2302.10149.
[3] Wan, A., et al., 2023. "Poisoning Language Models During Instruction Tuning." arXiv:2305.00944.
[4] Hubinger, E., et al., 2024. "Sleeper Agents: Training Deceptive LLMs that Persist Through
    Safety Training." arXiv:2401.05566.
[5] Souly, A., et al., 2025. "Poisoning Attacks on LLMs Require a Near-constant Number of
    Poison Samples." arXiv:2510.07192.
[6] NIST, 2025. "NIST AI 100-2 E2025: Adversarial Machine Learning: A Taxonomy and
    Terminology of Attacks and Mitigations." March 2025.
[7] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10, Art. 15.
[8] Wu, B., et al., 2022. "BackdoorBench: A Comprehensive Benchmark of Backdoor
    Learning." NeurIPS 2022 Datasets and Benchmarks Track. arXiv:2206.12654.
[9] Li, Y., Huang, H., Zhao, Y., Ma, X., Sun, J., 2025. "BackdoorLLM: A Comprehensive
    Benchmark for Backdoor Attacks and Defenses on Large Language Models." NeurIPS 2025
    Datasets and Benchmarks Track. arXiv:2408.12798.
[10] National Institute of Standards and Technology. "TrojAI: Overview." TrojAI
    leaderboard documentation, https://pages.nist.gov/trojai/docs/overview.html.
    Competition closed.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.2 (Data domain, Data Poisoning)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): "Large datasets dilute poison" is an intuitive but false assumption,
  directly overturned by Souly et al. (2025); FS data-quality teams check for completeness,
  not adversarial crafting.
✓ Test 2 (Plausible Harm): Extensively documented across BadNets, Carlini et al., Wan et al.,
  Hubinger et al. and Souly et al.
✓ Test 3 (Testable): Seeded-poison staging tests with trigger-condition evaluation are
  executable in non-production. ★2.
✓ Test 4 (Decision-Relevant): Gates whether a data-ingestion pipeline may feed a materially
  important model without remediation.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 7, 9, 18 and 20 — the Souly et al. paper is cited by its authors as issued (the first author is at the UK AI Security Institute; Anthropic is one of five affiliations) and under its title as issued, "Poisoning Attacks on LLMs Require a Near-constant Number of Poison Samples". Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — BackdoorBench, BackdoorLLM and the NIST
  TrojAI evaluation added as related work on backdoor attacks and defences, each with
  its limits. Field 20 — entries [8] to [10] added. Research-basis review date moved. No
  change to controls, test, ★2 or risk profile.
```

---
---

