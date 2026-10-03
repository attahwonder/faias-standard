# CANVAS: IRQ-SEC-008

## 1. IRQ ID & Title
**IRQ-SEC-008: Confidential Data Egress via Prompts, Context Windows, Telemetry or Logs**

Register question: "Can confidential firm or client data leak through prompts, context windows, telemetry or logs into environments outside the firm's control?"

## 2. Business Activities Affected
- **Any generative AI use with customer or firm-confidential input:** Staff pasting customer data, deal information, or internal analysis into a prompt creates an egress path the moment that prompt leaves the firm's control boundary.
- **Third-party-hosted models and platforms:** Where the model provider is external, every prompt, context-window content, and often diagnostic telemetry is a potential egress point unless contractually and technically constrained.
- **Logging and observability pipelines:** Application logs, debugging traces, and third-party observability tooling (APM, error tracking) commonly capture full prompt/response content by default, creating a secondary egress path independent of the model provider relationship.

## 3. AI Behaviour(s)
- Processes whatever content is placed in its prompt/context window, with no inherent distinction between public and confidential content.
- Generates telemetry (usage logs, error traces, sometimes full prompt/response pairs) as a normal operational by-product, often captured by default in third-party observability tools.
- Where agentic or tool-using, may pass context-window content onward to further tool calls or sub-agents, propagating exposure beyond the original boundary.

## 4. Failure Mode
> Confidential firm or customer data included in a prompt, retained in a context window, or captured in telemetry/logs, is transmitted to or persisted in an environment outside the firm's control — a third-party model provider's training/retention pipeline, an external observability vendor, or an unintended log destination — without the data-flow control or contractual basis required.

## 5. Potential Consequences
- **Customer:** Personal or account data disclosed to an environment outside the firm's control; potential UK GDPR breach.
- **Institution:** Loss of confidential deal, pricing, or strategic information to a third party; contractual breach if the provider agreement did not permit such use; regulatory scrutiny of data governance for AI.
- **Market/regulator:** ICO/FCA engagement; systemic concern if the egress path affects many users (e.g. a misconfigured default logging setting) rather than a single incident.

## 6. Failure Chain
```
Staff member or automated process includes confidential data in a prompt,
or the platform captures full prompt/response content in default telemetry
  ↓ (IRQ-TPR-007: provider retention/training-on-data terms not established
     or not honoured)
Content transmitted to third-party model API or observability vendor
  ↓ (IRQ-SEC-008 — THIS IRQ: no data-flow mapping or egress control catches this)
Content persists or is processed outside the firm's control boundary
  ↓ (IRQ-DAT-009: entitlement model not enforced on the egressed copy)
Confidential data now resides in an environment the firm cannot govern
  ↓
Discovered via audit, DSAR, or third-party breach notification →
regulatory notification obligation → remediation and possible enforcement

Control Breakpoints:
  • IRQ-TPR-007: contractual and technical verification of provider data handling
  • IRQ-SEC-008: data-flow mapping and egress controls (DLP, prompt-level filtering)
  • IRQ-GOV-005: acceptable-use policy restricting what may be entered into AI systems
  • IRQ-DAT-009: entitlement enforcement extended to logging/telemetry copies
```

## 7. Why a Domain Expert May Miss it
- Data governance SMEs map data flows for known systems of record; ad hoc prompt content is not typically captured in existing data-flow inventories, especially where staff use AI tools informally.
- Default telemetry/logging behaviour of third-party AI platforms and observability tools is often opaque to the deploying firm and not reviewed as part of standard vendor onboarding (which focuses on the primary model API, not secondary diagnostic pipelines).
- The intuitive model "the conversation is private to me and the AI" is false for most commercial AI deployments; staff and even technical reviewers commonly underestimate how many downstream systems see prompt content.
- This is a shadow-AI-adjacent risk (linked IRQ-GOV-002): the egress path can exist even where the AI use itself is sanctioned, purely through unreviewed logging configuration.

## 8. Assurance Objective
**AO-SEC-008:** Confidential firm or customer data shall not egress to environments outside the firm's control via prompts, context windows, telemetry or logs without an established lawful basis and contractual/technical control, demonstrated by complete data-flow mapping across all AI-adjacent egress paths.

## 9. Expected Controls (Traced)
- **Complete data-flow mapping across all AI-adjacent paths** — [DSIT, AI Cyber Security Code of Practice, Jan 2025] — mapping must cover the primary model API, any embedding/vector store, and secondary telemetry/observability pipelines, not the model API alone.
- **Contractual verification of provider data retention/training use** — [linked IRQ-TPR-007] — technical and contractual confirmation of whether the provider retains, logs, or trains on submitted content, including via sub-processors.
- **Data loss prevention / prompt-level filtering for confidential content** — [OWASP Top 10 for LLM Applications 2025, LLM02 Sensitive Information Disclosure] — technical controls to detect and block confidential-category content (account numbers, deal terms) before it reaches an external model or logging destination.
- **Acceptable-use policy technically enforced, not only stated** — [linked IRQ-GOV-005, IRQ-GOV-003] — restrictions on what categories of data may be entered into which AI tools, enforced at the platform level.
- **Logging/telemetry configuration review as part of AI vendor onboarding** — [Emerging Practice] — no FS-sector-standard checklist yet exists specifically for AI observability-pipeline data capture; review should be added explicitly to vendor due diligence rather than assumed covered by the primary model API contract review.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor assertion that "your data is not used for training" with no supporting contractual detail — **L1**.
- Data-flow diagram covering model API, embedding store, and telemetry/observability pipelines — **L2**.
- Technical inspection confirming DLP/filtering is actually applied pre-transmission and that logging configuration does not capture full prompt/response content by default (or that such capture is contractually and technically controlled) — **L3**.
- Staging test: submission of marked confidential test content, verification of whether and where it appears in logs/telemetry outside the firm's control boundary — **L3**.
- Independent data-flow/security assessment covering AI-adjacent egress paths specifically — **L4**.
- Contract review evidence (legal/procurement) confirming provider retention and sub-processor terms — **L4/L2 depending on depth**.

## 11. Independent Test
> In an isolated non-production environment, submit marked, clearly synthetic "confidential" test content (simulated account numbers, simulated deal terms) through the AI system's normal usage paths, including any agentic/tool-chained paths. Trace the content's propagation: (1) does it appear in third-party model provider logs or training-eligible storage per contractual terms; (2) does it appear in observability/APM tooling logs; (3) does it propagate to any downstream tool call or sub-agent context. Cross-check findings against the data-flow map and provider contract terms. Methodology per DSIT AI Cyber Security Code of Practice (2025) data-flow mapping principle and OWASP LLM02:2025 guidance. Synthetic marker content only; no real confidential data used in the test itself. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the underlying data-flow-mapping discipline is standard security practice with mature general methodology, but there is no AI-specific, cross-institution standardised test procedure for telemetry/logging egress paths specifically — this sub-area is newer and less benchmarked than direct model-prompt confidentiality testing, so rated below IRQ-SEC-006's ★3).

## 12. Pass Indicators
- Marked test content is not found in any telemetry/logging destination outside the firm's contractual control boundary.
- Provider contract terms confirmed (not merely asserted) to exclude training/retention use of submitted content, or such use is explicitly consented to and risk-accepted.
- DLP/filtering demonstrably blocks or flags confidential-category content before transmission.
- Data-flow map is current, covers all AI-adjacent paths including telemetry, and was independently verified (not self-declared by the platform team).

## 13. Fail Indicators
- Marked test content appears in an observability/logging destination not covered by the data-flow map or contract review.
- Provider contract is silent or ambiguous on training/retention use, with no compensating technical control.
- DLP/filtering does not exist or does not cover the categories of confidential data actually in use.
- Acceptable-use policy exists but is not technically enforced — staff can and do paste confidential content with no system-level prevention.

## 14. Reporting Language
**Pass:** "Data-flow mapping across all AI-adjacent paths — model API, embedding store, and telemetry/observability pipelines — confirms no confidential test content egresses to environments outside the firm's contractual control. Provider retention/training terms are contractually verified, and DLP filtering is technically confirmed. Testing rated ★2, reflecting the newer, less-benchmarked nature of telemetry-egress-specific testing; recommend this control area's evidence be refreshed at each material platform or vendor change."

**Fail:** "Testing found that submitted content, including simulated confidential markers, appears in [an observability vendor's logs / a telemetry pipeline] not covered by the current data-flow map or vendor contract review. This is an active, uncontrolled confidentiality egress path affecting all users of the platform, not a single incident, and requires immediate remediation of logging configuration and vendor contract terms."

**Partial:** "The primary model-API data flow is mapped and controlled, but the observability/APM tooling used for platform monitoring was not included in the original vendor due diligence and its data-capture behaviour is unverified. The assurance objective is not met until this secondary pipeline is reviewed and, if necessary, remediated."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (confidential firm/customer data disclosed outside the firm's control boundary;
              regulatory notification risk)
  Likelihood: 2 (plausible if a secondary pipeline is missed in due diligence; mitigated by
              complete data-flow mapping and DLP)
  Detectability: 3 (egress via a secondary, unreviewed pipeline is not typically monitored;
              detection often requires a dedicated audit rather than routine monitoring)
  Recoverability: 3 (remediation requires contract renegotiation or logging reconfiguration
              and, potentially, deletion requests to the third party; days-to-weeks)
  Novelty: 3 (data-flow mapping is standard security practice, but its AI-specific extension
              to prompts/context/telemetry is not yet routine in FS vendor due diligence)

Interpretation: acceptable with complete data-flow mapping including telemetry; highest
concern is that secondary pipelines (observability, APM) are systematically under-reviewed
relative to the primary model-API relationship.

If controls are absent or degraded:
  Severity: 3 (systemic, affecting all users of the platform, not a single incident)
  Likelihood: 3 (default logging behaviour commonly captures full prompt/response content
              unless deliberately configured otherwise)
  Detectability: 4 (silent; discovered typically only via audit, DSAR, or third-party breach
              notification, not routine monitoring)
  Recoverability: 3 (contractual and technical remediation; potential regulator engagement)
  Novelty: 3
Residual risk: Critical if secondary telemetry pipelines are unreviewed, given the systemic
(all-users) nature of the exposure.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Confidential data disclosed outside the firm's control boundary; regulatory notification risk; systemic if the cause is a default logging setting rather than an individual error. |
| **Likelihood** | 3 | Probable if secondary telemetry/observability pipelines are not included in AI vendor due diligence, which is common practice today. |
| **Detectability** | 4 | Silent by default; typically discovered only via dedicated audit, DSAR, or third-party breach notification rather than routine monitoring. |
| **Recoverability** | 3 | Requires contractual renegotiation, logging reconfiguration, and potentially third-party deletion requests; not fast. |
| **Novelty** | 3 | Data-flow mapping is standard practice, but its extension to AI-specific secondary pipelines (telemetry, embeddings) is not yet routine, making this a partial rather than total blind spot for security-literate SMEs. |

## 17. Regulatory Basis
> [UK GDPR Art. 5(1)(f), Art. 28 (processor obligations), Art. 32] — engaged directly wherever confidential personal data egresses to a third party without an established lawful basis and appropriate contractual/technical controls. [DSIT, AI Cyber Security Code of Practice, Jan 2025] — data-flow mapping as a core secure-AI-operation principle. [PRA SS1/23 Model Risk Management] and [FCA SYSC 8 outsourcing requirements] — where a third-party AI provider constitutes outsourcing/material third-party reliance, governance of data handling is a direct regulatory expectation.

## 18. Research Basis
> [OWASP Foundation, 2025, "Top 10 for LLM Applications 2025", LLM02 Sensitive Information Disclosure] — direct classification of this failure mode with mitigation guidance. [DSIT, "AI Cyber Security Code of Practice", January 2025] — UK-specific secure-AI-operation principles including data-flow mapping. No peer-reviewed academic paper specifically addresses telemetry/observability-pipeline egress for AI systems as a distinct research topic; this control area rests primarily on standards/regulatory sources rather than academic literature — noted as a comparative evidentiary gap versus other SEC IRQs.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-SEC-006 (E.2: system-prompt/secrets extraction — a related but distinct egress
    surface, adversarially induced rather than default-configuration-driven)
  - IRQ-TPR-007 (F.3: provider retention/training-on-firm-data — the contractual counterpart
    to this technical/architectural IRQ)
  - IRQ-DAT-009 (A.3: entitlement enforcement — should extend to logged/telemetry copies)
  - IRQ-GOV-002 (I.1: shadow AI inventory completeness — unreviewed tools are the highest-risk
    egress source)
  - IRQ-GOV-005 (I.2: acceptable-use policy — technical enforcement of what may be entered)
```

## 20. References
```
[1] OWASP Foundation, 2025. "OWASP Top 10 for LLM Applications 2025." LLM02:2025 Sensitive
    Information Disclosure.
[2] DSIT, 2025. "AI Cyber Security Code of Practice." January 2025.
[3] UK GDPR, retained EU law, Articles 5, 28, 32.
[4] FCA Handbook, SYSC 8 (Outsourcing).
[5] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.2 (Security domain, Extraction & Leakage)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Data governance SMEs map known systems of record; ad hoc prompt
  content and default AI-platform telemetry are not typically captured in existing data-flow
  inventories.
✓ Test 2 (Plausible Harm): Grounded in OWASP LLM02:2025 classification and DSIT AI Cyber
  Security Code of Practice (2025) data-flow mapping principle; UK GDPR mechanics through
  which the harm crystallises are well-established.
✓ Test 3 (Testable): Testable via staging content-propagation tracing across all AI-adjacent
  paths; ★2 methodology, honestly rated given the lack of AI-specific standardised testing
  for telemetry/observability egress.
✓ Test 4 (Decision-Relevant): Outcome gates whether AI vendor due diligence needs to extend
  beyond the primary model API to secondary telemetry/observability pipelines before
  confidential data may be processed.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
```

---
---

