# CANVAS: IRQ-TPR-001

## 1. IRQ ID & Title
**IRQ-TPR-001: Disproportionate or Absent Foundation Model / API Provider Due Diligence**

Register question: "Was due diligence on the foundation model or API provider proportionate to materiality, covering safety evaluations, security posture, and known model weaknesses?"

## 2. Business Activities Affected
- **Any AI-enabled customer or regulatory process built on a third-party model or API:** credit decisioning, claims triage, customer communications and AML screening all inherit the safety, security and weakness profile of the underlying provider without independent re-verification.
- **Model risk sign-off:** Model risk management approval (PRA SS1/23-aligned) presumes provider due diligence has already characterised the model's known failure modes; without it, approval rests on an evidence gap the firm cannot see.
- **Outsourcing/CTP register maintenance:** DORA and EBA outsourcing obligations require materiality-based due diligence as a precondition of onboarding, not an afterthought.

## 3. AI Behaviour(s)
- Firm integrates a third-party foundation model or hosted API into a production or near-production workflow via contract and technical integration.
- The model's behaviour (accuracy, refusal patterns, safety filtering, known jailbreak susceptibility) is determined entirely by the provider's training and deployment choices, invisible to the firm absent diligence.
- Firm's risk and control functions rely on provider-supplied documentation (model cards, safety reports) as the primary evidence source.

## 4. Failure Mode
> The firm onboards or continues to rely on a foundation model or API provider whose safety evaluation coverage, security posture and known weaknesses have not been assessed proportionately to the materiality of the use case, so material provider-side risk is inherited into customer-facing or regulated processes without independent characterisation.

## 5. Potential Consequences
- **Customer:** Undetected provider weaknesses (e.g. known jailbreak classes, biased training data, weak content filtering) propagate directly into customer-facing decisions or communications.
- **Institution:** Outsourcing/CTP register incompleteness findings; inability to defend a model risk approval when challenged on provider-side evidence; costly emergency re-diligence after an incident.
- **Regulator/market:** DORA Art. 28-style third-party risk management deficiency finding; EBA outsourcing guidelines non-compliance; reputational damage if a known, publicly documented provider weakness later surfaces in a customer harm event.

## 6. Failure Chain
```
Provider onboarded under time/commercial pressure; diligence scoped
to procurement/legal checklist, not AI-specific safety/security review
  ↓ (IRQ-GOV-001: no accountable owner mandates AI-specific diligence)
Model integrated into customer-facing or regulated workflow
  ↓ (IRQ-MOD-011: approval relies on vendor-reported, uncontaminated-unverified evaluation scores)
Known provider weakness (e.g. documented hallucination class, safety
filter gap) remains uncharacterised by the firm
  ↓
Weakness manifests in production (incorrect customer communication,
missed AML flag, biased decision)
  ↓
Incident investigation finds no internal record that the weakness
was ever assessed → outsourcing register gap identified

Control Breakpoints:
  • IRQ-GOV-001: named accountable owner mandates AI-specific diligence scope
  • IRQ-TPR-001: materiality-based due diligence framework, executed and evidenced
  • IRQ-MOD-011: evaluation evidence independently checked, not vendor-asserted
```

## 7. Why a Domain Expert May Miss It
- Traditional outsourcing due diligence (financial stability, data security, business continuity) does not naturally extend to AI-specific concepts like safety evaluation coverage or jailbreak susceptibility; procurement teams complete the checklist without knowing what's missing.
- "The provider is a major, reputable lab" is treated as a substitute for materiality-based diligence rather than a starting assumption still requiring evidence.
- Vendor model cards are marketing-adjacent documents; SMEs unfamiliar with AI evaluation literature cannot distinguish a rigorous safety evaluation from a promotional summary.
- Diligence is typically a one-time, pre-contract event; AI model behaviour changes post-contract (see TPR-004), so a "passed" diligence event provides false ongoing assurance.

## 8. Assurance Objective
**AO-TPR-001:** The firm shall complete and evidence AI-specific due diligence — proportionate to the materiality of the use case — covering safety evaluation coverage, security posture and known model weaknesses, before relying on a foundation model or API provider in production, and shall refresh this diligence at defined intervals.

## 9. Expected Controls (Traced)
- **Materiality-tiered third-party risk assessment** — [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02, Title IV, Section 12 (Pre-outsourcing analysis, incl. 12.3 Due diligence), with criticality determined under Title II, Section 4 (Critical or important functions)] (verified 29 Jul 2026) — due diligence depth scaled to criticality of the outsourced function.
- **ICT third-party risk management diligence** — [Regulation (EU) 2022/2554, DORA, Art. 28–29] — pre-contract due diligence on ICT third-party providers, including concentration and sub-outsourcing risk.
- **Outsourcing and third-party risk oversight** — [PRA SS2/21, March 2021, "Outsourcing and third party risk management"] — proportionate due diligence and ongoing oversight of critical outsourced services.
- **Model risk management provider evaluation** — [PRA SS1/23, May 2023, development/validation principles extended to vendor models] [VERIFIED 25 Aug 2026 against the SS1/23 text: its stated scope covers "all models, developed in-house or externally, including vendor" models, and Principle 2.6 ("Use of externally developed models, third-party vendor products") states vendor-model expectations directly. An earlier marker here claimed the opposite; corrected at the v1.1.1 errata batch] — independent characterisation of vendor model performance and weaknesses prior to reliance.
- **AI-specific safety/security evaluation checklist** — Emerging Practice — no single published FS-specific standard exists for AI provider diligence; firms are extending general model risk and outsourcing frameworks pending sector-specific guidance.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor's own model card or safety report, unverified — **L1**.
- Firm's due diligence policy naming AI-specific evaluation criteria — **L2**.
- Completed due diligence file for a sampled provider, evidencing safety/security/weakness assessment and materiality tiering — **L3**.
- Internal audit or second-line review confirming due diligence was executed to policy standard across the provider population — **L4**.
- Outsourcing/CTP register showing due diligence status and refresh dates for all in-scope AI providers over the last 12 months — **L5**.

**Dated worked examples, added at the September 2026 refresh — two diligence questions a file written before September 2026 will not have asked.** *(i) Which access tier is the provider, or the provider's own sub-provider, operating on?* A provider publicly operates a tiered access model in which the safeguards applied to general deployment are deliberately absent: "In production, we deploy system-level safeguards to screen cybersecurity-related requests to prevent misuse … Daybreak Blue access removes those guardrails", with the provider's own measurement of the difference — "GPT-5.6-Cyber completes 95.0% of these requests, compared with just 1.5% for GPT-5.6 Sol, and 2.0% when used with Daybreak Blue access", on an internal Advanced Cybersecurity Completion Rate covering "exploit-chain development, authentication bypass, privilege escalation, and other advanced cybersecurity scenarios" [OpenAI, "Expanding Daybreak as the cyber defense window narrows", 10 August 2026]. A diligence file that records a provider's published safety evaluations without establishing **which tier the firm's own traffic runs on** has not addressed known model weaknesses in the sense this IRQ's register question requires. *(ii) Is the tooling the firm's staff install actually the provider's?* A frontier lab's September 2026 threat report records credential harvesters distributed as "malicious client side applications often spoofing as popular AI harnesses including Claude Code but were in fact credential harvesters that would gather all of the victim's credentials and authenticated session tokens on their device", with the stolen material sold "through brokers, which often feed into fraudulent AI reseller networks" [Anthropic, *Detecting and countering misuse of AI: September 2026*, 10 September 2026, printed pp. 28–29]. Provenance of the client-side tooling, and the channel through which access was bought, are diligence objects — see IRQ-SEC-011 §9 for the publisher's stated control.

## 11. Independent Test
> Select a materiality-stratified sample of current AI providers from the outsourcing register. For each, verify (a) a due diligence file exists, (b) it addresses safety evaluation coverage, security posture and known weaknesses specifically (not generic vendor risk only), and (c) the depth is proportionate to materiality tier. Cross-check provider-claimed evaluation results against independently available information (public model cards, red-team reports) where accessible. Test executed against firm documentation and public sources only; no live provider system accessed. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, standards-anchored method; no single agreed FS benchmark for "proportionate AI diligence" scoring).

## 12. Pass Indicators
- 100% of critical-tier AI providers have a due diligence file addressing safety, security and known weaknesses.
- Due diligence depth is visibly proportionate to materiality tier, not uniform boilerplate.
- Refresh cadence is defined and evidenced (not one-time at onboarding).
- Sampled provider claims are cross-checked against independently available evidence, not accepted at face value.

## 13. Fail Indicators
- Due diligence files consist solely of commercial/legal checklists with no AI-specific safety or security content.
- Materiality tiering is absent or not reflected in diligence depth.
- No refresh mechanism exists; diligence is a single pre-contract event regardless of criticality.
- Provider-reported evaluation claims are accepted without any independent cross-check.

## 14. Reporting Language
**Pass:** "AI-specific due diligence, proportionate to materiality, is evidenced for all sampled critical-tier providers, covering safety evaluation coverage, security posture and known weaknesses. Refresh cadence is defined and operating. Conclusions rest on ★3 methodology — standards-anchored, no agreed FS benchmark — and should be read as professional assessment."

**Fail:** "Sampled provider due diligence files address only commercial and legal risk; no AI-specific safety, security or known-weakness assessment is evidenced for [x]% of critical-tier providers. This is a foundational third-party risk gap: the firm cannot demonstrate it understands the risk profile of models underpinning customer-facing decisions."

**Partial:** "Due diligence is robust for directly procured foundation model providers but absent for embedded vendor AI (see IRQ-TPR-003) and for providers onboarded before the current framework took effect. Remediation plan should prioritise the highest-materiality legacy gaps first."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (single provider weakness typically bounded to specific workflow; regulatory notice risk if outsourcing register found deficient)
  Likelihood: 2 (plausible if diligence process lapses under commercial pressure; not routine given policy existence)
  Detectability: 3 (surfaces via periodic audit or incident, not real-time)
  Recoverability: 2 (remediable via retrospective diligence and, if needed, provider substitution; moderate cost)
  Novelty: 3 (domain expert may miss AI-specific evaluation gaps within a familiar outsourcing-diligence process)

If controls are absent or degraded:
  Severity: 3 (multiple customers harmed via undetected provider weakness in customer-facing process)
  Likelihood: 3 (probable given diligence checklists rarely evolve to AI-specific content without deliberate redesign)
  Detectability: 3 (detected via incident or external disclosure, not internal monitoring)
  Recoverability: 3 (provider substitution and retrospective diligence take weeks-to-months; outsourcing register remediation plan required)
  Novelty: 3 (requires AI evaluation literacy uncommon in traditional outsourcing/procurement teams)

Residual risk interpretation: Acceptable with a functioning, evidenced, materiality-tiered diligence process; highest concern is novelty combined with detectability — gaps are easy to miss and slow to surface.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Bounded to the specific workflow served by the under-diligenced provider; escalates only if the weakness is systemic to the provider's model |
| **Likelihood** | 2 | Diligence policies generally exist; failure mode is process erosion or scope gaps rather than total absence |
| **Detectability** | 3 | Detected via periodic audit, outsourcing register review or incident — not real-time monitoring |
| **Recoverability** | 2 | Retrospective diligence and, where necessary, provider substitution are achievable within weeks |
| **Novelty** | 3 | AI-specific evaluation concepts (safety coverage, jailbreak susceptibility) fall outside traditional outsourcing diligence training |

## 17. Regulatory Basis
> [EBA Guidelines on outsourcing arrangements, EBA/GL/2019/02] require proportionate pre-contract due diligence for outsourced functions (Title IV, Section 12, incl. 12.3 Due diligence; criticality under Title II, Section 4) [UNVERIFIED — the Guidelines set general outsourcing due-diligence criteria and do not name AI-specific criteria; mapping to AI due diligence is FAIAS's own interpretive extension] (verified 29 Jul 2026). [Regulation (EU) 2022/2554, DORA, Art. 28] requires ICT third-party risk assessment before contracting, including concentration risk. [PRA SS2/21, March 2021] sets outsourcing and third-party risk management expectations for UK firms, including proportionate due diligence scaled to criticality.

## 18. Research Basis
> No peer-reviewed research specifically addresses "AI provider due diligence" as a discipline; this IRQ extends established outsourcing risk management literature and general model risk management practice (PRA SS1/23 development/validation principles) to the AI provider context. No published FS incident cleanly evidences an AI provider due-diligence failure as at 25 August 2026 — recorded as an absence, per this standard's convention. The NYDFS Apple Card report (March 2021), sometimes offered for this, is deliberately not cited here: the underwriting model was the issuing bank's own and NYDFS found no vendor-diligence failure (the report is used, correctly, for conduct in CANVASES_CON.md).
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-GOV-001 (I.1 Inventory & Ownership: accountable owner mandates diligence scope)
  - IRQ-MOD-011 (B.5 Distribution Shift & Evaluation Integrity: evaluation evidence independently checked)
  - IRQ-TPR-002 (F.1 Contracts & Licensing: diligence findings should shape contractual rights)
  - IRQ-TPR-008 (F.3 Concentration: diligence feeds concentration risk assessment)
  - IRQ-SEC-011 (E.4 Non-human identity and credentials: provenance of installed client tooling and the channel through which access is bought are diligence objects)
```

## 20. References
```
[1] European Banking Authority, 2019. "Guidelines on outsourcing arrangements." EBA/GL/2019/02.
    URL: https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-outsourcing-arrangements
    Accessed: 2026-07-29. EBA/GL/2019/02 confirmed as the current, applicable version (no superseding outsourcing guideline identified as at this date) (verified 29 Jul 2026).
    Checked 3 Oct 2026: still applicable. On 18 September 2026 the EBA published a final report for
    Guidelines on the sound management of third-party risk related to non-ICT services (EBA/GL/2026/09),
    which will repeal EBA/GL/2019/02 from a date not yet set.

[2] European Union, 2022. "Regulation (EU) 2022/2554 on digital operational resilience for the financial sector (DORA)."
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[3] Prudential Regulation Authority, 2021. "SS2/21 — Outsourcing and third party risk management."
    Published: March 2021
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/outsourcing-and-third-party-risk-management-ss

[4] New York State Department of Financial Services, 2021. "Report on Apple Card Investigation." (Retained as the source for field 18's deliberate non-citation note — the report evidences no vendor-diligence failure.)
    Published: March 2021 (issued 23 March 2021, per the Department's press release of that date)
    URL: https://www.dfs.ny.gov/reports_and_publications/202103_report_apple_card_investigation
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.1 (Third Party domain, Due Diligence, Contracts & Licensing)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Traditional outsourcing SMEs complete commercial/legal checklists without AI-specific safety/security evaluation content.
✓ Test 2 (Plausible Harm): Grounded in the DORA/EBA/PRA outsourcing regime; no published incident cleanly evidences a provider due-diligence failure — recorded as an absence in field 18.
✓ Test 3 (Testable): Answerable via sampled review of due diligence files against materiality tiering.
✓ Test 4 (Decision-Relevant): Outcome gates provider onboarding/continued reliance.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Expected Evidence — two dated worked examples added (a provider-operated access tier from which the system-level guardrails are removed, and beside it a separately trained cyber model: on the provider's own advanced-cybersecurity completion measure, 1.5% for the guardrailed baseline, 2.0% for the de-guardrailed tier and 95.0% for the separately trained model, 10 Aug 2026; credential harvesters spoofing AI coding harnesses, 10 Sep 2026). Research Basis unchanged: the absence of a published FS incident evidencing a provider due-diligence failure is not closed by either. Related IRQs — SEC-011 added. ★3 / P3 unchanged.
- v1.2.1 (2026-09-19): References — entry [4] corrected. The entry gave the Department's press release, with a title carried by neither document, while Field 18 relies on the report itself; the title and URL now name the report, and its date is given as the report's own, the day attributed to the press release. Field 18 and its deliberate non-citation note are unchanged, as is the absence recorded there; ★3 / P3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

