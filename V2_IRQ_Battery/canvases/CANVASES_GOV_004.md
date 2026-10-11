# CANVAS: IRQ-GOV-004

## 1. IRQ ID & Title
**IRQ-GOV-004: Tiering Methodology Fails to Capture Generative and Agentic Risk Drivers**

Register question: "Does the risk-based tiering methodology correctly capture generative and agentic characteristics (autonomy, tool access, customer proximity), driving proportionate control depth?"

## 2. Business Activities Affected
- **All AI systems subject to risk-based approval:** tiering determines how much assurance a system receives before and after deployment; a tiering methodology that under-rates a high-autonomy or high-customer-proximity system results in under-controlled deployment.
- **Agentic workflows specifically:** systems with tool access and multi-step autonomy carry risk characteristics (blast radius, irreversible actions) that a traditional model-risk tiering methodology, built for static predictive models, was never designed to weigh.
- **Rapidly evolving deployments:** a system tiered correctly at approval can become under-tiered if autonomy or tool access expands later without re-tiering (linking to IRQ-GOV-012).

## 3. AI Behaviour(s)
- Exercises varying degrees of autonomy (single-turn response vs multi-step agentic action), tool access (read-only retrieval vs write/transactional tools) and customer proximity (internal-only vs directly customer-facing) — the very characteristics a tiering methodology must weigh.
- The same underlying model can be deployed in configurations with very different risk profiles depending on these characteristics, meaning tiering must assess the deployment, not just the model.

## 4. Failure Mode
> The firm's risk-based tiering methodology weighs traditional model-risk factors (data sensitivity, decision materiality, model complexity) but does not adequately capture AI-specific risk drivers — autonomy, tool access and irreversible-action capability, and customer proximity — so a high-risk generative or agentic system is tiered as though it were a low-risk static model, receiving disproportionately shallow control depth.

## 5. Potential Consequences
- **Customer:** A customer-facing agentic system with transactional tool access is subjected to only the light-touch controls appropriate to an internal drafting tool, missing bias testing, escalation design and blast-radius controls the actual risk profile requires.
- **Institution:** The firm's overall control effort is misallocated — resource-intensive assurance is spent on well-understood but lower-risk static models, while genuinely higher-risk agentic deployments pass through with minimal scrutiny.
- **Regulator/market:** A supervisory review that finds tiering does not reflect AI-specific risk characteristics undermines confidence in the whole proportionality basis of the firm's AI governance framework, and is directly contrary to the EU AI Act's risk-tiered structure that regulators increasingly expect firms to mirror internally.

## 6. Failure Chain
```
Tiering methodology inherited or adapted from traditional model risk management,
weighted to data sensitivity and decision materiality
  ↓ (IRQ-GOV-004 — THIS IRQ: autonomy, tool access, customer proximity not adequately weighted)
Agentic system with transactional tool access and customer-facing use is tiered as
"low" because its underlying decision type (e.g., drafting a response) looks routine
  ↓ (IRQ-AGT-003: tool inventory review never triggered because tiering set it out of scope)
System receives shallow control depth: no adversarial testing, no blast-radius review,
minimal human oversight design
  ↓ (IRQ-HUM-004: escalation design proportionate to a "low" tier, not the real risk)
Agentic failure occurs (unauthorised tool action, cascading multi-step error) that
deeper tier-appropriate controls would have caught
  ↓
Customer/institutional harm → post-incident review finds the system was mis-tiered from
approval → tiering methodology itself becomes the root-cause finding

Control Breakpoints:
  • IRQ-GOV-004: tiering methodology explicitly weights autonomy, tool access, customer proximity
  • IRQ-AGT-003: tool inventory and least-privilege review triggered by correct tiering
  • IRQ-GOV-012: re-tiering triggered when autonomy/tool access/customer proximity changes
  • IRQ-HUM-004: escalation design proportionate to actual, not nominal, tier
```

## 7. Why a Domain Expert May Miss It
- Traditional model-risk tiering criteria (data sensitivity, financial materiality, model complexity) are well-established and intuitive to a model risk SME; the additional dimensions specific to generative/agentic systems are not part of that inherited mental model.
- A drafting assistant "just writes text" and can look lower-risk than a numeric scoring model by traditional criteria, even where the drafting assistant has tool access to send that text directly to a customer — the risk driver (autonomy to act, not just to advise) is not captured by materiality-of-output criteria alone.
- Tiering is often set once at initial approval; SMEs used to static models do not anticipate that the same system's risk profile can shift substantially through incremental tool or autonomy additions without triggering a formal re-tiering event.
- Customer proximity as a distinct risk driver (as opposed to decision materiality) is not a standard traditional model-risk dimension — a low-materiality but high-customer-proximity system (e.g., a chat interface with broad but individually low-stakes interactions) can be systematically under-tiered.

## 8. Assurance Objective
**AO-GOV-004:** The firm's risk-based tiering methodology shall explicitly and demonstrably weight generative and agentic risk drivers — autonomy, tool access and irreversible-action capability, and customer proximity — such that control depth is proportionate to the deployment's actual risk profile, not only its underlying model type.

## 9. Expected Controls (Traced)
- **Tiering criteria explicitly including autonomy level, tool/action permissions and customer proximity as scored dimensions** — [Bank of England and PRA, "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI," 22 April 2024, mapping DSIT AI principles onto SS1/23; MAS Information Paper ID 18/24, Dec 2024, materiality/proportionality good practice] — extends traditional model-risk tiering criteria with AI-specific dimensions.
- **Alignment to EU AI Act risk-tier structure for classification consistency where in scope** — [Regulation (EU) 2024/1689, Annex III and Art. 6 (classification rules for high-risk AI systems)] — provides an externally validated reference tiering logic (unacceptable/high/limited/minimal risk) that firms can cross-check internal tiering against, particularly for credit and insurance use cases explicitly named in Annex III.
- **Periodic re-tiering trigger when autonomy, tool access or customer proximity changes** — [linked IRQ-GOV-012; ENGAGEMENT_MODEL.md Major-Change Re-Assessment Trigger 4, "Operating Envelope Expansion"] — tiering is not a one-time assessment at approval.
- **MAS AIRG consultation proposed proportionality framework** — [MAS, "Consultation Paper: Proposed Guidelines on Artificial Intelligence Risk Management (AIRG)," Nov 2025] — proposes materiality/proportionality criteria for AI risk tiering as a cross-sector expectation; consultation closed Jan 2026 and MAS issued the final Guidelines on 7 Oct 2026, which retain the risk materiality assessment expectation (paragraph 4.10), apply in proportion to size and risk profile (paragraph 2.1) and take effect on 7 Oct 2027 [CONFIRMED — the final Guidelines read at mas.gov.sg on 7 Oct 2026] (verified 7 Oct 2026).
- **Independent challenge of tiering outcomes by a function independent of the deployment team** — [linked IRQ-GOV-007; PRA SS1/23, independent validation principle] — Emerging Practice: applying SS1/23's independent-validation principle specifically to challenge tiering *classification* decisions (not just model performance) is not yet standard MRM practice.

## 10. Expected Evidence (Tagged L1–L5)
- Tiering methodology document listing scoring criteria — **L2** (documentation of intent; does not evidence correct application).
- Sample tiering decision records for a cross-section of deployments (static predictive model, generative drafting tool, agentic transactional system) showing the criteria applied — **L2/L3**.
- Design review confirming autonomy, tool access and customer proximity are scored fields in the tiering tool/template, not implicit judgement calls — **L3**.
- Independent re-scoring of a sample of tiering decisions by a reviewer applying the stated criteria, compared against the original tier assigned — **L3**.
- Internal audit or model risk function finding on tiering methodology adequacy, including any finding of systematic under-tiering of agentic systems — **L4**.
- Record of at least one system re-tiered upward following a tool/autonomy change, evidencing the re-tiering trigger is live — **L5**.

## 11. Independent Test
> Select a sample of approved AI systems spanning static predictive models, generative (non-agentic) assistants, and agentic systems with tool access. Independently re-score each system against the firm's stated tiering criteria, explicitly assessing whether autonomy level, tool/action permissions (including irreversibility) and customer proximity were captured in the original tiering decision. Compare the independently derived tier against the tier actually assigned and control depth actually applied. Cross-reference agentic systems against the EU AI Act Annex III classification logic as an external reference point for whether the firm's tier would plausibly align with an externally validated risk classification. Methodology follows standard control-design-adequacy review practice (criteria walkthrough, independent re-scoring, benchmark cross-reference), extended to AI-specific tiering dimensions with no AI-specific benchmark for "correct" tiering. Conducted against governance records only; no production system access required. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established control-adequacy review methodology, strengthened by cross-referencing the published EU AI Act risk-tier structure as an external reference; no single canonical AI tiering methodology exists, so the independently-derived tier itself involves professional judgement).

## 12. Pass Indicators
- Tiering methodology explicitly includes autonomy, tool/action permissions and customer proximity as scored criteria, not implicit judgement.
- Independent re-scoring of the sample produces tiers consistent with the tiers actually assigned; an isolated divergence outside any pattern is recorded as a judged finding, not a Fail by itself — no systematic under-tiering of agentic or customer-facing systems is found.
- Agentic/customer-facing systems in the sample are tiered proportionately to their EU AI Act Annex III classification analogue where applicable.
- A re-tiering trigger exists and has been exercised for at least one system following a material tool/autonomy change.
- Tiering decisions are independently challenged (not self-assigned by the deployment team alone).

## 13. Fail Indicators
- Tiering criteria weight only data sensitivity/decision materiality; autonomy, tool access and customer proximity are absent or implicit.
- Independent re-scoring finds systematic under-tiering of agentic systems relative to their actual risk profile.
- No re-tiering trigger exists; tiers are set once at approval and never revisited despite subsequent tool/autonomy expansion.
- Tiering is self-assigned by the deployment team with no independent challenge (L1/L2 evidence only).
- A customer-facing, high-volume but individually low-materiality system (e.g., a broad-reach chat interface) is tiered low purely on materiality grounds, missing customer-proximity risk.

## 14. Reporting Language
**Pass:** "Independent re-scoring of a cross-section of [n] approved systems, including agentic and customer-facing deployments, confirms the tiering methodology explicitly weights autonomy, tool access and customer proximity, and produces tiers consistent with an independent assessment and with the EU AI Act's published risk-tier structure. A re-tiering trigger is demonstrated live for at least one system following a tool/autonomy change. Conclusions rest on ★3 methodology — established control-adequacy review with no single canonical AI tiering benchmark — and should be read as professional assessment."
**Fail:** "Independent re-scoring found that [n] of [sample size] agentic or customer-facing systems are systematically under-tiered relative to their actual autonomy, tool access and customer proximity, receiving control depth appropriate to a materially lower risk profile. No re-tiering trigger exists for changes in tool access or autonomy post-approval. The proportionality basis of the firm's AI governance framework cannot currently be relied upon for these system classes; re-tiering and remediation of control depth is required before further reliance."
**Partial:** "Tiering methodology correctly captures autonomy and tool access for newly approved systems but has not been retrospectively applied to systems approved before the methodology was updated, affecting [x]% of the current inventory. The assurance objective is not yet met for that legacy population; remediation should complete retrospective re-tiering within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a tiering methodology gap is a control-design issue; realised severity depends
              on what a mis-tiered system actually does)
  Likelihood: 2 (plausible where tiering criteria have not been explicitly updated for
              generative/agentic characteristics; less likely once criteria are current)
  Detectability: 2 (found via periodic independent re-scoring or internal audit; not visible
              from routine operation)
  Recoverability: 1 (reversible by re-tiering and applying the correct control depth once found)
  Novelty: 3 (domain expert applying traditional model-risk tiering criteria would very likely
              under-weight autonomy and customer proximity as distinct risk drivers)

Interpretation: acceptable residual risk once tiering criteria are AI-aware and independently
challenged; the material concern is systemic under-control of the agentic population, which
propagates into every downstream control that depends on correct tiering (testing depth,
escalation design, monitoring intensity).

If controls are absent or degraded:
  Severity: 3 (systematically under-controlled agentic/customer-facing systems can cause
              multi-customer harm via failure modes their shallow control depth never tested for)
  Likelihood: 3 (foreseeable wherever tiering criteria have not been explicitly updated —
              this is the default state for tiering frameworks inherited unchanged from
              traditional model risk management)
  Detectability: 3 (requires a dedicated tiering-adequacy review to surface; not visible from
              within the (mis)tiered system's own monitoring, which is itself shallow)
  Recoverability: 2 (once found, requires re-tiering and retrofitting the correct control
              depth across potentially the whole agentic population — moderate effort)
  Novelty: 3
Residual risk: High if the tiering methodology is stale; systemic because it under-controls
an entire risk class rather than a single deployment.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | The tiering gap itself is a control-design issue; realised severity is inherited from whatever the resulting under-controlled deployments actually do. |
| **Likelihood** | 3 | Probable wherever tiering criteria are inherited unchanged from traditional model risk management without explicit AI-specific update. |
| **Detectability** | 3 | Requires a dedicated independent re-scoring exercise to surface; the mis-tiered system's own (shallow) monitoring will not reveal the gap. |
| **Recoverability** | 2 | Re-tiering a single system is fast, but retrofitting correct control depth across a systematically under-tiered population is moderate effort. |
| **Novelty** | 3 | Autonomy, tool access and customer proximity as distinct risk drivers (separate from data sensitivity/materiality) are AI-specific dimensions a traditional model-risk SME would not default to weighting. |

## 17. Regulatory Basis
> [Bank of England and PRA, "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI," 22 April 2024] and [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023)] establish that model risk tiering/materiality assessment must extend to AI/ML, without prescribing the specific AI-relevant criteria — leaving this an area where firms must demonstrate their own methodology is fit for purpose. [Regulation (EU) 2024/1689 (EU AI Act), Annex III and Art. 6] provides an externally validated risk-tier classification (including credit scoring and life/health insurance pricing as named high-risk uses) that firms can cross-check internal tiering logic against, and which is directly binding for in-scope systems. [MAS, Information Paper ID 18/24, Dec 2024] documents materiality/proportionality as an observed good-practice dimension across surveyed institutions.

## 18. Research Basis
> No peer-reviewed academic literature specifically validating an AI risk-tiering methodology for financial services was identified in the source registers; this control area is regulatory/audit practice rather than a research literature, consistent with this domain's evidentiary profile. The EU AI Act's Annex III classification structure and the MAS thematic review are treated as the most credible available reference points for what AI-aware tiering criteria should weight.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-012 (I.2: envelope drift — re-tiering trigger when autonomy/tools/customer
    proximity change post-approval)
  - IRQ-AGT-003 (C.2: tool inventory and least-privilege — correct tiering determines whether
    this review is triggered at appropriate depth)
  - IRQ-MOD-001 (B.1: capability envelope — tiering should reflect tested capability boundaries)
  - IRQ-GOV-007 (I.3: independent validation — parallel independent-challenge principle applied
    to tiering decisions specifically)
  - IRQ-HUM-004 (D.3: escalation design — proportionate to actual, correctly assessed, tier)
```

## 20. References
```
[1] Bank of England/PRA, 2024. "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI." 22 April 2024.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L, 12 July 2024. Annex III, Art. 6.
[4] Monetary Authority of Singapore, 2024. "Information Paper: Artificial Intelligence Model
    Risk Management — Observations from a Thematic Review." ID 18/24. December 2024.
[5] Monetary Authority of Singapore, 2025. "Consultation Paper: Proposed Guidelines on
    Artificial Intelligence Risk Management (AIRG)." November 2025. Consultation Paper P017-2025 (URL: mas.gov.sg/publications/consultations/2025/consultation-paper-on-guidelines-on-artificial-intelligence-risk-management); consultation closed Jan 2026, final Guidelines issued 7 Oct 2026 and effective 7 Oct 2027 (verified 7 Oct 2026).
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.2 (Governance domain, Approval, Tiering & Policy)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Model-risk SMEs default to data-sensitivity and materiality
  criteria inherited from static predictive models; autonomy, tool access and customer
  proximity are not part of that traditional tiering vocabulary.
✓ Test 2 (Plausible Harm): Grounded in MAS's thematic review findings and the EU AI Act's
  own risk-tier structure, both of which treat these AI-specific dimensions as material to
  classification; under-tiering propagates into every downstream control.
✓ Test 3 (Testable): Testable via independent re-scoring of sampled tiering decisions and
  cross-reference to the EU AI Act's published classification logic. ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome determines whether control depth across the whole AI
  estate is proportionate to actual risk, and whether resource allocation across the
  governance programme is correctly targeted.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 12 — the independent re-scoring Pass indicator clarified: an isolated divergence outside any pattern is recorded as a judged finding, not a Fail by itself, the Pass still turning on the absence of systematic under-tiering of agentic or customer-facing systems. Mirrored in PLAYBOOK_GOV.md's threshold table and §6 Pass clause so the procedure does not read harder than the canvas. Field 13 untouched; no Pass/Fail boundary moved; ★3 unchanged.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Field 9 Expected Controls — the Bank of England and PRA letter of 22 April 2024 cited by its title, The Bank and the PRA's response to DSIT/HMT: update on our approach to AI, with the Bank of England and the PRA as issuers; the statements that the final MAS Guidelines were not yet issued replaced by the fact that MAS issued them on 7 Oct 2026, effective 7 Oct 2027, with the risk materiality assessment expectation retained (paragraphs 2.1 and 4.10). Field 17 Regulatory Basis — the letter citation as in Field 9. Field 20 References — the letter citation as in Field 9; the MAS consultation paper entry carries its reference number, P017-2025, the statement that MAS published none is removed, and the issue date of the final Guidelines is added. No change to controls, test, ★ rating or risk profile.
```

---
---

