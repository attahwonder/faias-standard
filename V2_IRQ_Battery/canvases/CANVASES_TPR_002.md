# CANVAS: IRQ-TPR-002

## 1. IRQ ID & Title
**IRQ-TPR-002: Contracts Failing to Secure Transparency, Audit, Notification and Exit Rights**

Register question: "Do contracts secure the transparency, notification, audit, licensing and exit rights the firm needs — including advance notice of model changes, deprecations, and output usage rights?"

## 2. Business Activities Affected
- **Any regulated AI-enabled service:** Without contractual audit and notification rights, the firm cannot fulfil its own regulatory obligations (evidencing control, responding to supervisory requests) regardless of how well the provider actually performs.
- **Business continuity planning:** Exit and portability rights determine whether the firm can substitute providers within impact-tolerance timeframes if a provider fails or is withdrawn (links RES-001, RES-004).
- **Content and output usage:** Licensing of model outputs (e.g. generated customer communications) determines whether the firm has clear rights to use, retain and defend that content.

## 3. AI Behaviour(s)
- Model/API is delivered under a commercial contract negotiated primarily on price, SLA uptime and data protection terms, with AI-specific clauses (change notification, audit access, model-version pinning, output rights) frequently absent or generic.
- Provider retains unilateral rights, under standard terms of service, to update, deprecate or modify the model without individualised notice to the firm.
- Firm's downstream processes are built assuming behavioural stability the contract does not actually guarantee.

## 4. Failure Mode
> The firm relies on a model or API provider under a contract that does not secure advance notification of model changes/deprecations, meaningful audit rights, or clear output usage and exit rights, leaving the firm structurally unable to detect, challenge or unwind provider-driven change before it affects customers or controls.

## 5. Potential Consequences
- **Institution:** Forced acceptance of provider-driven model changes with no re-approval window; inability to evidence control during a regulatory audit because contractual audit rights do not exist; costly, rushed provider substitution when exit rights are inadequate.
- **Customer:** Undetected behavioural change in customer-facing AI (tone, accuracy, refusal patterns) following an un-notified model update.
- **Regulator/market:** DORA Art. 30 mandatory contractual provisions non-compliance; EBA outsourcing guidelines contractual-content deficiency finding.

## 6. Failure Chain
```
Contract negotiated using standard commercial/procurement templates;
AI-specific clauses (change notice, audit, exit, output licence) not
included or negotiated away under commercial pressure
  ↓ (IRQ-TPR-001: diligence gap means AI-specific needs never articulated to legal)
Provider updates model/service under standard terms of service; no
individualised notice reaches the firm
  ↓ (IRQ-TPR-004: silent change goes undetected without contractual trigger)
Firm cannot invoke audit rights to investigate; cannot easily exit
because portability/exit terms are inadequate
  ↓
Behavioural change propagates into production; firm has no contractual
lever to compel remediation or secure timely substitution

Control Breakpoints:
  • IRQ-TPR-001: diligence identifies AI-specific contractual requirements
  • IRQ-TPR-002: contract negotiation secures notification/audit/exit rights
  • IRQ-TPR-004: technical canary testing complements contractual notice
```

## 7. Why a Domain Expert May Miss It
- Procurement/legal teams apply standard outsourcing contract templates (data protection, uptime SLA, liability caps) that predate AI-specific risks like model versioning and behavioural drift; "the model" is not a concept the template anticipates.
- Vendors' standard terms of service for API access are often accepted with minimal negotiation for lower-value or trial engagements, which later scale into material production dependencies without contract renegotiation.
- "Exit rights" are traditionally interpreted as data portability, not behavioural/model portability — a firm may secure its data but have no path to replicate model behaviour elsewhere.
- Output/content licensing (who owns a generated customer letter) is a novel IP question traditional contract review may not flag as material.

## 8. Assurance Objective
**AO-TPR-002:** Contracts with AI model/API providers shall secure advance notification of material model changes and deprecations, meaningful audit rights, and defined output usage and exit/portability rights, proportionate to the materiality of the dependent business activity.

## 9. Expected Controls (Traced)
- **Mandatory contractual provisions for ICT third-party arrangements** — [Regulation (EU) 2022/2554, DORA, Art. 30] — contracts for critical/important functions must include audit rights, service description, termination rights and exit strategy provisions.
- **Outsourcing contract minimum content standards** — [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, Title IV, Section 13 (Contractual phase, incl. 13.3 Access, information and audit rights; 13.4 Termination rights)] (verified 29 Jul 2026) — audit, access and termination rights proportionate to criticality.
- **Third-party contractual risk management** — [PRA SS2/21, November 2024 (15 November 2024, updating 29 March 2021)] — contractual terms should enable ongoing oversight and exit within business continuity requirements.
- **AI-specific change-notification clause** — Emerging Practice — firms are extending standard SLA notice-of-change clauses to explicitly cover model weight/version/safety-filter changes; no published FS-sector standard clause library identified.
- **Output/content usage rights review** — Emerging Practice, informed by general IP/licensing contract law — no AI-specific FS regulatory standard identified for output ownership terms.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor standard terms of service asserting "customer data is protected" — **L1**.
- Firm's contract negotiation checklist requiring AI-specific clauses — **L2**.
- Sampled executed contracts reviewed against the checklist, gaps logged — **L3**.
- Legal/procurement audit confirming contractual gap remediation across the critical-provider population — **L4**.
- Contract register showing notification/audit/exit clause status for all in-scope AI providers, refreshed at renewal — **L5**.

**Dated worked example, added at the September 2026 refresh — an upstream model supplier exercising a change-of-control cancellation right against a tool a firm may already be using.** On 28 August 2026 a model provider announced it would "wind down our contract providing OpenAI models to Cursor, with a proposed shutoff date of November 12, 2026", on the basis that "Our custom agreement with Cursor gives us a limited time window to cancel it after a change of control" following the tool's acquisition, and that "we cannot be confident that SpaceX will use our technology within our terms of service" [OpenAI, "Our decision on Cursor following its acquisition by SpaceX", 28 August 2026]. On notice, the provider says only that "we are giving the maximum notice provided by our contract" — the contractual notice period is **not stated** anywhere on the page; the interval between announcement and proposed shutoff is 76 days. Two tests follow for this IRQ's §11(a) and §11(d): whether the firm's own contract carries notice of a **sub-provider's** withdrawal as distinct from a model change, and whether exit and portability rights survive a change of control upstream of the firm's direct counterparty. **A material absence travels with the example:** the disclosure says nothing at all about customer data — retrieval, migration, portability or continuity for affected users — and the absence is part of what the example evidences.

## 11. Independent Test
> Sample executed contracts across materiality tiers; assess presence and enforceability of (a) advance notice of model change/deprecation, (b) audit rights, (c) output usage rights, (d) exit/portability provisions. Compare against DORA Art. 30 minimum contractual content and firm's own checklist. Desk-based contract review only; no live provider engagement. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (regulation-anchored checklist exists for DORA-in-scope contracts; AI-specific clause content is still emerging practice with professional judgement required for adequacy).

## 12. Pass Indicators
- All critical-tier contracts contain explicit model-change notification clauses with defined notice periods.
- Audit rights are contractually enforceable, not merely referenced as "available on request".
- Exit/portability provisions specify a timeframe consistent with the firm's business continuity/impact tolerance requirements.
- Output usage rights are explicitly addressed, not silent.

## 13. Fail Indicators
- Contracts rely on generic vendor terms of service with no AI-specific notification, audit or exit clauses.
- "Audit rights" clause exists on paper but has never been exercised or tested for practical enforceability.
- No defined exit timeframe; substitution planning assumes indefinite provider availability.
- Output ownership/usage rights are silent or ambiguous.

## 14. Reporting Language
**Pass:** "Sampled critical-tier contracts secure advance notification of model changes, enforceable audit rights, and exit provisions consistent with business continuity requirements. Conclusions rest on ★3 methodology, combining DORA-anchored minimum content checks with emerging-practice adequacy judgement."

**Fail:** "Sampled contracts rely on generic vendor terms of service; no contract in the sample contains an explicit model-change notification clause or enforceable audit right. This is a structural third-party risk gap: the firm has no contractual lever to detect or challenge provider-driven change."

**Partial:** "Notification and audit rights are present in contracts renewed under the current framework ([x]% of the critical-tier population) but absent in legacy contracts pre-dating the framework. Remediation plan should prioritise renegotiation ahead of next renewal for the highest-materiality legacy contracts."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (contractual gap itself does not harm customers directly; escalates only combined with an actual provider change — see TPR-004)
  Likelihood: 2 (plausible where legacy contracts pre-date AI-specific clause libraries)
  Detectability: 3 (surfaces at contract renewal review or when a change incident forces contract inspection)
  Recoverability: 2 (renegotiable at renewal; interim risk mitigated by technical canary testing)
  Novelty: 3 (contract/legal SMEs unfamiliar with AI-specific clause requirements)

If controls are absent or degraded:
  Severity: 3 (firm structurally unable to respond to a material provider-driven change affecting customers)
  Likelihood: 3 (probable given standard vendor terms of service rarely include AI-specific notice by default)
  Detectability: 3 (only detected reactively, via incident or supervisory request)
  Recoverability: 3 (contract renegotiation and provider substitution take months without pre-agreed exit terms)
  Novelty: 3 (requires combined AI and contract-law literacy)

Residual risk interpretation: Manageable with a disciplined contract renewal cycle enforcing AI-specific clauses; legacy-contract exposure is the primary residual concern.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Gap is structural/preventative; direct harm requires a compounding event (an actual undetected change) |
| **Likelihood** | 2 | Legacy contracts commonly lack AI-specific clauses; new contracts under updated checklist are lower risk |
| **Detectability** | 3 | Typically surfaces only at renewal review or post-incident |
| **Recoverability** | 2 | Renegotiable at renewal cycle; interim technical controls (TPR-004) partially compensate |
| **Novelty** | 3 | Requires combined legal and AI-domain literacy uncommon in standard contract review |

## 17. Regulatory Basis
> [Regulation (EU) 2022/2554, DORA, Art. 30] mandates specific contractual provisions for arrangements supporting critical or important functions, including audit rights, service levels, and termination/exit rights. [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, Title IV, Section 13 (Contractual phase)] set minimum contractual content expectations (verified 29 Jul 2026). [PRA SS2/21, November 2024 (15 November 2024, updating 29 March 2021)] expects contractual terms to enable ongoing oversight and exit consistent with business continuity planning.

## 18. Research Basis
> No peer-reviewed academic literature specifically addresses AI-provider contract clause design; this IRQ extends established outsourcing contract law and DORA's ICT contractual-content regime to the AI-specific case of model versioning and behavioural change. [UNVERIFIED — no UK Finance or ISDA publication specifically addressing AI-model versioning/behavioural-change contract clauses was located; the FINOS AI Governance Framework mitigation AIR-PREV-010 (AI Model Version Pinning) sets out versioning, release-note and advance-notice terms for supplier contracts] (verified 29 Jul 2026; AIR-PREV-010 read 7 Oct 2026).
>
> **[FAIAS Incident Register, row 87, "Windsurf Claude capacity cut", 2025]** — the customer's own statement records that "[w]ith less than a week of notice, Anthropic informed us they were cutting off nearly all of our first-party capacity to the Claude 3.x models", and that capacity from other inference providers was "not enough today, given the length of notice, to support all of the existing demand". It is one party's account: the contract terms and the provider's reasons are not in the source, and whether the notice breached any term is not known.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-TPR-001 (F.1 Due Diligence: diligence findings inform contractual requirements)
  - IRQ-TPR-004 (F.2 Model Change Management: contractual notice complements technical canary detection)
  - IRQ-GOV-011 (I.4 Documentation, Records & Regulatory: regulatory obligation mapping includes contractual compliance)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 30.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] European Banking Authority, 2019. "Guidelines on outsourcing arrangements." EBA/GL/2019/02.
    URL: https://www.eba.europa.eu/sites/default/files/documents/10180/2551996/38c80601-f5d7-4855-8ba3-702423665479/EBA%20revised%20Guidelines%20on%20outsourcing%20arrangements.pdf
    Accessed: 2026-07-29 (source confirmed live and current as at this date; URL changed to the Final Report PDF, read 8 Oct 2026) (verified 29 Jul 2026).

[3] Prudential Regulation Authority, 2024. "SS2/21 — Outsourcing and third party risk management."
    Published: November 2024 (15 November 2024, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/outsourcing-and-third-party-risk-management-ss
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.1 (Third Party domain, Due Diligence, Contracts & Licensing)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Contract/legal SMEs apply standard outsourcing templates that do not anticipate model-version behavioural change.
✓ Test 2 (Plausible Harm): Grounded in DORA Art. 30 mandatory contractual content regime; absence directly disables detection and remediation.
✓ Test 3 (Testable): Answerable via sampled contract review against a defined checklist.
✓ Test 4 (Decision-Relevant): Outcome gates contract renewal/negotiation priorities and provider risk acceptance.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Expected Evidence — dated worked example added (an upstream model supplier exercising a change-of-control cancellation right, 28 Aug 2026: "the maximum notice provided by our contract", 76 days, and no statement on customer data). IRQ-TPR-009 not carried. ★3 / P3 unchanged.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS2/21 gives its current version, November 2024 (15 November 2024, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS2/21 cited as its November 2024 version (15 November 2024, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 20 References — the URL of EBA/GL/2019/02 points to the Final Report PDF, in place of a page that now shows the EBA third-party risk management guidelines; the note "source confirmed live and current as at this date" says that it covers the earlier URL. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 87, Windsurf statement on a provider's withdrawal of model capacity, one party's account). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — the tag on sector-body publications now names the FINOS AI Governance Framework mitigation AIR-PREV-010 (AI Model Version Pinning) as setting out versioning, release-note and advance-notice terms for supplier contracts; the search statement now names UK Finance and ISDA only, and the words "or equivalent sector body" are removed. No change to the ★ rating or the risk profile.
```

---
---

