# CANVAS: IRQ-TPR-008

## 1. IRQ ID & Title
**IRQ-TPR-008: Excessive Model/Cloud/GPU Provider Concentration Risk**

Register question: "Does dependence on a small number of model, cloud or GPU providers create concentration risk exceeding the firm's stated appetite, with credible substitution options?"

## 2. Business Activities Affected
- **Every AI-enabled business activity across the firm**, in aggregate: because most firms route the majority of AI workloads through one or two foundation model providers and a small number of hyperscale cloud/GPU providers, a single provider failure or material price/terms change has firm-wide reach.
- **Business continuity and important business service (IBS) delivery:** Where AI is embedded in an IBS, provider concentration directly determines the firm's ability to meet its impact tolerance if that provider becomes unavailable (links RES-001, RES-007).
- **Commercial negotiating position:** Concentration without credible substitution options weakens the firm's ability to negotiate price, terms or service levels.

## 3. AI Behaviour(s)
- Multiple, functionally distinct AI systems across the firm are built on the same underlying foundation model provider and/or the same cloud/GPU infrastructure provider, often for good technical and commercial reasons (integration ease, volume discounts, staff familiarity).
- This concentration is typically invisible at the level of any single system's risk assessment, because each individual deployment appears adequately diligenced and contracted (see TPR-001, TPR-002) in isolation.
- Aggregate exposure only becomes visible when mapped across the full AI inventory.

## 4. Failure Mode
> The firm's aggregate dependence on a small number of model, cloud or GPU providers exceeds its stated risk appetite for concentration, without the firm having measured this aggregate exposure or established credible, tested substitution options — so a single provider's failure, material change, or exit would affect multiple business activities simultaneously beyond the firm's tolerance.

## 5. Potential Consequences
- **Institution:** Simultaneous, correlated failure or degradation across multiple AI-dependent business activities if a single dominant provider suffers an outage, security incident, commercial failure, or unilaterally changes terms.
- **Market/systemic:** Aligns with the systemic concern flagged by the Bank of England's Financial Policy Committee — correlated AI/cloud provider concentration across the sector, not just within one firm, amplifying market-wide impact of a single provider event.
- **Regulator:** DORA critical ICT third-party provider (CTP) oversight regime and concentration risk reporting obligations are not met if aggregate exposure is unmeasured.

## 6. Failure Chain
```
Individual AI systems each independently select the same (or very
few) foundation model / cloud / GPU providers, each passing its own
due diligence and contracting review in isolation
  ↓ (IRQ-TPR-001/002: diligence and contracting are system-by-system,
     not aggregate)
No firm-wide aggregation of AI provider dependency exists across
the AI inventory
  ↓ (IRQ-TPR-008 — THIS IRQ: concentration risk is never measured
     against a stated appetite)
A dominant provider experiences an outage, security incident,
commercial failure, or exits the FS market / changes terms materially
  ↓ (IRQ-RES-001: fallback modes, if any, were designed per-system,
     not for a simultaneous multi-system event)
Multiple business activities are affected simultaneously; the firm's
aggregate impact exceeds any single system's individually-assessed
tolerance

Control Breakpoints:
  • IRQ-TPR-008: aggregate concentration measurement against stated appetite
  • IRQ-RES-007: AI dependencies mapped into IBS and scenario-tested for
    a correlated multi-system provider failure, not just single-system failure
  • IRQ-RES-001: fallback modes designed with awareness of shared dependency
```

## 7. Why a Domain Expert May Miss It
- Third-party risk review is typically conducted per-vendor, per-contract; no natural process aggregates "how many of our systems ultimately depend on Provider X" across the whole AI estate.
- Individual system owners have no visibility into other systems' provider choices, so concentration is invisible from any single vantage point within the firm.
- The commercial logic for concentration (volume discounts, integration ease, staff expertise) is individually rational for each system owner while being collectively risky — a classic aggregation blind spot that traditional per-system due diligence does not surface.
- "We have contracts with two cloud providers" can create a false sense of diversification if both ultimately depend on the same underlying GPU supply chain or the same foundation model family via API.

## 8. Assurance Objective
**AO-TPR-008:** The firm shall measure aggregate concentration of AI-related dependence on model, cloud and GPU providers across its full AI inventory, compare this against a board-stated risk appetite, and maintain credible, tested substitution options where concentration exceeds appetite.

## 9. Expected Controls (Traced)
- **Critical ICT third-party provider concentration assessment** — [Regulation (EU) 2022/2554, DORA, Chapter V (Managing of ICT third-party risk), Section II — Oversight Framework of critical ICT third-party service providers] — regime specifically targets systemic concentration risk from critical ICT/cloud providers, extending to AI infrastructure providers.
- **Aggregate third-party dependency mapping** — [PRA SS2/21, November 2024 (15 November 2024, updating 29 March 2021)] — expects firms to understand aggregate outsourcing exposure, not only individual arrangements.
- **Board-approved risk appetite with measurable concentration indicators** — [linked IRQ-GOV-006] — concentration is one measurable indicator within the firm's overall AI risk appetite statement.
- **Substitutability/exit strategy testing** — [Regulation (EU) 2022/2554, DORA, Art. 28(8) exit strategies] — exit strategies are required for ICT services supporting critical or important functions, with exit plans documented and sufficiently tested, proportionately under Art. 4(2).
- **Systemic AI/cloud concentration monitoring** — [Bank of England Financial Policy Committee, "Financial Stability in Focus: Artificial intelligence in the financial system," April 2025] — supervisory-level framing that firms should be aware of and responsive to, informing internal risk appetite calibration.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "we use multiple providers so we are diversified" with no supporting data — **L1**.
- Risk appetite statement defining measurable concentration indicators/thresholds — **L2**.
- Aggregate dependency map across the full AI inventory, showing concentration by provider (model, cloud, GPU) against appetite thresholds — **L3**.
- Independent audit or second-line review confirming the concentration measurement methodology and its accuracy against a sample of the inventory — **L4**.
- Board/risk committee MI showing concentration measured and reported against appetite over the last 12 months, including any breach escalations — **L5**.

**Dated worked example, added at the September 2026 refresh — a shared dependency the aggregate map will not show.** A frontier lab's September 2026 threat report records credential harvesters distributed as "malicious client side applications often spoofing as popular AI harnesses including Claude Code", taking "any AI related session tokens or API keys on the victim's device" and continuing to harvest new sessions after a reset, with the proceeds sold "through brokers, which often feed into fraudulent AI reseller networks"; the report separately describes resellers offering cheap access whose "traffic was in fact silently proxied to a different AI model" [Anthropic, *Detecting and countering misuse of AI: September 2026*, 10 September 2026, printed pp. 28–29]. The bearing on this IRQ is the §12 indicator that apparently diversified choices be "checked for shared underlying dependencies … rather than assumed independent": where access is procured through an intermediary, the model actually serving the traffic may not be the model the inventory records, and two nominally distinct providers may resolve to one. An aggregate dependency map built from the **inventory** rather than from the **procurement channel** will not show it.

## 11. Independent Test
> Using the firm's AI inventory (IRQ-GOV-002), independently aggregate provider dependency across model, cloud and GPU layers; calculate concentration (e.g. % of AI-dependent business activities reliant on a single provider at each layer) and compare against the stated risk appetite. Attempt to trace whether apparently diversified choices share a common underlying dependency (e.g. two "different" model providers both hosted on the same cloud infrastructure). Documentation-based test; no live provider systems accessed. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (DORA's critical-ICT-provider concentration concept provides regulatory grounding, but firm-level aggregate AI-specific concentration measurement methodology is still emerging practice with no standardised calculation approach — professional judgement dominates the aggregation methodology).

## 12. Pass Indicators
- Aggregate concentration is measured and reported against a board-approved appetite on a regular cadence.
- No single provider (at model, cloud or GPU layer) exceeds the stated concentration threshold, or breaches are escalated with a remediation plan.
- Substitution/exit strategies exist and have been tested (not merely documented) for at least the most concentrated dependency.
- "Diversified" provider choices are checked for shared underlying dependencies (e.g. common cloud infrastructure) rather than assumed independent.

## 13. Fail Indicators
- No aggregate concentration measurement exists; risk assessment is conducted only per-system.
- Risk appetite statement contains no measurable concentration indicator specific to AI providers.
- A dominant provider is found to exceed any reasonable concentration threshold with no escalation or remediation plan on record.
- Substitution/exit strategy, where documented, has never been tested even at a desk-based walkthrough level.

## 14. Reporting Language
**Pass:** "Aggregate AI provider concentration has been measured against the board-approved risk appetite, with no unremediated breaches identified; substitution strategy for the most concentrated dependency has been tested. Conclusions rest on ★2 methodology — DORA-grounded concept, but bespoke firm-level aggregation methodology with no standardised benchmark — and should be treated as a point-in-time professional assessment."

**Fail:** "No aggregate measurement of AI provider concentration exists; risk assessment has been conducted only at the individual-system level. The firm cannot evidence whether its aggregate dependence on a small number of model, cloud or GPU providers exceeds its own stated risk appetite, and no substitution strategy has been tested for the most material provider."

**Partial:** "Aggregate concentration has been measured for foundation model providers but not extended to the underlying cloud/GPU infrastructure layer, where genuine diversification may be lower than apparent. Remediation should extend the measurement methodology to all three layers (model, cloud, GPU)."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (correlated failure across multiple business activities if concentration is real, even if measured and monitored)
  Likelihood: 2 (measurement and appetite-setting reduce but do not eliminate the underlying structural concentration common across the sector)
  Detectability: 2 (aggregate measurement, if operating, provides visibility ahead of an event)
  Recoverability: 2 (tested substitution strategy enables recovery within a planned timeframe)
  Novelty: 3 (aggregation blind spot is structurally invisible from any single system's review; requires firm-wide perspective)

If controls are absent or degraded:
  Severity: 4 (a single dominant provider's failure or exit could simultaneously disrupt multiple important business services — systemic within the firm, and potentially contributing to sector-wide correlated impact per BoE FPC framing)
  Likelihood: 2 (provider-level failure/exit events are individually low-probability but the consequence, if one occurs, is amplified by unmanaged concentration)
  Detectability: 3 (concentration itself is invisible without aggregation; the triggering provider event, once it occurs, is obvious but too late for proactive substitution)
  Recoverability: 3 (untested substitution means recovery timeline is unpredictable, likely weeks-to-months, risking IBS impact tolerance breaches)
  Novelty: 4 (fully outside any single system owner's field of view; requires deliberate firm-wide aggregation)

Residual risk interpretation: This is a severity-and-novelty-dominant IRQ — individually low-likelihood provider failure events combine with genuinely high consequence and near-total structural invisibility absent deliberate aggregation, making it a priority for governance attention even though no single incident may ever be observed.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Correlated, multi-service impact if a dominant provider fails; escalates toward systemic if unmanaged |
| **Likelihood** | 2 | Individual provider failure/exit events are relatively rare, though structural concentration itself is common |
| **Detectability** | 3 | Concentration is invisible without deliberate aggregation across the AI inventory |
| **Recoverability** | 2 | Achievable within a planned recovery window if substitution strategy is tested in advance |
| **Novelty** | 4 | Aggregation blind spot is structurally undetectable from any single system's perspective |

## 17. Regulatory Basis
> [Regulation (EU) 2022/2554, DORA, Chapter V] establishes an oversight framework for critical ICT third-party providers explicitly targeting concentration risk, with Art. 28(8) requiring exit strategies and documented exit plans, sufficiently tested in accordance with the proportionality criteria of Art. 4(2). [PRA SS2/21, November 2024 (15 November 2024, updating 29 March 2021)] expects firms to understand aggregate outsourcing exposure across arrangements, not only individually. [Bank of England Financial Policy Committee, "Financial Stability in Focus," April 2025] frames AI/cloud provider concentration as a monitored systemic risk factor, informing the supervisory lens likely to be applied to firm-level concentration management.

## 18. Research Basis
> [Bank of England Financial Policy Committee, "Financial Stability in Focus: Artificial intelligence in the financial system," April 2025] provides the primary evidentiary basis, explicitly flagging concentration in a small number of AI/cloud providers as a systemic monitoring priority (verified 29 Jul 2026). No firm-level academic study of AI-specific concentration risk measurement methodology is confirmed in this repository's source registers [UNVERIFIED — no such firm-level methodology study was located after search; this remains a supervisory-level, not academic, evidence base] (verified 29 Jul 2026).
>
> **[FAIAS Incident Register, row 87, "Windsurf Claude capacity cut", 2025]** — the AI coding-tool vendor's own statement shows dependence on one provider's models, with substitute capacity "from other inference providers" that was, on its account, not enough at that length of notice to support all of the existing demand. The cause was a decision by the provider and not an outage, and the source holds no risk appetite or measure of aggregate exposure.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-RES-001 (G.1 Fallback & Degradation: fallback modes should account for shared dependency)
  - IRQ-RES-007 (G.4 Resilience Mapping: AI dependencies mapped into IBS scenario testing, incl. correlated provider failure)
  - IRQ-GOV-011 (I.4 Documentation, Records & Regulatory: regulatory obligation mapping incl. DORA CTP oversight regime)
  - IRQ-GOV-006 (I.2 Approval, Tiering & Policy: board-approved risk appetite with measurable indicators)
  - IRQ-TPR-001 (F.1 Due Diligence: procurement channel as a concentration input — an intermediary may resolve two nominally distinct providers to one)
  - IRQ-SEC-011 (E.4 Non-human identity and credentials: compromised keys are the mechanism by which a recorded dependency and the actual one diverge)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Chapter V and Art. 28(8).
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] Prudential Regulation Authority, 2024. "SS2/21 — Outsourcing and third party risk management."
    Published: November 2024 (15 November 2024, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/outsourcing-and-third-party-risk-management-ss

[3] Bank of England, Financial Policy Committee, 2025. "Financial Stability in Focus: Artificial intelligence in the financial system."
    Published: April 2025
    URL: https://www.bankofengland.co.uk/financial-stability-in-focus/2025/april-2025
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.3 (Third Party domain, Dependencies, Concentration & Data Handling)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Per-system due diligence cannot see firm-wide aggregate concentration; requires deliberate aggregation.
✓ Test 2 (Plausible Harm): Grounded in DORA's critical ICT third-party provider regime and BoE FPC's explicit AI/cloud concentration monitoring.
✓ Test 3 (Testable): Answerable via aggregate dependency mapping and substitution strategy testing.
✓ Test 4 (Decision-Relevant): Outcome gates risk appetite compliance and substitution investment priorities.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Expected Evidence — dated worked example added on procurement-channel dependency (harnesses spoofed to harvest credentials; resellers silently proxying to a different model, 10 Sep 2026). Related IRQs — TPR-001 and SEC-011 added. ★2 / P2 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS2/21 gives its current version, November 2024 (15 November 2024, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS2/21 cited as its November 2024 version (15 November 2024, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 87, Windsurf statement on a provider's withdrawal of model capacity, for substitute capacity that was not enough at that length of notice). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Fields 18 and 20 — the Financial Stability Report of July 2025 is no longer cited as a source on AI (the report has no section on AI, mentions AI only in passing, does not discuss cloud provider concentration, and points to the April 2025 Financial Stability in Focus), and its reference entry is removed. The April 2025 Financial Stability in Focus remains the evidentiary basis for AI and cloud provider concentration. Research-basis review date moved. No change to the ★ rating or the risk profile.
```

---
---

