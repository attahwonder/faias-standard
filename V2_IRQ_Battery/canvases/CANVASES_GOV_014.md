# CANVAS: IRQ-GOV-014

## 1. IRQ ID & Title
**IRQ-GOV-014: Incident Taxonomy Without AI-Specific Failure Categories**

Register question: "Does the firm's incident classification scheme recognise AI-specific failure classes — mass confabulation, prompt-injection compromise, agentic misaction, silent bias event — with defined severity mapping and regulator-notification paths, such that the notification clock can start on an AI failure at all?"

## 2. Business Activities Affected
- **Any AI-influenced process whose failure mode falls outside conventional IT or fraud incident categories:** mass confabulation in a customer-facing generative assistant, a compromised system following prompt injection, an agentic system taking an unintended write action, or a bias pattern in decisioning output that is not itself a system outage — none of which naturally register as an "incident" under a taxonomy built for infrastructure failures and known fraud typologies.
- **Regulatory notification processes (ICT-incident reporting, Principle 11 notifications):** the notification clock depends on the firm first recognising the event as an incident; an AI failure class with no matching category delays that recognition, and therefore the clock, regardless of how the underlying notification rule is drafted.
- **Scope note:** this IRQ tests only whether the existing incident classification scheme's category list has AI-specific entries with defined severity mapping and notification routing — it does not test whether incident management, a severity matrix or notification processes exist at all; that is a separate, non-AI-specific control assessed elsewhere.

## 3. AI Behaviour(s)
- Generates plausible but fabricated content at scale (mass confabulation) in a way that produces no error state, exception or system alert distinguishable from normal operation.
- Can be induced, via prompt injection, to depart from its intended instructions while continuing to produce fluent, superficially normal output.
- Where agentic, can take an unintended or unauthorised action (an agentic misaction) through its own tool use, distinct from a human-initiated unauthorised transaction.
- Can produce a systematically biased pattern of output across a protected characteristic or cohort without any single output appearing anomalous in isolation (a silent bias event) — the failure is visible only in aggregate, not at the level of any one interaction an incident-response process would typically inspect.

## 4. Failure Mode
> The firm's incident classification scheme has no category — or no category with defined severity mapping and a notification route — for AI-specific failure classes (mass confabulation, prompt-injection compromise, agentic misaction, silent bias event), so an AI-specific event that occurs has nowhere to go on the intake form: it is either not identified and logged as an incident at all, or force-fitted into an ill-matching category that understates its severity or mis-routes its notification, and the regulatory-notification clock does not start, or starts late and on the wrong basis — not through concealment but because the taxonomy has no entry for it.

## 5. Potential Consequences
- **Customer:** Harm from an AI-specific failure (fabricated information relied upon, an unauthorised agentic action, a silent bias pattern) persists undetected and unescalated for longer than a conventionally categorised incident would, because no severity threshold or escalation path exists to trigger a response.
- **Institution:** The firm cannot demonstrate to a regulator that its incident management process actually covers its AI risk surface; where a notification duty is later found to have applied, the firm faces a finding that its own taxonomy prevented timely awareness, which is a materially worse position than a late notification following timely classification.
- **Regulator/market:** A supervisory finding that the incident taxonomy has no AI-specific entries — after ICT-incident classification and reporting obligations (DORA) and general notification duties (SUP 15.3) have applied for some time — signals that the firm's operational-resilience and governance frameworks have not kept pace with its AI deployment, inviting broader scrutiny.

## 6. Failure Chain
```
AI-specific failure occurs in production (mass confabulation at scale, a
successful prompt-injection compromise, an agentic misaction, or a silent bias
event visible only in aggregate)
  ↓ (IRQ-RES-005/006: monitoring may generate a signal, but the signal has
  nowhere to be classified against)
Incident classification scheme is checked against the event; no AI-specific
category exists, or an existing category (e.g. "system outage", "fraud", "data
breach") is a poor structural fit
  ↓ (IRQ-GOV-014 — THIS IRQ: the taxonomy's category list itself lacks
  AI-specific entries with severity mapping and notification routing)
Event is either force-fitted into an ill-matching category (understating
severity or mis-routing notification) or not classified as an incident at all
  ↓ (IRQ-GOV-008: even a correctly classified signal still depends on reaching
  an accountable governance body — a separate control this IRQ does not test)
Regulatory notification clock (DORA Art. 19; FCA SUP 15.3.1R) does not start,
or starts late and on the wrong basis
  ↓
Harm continues unaddressed / notification is late or absent → supervisory
finding that the firm's own taxonomy prevented timely classification →
enforcement/reputational damage compounding the underlying AI failure

Control Breakpoints:
  • IRQ-RES-005/006: monitoring produces a signal for the AI-specific event to
    be classified against in the first place
  • IRQ-GOV-014: incident taxonomy category list includes AI-specific failure
    classes with defined severity mapping and notification routing
  • IRQ-GOV-008: classified signal reaches an accountable governance body
  • IRQ-GOV-011: regulatory obligation mapping ensures the correct notification
    route (DORA/SUP 15.3) is known once the event is classified
```

## 7. Why a Domain Expert May Miss It
- Incident taxonomies are typically built and periodically reviewed by operational-resilience or cyber teams working from established categories (system outage, data breach, fraud, third-party failure); AI failure classes did not exist when the taxonomy was designed and are not obviously analogous to any existing category, so a taxonomy review that checks "is the list complete" against its own historical categories will not surface the gap.
- Mass confabulation and silent bias events produce no error state, alert or exception in the conventional IT-monitoring sense — the system is "working" throughout, in that it is available, responsive and not throwing errors — so an incident-detection mindset trained to look for system malfunction will not flag them as candidate incidents at all.
- Prompt-injection compromise can look, to a reviewer without AI-specific training, like a security event already covered by an existing "unauthorised access" or "data breach" category, obscuring that the injection mechanism, evidence trail and appropriate response differ materially from a conventional compromise.
- Agentic misaction is easily conflated with a conventional "unauthorised transaction" category built around a human actor circumventing controls, missing that the actor here is the system itself acting on its own tool permissions, which changes both the root-cause investigation and the remediation.

## 8. Assurance Objective
**AO-GOV-014:** The firm's incident classification scheme shall recognise AI-specific failure classes — at minimum mass confabulation, prompt-injection compromise, agentic misaction, and silent bias event — with defined severity mapping and a regulator-notification route for each, such that an AI-specific event can be classified and the notification clock can start.

## 9. Expected Controls (Traced)
- **ICT-related incident management process defining, establishing and implementing procedures to identify, track and categorise incidents by priority, severity and criticality, extended to include AI-specific category entries** — [DORA, Regulation (EU) 2022/2554, Art. 17; in force 16 January 2023, applies from 17 January 2025] — Art. 17's categorisation requirement presupposes that the event is first identified and logged as an incident; a taxonomy with no AI-specific failure class makes that unlikely for failures that raise no conventional error state.
- **Classification against the six DORA criteria (clients/counterparts affected and reputational impact; duration/downtime; geographical spread; data losses across availability, authenticity, integrity and confidentiality; criticality of services affected; economic impact), applied to AI-specific failure classes and mapped against the classification RTS materiality thresholds** — [DORA, Art. 18 and the classification Regulatory Technical Standards supplementing Art. 18(3)] — this control tests whether AI-specific events can be mapped to these criteria at all, not merely whether the criteria exist.
- **Three-report notification structure (initial, intermediate, final) to the competent authority for AI-specific events meeting materiality thresholds** — [DORA, Art. 19] — the notification mechanics exist regardless of AI-specificity; this control is that AI-specific events are actually routed into them.
- **UK notification route: immediate notification to the FCA on becoming aware of a matter that could have a significant adverse impact on the firm's reputation, could affect its ability to continue to provide adequate services to its customers and result in serious detriment to a customer, or could have serious financial consequences for the UK financial system or other firms** — [FCA, SUP 15.3.1R, as at 31/07/2026] — the "becomes aware" trigger depends on the firm first recognising the event as an incident; an AI failure class absent from the taxonomy delays that recognition and therefore the SUP 15.3.1R clock.
- **AI-specific category definitions with severity mapping and notification routing for mass confabulation, prompt-injection compromise, agentic misaction and silent bias event** — [Emerging Practice] — no published incident-taxonomy standard defines these four categories; DORA and SUP 15.3 supply the classification-and-notification architecture the categories must be added to, but the category definitions themselves have no external precedent and are marked accordingly.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the firm has an incident classification scheme" — **L1** (asserts a scheme exists; does not evidence AI-specific category coverage).
- Incident taxonomy documentation listing all defined categories, with severity mapping and notification routing shown for each — **L2**.
- Documentation review confirming whether mass confabulation, prompt-injection compromise, agentic misaction and silent bias event appear as distinct categories (or are explicitly and adequately mapped onto existing categories) with severity and notification routing defined — **L3**.
- Tabletop walk-through of one AI-specific failure class (e.g. a simulated mass-confabulation scenario) through the classification, severity-mapping and notification-routing steps, with gaps or ambiguities recorded — **L3**.
- Internal audit or independent review of the taxonomy against DORA Art. 17/18 classification requirements and SUP 15.3 notification triggers, specifically for AI-specific coverage — **L4**.
- Evidence from an actual historical AI-specific event showing how it was in fact classified, and whether the classification and notification (if applicable) were timely and correctly routed — **L5**.
- **Worked example — an emerging industry reporting category with no taxonomy yet to receive it, 9 September 2026 (OpenAI, "The AI policy window is open. We need to act.", §"Calling for industry standards to monitor frontier AI").** A frontier provider states: "As we shared last week, OpenAI is developing a framework for reporting consequential misalignment incidents and systematically monitoring frontier-model activity, including internal use." For this canvas the significance is not the framework, which was not published at the date of this entry, but the category: "consequential misalignment incident" is a failure class that no firm incident taxonomy, and neither DORA Art. 17/18 nor FCA SUP 15.3, currently names. A reviewer should expect the firm's taxonomy to be capable of receiving a newly articulated AI failure class without a structural change — and should treat the absence of any route for one as the finding, rather than waiting for an external definition to settle. **Status, stated:** a provider's statement of intent, not a published framework and not a regulatory expectation; it is evidence that the category is forming, not authority for its content — **L1**.

## 11. Independent Test
> Documentation review of the firm's incident taxonomy against the four named AI failure classes (mass confabulation, prompt-injection compromise, agentic misaction, silent bias event), checking for a distinct category or an explicit, adequate mapping onto an existing category, with severity mapping and a notification route (DORA Art. 19 report path; FCA SUP 15.3.1R) defined for each. This is supplemented by a tabletop walk-through of one class, selected by the reviewer, tracing a hypothetical event of that class through classification, severity mapping and notification-routing to identify where the taxonomy is silent or ambiguous. No published protocol exists for testing AI-specific incident-taxonomy coverage — stated plainly; the test is a bespoke documentation-and-walkthrough exercise, professional-judgement-led. Conducted entirely against governance documentation and a desk-based tabletop exercise; no production system access required. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (DORA and SUP 15.3 supply a credible, binding classification-and-notification architecture to test against, but no published methodology defines AI-specific incident-category adequacy, and the walk-through's coverage of only one class per exercise means residual classes are assessed by documentation review alone, not exercised).

## 12. Pass Indicators
- All four named AI-specific failure classes appear in the taxonomy either as distinct categories or with an explicit, reasoned mapping onto an existing category, in both cases with defined severity mapping.
- Each of the four classes has a defined notification route referencing DORA Art. 19 report stages and/or FCA SUP 15.3.1R, as applicable.
- The tabletop walk-through completes without identifying an ambiguity that would delay classification or notification for the exercised class.
- Severity mapping for AI-specific categories references the DORA Art. 18 classification criteria (or the firm's equivalent), not merely a generic "high/medium/low" scale untethered to those criteria.
- At least one historical AI-specific event evidences correct, timely classification under the taxonomy.

## 13. Fail Indicators
- One or more of the four named AI-specific failure classes has no category and no explicit mapping onto an existing category — the taxonomy is silent on it.
- Where a mapping exists, it is a poor structural fit (e.g. mass confabulation force-fitted into a "data quality" category with no severity or notification consequence appropriate to a customer-facing failure).
- The tabletop walk-through surfaces genuine ambiguity or a dead end — reviewers cannot agree how the simulated event would be classified or whether it would trigger DORA/SUP 15.3 notification.
- Severity mapping for AI-specific categories, where present, is not referenced to the DORA Art. 18 criteria or any equivalent structured basis.
- A historical AI-specific event is found to have gone unclassified or misclassified, with a corresponding delay to notification.

## 14. Reporting Language
**Pass:** "Documentation review and a tabletop walk-through confirm that the firm's incident taxonomy recognises all four AI-specific failure classes tested — mass confabulation, prompt-injection compromise, agentic misaction, silent bias event — with severity mapping referenced to the DORA Art. 18 criteria and a defined notification route (DORA Art. 19 / FCA SUP 15.3.1R). Conclusions rest on ★2 methodology — a bespoke documentation-and-walkthrough exercise with no published protocol — and should be read as professional assessment of taxonomy coverage, not of the firm's broader incident-management capability, which this IRQ does not test."
**Fail:** "Review found that [n] of the four AI-specific failure classes tested have no category, and no adequate mapping onto an existing category, in the firm's incident taxonomy. Events of this class have no defined severity mapping or notification route; the regulatory-notification clock (DORA Art. 19 / FCA SUP 15.3.1R) cannot reliably start on such an event under the current taxonomy. This is a material gap in classification coverage, distinct from and not remediated by the existence of incident management or notification processes generally."
**Partial:** "Mass confabulation and agentic misaction are recognised as distinct categories with defined severity mapping and notification routing; prompt-injection compromise is mapped onto an existing security category without AI-specific severity guidance, and silent bias event has no category or mapping at all. The assurance objective is not yet met for the latter two classes; remediation should add or adequately map the missing categories within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a classification gap delays response and notification rather
              than causing harm directly; severity is inherited from whatever
              the underlying AI-specific event turns out to be)
  Likelihood: 2 (plausible given incident taxonomies are typically reviewed
              against their own historical categories rather than against a
              deliberately AI-specific checklist; reduces materially once the
              four classes are explicitly tested and added)
  Detectability: 3 (a taxonomy gap is itself invisible until either a dedicated
              review is run or an actual AI-specific event exposes it by
              failing to classify)
  Recoverability: 1 (cheaply and quickly fixed once identified — adding a
              category with severity mapping and a notification route is a
              documentation and governance change, not a system rebuild)
  Novelty: 4 (very likely to be missed: AI-specific failure classes have no
              obvious analogue in a taxonomy built for infrastructure and fraud
              incidents, and three of the four classes — mass confabulation,
              silent bias, agentic misaction — produce no conventional error
              state at all)

Interpretation: acceptable residual risk once the four classes are explicitly
tested and any gaps closed; the low recoverability cost means there is little
reason not to remediate promptly once a gap is found — the material risk is in
never looking, given how well the taxonomy's own review process is likely to
miss the gap unaided.

If controls are absent or degraded:
  Severity: 3 (an AI-specific event with no classification path can continue
              unaddressed materially longer than a conventionally categorised
              incident, and a DORA/SUP 15.3 notification obligation may be
              breached through no concealment but structural taxonomy absence)
  Likelihood: 3 (foreseeable given incident taxonomies predate AI-specific
              failure classes almost everywhere they have not been
              deliberately updated)
  Detectability: 4 (silent by construction — the taxonomy gap and the event it
              fails to classify are both invisible until a dedicated review or
              an actual unclassified incident forces discovery)
  Recoverability: 2 (the taxonomy fix itself is cheap, but any notification
              breach or unaddressed harm accrued during the gap period is not
              retrospectively curable)
  Novelty: 4
Residual risk: Moderate-to-high while untested; low-cost to remediate once a
gap is identified, which argues for testing this IRQ routinely rather than
once.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | A classification gap delays response and notification rather than causing harm directly; severity is inherited from the underlying AI-specific event. |
| **Likelihood** | 3 | Probable given incident taxonomies are typically reviewed against their own historical categories, not a deliberately AI-specific checklist. |
| **Detectability** | 4 | Silent by construction — the gap is invisible until a dedicated review or an actual unclassified AI-specific event forces discovery. |
| **Recoverability** | 1 | Cheap and quick to fix once found — adding a category with severity mapping and a notification route is a documentation/governance change, not a system rebuild. |
| **Novelty** | 4 | AI-specific failure classes have no obvious analogue in a taxonomy built for infrastructure and fraud incidents; three of the four classes produce no conventional error state at all. |

## 17. Regulatory Basis
> [DORA, Regulation (EU) 2022/2554, Art. 17 — "ICT-related incident management process," in force 16 January 2023, applies from 17 January 2025] requires financial entities to define, establish and implement procedures to identify, track and categorise ICT-related incidents by priority, severity and criticality; this categorisation requirement presupposes that the event is first identified and logged as an incident, which is the specific gap this IRQ tests: a taxonomy with no AI-specific failure class makes that unlikely for failures that raise no conventional error state. [DORA, Art. 18] sets six classification criteria (clients/counterparts affected and reputational impact; duration/downtime; geographical spread; data losses across availability, authenticity, integrity and confidentiality; criticality of services affected; economic impact) with materiality thresholds set by the classification Regulatory Technical Standards supplementing Art. 18(3). [DORA, Art. 19] sets a three-report notification structure (initial, intermediate, final) to the competent authority for major ICT-related incidents. [FCA, SUP 15.3.1R, as at 31/07/2026] separately requires immediate notification on the firm becoming aware of a matter that could have a significant adverse impact on its reputation, could affect its ability to continue to provide adequate services to its customers and result in serious detriment to a customer, or could have serious financial consequences for the UK financial system or other firms — a "becomes aware" trigger that depends on the firm first recognising the event as an incident. No US or macroprudential regulatory anchor requiring AI-specific incident categorisation was identified in the verified source set; this gap is stated openly rather than an anchor being invented, and testing under this IRQ is therefore scoped to the DORA/SUP 15.3 UK/EU framework.

## 18. Research Basis
> No peer-reviewed literature specifically evaluating incident-taxonomy coverage of AI-specific failure classes in deployed financial-services systems was identified in the source registers; this control area is regulatory-instrument-led (DORA, SUP 15.3) rather than research-led, consistent with the Governance domain's wider evidentiary profile. The four named failure classes — mass confabulation, prompt-injection compromise, agentic misaction, silent bias event — are drawn from the failure-mode vocabulary used elsewhere in this IRQ battery (see linked IRQ-MOD, IRQ-SEC, IRQ-AGT and IRQ-CON canvases for the evidence base underlying each individual failure class); this IRQ tests only whether the incident classification scheme, as a governance artefact, recognises them — not the underlying technical evidence for their existence, which is established elsewhere in the battery. A silent bias event, specifically, shares its evidentiary root with the fairness/bias testing IRQs elsewhere in the battery; that linkage is carried at the claims-matrix level, not restated here.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-RES-005 (G.3: monitoring/alerting — produces the signal this IRQ's
    taxonomy must be able to classify)
  - IRQ-RES-006 (G.3: monitoring/alerting — as above, upstream signal source)
  - IRQ-GOV-008 (I.3: monitoring signals reaching accountable governance —
    presumes the event was already classified; this IRQ tests the
    classification scheme itself)
  - IRQ-GOV-011 (I.4: regulatory obligation mapping — supplies the correct
    notification route once an event is classified)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 — Digital Operational
    Resilience Act (DORA)." OJ L 333, 27.12.2022. In force 16 January 2023,
    applies from 17 January 2025. Arts. 17, 18, 19.
[2] Financial Conduct Authority. "SUP 15.3 — General Notification
    Requirements." FCA Handbook, as at 31/07/2026 (last updated 01/06/2026).
    SUP 15.3.1R, SUP 15.3.8G(2).
[3] OpenAI, 2026. "The AI policy window is open. We need to act." 9 September 2026.
    URL: https://openai.com/index/ai-policy-window/
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Incident taxonomies are reviewed against their own
  historical categories (outage, breach, fraud); AI-specific failure classes
  have no obvious analogue, and three of the four produce no conventional
  error state, so a taxonomy-completeness review will not surface the gap
  unaided.
✓ Test 2 (Plausible Harm): Grounded in DORA Art. 17's categorisation
  requirement and Art. 19's notification structure, and FCA SUP 15.3.1R's
  "becomes aware" trigger — all of which presuppose that the event is first
  identified and logged as an incident, which a taxonomy with no AI-specific
  failure class makes unlikely for failures that raise no conventional error
  state.
✓ Test 3 (Testable): Testable via documentation review of the taxonomy against
  four named failure classes plus a tabletop walk-through of one class. ★2
  methodology, honestly caveated — no published protocol exists.
✓ Test 4 (Decision-Relevant): Outcome determines whether the firm's DORA/SUP
  15.3 notification capability actually extends to AI-specific failure, and
  gates authorisation conditions accordingly.

Change Log:
- v1.0 (2026-07-31): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 10 — OpenAI's statement of 9 Sep 2026 that it "is developing a framework for reporting consequential misalignment incidents" added as a worked example of an AI failure class forming outside the classes this canvas names and outside DORA Art. 17/18 and FCA SUP 15.3, with its status as a statement of intent rather than a published framework or regulatory expectation stated. ★2 unchanged.
- v1.2.1 (2026-09-19): Fields 2, 4, 9, 17 and 21 — erratum: Test 2's statement that DORA Art. 17 and 19 and FCA SUP 15.3.1R presuppose that the event "can first be classified, which an absent AI-specific category defeats" is corrected to what they presuppose: that the event is first identified and logged as an incident, which a taxonomy with no AI-specific failure class makes unlikely for failures that raise no conventional error state. DORA classifies an incident by its impact, which does not require an AI-specific category. Business Activities Affected (Field 2), Failure Mode (Field 4), Expected Controls (Field 9) and Regulatory Basis (Field 17) restated the same presupposition and are corrected alike; the failure mode now runs on the event not being identified and logged as an incident, or being force-fitted into an ill-matching category, with the clock not starting, or starting late and on the wrong basis. No change to controls, test, ★2 or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

