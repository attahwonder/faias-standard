# CANVAS: IRQ-SEC-007

## 1. IRQ ID & Title
**IRQ-SEC-007: Training-Data Extraction, Membership Inference and Model Inversion Recovering Personal or Proprietary Information**

Register question: "Can training-data extraction, membership inference or model inversion recover personal or proprietary information from the model or embeddings?"

## 2. Business Activities Affected
- **Fine-tuned in-house models:** Where a firm fine-tunes on customer transcripts, complaint text, or proprietary underwriting rationale, extraction risk applies directly to that fine-tuning corpus.
- **Embedding-based retrieval systems:** Vector embeddings of customer documents can themselves leak information about the underlying content via inversion techniques, independent of the generative model.
- **Any customer data used in prompt-engineering or few-shot examples:** Data included as in-context examples is a lower-bar leakage risk than fine-tuning but shares the same underlying concern.

## 3. AI Behaviour(s)
- Fine-tuning and embedding processes statistically compress training examples into model parameters or vector representations; this compression is imperfect and can retain recoverable traces of specific training instances, especially duplicated or rare examples.
- Generation processes, when queried in specific adversarial ways (divergence attacks, membership-inference probes), can be induced to reproduce or reveal statistical evidence of particular training instances.
- Alignment/safety fine-tuning reduces but does not eliminate this risk — extraction has been demonstrated against aligned, production models, not only base models.

## 4. Failure Mode
> Adversarial querying of a fine-tuned model or its embeddings recovers personal or proprietary information about a specific training instance — verbatim reproduction, confident membership inference (was this individual's data used), or reconstruction via model inversion — that was not intended to be individually recoverable.

## 5. Potential Consequences
- **Customer:** Personal data disclosed to an unauthorised party via extraction; membership inference itself can be a privacy harm (confirming an individual was, e.g., part of a fraud-investigation training set).
- **Institution:** UK GDPR breach with notification obligations; loss of any competitive advantage embedded in proprietary fine-tuning data (e.g. underwriting rationale) if extracted by a competitor or adversary.
- **Market/regulator:** ICO enforcement risk; demonstrates that fine-tuning on customer data requires privacy-engineering controls beyond standard data protection practice.

## 6. Failure Chain
```
Personal/proprietary data used in fine-tuning or embedding generation
  ↓ (IRQ-DAT-002: lawful basis and minimisation for that data use)
Model or embeddings statistically retain recoverable traces of specific instances
(more retrievable for duplicated, rare, or high-salience examples)
  ↓ (IRQ-SEC-007 — THIS IRQ: no extraction-risk assessment or mitigation applied)
Adversary queries with extraction/membership-inference/inversion technique
  ↓ (IRQ-SEC-008: no output/context-level filtering catches the disclosure)
Personal or proprietary information disclosed
  ↓
Data breach → ICO notification obligation → customer harm and remediation cost

Control Breakpoints:
  • IRQ-DAT-002: lawful basis and DPIA before personal data enters training
  • IRQ-SEC-007: extraction-risk assessment and mitigation (DP techniques, deduplication,
    access limits) applied to fine-tuning and embedding pipelines
  • IRQ-SEC-008: output-level filtering as a final backstop
```

## 7. Why a Domain Expert May Miss It
- Data protection SMEs assess lawful basis and purpose limitation for the *use* of data in training, but the technical question of whether the trained artefact itself can leak specific training instances back out is a machine-learning-specific concern outside standard DPIA methodology.
- The intuitive model of "the AI learned patterns, not records" is only approximately true — duplicated or rare examples are disproportionately memorised and recoverable, a counter-intuitive scaling property.
- Embeddings are often treated as "just numbers" (not personal data) by non-specialist reviewers, missing that they can be inverted to recover meaningful content about the underlying document.
- Alignment/safety training is assumed to have "fixed" extraction risk; research demonstrates aligned production models remain vulnerable to targeted divergence-style extraction attacks.

## 8. Assurance Objective
**AO-SEC-007:** Extraction, membership-inference and model-inversion risk against any fine-tuned model or embedding store containing personal or proprietary data shall be assessed, and mitigations (data minimisation, deduplication, differential privacy or equivalent, access limits) shall be evidenced proportionate to the sensitivity of the underlying data.

## 9. Expected Controls (Traced)
- **Deduplication of fine-tuning data** — [Carlini, N., et al., 2022, "Quantifying Memorization Across Neural Language Models", arXiv:2202.07646] — memorisation scales with duplication; deduplication is a direct, evidenced mitigation.
- **Extraction-risk testing prior to deployment** — [Carlini, N., et al., 2021, "Extracting Training Data from Large Language Models", USENIX Security 2021, arXiv:2012.07805; Nasr, M., et al., 2023, "Scalable Extraction of Training Data from (Production) Language Models", arXiv:2311.17035] — direct extraction-attack methodology, including divergence-style attacks shown to work against aligned production models, informing the test design below.
- **Membership-inference measurement at low false-positive rate** — [Carlini, N., et al., 2022, "Membership Inference Attacks From First Principles" (LiRA), IEEE S&P, arXiv:2112.03570] — the current correct standard for measuring MIA risk (evaluating at low FPR, not aggregate accuracy, per this paper's critique of prior weaker methodology).
- **Data minimisation and privacy-preserving training techniques where materiality warrants** — [linked IRQ-DAT-002; UK GDPR Art. 5(1)(c) data minimisation] — differential privacy or equivalent techniques, or exclusion of high-sensitivity personal data from fine-tuning entirely, as Emerging Practice for FS-specific application (no FS-sector-standard DP configuration yet published; mark as such).
- **Access limits on embeddings and model artefacts** — [Tramèr, F., et al., 2016, "Stealing Machine Learning Models via Prediction APIs", USENIX Security 2016, arXiv:1609.02943] — query-access controls (rate limiting, output restriction) reduce the practical feasibility of extraction and model-stealing attacks conducted via API access.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor claim that "the model does not memorise training data" — **L1**.
- Documentation of deduplication process and any privacy-preserving training technique applied to the fine-tuning pipeline — **L2**.
- Code/pipeline inspection confirming deduplication and access-limiting controls are actually applied — **L3**.
- Staging extraction/membership-inference test results per Carlini et al. (2021/2022) and Nasr et al. (2023) methodology, with recovery/inference success rates — **L3**.
- Independent privacy/security assessment of the fine-tuning and embedding pipeline — **L4**.
- Comparable-deployment operational evidence of extraction-attempt detection or confirmed incident (if any) — **L5**.

## 11. Independent Test
> In an isolated non-production environment, using a held-out labelled subset of the fine-tuning corpus with known ground truth of inclusion/exclusion: (1) run a training-data extraction attack, including divergence-style prompting per Nasr et al. (2023), against the fine-tuned model, and measure verbatim/near-verbatim recovery rate; (2) run a membership-inference attack evaluated at low false-positive rate (LiRA-style, per Carlini et al. 2022) to assess whether specific-instance membership can be confidently inferred; (3) where embeddings are used, attempt inversion of a sample of embedding vectors to assess reconstructable content. Compare recovery/inference rates against the Carlini et al. (2021, 2022) and Nasr et al. (2023) published baselines for context. Synthetic/anonymised held-out data only; no production personal data used in the attack corpus itself. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (multiple independent, peer-reviewed research groups use closely related methodology — Carlini et al., Nasr et al., Shokri et al. — giving credible convergence, but no single industry-standard benchmark or FS-specific threshold exists, so pass/fail thresholds rest on professional judgement calibrated to data sensitivity).

## 12. Pass Indicators
- No verbatim or near-verbatim recovery of held-out training instances under extraction testing.
- Membership-inference attack, evaluated at low false-positive rate, achieves no better than near-chance discrimination on the held-out set.
- Embedding inversion recovers no material sufficient to reconstruct meaningful document content.
- Deduplication and access-limiting controls confirmed applied in the fine-tuning/embedding pipeline (not asserted only).

## 13. Fail Indicators
- Verbatim or near-verbatim personal/proprietary content recovered from held-out training instances.
- Membership inference achieves materially better-than-chance discrimination at low false-positive rate on genuinely sensitive data.
- No deduplication applied; rare or duplicated high-sensitivity examples identified as present in the fine-tuning corpus without mitigation.
- Testing evaluated membership inference only by aggregate accuracy (the discredited weaker methodology this IRQ's controls explicitly supersede), rather than at low FPR.

## 14. Reporting Language
**Pass:** "Extraction and membership-inference testing on held-out fine-tuning data, per Carlini et al. (2021, 2022) and Nasr et al. (2023) methodology, found no material verbatim recovery and no better-than-chance membership discrimination at low false-positive rate. Deduplication and access-limiting controls are confirmed applied in the fine-tuning pipeline. Testing rated ★3; given the sensitivity of any personal data involved, periodic re-testing on each fine-tuning refresh is recommended."

**Fail:** "Extraction testing recovered [n] near-verbatim training instances containing personal/proprietary data, and membership inference achieved materially better-than-chance discrimination at low false-positive rate. This is evidence of an active UK GDPR-relevant disclosure risk and, separately, a proprietary-information leakage risk; the fine-tuning pipeline requires deduplication and access-control remediation, and a DPIA update, before continued use."

**Partial:** "No verbatim extraction was achieved, but membership inference showed moderate above-chance discrimination on the highest-sensitivity data subset. This residual risk has not yet been assessed against the firm's DPIA risk-acceptance threshold and should be escalated to the data protection function for a materiality decision."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (personal/proprietary data disclosure; UK GDPR notification risk)
  Likelihood: 2 (plausible but requires deliberate, technically sophisticated attack;
              mitigated by deduplication and access limits)
  Detectability: 3 (query-pattern anomaly detection, where present, surfaces attempts;
              absent monitoring, extraction may be indistinguishable from ordinary use)
  Recoverability: 3 (data-breach remediation, notification, and pipeline rework; days-to-weeks)
  Novelty: 4 (counter-intuitive memorisation-scaling property; well outside standard DPIA
              methodology and traditional data-protection review practice)

Interpretation: acceptable with deduplication, access limits and periodic re-testing;
highest concern is Novelty — DPO/data-protection teams need AI-specific training to assess
this risk at all.

If controls are absent or degraded:
  Severity: 3 (as above; scale depends on how much sensitive data entered fine-tuning)
  Likelihood: 3 (demonstrated feasible against aligned production models, not only base models)
  Detectability: 4 (silent; requires dedicated query-pattern monitoring uncommon in current
              FS AI deployments)
  Recoverability: 3 (breach notification, pipeline rework, potential ICO engagement)
  Novelty: 4
Residual risk: Critical for any fine-tuning on genuinely sensitive personal or proprietary data.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Personal/proprietary data disclosure with UK GDPR notification obligations; scale depends on data sensitivity. |
| **Likelihood** | 2 | Plausible if controls absent but requires a technically deliberate attack; readily mitigated by deduplication and access limits per the cited research. |
| **Detectability** | 4 | Extraction/membership-inference queries can be indistinguishable from ordinary use absent dedicated query-pattern monitoring, which is uncommon in current FS deployments. |
| **Recoverability** | 3 | Breach notification, pipeline remediation, and potential regulator engagement; not fast to unwind. |
| **Novelty** | 4 | Counter-intuitive memorisation-scaling property outside standard DPIA/data-protection methodology; a privacy specialist without ML-specific training will very likely miss it. |

## 17. Regulatory Basis
> [UK GDPR Art. 5(1)(c) data minimisation, Art. 32 security of processing, Art. 35 DPIA requirement] — engaged directly where fine-tuning uses personal data and extraction risk is not assessed. [ICO, Guidance on AI and data protection (updated 15 March 2023), section "How should we assess security and data minimisation in AI?"] — expects organisations to assess and mitigate memorisation/re-identification risk in AI systems trained on personal data. [PRA SS1/23 Model Risk Management, April 2026 (16 April 2026, updating 17 May 2023), Principle 3/4] — where the fine-tuned model is in MRM scope, data-handling risk assessment forms part of validation. [CONFIRMED — the guidance hub (ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/) lists named sections, and the section "How should we assess security and data minimisation in AI?" has its own page, which covers model inversion and membership inference and the steps to manage the risk of privacy attacks on AI models. The hub states that the guidance was updated on 15 March 2023 and that, because of changes made by the Data (Use and Access) Act, it is under review and may change] (verified 7 Oct 2026).

## 18. Research Basis
> [Carlini, N., et al., 2021, "Extracting Training Data from Large Language Models", USENIX Security 2021, arXiv:2012.07805] — demonstrated verbatim PII extraction from GPT-2. [Nasr, M., et al., 2023, "Scalable Extraction of Training Data from (Production) Language Models", arXiv:2311.17035] — divergence attack extracting data from aligned, production ChatGPT, showing alignment does not prevent extraction. [Carlini, N., et al., 2022, "Membership Inference Attacks From First Principles", IEEE S&P, arXiv:2112.03570] — LiRA methodology; establishes low-FPR evaluation as the correct measurement standard. [Shokri, R., et al., 2017, "Membership Inference Attacks Against Machine Learning Models", IEEE S&P, arXiv:1610.05820] — founding shadow-model MIA methodology. [Carlini, N., et al., 2022, "Quantifying Memorization Across Neural Language Models", arXiv:2202.07646] — memorisation scales with model size, data duplication, and context length. [Tramèr, F., et al., 2016, "Stealing Machine Learning Models via Prediction APIs", USENIX Security 2016, arXiv:1609.02943] — model-extraction-via-query-access, relevant to API-exposed FS models.
>
> **[FAIAS Incident Register, row 39, "GEMA v OpenAI — lyrics memorisation", 2025]** — a court held, in the words of its press release, that the works in issue are "reproduzierbar in den Sprachmodellen 4 und 4o der Beklagten enthalten", and that their encoding in the model's specified parameters constitutes a reproduction, the memorisation having been established by comparing the lyrics present in the training data with the model's outputs [Landgericht München I, 2025, "GEMA v OpenAI", Az. 42 O 14139/24, judgment of 11 November 2025; court press release of the same date]. This is a judicial determination that specific training instances remain recoverable from a deployed production model. The works recovered were copyright works rather than personal data, so the determination reaches the recoverability limb and not membership inference or inversion; the judgment is not final, and its currency is to be re-checked at the next review.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-DAT-002 (A.1: lawful basis and DPIA for personal data entering training — the
    upstream governance control)
  - IRQ-SEC-006 (E.2: system-prompt/secrets extraction — related but distinct extraction
    surface, in-context rather than training-time)
  - IRQ-SEC-008 (E.2: confidential egress through prompts/context/logs — the output-level
    backstop)
  - IRQ-TPR-007 (F.3: provider retention/training-on-firm-data — the vendor-side mirror of
    this risk)
```

## 20. References
```
[1] Carlini, N., et al., 2021. "Extracting Training Data from Large Language Models."
    USENIX Security 2021. arXiv:2012.07805.
[2] Nasr, M., et al., 2023. "Scalable Extraction of Training Data from (Production)
    Language Models." arXiv:2311.17035.
[3] Carlini, N., et al., 2022. "Membership Inference Attacks From First Principles."
    IEEE S&P 2022. arXiv:2112.03570.
[4] Shokri, R., Stronati, M., Song, C., Shmatikov, V., 2017. "Membership Inference Attacks
    Against Machine Learning Models." IEEE S&P 2017. arXiv:1610.05820.
[5] Carlini, N., et al., 2022. "Quantifying Memorization Across Neural Language Models."
    arXiv:2202.07646.
[6] Tramèr, F., et al., 2016. "Stealing Machine Learning Models via Prediction APIs."
    USENIX Security 2016. arXiv:1609.02943.
[7] ICO, 2023 (updated). "Guidance on AI and data protection," section "How should we assess security and data minimisation in AI?"
    https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/how-should-we-assess-security-and-data-minimisation-in-ai/
    [CONFIRMED — section read at this URL; the guidance hub states that the guidance was updated
    on 15 March 2023 and is under review after the Data (Use and Access) Act] (verified 7 Oct 2026).
[8] UK GDPR, retained EU law, Articles 5, 32, 35.
[9] Landgericht München I, 2025. "GEMA v OpenAI." Az. 42 O 14139/24, judgment of
    11 November 2025, not final. Court press release:
    https://www.justiz.bayern.de/gerichte-und-behoerden/landgericht/muenchen-1/presse/2025/11.php
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.2 (Security domain, Extraction & Leakage)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Data protection SMEs assess lawful basis for data use, not
  whether the trained artefact itself can leak specific instances back out — a
  machine-learning-specific concern outside standard DPIA method.
✓ Test 2 (Plausible Harm): Extensively documented in peer-reviewed research (Carlini et al.
  2021/2022, Nasr et al. 2023, Shokri et al. 2017, Tramèr et al. 2016).
✓ Test 3 (Testable): Testable via staging extraction/MIA/inversion attacks on held-out data
  with known ground truth; ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome gates whether a fine-tuning pipeline using personal or
  proprietary data may proceed, and informs DPIA risk-acceptance decisions.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form
  (row 39), a judicial determination that specific training instances remain
  recoverable from a deployed production model, carried with the judgment's non-final
  status and confined to the recoverability limb, its quoted words attributed to the court's
  press release; reference entry [9] added at Field 20. Research-basis review date moved.
  ★3 unchanged.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 17 and 20 — the ICO Guidance on AI and data protection cited at the section "How should we assess security and data minimisation in AI?", with its URL; the statement that the guidance has no stable sections and cannot be pinpointed is removed; the hub notice that the guidance is under review after the Data (Use and Access) Act is carried. No change to controls, test, ★ rating or risk profile.
```

---
---

