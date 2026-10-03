# CANVAS: IRQ-GOV-002

## 1. IRQ ID & Title
**IRQ-GOV-002: Incomplete AI Inventory Concealing Shadow, Embedded and Agentic AI Use**

Register question: "Is the AI inventory demonstrably complete — capturing shadow AI, embedded vendor AI, spreadsheets-plus-API usage and agentic workflows — with a mechanism that finds unrecorded use?"

## 2. Business Activities Affected
- **Any business process using an unrecorded AI capability:** if a team wires a spreadsheet macro to a public LLM API, or a vendor tool ships a GenAI feature switched on by default, that use sits entirely outside governance, tiering, approval and testing.
- **Customer-facing and material decisioning processes specifically:** the highest-risk case is shadow or embedded AI operating in a customer-facing or regulatory-material process without ever having passed through IRQ-GOV-003/-004 approval and tiering.
- **Third-party risk management:** AI embedded inside procured platforms (CRM, HR, surveillance, fraud tooling) is a distinct inventory blind spot from directly built or procured AI.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns whether the firm knows the AI system exists at all, prior to any assessment of its behaviour.
- Where present, shadow/embedded/agentic AI performs the same classes of behaviour (generation, retrieval, tool use, delegation) as governed systems, but entirely outside any monitoring or control scope.

## 4. Failure Mode
> An AI system is in live use within the firm — as shadow IT, as a feature embedded inside procured software, as an informal spreadsheet-plus-API workflow, or as an emergent agentic capability — without appearing in the firm's AI inventory, so none of the firm's governance, approval, tiering or monitoring controls ever engage with it.

## 5. Potential Consequences
- **Customer:** Decisions or communications influenced by an ungoverned AI system carry none of the assurance (bias testing, hallucination controls, human oversight) applied to inventoried systems.
- **Institution:** Complete governance frameworks (tiering, approval, monitoring) are undermined by an unknown population outside their scope; regulatory reporting on AI use (e.g., EU AI Act registers, supervisory returns) is materially incomplete.
- **Regulator/market:** Discovery of unrecorded AI use during a supervisory review or incident investigation signals a governance framework that does not actually cover the firm's real AI footprint, inviting broader scrutiny of the entire assurance programme.

## 6. Failure Chain
```
Business unit or individual adopts an AI capability outside procurement/IT governance
(public LLM API via spreadsheet macro, vendor feature switched on by default, informal
agentic automation)
  ↓ (IRQ-GOV-002 — THIS IRQ: no discovery mechanism finds it)
System is never entered in the AI inventory
  ↓ (IRQ-GOV-004: never tiered, so no proportionate control depth is ever set)
System is never approved, never subjected to IRQ battery testing, never monitored
  ↓ (IRQ-GOV-003: no conditions of use exist to enforce)
System operates against real customer data or decisions, ungoverned
  ↓ (IRQ-SEC-008: unsanctioned tool exfiltration risk compounds the exposure)
Failure occurs (bias, hallucination, data leak) with no controls to catch it
  ↓
Harm surfaces via complaint, incident or supervisory discovery →
firm cannot demonstrate it knew the system existed → governance credibility damage

Control Breakpoints:
  • IRQ-GOV-002: active discovery mechanism (not self-declaration) finds unrecorded AI
  • IRQ-GOV-004: tiering applies proportionate control once discovered
  • IRQ-GOV-003: conditions of use enforced once approved
  • IRQ-SEC-008: technical controls on unsanctioned tool/data egress as a backstop
```

## 7. Why a Domain Expert May Miss It
- Traditional model inventories are built from a known population (models submitted through model risk approval); the concept of actively hunting for *unknown* AI use is foreign to a process designed around self-declaration.
- "Embedded AI" is easy to miss because it does not look like an AI project — it is a feature toggle inside a CRM or HR platform that a vendor account manager enabled without a formal change request.
- Spreadsheet-plus-API usage (a business analyst calling an LLM API from an Excel add-in) does not pass through any of the firm's standard software procurement or IT asset management gates, so IT asset registers do not catch it either.
- Agentic workflows can emerge incrementally (a chatbot given an email-sending plugin, then a calendar plugin, then a payment plugin) without any single change event triggering inventory review.

## 8. Assurance Objective
**AO-GOV-002:** The firm shall maintain an AI inventory that is verified complete through active discovery — including shadow AI, embedded vendor AI, informal spreadsheet-plus-API use, and agentic workflows — not solely through self-declaration.

## 9. Expected Controls (Traced)
- **Active discovery mechanism (network/API egress monitoring, procurement/vendor questionnaire screening, periodic attestation with audit sampling)** — [ISO/IEC 42001:2023, clause 4.1 (understanding the organisation) and clause 8 (operational planning and control)] — AI management system scope must be actively determined, not assumed.
- **Embedded vendor AI capture via third-party risk management questionnaires that specifically ask about AI/ML features** — [linked IRQ-TPR-003; MAS Information Paper ID 18/24, Dec 2024, thematic good practice on AI inventory scope including vendor-embedded AI] — extends TPRM screening to specifically probe for embedded AI capability, not just AI-branded procurement.
- **API/network egress monitoring for calls to known GenAI provider endpoints** — [NIST AI 600-1 (GenAI Profile), Jul 2024, action items on inventory and asset management] — technical detection of unsanctioned AI use as a complement to self-declaration.
- **Periodic attestation with independent audit sampling (spot-checks against discovery evidence, not attestation alone)** — [PRA SS1/23, May 2023, model identification principle, extended to a firm-wide inventory-completeness control] — Emerging Practice: applying model-inventory completeness testing to the broader "any AI use" population is not yet standard MRM practice but follows directly from SS1/23's identification principle.
- **MAS AIRG consultation proposed inventory requirement** — [MAS, "Consultation Paper: Proposed Guidelines on Artificial Intelligence Risk Management (AIRG)," Nov 2025] — proposes AI inventory as a foundational cross-sector expectation; cited as the closest regulatory analogue to this control, currently at consultation stage; consultation closed Jan 2026 and final Guidelines text was not confirmed published as of 29 Jul 2026 — no formal MAS document reference number (e.g. "P0xx-2025") is published for this consultation paper [UNVERIFIED — final Guidelines text/reference number not yet issued] (verified 29 Jul 2026).

## 10. Expected Evidence (Tagged L1–L5)
- Self-declared AI inventory document — **L1** (assertion of completeness only, unless independently tested).
- Inventory governance policy defining what must be captured (shadow, embedded, agentic, spreadsheet-plus-API) and the discovery mechanism used — **L2**.
- Configuration/design evidence of an active discovery mechanism (API egress monitoring rules, vendor questionnaire template with AI-specific questions) — **L3**.
- Internal audit report testing inventory completeness by independent sampling (e.g., procurement records cross-checked against inventory; network egress logs cross-checked against inventory) — **L4**.
- Record of at least one instance where the discovery mechanism found an unrecorded AI system, and the remediation taken — **L5** (demonstrates the mechanism functions, not merely exists).
- Third-party risk management questionnaire responses showing embedded AI capability was identified and inventoried for a sample of vendor relationships — **L3**.

## 11. Independent Test
> Select a sample of business units and a sample of vendor relationships (weighted to those with plausible AI exposure — customer service, HR, fraud, marketing). Independently attempt to identify AI use through three routes not dependent on self-declaration: (1) review of API/network egress logs for calls to known GenAI provider endpoints, (2) review of vendor contracts and product documentation for embedded AI/ML features, (3) structured interviews with a sample of front-line staff about tools they use day-to-day. Reconcile findings against the declared AI inventory; any AI use found through the independent routes but absent from the inventory is a discovery-mechanism failure. Methodology follows standard IT asset management and internal audit reconciliation practice (independent-source cross-checking), applied here to the AI-specific population with no AI-specific benchmark or established sampling frame for "shadow AI" prevalence. Conducted against logs, contracts and interviews only; no production system access required. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (research evidence that shadow/embedded AI is a real and growing exposure exists, but the test design — which routes to sample, how large a sample constitutes reasonable assurance of "completeness" — is bespoke to the firm and relies heavily on reviewer professional judgement; no standard methodology or benchmark for inventory-completeness testing was identified).

## 12. Pass Indicators
- Independent discovery routes find zero AI uses absent from the declared inventory across the sampled population.
- Vendor questionnaires for the sampled relationships specifically probe for embedded AI/ML features and responses are corroborated against product documentation.
- At least one documented instance exists of the discovery mechanism successfully finding and remediating a previously unrecorded AI use (demonstrates it is live, not theoretical).
- Front-line staff interviews corroborate that tools they describe using are all present in the inventory.
- Discovery mechanism operates on a defined recurring cadence (not a one-off exercise).

## 13. Fail Indicators
- Independent discovery routes surface AI use (shadow, embedded or agentic) not present in the declared inventory.
- Inventory relies solely on self-declaration/attestation with no independent verification mechanism (L1 evidence only).
- Vendor questionnaires ask generic security questions but do not specifically probe for embedded AI/ML capability.
- No evidence the discovery mechanism has ever actually found anything — suggests it is a paper control rather than an operating one.
- Agentic workflows built by combining existing approved tools (chatbot + plugins added incrementally) are not captured because no single change event triggered inventory review.

## 14. Reporting Language
**Pass:** "Independent discovery testing across [n] business units and [n] vendor relationships found no AI use absent from the declared inventory. The discovery mechanism has a demonstrated track record of finding and remediating unrecorded use, and vendor questionnaires specifically probe for embedded AI/ML capability. Conclusions rest on ★2 methodology — a bespoke, professional-judgement-led test with no established benchmark for inventory-completeness — and should be read as a reasonable but not exhaustive assurance of completeness."
**Fail:** "Independent testing identified [n] AI systems in live use — including [describe: an embedded CRM feature / a spreadsheet-plus-API workflow / an agentic plugin chain] — that were absent from the declared AI inventory and had therefore never been tiered, approved or subjected to any FAIAS control. The inventory cannot currently be relied upon as complete; governance conclusions dependent on inventory completeness (tiering, approval coverage) should be treated as provisional until discovery gaps are remediated."
**Partial:** "Directly procured and internally built AI is comprehensively inventoried, but embedded vendor AI is inconsistently captured — [x]% of sampled vendor relationships with plausible AI exposure had no AI-specific questionnaire response. The assurance objective is not yet met for that subset; remediation should extend embedded-AI screening across the vendor population within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (undermines governance coverage rather than directly causing harm; severity is inherited from whatever the undiscovered system does)
  Likelihood: 2 (plausible for embedded/shadow AI specifically given how easily it enters; unlikely for directly governed systems with mature procurement gates)
  Detectability: 2 (found via periodic active discovery within a review cycle; not visible through routine business monitoring)
  Recoverability: 1 (once found, remediation is adding the system to the inventory and applying proportionate tiering — low cost)
  Novelty: 3 (domain expert applying a traditional model-inventory mental model would very likely miss embedded and spreadsheet-plus-API AI specifically)

Interpretation: acceptable residual risk if the discovery mechanism is genuinely active and
tested; the material concern is that an untested, self-declaration-only inventory gives false
comfort — this IRQ's value lies specifically in verifying the mechanism works, not the document.

If controls are absent or degraded:
  Severity: 3 (an unknown population of AI systems operates entirely outside every other
              governance control in this file, with severity inherited from the worst case
              among them)
  Likelihood: 3 (foreseeable and empirically documented that shadow/embedded AI proliferates
              faster than formal procurement processes)
  Detectability: 4 (by definition undiscovered until an incident or external review surfaces it)
  Recoverability: 2 (once found, remediation is straightforward, but the exposure window before
              discovery may have allowed material harm)
  Novelty: 3
Residual risk: High while the discovery mechanism is unverified; low-cost to remediate once found.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Does not itself cause harm; severity is inherited from whatever the undiscovered system does, most of which sits below the highest tiers by volume. |
| **Likelihood** | 3 | Probable given documented ease of shadow/embedded AI adoption outpacing formal governance, particularly via vendor-embedded features and spreadsheet-plus-API use. |
| **Detectability** | 4 | By definition undiscovered until an active discovery mechanism, incident or external review surfaces it; self-declaration alone has a structural blind spot. |
| **Recoverability** | 1 | Cheap and fast to remediate once found — add to inventory, apply tiering — but cannot undo harm that occurred during the undetected window. |
| **Novelty** | 3 | AI-specific: traditional IT asset management and model-inventory processes are not designed to hunt for AI capability hidden inside non-AI-branded software or informal workflows. |

## 17. Regulatory Basis
> [PRA, SS1/23, May 2023, Principle 1 — Model Identification] establishes that firms must have a complete, accurate model inventory; this IRQ extends the identification principle to the AI-specific discovery challenge. [MAS, Information Paper ID 18/24, "Artificial Intelligence Model Risk Management — Observations from a Thematic Review," Dec 2024] documents AI inventory completeness, including third-party/embedded AI, as an observed good practice gap across surveyed institutions. [MAS, "Consultation Paper: Proposed Guidelines on Artificial Intelligence Risk Management (AIRG)," Nov 2025] proposes AI inventory as a foundational cross-sector requirement; consultation closed Jan 2026, final Guidelines not yet confirmed published as of 29 Jul 2026, and MAS has not assigned a distinct reference number to this consultation paper [UNVERIFIED — final Guidelines text/reference number not yet issued] (verified 29 Jul 2026). [ISO/IEC 42001:2023, clause 4.1] requires firms to determine the scope of their AI management system, implying active scoping rather than passive self-declaration.

## 18. Research Basis
> No peer-reviewed academic literature specifically quantifying shadow/embedded AI prevalence in financial services was identified in the source registers; this is consistent with governance-domain evidence being audit/regulatory-practice-led rather than research-led. [MAS Information Paper ID 18/24, Dec 2024] is treated as the closest available empirical evidence base, being a supervisor-conducted thematic review documenting inventory gaps across real institutions rather than a single-firm assertion.
>
> [Information and Privacy Commissioner of Ontario, 2025, letter to a health information custodian, "Reported Breach HR24-00691", 27 October 2025] supplies a supervisory record of an unapproved AI tool operating undetected inside an institution's own meeting. An artificial-intelligence transcription tool joined and recorded a clinical meeting at which the personal health information of seven patients was discussed, and the letter records the hospital's own report that "[t]he Tool has not been approved for use at the hospital." The tool was admitted through a departed physician's personal calendar — the physician had left in June 2023, had not been removed from the meeting invitation, and installed the tool on a personal device in September 2024 — so that it "was able to join the September 23, 2024 hepatology rounds meeting via accessing the link to it in the physician's personal email calendar and record the meeting without notice". Its presence was discovered only afterwards, "when a meeting summary and access to a transcript of the recording was automatically emailed to participants after the meeting"; no inventory or discovery mechanism found it while it was operating. The recommendations in the letter include technically enforcing a participant lobby for virtual meetings in which personal health information is discussed, "requiring the host to manually approve each participant", so as to "decrease the possibility of an unauthorized AI tool automatically joining the meeting as a participant". Stated precisely: the custodian is a hospital, not a regulated financial-services firm, and is anonymised in the published letter; the account holder was a former agent of the institution rather than a current one. The transferable element is that an unrecorded tool operated inside the institution's own meeting and was found by accident, and that the measure the supervisor recommended for it, a host-approved meeting lobby, is preventive — it reduces the possibility of such a tool joining — while the step the letter records for finding such a tool in a meeting is manual and the hospital's own: its policy, revised in June 2025, asks staff to "review meeting participant lists for any inclusion of unapproved AI tools or automated agents, and remove them from meetings".
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-001 (I.1: ownership — an undiscovered system also has no owner assigned)
  - IRQ-GOV-004 (I.2: tiering — cannot occur until the system is inventoried)
  - IRQ-TPR-003 (F.1: embedded vendor AI due diligence — shares the vendor-screening control)
  - IRQ-SEC-008 (E.2/technical: unsanctioned tool data egress — technical backstop control)
  - IRQ-AGT-011 (C.7: complete action traces — relevant once an agentic system is discovered)
```

## 20. References
```
[1] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[2] Monetary Authority of Singapore, 2024. "Information Paper: Artificial Intelligence Model
    Risk Management — Observations from a Thematic Review." ID 18/24. December 2024.
[3] Monetary Authority of Singapore, 2025. "Consultation Paper: Proposed Guidelines on
    Artificial Intelligence Risk Management (AIRG)." November 2025. Consultation paper (URL: mas.gov.sg/publications/consultations/2025/consultation-paper-on-guidelines-on-artificial-intelligence-risk-management); MAS has not published a distinct reference number for this paper; consultation closed Jan 2026, final Guidelines not yet issued as of 29 Jul 2026 (verified 29 Jul 2026).
[4] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management system."
    Clauses 4.1, 8.
[5] NIST, 2024. "NIST AI 600-1 — Artificial Intelligence Risk Management Framework:
    Generative Artificial Intelligence Profile." July 2024.
[6] Information and Privacy Commissioner of Ontario, 2025. Letter to a health
    information custodian, "Reported Breach HR24-00691." 27 October 2025.
    (URL: https://www.ipc.on.ca/en/media/5995/download)
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.1 (Governance domain, Inventory & Ownership)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional model-inventory processes are built around a known,
  self-declared population; SMEs do not naturally think to hunt for AI hidden inside procured
  non-AI-branded software or informal spreadsheet-plus-API workflows.
✓ Test 2 (Plausible Harm): Grounded in MAS's own supervisor-conducted thematic review (ID 18/24)
  documenting this exact gap across real institutions; an undiscovered system carries none of
  the assurance applied to inventoried systems.
✓ Test 3 (Testable): Testable via independent discovery routes (egress logs, vendor contract
  review, staff interviews) reconciled against the declared inventory; no production access
  required. ★2 methodology, honestly caveated (no benchmark).
✓ Test 4 (Decision-Relevant): Outcome determines whether the firm's entire tiering, approval
  and monitoring framework can be trusted to cover its real AI footprint.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.1 (2026-09-19): Field 18 — the Ontario Information and Privacy Commissioner's breach letter of 27 October 2025 added as a supervisory record of an unapproved AI transcription tool operating inside an institution's own meeting and being found only by accident. Field 20 — entry [6] added for the letter. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
```

---
---

