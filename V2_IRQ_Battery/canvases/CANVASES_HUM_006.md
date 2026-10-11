# CANVAS: IRQ-HUM-006

## 1. IRQ ID & Title
**IRQ-HUM-006: Accountability Gap Through Delegated and Multi-Agent Workflows**

Register question: "Is there a named accountable owner for each AI-influenced decision, with accountability traceable through delegated and multi-agent workflows to attributable approval records?"

## 2. Business Activities Affected
- **Underwriting review:** Where an AI drafts a recommendation, a second AI or agent applies policy checks, and a human approves, it must be clear which named individual is accountable for the final decision — not merely which system touched it last.
- **Claims approval:** Multi-agent claims workflows (triage agent, liability agent, settlement agent) can leave the question of "who is accountable for this settlement" genuinely ambiguous if accountability was never explicitly mapped through the delegation chain.
- **AML case handling:** Where an investigator delegates evidence-gathering to an AI assistant and a second reviewer approves the closure, accountability for the ultimate typology conclusion must be traceable to a named individual, not diffused across the workflow.

## 3. AI Behaviour(s)
- Participates in multi-step or multi-agent workflows where several AI components and human actors each contribute a partial input to the final decision.
- Produces outputs that are consumed and modified by downstream agents or humans, such that the final decision's provenance is a composite of several contributions.
- Does not itself carry or assert accountability; accountability is a purely organisational construct that must be explicitly designed onto the workflow.

## 4. Failure Mode
> No single named individual can be identified as accountable for a given AI-influenced decision once it has passed through a delegated or multi-agent workflow, because accountability was designed around single-system, single-approver processes and was never explicitly re-mapped as the workflow became multi-step and multi-agent.

## 5. Potential Consequences
- **Customer:** In the event of a wrong decision, there is no clear route to establish who should have caught the error, delaying and potentially frustrating complaint resolution and redress.
- **Institution:** SM&CR obligations cannot be discharged if accountability cannot be traced to a specific senior manager for a specific class of AI-influenced decision; regulatory finding of inadequate governance.
- **Regulator/market:** Loss of confidence that the firm can answer the basic supervisory question "who was accountable for this decision," a foundational expectation of UK prudential and conduct regulation.

## 6. Failure Chain
```
Workflow expands from a single AI-plus-human-approver design to a
multi-step, multi-agent design (additional agents added incrementally
for efficiency)
  ↓ (IRQ-GOV-001: named accountable owner mapping was designed for the
     original, simpler workflow and not re-mapped)
Each agent/human contributes a partial input; no single step is
designated as "the accountable decision point"
  ↓ (IRQ-HUM-006 — THIS IRQ: accountability gap — no traceable named
     owner for the composite decision)
An incorrect decision reaches the customer or regulator; internal
investigation cannot identify who was accountable
  ↓ (IRQ-AGT-007: multi-agent consensus effects may have obscured which
     agent's error actually drove the wrong outcome)
Investigation stalls or produces an unsatisfying diffuse-responsibility
finding
  ↓
Customer/regulatory complaint cannot be properly resolved →
SM&CR-accountability finding against the firm for inadequate
governance design

Control Breakpoints:
  • IRQ-GOV-001: accountable-owner mapping actively maintained as
    workflows evolve, not designed once and left stale
  • IRQ-HUM-006: explicit accountability-point design at each stage of
    a delegated/multi-agent workflow, not assumed to follow from the
    original single-approver design
  • IRQ-AGT-007: per-action responsibility mapping in multi-agent
    orchestrations, feeding into the accountability trace
```

## 7. Why a Domain Expert May Miss It
- Assumption: "we have an accountable senior manager for the AI system" — true at the system level, but the failure mode is at the decision level, where a specific instance of a multi-agent workflow may not map cleanly back to that senior manager's direct oversight of the specific contributing steps.
- Governance frameworks designed under SM&CR predate widespread multi-agent AI workflows and were built around a mental model of a single system with a single owner; incremental addition of intermediate agents or automation steps is a gradual architectural change that rarely triggers a formal re-assessment of the accountability map.
- Process gap: adding a new agent or automation step to an existing workflow is often treated as a technical change requiring code review, not a governance change requiring accountability re-mapping — a categorisation gap, not a deliberate oversight.
- Testing gap: accountability is typically audited by checking that a named owner exists for the system, not by tracing a sample of actual decisions through the full delegation chain to confirm accountability is genuinely attributable at the decision level.

## 8. Assurance Objective
**AO-HUM-006:** Every AI-influenced decision shall be traceable to a named, accountable individual, with accountability explicitly mapped through each stage of any delegated or multi-agent workflow contributing to that decision, and evidenced in attributable approval records.

## 9. Expected Controls (Traced)
- **Decision-level (not merely system-level) accountability mapping** — [FCA/PRA, Senior Managers & Certification Regime, individual accountability framework] — accountability is mapped to the specific decision type and workflow stage, not asserted only at the level of "who owns the AI system."
- **Accountability re-mapping triggered by workflow architecture change** — [linked IRQ-GOV-012; FCA, Handbook SYSC 4.1.1R] — any addition of an intermediate agent, automation step, or delegation point to an existing workflow triggers a review of the accountability map, analogous to change-control practice for the technical architecture.
- **Attributable approval records through the full delegation chain** — [FCA, Handbook SYSC 9, Record Keeping] — records capture not only the final sign-off but the identity (human or specific agent instance/version) responsible for each material contributing step.
- **Per-action responsibility mapping in multi-agent orchestrations** — [linked IRQ-AGT-007; OWASP Agentic AI: Threats and Mitigations, Feb 2025] — where multiple agents contribute, the orchestration design attributes each action to a specific agent instance, avoiding diffuse "the system decided" framing.
- **Decision-trace sampling audit** — [Emerging Practice; extends conventional internal-audit trace-testing methodology to multi-agent decision chains] — periodic sampling of actual decisions, traced end-to-end through the delegation chain to confirm a named individual is genuinely identifiable and was genuinely positioned to exercise accountability.

## 10. Expected Evidence (Tagged L1–L5)
- Governance paper naming a senior manager accountable for "the AI system" — **L1** (system-level only, not decision-level).
- Documented decision-level accountability map for each in-scope workflow — **L2**.
- Workflow/architecture change-log confirming accountability re-mapping occurred at each material workflow change — **L3**.
- Staging trace-sampling exercise: a set of dev/test decisions traced end-to-end through the delegation chain to confirm a named individual is identifiable at each stage — **L3**.
- Independent audit tracing a sample of real historical decisions through the actual multi-agent workflow to confirm accountability was genuinely attributable, not merely mapped on paper — **L4**.
- Historical SM&CR-related enforcement or internal-investigation outcomes referencing this workflow, if any, evidencing whether accountability tracing functioned in practice — **L5**.

## 11. Independent Test
> In a non-production environment, select a representative sample of dev/test decisions that passed through each in-scope delegated or multi-agent workflow. For each, trace the full contributing chain (every agent, automation step and human touchpoint) and attempt to identify a single named individual who was genuinely accountable for the final decision, per the documented accountability map. Score each traced case as "clearly attributable," "attributable with ambiguity," or "not attributable." Separately, review whether the accountability map was updated at the point each intermediate agent or automation step was added to the workflow, using architecture/change-control records. Executed on de-identified dev/test cases and internal change records; no live decisions are affected. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (decision-trace sampling is a recognisable extension of established internal-audit methodology, but its application to multi-agent AI delegation chains is FS-context-bespoke, with professional judgement required to assess what "genuinely attributable" means for a given workflow; no agreed benchmark exists).

## 12. Pass Indicators
- The large majority of sampled decisions are scored "clearly attributable" to a named individual.
- The accountability map has been demonstrably updated at every material workflow architecture change in the review period.
- Approval records capture the identity of each material contributing step (human and specific agent instance/version), not only the final sign-off.
- No sampled decision is scored "not attributable."
- SM&CR mapping documentation references the specific decision types and workflow stages, not only the system as a whole.

## 13. Fail Indicators
- A material proportion of sampled decisions are scored "not attributable" or "attributable with ambiguity."
- The accountability map has not been updated despite one or more material workflow architecture changes (e.g. a new intermediate agent added).
- Approval records capture only the final sign-off, with no attribution for intermediate agent/automation contributions.
- Accountability documentation exists only at the system level ("Senior Manager X owns the AI system"), with no decision-level or workflow-stage mapping.
- A real historical incident or complaint investigation for this workflow was unable to identify an accountable individual.

## 14. Reporting Language
**Pass:** "Decision-trace sampling across [workflow] shows the large majority of decisions are clearly attributable to a named accountable individual through the full delegation chain, and the accountability map has been demonstrably updated at each material workflow change. This is a ★2 assessment — credible extension of established audit methodology, bespoke to multi-agent workflows — and should be re-sampled whenever the workflow architecture changes materially."

**Fail:** "Decision-trace sampling shows a material proportion of decisions passing through [workflow] cannot be traced to a single accountable individual; accountability documentation exists only at the system level and was not updated when [specific agent] was added to the workflow. This represents a governance gap that would materially impede complaint resolution, internal investigation and SM&CR discharge, and should be remediated with an explicit decision-level accountability map before continued reliance."

**Partial:** "Decision-trace sampling shows accountability is clearly attributable for the [primary workflow path] but ambiguous for the [exception-handling path], which was added later without a corresponding accountability re-mapping. Remediation should extend the accountability map to cover the exception path specifically."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (accountability gap itself does not directly cause
    customer harm, but materially impedes resolution and regulatory
    discharge if a harm event occurs elsewhere in the chain)
  Likelihood: 2 (unlikely to be material if accountability re-mapping
    is triggered by workflow change and periodically sampled)
  Detectability: 2 (detectable via periodic decision-trace sampling
    audit, ahead of any real incident)
  Recoverability: 3 (reversible via a re-mapping exercise once
    identified; days-to-weeks)
  Novelty: 3 (domain expert assumes SM&CR system-level ownership
    resolves the accountability question; the decision-level and
    multi-agent-specific gap is not standard governance-audit practice)

Residual risk interpretation: Acceptable with active re-mapping
triggers and periodic sampling; the practical risk driver is workflow
architecture evolving faster than governance documentation, a common
and largely unintentional drift.

If controls are absent or degraded:
  Severity: 3 (a genuine harm event elsewhere in the chain cannot be
    properly investigated, remediated or attributed, compounding
    reputational and regulatory consequence)
  Likelihood: 3 (probable given how routinely workflows are extended
    with additional automation steps without a corresponding
    governance re-mapping trigger)
  Detectability: 3 (typically only surfaces when an actual incident
    investigation stalls on the attribution question)
  Recoverability: 3 (multi-week remediation; SM&CR enforcement
    exposure if the gap is discovered during a regulatory
    investigation rather than proactively)
  Novelty: 4 (governance papers assert accountability exists with no
    decision-level or multi-agent-specific tracing evidence; the gap
    is invisible without today's specific sampling exercise)

Residual risk: High. Should be actively monitored given the routine
pace of workflow architecture change relative to governance
documentation update cycles.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Does not directly cause customer harm but materially impedes resolution, investigation and SM&CR discharge if harm occurs elsewhere |
| **Likelihood** | 3 | Probable given how routinely workflow architecture is extended without a corresponding accountability re-mapping trigger |
| **Detectability** | 2 | Detectable via periodic decision-trace sampling audit, ahead of any real incident, if the sampling programme is active |
| **Recoverability** | 3 | Reversible via a re-mapping exercise once identified, typically within weeks |
| **Novelty** | 3 | Domain expert assumes system-level SM&CR ownership resolves the accountability question; decision-level, multi-agent-specific tracing is not standard governance-audit practice |

## 17. Regulatory Basis
> [FCA/PRA, Senior Managers & Certification Regime] requires individual accountability for material business functions, which extends to AI-influenced decisions but was designed before widespread multi-agent AI workflows existed, creating an interpretive gap this canvas addresses. [FCA, Handbook SYSC 4.1.1R] requires robust governance arrangements generally, including control and safeguard arrangements for information processing systems. [FCA, Handbook SYSC 9, Record Keeping] requires records sufficient to reconstruct and attribute decisions. Section pinpoints on SM&CR application to multi-agent workflows specifically [UNVERIFIED — SM&CR, SYSC 4 and SYSC 9 confirmed extant (SYSC 19D removed 25 Aug 2026 — Remuneration Code, mis-cited; SYSC 4.1.1R substituted, Handbook-verified); no FCA/PRA text specifically addressing multi-agent AI workflow attribution has been published to cite] (verified 29 Jul 2026).

## 18. Research Basis
> [OWASP GenAI Security Project, "Agentic AI: Threats and Mitigations", Feb 2025] documents the "confused deputy" and diffuse-responsibility patterns in multi-agent systems relevant to this failure mode. [Vaccaro, K., Sandvig, C. & Karahalios, K., 2020, "'At the End of the Day Facebook Does What It Wants': How Users Experience Contesting Algorithmic Content Moderation", CSCW 2020] documents user experience of unattributable algorithmic decisions, illustrating the downstream contestability consequence of an accountability gap. Wells Fargo's 2016 cross-selling scandal (public regulatory settlement record, CFPB Consent Order, Sept 2016) is cited as a non-AI real-world analogue for diffuse organisational accountability across a delegated process, illustrating the consequence pattern this IRQ seeks to prevent in an AI context — cited for the accountability-diffusion pattern, not as an AI-specific precedent.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-GOV-001 (I.1 Inventory & Ownership: system-level accountable
    owner, the foundation this IRQ extends to decision level)
  - IRQ-AGT-007 (C.4 Multi-Agent Systems: per-action responsibility
    mapping in multi-agent orchestrations, feeding this IRQ's trace)
  - IRQ-HUM-008 (D.4 Accountability & Contestability: contest route
    depends on accountability being traceable in the first place)
  - IRQ-GOV-010 (I.4 Documentation, Records & Regulatory: record-
    keeping supporting decision reconstruction)
```

## 20. References
```
[1] OWASP GenAI Security Project, 2025. "Agentic AI: Threats and Mitigations."
    Published: February 2025
    URL: https://genai.owasp.org/

[2] Vaccaro, K., Sandvig, C. & Karahalios, K., 2020. "'At the End of the Day Facebook Does What It Wants': How Users Experience Contesting Algorithmic Content Moderation." Proceedings of the ACM on Human-Computer Interaction, CSCW 2020.
    Accessed: 2026-07-29

[3] Consumer Financial Protection Bureau, 2016. "Consent Order: Wells Fargo Bank, N.A." File No. 2016-CFPB-0015.
    Published: 2016-09-08
    URL: https://www.consumerfinance.gov/

[4] Financial Conduct Authority. "Handbook SYSC 4" and "Handbook SYSC 9."
    URL: https://www.handbook.fca.org.uk/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.4 (Human Oversight, Accountability & Contestability)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs treat system-level SM&CR ownership as sufficient; the decision-level accountability gap through delegated/multi-agent workflows is not standard governance-audit scope.
✓ Test 2 (Plausible Harm): Grounded in OWASP's documented confused-deputy/diffuse-responsibility pattern and the Wells Fargo accountability-diffusion analogue.
✓ Test 3 (Testable): Answerable via decision-trace sampling through the actual delegation chain, with a defined attributability scoring rubric.
✓ Test 4 (Decision-Relevant): Directly determines whether the firm can discharge SM&CR obligations and support complaint/regulatory investigation for AI-influenced decisions, gating workflow expansion.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — the Vaccaro et al. title given as the article's own first page gives it ("Does What It Wants"), in place of "Does What ItWants", the form in the publisher's landing-page and DOI metadata; reference [2] in field 20 already gave it so. Research-basis review date moved. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery typically within weeks, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. The other axes, the ★ rating and the research basis are unchanged.
```

---
---

