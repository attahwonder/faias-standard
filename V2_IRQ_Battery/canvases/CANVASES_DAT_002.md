# CANVAS: IRQ-DAT-002

## 1. IRQ ID & Title
**IRQ-DAT-002: Personal or Confidential Data Entering Training Without Lawful Basis**

Register question: "Could personal or client-confidential data have entered training or fine-tuning corpora without a documented lawful basis and minimisation assessment?"

## 2. Business Activities Affected
- **Fine-tuning on internal case histories:** Claims, complaints, KYC or credit files are attractive fine-tuning material precisely because they are realistic — and precisely because they contain personal and special-category data.
- **Customer service assistants:** Training or few-shot examples drawn from real transcripts risk embedding customer PII into model weights or prompt libraries beyond the original processing purpose.
- **AML/fraud model development:** Feature-rich personal and transactional data is routinely repurposed for model development without a fresh lawful-basis assessment for the new (AI-training) purpose.

## 3. AI Behaviour(s)
- Learns statistical associations from whatever is in its training set, including personal data present without curation for purpose-limitation.
- Can memorise and later regurgitate verbatim or near-verbatim fragments of training examples, including personal identifiers.
- Provides no signal to downstream users about whether a given training example carried documented lawful basis.

## 4. Failure Mode
> Personal or client-confidential data is incorporated into a training or fine-tuning corpus for a new AI purpose without a documented lawful basis and data-minimisation assessment for that purpose, exposing the firm to unlawful processing and the model to memorisation/extraction risk.

## 5. Potential Consequences
- **Customer:** Personal data used for a purpose they did not consent to or reasonably expect; potential re-identification via model extraction.
- **Institution:** ICO enforcement, UK GDPR fines, DSAR complications where data is embedded in model weights (technically difficult to erase); reputational damage.
- **Regulator:** Evidence of purpose-limitation and minimisation failure feeding EU AI Act Art. 10 and UK GDPR Art. 5(1)(b)/(c) findings.

## 6. Failure Chain
```
Internal operational data (case files, transcripts, KYC records)
repurposed for AI training/fine-tuning without a fresh DPIA
  ↓ (IRQ-GOV-005: policy gap — AI training not treated as a new purpose)
Personal/special-category data enters the corpus without minimisation
  ↓ (IRQ-DAT-002 — THIS IRQ: unlawful basis undetected)
Model trained/fine-tuned; may memorise identifiable fragments
  ↓ (IRQ-SEC-007: memorisation enables extraction/membership inference)
Extraction attack, DSAR, or ICO audit surfaces the unlawful processing
  ↓
Regulatory enforcement, remediation cost, reputational damage

Control Breakpoints:
  • IRQ-GOV-005: policy explicitly covers AI training as a new processing purpose
  • IRQ-DAT-002: DPIA and minimisation assessment gate corpus assembly
  • IRQ-SEC-007: extraction-risk mitigation (filtering, DP, access limits)
```

## 7. Why a Domain Expert May Miss It
- Data protection officers assess *new external* processing activities; internal reuse of "our own" operational data for AI training feels exempt from fresh review.
- The assumption that anonymisation/pseudonymisation applied for the original purpose survives into a training pipeline is frequently false — re-identification risk changes when data is embedded in model weights.
- Fine-tuning teams optimise for realism and volume, not privacy minimisation, unless a gate specifically intercepts this.
- Model memorisation and extraction are non-obvious risks to a privacy SME unfamiliar with the ML literature (Carlini et al.).

## 8. Assurance Objective
**AO-DAT-002:** The firm shall not incorporate personal or confidential client data into a training or fine-tuning corpus for a new AI purpose without a documented lawful basis and minimisation assessment specific to that purpose.

## 9. Expected Controls (Traced)
- **DPIA for AI training/fine-tuning as a distinct processing purpose** — [UK GDPR Art. 35; ICO guidance on AI and data protection] — a fresh DPIA is triggered whenever operational data is repurposed for model training.
- **Data minimisation and de-identification prior to training** — [UK GDPR Art. 5(1)(c)] — only data necessary for the training objective is retained; identifiers stripped or tokenised where feasible.
- **Memorisation and extraction testing** — [Carlini et al., 2021, "Extracting Training Data from Large Language Models", USENIX Security; Carlini et al., 2022, "Quantifying Memorization Across Neural Language Models"] — post-training verbatim-extraction testing on held-out canary sequences.
- **Purpose-limitation policy covering internal AI reuse** — [linked IRQ-GOV-005] — explicit policy that "our own data" reuse for AI is a new purpose requiring assessment.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "training data is anonymised" with no methodology — **L1**.
- DPIA document covering the specific training/fine-tuning activity — **L2**.
- Code/pipeline inspection confirming minimisation/de-identification steps actually run before training — **L3**.
- Memorisation test results: canary-sequence extraction rate on the fine-tuned model — **L3/L4** depending on who executed it.
- Independent DPO or privacy audit sign-off referencing inspected evidence, not assertion — **L4**.
- Production DSAR handling records showing the firm can identify and respond to data-subject requests concerning training data — **L5**.

## 11. Independent Test
> In a non-production fine-tuning environment, embed a small number of unique canary sequences (synthetic personal-data-shaped strings) into a held-out training subset. After fine-tuning, probe the model with targeted and untargeted extraction prompts to measure verbatim/near-verbatim recall of canaries, per the divergence-attack and membership-inference methodology of Carlini et al. (2021, 2022) and Nasr et al. (2023). No real customer data used. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, multiply-replicated academic methodology; no single industry-standard extraction-rate threshold exists for FS fine-tuning, so pass/fail thresholds rest on firm judgement).

## 12. Pass Indicators
- DPIA on file for every training/fine-tuning activity using internal operational data, dated before training commenced.
- Canary extraction rate at or near the firm's documented tolerance (typically near-zero for verbatim recall).
- Minimisation steps demonstrable in pipeline code, not policy alone.
- DSAR process can identify whether a given data subject's records fed a specific model version.

## 13. Fail Indicators
- No DPIA exists for a training activity using personal/confidential data; assessment is retrospective only.
- Canary sequences are extractable verbatim at non-trivial rates.
- Minimisation policy exists but pipeline inspection shows raw identifiers still present in the training set.
- DSAR erasure requests cannot be mapped to specific model training runs (echoes IRQ-DAT-010 memory-erasure gap).

## 14. Reporting Language
**Pass:** "A documented DPIA and minimisation assessment exists for the training activity reviewed; independent canary-extraction testing found no material verbatim recall of embedded test sequences, evidencing that memorisation risk is controlled at the level tested (★3 methodology)."

**Fail:** "Personal customer data was incorporated into the fine-tuning corpus without a documented lawful-basis assessment for the AI-training purpose. Canary extraction testing recovered [x]% of embedded sequences verbatim, indicating the resulting model has memorised training examples that could be extracted by an adversarial prompt. This is an unlawful-processing and extraction-risk finding requiring remediation before further use."

**Partial:** "DPIA coverage exists for the primary training run but not for subsequent incremental fine-tuning cycles, which account for [x]% of the model's current training history. Extend DPIA discipline to every training event before the objective is considered met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (unlawful-processing finding; multiple data subjects affected)
  Likelihood: 2 (requires DPIA/minimisation gate to be bypassed or absent)
  Detectability: 3 (surfaces via audit, DSAR forensics, or extraction red-team, not real time)
  Recoverability: 2 (remediable via retraining/filtering; reversible within weeks)
  Novelty: 3 (privacy SMEs know DPIA discipline but not model-memorisation extraction risk)

If controls are absent or degraded:
  Severity: 4 (systemic unlawful processing; ICO enforcement; embedded PII un-erasable from weights)
  Likelihood: 3 (repurposing "our own" data without fresh assessment is a common organisational default)
  Detectability: 4 (silent until extraction attack or DSAR investigation)
  Recoverability: 3 (retraining/decommissioning required; PII cannot be selectively deleted from trained weights)
  Novelty: 3
Residual risk: Critical if minimisation and extraction controls are both absent.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unlawful processing finding; potential multi-subject exposure and ICO enforcement. |
| **Likelihood** | 2 | Plausible where DPIA-for-AI-training discipline is absent, which is common but not universal. |
| **Detectability** | 3 | Surfaces via audit or extraction testing, not real-time monitoring. |
| **Recoverability** | 2 | Remediable via retraining or filtering; embedded weights are the harder residual case. |
| **Novelty** | 3 | Privacy SMEs know DPIA process but not model-memorisation/extraction mechanics — an AI-specific blind spot. |

## 17. Regulatory Basis
> [UK GDPR / Data Protection Act 2018, Art. 5(1)(b) (purpose limitation), Art. 5(1)(c) (data minimisation) and Art. 35 (DPIA)] require purpose limitation, data minimisation and a DPIA for high-risk processing; AI training on repurposed personal data is high-risk processing requiring assessment. [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(b) and (f)] requires data governance measures including examination for possible biases and appropriateness for the intended purpose. (verified 29 Jul 2026)

## 18. Research Basis
> [Carlini et al., 2021, "Extracting Training Data from Large Language Models", USENIX Security 2021, arXiv:2012.07805] — demonstrated verbatim PII extraction from a production-scale language model. [Carlini et al., 2022, "Quantifying Memorization Across Neural Language Models", arXiv:2202.07646] — memorisation increases with scale and duplication. [Nasr et al., 2023, "Scalable Extraction of Training Data from (Production) Language Models", arXiv:2311.17035] — divergence attacks extract data even from aligned, deployed models.
>
> **[FAIAS Incident Register, row 42, "Otter.ai meeting-transcription class action", 2025]**, citing [Complaint, Brewer v. Otter.ai, Inc., No. 5:25-cv-06911-EKL (N.D. Cal., filed 15 August 2025)] — a class action pleads that a meeting-transcription tool recorded participants who held no account with the provider, and that the provider records "the contents of private conversations between Otter accountholders who use the Otter Notetaker and meeting participants who do not subscribe to Otter's services" while failing to disclose even to those who set the tool up "that their conversations are being used to train Otter Notetaker's automatic speech recognition ('ASR') and machine learning models, and in turn, to financially benefit Otter's business" (¶3), and without seeking the consent of "meeting participants, besides the Otter accountholder" for that use (¶28). The complaint pleads federal and Californian interception and computer-access claims, with common-law intrusion upon seclusion and conversion and a California unfair-competition claim. The actions were consolidated as *In re Otter.ai Privacy Litigation*; the consolidated complaint of 5 December 2025 repeats both passages quoted here and adds claims including under the Illinois Biometric Information Privacy Act, and on 13 August 2026 the court granted a motion to dismiss in part and denied it in part, the federal interception claim among those proceeding. The allegations are pleaded and unproven.
>
> **[FAIAS Incident Register, row 43, "Granola meeting-transcription class action", 2026]**, citing [Complaint, Chamberlain v. Granola, Inc., No. 3:26-cv-07926-EMC (N.D. Cal., filed 30 July 2026)] — a second class action, against a different provider, pleads the training limb more directly: that the provider "by default, uses the contents of those communications for its own commercial purposes, including training its AI systems", and that "[t]his setting can only be turned off by Granola users, which excludes individuals like Plaintiff and Class Members who did not authorize or consent to Granola's secret recording practices in the first place". Pleaded, not adjudicated. Taken together the two allege a route into a training corpus that this question's register wording covers but its Independent Test does not reach — the provider-side variant field 19 assigns to IRQ-TPR-007: personal data can enter a provider's training corpus through a person who was never in a position to give or refuse consent for that purpose, with the opt-out held by the account holder rather than by the person recorded; neither pleading says so, but on the facts as pleaded the firm whose meeting it was may hold no record that it happened.
>
> **[FAIAS Incident Register, row 44, "Worldcoin / Tools for Humanity biometric consent", 2025]**, citing [Comissão Nacional de Proteção de Dados (Portugal), 2024, "Deliberação/2024/137", case AVG/2023/1205, 25 March 2024, §23 (the Commission's non-official English translation); High Court of Kenya, 2025, "Republic v Tools for Humanity Corporation (US) & 9 others", [2025] KEHC 5629 (KLR), 5 May 2025, §§77–78, §191 and §207, orders (a)–(c)] — a biometric-identity deployment sought consent to use enrolment images for training its own matching algorithms: an optional, retention-stage consent in the Portuguese record, and, in the consent form before the Kenyan court, a purpose bundled in a single consent with unrelated purposes. The Portuguese supervisory authority records that consent was sought "as regards the storage of data and its use for training Worldcoin algorithms", with full functionality retained if it was refused; the Kenyan court records the Data Protection Commissioner's submission that a single consent form covered "calculating and comparing unique identifiers, optimizing algorithms, training AI models using iris images, detecting human users and personnel training", found that the consents obtained were not valid for multiple processing purposes, and ordered the data "permanently erase[d] and destroy[ed] … for having been obtained unlawfully", on an inadequate data protection impact assessment and on consent "obtained through inducement of a cryptocurrency". Stated precisely: the deployer is not a regulated financial-services firm, in the Portuguese record the training use is an optional, retention-stage purpose separate from the service, while the consent form before the Kenyan court, as the Data Protection Commissioner described it (§78), had users agree to the collection of iris data and its transfer "for training neural networks" among the bundled purposes — a submission the court recorded, not a finding it made; neither the court nor a supervisory authority found that the data was collected in order to train a model.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-SEC-007 (E.2: training-data extraction/membership inference — the technical realisation of this risk)
  - IRQ-DAT-010 (A.4: memory as a data asset — parallel erasure/DSAR challenge)
  - IRQ-GOV-005 (I.2: policy coverage for AI-specific data reuse)
  - IRQ-TPR-007 (F.3: provider retention/training on firm data — third-party variant)
```

## 20. References
```
[1] Carlini, N., et al., 2021. "Extracting Training Data from Large Language Models." USENIX Security 2021. arXiv:2012.07805.
[2] Carlini, N., et al., 2022. "Quantifying Memorization Across Neural Language Models." arXiv:2202.07646.
[3] Nasr, M., et al., 2023. "Scalable Extraction of Training Data from (Production) Language Models." arXiv:2311.17035.
[4] UK Government, 2018/2021. "UK GDPR / Data Protection Act 2018." Articles 5, 35.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 10.
[6] Brewer v. Otter.ai, Inc., No. 5:25-cv-06911-EKL (N.D. Cal.). Complaint, ECF No. 1, filed 15 August 2025. https://storage.courtlistener.com/recap/gov.uscourts.cand.454675/gov.uscourts.cand.454675.1.0.pdf
[7] In re Otter.ai Privacy Litigation, No. 5:25-cv-06911-EKL (N.D. Cal.). Consolidated Class Action Complaint, ECF No. 35, filed 5 December 2025; Order Granting Motion to Dismiss in Part, ECF No. 68, filed 13 August 2026. https://storage.courtlistener.com/recap/gov.uscourts.cand.454675/gov.uscourts.cand.454675.35.0.pdf ; https://storage.courtlistener.com/recap/gov.uscourts.cand.454675/gov.uscourts.cand.454675.68.0.pdf
[8] Chamberlain v. Granola, Inc., No. 3:26-cv-07926-EMC (N.D. Cal.). Complaint, ECF No. 1, filed 30 July 2026. https://storage.courtlistener.com/recap/gov.uscourts.cand.475308/gov.uscourts.cand.475308.1.0.pdf
[9] Comissão Nacional de Proteção de Dados (Portugal), 2024. "Deliberação/2024/137", case AVG/2023/1205, 25 March 2024 (non-official English translation). https://www.cnpd.pt/media/imub4o4i/pt-sa-decision-worldcoin_temporary-limitation-of-processing_20240325.pdf
[10] High Court of Kenya, 2025. "Republic v Tools for Humanity Corporation (US) & 9 others", [2025] KEHC 5629 (KLR), judgment of 5 May 2025. https://new.kenyalaw.org/akn/ke/judgment/kehc/2025/5629/eng@2025-05-05
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Privacy teams review external processing; internal AI-training
  reuse of "our own" data is routinely missed as a new purpose.
✓ Test 2 (Plausible Harm): Carlini et al. (2021, 2022) and Nasr et al. (2023) demonstrate
  extraction is real and scales with memorisation.
✓ Test 3 (Testable): Canary-sequence extraction testing is executable in non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates whether a training/fine-tuning activity may proceed
  and whether DSAR processes need extension to model weights.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.2.1 (2026-09-19): Field 18 — incident-register citations added in the reserved form (row 42, Otter.ai meeting-transcription class action, and row 43, Granola meeting-transcription class action, both pleaded and unproven, the first partly past a motion to dismiss; row 44, Worldcoin / Tools for Humanity biometric consent, on the training purpose as each record describes it — optional and retention-stage in the Portuguese record, bundled into the collection consent in the form before the Kenyan court as the Commissioner described it). Field 20 — entries [6]–[10] added for the pleadings, the order and the two decisions cited. Research-basis review date moved. No change to controls, test, ★3 or risk profile.
```

---
---

