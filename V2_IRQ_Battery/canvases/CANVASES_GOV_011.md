# CANVAS: IRQ-GOV-011

## 1. IRQ ID & Title
**IRQ-GOV-011: Applicable Regulatory Obligations Not Mapped to Each AI System with an Evidenced Compliance Owner**

Register question: "Are applicable regulatory obligations (EU AI Act classification, outsourcing/CTP registers, Consumer Duty MI, model risk expectations) mapped to each system with evidenced compliance owners?"

## 2. Business Activities Affected
- **Every AI system, but with sharpest materiality for those touching credit, insurance pricing or other Annex III activities:** without an explicit EU AI Act classification per system, the firm cannot demonstrate it has correctly identified which of its systems attract high-risk obligations, and by extension cannot demonstrate compliance with those obligations.
- **Third-party and vendor-embedded AI specifically:** outsourcing and Critical Third Party (CTP) register obligations attach to the relationship, not just the technology; an unmapped AI-enabled vendor service can silently fall outside the outsourcing register's scope.
- **Consumer Duty MI reporting:** where AI influences customer outcomes, Consumer Duty MI obligations apply to that outcome regardless of whether the firm has explicitly mapped the AI system as a Consumer Duty-relevant component, creating a reporting gap if the mapping has not been done.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns whether the firm's regulatory-obligation mapping exercise (a governance/compliance process) has been performed per system, with an evidenced accountable owner, not the system's own behaviour.

## 4. Failure Mode
> The specific regulatory obligations applicable to a given AI system — EU AI Act risk classification, outsourcing/CTP register status, Consumer Duty MI requirements, and model risk management scope — have not been explicitly determined and mapped for that system, or have been mapped without an evidenced, accountable compliance owner responsible for maintaining and acting on the mapping, such that the firm cannot demonstrate it knows which obligations apply where.

## 5. Potential Consequences
- **Customer:** Obligations designed to protect customers (Consumer Duty MI visibility, high-risk AI Act protections) do not attach in practice if the underlying system was never identified as being in scope for them.
- **Institution:** An unmapped or misclassified system creates latent compliance exposure that only surfaces at the point of a regulatory examination or a triggering incident, by which point remediation is reactive rather than planned, and often accompanied by a finding of inadequate governance process rather than merely a technical gap.
- **Regulator/market:** The EU AI Act's own classification obligation (Art. 6, Annex III) and the broader expectation across PRA/FCA/ECB/MAS guidance that firms maintain a complete, risk-mapped AI inventory make an absent or incomplete regulatory-obligation map a direct, easily-identified governance finding, independent of whether any individual system actually causes harm.

## 6. Failure Chain
```
AI system is inventoried (IRQ-GOV-002) and approved (IRQ-GOV-003) but the specific
regulatory obligations applicable to it are not explicitly determined at that point
  ↓ (IRQ-GOV-011 — THIS IRQ: no per-system regulatory-obligation map exists, or
  the map exists without an evidenced accountable owner)
System is later used in a way that would trigger a specific obligation (e.g. it
supports a credit-scoring or insurance-pricing decision, engaging EU AI Act Annex III;
or a vendor providing it should have been added to the outsourcing/CTP register)
  ↓ (IRQ-GOV-005: policy suite may not require an obligation-mapping step at
  approval, compounding the gap)
The applicable obligation (technical documentation, human oversight design, Consumer
Duty MI, outsourcing register entry) is not fulfilled because it was never identified
as applying
  ↓ (IRQ-GOV-009 / IRQ-GOV-010: without a classification, downstream documentation
  and record-keeping requirements specific to that classification are also missed)
Regulatory examination or a triggering incident surfaces the unmapped/misclassified
system
  ↓
Compliance finding on the mapping process itself, independent of the system's actual
technical safety; remediation is reactive, and any obligation-specific gaps (e.g.
missing Annex IV documentation) compound the finding

Control Breakpoints:
  • IRQ-GOV-002: inventory completeness gives this IRQ a population to map against
  • IRQ-GOV-011: explicit, evidenced, owned obligation mapping performed per system
  • IRQ-GOV-005: policy suite requires obligation mapping as a step of the approval
    process, not a standalone exercise performed inconsistently
  • IRQ-GOV-009: obligation-specific documentation requirements (e.g. Annex IV) flow
    from this IRQ's classification and cannot be met without it
```

## 7. Why a Domain Expert May Miss it
- Compliance SMEs experienced with traditional outsourcing and MRM registers assume existing processes (outsourcing register, MRM inventory) automatically capture AI-enabled arrangements; they may not check whether the specific trigger criteria for those registers have been re-examined for AI-specific characteristics (e.g. whether a GenAI feature embedded in a procured HR or CRM tool was ever assessed against outsourcing-register criteria).
- The EU AI Act's Annex III classification logic is genuinely novel and requires an AI-specific determination (is this a credit-scoring or insurance-pricing system as defined by Annex III) that traditional model risk classification (which asks "is this a model," not "is this AI Act high-risk") does not automatically produce.
- Obligation mapping is easy to perform once, generically, at a firm level ("we are subject to EU AI Act, Consumer Duty, SS1/23") without the harder, system-specific step of determining which obligations apply to which specific deployed system — a reviewer checking "does the firm know about these regulations" can miss that the per-system mapping was never done.
- Ownership of the mapping itself is often diffuse (legal, compliance, model risk and the outsourcing/procurement function may each hold a piece) with no single accountable owner for the complete map — a structural gap that is easy to overlook because each function believes another covers it.

## 8. Assurance Objective
**AO-GOV-011:** Applicable regulatory obligations — EU AI Act classification, outsourcing/CTP register status, Consumer Duty MI requirements, and model risk management scope — shall be explicitly determined and mapped for every AI system in the inventory, with an evidenced, named compliance owner accountable for maintaining the mapping and acting on it.

## 9. Expected Controls (Traced)
- **Per-system EU AI Act risk classification determination (prohibited / high-risk-Annex III / limited-risk / minimal-risk), documented and re-assessed on material change** — [EU AI Act, Regulation (EU) 2024/1689, Art. 6 and Annex III] — the direct, binding classification obligation for firms operating in or serving the EU market, with credit-scoring and life/health insurance pricing named explicitly in Annex III.
- **Outsourcing and Critical Third Party (CTP) register cross-check for every AI system involving a vendor, cloud provider or embedded third-party AI component** — [PRA, SS2/21 — Outsourcing and third-party risk management, Mar 2021] — ensures AI-enabled vendor relationships are assessed against the firm's existing outsourcing-register criteria, not assumed out of scope because the arrangement is framed as "software" rather than "outsourcing."
- **Consumer Duty MI mapping identifying which AI systems influence customer outcomes and therefore require Consumer Duty MI reporting** — [FCA, PRIN 2A Consumer Duty, in force 31 Jul 2023; FCA, "AI Update," Apr 2024] — closes the gap between "the firm has a Consumer Duty MI process" and "this specific AI system's outcomes feed into it."
- **Model risk management scope determination confirming whether a given AI system falls within SS1/23's MRM definition of a model** — [PRA, SS1/23, May 2023] — ensures the firm has made and documented an explicit in-scope/out-of-scope determination, rather than defaulting a novel system type (e.g. an agentic workflow orchestrator) to "not a model" without assessment.
- **Named, evidenced compliance owner for the complete regulatory-obligation map per system, distinct from (and reconciled with) the technical/business system owner under IRQ-GOV-001** — [FCA/PRA SM&CR] — gives the mapping itself an accountable individual, closing the diffuse-ownership gap.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the firm is compliant with applicable AI regulation" at firm level — **L1** (assertion; does not evidence per-system mapping).
- Regulatory-obligation mapping template/register specifying required determinations (AI Act classification, outsourcing/CTP status, Consumer Duty MI relevance, MRM scope) per system — **L2**.
- Completed mapping record for a sample of specific systems, showing the determination made and its rationale — **L3**.
- Cross-check of the mapping against the outsourcing/CTP register and MRM inventory to confirm consistency (no system marked "in scope" in the mapping but absent from the corresponding register) — **L3**.
- Internal audit or compliance-function review of mapping completeness and accuracy across the full inventory — **L4**.
- Evidence of an evidenced compliance owner taking a specific action based on the mapping (e.g. triggering Annex IV documentation on Annex III classification, or adding a vendor to the outsourcing register following the mapping exercise) — **L5**.

## 11. Independent Test
> Select a risk-based sample of AI systems from the complete inventory (IRQ-GOV-002), weighted toward systems plausibly engaging credit, insurance pricing, or vendor/embedded AI arrangements. For each, independently determine: (1) whether it should be classified under EU AI Act Annex III based on its actual use case, (2) whether it should appear on the outsourcing/CTP register based on its vendor/cloud dependency, (3) whether its outcomes should feed Consumer Duty MI, and (4) whether it falls within SS1/23 MRM scope. Compare the independently derived determination against the firm's own documented mapping for the same system, and identify any system where the firm's mapping omits an obligation the independent determination identifies as applicable. Separately, interview the named compliance owner(s) for the mapping to confirm they can describe recent mapping updates and actions taken. Methodology follows standard regulatory-obligation-mapping adequacy review practice (independent re-determination and gap comparison), extended to the AI-specific classification criteria (EU AI Act Annex III) with no AI-specific benchmark for mapping completeness beyond the Act's own classification logic. Conducted against governance records and interviews only; no production system access required. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P3 (§6A.4)** (credible, established regulatory-mapping adequacy review methodology, strengthened by the EU AI Act's own published classification criteria as an external reference point for the highest-materiality obligation; no benchmark exists for the combined four-obligation mapping exercise as a whole, so professional judgement determines overall mapping adequacy).

## 12. Pass Indicators
- Independent re-determination matches the firm's documented mapping for 100% of the sample across all four obligation types.
- Named compliance owner(s) can describe the current state of the mapping and cite a recent action taken as a result of it (e.g. an Annex IV documentation trigger, an outsourcing register addition).
- Outsourcing/CTP register and MRM inventory are consistent with the mapping (no system marked in-scope in one record and absent from the corresponding register).
- Mapping is re-triggered on material system change (new use case, new vendor, new customer segment), evidenced by version history.
- No vendor-embedded AI arrangement identified in the sample is absent from the outsourcing/CTP register despite meeting the register's own trigger criteria.

## 13. Fail Indicators
- Independent re-determination identifies at least one applicable obligation (most commonly EU AI Act Annex III classification, or outsourcing-register status for embedded vendor AI) that the firm's documented mapping omitted.
- No named, evidenced compliance owner exists for the mapping as a whole; responsibility is diffuse across legal, compliance, model risk and procurement functions with no single accountable individual.
- Mapping was performed once at a firm level (generic regulatory-awareness statement) with no per-system determination.
- Outsourcing/CTP register and the regulatory-obligation mapping are inconsistent for a sampled vendor-embedded AI arrangement.
- Mapping has not been updated despite a known material system change (new use case, vendor, or customer segment) in the review period.

## 14. Reporting Language
**Pass:** "Independent re-determination of applicable regulatory obligations for [n] sampled systems matched the firm's documented mapping in all cases; the named compliance owner evidenced recent mapping-driven actions and version history confirms the mapping is updated on material system change. Conclusions rest on ★3 methodology — established regulatory-mapping adequacy review, referenced against EU AI Act Annex III classification criteria — and should be read as professional assessment."
**Fail:** "Independent re-determination found that [n] of [sample size] systems should have been classified as EU AI Act Annex III high-risk, or should appear on the outsourcing/CTP register, and were not identified as such in the firm's mapping. No single accountable compliance owner for the mapping was identified. This represents a material governance gap with direct compliance exposure; remediation should complete and evidence the mapping, assign a named owner, and trigger any consequential obligations (e.g. Annex IV documentation) before external issue of any assurance relying on regulatory-scope determinations for these systems."
**Partial:** "Regulatory-obligation mapping is complete and evidenced for directly developed systems but has not been extended to vendor-embedded AI arrangements identified via IRQ-GOV-002's completeness sweep, affecting [x]% of the inventory. The assurance objective is not yet met for that subset; remediation should extend the mapping within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a mapping gap is a compliance-process issue whose realised severity
              depends on which specific obligation was missed and for how long)
  Likelihood: 2 (plausible given the genuine novelty of EU AI Act classification
              logic and the diffuse ownership pattern across legal/compliance/model
              risk/procurement; reduces materially with a named owner and periodic
              independent re-determination)
  Detectability: 3 (invisible until either an independent re-determination exercise
              or an actual regulatory examination tests the mapping against the
              system population; a firm-level "we are aware of the AI Act" statement
              does not surface per-system gaps)
  Recoverability: 1 (once identified, completing the mapping and triggering any
              consequential obligations is a governance-process fix, achievable
              within a defined remediation period)
  Novelty: 3 (a compliance SME experienced with traditional outsourcing/MRM registers
              may not recognise that AI-specific classification criteria — especially
              EU AI Act Annex III — require a fresh, AI-specific determination rather
              than reliance on existing register criteria)

Interpretation: acceptable residual risk with a named compliance owner and periodic
independent re-determination; principal concern is the diffuse-ownership pattern
across compliance functions, which this IRQ is specifically designed to close.

If controls are absent or degraded:
  Severity: 3 (direct compliance finding under EU AI Act Art. 6/Annex III or PRA
              SS2/21 outsourcing expectations, discoverable by any external examiner
              performing the same cross-check this IRQ's test performs)
  Likelihood: 3 (foreseeable given the well-documented novelty of EU AI Act
              classification and the common diffuse-ownership pattern for
              cross-functional compliance mapping exercises)
  Detectability: 3 (surfaces reliably once an independent re-determination or
              regulatory examination is performed, though not proactively before)
  Recoverability: 2 (the mapping itself is fixable, but a period of unmapped
              operation without required obligations (e.g. Annex IV documentation,
              outsourcing register entry) having been fulfilled cannot be fully
              retrospectively cured)
  Novelty: 3
Residual risk: Moderate-to-high if mapping is absent or unowned; principally a
governance-process finding but with direct, examinable compliance consequences.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | A compliance-process gap whose realised severity is inherited from the specific obligation missed; not a standalone customer-harm mechanism. |
| **Likelihood** | 2 | Plausible given EU AI Act classification novelty and diffuse cross-functional ownership; reduces materially with a named owner and periodic re-determination. |
| **Detectability** | 3 | Invisible until an independent re-determination exercise or an actual regulatory examination tests the mapping; a firm-level awareness statement does not surface per-system gaps. |
| **Recoverability** | 1 | A governance-process fix once identified, achievable within a defined remediation period. |
| **Novelty** | 3 | Compliance SMEs versed in traditional outsourcing/MRM registers may not recognise that EU AI Act Annex III classification requires a fresh, AI-specific determination. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 6 and Annex III] establishes the binding high-risk classification obligation, naming credit-scoring/creditworthiness and life/health insurance pricing/risk-assessment AI explicitly, with obligations applying from 2 Dec 2027 for Annex III systems (postponed from 2 Aug 2026 by the Digital Omnibus, Regulation (EU) 2026/1744, in force 27 Jul 2026). [PRA, SS2/21 — Outsourcing and third-party risk management, Mar 2021] requires outsourcing/CTP register capture of relevant third-party arrangements, applicable to AI-enabled vendor services meeting the register's trigger criteria. [FCA, PRIN 2A Consumer Duty, in force 31 Jul 2023] requires MI on customer outcomes, engaging any AI system materially influencing those outcomes. [PRA, SS1/23, May 2023] requires an explicit scope determination of what constitutes a "model" for MRM purposes, extended to AI/ML. Section pinpoints [UNVERIFIED — cited modules/articles confirmed extant (PRA SS1/23, SS1/21, PS21/3, ISO/IEC 42001:2023, EU AI Act Arts. 9/11/12/19); no AI-specific sub-clause pinpoint published by the regulator beyond module/clause level cited] (verified 29 Jul 2026).

## 18. Research Basis
> No peer-reviewed academic literature specifically evaluates regulatory-obligation-mapping completeness practice for enterprise AI deployment; this control area is compliance and regulatory practice rather than a research literature, consistent with this domain's evidentiary profile. The MAS AI Risk Management Guidelines consultation [MAS, "Consultation Paper: Proposed Guidelines on Artificial Intelligence Risk Management (AIRG)," Nov 2025] is the closest published cross-sector regulatory analogue explicitly requiring firms to map AI systems against a defined risk/materiality/proportionality framework, and is cited here as reinforcing evidence of the direction of international regulatory expectation.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-002 (I.1: inventory completeness — supplies the system population this
    IRQ's mapping must cover, including shadow and embedded AI)
  - IRQ-GOV-001 (I.1: named system ownership — distinct from, and should reconcile
    with, this IRQ's compliance-mapping ownership)
  - IRQ-GOV-005 (I.2: policy suite coverage — should mandate obligation mapping as
    an approval-process step, not a standalone exercise)
  - IRQ-GOV-009 (I.4: documentation adequacy — Annex IV documentation obligations
    flow from this IRQ's EU AI Act classification and cannot be fulfilled without it)
  - IRQ-TPR-002 (F.1: contractual/licensing rights — outsourcing register status
    identified by this IRQ determines which contractual rights the firm must secure)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L 12.7.2024. Art. 6 and Annex III, High-Risk Classification.
[2] PRA, 2021. "SS2/21 — Outsourcing and third-party risk management." March 2021.
[3] FCA, 2022/2023. "PS22/9 / FG22/5: A New Consumer Duty." PRIN 2A in force 31 July 2023.
[4] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[5] Monetary Authority of Singapore, 2025. "Consultation Paper: Proposed Guidelines on
    Artificial Intelligence Risk Management (AIRG)." November 2025.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Compliance SMEs assume existing outsourcing/MRM registers
  automatically capture AI-enabled arrangements, missing that EU AI Act Annex III
  classification requires a fresh, AI-specific determination existing processes were not
  built to make.
✓ Test 2 (Plausible Harm): Grounded directly in the EU AI Act's binding classification
  obligation (Art. 6/Annex III) and PRA SS2/21 outsourcing expectations; an unmapped system
  is a discoverable compliance finding independent of its actual technical safety.
✓ Test 3 (Testable): Testable via independent re-determination against a sample and gap
  comparison to the firm's documented mapping. ★3 methodology, referenced against the AI
  Act's own classification criteria.
✓ Test 4 (Decision-Relevant): Gates whether the firm can demonstrate it knows which binding
  obligations apply to which specific system, ahead of a regulatory examination.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
```

---
---

