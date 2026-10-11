# CANVAS: IRQ-GOV-012

## 1. IRQ ID & Title
**IRQ-GOV-012: Effective Operating Envelope Has Drifted from the Approved Envelope Without Re-Assurance**

Register question: "Has the system's effective operating envelope drifted from its approved envelope — through changes in intended use, user behaviour, prompts, tools, integrations, or the surrounding business process — while the model itself remained unchanged?"

## 2. Business Activities Affected
- **Every AI system approved against a stated, bounded operating envelope:** lending triage tools quietly becoming lending decision tools; customer-service assistants originally scoped to FAQ answering being asked to draft binding commitments; AML investigation copilots originally scoped to English-language, domestic typologies being applied to cross-border, multilingual cases without re-validation.
- **Agentic and tool-integrated systems specifically:** integration drift (a standalone triage tool wired into downstream pricing or payment systems after go-live) and tool/permission expansion are the highest-velocity envelope-drift vectors, because they can occur through a single engineering change with no formal governance touchpoint.
- **Any deployment where business teams control prompts or configuration:** prompt drift ("be more permissive," "handle vulnerable customers directly") can silently expand the effective envelope with no code change and, absent controls, no governance visibility at all.

## 3. AI Behaviour(s)
- N/A directly at the model-behaviour level — the model itself is, by the terms of this IRQ, unchanged; what changes is the *use* made of it: the tasks assigned, the users granted access, the prompts issued, the tools connected, and the business process surrounding its output. The system faithfully executes whatever it is asked to do within its technical capability, which is precisely why expanding what it is asked to do is invisible to any model-level control.

## 4. Failure Mode
> The system's effective, in-practice operating envelope — defined by actual intended use, user population, prompt content, connected tools/integrations, and surrounding business process — has expanded beyond the envelope explicitly approved at deployment, without triggering re-assurance, even though the model's own weights and version remain unchanged. Because assurance evidence (validation, testing, risk appetite sign-off) was obtained for the *approved* envelope, none of it demonstrably applies to the *actual* one, and no single control owner is positioned to notice the divergence because each individual change (a prompt edit, a new integration, a shift in who uses the tool) can look locally reasonable.

## 5. Potential Consequences
- **Customer:** A system validated as a low-risk "triage tool with 10% human escalation" that has drifted, through incremental process change, into a de facto "decision tool with rubber-stamp review" exposes customers to decisions made with a level of AI autonomy that was never actually tested or approved — the harm is not a new model failure, but an old, untested risk surface now bearing real weight.
- **Institution:** The firm's approval paper, safety case and risk appetite sign-off for the system are no longer an accurate description of what is actually happening; in the event of an incident, "we tested and approved this" is not a valid defence because what was tested is not what occurred — this is a fundamental integrity failure of the assurance record itself.
- **Regulator/market:** Regulators increasingly expect firms to demonstrate that approved scope and actual use remain reconciled over time (EU AI Act Art. 9's continuous risk-management-system requirement, PRA SS1/23's ongoing-monitoring principle); an envelope-drift finding is a governance-integrity failure distinct from — and often a root cause behind — any specific technical or customer-harm finding.

## 6. Failure Chain
```
System approved against an explicit, documented operating envelope (designed-for
scope: task type, user group, customer segment, tools, language, escalation rate)
  ↓ (IRQ-GOV-003: approved conditions of use are the baseline this IRQ reconciles
  actual use against)
One or more drift vectors occurs incrementally, each individually unremarkable:
  • Business process drift — "triage" quietly becomes "decision" as escalation
    review becomes a rubber stamp (IRQ-HUM-002: approval theatre)
  • Prompt drift — business users edit system prompts toward permissiveness with
    no re-test (IRQ-MOD-013: prompt change control)
  • Tool/integration drift — the system is wired into downstream pricing, payment
    or approval systems post-go-live, so its outputs now cascade into irreversible
    actions never contemplated at approval (IRQ-AGT-010: workflow reconciliation)
  • Customer-segment drift — the model, validated on prime retail, is applied to
    self-employed or international applicants outside its tested population
    (IRQ-MOD-001: capability envelope)
  • Capability drift (silent) — a vendor-side model update expands capability
    without the firm's knowledge (IRQ-TPR-004: vendor change detection)
  ↓ (IRQ-GOV-012 — THIS IRQ: no periodic reconciliation of effective use against
  approved envelope exists, or exists but does not trigger re-approval)
None of the original assurance evidence (validation, testing, risk appetite
sign-off) covers the now-actual envelope; the safety case is stale
  ↓ (IRQ-GOV-008: even if a monitoring signal exists somewhere for one drift
  vector, it may not reach governance with envelope-drift framing)
System operates, unremediated, under conditions materially different from those
its assurance evidence was ever obtained for
  ↓
A failure mode never tested for the actual envelope materialises (e.g. hallucination
rate untested for the self-employed segment; irreversible downstream action never
gated because integration was never assessed) → customer harm → post-incident
review discovers the approved envelope had silently drifted months or years earlier
→ finding that governance failed to detect its own approval basis had become false

Control Breakpoints:
  • IRQ-GOV-003: technically enforced, monitored conditions of use as the baseline
    envelope statement
  • IRQ-GOV-012: periodic, structured reconciliation of effective use against
    approved envelope, with defined drift triggers for mandatory re-approval
  • IRQ-MOD-001/-002: capability-envelope testing and re-approval on capability delta
  • IRQ-AGT-010: per-execution workflow reconciliation feeding this IRQ's
    population-level drift assessment
  • IRQ-MOD-013: prompt/config version control as the primary defence against
    silent prompt drift
```

## 7. Why a Domain Expert May Miss It
- Traditional model risk management validates a model *once* against a *static* specification; the idea that the thing requiring ongoing assurance is not the model but the evolving *relationship* between the model and an ever-changing business process, user population and toolset is foreign to that mental model — SMEs look for "has the model changed?" and, finding it unchanged, conclude no re-assurance is needed.
- Each individual drift vector, examined in isolation by the function that owns it, looks like an ordinary, low-risk operational change: a prompt tweak is a copy-editing task to the business user who makes it; a new downstream integration is a standard engineering change to the platform team; a shift in who reviews escalations is an ordinary staffing decision to the operations manager. No single function sees the *cumulative* divergence from the approved envelope, because no single function is tasked with looking at the envelope as a whole.
- The system's technical behaviour genuinely has not changed — the model output for a given input is the same as it was at approval — so any control that only asks "does the model still perform as tested" (a legitimate, necessary, but insufficient question) will pass, giving false reassurance that nothing requiring attention has occurred.
- Approval papers and safety cases are typically read once, at go-live, and rarely revisited as a living reconciliation target; without a deliberate mechanism to compare *today's* actual use against *that document*, drift is structurally invisible until an incident forces the comparison retrospectively.

## 8. Assurance Objective
**AO-GOV-012:** The system's effective, in-practice operating envelope — intended use, user population, prompt content, connected tools/integrations, and surrounding business process — shall be periodically and structurally reconciled against its approved operating envelope, with any material divergence (drift) triggering mandatory re-approval or re-assurance before the drifted use continues, regardless of whether the underlying model itself has changed.

## 9. Expected Controls (Traced)
- **Explicit, documented Operating Envelope Declaration at approval — a yes-list/no-list of designed-for and not-designed-for scope (customer segments, languages, products, use case, escalation rate, stress scenarios) that serves as the reconciliation baseline** — [ASSURANCE_ARCHITECTURE.md, Layer 4, AI Safety Case, "Operating Envelope Declaration"] — the FAIAS-native anchor for this control, itself grounded in the same safety-case discipline (ARP 4761; IEC 61508; ISO/IEC 15026-2) used in aviation and functional-safety domains for explicit, bounded scope-of-safety-claim declarations.
- **Periodic, structured reconciliation of effective use (actual task types, actual user population, current prompt/system-instruction content, current tool/integration map, current business-process description) against the approved envelope, at a defined cadence and on defined triggers (major change, incident, periodic review)** — [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023), ongoing monitoring and periodic review principle, extended per ASSURANCE_ARCHITECTURE.md's Periodic Assurance Phase] — the direct AI-neutral MRM anchor for "does the model still operate as validated," extended here to the AI-specific question of whether *use* still matches the *validated* use.
- **Defined drift triggers mapped to specific vectors — business-process change, prompt/config change (linked IRQ-MOD-013), new tool/integration (linked IRQ-AGT-010), customer-segment expansion (linked IRQ-MOD-001), vendor-side silent capability change (linked IRQ-TPR-004) — each requiring mandatory re-approval before the drifted use continues** — [EU AI Act, Regulation (EU) 2024/1689, Art. 9 — continuous, iterative risk management system requiring the risk-management process to be regularly reviewed and updated throughout the lifecycle] — the clearest binding regulatory anchor requiring lifecycle-continuous (not point-in-time) risk management for in-scope high-risk systems, directly supporting a mandatory re-trigger requirement rather than a discretionary one.
- **Technical enforcement (not policy-only) of the approved envelope's boundaries where feasible — e.g. platform-level restriction of user groups, task types or connected tools to those approved, per IRQ-GOV-003 — reducing the population of drift vectors that depend on human process discipline alone** — [linked IRQ-GOV-003; NIST AI 100-1, Jan 2023, GOVERN function] — narrows the surface this IRQ must monitor by preventing some drift vectors architecturally rather than only detecting them after the fact.
- **Named, empowered accountability for the reconciliation exercise and authority to require re-approval or suspend drifted use, distinct from (and escalating from) individual function owners who each control only one drift vector** — [linked IRQ-GOV-001, IRQ-HUM-005; ASSURANCE_ARCHITECTURE.md, Layer 2, Mandatory Completeness Rule] — closes the "no single function sees the cumulative picture" blind spot identified in field 7.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the system operates as approved" with no supporting reconciliation exercise — **L1** (near-worthless; this IRQ exists precisely because this assertion is what governance defaults to absent a structured check).
- Operating Envelope Declaration document (yes-list/no-list) produced at approval and version-controlled — **L2**.
- Reconciliation methodology and cadence documentation specifying what "effective use" evidence is gathered (actual task logs, actual user access logs, current prompt/system-instruction text, current integration map) and how it is compared against the declaration — **L2**.
- A completed reconciliation exercise for a specific system, with the actual-use evidence gathered and each drift vector explicitly assessed against the declaration, dated and retained — **L3**.
- Staging/configuration test attempting to exercise the system slightly outside its declared envelope (an out-of-scope task type, an unapproved user role, a downstream integration attempt) to test whether technical controls, not policy alone, resist the attempt — **L3**.
- Internal audit or independent review of the reconciliation control's design and operating effectiveness across a sample of systems, including whether any re-approval was actually triggered where drift was found — **L4**.
- Production evidence (last 12 months): actual task-type distribution, actual user access logs, prompt/config version history, and integration change log for a specific system, independently compared against its declared envelope, with any identified divergence and the governance action (or inaction) taken in response — **L5**.

## 11. Independent Test
> For a risk-based sample of approved AI systems, obtain the system's Operating Envelope Declaration (designed-for/not-designed-for scope) as recorded at approval. Independently gather current-state evidence across each drift vector: (1) a sample of actual production task/query logs, classified against the declared task-type scope; (2) current user-access records, checked against the declared user population; (3) the current system prompt/instruction text, diffed against the version in force at approval; (4) the current tool/integration map, checked for any connection not present at approval; (5) a structured interview with the business process owner on whether the surrounding human-review process (e.g. escalation review substance) still matches the process described at approval. For each drift vector, classify the finding as no drift, drift within tolerance (documented and approved), or undocumented drift. Separately, attempt in a staging replica to exercise the system slightly outside one declared boundary (e.g. submit an out-of-declared-scope task type, or attempt access as a non-approved user role) to test whether technical controls, not policy statement alone, resist the attempt. Cross-reference any undocumented drift found against whether a corresponding re-approval or re-assurance record exists. Methodology follows standard configuration/process-audit reconciliation practice (as-approved vs as-operating comparison, drawing on internal-audit walkthrough and sampling techniques and IT change-management drift-detection practice), extended to the AI-specific envelope-drift vector taxonomy defined in ASSURANCE_ARCHITECTURE.md Layer 4 (business-process, user-behaviour, tool/integration, prompt, customer-segment, and silent capability drift), for which no AI-specific benchmark or standardised detection methodology yet exists. Conducted against logs, configuration records, version-control history and interviews in a non-production/staging environment for the boundary-exercise component; no live production system access required for the reconciliation component beyond retrieving historical logs. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P1 (§6A.4)** (the underlying reconciliation technique — as-approved vs as-operating comparison — is established, credible audit practice, but the specific six-vector envelope-drift taxonomy this test is built around is FAIAS/ASSURANCE_ARCHITECTURE-native rather than an externally published, benchmarked methodology; no cross-institution consensus exists yet on what constitutes a complete drift-vector checklist or an acceptable drift-detection sampling frame, so test design and the materiality threshold for "undocumented drift" rest heavily on reviewer professional judgement — this is stated honestly rather than inflated, consistent with this being an assurance-architecture-native rather than externally standardised test).

## 12. Pass Indicators
- Actual task/query distribution for the sampled systems falls entirely within the declared task-type scope, with any exceptions documented and separately re-approved.
- Current user-access records match the declared user population; no access group exists in production that was not in the approved declaration.
- Current system-prompt text matches the version in force at approval, or any change is version-controlled with an accompanying re-test record.
- No tool/integration exists in production that was not present, or explicitly approved as an addition with re-assessment, at the time of original approval.
- The staging boundary-exercise attempt is technically resisted (not merely discouraged by policy) for at least the tested boundary.
- Where any drift is found, a corresponding re-approval or re-assurance record exists, dated at or before the drift's introduction.

## 13. Fail Indicators
- Production task/query logs show a material proportion of activity outside the declared task-type scope, with no corresponding re-approval record (the clearest and most common finding: "triage" tool functioning as a "decision" tool).
- Current system-prompt text differs materially from the approved-at-go-live version with no version-control trail and no re-test evidence.
- A downstream integration or tool connection exists in production that was not present or contemplated at approval, and no re-assessment of the consequent risk (e.g. irreversible downstream action) has occurred.
- The staging boundary-exercise attempt succeeds — the system accepts an out-of-declared-scope task or an unapproved user role with no technical resistance, confirming envelope boundaries exist only in policy documentation.
- Business-process-owner interview reveals the surrounding human-review process has materially changed (e.g. escalation review has become nominal) since approval, with no corresponding reassessment of the system's effective autonomy.

## 14. Reporting Language
**Pass:** "Reconciliation of effective use against the approved Operating Envelope Declaration for [n] sampled systems found no undocumented drift across the tested vectors (task scope, user population, prompt content, tool/integration map, surrounding process); the staging boundary-exercise confirmed technical, not merely policy-based, enforcement of at least the tested boundary. Conclusions rest on ★2 methodology — a FAIAS/ASSURANCE_ARCHITECTURE-native drift-vector taxonomy applied via established audit-reconciliation technique, with no external benchmark for envelope-drift detection — and should be read as professional assessment, re-performed at the next periodic review or major-change trigger."
**Fail:** "Reconciliation testing found that [system] is now operating materially outside its approved Operating Envelope Declaration: [specific finding, e.g. the escalation-review process approved at 10% human sign-off now functions as a rubric-only pass-through; the system has been integrated into a downstream pricing engine never assessed at approval]. No re-approval or re-assurance record exists for this drift. Because the original validation evidence, testing and risk-appetite sign-off were obtained against the approved envelope, none of that assurance basis demonstrably covers the system's actual current operation. This is a governance-integrity failure independent of whether the underlying model itself has changed, and should trigger immediate re-assurance before further reliance is placed on the existing approval."
**Partial:** "Reconciliation confirms task scope, user population and tool/integration map remain within the approved envelope, but the current system-prompt text has diverged from the approved-at-go-live version with no version-control trail identified, preventing confirmation that prompt-level drift has not occurred. The assurance objective is not yet met for the prompt-drift vector specifically; remediation should establish prompt version control and confirm or remediate drift within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (drift converts a system whose assurance basis was calibrated to a
              bounded, tested envelope into one operating, untested, against an
              expanded envelope; realised severity depends on the specific drift
              vector but commonly involves reduced human oversight or expanded
              customer-segment exposure, both individually rated 3-4 in their own
              home domains)
  Likelihood: 3 (foreseeable and, per ASSURANCE_ARCHITECTURE.md's own six named
              drift vectors, probable over any extended deployment lifetime absent
              structured periodic reconciliation — prompt and business-process drift
              in particular require no formal change-control trigger at all, and
              therefore occur by default rather than by exception)
  Detectability: 4 (structurally invisible to any control that only asks "has the
              model changed" — precisely the question most existing MRM/governance
              processes already ask — because the model, by this IRQ's own
              definition, has not; only a dedicated envelope-reconciliation exercise
              surfaces it)
  Recoverability: 2 (once identified, re-approval or restriction of the drifted use
              is a governance-process action achievable within a defined period, but
              any customer decisions made during the undetected-drift window under
              an effectively untested envelope cannot be retrospectively re-assured)
  Novelty: 4 (this is precisely the risk the Novelty axis anchors describe at its
              highest level: emergent, outside the traditional banking risk model,
              and very likely to be missed by a domain expert whose entire mental
              model of "has this system changed" is keyed to model version, not to
              the surrounding use pattern — this is also why ASSURANCE_ARCHITECTURE.md
              names envelope drift as a distinct, structural concept rather than
              folding it into ordinary change management)

Interpretation: this is the flagship governance risk in the FAIAS domain set —
high severity, foreseeable likelihood absent structural controls, and the single
worst detectability profile of any GOV IRQ, because the standard question every
other governance and MRM control asks ("has the model changed?") returns a
reassuring "no" even while the actual risk picture has moved substantially.
Structured periodic reconciliation against an explicit Operating Envelope
Declaration is not an optional refinement; it is the only control that asks the
right question.

If controls are absent or degraded:
  Severity: 4 (systemic: envelope drift is rarely a single-system event — the same
              organisational pressures, e.g. "let's use the triage tool for
              decisions too, it's working well," recur across a deployment estate;
              undetected, compounding drift across multiple systems is plausible
              and can produce widespread customer harm operating under an
              assurance basis that no longer describes reality)
  Likelihood: 4 (near-certain over any multi-year deployment lifetime with no
              structural reconciliation mechanism, given prompt and business-process
              drift require no formal trigger to occur)
  Detectability: 4 (silent by construction; discovered only via a dedicated
              reconciliation exercise or, worse, via a post-incident investigation
              that asks "wait, is this what we actually approved?")
  Recoverability: 3 (the drift itself is correctable through re-approval, but the
              specific decisions and outcomes produced during the undetected-drift
              period, potentially spanning years, cannot be retrospectively
              re-assured or, in many cases, even fully reconstructed for remediation)
  Novelty: 4
Residual risk: Critical if no structural reconciliation mechanism exists. This IRQ
should be treated as a standing deployment-gate condition (periodic reconciliation
cadence defined and evidenced) for any system with a multi-year expected lifetime,
consistent with ASSURANCE_ARCHITECTURE.md's Periodic Assurance and Major Change
Review phases.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Drift converts a system with a bounded, tested assurance basis into one operating, untested, against an expanded envelope; realised harm is commonly reduced human oversight or expanded customer-segment exposure, each individually severe. |
| **Likelihood** | 3 | Foreseeable and probable over any extended deployment lifetime absent structural reconciliation; prompt and business-process drift require no formal change-control trigger and so occur by default. |
| **Detectability** | 4 | Invisible to any control that only asks "has the model changed" — the question most existing MRM processes already ask — because by this IRQ's own definition the model has not changed; only a dedicated reconciliation exercise surfaces it. |
| **Recoverability** | 2 | Re-approval or restriction is achievable once identified, but decisions made during the undetected-drift window under an effectively untested envelope cannot be retrospectively re-assured. |
| **Novelty** | 4 | The archetypal AI-native governance blind spot: outside the traditional banking risk model, emergent, and very likely to be missed by a domain expert whose "has this changed" instinct is keyed to model version rather than surrounding use pattern. |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Art. 9] requires a continuous, iterative risk-management system, regularly reviewed and updated throughout the AI system's lifecycle — the clearest binding requirement that risk management (and, by extension, the scope it was performed against) cannot be a point-in-time exercise, directly supporting a mandatory re-trigger requirement for envelope drift in Annex III high-risk systems. [PRA, SS1/23, April 2026 (16 April 2026, updating 17 May 2023)] ongoing monitoring and periodic review principle requires firms to confirm models continue to perform and be used as validated, extended here to the AI-specific question of whether *use* still matches *validated use*, not only whether the model's technical performance is stable. [Bank of England and PRA, "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI," 22 April 2024] notes that SS1/23 includes expectations for dynamic models (models able to adapt, recalibrate or otherwise change autonomously in response to new inputs) and that, given the evolution of use cases, the Bank and the PRA will keep their approach under continuous review; the PRA's Oct 2025 MRM AI/ML roundtable signals increasing supervisory attention to how AI use evolves post-approval. No UK/FS regulation names "operating envelope drift" as a defined term; this IRQ's framing is FAIAS's own structural contribution (per ASSURANCE_ARCHITECTURE.md, Layer 4), built on the continuous-risk-management obligations cited above. Section pinpoints [UNVERIFIED — cited modules/articles confirmed extant (PRA SS1/23, SS1/21, PS21/3, ISO/IEC 42001:2023, EU AI Act Arts. 9/11/12/19); no AI-specific sub-clause pinpoint published by the regulator beyond module/clause level cited] (verified 29 Jul 2026).

## 18. Research Basis
> The envelope-drift concept and its named drift vectors (business-process, user-behaviour, tool/integration, prompt, customer-segment, silent capability drift) are drawn directly from ASSURANCE_ARCHITECTURE.md's Layer 4 AI Safety Case framework, itself grounded in the safety-case discipline of aviation and functional-safety standards [ARP 4761, SAE International; IEC 61508; ISO/IEC 15026-2, Systems and Software Assurance — Assurance Case] where an explicit, bounded "operating envelope" or "operational design domain" and its drift are long-established structural concepts (the closest direct analogue being the automated-driving-systems Operational Design Domain concept in UL 4600 and ISO 34503). No FS-specific academic literature yet quantifies AI operating-envelope drift as a distinct empirical phenomenon; this is consistent with the concept's status as an emerging, cross-domain-transferred safety-engineering construct rather than a benchmarked AI-safety research finding, and is stated honestly as such (★2, not ★3+, for the Independent Test above).
>
> **[FAIAS Incident Register, row 69, "State v. Loomis COMPAS", 2016]** — the Wisconsin Supreme Court records that "COMPAS was not developed for use at sentencing, but was intended for use by the Department of Corrections in making determinations regarding treatment, supervision, and parole" (para 100), and that "no cross-validation study for a Wisconsin population has yet been completed". A tool built for one use was considered for another, and the record carried no validation for the population concerned; the Court allowed that use only with a written advisement of these limitations. The setting is criminal sentencing, not financial services.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-003 (I.2: technically enforced conditions of use — the approved-envelope
    baseline this IRQ's reconciliation is performed against)
  - IRQ-MOD-001 (B.1: capability envelope testing — the model-capability-boundary
    dimension of drift; distinguished from this IRQ's population-level use-profile
    drift per TAXONOMY.md ruling 14)
  - IRQ-AGT-010 (C.7: per-execution workflow reconciliation — supplies the
    within-run divergence signal that, aggregated over time, feeds this IRQ's
    population-level drift assessment; distinguished per TAXONOMY.md ruling 14)
  - IRQ-MOD-013 (B.6: prompt/config version control — the primary technical defence
    against the prompt-drift vector)
  - IRQ-TPR-004 (F.2: vendor model-change detection — the primary defence against
    the silent capability-drift vector)
  - IRQ-HUM-002 (D.1: approval-theatre detection — the mechanism by which
    business-process drift, specifically escalation review becoming nominal, is
    independently evidenced)
  - IRQ-GOV-008 (I.3: monitoring signals reaching governance — envelope-drift
    findings depend on this IRQ's escalation route to actually trigger re-approval)
```

## 20. References
```
[1] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L 12.7.2024. Art. 9, Risk Management System.
[2] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023), effective 17 May 2024.
[3] Bank of England/PRA, 2024. "The Bank and the PRA's response to DSIT/HMT: update on our approach to AI." 22 April 2024.
[4] Bank of England/PRA, 2025. "The PRA holds model risk management roundtable on artificial
    intelligence and machine learning technologies." Published November 2025.
[5] SAE International, 2010. "ARP 4761 — Guidelines and Methods for Conducting the Safety
    Assessment Process on Civil Airborne Systems and Equipment."
[6] IEC, 2010. "IEC 61508 — Functional Safety of Electrical/Electronic/Programmable
    Electronic Safety-Related Systems."
[7] ISO/IEC, 2011. "ISO/IEC 15026-2 — Systems and Software Assurance — Part 2: Assurance
    Case."
[8] Underwriters Laboratories, 2023. "UL 4600 — Standard for Evaluation of Autonomous
    Products," Edition 3, 17 March 2023. (Operational Design Domain concept, cited as
    cross-domain analogue.)
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.2 (Governance domain, Approval, Tiering & Policy) — Flagship IRQ
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): The archetypal blind spot this IRQ exists to close: every
  traditional model-governance instinct asks "has the model changed?", and envelope drift
  by definition occurs while the answer remains "no" — the model is unchanged; only the use
  made of it has expanded, invisibly to that question.
✓ Test 2 (Plausible Harm): Grounded in ASSURANCE_ARCHITECTURE.md's Layer 4 Safety Case
  concept (Operating Envelope Declaration, Envelope Drift as Named Concept) and the EU AI
  Act Art. 9 continuous risk-management obligation; harm scenarios (triage-to-decision
  drift, silent tool integration, prompt permissiveness creep) are drawn directly from the
  named drift vectors in that framework.
✓ Test 3 (Testable): Testable via structured reconciliation of current-state evidence
  (task logs, access logs, prompt version diff, integration map, process-owner interview)
  against the approved Operating Envelope Declaration, plus a staging boundary-exercise
  test of technical enforcement. ★2 Confidence — honestly rated: the reconciliation
  technique is established audit practice, but the six-vector drift taxonomy is
  FAIAS-native with no external benchmark, and this is stated rather than inflated.
✓ Test 4 (Decision-Relevant): Directly gates whether the firm's existing approval, safety
  case and risk-appetite sign-off can still be relied upon at all — a "yes" finding on drift
  invalidates reliance on every other IRQ's assurance conclusions for the affected system
  until re-assurance occurs. This is the flagship IRQ of the Governance domain.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed as the domain's flagship IRQ.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20, reference [8] — UL 4600 takes the title of its current edition, "Standard for Evaluation of Autonomous Products" (Edition 3, 17 March 2023). Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20, reference [4] — the PRA roundtable page is cited by its heading as published, "The PRA holds model risk management roundtable on artificial intelligence and machine learning technologies". Form corrections only. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 69, State v. Loomis, in a criminal sentencing setting). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Fields 9 and 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Field 17 Regulatory Basis — the Bank of England and PRA letter of 22 April 2024 cited by its title, The Bank and the PRA's response to DSIT/HMT: update on our approach to AI; the letter's part of the post-approval sentence narrowed to what the letter says (SS1/23 expectations for dynamic models; the approach kept under continuous review as use cases evolve); the roundtable part unchanged. Field 20 References — the same title. No change to controls, test, ★ rating or risk profile.
- v1.3.3 (2026-10-09): Field 20 References — reference [4], the PRA roundtable page: its description corrected to a page published in November 2025, since the page reports two roundtable sessions and links the presentation slides. No change to the ★ rating or the risk profile.
```

---
---

