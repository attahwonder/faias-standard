# CANVAS: IRQ-TPR-009

## 1. IRQ ID & Title
**IRQ-TPR-009: Vendor Financial Standing and Continuity on Vendor Failure**

Register question: "Does due diligence on AI vendors assess financial standing, funding runway and management integrity proportionate to materiality, in addition to the safety, security and model-weakness diligence already required — and can the firm retrieve its data, models, prompts and configurations and continue the service, in-house or via a substitute provider, if the vendor fails or exits mid-contract?"

## 2. Business Activities Affected
- **Any AI-enabled business activity dependent on a single vendor's continued operation:** credit decisioning, claims handling and customer service tooling built on a vendor's model or platform inherit that vendor's solvency risk regardless of how well the underlying system itself has been diligenced.
- **Business continuity and important business service (IBS) delivery:** where an AI vendor supports an important business service, an unplanned vendor exit tests the firm's ability to retrieve its data and configurations and to continue the service within impact tolerance.
- **Model risk sign-off:** an approval granted on the strength of a vendor's safety and security posture provides no assurance that the vendor will still exist, or still be solvent, for the life of the contract.

## 3. AI Behaviour(s)
- Firm integrates a third-party AI vendor's model, platform or API into a production or near-production workflow via contract and technical integration, in reliance on the vendor's continued commercial operation.
- The vendor's commercial standing — funding position, revenue durability, management stability — is not a technical property of the AI system and is not surfaced by safety or security diligence of the kind described in IRQ-TPR-001.
- On vendor failure or exit, the firm's ability to retrieve its own data, models, prompts and configurations, and to continue the service in-house or via a substitute, depends entirely on provisions made in advance, not on anything the vendor does in the moment of failure.

## 4. Failure Mode
> An AI vendor is onboarded and relied upon without due diligence on its financial standing, funding runway or management integrity, and without contractual or technical provision for data, model and configuration retrieval and service continuation — so a vendor failure or exit mid-contract leaves the firm unable to evidence that it assessed this risk in advance, and potentially unable to recover its own data or continue the dependent service at all.

## 5. Potential Consequences
- **Institution:** Loss of continuity of an important business activity if a vendor fails or exits mid-contract; potential inability to retrieve the firm's own data, prompts, model artefacts or configurations from a failed or insolvent entity; a costly, unplanned migration to a substitute provider under time pressure.
- **Customer:** Service interruption or degraded service to customers dependent on the affected workflow while the firm arranges continuity.
- **Regulator/market:** An outsourcing/third-party risk management deficiency finding if the firm cannot evidence that continuity risk was assessed proportionate to materiality; reputational exposure if a vendor failure becomes public and the firm is shown to have had no contingency in place.

## 6. Failure Chain
```
Vendor selected and diligenced on safety, security and model-weakness
grounds (IRQ-TPR-001); financial standing and continuity are not in
scope of that diligence by design
  ↓ (IRQ-TPR-009 — THIS IRQ: financial-standing and continuity
     diligence never separately performed)
Vendor experiences a funding shortfall, insolvency event, or
commercial wind-down
  ↓ (IRQ-TPR-002: contract lacks data/model/configuration retrieval
     rights or an exit path, if not separately secured)
Firm cannot retrieve its own data, models or configurations, and has
no tested continuation path in-house or via a substitute provider
  ↓
Dependent business activity is interrupted; incident investigation
finds no record that continuity risk was ever assessed

Control Breakpoints:
  • IRQ-TPR-009: financial-standing and continuity diligence, proportionate to materiality
  • IRQ-TPR-002: contractual retrieval and exit rights secured in advance
  • IRQ-RES-001: a designed and, where proportionate, tested continuation path
```

## 7. Why a Domain Expert May Miss It
- AI-specific due diligence, once introduced, tends to focus attention on safety evaluation coverage, security posture and known model weaknesses (see IRQ-TPR-001); financial-standing diligence is easily assumed to sit elsewhere, in a separate procurement or credit-risk process not tailored to AI-specific continuity risk, and can fall between the two.
- A vendor's safety and security posture can be strong even where its commercial position is fragile — the two are independent, and a reviewer satisfied on one may not think to check the other.
- Contractual exit and retrieval rights (see IRQ-TPR-002) are often assessed against an orderly termination scenario (non-renewal, planned exit) rather than a disorderly one (insolvency, sudden wind-down), which can behave very differently in practice.
- Early-stage or venture-funded AI vendors are common in this market by nature of how young the sector is; a reviewer unfamiliar with vendor financial-standing assessment may not recognise funding runway as a material, checkable fact rather than a matter of trust in the vendor's reputation.

## 8. Assurance Objective
**AO-TPR-009:** The firm shall assess the financial standing, funding runway and management integrity of AI vendors, proportionate to the materiality of the dependent business activity, in addition to safety, security and model-weakness diligence, and shall secure the ability to retrieve its data, models, prompts and configurations and continue the dependent service, in-house or via a substitute provider, if the vendor fails or exits mid-contract.

## 9. Expected Controls (Traced)
- **Materiality-tiered third-party risk assessment, extended to financial standing** — [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, Title IV, Section 12 (Pre-outsourcing analysis, incl. 12.3 Due diligence), with criticality determined under Title II, Section 4 (Critical or important functions)] — the Guidelines expressly require assessment of the provider's resources — "e.g. human, IT, financial" (§12.3 para 70) — and of its "financial situation, ownership and group structure" (para 71); only the AI-vendor-specific application is FAIAS's extension, since the Guidelines name no AI-specific criteria. [PRA SS2/21, Chapter 10 (business continuity and exit plans)] anchors the continuity limb.
- **Outsourcing and third-party risk oversight, including exit planning** — [PRA SS2/21, March 2021, "Outsourcing and third party risk management"] — proportionate due diligence and exit strategy provisions scaled to criticality, extending to financial-standing assessment of the provider.
- **Mandatory contractual exit and data-retrieval provisions** — [linked IRQ-TPR-002] [Regulation (EU) 2022/2554, DORA, Art. 28–30] — contracts for critical or important functions must secure termination rights, exit strategy and, in principle, the access, recovery and return of the firm's data on exit.
- **Continuity/substitution path design and testing** — [linked IRQ-RES-001] — a designed, and where proportionate tested, path to continue the dependent service in-house or via a substitute provider if the primary vendor becomes unavailable.
- **Financial-standing due diligence checklist for AI vendors specifically** — Emerging Practice — no published FS-specific standard names AI vendor financial-standing diligence as a distinct discipline; firms are extending general vendor financial-standing assessment practice to the AI vendor population.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor's own funding announcement or investor relations material, unverified — **L1**.
- Firm's due diligence policy naming financial standing, funding runway and management integrity as required assessment criteria for AI vendors, proportionate to materiality — **L2**.
- Completed due diligence file for a sampled vendor, evidencing a financial-standing assessment and, separately, documented data/model/configuration retrieval and continuation provisions — **L3**.
- Internal audit or second-line review confirming financial-standing diligence and continuity provisions were executed to policy standard across the critical-vendor population — **L4**.
- Outsourcing/vendor register showing financial-standing review status and continuity-plan status, refreshed at a defined cadence, for all in-scope AI vendors over the last 12 months — **L5**.

## 11. Independent Test
> For a materiality-stratified sample of AI vendors, review the due diligence file to confirm financial standing, funding runway and management integrity were assessed as a distinct item alongside (not folded into) safety and security diligence; separately review the contract for data, model and configuration retrieval rights and any documented continuation path. No production testing is possible or required. **No published testing methodology exists for this discipline; this is a due diligence and contract review item, described as such, not an empirical test.** — **★1 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (the mechanism — commercial failure risk sitting outside safety/security diligence — is well understood in general vendor risk management, but the AI-vendor-specific incident evidence base is thin, and no FS-specific benchmark or acceptance threshold exists for what "proportionate" financial-standing diligence looks like for an AI vendor).

## 12. Pass Indicators
- Financial-standing, funding runway and management integrity are assessed as a distinct, documented item in the due diligence file for critical-tier AI vendors, separate from safety/security diligence.
- Contractual data, model and configuration retrieval rights are evidenced, and a continuation path (in-house or substitute provider) is documented for the highest-materiality dependencies.
- Refresh cadence for financial-standing review is defined and evidenced, not a one-time check at onboarding.

## 13. Fail Indicators
- Due diligence files address only safety, security and model-weakness diligence, with no financial-standing or continuity content.
- No contractual retrieval rights or continuation path exist for a critical-tier vendor; reliance assumes indefinite vendor availability.
- Financial-standing review, where it exists, is a one-time check with no refresh mechanism as vendor circumstances change.

## 14. Reporting Language
**Pass:** "Financial-standing and continuity diligence, proportionate to materiality, is evidenced for sampled critical-tier AI vendors as a distinct item alongside safety and security diligence. Data and configuration retrieval rights are contractually secured and a continuation path is documented for the highest-materiality dependencies. Conclusions rest on ★1 methodology — the mechanism is well understood, but the AI-vendor-specific evidence base is thin and no benchmark exists — and should be read as professional assessment, not a certified compliance determination."

**Fail:** "Sampled AI vendor due diligence addresses only safety, security and model-weakness risk; financial standing, funding runway and continuity provisions are not assessed for [x]% of critical-tier vendors. The firm cannot evidence that it has considered what happens to a dependent business activity, or to its own data and configurations, if a vendor fails."

**Partial:** "Financial-standing diligence has been introduced for vendors onboarded under the current framework but not extended retrospectively to legacy vendor relationships. Remediation should prioritise the highest-materiality legacy dependencies first."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a single vendor failure is typically bounded to the specific workflow it supports; escalates if that workflow is a material or important business service)
  Likelihood: 2 (plausible given the AI vendor market includes many early-stage, venture-funded entities; mitigated where financial-standing diligence is routinely performed)
  Detectability: 3 (a vendor's deteriorating financial position is not visible through safety/security monitoring; typically surfaces via periodic financial-standing review or the failure event itself)
  Recoverability: 2 (recoverable via a pre-designed continuation path; materially slower and costlier if no such path exists)
  Novelty: 3 (financial-standing risk is a familiar concept in general vendor management, but its specific application to AI vendors — alongside, not instead of, safety/security diligence — is easy to overlook)

If controls are absent or degraded:
  Severity: 3 (an important business activity, or its data, may be lost or interrupted with no fallback)
  Likelihood: 2 (individual vendor failure events remain relatively infrequent, but the AI vendor population includes a higher proportion of early-stage entities than typical FS vendor populations)
  Detectability: 4 (silent by nature — nothing in safety/security diligence or monitoring would surface a vendor's commercial fragility)
  Recoverability: 3 (an untested or absent continuation path means recovery timelines are unpredictable, likely weeks-to-months, with possible permanent loss of retrievable data)
  Novelty: 3 (requires combined AI-vendor and financial-standing literacy not routinely present in either function alone)

Residual risk interpretation: Detectability is the dominant concern absent controls — a vendor's commercial fragility gives no technical signal. This IRQ is best treated as a proportionate, materiality-scaled addition to existing diligence rather than a new standalone process, given the currently thin evidence base reflected in the ★1 rating.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Bounded to the specific workflow supported by the failed vendor, unless that workflow is a material or important business service |
| **Likelihood** | 2 | Plausible given the prevalence of early-stage, venture-funded entities in the AI vendor market; not routine where diligence is performed |
| **Detectability** | 3 | Not visible through safety/security monitoring; surfaces via periodic financial-standing review or the failure event itself |
| **Recoverability** | 2 | Achievable within a planned recovery window if a continuation path was designed in advance; otherwise unpredictable |
| **Novelty** | 3 | Financial-standing risk is a familiar general concept but its specific application to AI vendor diligence is easy to overlook alongside safety/security focus |

## 17. Regulatory Basis
> [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, Title IV, Section 12 (Pre-outsourcing analysis, incl. 12.3 Due diligence)] require proportionate pre-contract due diligence for outsourced functions, expressly including the provider's resources ("e.g. human, IT, financial", §12.3 para 70) and its "financial situation, ownership and group structure" (para 71); the Guidelines name no AI-vendor-specific criteria — that gap, not the financial-standing requirement itself, is FAIAS's finding. [PRA SS2/21, March 2021, Chapter 10] anchors business continuity and exit planning. [Regulation (EU) 2022/2554, DORA, Art. 28–30] requires ICT third-party risk assessment before contracting and mandatory contractual provisions including termination rights and exit strategy, extending to data access, recovery and return. [PRA SS2/21, March 2021] sets outsourcing and third-party risk management expectations, including proportionate due diligence and exit planning scaled to criticality. No FS regulator has published guidance naming AI vendor financial-standing and continuity diligence as a distinct requirement; this IRQ extends established outsourcing risk management principles to the AI vendor context.

## 18. Research Basis
> No peer-reviewed research specifically addresses AI vendor financial-standing or continuity-on-failure risk as a discipline; this IRQ extends established general outsourcing and vendor risk management practice to the AI vendor context. **Mobley v. Workday, Inc.**, N.D. Cal., docket 3:23-cv-00770-RFL, order dated 12 July 2024 (permitting the case to proceed on an agent theory of vendor liability) is cited for the narrower principle that an AI vendor's own conduct and standing can become the firm's direct exposure — it concerns discrimination liability, not vendor insolvency or business continuity, and is not relied on here as evidence of the continuity-on-failure mechanism specifically. Beyond this, the specific continuity-on-vendor-failure incident evidence base for AI vendors remains thin; no verified incident of an AI vendor failure causing an FS firm continuity impact is cited in this canvas, which the ★1 rating reflects.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-TPR-001 (F.1 Due Diligence: safety, security and model-weakness diligence — deliberately excludes financial standing, which this IRQ covers)
  - IRQ-TPR-002 (F.1 Contracts & Licensing: exit, retrieval and portability rights that a continuation path depends on)
  - IRQ-RES-001 (G.1 Fallback & Degradation: continuation path design and testing)
```

## 20. References
```
[1] European Banking Authority, 2019. "Guidelines on outsourcing arrangements." EBA/GL/2019/02.
    URL: https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-outsourcing-arrangements
    Accessed: 2026-08-01

[2] European Union, 2022. "Regulation (EU) 2022/2554 on digital operational resilience for the financial sector (DORA)," Art. 28–30.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[3] Prudential Regulation Authority, 2021. "SS2/21 — Outsourcing and third party risk management."
    Published: March 2021
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/outsourcing-and-third-party-risk-management-ss

[4] Mobley v. Workday, Inc., United States District Court, Northern District of California, Case No. 3:23-cv-00770-RFL.
    Order (permitting agent-theory claim to proceed): 12 July 2024.
    Court docket: https://www.courtlistener.com/docket/66831340/mobley-v-workday-inc/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.1 (Third Party domain, Due Diligence, Contracts & Licensing)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): AI-specific diligence attention concentrates on safety, security and model weakness; financial-standing risk is easily assumed to sit in a separate, unconnected procurement process.
✓ Test 2 (Plausible Harm): Grounded in general outsourcing/vendor-risk regulatory principles (DORA, EBA outsourcing guidelines, PRA SS2/21) and the narrower vendor-exposure principle in Mobley v. Workday; the continuity-on-failure evidence base for AI vendors specifically is acknowledged as thin.
✓ Test 3 (Testable): Answerable via sampled due diligence file and contract review against a defined checklist.
✓ Test 4 (Decision-Relevant): Outcome bears on approval conditions for materially important vendor-dependent deployments.

**Change Log:**
- v1.0 (2026-08-01): Initial publication (v1.0.3 batch).
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```
