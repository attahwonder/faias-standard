# CANVAS: IRQ-TPR-003

## 1. IRQ ID & Title
**IRQ-TPR-003: Undiscovered AI Embedded Inside Procured Software**

Register question: "Where vendors embed AI inside procured software (CRM, surveillance, HR tools), are those capabilities identified, risk-assessed and brought under the same governance?"

## 2. Business Activities Affected
- **Customer relationship management and sales:** CRM platforms increasingly embed generative "assist" and lead-scoring features by default, silently making AI-driven decisions inside a tool the firm procured as conventional software.
- **Employee surveillance and productivity tools:** AI-driven monitoring/analytics embedded in HR or communications-surveillance software can produce conduct or performance inferences affecting staff without HR or compliance sign-off.
- **AML/fraud detection tooling:** Vendor case-management platforms may embed AI-driven risk scoring updated by the vendor independently of the firm's own model governance.

## 3. AI Behaviour(s)
- AI capability is switched on by default or via a minor feature update within software procured and approved as non-AI or lower-risk software.
- Vendor updates the embedded AI capability under standard software update terms, without the firm's AI governance function being notified.
- Business users adopt embedded AI features because they are presented as ordinary product functionality, not a new AI deployment requiring approval.

## 4. Failure Mode
> AI capability embedded inside procured software operates in production, influencing customer, employee or risk decisions, without having been identified, risk-assessed or brought under the firm's AI governance framework — because it was never recognised as "AI" at intake or through subsequent vendor updates.

## 5. Potential Consequences
- **Institution:** AI inventory (IRQ-GOV-002) is materially incomplete; governance, model risk and Consumer Duty obligations are not discharged for capabilities the firm does not know exist.
- **Employee/customer:** Unassessed AI-driven inferences (surveillance flags, CRM-driven customer segmentation) affect people without any documented risk assessment or right of challenge.
- **Regulator/market:** Supervisory finding of AI governance scope incompleteness; reputational exposure if an embedded AI feature is later found to have driven a harmful outcome the firm cannot explain.

## 6. Failure Chain
```
Software procured under standard IT/vendor management process;
AI capability not disclosed prominently or missed at intake
  ↓ (IRQ-GOV-002: inventory discovery mechanism does not proactively scan for embedded AI)
Vendor enables or updates an embedded AI feature (e.g. "smart" lead
scoring, sentiment flagging) via routine product update
  ↓ (IRQ-TPR-003 — THIS IRQ: capability never risk-assessed or governed)
Business users rely on the feature's outputs as ordinary product
functionality
  ↓
Decision or inference influenced by unassessed AI affects a customer
or employee; no governance record exists to explain or defend it
  ↓
Incident or audit finding surfaces the gap; retrospective governance
scramble; potential regulatory or employment-law exposure

Control Breakpoints:
  • IRQ-GOV-002: active discovery mechanism for embedded/shadow AI
  • IRQ-TPR-003: vendor-embedded AI risk assessment and governance intake
  • IRQ-GOV-001: accountable ownership extended to embedded capabilities
```

## 7. Why a Domain Expert May Miss It
- Procurement and IT teams categorise software by primary function (CRM, HR system) not by whether it contains AI; an "AI capability" field rarely exists in vendor management questionnaires for non-AI-labelled products.
- Vendors market embedded AI as an incremental feature enhancement rather than a new capability requiring re-approval, so it lands via a routine software update cycle that bypasses AI governance entirely.
- Business users experience the feature as "the software got smarter," not as "we deployed a new AI system," so they have no reason to raise it to governance.
- AI governance functions often scope their inventory-building exercise around directly procured AI/ML tools, missing capability embedded inside adjacent categories (surveillance, HR, sales enablement).

## 8. Assurance Objective
**AO-TPR-003:** The firm shall maintain an active discovery mechanism capable of identifying AI capabilities embedded within procured software, and shall bring every identified capability under the same risk assessment and governance framework applied to directly procured AI systems.

## 9. Expected Controls (Traced)
- **AI inventory completeness verification** — [linked IRQ-GOV-002] — active discovery mechanisms (vendor re-questionnaires, technical scanning, feature audits) rather than self-declaration alone.
- **Embedded vendor AI governance** — [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, scope extension to sub-outsourced/embedded functions] [UNVERIFIED — the Guidelines govern outsourced *functions* generally and do not address embedded/feature-level AI specifically; this is FAIAS's interpretive extension, not a stated EBA position] (verified 29 Jul 2026) — outsourcing governance extends to material functions delivered via embedded capability, not only headline services.
- **Vendor change notification for feature updates** — [linked IRQ-TPR-002] — contractual notification rights should cover material feature additions, not only core service changes.
- **Periodic vendor re-questionnaire on AI content** — Emerging Practice — no single published FS standard mandates recurring AI-capability re-disclosure from software vendors; firms are adapting existing third-party risk re-assessment cycles.
- **Governance owner accountability extension** — [linked IRQ-GOV-001] — accountable owner for a procured software category is also accountable for identifying and governing embedded AI within it.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor assertion "no AI functionality" in original procurement questionnaire — **L1**.
- Updated vendor management policy requiring AI-capability disclosure at intake and at each material update — **L2**.
- Sample audit of a cross-section of procured software (CRM, HR, surveillance, case management) for undisclosed embedded AI features, using technical inspection and vendor re-questionnaire — **L3**.
- Second-line/internal audit report confirming AI inventory completeness testing was performed and gaps remediated — **L4**.
- AI inventory register showing embedded-AI entries added over the last 12 months as a result of active discovery (not vendor self-report alone) — **L5**.

## 11. Independent Test
> Select a sample of procured software across categories not originally flagged as "AI" (CRM, HR, surveillance/monitoring, case management). Technically inspect current feature sets and re-issue AI-capability questionnaires to vendors; compare findings against the firm's AI inventory. Record the number and materiality of undisclosed embedded AI capabilities found. Test conducted via documentation review and vendor engagement; no live production data manipulated. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (research supports the "shadow/embedded AI" phenomenon generally; no standardised, benchmarked discovery methodology exists for FS — this is largely bespoke, professional-judgement-driven investigation).

## 12. Pass Indicators
- Sample technical inspection finds no material undisclosed embedded AI capability in procured software.
- Vendor management policy requires AI-capability disclosure at intake and at each material feature update, evidenced in recent procurement files.
- AI inventory shows entries added specifically as a result of active discovery activity, not solely vendor self-declaration.

## 13. Fail Indicators
- Sample inspection finds embedded AI features (e.g. AI-driven scoring, sentiment analysis) operating in production software with no corresponding inventory entry or risk assessment.
- Vendor management questionnaires have no AI-capability field; disclosure relies entirely on unprompted vendor honesty.
- No mechanism exists to catch AI capability added via routine software update after initial procurement.

## 14. Reporting Language
**Pass:** "Sample technical inspection of procured software across CRM, HR and surveillance categories found no material undisclosed embedded AI capability; the firm's discovery mechanism (vendor re-questionnaire plus technical inspection) is active and evidenced. Conclusions rest on ★2 methodology — a bespoke, professional-judgement-driven test with no standardised FS benchmark — and should be read as a point-in-time finding, not a guarantee of future completeness."

**Fail:** "Sample inspection identified [x] instances of embedded AI functionality operating in production procured software with no corresponding AI inventory entry or risk assessment. The firm's AI governance scope is materially incomplete; obligations under Consumer Duty, model risk and outsourcing frameworks cannot be discharged for capabilities the firm has not identified."

**Partial:** "Discovery activity has closed known gaps in CRM and case-management categories but has not yet extended to HR and surveillance software procured before the current vendor management policy. Remediation plan should prioritise categories with the highest employee or customer impact potential."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (typically bounded to a specific business process; escalates if embedded AI drives a materially unfair outcome)
  Likelihood: 2 (plausible given the pace of vendor feature rollout versus governance re-assessment cadence)
  Detectability: 4 (silent by design — vendor feature updates rarely trigger any internal alert)
  Recoverability: 2 (once discovered, remediable via risk assessment and, if needed, feature disablement)
  Novelty: 4 (domain expert very likely to miss; embedded AI is specifically designed to feel like ordinary software enhancement)

If controls are absent or degraded:
  Severity: 3 (multiple employees or customers affected by an ungoverned AI-driven inference with no assessment or challenge route)
  Likelihood: 3 (probable given default-on vendor AI feature rollout trends)
  Detectability: 4 (discovered only via incident, complaint, or rare deep audit)
  Recoverability: 3 (retrospective governance, potential feature disablement negotiation with vendor, weeks-to-months)
  Novelty: 4 (fully outside traditional vendor management scope)

Residual risk interpretation: Detectability and novelty are the dominant concerns; this IRQ warrants proactive, recurring discovery activity rather than one-off inventory completion.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Typically process-bounded; severity rises only if the embedded AI materially affects a customer or employee outcome |
| **Likelihood** | 2 | Vendor default-on feature rollout makes this plausible without active discovery, though not universal |
| **Detectability** | 4 | Silent by construction — no natural trigger alerts governance to a vendor feature update |
| **Recoverability** | 2 | Once identified, governance and remediation are achievable within a normal risk-assessment cycle |
| **Novelty** | 4 | Domain and vendor-management experts are structurally unlikely to recognise embedded AI as a governance trigger |

## 17. Regulatory Basis
> [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02] extend governance obligations to material outsourced functions, arguably including embedded capabilities within procured software [UNVERIFIED — no EBA text confirmed extending outsourcing governance explicitly to feature-level embedded AI; this remains FAIAS's interpretive extension] (verified 29 Jul 2026). No FS regulator has published AI-specific guidance mandating discovery of embedded vendor AI at feature level; this IRQ is grounded in the general AI governance expectation (FCA AI Update, April 2024; PRA/BoE response to DSIT AI principles, April 2024) that firms maintain a complete inventory of AI use, however delivered.

## 18. Research Basis
> No peer-reviewed research specifically addresses "embedded/shadow AI in procured software" in FS; the phenomenon is documented in general enterprise AI governance commentary [UNVERIFIED — no single citable peer-reviewed or regulator source specifically on 'embedded/shadow AI in procured FS software' was located; commentary exists at vendor/analyst level (e.g. Gartner, industry blogs) but not as an academically citable source] (verified 29 Jul 2026). This IRQ is grounded in the general shadow-AI/AI-inventory-completeness problem recognised across governance frameworks (NIST AI RMF MAP function; ISO/IEC 42001 inventory requirement) rather than a single empirical study.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-GOV-002 (I.1 Inventory & Ownership: active discovery of shadow/embedded AI)
  - IRQ-GOV-001 (I.1 Inventory & Ownership: accountable owner extended to embedded capabilities)
  - IRQ-TPR-002 (F.1 Contracts & Licensing: notification rights should cover feature updates)
```

## 20. References
```
[1] European Banking Authority, 2019. "Guidelines on outsourcing arrangements." EBA/GL/2019/02.
    URL: https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-outsourcing-arrangements
    Accessed: 2026-07-29 (source confirmed live and current as at this date) (verified 29 Jul 2026).

[2] Financial Conduct Authority, 2024. "AI Update."
    Published: April 2024
    URL: https://www.fca.org.uk/publications/corporate-documents/artificial-intelligence-ai-update-further-governments-response-ai-white-paper

[3] Bank of England / PRA, 2024. "Response to DSIT AI regulation principles."
    Published: April 2024
    URL: https://www.bankofengland.co.uk/prudential-regulation/letter/2024/artificial-intelligence-and-machine-learning-letter
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.1 (Third Party domain, Due Diligence, Contracts & Licensing)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Vendor management SMEs categorise by product function, not AI content; embedded AI arrives via routine update.
✓ Test 2 (Plausible Harm): Grounded in the AI inventory completeness expectation across FS AI governance guidance.
✓ Test 3 (Testable): Answerable via sampled technical inspection plus vendor re-questionnaire.
✓ Test 4 (Decision-Relevant): Outcome determines whether the AI governance perimeter is trustworthy.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

