# CANVAS: IRQ-TPR-007

## 1. IRQ ID & Title
**IRQ-TPR-007: Unestablished Provider Data Retention, Logging and Sub-Processor Training Use**

Register question: "Is it contractually and technically established whether the provider retains, logs or trains on the firm's prompts, files and outputs, including via sub-processors?"

## 2. Business Activities Affected
- **Any workflow submitting customer or firm-confidential data to a third-party model/API:** credit assessment, claims handling, AML investigation and customer service all routinely place confidential content into prompts and context windows.
- **Data protection and confidentiality obligations:** The firm's ability to meet GDPR/UK GDPR and client confidentiality duties depends entirely on knowing, not assuming, what the provider does with submitted content.
- **Competitive/proprietary information protection:** Proprietary firm content (pricing models, internal analysis) submitted as context risks incorporation into a provider's training data, potentially benefiting competitors indirectly.

## 3. AI Behaviour(s)
- Firm submits prompts, files and context (potentially including customer personal data and firm-confidential information) to a third-party model/API as part of normal operation.
- Provider's default data handling policy — retention period, logging for abuse monitoring, and whether content is used to improve or train future models — governs what happens to that content after submission.
- Provider may route requests through sub-processors (cloud infrastructure, safety-classification services) with their own, potentially different, data handling terms.

## 4. Failure Mode
> The firm submits customer or firm-confidential data to a third-party AI provider without contractually and technically establishing whether that data is retained, logged, or used to train the provider's models — including via sub-processors — so the firm cannot evidence compliance with its confidentiality and data protection obligations for content it has already submitted.

## 5. Potential Consequences
- **Customer:** Personal data submitted in a prompt is retained beyond the firm's own retention policy or used to train a model that later serves other customers, breaching data protection principles.
- **Institution:** GDPR/UK GDPR breach exposure (unlawful processing, purpose limitation breach); inability to fulfil a data subject access or erasure request because the firm cannot compel provider-side deletion; loss of confidentiality over proprietary content.
- **Regulator/market:** ICO enforcement action; DORA/EBA outsourcing data-handling deficiency finding; reputational damage if a provider is later found to have retained sensitive FS customer data beyond firm expectations.

## 6. Failure Chain
```
Provider default terms permit data retention/logging/training-use
unless the firm actively negotiates an opt-out or enterprise terms
  ↓ (IRQ-TPR-001/002: due diligence and contracting did not
     specifically interrogate data handling and sub-processor terms)
Firm submits customer/confidential data via prompts and context in
normal operation, unaware of the actual retention/training posture
  ↓ (IRQ-SEC-008: data-flow mapping does not confirm egress
     boundaries, so this goes undetected)
Provider (or a sub-processor) retains, logs, or trains on the
submitted content beyond the firm's expectation or lawful basis
  ↓
Data subject request, audit, or provider disclosure reveals the gap;
firm cannot demonstrate purpose limitation or fulfil erasure duties

Control Breakpoints:
  • IRQ-TPR-001: due diligence specifically interrogates data handling terms
  • IRQ-TPR-007: technical and contractual confirmation of retention/training posture, incl. sub-processors
  • IRQ-SEC-008: data-flow mapping confirms no uncontrolled egress
```

## 7. Why a Domain Expert May Miss It
- Data protection SMEs are trained on the firm's own systems' data flows; a third-party AI API is often treated like any other SaaS vendor rather than one with a distinct, AI-specific risk (content used for model training, not just storage).
- "We have a Data Processing Agreement" is treated as sufficient, without verifying whether the specific product tier used (free/trial vs enterprise) actually disables training-use, which frequently differs by tier.
- Sub-processor chains for AI providers can be opaque (safety classifiers, content moderation services, underlying cloud infrastructure), and standard DPA sub-processor lists may not clearly flag AI-specific processing (e.g. "this sub-processor screens content for abuse and retains flagged samples").
- Staff using AI tools informally (shadow AI) bypass the contracting process entirely, submitting confidential data to consumer-tier products with no enterprise data protections at all.

## 8. Assurance Objective
**AO-TPR-007:** The firm shall contractually and technically establish, for every AI provider processing firm or customer data, whether that provider (or any sub-processor) retains, logs or trains on submitted prompts, files and outputs, and shall confirm this is consistent with the firm's confidentiality and data protection obligations before reliance.

## 9. Expected Controls (Traced)
- **Data processing agreement with explicit AI-specific terms** — [UK GDPR, Article 28 processor obligations] — DPA specifies retention period, logging purpose, and explicit confirmation of training-use status (opt-out or contractual exclusion).
- **Sub-processor transparency and flow-down obligations** — [UK GDPR, Article 28(2)–(4)] — sub-processor list disclosed and flow-down of the same data protection obligations confirmed.
- **Data-flow mapping to confirm egress boundaries** — [linked IRQ-SEC-008] — technical verification that no uncontrolled data egress occurs beyond the contracted terms.
- **DPIA covering AI-specific processing risk** — [UK GDPR, Article 35; ICO, "Guidance on AI and data protection" (updated Mar 2023) and ICO, "Generative AI: eight questions that developers and users need to ask" (2023, updated as part of ICO's ongoing generative AI consultation series 2023–2024)] (verified 29 Jul 2026) — data protection impact assessment specifically addresses training-use and retention risk for AI processing.
- **Enterprise/business-tier product enforcement** — Emerging Practice — technical and procurement controls preventing use of consumer-tier AI products (with weaker default data protections) for firm or customer data.

## 10. Expected Evidence (Tagged L1–L5)
- Provider marketing page stating "we don't train on your data" with no contractual backing — **L1**.
- Executed DPA with explicit clauses on retention, logging and training-use status — **L2**.
- Sampled review confirming the DPA terms match the actual product tier in use (not a lower, weaker default tier) — **L3**.
- Data protection/legal audit confirming sub-processor flow-down obligations are met for the critical AI provider population — **L4**.
- Data-flow mapping and monitoring evidence confirming no uncontrolled egress over the last 12 months, cross-checked against contracted terms — **L5**.

**Dated worked example, added at the September 2026 refresh — a marketing-page data commitment, read as this IRQ's §10 L1 bullet requires.** The launch page for a provider's financial-services product states: "Your firm's business data is not used to train our models by default." [OpenAI, "Introducing ChatGPT for Financial Services", 10 September 2026, §"Work with security and governance you can trust"]. Two features of that sentence are the worked example. The words "by default" locate the commitment in a **configurable setting** rather than a term, so the §11(a) test — whether the data processing agreement "explicitly addresses retention, logging and training-use" — is not answered by the page, and the §11(b) test — whether the tier actually deployed is the tier the agreement covers — is precisely what the phrase leaves open. The sentence immediately following states that the data "is encrypted at rest and in transit, and admins can configure workspace retention", which makes the retention position a matter of **tenant configuration evidence** as well as contract: a reviewer should obtain the configuration as applied, not the page. Recorded as **L1 on its own** (a provider statement with no contractual backing — §10's first bullet), promotable to L3 only by the agreement and the configuration inspection together.

## 11. Independent Test
> For a sample of AI providers processing firm or customer data, verify (a) the DPA explicitly addresses retention, logging and training-use, (b) the product tier actually deployed matches the tier covered by that DPA, (c) sub-processors are disclosed and covered by flow-down obligations. Cross-check via technical inspection of API configuration (e.g. enterprise API keys with training opt-out vs consumer endpoints) where feasible. Documentation and configuration review only. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (GDPR Article 28 provides a well-established compliance checklist — reasonably standardised — but AI-specific training-use verification and sub-processor AI-specific disclosure remain less mature, pulling overall confidence down from ★4).

## 12. Pass Indicators
- All sampled AI providers have DPAs explicitly confirming retention, logging and training-use terms.
- Product tier in actual use matches the tier covered by contractual protections (no shadow use of weaker consumer tiers for firm/customer data).
- Sub-processors are disclosed with confirmed flow-down obligations.
- Data-flow mapping confirms no uncontrolled egress beyond contracted terms.

## 13. Fail Indicators
- DPAs are silent on training-use or retention specifics; firm relies on marketing claims rather than contractual terms.
- Staff or business units are found using consumer-tier AI products for confidential data, bypassing enterprise contractual protections.
- Sub-processor list is undisclosed or not reviewed for AI-specific processing risk.
- No DPIA exists covering AI-specific processing for a materially-used provider.

## 14. Reporting Language
**Pass:** "Sampled AI provider DPAs explicitly confirm retention, logging and training-use terms consistent with the firm's obligations, and the product tier in actual use matches the contracted protections. Conclusions rest on ★3 methodology — GDPR-anchored but with less mature AI-specific verification — and should be read as professional assessment, not a certified compliance determination."

**Fail:** "Sampled DPAs do not address AI-specific training-use or retention terms; the firm cannot evidence what happens to customer data submitted to at least one materially-used provider. This is a data protection compliance gap with direct GDPR/UK GDPR exposure."

**Partial:** "Enterprise-tier providers with explicit DPAs cover the majority of sanctioned AI use, but shadow use of consumer-tier tools by business units was identified in the sample, submitting data outside any contractual protection. Remediation should combine technical blocking of unsanctioned tools with expanded enterprise provisioning."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (contained data protection exposure, typically remediable via provider-level deletion request)
  Likelihood: 2 (plausible for shadow/consumer-tier use; lower for sanctioned enterprise use with reviewed DPAs)
  Detectability: 3 (surfaces via DPIA review, audit, or provider disclosure, not real-time)
  Recoverability: 2 (remediable via contract renegotiation and, where needed, deletion requests; moderate cost)
  Novelty: 3 (AI-specific training-use risk is a distinct concept from standard vendor data storage risk, easy for data protection generalists to miss)

If controls are absent or degraded:
  Severity: 3 (customer personal data used to train a third-party model represents a material, hard-to-reverse data protection breach)
  Likelihood: 3 (probable given default provider terms often permit training-use absent active negotiation, and shadow AI use is common)
  Detectability: 4 (silent — the firm has no visibility into provider-side data handling absent contractual audit rights)
  Recoverability: 3 (data already used in training cannot be meaningfully "recalled"; remediation is largely reputational and regulatory, not technical)
  Novelty: 3 (requires AI-specific data protection literacy beyond generic vendor DPA review)

Residual risk interpretation: Recoverability is the standout concern if controls fail — unlike most operational risks, data already absorbed into a third-party training run cannot be cleanly reversed, making upfront contractual and technical verification disproportionately important.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Bounded exposure for sanctioned enterprise use with reviewed terms; escalates for shadow/consumer-tier use |
| **Likelihood** | 2 | Real, especially via shadow AI use bypassing enterprise contracting, though sanctioned channels are lower risk |
| **Detectability** | 3 | Not visible in real time; surfaces via periodic DPIA/audit or provider disclosure |
| **Recoverability** | 2 | Contractually remediable going forward; already-processed data is harder to fully unwind |
| **Novelty** | 3 | AI-specific training-use risk is a distinct, easy-to-miss extension of standard vendor data protection review |

## 17. Regulatory Basis
> [UK GDPR, Article 28] requires processor agreements specifying the nature, purpose and duration of processing, with sub-processor flow-down obligations under Article 28(2)–(4). [UK GDPR, Article 35] requires a DPIA for high-risk processing, which AI-based processing of customer data is likely to constitute; ICO's "Guidance on AI and data protection" confirms AI/ML processing frequently meets Article 35(3)/(1) high-risk criteria (large-scale profiling, novel technology, automated decision-making with legal/similarly significant effect), triggering a DPIA requirement (verified 29 Jul 2026). [Regulation (EU) 2022/2554, DORA] and [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02] additionally require data handling terms to be established as part of outsourcing due diligence and contracting.

## 18. Research Basis
> No peer-reviewed research is required to establish this risk — it derives directly from documented provider terms-of-service variability between consumer and enterprise product tiers, a well-known industry pattern [UNVERIFIED — no single citable comparative academic study of consumer-vs-enterprise AI data-usage terms was located; the pattern is documented at the level of individual providers' own published terms rather than a comparative study] (verified 29 Jul 2026). The general principle that content submitted to generative AI systems may be logged, reviewed by human moderators, or used for training absent explicit opt-out is documented in multiple providers' own published data usage policies.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-SEC-008 (E.2 Extraction & Leakage: data-flow mapping confirms no uncontrolled egress)
  - IRQ-DAT-002 (A.1 Training Data Provenance: lawful basis for personal data entering any training corpus, incl. provider-side)
  - IRQ-TPR-001 (F.1 Due Diligence: data handling terms as a diligence dimension)
```

## 20. References
```
[1] UK Government, 2018 (as amended). "UK General Data Protection Regulation," Articles 28 and 35.
    URL: https://www.legislation.gov.uk/eur/2016/679/contents

[2] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)."
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[3] European Banking Authority, 2019. "Guidelines on outsourcing arrangements." EBA/GL/2019/02.
    URL: https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-outsourcing-arrangements
    Accessed: 2026-07-29 (source confirmed live and current as at this date) (verified 29 Jul 2026).
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.3 (Third Party domain, Dependencies, Concentration & Data Handling)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): AI providers are treated as generic SaaS vendors; training-use risk is a distinct, AI-specific extension of vendor DPA review.
✓ Test 2 (Plausible Harm): Grounded in UK GDPR Article 28/35 obligations and documented consumer-vs-enterprise tier variability in provider data handling terms.
✓ Test 3 (Testable): Answerable via DPA review and technical configuration cross-check.
✓ Test 4 (Decision-Relevant): Outcome gates whether a provider/tier may be used for confidential or personal data.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Expected Evidence — one consolidated dated worked example added (a "not used to train our models by default" launch-page commitment plus administrator-configurable retention, 10 Sep 2026), recorded as L1 on its own. ★3 / P3 unchanged.
```

---
---

