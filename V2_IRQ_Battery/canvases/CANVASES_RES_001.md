# CANVAS: IRQ-RES-001

## 1. IRQ ID & Title
**IRQ-RES-001: Absent or Untested Fallback Mode for AI-Dependent Important Business Services**

Register question: "Is there a defined, tested fallback mode delivering the important business service within impact tolerance when the AI component is unavailable or untrusted?"

## 2. Business Activities Affected
- **Any important business service (IBS) with an embedded AI component:** payment processing support, claims triage, customer onboarding and fraud screening are increasingly AI-assisted; if the AI component fails or must be distrusted, the underlying customer-facing service still has a regulatory impact tolerance that must be met regardless.
- **Customer service and complaint handling:** AI-assisted response drafting or triage needs a manual fallback that staff can genuinely execute at volume, not a theoretical one.
- **Credit and underwriting decisioning:** Where AI materially speeds or shapes decisioning, a fallback to manual/legacy-rules processing must exist and be resourced, not merely documented.

## 3. AI Behaviour(s)
- AI component is embedded within a broader business process as a functional dependency (decision support, triage, drafting, screening), such that the process as currently designed assumes the AI component is available and trustworthy.
- When the AI component becomes unavailable (outage) or untrusted (quality incident, detected drift, security concern), the surrounding process has no automatic or well-rehearsed alternative path.
- Staff and systems downstream of the AI component are calibrated to its normal throughput and behaviour, not to a fallback mode's different characteristics (lower speed, different decision logic).

## 4. Failure Mode
> An important business service with an embedded AI component has no defined, resourced and tested fallback mode capable of delivering the service within its impact tolerance when the AI component becomes unavailable or untrusted, so an AI outage or quality incident directly threatens a regulatory impact tolerance breach rather than being absorbed by a rehearsed alternative.

## 5. Potential Consequences
- **Customer:** Service disruption or delay beyond what the firm's own impact tolerance permits — e.g. claims not processed, payments not actioned, complaints not responded to — during an AI outage or quality incident.
- **Institution:** Impact tolerance breach triggers mandatory regulatory notification and post-incident review under the UK operational resilience regime; reputational damage from visible service failure.
- **Regulator:** FCA SYSC 15A / PRA SS1/21 finding that the firm has not demonstrated resilience of an IBS specifically with respect to its AI dependency, notwithstanding a compliant IBS framework overall.

## 6. Failure Chain
```
AI component embedded into an IBS-supporting process; process design
assumes AI availability without an explicit fallback design step
  ↓ (IRQ-HUM-003: skill atrophy — even if a fallback exists on paper,
     staff may no longer be able to execute it to standard)
AI component becomes unavailable or untrusted (outage, quality
incident, detected drift, security concern)
  ↓ (IRQ-RES-001 — THIS IRQ: no tested fallback mode exists, or
     exists only in policy documentation, never exercised)
Process cannot deliver the IBS within impact tolerance; manual
workaround is improvised under pressure, inconsistent and slow
  ↓
Impact tolerance breach; regulatory notification obligation triggered;
post-incident review finds fallback was never rehearsed

Control Breakpoints:
  • IRQ-RES-001: fallback mode defined, resourced and tested against
    the actual impact tolerance, not just documented
  • IRQ-HUM-003: AI-free competency periodically assessed, not assumed
  • IRQ-TPR-008: concentration risk assessment informs how likely and
    how broad an AI unavailability event might be
```

## 7. Why a Domain Expert May Miss It
- Existing operational resilience frameworks were built around traditional IT/infrastructure failure modes (system outage, data centre loss); "the AI component gave an untrustworthy answer while remaining technically online" is a different failure mode that a standard fallback plan (built for outright unavailability) does not cover.
- Fallback plans are frequently written and approved once, then never exercised at realistic volume — a document existing is treated as equivalent to a capability existing.
- Op-res SMEs may assume "we have a manual process as backup" without verifying that manual process has been resourced at current volumes; AI adoption often coincided with headcount reduction in the very function meant to serve as fallback.
- The trigger for "untrusted" (as distinct from "unavailable") is rarely defined — who decides the AI output can no longer be trusted, and does that decision itself have a rehearsed process (links HUM-005, RES-003)?

## 8. Assurance Objective
**AO-RES-001:** For every important business service with an embedded AI component, the firm shall define, resource and periodically test a fallback mode capable of delivering the service within its stated impact tolerance when the AI component is unavailable or untrusted.

## 9. Expected Controls (Traced)
- **IBS mapping and impact tolerance setting** — [FCA, Handbook SYSC 15A.2.1R and 15A.2.5R, per PS21/3, March 2021] — every IBS has a defined impact tolerance against which fallback adequacy is measured.
- **Operational resilience self-assessment and scenario testing** — [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021), "Operational resilience: Impact tolerances for important business services"] — firms must test their ability to remain within impact tolerance under severe but plausible scenarios, extended here to AI component unavailability/untrustworthiness.
- **Fallback mode resourcing and rehearsal** — [FCA SYSC 15A.5.3R (scenario testing) / PRA SS1/21 combined expectation for tested, not merely documented, resilience arrangements] — fallback capacity is tested at realistic volume, not assumed.
- **AI-free competency assessment** — [linked IRQ-HUM-003] — periodic verification that staff can execute the fallback to standard without AI assistance.
- **Explicit "untrusted" trigger and decision authority** — [linked IRQ-HUM-005, IRQ-RES-003] — Emerging Practice for the AI-specific case; general escalation/authority principles are established, their application to "AI output no longer trusted" as a fallback trigger is less standardised.

## 10. Expected Evidence (Tagged L1–L5)
- Policy statement asserting "a manual fallback exists" with no test evidence — **L1**.
- Fallback process design document specifying trigger conditions, resourcing model and expected throughput — **L2**.
- Tabletop or live fallback exercise results: time to switch over, throughput achieved versus impact tolerance requirement — **L3**.
- Independent audit or internal resilience testing report confirming the fallback was exercised at a realistic volume and met impact tolerance — **L4**.
- Records of an actual AI unavailability/quality incident (if one occurred) showing the fallback was invoked and its real-world performance against impact tolerance — **L5**.
- **Note, 2–3 September 2026 — pending primary records.** Near-simultaneous multi-hour availability incidents were reported across more than one frontier model provider on 2–3 September 2026. This is the first real-world instance on this standard's file of the precise failure this IRQ tests — an AI component becoming unavailable across providers at the same time, which is the scenario a single-provider fallback design does not answer. **It is recorded here as a note and nothing is asserted about it:** no duration, no provider-by-provider figure, no correlation finding and no financial-services impact, because no provider status-page incident record has been retrieved and saved, and one trade-press attribution of a financial-services victim was withdrawn by its publisher's own account. The entry is completed, or removed, when the status-page incident records are fetched and saved; until then it stands as a reminder that this IRQ's fallback-adequacy test should be exercised against a *concurrent multi-provider* scenario and not only a single-provider one — **no evidence tier assigned.**

## 11. Independent Test
> In a non-production/staging environment, simulate AI component unavailability for the in-scope IBS and measure: (a) time to detect and trigger fallback, (b) fallback throughput at a volume representative of peak/average load, (c) whether the resulting service delivery meets the stated impact tolerance. Where the firm has run its own controlled live exercise of the fallback, its results — observed by the reviewer or taken from the firm's records — are admissible evidence, identified as such (METHODOLOGY_STANDARDS.md §3); the reviewer does not run a live exercise. Compare design and results against the firm's own IBS mapping and impact tolerance documentation. Methodology follows established UK operational resilience scenario-testing practice (FCA SYSC 15A / PRA SS1/21), applied to an AI-specific trigger. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (scenario testing against impact tolerance is established, regulator-mandated practice; the AI-specific trigger condition and "untrusted" determination are less standardised, moderating confidence from ★4).

## 12. Pass Indicators
- Fallback mode is defined with explicit trigger conditions covering both unavailability and "untrusted" states.
- Rehearsed exercise demonstrates throughput sufficient to meet the IBS's impact tolerance.
- Staff executing the fallback demonstrate current competency, not reliance on stale training.
- Trigger decision authority is named and has practised invoking the fallback.

## 13. Fail Indicators
- Fallback mode exists only as a policy statement; no rehearsal evidence exists.
- Rehearsed throughput falls materially short of impact tolerance requirements.
- No defined trigger for "untrusted" AI output exists; only outright technical unavailability is covered.
- Staff report inability to execute the fallback process to standard when tested.

## 14. Reporting Language
**Pass:** "A fallback mode for [IBS] has been defined, resourced and exercised, meeting the stated impact tolerance for both AI unavailability and untrusted-output trigger conditions. Conclusions rest on ★3 methodology — established op-res scenario testing extended to a less-standardised AI-specific trigger — and should be read as professional assessment of a genuinely tested capability."

**Fail:** "No tested fallback mode exists for [IBS]; policy documentation asserts a manual process exists, but no rehearsal or throughput evidence supports this claim. This is a direct operational resilience gap: an AI outage or quality incident in this service would put the firm's impact tolerance commitment at immediate risk."

**Partial:** "A fallback mode has been rehearsed for outright AI unavailability but not for the 'untrusted output' trigger condition, which currently has no defined decision authority or rehearsed process. Remediation should extend scenario testing to cover quality-degradation triggers, not only technical outage."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (temporary service degradation, contained within impact tolerance by design)
  Likelihood: 2 (AI component failures/quality incidents are plausible over an extended horizon, not routine)
  Detectability: 2 (unavailability is typically immediately visible; "untrusted" state detection depends on RES-005/006 maturity)
  Recoverability: 2 (fallback, once triggered, restores service within impact tolerance by design)
  Novelty: 3 (the "untrusted but technically available" trigger is a genuinely AI-specific concept beyond traditional outage-based fallback design)

If controls are absent or degraded:
  Severity: 3 (impact tolerance breach with mandatory regulatory notification; customer-facing service disruption)
  Likelihood: 3 (probable over time given AI components do fail, degrade or require deliberate suspension)
  Detectability: 2 (outright unavailability is obvious; quality-based "untrusted" triggers are harder to detect absent RES-005/006)
  Recoverability: 3 (improvised manual workaround is slow to stand up and inconsistent; recovery to full compliance may take days)
  Novelty: 3 (traditional resilience testing may not have exercised this specific trigger)

Residual risk interpretation: Acceptable where fallback is genuinely rehearsed against both trigger types; the "untrusted output" trigger is the weakest point across most firms observed to date and merits explicit testing focus.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Direct impact tolerance breach risk with mandatory regulatory notification if fallback fails |
| **Likelihood** | 2 | AI component failure/quality incidents are foreseeable but not routine over a typical assessment horizon |
| **Detectability** | 2 | Outright unavailability is immediately visible; "untrusted" state detection depends on separate monitoring maturity |
| **Recoverability** | 2 | Fallback, if genuinely rehearsed, restores compliant service promptly; untested fallback risks prolonged disruption |
| **Novelty** | 3 | The "untrusted-but-available" trigger extends traditional outage-based resilience thinking into AI-specific territory |

## 17. Regulatory Basis
> [FCA, Handbook SYSC 15A.2.1R, 15A.2.5R and 15A.2.9R, per PS21/3, March 2021, "Building operational resilience"] requires firms to identify important business services, set impact tolerances, and be able to remain within them for each IBS. [PRA, SS1/21, March 2022 (11 March 2022, updating 29 March 2021), "Operational resilience: Impact tolerances for important business services"] requires mapping and severe-but-plausible scenario testing to evidence this capability, which this IRQ extends explicitly to AI component unavailability/untrustworthiness as a scenario type.

## 18. Research Basis
> No peer-reviewed academic literature is required to establish this risk; it is a direct application of the established UK operational resilience regulatory framework to a newer dependency type (embedded AI components) rather than a novel research finding. [CORRECTED & VERIFIED — CMORG has published "AI Baseline Guidance Review" (Version 1.0, January 2025 cover date; published 15 May 2025; TLP Clear), CMORG AI Taskforce guidance (cmorg.org.uk) and, more recently, "Firm Guidance for Frontier AI" v1.0 (June 2026 cover date, TLP CLEAR), which together provide a reference-reading compilation across governance/risk/technical/legal themes and a set of frontier-AI cyber-preparedness expectations; **none of them specifies AI-component fallback *design* standards at the granularity this IRQ addresses, so "none established" at this specific level remains accurate** — re-checked against the June 2026 document] (verified 29 Jul 2026; currency re-verified 11 Sep 2026).
>
> **[FAIAS Incident Register, row 2, "Knight Capital deployment error", 2012]** — the supervisor found, in an order entered on the firm's offer of settlement and to which the firm consented without admitting or denying the findings, that the firm "did not have procedures in place to halt SMARS's operations in response to its own aberrant activity", that it "did not have supervisory procedures concerning incident response" and "relied primarily on its technology team to attempt to identify and address the SMARS problem in a live trading environment", and that it "needed clear guidance for its technology personnel as to when to disconnect a malfunctioning system from the market" [Securities and Exchange Commission, 2013, "In the Matter of Knight Capital Americas LLC", Admin. Proc. File No. 3-15570, Rel. No. 34-70694, 16 October 2013, ¶¶21, 27, 42]. This is the untrusted-but-available trigger evidenced in a financial-services setting, as an automation analogue predating current AI components. **[FAIAS Incident Register, row 40, "Eight Sleep cloud outage", 2025]** — a service dependent on a hosted component could not be adjusted by its users when that component became unreachable, with no degraded mode available to them, and the operator built an offline control path only after the event: the unavailable trigger, and the ordinary sequence in which fallback design follows rather than precedes the first outage. The deployment is outside financial services; the offline path and its timing are the operator's own account, and the devices' state rests on users' reports carried by the press.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-003 (D.2 Skill Atrophy: AI-free competency periodically assessed)
  - IRQ-RES-003 (G.2 Containment & Recovery: decision authority to trigger fallback/halt)
  - IRQ-TPR-008 (F.3 Concentration: informs likelihood/breadth of AI unavailability events)
  - IRQ-RES-007 (G.4 Resilience Mapping: AI dependency explicitly mapped into IBS scenario testing)
```

## 20. References
```
[1] Financial Conduct Authority, 2021. "PS21/3 — Building operational resilience." Handbook SYSC 15A.
    Published: March 2021
    URL: https://www.fca.org.uk/publications/policy-statements/ps21-3-building-operational-resilience

[2] Prudential Regulation Authority, 2022. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2022 (11 March 2022, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss

[3] Securities and Exchange Commission, 2013. "In the Matter of Knight Capital Americas LLC." Admin. Proc. File No. 3-15570, Rel. No. 34-70694.
    Published: 16 October 2013
    URL: https://www.sec.gov/files/litigation/admin/2013/34-70694.pdf
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.1 (Operational Resilience domain, Fallback & Degradation)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Traditional resilience testing covers outright outage; the "untrusted but available" AI-specific trigger is commonly untested.
✓ Test 2 (Plausible Harm): Grounded directly in the FCA/PRA operational resilience regime's impact tolerance requirement.
✓ Test 3 (Testable): Answerable via simulated unavailability/untrusted-state exercise measured against impact tolerance.
✓ Test 4 (Decision-Relevant): Outcome gates whether the IBS resilience self-assessment can rely on the AI fallback as evidenced.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Field 10 — a note recorded on the 2–3 Sep 2026 near-simultaneous multi-provider availability incidents, deliberately carrying no figures, no provider comparison and no financial-services impact pending retrieval of the provider status-page records, and flagging that the fallback-adequacy test should be exercised against a concurrent multi-provider scenario. Field 18 — CMORG currency erratum: "Firm Guidance for Frontier AI" v1.0 (June 2026) named alongside the May-2025 Baseline Guidance Review, with the "none established" conclusion re-checked against it and restated unchanged. ★3 unchanged.
- v1.2.1 (2026-09-19): Field 18 — incident-register citations added in the reserved form as a separate paragraph, evidencing both triggers: row 2 for the untrusted-but-available trigger in a financial-services setting, and row 40 for the unavailable trigger, the latter carried with its reservations that the devices' state rests on users' reports and that the deployment is outside financial services. Reference entry [3] added at Field 20 for the SEC order. The statement that no peer-reviewed academic literature is required to establish this risk is unchanged. Research-basis review date moved. ★3 unchanged.
- v1.3.0 (2026-10): Field 9 — the scenario-testing citation corrected from FCA SYSC 15A.5.1R, the testing-plan rule, to 15A.5.3R, the rule that requires scenario testing against a severe but plausible disruption. Field 11 — the controlled live exercise is the firm's own: the reviewer may observe it or use its results as evidence, identified as such under the non-production rule (METHODOLOGY_STANDARDS.md §3), and does not run it. Method and ★3 unchanged.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS1/21 gives its current version, March 2022 (11 March 2022, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/21 cited as its March 2022 version (11 March 2022, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 18 — the CMORG AI Baseline Guidance Review cited by its cover date, Version 1.0, January 2025, with its publication date, 15 May 2025, in place of a May 2025 cover date. Research-basis review date moved. The ★ rating and the risk profile are unchanged.
```

---
---

