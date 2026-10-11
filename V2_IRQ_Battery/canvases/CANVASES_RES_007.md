# CANVAS: IRQ-RES-007

## 1. IRQ ID & Title
**IRQ-RES-007: AI Dependencies Absent from IBS Mapping and Scenario Testing**

Register question: "Are AI dependencies mapped into the firm's important business services and scenario testing, including severe-but-plausible AI-specific scenarios?"

## 2. Business Activities Affected
- **Every important business service (IBS) with any AI dependency**, directly: the firm's core operational resilience self-assessment (mandated for all IBS) is incomplete, and therefore potentially misleading to the Board and regulators, if AI components are not explicitly mapped as dependencies.
- **Scenario testing programme design:** severe-but-plausible scenario libraries built before significant AI adoption may not include AI-specific scenario types (provider outage, model behavioural drift, agentic runaway action), leaving genuine tail risks untested.
- **Board and regulatory reporting on operational resilience:** self-assessment reports that omit AI dependencies present an incomplete resilience picture regardless of how well other IRQs in this canvas set are individually addressed.

## 3. AI Behaviour(s)
- AI components (models, agents, RAG pipelines, embedded vendor AI) sit within the technology and process stack supporting one or more IBS, functioning as a dependency in the same sense as a database, a payment rail, or a third-party data feed.
- The firm's existing IBS mapping and dependency documentation, built under the general operational resilience framework, may not have been explicitly extended to capture AI components as a distinct, first-class dependency category.
- Scenario testing exercises severe-but-plausible events against mapped dependencies; unmapped dependencies are, by construction, never scenario-tested.

## 4. Failure Mode
> AI components are not explicitly mapped as dependencies within the firm's important business service resilience framework, and severe-but-plausible AI-specific scenarios (provider outage, model behavioural drift, agentic misbehaviour) are absent from scenario testing, so the firm's operational resilience self-assessment is materially incomplete with respect to an increasingly significant class of dependency.

## 5. Potential Consequences
- **Institution:** Operational resilience self-assessment presented to the Board and, where relevant, to regulators is materially incomplete, understating true dependency and vulnerability; a real AI-specific incident falls outside any previously-tested scenario, leaving the firm's response genuinely untested rather than merely under-rehearsed.
- **Customer:** An AI-specific severe-but-plausible event (e.g. correlated provider outage affecting multiple IBS simultaneously, per TPR-008) occurs without the firm having ever exercised its response, extending both detection and recovery time.
- **Regulator:** Direct finding against FCA SYSC 15A.6.1R (the written self-assessment record) / PRA SS1/21 self-assessment completeness requirements, given AI dependency mapping is a natural and foreseeable extension of the existing mandatory framework.

## 6. Failure Chain
```
IBS mapping exercise conducted (or last refreshed) without an
explicit, deliberate step to identify AI components as a distinct
dependency category
  ↓ (IRQ-GOV-002: AI inventory itself may be incomplete, compounding
     the mapping gap at source)
Scenario testing library is built against the (AI-incomplete)
dependency map; no AI-specific severe-but-plausible scenarios are
included (provider outage, silent model drift, agentic runaway
action, correlated multi-provider concentration event)
  ↓ (IRQ-RES-007 — THIS IRQ: the resilience programme has a
     structural blind spot at the mapping stage, before any
     individual control failure)
A real AI-specific severe event occurs; the firm's response is
genuinely improvised, not merely under-rehearsed, because the
scenario was never contemplated
  ↓
Extended impact tolerance breach; post-incident review finds the
event type was foreseeable (documented in this canvas set and
public regulatory/industry commentary) but was never scenario-tested

Control Breakpoints:
  • IRQ-RES-007: AI dependencies explicitly mapped into IBS
    documentation and scenario testing programme
  • IRQ-GOV-002: complete AI inventory feeds accurate dependency mapping
  • IRQ-TPR-008: concentration risk assessment informs which
    AI-specific scenarios are genuinely severe-but-plausible
```

## 7. Why a Domain Expert May Miss It
- Operational resilience teams built their IBS mapping methodology under the 2021 FCA/PRA framework, largely before GenAI/agentic adoption became material; the methodology itself may not have an explicit prompt to consider "AI component" as a distinct dependency type, so it is missed by omission rather than deliberate exclusion.
- AI components are often embedded inside a broader technology service (e.g. "the customer service platform") in dependency documentation, obscuring the AI-specific sub-dependency (the underlying model provider) that carries its own distinct failure characteristics.
- Scenario testing libraries tend to be refreshed incrementally, carrying forward prior years' scenarios with additions rather than a full re-derivation; AI-specific scenario types may simply never have been proposed for inclusion.
- Resilience SMEs may reasonably (but incorrectly) assume that "if the AI system fails, that's just a system outage, already covered by our existing IT outage scenario" — missing that AI-specific failure modes (silent drift, agentic action, correlated provider concentration) are qualitatively different from a binary system-up/system-down outage.

## 8. Assurance Objective
**AO-RES-007:** The firm shall explicitly map AI dependencies into its important business service resilience documentation and include severe-but-plausible AI-specific scenarios (provider outage, model behavioural drift, agentic misbehaviour, correlated concentration events, disruption by externally originated synthetic media) within its scenario testing programme.

## 9. Expected Controls (Traced)
- **IBS mapping including AI-specific dependency identification** — [FCA, Handbook SYSC 15A.4.1R, per PS21/3, March 2021] — mapping of resources (people, processes, technology, facilities, information) supporting each IBS, explicitly extended to identify AI components as a distinct technology dependency category.
- **Severe-but-plausible scenario testing including AI-specific scenario types** — [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021)] — scenario library explicitly includes AI provider outage, silent model drift, agentic misbehaviour, correlated multi-provider concentration events and, as scenario content, disruption of an important business service by externally originated synthetic media [Financial Stability Board, 14 November 2024, §4.2.5, p.26 and footnote 112], the last scoped to the firm's own response.
- **AI inventory as an input to dependency mapping** — [linked IRQ-GOV-002] — mapping accuracy depends on the completeness of the underlying AI inventory.
- **Concentration-informed scenario design** — [linked IRQ-TPR-008] — scenario severity/plausibility informed by measured provider concentration, not assumed diversification.
- **Cross-industry AI resilience scenario libraries** — Emerging Practice — [CORRECTED & VERIFIED — CMORG has published general AI risk reference guidance ("AI Baseline Guidance Review", Version 1.0, January 2025 cover date; published 15 May 2025) and, more recently, "Firm Guidance for Frontier AI" v1.0 (June 2026 cover date, TLP CLEAR), but **no AI-specific severe-but-plausible scenario library was located in either; "still developing" remains an accurate characterisation** — the June 2026 document mentions scenarios only in passing and contains no scenario library] (verified 29 Jul 2026; currency re-verified 11 Sep 2026) — sector-level scenario libraries for AI-specific severe-but-plausible events are still developing.

## 10. Expected Evidence (Tagged L1–L5)
- IBS mapping document that references "technology" generically with no AI-specific dependency identification — **L1**.
- Updated IBS mapping methodology explicitly including an AI dependency identification step — **L2**.
- Sampled IBS mapping output showing AI components identified as distinct dependencies, cross-checked against the AI inventory for completeness — **L3**.
- Internal audit or second-line review confirming the scenario testing library includes AI-specific severe-but-plausible scenarios and that at least one has been exercised — **L4**.
- Board/risk committee papers over the last 12 months showing AI-specific scenario testing results and any resulting remediation actions — **L5**.

## 11. Independent Test
> For a sample of important business services with known AI dependencies (cross-checked against the AI inventory), review the current IBS mapping documentation to confirm AI components are explicitly identified as dependencies. Review the current scenario testing library to confirm inclusion of AI-specific severe-but-plausible scenario types. Where a relevant scenario has been exercised, review the test design and results for adequacy. Confirm that the severe-but-plausible scenario library includes at least one scenario in which an important business service is disrupted by externally originated synthetic media — a fabricated image, recording or video concerning the firm, its executives, or a market in which it operates — and that the scenario is scoped to the firm's own response, communications and impact-tolerance position, not to preventing the fabrication. The scenario tests the completeness of the firm's own resilience programme; the firm's resistance to the fabrication itself lies outside FAIAS under the scope exclusion stated in TAXONOMY.md. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (IBS mapping and scenario testing methodology is an established, regulator-mandated discipline; the specific extension to AI-specific scenario content is less standardised across the industry, moderating confidence from ★4).

## 12. Pass Indicators
- Sampled IBS mapping explicitly identifies AI components as dependencies, consistent with the AI inventory.
- Scenario testing library includes at least provider outage, model behavioural drift and agentic misbehaviour scenario types.
- The scenario testing library includes at least one scenario in which an important business service is disrupted by externally originated synthetic media, scoped to the firm's own response, communications and impact-tolerance position.
- At least one AI-specific scenario has been exercised within the current review cycle, with results reported to governance.
- Scenario severity/plausibility assessment is informed by actual measured concentration (TPR-008), not assumed diversification.

## 13. Fail Indicators
- IBS mapping documentation does not identify AI components as a distinct dependency category; AI is subsumed generically within "technology."
- Scenario testing library contains no AI-specific scenario types; only traditional infrastructure outage scenarios are tested.
- Scenario testing library holds none of the provider outage, model behavioural drift and agentic misbehaviour scenario types, whatever other AI-specific scenarios it holds.
- A materially AI-dependent IBS has never had an AI-specific scenario exercised.
- Cross-check against the AI inventory reveals known AI dependencies missing from the IBS mapping.
- The scenario library holds no scenario of disruption by externally originated synthetic media, or scopes such a scenario to preventing the fabrication rather than to the firm's own response.

## 14. Reporting Language
**Pass:** "Sampled IBS mapping explicitly identifies AI components as dependencies, consistent with the AI inventory, and the scenario testing library includes AI-specific severe-but-plausible scenarios that have been exercised within the current cycle. Conclusions rest on ★3 methodology — established mapping/scenario-testing discipline, AI-specific content extension less standardised — and should be read as professional assessment."

**Fail:** "Sampled IBS mapping does not identify AI components as dependencies despite known AI use within the service, and the scenario testing library contains no AI-specific scenario types. The firm's operational resilience self-assessment is materially incomplete with respect to AI dependency, and no AI-specific severe-but-plausible event has ever been exercised."

**Partial:** "AI dependencies are mapped for the flagship customer-service IBS but not yet extended to claims handling or AML investigation IBS, which also rely materially on AI components per the inventory. Remediation should extend the mapping methodology across all AI-dependent IBS at the next scheduled refresh." Where IBS mapping and the scenario testing library meet their pass indicators, but AI-specific scenarios have been exercised only in an earlier review cycle, or scenario severity/plausibility assumes diversification that measured concentration (TPR-008) does not support, the result is also Partial, and the Partial language names that gap.

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (an unmapped, untested AI-specific severe event affects an IBS's ability to meet its impact tolerance)
  Likelihood: 2 (mapping/scenario testing gaps are plausible given the framework's age relative to AI adoption pace, but improving as programmes mature)
  Detectability: 3 (surfaces at scheduled resilience self-assessment refresh or audit, not continuously)
  Recoverability: 2 (remediable by extending mapping/scenario methodology at the next refresh cycle)
  Novelty: 3 (requires recognising that AI dependency is qualitatively distinct from generic "technology" dependency for mapping purposes)

If controls are absent or degraded:
  Severity: 4 (a genuinely untested, unmapped AI-specific severe event could breach impact tolerance for one or more IBS with a wholly improvised response)
  Likelihood: 2 (individual severe events remain relatively rare, though the underlying dependency and its various failure modes are increasingly common)
  Detectability: 4 (the mapping gap itself is invisible until deliberately audited; the triggering event, when it occurs, is obvious but too late for proactive preparation)
  Recoverability: 3 (response to an unrehearsed, unmapped scenario is improvised, extending both detection and recovery time)
  Novelty: 4 (fully dependent on the resilience programme deliberately updating its methodology to treat AI as a first-class dependency category)

Residual risk interpretation: This IRQ is the resilience domain's equivalent of a foundational mapping gap — its consequence is realised only through a compounding severe event, but its presence undermines confidence in the entire domain's self-assessment completeness in the meantime.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | An untested AI-specific severe event directly threatens impact tolerance for the affected IBS |
| **Likelihood** | 2 | Individual severe events are relatively rare, though the underlying mapping gap itself is common given framework/adoption-pace mismatch |
| **Detectability** | 4 | The mapping gap is invisible until deliberately audited against the AI inventory |
| **Recoverability** | 3 | An unrehearsed response to a novel scenario type extends detection and recovery time materially |
| **Novelty** | 4 | Requires the resilience programme to deliberately recognise AI as a distinct, first-class dependency category rather than generic "technology" |

## 17. Regulatory Basis
> [FCA, Handbook SYSC 15A.4.1R, per PS21/3, March 2021] requires firms to map the resources supporting each important business service, which this IRQ interprets as necessarily including AI components where they materially support service delivery. [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021)] requires severe-but-plausible scenario testing to evidence resilience within impact tolerance, which this IRQ interprets as necessarily including AI-specific scenario types given their increasing materiality to IBS delivery.

## 18. Research Basis
> No peer-reviewed research is required to establish this risk; it follows directly from applying the established UK operational resilience mapping and scenario-testing methodology comprehensively to a materially significant, relatively new dependency class. [Bank of England Financial Policy Committee, "Financial Stability in Focus: Artificial intelligence in the financial system," April 2025] provides supervisory-level evidence that AI dependency is now considered a systemic-relevant factor, supporting the case that firm-level IBS mapping should explicitly capture it. [CORRECTED & VERIFIED — CMORG's published AI guidance comprises the "AI Baseline Guidance Review" (Version 1.0, January 2025 cover date; published 15 May 2025), a reading/reference compilation, and "Firm Guidance for Frontier AI" v1.0 (June 2026 cover date, TLP CLEAR), a set of frontier-AI cyber-preparedness expectations; **neither is scenario-testing methodology specific to AI, and no AI-specific scenario-testing guidance for the UK financial sector was located at time of review** — the June 2026 document was re-checked for this purpose] (verified 29 Jul 2026; currency re-verified 11 Sep 2026).
>
> [European Central Bank and EU national central banks, 2018, updated 2024, "TIBER-EU Framework: How to implement the European framework for Threat Intelligence-based Ethical Red Teaming"; Bank of England (with PRA and FCA), "CBEST Threat Intelligence-Led Assessments — Implementation Guide", current version] — the regulator-mandated threat-led testing regimes into which a firm's operational-resilience scenario programme already feeds. For this IRQ they establish the maturity bar for scenario design (intelligence-led, critical-function-scoped, independently executed) that AI-specific severe-but-plausible scenarios should meet when AI components are mapped into important business services; and where a firm's AI dependencies fall within a TIBER/CBEST scope, the reviewer should expect coherence between the FAIAS assurance evidence and the firm's threat-led testing scoping documents. This lets the review test the *interface* — verifying that AI systems supporting important business services appear in the firm's TIBER-EU/CBEST scoping and scenario inventories, and that FAIAS findings and threat-led testing findings cross-reference rather than pass each other in silence. **Boundary statement: TIBER-EU and CBEST are NOT tests FAIAS performs, and FAIAS assigns them no ★ rating.** FAIAS does not conduct, replicate, score or subsume threat-led penetration testing; per the scope decision recorded at v1.0.3, the resistance of the firm's controls, other than its own AI systems, to attack by external parties — including its identity, authentication and payment-authorisation controls — whether or not the attack uses AI, is out of FAIAS scope precisely because these regimes serve it. Their presence here is referential (grounding the scope exclusion recorded at v1.0.3) and contextual (informing this canvas's scenario-maturity expectations) only. No ★ change follows from this addition.
>
> [Financial Stability Board, 2024, "The Financial Stability Implications of Artificial Intelligence", 14 November, §4.2.5 "Other vulnerabilities", p.26] records that generative AI "could enable more sophisticated disinformation campaigns that have financial stability implications if they cause acute crises, such as flash crashes or bank runs", and names an instance: in May 2023 "a fake image of an explosion at the U.S. Pentagon, which was likely AI-generated, appeared to have affected equities markets, albeit briefly". Its footnote 112 gives further examples of disinformation that could precipitate acute crises — "fake images of depositor withdrawal lines or so-called deep fakes of finance executives and public authorities expressing negative information about institutions or markets" — each a scenario type a severe-but-plausible library would need to contemplate. The report states this as a vulnerability rather than a measured effect, and its own hedged wording is retained here.
>
> [Grance, T., Nolan, T., Burke, K., Dudley, R., White, G., Good, T., 2006, "Guide to Test, Training, and Exercise Programs for IT Plans and Capabilities", NIST Special Publication 800-84, September 2006] is the published method for designing, conducting and evaluating exercise events, and the field 11 review of the design and results of a scenario exercise can use its structure. Its chapters 4, 5 and 6 cover tabletop exercises, functional exercises and tests, each with a section on evaluating the event, and its Appendices A and B give sample after action reports. It is written for IT plans and capabilities. It has no AI scenario content, and it does not test whether the mapping of important business services is complete, so it informs the review of exercise design and results only. No ★ change follows from this addition.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-TPR-008 (F.3 Concentration: informs scenario severity/plausibility assessment)
  - IRQ-GOV-002 (I.1 Inventory & Ownership: AI inventory completeness feeds accurate mapping)
  - IRQ-GOV-011 (I.4 Documentation, Records & Regulatory: regulatory obligation mapping, incl. operational resilience self-assessment completeness)
  - IRQ-RES-001 (G.1 Fallback & Degradation: fallback design should be informed by scenario testing findings)
```

## 20. References
```
[1] Financial Conduct Authority, 2021. "PS21/3 — Building operational resilience." Handbook SYSC 15A.
    Published: March 2021
    URL: https://www.fca.org.uk/publications/policy-statements/ps21-3-building-operational-resilience

[2] Prudential Regulation Authority, 2022. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2022 (11 March 2022, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss

[3] Bank of England, Financial Policy Committee, 2025. "Financial Stability in Focus: Artificial intelligence in the financial system."
    Published: April 2025
    URL: https://www.bankofengland.co.uk/financial-stability-in-focus/2025/april-2025

[4] Financial Stability Board, 2024. "The Financial Stability Implications of Artificial Intelligence."
    Published: 14 November 2024. §4.2.5 "Other vulnerabilities", p.26 and footnote 112.
    URL: https://www.fsb.org/uploads/P14112024.pdf

[5] Grance, T., Nolan, T., Burke, K., Dudley, R., White, G., Good, T., 2006. "Guide to Test, Training, and Exercise Programs for IT Plans and Capabilities." NIST Special Publication 800-84. (Cited for exercise design and evaluation only.)
    Published: September 2006
    URL: https://csrc.nist.gov/pubs/sp/800/84/final
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.4 (Operational Resilience domain, Resilience Mapping)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): IBS mapping methodology predates material AI adoption; AI is subsumed generically within "technology" rather than mapped as a distinct dependency.
✓ Test 2 (Plausible Harm): Grounded directly in FCA SYSC 15A.4.1R (mapping) and 15A.5.3R (scenario testing) / PRA SS1/21 obligations and BoE FPC's AI systemic-risk framing.
✓ Test 3 (Testable): Answerable via cross-check of IBS mapping against the AI inventory and scenario library review.
✓ Test 4 (Decision-Relevant): Outcome gates the completeness of the firm's operational resilience self-assessment.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Fields 9 and 18 — CMORG currency errata: "Firm Guidance for Frontier AI" v1.0 (June 2026) named alongside the May-2025 Baseline Guidance Review at both sites, with the "no AI-specific scenario library" and "still developing" conclusions re-checked against the newer document and restated unchanged. Batched with the existing ANALYSIS_LOG CMORG cover-date erratum for these same sites. ★3 · P3 unchanged.
- v1.2.1 (2026-09-19): Fields 18 and 20 — Financial Stability Board, "The Financial Stability Implications of Artificial Intelligence" (14 November 2024), §4.2.5, p.26 and footnote 112, added for externally originated synthetic media as scenario content, with the report's own hedged wording retained. Field 11 — a scenario-completeness step added for that class, scoped to the firm's own response, communications and impact-tolerance position, with a sentence placing the firm's resistance to the fabrication itself outside the standard's scope; Fields 12 and 13 — one Pass and one Fail indicator added for that step. The widening concerns scenario completeness, not attack resistance. Field 8 — the assurance objective's scenario list names the same class. Field 9 — the traced scenario-library control names the class, citing the same report. Field 18 — the restatement of the scope exclusion recorded at v1.0.3 aligned to the published exclusion wording: the resistance of the firm's controls, other than its own AI systems, to attack by external parties — including its identity, authentication and payment-authorisation controls — whether or not the attack uses AI. Research-basis review date moved. ★3 · P3 unchanged.
- v1.3.0 (2026-10): Field 21 — the scenario-testing citation in the Four-Test footer corrected from FCA SYSC 15A.5.1R, the testing-plan rule, to 15A.5.3R, the scenario-testing rule. ★3 · P3 unchanged.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS1/21 gives its current version, March 2022 (11 March 2022, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 14 Reporting Language — the Partial entry adds that, where IBS mapping and the scenario library meet their pass indicators, AI-specific scenarios exercised only in an earlier review cycle, or a severity assessment that assumes diversification measured concentration does not support, give a Partial with the gap named. ★3 · P3 unchanged.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/21 cited as its March 2022 version (11 March 2022, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 13 Fail Indicators — a Fail indicator added for a scenario library that holds none of the provider outage, model behavioural drift and agentic misbehaviour scenario types, whatever other AI-specific scenarios it holds. The assurance objective is unchanged. ★3 · P3 unchanged.
- v1.3.3 (2026-10-09): Fields 9 and 18 — the CMORG AI Baseline Guidance Review cited by its cover date, Version 1.0, January 2025, with its publication date, 15 May 2025, in place of a May 2025 cover date. The ★ rating and the risk profile are unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — NIST SP 800-84 cited for exercise design and evaluation, with its scope limit stated. Field 20 References — entry [5] added. Research-basis review date moved. ★3 · P3 unchanged.
```
