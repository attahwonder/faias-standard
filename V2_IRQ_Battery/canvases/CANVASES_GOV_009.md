# CANVAS: IRQ-GOV-009

## 1. IRQ ID & Title
**IRQ-GOV-009: Documentation Below Review-Grade Standard for Independent Review or Regulatory Response**

Register question: "Does documentation (system/model cards, data statements, intended-use and limitation statements) exist at a standard enabling effective independent review and regulatory response?"

## 2. Business Activities Affected
- **Every AI system subject to independent validation, internal audit or regulatory inquiry:** none of these functions can perform their role without documentation of sufficient depth and currency; thin or stale documentation forces reviewers to reconstruct system understanding from scratch, or accept assertions at face value.
- **Regulatory examination or incident response specifically:** a supervisory request for a system/model card, data statement or limitation statement with a short deadline exposes documentation gaps immediately and publicly; this is one of the most visible governance failure modes to an external party.
- **Handover across teams (staff turnover, outsourcing, vendor transition):** documentation is frequently the only artefact that survives a change of personnel; where it is thin, institutional knowledge of a system's actual behaviour and limitations is lost with the departing individual.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns whether documentary artefacts describing the system (system/model cards, data statements, intended-use and limitation statements) exist at a standard sufficient for independent review, not the system's own outputs.

## 4. Failure Mode
> Documentation describing an AI system's design, data basis, intended use, known limitations and evaluation results exists only as thin, generic, stale or vendor-boilerplate material — insufficient in depth, specificity or currency to enable a reviewer independent of the development team, or a regulator responding to an inquiry, to understand what the system actually does, on what basis it was approved, and where its known weaknesses lie.

## 5. Potential Consequences
- **Customer:** Where documentation is inadequate, downstream reviewers (validation, audit, complaint-handling) cannot properly assess whether a specific customer harm traces to a known, documented limitation or an undocumented gap — slowing and weakening the firm's ability to respond to and remediate the harm.
- **Institution:** Inadequate documentation is discoverable and reputationally damaging in its own right during a regulatory examination or litigation discovery process, independent of whether the underlying system actually performed safely.
- **Regulator/market:** The EU AI Act's technical documentation obligation (Art. 11, Annex IV) and PRA SS1/23's documentation principle both make documentation adequacy an examinable requirement in itself; a firm that cannot produce review-grade system/model cards on request faces a direct compliance finding regardless of the system's actual safety performance.

## 6. Failure Chain
```
System/model card and data statement produced once at initial approval, using
vendor boilerplate or a generic template with minimal system-specific content
  ↓ (IRQ-GOV-009 — THIS IRQ: documentation does not reach review-grade depth
  or is not maintained current with system changes)
System evolves (prompt changes, model version updates, new use cases) without
documentation being updated to reflect the change
  ↓ (IRQ-MOD-013: prompt/config changes occur without a documentation trail)
Independent validator, internal auditor or regulator requests the system/model
card and receives material that is thin, generic or materially out of date
  ↓ (IRQ-GOV-007: independent validation cannot function without adequate
  documentation to review against)
Reviewer cannot form an independent assessment; either defers to unverified
assertion, or the review itself stalls/fails
  ↓
Regulatory finding on documentation adequacy, independent of underlying system
performance; or, in an incident, slower and weaker root-cause investigation and
customer remediation because the system's actual known limitations are not
findable in any document

Control Breakpoints:
  • IRQ-GOV-009: review-grade documentation standard set, applied and version-controlled
  • IRQ-MOD-013: documentation updated as part of every change-control event, not only
    at initial approval
  • IRQ-GOV-007: validation depends on this IRQ's documentation as its primary input
  • IRQ-GOV-010: decision-record retention depends on documentation identifying what
    the system was approved to do, against which records are reconciled
```

## 7. Why a Domain Expert May Miss It
- SMEs experienced with traditional model documentation (a static statistical model, documented once at build) may not appreciate that GenAI/agentic systems change behaviour materially through prompt, configuration or vendor-model updates without any code change — and that documentation must therefore be a living artefact updated at each change, not a one-off deliverable.
- Vendor-supplied "model cards" (a published format, e.g. from foundation model providers) look authoritative and complete, but describe the vendor's general-purpose model, not the firm's specific fine-tuning, prompting, guardrails, integration or intended use — a reviewer can mistake vendor documentation for firm-specific documentation.
- Documentation adequacy is invisible until someone actually tries to use it for an independent purpose (validation, audit, regulatory response); a document that "exists" satisfies a checklist tick without ever being tested for whether it actually enables the review it is meant to support.
- Intended-use and limitation statements are the fields most likely to be generic ("use responsibly," "may occasionally be inaccurate") rather than specific to the firm's actual deployment — a governance-literate reviewer checking for the field's presence can miss that its content is not review-grade.

## 8. Assurance Objective
**AO-GOV-009:** Documentation (system/model cards, data statements, intended-use and limitation statements) shall exist for every AI system at a standard of specificity and currency sufficient to enable effective independent review by a party without prior system knowledge, and shall be maintained current through the system's change-control process.

## 9. Expected Controls (Traced)
- **Firm-specific system/model card covering intended use, known limitations, evaluation results and approved operating envelope, distinct from vendor-supplied generic model documentation** — [EU AI Act, Regulation (EU) 2024/1689, Art. 11 and Annex IV — technical documentation requirements for high-risk AI systems] — the direct anchor for Annex III high-risk use cases (credit, insurance pricing); extended as good practice to non-Annex-III systems given the same reviewability need.
- **Documentation update triggered as a mandatory step of every material change-control event (model version, prompt/config change, new use case)** — [PRA, SS1/23, May 2023, documentation principle] — ties documentation currency to the firm's existing change-control process rather than leaving it as a standalone task.
- **Independent readability/completeness check: a reviewer without prior system knowledge can answer defined key questions (intended use, known limitations, approved envelope, evaluation basis) from the documentation alone** — [ISO/IEC 42001:2023, clause 7.5 — documented information] — a practical adequacy test distinct from mere existence.
- **Data statement documenting training/grounding data provenance, cross-referenced to IRQ-DAT-001** — [EU AI Act, Art. 11 and Annex IV, point 2(d)] — data governance documentation is an explicit Annex IV component.
- **Version-controlled documentation register with a defined retention period aligned to regulatory examination and complaint-handling timeframes** — [FCA/PRA record-keeping expectations under SYSC; EU AI Act Art. 18, retention of technical documentation] — ensures historical documentation versions remain retrievable, not only the current version.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor model card cited as the firm's system documentation with no firm-specific supplement — **L1** (assertion of adequacy; does not evidence firm-specific reviewability).
- Firm-specific system/model card template specifying required fields (intended use, limitations, envelope, evaluation basis, data statement) — **L2**.
- Sample completed system/model card for a specific deployed system, reviewed for specificity (not generic boilerplate) — **L3**.
- Independent readability test: a reviewer with no prior system knowledge attempts to answer defined key questions from the documentation alone, with results recorded — **L3**.
- Internal audit or independent validation report assessing documentation adequacy across a sample of systems — **L4**.
- Documentation version history for a sample of systems, cross-checked against the change-control log to confirm updates occurred at each material change — **L5**.
- **Worked example — documentation currency where the source itself changes, 8–10 September 2026 (OpenAI, "On the Navier–Stokes Millennium Prize Problem").** The page as published on 8 September 2026 was amended on 10 September. Footnote 2 of the current page discloses, in a dated note naming the section, that it changed and why: "Update — September 10, 2026: We have updated “Concurrent work” with findings from our investigation into whether user inputs could have influenced this result." What the note does **not** disclose is that a hedge sentence was removed from that section, or its wording; the removal is established only by comparing a pre-deletion archived capture against the live page, and the edit is wider than one deletion — **two provenance sentences were added and two further sentences recast**, one of which adds an attribution to a competitor's model. The removed sentence remained published on the same provider's X post of 8 September as at the date of capture. **This is neither a silent edit nor a retraction, and neither word is used.** Expected evidence, where a firm relies on an external page as documentation or substantiation: a dated, hashed snapshot captured at the time of reliance, because a dated update note is not the same artefact as a system-card change log and the absence of one does not mean the page is stable — **L3**.
- **Worked example — launched products without a product card, 10 September 2026, checked as at 11 September 2026 (OpenAI, "Introducing the Agents API" and "Introducing ChatGPT for Financial Services").** An agent platform whose own launch page states "OpenAI hosts and maintains the harness. You choose the agent’s compute environment: in an OpenAI-managed sandbox, on your own infrastructure" carries no system card and no safety, evaluation, guardrail or misuse content: the string "safety" appears on that page only in site-wide navigation and in a customer's brand name. **The absence is stated within the scope in which it was checked: within the product's launch page as at 11 September 2026**, not as a claim that nothing exists anywhere. A sector-named product launched the same day — positioned for "investment banking and equity research", stating "Your firm’s business data is not used to train our models by default" and offering multiple workspaces "to enforce information barriers" — carries no sector-specific risk assessment, bias evaluation, or market-abuse/MNPI-handling test evidence. Its Benchmarks section carries three capability/accuracy evaluations (OfficeQA Pro on U.S. Treasury Bulletins, BoxBench, and an internal slide-creation evaluation), none of which addresses risk, bias or market conduct — which is the point: capability benchmarking is present and control evidence is absent. Together these are documented instances in which this canvas's key-question set (intended use, known limitations, approved operating envelope, evaluation basis) scores *unanswerable* from the vendor's own material, and the firm-specific supplement is the only available source — **L1 in both instances**.

## 11. Independent Test
> Select a risk-based sample of deployed AI systems. For each, obtain the current system/model card, data statement and intended-use/limitation statement. Task a reviewer with no prior knowledge of the specific system with answering a fixed set of key questions (what is this system's approved intended use; what are its documented known limitations; what evaluation evidence underpins its approval; has the approved operating envelope been stated explicitly) using only the documentation provided, under a defined time limit. Score whether each question is answerable, partially answerable, or unanswerable from the material. Separately, cross-check documentation version dates against the change-control log for the same systems to test currency. Methodology follows standard documentation-adequacy and readability-testing practice (as applied in technical-writing and compliance-documentation audits), extended to the AI-specific field set (limitations, envelope, evaluation basis) with no AI-specific benchmark for "sufficient" documentation depth. Conducted against documentation and change-control records only; no production system access required. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (credible, established documentation-adequacy and readability-testing methodology; the specific field set and answerability threshold for AI system documentation has no AI-specific benchmark, so the key-question set and pass threshold rest on reviewer professional judgement, informed by the EU AI Act Annex IV structure as an external reference).

## 12. Pass Indicators
- ≥90% of key questions answerable from documentation alone across the sample, with no reliance on the original development team's tacit knowledge.
- Documentation is firm-specific (not vendor boilerplate) for all sampled systems, with intended-use and limitation statements specific to the actual deployment.
- Documentation version dates align with the change-control log; no material change identified without a corresponding documentation update.
- Data statements cross-reference to IRQ-DAT-001 provenance evidence, not asserted separately.
- Version history is retrievable for prior documentation states, not only the current version.

## 13. Fail Indicators
- Key questions are unanswerable from documentation alone for a material proportion of the sample, requiring the reviewer to contact the original development team.
- Documentation consists substantially of vendor-supplied generic model cards with no firm-specific content on intended use, limitations or envelope.
- Documentation version dates predate known material changes (model update, prompt change) identified in the change-control log — a currency gap.
- Intended-use and limitation statements are generic ("use responsibly") rather than specific to the actual deployment and known failure modes.
- No version history exists; only the current documentation state is retrievable, preventing reconstruction of what was known at the time of a past decision.

## 14. Reporting Language
**Pass:** "System/model card documentation for the sampled systems enabled a reviewer with no prior system knowledge to answer [n]% of defined key questions unaided, and documentation version dates align with the change-control log across the sample. Conclusions rest on ★3 methodology — established documentation-adequacy and readability-testing practice, with the AI-specific field set informed by the EU AI Act Annex IV structure — and should be read as professional assessment."
**Fail:** "Testing found that documentation for [n] of [sample size] systems consisted substantially of vendor-supplied generic model cards, with key questions on intended use, limitations and approved envelope unanswerable without contacting the original development team. This does not meet the review-grade standard required for independent validation, audit or regulatory response, and represents a standalone compliance exposure under EU AI Act Art. 11/Annex IV for in-scope systems. Remediation should produce firm-specific documentation before further reliance is placed on validation conclusions for these systems."
**Partial:** "Documentation is review-grade and current for [x]% of the sample but has not been updated to reflect a subsequent model or prompt version change for the remainder, creating a currency gap. The assurance objective is not yet met for the affected systems; remediation should update documentation to the current state within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (a documentation gap is primarily a reviewability and compliance-exposure
              issue; it compounds the severity of whatever underlying weakness it
              obscures rather than causing standalone customer harm directly)
  Likelihood: 2 (plausible where documentation is treated as a one-off deliverable
              rather than a living artefact tied to change control; reduces materially
              with a version-controlled, change-triggered process)
  Detectability: 3 (invisible until a reviewer actually attempts to use the
              documentation for an independent purpose; a checklist "document exists"
              tick does not surface content-adequacy gaps)
  Recoverability: 1 (a documentation remediation exercise, once identified, is
              achievable relatively quickly, though historical decisions made under
              inadequate documentation cannot be retrospectively re-documented with
              full fidelity)
  Novelty: 2 (a governance-literate reviewer would generally expect documentation to
              exist and be checked for presence; the AI-specific nuance — vendor
              model cards are not firm-specific documentation, and prompt/config
              changes require documentation updates without a code change trigger —
              is a moderate rather than severe blind spot)

Interpretation: acceptable residual risk with a version-controlled, change-triggered
documentation process and periodic readability testing; principal concern is that
this IRQ is foundational to IRQ-GOV-007 (validation) and IRQ-GOV-010 (decision
reconstruction) — its failure degrades the evidentiary basis of both.

If controls are absent or degraded:
  Severity: 3 (documentation inadequacy is directly examinable by a regulator under
              EU AI Act Art. 11/Annex IV for in-scope systems, and independently
              undermines every downstream review that depends on it)
  Likelihood: 3 (foreseeable where GenAI documentation practice has not yet matured
              to treat prompt/config changes as documentation-triggering events)
  Detectability: 3 (surfaces reliably once tested against an independent-reviewer
              exercise or a regulatory documentation request, though not before)
  Recoverability: 2 (remediable through a documentation programme, but historical
              decision context lost during the inadequate-documentation period
              cannot be fully reconstructed)
  Novelty: 2
Residual risk: Moderate-to-high if documentation is thin or stale; material because
this IRQ underpins the evidentiary integrity of both validation (GOV-007) and
decision-reconstruction (GOV-010).
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | A reviewability/compliance-exposure issue that compounds underlying risk rather than causing standalone customer harm directly. |
| **Likelihood** | 2 | Plausible where documentation is treated as a one-off deliverable rather than tied to change control; reduces with a version-controlled process. |
| **Detectability** | 3 | Invisible until a reviewer actually attempts independent use of the documentation; a presence-only checklist tick does not surface content-adequacy gaps. |
| **Recoverability** | 1 | A documentation remediation programme, once identified, is achievable relatively quickly. |
| **Novelty** | 2 | Moderate blind spot: governance SMEs expect documentation to exist, but the AI-specific nuance (vendor cards are not firm-specific; prompt changes need documentation updates) is less severe a gap than most GOV IRQs. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 11 and Annex IV] requires technical documentation for high-risk AI systems covering intended purpose, design specifications, data requirements, evaluation results and known limitations, applicable to Annex III credit-scoring and insurance-pricing systems from 2 Dec 2027 (postponed from 2 Aug 2026 by the Digital Omnibus, Regulation (EU) 2026/1744, in force 27 Jul 2026), retained per Art. 18. [PRA, SS1/23, May 2023] documentation principle requires models to be documented to a standard enabling effective independent review and validation, extended to AI/ML. [ISO/IEC 42001:2023, clause 7.5] requires documented information to be controlled, current and available to those who need it. Section pinpoints [UNVERIFIED — cited modules/articles confirmed extant (PRA SS1/23, SS1/21, PS21/3, ISO/IEC 42001:2023, EU AI Act Arts. 9/11/12/19); no AI-specific sub-clause pinpoint published by the regulator beyond module/clause level cited] (verified 29 Jul 2026).

## 18. Research Basis
> [Mitchell, M. et al., 2019, "Model Cards for Model Reporting," ACM FAT* 2019 (arXiv:1810.03993)] is the foundational published framework for structured model documentation and the direct ancestor of the system/model-card control cited here. [Gebru, T. et al., 2021, "Datasheets for Datasets," Communications of the ACM (arXiv:1803.09010)] provides the equivalent structured framework for the data-statement component of this IRQ's control. No FS-specific empirical literature quantifies documentation-adequacy failure rates for deployed GenAI systems; this control area otherwise draws on regulatory and audit practice rather than a dedicated FS research literature.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-001 (A.1: training data provenance — the evidentiary basis the data
    statement component of this IRQ's documentation must reflect)
  - IRQ-MOD-009 (B: unfaithful reasoning/interpretability limits — a documented
    limitation this IRQ's intended-use/limitation statement should capture)
  - IRQ-MOD-013 (B.6: prompt/config version control — the change-control trigger
    that should mandate a documentation update)
  - IRQ-GOV-007 (I.3: independent validation — depends on this IRQ's documentation
    as its primary review input)
  - IRQ-GOV-010 (I.4: decision-reconstruction records — depends on this IRQ's
    documentation identifying what the system was approved to do)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L 12.7.2024. Art. 11 and Annex IV, Technical Documentation.
[2] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[3] ISO/IEC, 2023. "ISO/IEC 42001:2023 — Artificial intelligence management systems —
    Requirements." Clause 7.5, Documented Information.
[4] Mitchell, M., Wu, S., Zaldivar, A., et al., 2019. "Model Cards for Model Reporting."
    ACM FAT* 2019. arXiv:1810.03993.
[5] Gebru, T., Morgenstern, J., Vecchione, B., et al., 2021. "Datasheets for Datasets."
    Communications of the ACM. arXiv:1803.09010.
[6] OpenAI, 2026. "On the Navier–Stokes Millennium Prize Problem." 8 September 2026,
    updated 10 September 2026.
    URL: https://openai.com/index/navier-stokes-solution/
[7] OpenAI, 2026. "Introducing the Agents API." 10 September 2026.
    URL: https://openai.com/index/introducing-the-agents-api/
[8] OpenAI, 2026. "Introducing ChatGPT for Financial Services." 10 September 2026.
    URL: https://openai.com/index/introducing-chatgpt-financial-services/
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): SMEs mistake vendor-supplied generic model cards for firm-specific
  documentation, and do not appreciate that GenAI prompt/config changes require documentation
  updates without any code-change trigger.
✓ Test 2 (Plausible Harm): Grounded in the EU AI Act Art. 11/Annex IV technical documentation
  obligation (directly examinable) and PRA SS1/23's documentation principle; failure here
  degrades the evidentiary basis of validation (GOV-007) and decision reconstruction (GOV-010).
✓ Test 3 (Testable): Testable via an independent-reviewer readability exercise against defined
  key questions, and documentation-version-vs-change-control-log reconciliation. ★3 methodology.
✓ Test 4 (Decision-Relevant): Gates whether validation, audit and regulatory-response findings
  for a system can be trusted to rest on adequate, current documentation.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 10 — two dated worked examples added on documentation currency and adequacy: the OpenAI Navier–Stokes page amended 10 Sep 2026 under a dated footnote naming the section, with the removed hedge undisclosed on the page and still live on the provider's X post at capture (described as neither a silent edit nor a retraction, and recorded as five changes, not one deletion), giving rise to a dated, hashed-snapshot expectation where an external page is relied upon; and two products launched 10 Sep 2026 with no product card — the Agents API, checked within its own launch page as at 11 Sep 2026, and ChatGPT for Financial Services, which carries capability benchmarking (OfficeQA Pro, BoxBench, an internal slide-creation evaluation) but no sector-specific risk, bias or market-conduct control evidence. ★3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

