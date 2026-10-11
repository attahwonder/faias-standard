# CANVAS: IRQ-DAT-001

## 1. IRQ ID & Title
**IRQ-DAT-001: Untraceable Training and Grounding Data Lineage**

Register question: "Can the firm evidence end-to-end provenance for every training, fine-tuning or grounding dataset — lawful origin, licence compatibility, copyright status, transformation history and reproducible lineage?"

## 2. Business Activities Affected
- **Model development and fine-tuning:** In-house or vendor-tuned models for credit scoring, claims triage or customer communication rely on training corpora whose origin and licence status directly determine legal usability of the resulting model.
- **RAG-grounded advisory and customer service:** Grounding corpora (policy documents, product terms, historical correspondence) must be traceable to a lawful, current source before being surfaced to customers as fact.
- **Model risk management sign-off:** SS1/23-style model approval depends on the data lineage being reconstructable at the point of independent validation, not only at build time.

## 3. AI Behaviour(s)
- Consumes training, fine-tuning and grounding datasets assembled from internal systems, licensed feeds, web-scraped or vendor-supplied sources, and synthetic augmentation.
- Inherits whatever legal and quality properties its source data carries, without itself flagging provenance gaps.
- Produces outputs (predictions, generations, retrieved passages) that are presented as authoritative regardless of whether their originating data's lineage is documented.

## 4. Failure Mode
> A model is trained, fine-tuned or grounded on data whose lawful origin, licence terms, copyright status or transformation history cannot be reconstructed, so the firm cannot demonstrate — to a regulator, litigant or internal validator — that the resulting outputs and the model itself rest on a lawful and quality-assured data basis.

## 5. Potential Consequences
- **Institution:** Inability to defend a copyright, licence-breach or unlawful-processing challenge; forced retraining or model withdrawal if a data source is later found tainted.
- **Regulator/market:** EU AI Act Annex III data-governance failure finding; PRA SS1/23 validation failure ("development" principle not evidenced); reputational damage from public disclosure of untraceable sourcing (cf. Stable Diffusion/LAION CSAM contamination finding).
- **Customer:** Downstream harm is indirect but real — a model built on unlawfully obtained personal data or systematically mis-sourced content propagates that defect into every decision it supports.

## 6. Failure Chain
```
Data ingested from multiple sources (internal, licensed, scraped, vendor,
synthetic) without a mandatory lineage-capture step at ingestion
  ↓ (IRQ-DAT-006: no integrity/provenance screening at intake)
Dataset assembled for training/fine-tuning/grounding; transformation
steps (cleaning, deduplication, merging) not logged
  ↓ (IRQ-DAT-001 — THIS IRQ: lineage becomes unreconstructable)
Model built, validated and approved on evidence that assumes
lineage exists but never independently verifies it
  ↓ (IRQ-GOV-007: independent validation relies on unverified provenance claim)
Model deployed; produces outputs whose legal/quality basis cannot
be defended
  ↓
Copyright claim, DPA/GDPR challenge, or contamination finding surfaces
externally → regulatory enforcement, retraining cost, reputational harm

Control Breakpoints:
  • IRQ-DAT-006: integrity/provenance screening at ingestion
  • IRQ-DAT-001: mandatory lineage capture and versioned data registry
  • IRQ-GOV-007: independent validation actually tests lineage claims
  • IRQ-GOV-009: documentation standard requires lineage evidence
```

## 7. Why a Domain Expert May Miss It
- Credit/insurance SMEs are trained to validate model outputs (accuracy, discrimination) not the chain of custody of the data that built the model — lineage sits upstream of their usual review scope.
- "We licensed the data" is treated as a closing statement rather than the start of a documentation obligation covering every transformation since acquisition.
- Vendor-supplied fine-tuned models obscure lineage entirely; SMEs assume the vendor has handled it, with no contractual right to inspect (links IRQ-TPR-002).
- Web-scale and synthetic augmentation blend sources so thoroughly that no single team retains an end-to-end picture; the gap is discovered only when a specific record is challenged.

## 8. Assurance Objective
**AO-DAT-001:** The firm shall be able to reconstruct, for any training, fine-tuning or grounding dataset in current use, its lawful origin, licence status, copyright position and complete transformation history, on demand and within a defined timeframe.

## 9. Expected Controls (Traced)
- **Versioned data lineage registry** — [ISO/IEC 5338:2023, AI system life cycle processes, data engineering stage] — every dataset version, source and transformation recorded and retrievable.
- **Licence and copyright clearance workflow at intake** — [EU AI Act, Regulation (EU) 2024/1689, Art. 10 data governance requirements for high-risk AI] — datasets are cleared before use, not retrospectively.
- **Independent validation of lineage claims** — [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), development and independent validation principles] — a function independent of development actually inspects lineage evidence rather than accepting an assertion.
- **Model/data documentation cards** — [NIST AI RMF 1.0, Jan 2023, MAP function; ISO/IEC 42001:2023 clause 7.5 documented information] — system and data cards record provenance at a standard sufficient for regulatory response.
- **Open-source/third-party intake gating** — [linked IRQ-TPR-005] — publisher authenticity and weight/data integrity verified before use.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "all data is properly licensed" with no supporting register — **L1** (flag: assertion only).
- Data lineage registry design and schema (source, licence, transformation log fields) — **L2**.
- Sample audit: 20 datasets traced end-to-end from ingestion to current model version; lineage reconstruction success rate recorded — **L3**.
- Independent validation report confirming lineage evidence was inspected (not merely referenced) for the datasets underpinning a specific model approval — **L4**.
- Production data registry logs showing continuous lineage capture across the last 12 months of dataset changes — **L5**.

## 11. Independent Test
> In a non-production environment, select a stratified sample of datasets feeding current or in-development models (internal, licensed, scraped, vendor-supplied, synthetic). Attempt full lineage reconstruction — origin, licence terms, transformation history — using only the firm's data registry and documentation, without recourse to informal team knowledge. Record reconstruction success rate and time-to-reconstruct per source type. Methodology follows ISO/IEC 5338:2023 lifecycle documentation expectations; no single published benchmark exists for "lineage reconstruction success rate" in FS. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible standards-based method, no agreed pass/fail benchmark; professional judgement required in scoring "reconstructed").

## 12. Pass Indicators
- ≥95% of sampled datasets fully reconstructable from the registry alone within a defined SLA.
- No dataset in active model-feeding use lacks a licence/copyright determination.
- Independent validation reports explicitly confirm lineage inspection (not assertion) for approved models.
- Vendor/open-source intake shows documented provenance checks prior to use, not after incident.

## 13. Fail Indicators
- Lineage reconstruction relies on individual staff memory or ad hoc emails; registry incomplete or absent.
- Datasets in production model pipelines have no recorded licence determination.
- Independent validation sign-off references "provenance confirmed" with no underlying evidence trail (L1 only).
- Vendor-supplied fine-tuned models have no contractual or technical mechanism for the firm to inspect training data lineage.

## 14. Reporting Language
**Pass:** "Lineage for sampled training and grounding datasets was independently reconstructed from the firm's data registry with a [x]% success rate, evidencing that licence, copyright and transformation history are recorded at source rather than reconstructed after the fact. Independent validation confirmed lineage inspection, not assertion, for the models tested. Conclusions rest on ★3 methodology — a credible standards-based method with no agreed pass/fail benchmark — and should be read as professional assessment."

**Fail:** "Lineage reconstruction failed for [x]% of sampled datasets; licence and copyright status for material training data could not be established from firm records. This is a foundational data-governance gap: it undermines every downstream claim about the model's lawful basis and leaves the firm unable to respond to a copyright or regulatory challenge."

**Partial:** "Lineage is well-evidenced for internally sourced data but absent for vendor-supplied fine-tuning corpora, covering [x]% of the model estate. The assurance objective is not met until vendor contracts secure inspection rights or equivalent attestation with underlying evidence."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (regulatory notice risk; retraining/withdrawal cost if a source is challenged)
  Likelihood: 2 (requires registry/process to actually lapse; plausible given documentation discipline is easy to erode)
  Detectability: 3 (surfaces only via audit, external claim, or incident — not real-time)
  Recoverability: 3 (reversible via registry remediation and retrospective clearance; moderate cost)
  Novelty: 2 (data lineage is a recognised documentation discipline; AI-specific element is scale/blending of sources)

If controls are absent or degraded:
  Severity: 4 (model withdrawal or enforcement if unlawful data underpins a material decisioning model)
  Likelihood: 3 (foreseeable given how routinely lineage discipline lapses under delivery pressure)
  Detectability: 4 (silent until an external party challenges a specific dataset)
  Recoverability: 3 (retraining, legal exposure, multi-team remediation)
  Novelty: 2
Residual risk: material without registry discipline; escalates quickly if unaddressed.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Regulatory notice and remediation cost; potential model withdrawal if a source is unlawful. |
| **Likelihood** | 2 | Plausible if registry discipline lapses; not the default failure mode with basic controls in place. |
| **Detectability** | 3 | Detected via periodic audit or external challenge, not real-time monitoring. |
| **Recoverability** | 3 | Reversible via retrospective clearance and registry remediation within days-to-weeks. |
| **Novelty** | 2 | Domain expert with data-governance background would likely flag this; the AI-specific element is the scale of blended sourcing. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 10(2)(a)–(f), data and data governance for high-risk AI systems] requires training, validation and testing data to meet quality criteria including relevant provenance examination; applies to Annex III credit-scoring and insurance-pricing systems from 2 Dec 2027 (postponed from the original 2 Aug 2026 date by the Digital Omnibus, agreed and in force Jul 2026 — 2 Aug 2026 remains the applicable date for the separate Art. 50 transparency obligations, save that Art. 50(2) marking for systems placed on the market before that date applies from 2 Dec 2026). [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023), effective May 2024, Principle 3 (model development, implementation and use) and Principle 4 (independent model validation)] require the data basis of a model to be evidenced and independently checked. [ISO/IEC 42001:2023 clause 7.5, "Documented information"] requires documented information supporting AI system claims. (corrected & verified 29 Jul 2026)

## 18. Research Basis
> [Stanford Internet Observatory, Dec 2023, "Investigation Finds AI Image Generation Models Trained on Child Abuse"] — documented real-world consequence of web-scale ingestion without provenance controls (LAION/Stable Diffusion), the closest published analogue to unverified FS data sourcing. [Allen Institute, OLMo + Dolma full-transparency releases, 2024–2025] — demonstrates that full lineage transparency is achievable and enables contamination/provenance auditing otherwise impossible. No FS-specific empirical study of lineage reconstruction success rates was located; this is an evidence gap, not an omission — flagged [UNVERIFIED — no FS-specific published study located; general analogues (Stanford Internet Observatory, Allen Institute OLMo/Dolma) confirmed as cited] (verified 29 Jul 2026).
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-006 (A.2: integrity screening at ingestion — upstream control)
  - IRQ-TPR-005 (F.3: open-source provenance verification)
  - IRQ-GOV-007 (I.3: independent validation must test, not assert, lineage)
  - IRQ-GOV-009 (I.4: documentation standard for lineage evidence)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." OJ L 12.7.2024. Art. 10.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] ISO/IEC, 2023. "ISO/IEC 5338:2023 — AI system life cycle processes." December 2023.
[4] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management system." December 2023.
[5] Stanford Internet Observatory, 2023. "Investigation Finds AI Image Generation Models Trained on Child Abuse." December 2023.
    URL: https://cyber.fsi.stanford.edu/io/news/investigation-finds-ai-image-generation-models-trained-child-abuse
    Archived copy: https://web.archive.org/web/20231220175623/https://cyber.fsi.stanford.edu/io/news/investigation-finds-ai-image-generation-models-trained-child-abuse
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.1 (Data domain, Training Data Provenance)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Model-output-focused SMEs rarely audit upstream data lineage;
  vendor fine-tuning obscures it further.
✓ Test 2 (Plausible Harm): Documented in the LAION/Stable Diffusion contamination finding;
  direct regulatory hook in EU AI Act Art. 10 and PRA SS1/23.
✓ Test 3 (Testable): Sample-based lineage reconstruction is executable in non-production
  against the firm's own registry. ★3.
✓ Test 4 (Decision-Relevant): Gates model approval and vendor-data intake decisions.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within days-to-weeks, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. The other axes, the ★ rating and the research basis are unchanged.
```

---
---

