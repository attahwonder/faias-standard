# CANVAS: IRQ-GOV-013

## 1. IRQ ID & Title
**IRQ-GOV-013: Complaint-Led Remediation Blind to the Full Affected Cohort**

Register question: "Given a defined failure signature (model/configuration version, prompt or logic defect, affected date range), can the institution identify the *full* affected cohort of decisions — not only reconstruct the individual decision under complaint — and does a proactive remediation process exist to reach that cohort without waiting for a complaint to arrive?"

## 2. Business Activities Affected
- **Consequential decisioning processes subject to versioned model/prompt/logic changes:** lending, claims disposition, pricing, AML disposition — any process where a defective version, threshold or prompt affects every decision routed through it during the defect window, not just the one a customer happens to complain about.
- **Complaint handling and FOS-referral processes:** current remediation is triggered and scoped by the individual complaint; the cohort behind that complaint is not routinely identified or reached.
- **Regulatory redress and back-book review:** where a systemic defect is later confirmed (via audit, incident investigation or supervisory finding), the firm's capability to enumerate the full affected population determines whether remediation is comprehensive or partial.

## 3. AI Behaviour(s)
- Applies the same model/configuration/prompt version, and therefore the same defect (where one exists), uniformly across every decision routed through it during the affected window — the defect is not customer-specific, even though its downstream effect (a wrong decline, a wrong price, a wrong flag) lands on individual customers one at a time.
- Produces no self-signal that a given output was affected by a defect; the defect is discoverable only by knowing which version/configuration produced the output, not from the output itself.

## 4. Failure Mode
> The firm's remediation capability reconstructs and remediates the single decision a customer complained about (per IRQ-GOV-010), but has no capability — given a defined failure signature (model/configuration version, prompt or logic defect, affected date range) — to query for and identify the *full* cohort of decisions sharing that signature, so remediation is confined to the subset of the affected population that happened to complain.

## 5. Potential Consequences
- **Customer:** Every member of the affected cohort who did not complain — plausibly the majority, given well-documented complaint friction in financial services — receives no remediation despite having been wronged by the identical defect as the complainant who was made whole.
- **Institution:** Remediation cost and liability accrue cumulatively and are discovered piecemeal rather than resolved once; a later regulatory or audit discovery of the full cohort converts a manageable, proactive exercise into a large, reactive, reputationally damaging back-book remediation programme.
- **Regulator/market:** A finding that redress was structurally confined to complainants, while an institution could reasonably have determined the defect's full population, is the precise failure the Robodebt Royal Commission identified, and is squarely the kind of systemic-harm finding UK/FS regulators are increasingly alert to.

## 6. Failure Chain
```
Model, configuration, prompt or decisioning-logic defect is introduced (version
change, threshold mis-set, prompt regression) and deployed to production
  ↓ (IRQ-MOD-013: change control may not itself flag decision-relevant defects)
Defect applies uniformly to every decision routed through the affected
version/configuration during the affected date range
  ↓ (IRQ-GOV-010: retained records could support reconstruction, but only
  per-decision, not cohort-wide, unless specifically queried that way)
A subset of the affected cohort complains; the firm investigates and
reconstructs and remedies that individual decision only
  ↓ (IRQ-GOV-013 — THIS IRQ: no cohort-level query capability exists to find
  the rest of the affected population from the failure signature)
Remainder of the affected cohort — those who did not complain — receives no
remediation and no proactive contact
  ↓
Defect surfaces at scale via audit, incident investigation or supervisory
review → full cohort discovered reactively → back-book remediation programme
→ regulatory finding of complaint-confined redress → enforcement/reputational
damage

Control Breakpoints:
  • IRQ-MOD-013: change control flags decision-relevant version/config changes
  • IRQ-GOV-010: per-decision record reconstruction (necessary but not sufficient)
  • IRQ-GOV-013: cohort-level query capability, keyed to failure signature, with
    a proactive remediation trigger independent of inbound complaint
  • IRQ-HUM-008: contestability route gives complainants a channel, but does not
    substitute for proactive cohort identification
```

## 7. Why a Domain Expert May Miss It
- FS complaint-handling practice (DISP) is built around, and trains reviewers to think in terms of, the individual complaint as the unit of remediation; working backwards from a technical failure signature to an entire affected population is a manufacturing/product-recall concept, not a native FS complaints-handling one.
- Traditional model errors (a miscalibrated credit score) are usually caught through aggregate performance monitoring, which naturally surfaces a population; a single bad prompt version or a threshold mis-set in an LLM-based system can be far more surgical in its effect and much less visible in aggregate metrics, so the SME's usual "monitoring would have caught a cohort-wide issue" assumption does not transfer.
- "We can reconstruct any decision on request" (IRQ-GOV-010) is easily mistaken for "we can find everyone this happened to" — the two capabilities sound adjacent but require entirely different query architecture (per-decision key lookup versus signature-based cohort enumeration).
- Remediation programmes are typically resourced and triggered reactively, after a confirmed systemic issue; SMEs are not used to being asked whether the capability to proactively find a cohort exists at all, independent of whether an issue has yet been confirmed.

## 8. Assurance Objective
**AO-GOV-013:** Given a defined failure signature (model/configuration version, prompt or logic defect, affected date range), the firm shall be able to identify the full affected cohort of decisions and shall operate a proactive remediation process that reaches that cohort without depending on an inbound complaint.

## 9. Expected Controls (Traced)
- **Queryable decision store indexed by model/configuration/prompt version, defect signature and date range, capable of returning the full matching population, not only a named record** — [Emerging Practice] — no published protocol for this capability was identified; the control follows directly from the record-keeping foundation at IRQ-GOV-010 but extends it to cohort-level query, which is not itself a requirement of any cited standard.
- **Proactive remediation trigger, structurally independent of an inbound complaint, activated once a defect signature and affected cohort are identified** — [Royal Commission into the Robodebt Scheme, Report, Vol. 1, 7 July 2023] — the Commission's finding that the scheme "neither produced accurate results nor complied with" its governing statute is the direct evidentiary basis for requiring a remediation trigger that does not wait for the individual to come forward.
- **Named ownership for cohort-level remediation decisions, distinct from individual complaint-handling ownership** — [linked IRQ-HUM-008; IRQ-GOV-001 ownership principle extended to the cohort-remediation function].
- **Defined relationship to the complaint-handling framework: cohort-level identification treated as additional to, not a substitute for, the complaint-initiated route** — [FCA, DISP 1.1.3R, as at 31/07/2026] — DISP binds the firm once a complaint arrives from an eligible complainant; it does not itself require the firm to look for uncomplained members of an affected cohort, which is precisely the gap this control closes.
- **Rehearsal or exercise of the cohort-identification capability against a synthetic or historical defect signature, with time-to-identify-cohort measured** — [Emerging Practice] — no published protocol; included because an untested capability offers no more assurance than an untested disaster-recovery plan.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "any decision can be reconstructed on request" — **L1** (evidences per-decision capability only; does not evidence cohort-level query capability).
- Design documentation of the decision store's query capability, specifying which fields (version, configuration, prompt, defect signature, date range) can be queried and whether the query is complete-population or single-record — **L2**.
- Configuration/code review confirming the query capability is actually implemented and returns population-level results, not just a lookup by decision ID — **L3**.
- Rehearsal or exercise log: a synthetic or historical defect signature was supplied and the full matching cohort was enumerated, with completeness and time-to-identify recorded — **L3**.
- Governance record showing named ownership and a defined trigger for proactive remediation, independent of inbound complaint — **L2/L3**.
- Evidence from an actual historical instance where a defect was identified and the firm proactively remediated the full cohort without waiting for complaints from every member — **L5** (demonstrates the mechanism functions, not merely exists).

## 11. Independent Test
> The reviewer supplies a synthetic defect signature (a model/configuration version, a defined date range, and a stated logic or prompt defect) not previously used by the firm for this purpose. The firm is asked to demonstrate, in a test/staging environment, enumeration of the *full* cohort of decisions matching that signature — not retrieval of one named record — and to state the time taken and any manual steps required. The reviewer separately confirms whether a proactive remediation trigger exists that would act on this cohort without requiring an inbound complaint from any of its members, and reviews any rehearsal or historical exercise evidence. No published protocol exists for this test — stated plainly; the demonstration is a bespoke capability exercise, professional-judgement-led, conducted entirely in test/staging with no production data or live customer contact. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the underlying harm — complaint-confined redress leaving an affected cohort unremediated — is well evidenced by the Robodebt Royal Commission finding, but the test method itself is bespoke, with no published protocol, benchmark or established sampling frame for "cohort-identification completeness"; the assessment rests heavily on reviewer professional judgement).

## 12. Pass Indicators
- The firm enumerates the full synthetic cohort from the supplied failure signature within a reasonable, stated timeframe, without manual case-by-case investigation.
- A proactive remediation trigger exists and is evidenced to have activated at least once historically without waiting for a complaint.
- Named ownership for cohort-level remediation is distinct from, and does not default to, individual complaint-handling ownership.
- Query capability spans model/configuration/prompt version, logic defect and date range — not only a subset of these fields.
- The exercise log shows the capability has been rehearsed, not only designed.

## 13. Fail Indicators
- The firm can only reconstruct the individual decision supplied by the reviewer and has no mechanism to enumerate other decisions sharing the same signature.
- Cohort identification, where possible at all, requires extensive manual investigation with no defined query capability or measurable timeframe.
- No proactive remediation trigger exists; remediation is confirmed to occur only in response to an inbound complaint.
- The decision store cannot be queried by model/configuration/prompt version or defect signature — only by customer or decision identifier.
- No rehearsal or historical exercise evidence exists; the capability, if claimed, has never actually been tested.

## 14. Reporting Language
**Pass:** "Testing confirms the firm can enumerate the full cohort of decisions matching a supplied synthetic failure signature (model/configuration version, defect, date range) within [time], and that a proactive remediation trigger, independent of inbound complaint, exists and has activated at least once historically. Conclusions rest on ★2 methodology — a bespoke capability demonstration with no published protocol — and should be read as professional assessment, not benchmarked assurance."
**Fail:** "Testing found the firm could reconstruct only the single decision supplied, with no capability to enumerate other decisions sharing the same defect signature. Remediation is confined to inbound complaints; an unknown-sized cohort of similarly affected customers has received no remediation and no proactive contact. This is a material gap against the assurance objective and should be reported as a finding requiring remediation before reliance is placed on the firm's redress capability for cohort-scale defects."
**Partial:** "The firm can enumerate a cohort by model/configuration version but not by prompt or logic-defect signature specifically, and no proactive remediation trigger has been exercised, only designed. The assurance objective is not yet met; remediation should extend query capability to all signature fields and rehearse the proactive trigger within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (an unremediated cohort represents cumulative, multiplied customer
              harm beyond the single complainant; consistent with the scale of
              harm found in the Robodebt case)
  Likelihood: 2 (plausible where remediation capability was built complaint-first,
              as most FS complaint-handling architecture is; reduces materially
              where cohort-query capability has been deliberately built and
              rehearsed)
  Detectability: 3 (invisible until either a proactive exercise is run or a
              systemic issue is confirmed through audit/incident investigation;
              routine complaint volumes give no signal that a cohort exists)
  Recoverability: 2 (once identified, remediation can proceed, but the exposure
              window during which the cohort went unremediated cannot be undone,
              and interest/detriment accrues throughout it)
  Novelty: 4 (very likely to be missed by a domain expert: complaint-led redress
              is the FS default and the cohort-query capability this IRQ tests
              is not part of that default mental model at all)

Interpretation: acceptable residual risk where cohort-query capability is built,
rehearsed and proactively triggered; the principal concern is that, absent this
IRQ, a firm may reasonably believe DISP compliance and per-decision
reconstruction (IRQ-GOV-010) together constitute adequate redress capability,
when neither requires or provides cohort-level identification.

If controls are absent or degraded:
  Severity: 4 (systemic, multiplied customer harm across an entire unremediated
              cohort; directly analogous to the scale of harm identified in the
              Robodebt Royal Commission)
  Likelihood: 3 (foreseeable wherever a firm's redress architecture is built
              complaint-first, which is the FS norm, not the exception)
  Detectability: 4 (silent by construction — nothing in routine operation
              signals that an unremediated cohort exists until an external
              trigger, such as an audit or a regulatory investigation, forces
              discovery)
  Recoverability: 3 (remediable once discovered, but the accrued detriment and
              the reputational and regulatory consequence of a "complaint-only"
              redress finding are not reversible retrospectively)
  Novelty: 4
Residual risk: High if the capability is untested; this IRQ tests for exactly
the structural gap the Robodebt Royal Commission identified.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unremediated cohort represents cumulative, multiplied harm beyond the individual complainant, at the scale identified in the Robodebt Royal Commission finding. |
| **Likelihood** | 3 | Probable given that FS complaint-handling architecture is built complaint-first (DISP is complaint-initiated); cohort-query capability is not a natural by-product of that design. |
| **Detectability** | 4 | Silent by construction — no routine signal indicates an unremediated cohort exists; discovery typically requires an external trigger (audit, incident investigation, supervisory review). |
| **Recoverability** | 2 | Remediable once the cohort is identified, but accrued detriment during the unremediated window, and any reputational/regulatory consequence of a complaint-confined finding, cannot be undone retrospectively. |
| **Novelty** | 4 | Complaint-led redress is the FS default; proactive, signature-based cohort identification is a product-recall concept largely absent from FS complaint-handling mental models. |

## 17. Regulatory Basis
> [FCA, DISP 1.1.3R, as at 31/07/2026, DISP 1.1.3 last updated 17/03/2026] provides that the complaints chapter "(1) Subject to DISP 1.1.5R, … applies to a firm in respect of complaints from eligible complainants concerning activities carried on from an establishment maintained by it or its appointed representative" (DISP 1.1.5R being a carve-out list, none of whose limbs bears on this point) in the UK — a complaint-initiated framework that binds the firm once a complaint arrives, but does not itself require the firm to identify uncomplained members of an affected cohort; that capability gap is precisely what this IRQ tests. No UK or EU regulatory instrument imposing a proactive, signature-based cohort-identification duty specific to AI-influenced decisions was identified in the verified source set; this control area currently rests on the Robodebt Royal Commission's finding — an Australian public-inquiry precedent, not a UK/EU regulatory instrument — rather than a binding UK/EU rule, and this gap is stated openly rather than a regulatory anchor being invented.

## 18. Research Basis
> [Royal Commission into the Robodebt Scheme, Report, Vol. 1, 7 July 2023, p. v] found of the automated debt-recovery scheme that "[a]s used, it neither produced accurate results nor complied with the income calculation provisions of the Social Security Act 1991 (Cth)" — a public-inquiry finding evidencing, at scale, exactly this IRQ's failure mode: a defective automated decisioning process whose harm was confined to individual, complaint-shaped remediation until forced into systemic recognition. No peer-reviewed literature specifically quantifying cohort-level redress capability gaps in deployed AI decisioning systems was identified in the source registers; this control area is public-inquiry and audit-practice-led rather than research-led, consistent with the wider evidentiary profile of the Governance domain.
>
> **[FAIAS Incident Register, row 27, "Robodebt (Australia)", 2023]** — the Royal Commission finding set out above, cited here as the register entry that evidences this question: a defective automated decisioning process whose harm remained confined to individual, complaint-shaped remediation until it was forced into systemic recognition.
>
> **[FAIAS Incident Register, row 14, "UK Post Office Horizon scandal", 2025]**, citing [Williams, Sir Wyn (Chair), 2025, "Post Office Horizon IT Inquiry Report: Volume 1", HC 1119, presented to Parliament pursuant to section 26 of the Inquiries Act 2005, ordered to be printed 8 July 2025, §4.285] — a United Kingdom instance of the cohort-identification gap, beside the Australian instance above. The Inquiry recorded at §4.285 that a parliamentary committee's major concern was "the evidence which suggested that there were difficulties in identifying and notifying individuals that their convictions had been quashed", and that the committee "considered itself hampered by a lack of data surrounding this issue". It is cited as an automation analogue; the transferable element is an institution's inability to enumerate the population a known defect affected, and not the technique that produced the defect.
>
> **[FAIAS Incident Register, row 13, "Dutch childcare benefits scandal (toeslagenaffaire)", 2021]**, citing [Amnesty International, 2021, "Xenophobic Machines: Discrimination through unregulated use of algorithms in the Dutch childcare benefits scandal", Index EUR 35/4686/2021, October 2021] — a second public-sector instance in which a risk-classification model was one component of a fraud-enforcement practice that affected a large population and was recognised systemically only long afterwards. The report records that "tens of thousands of parents, caregivers and children have been affected by the scandal", and that "[y]ears later, long after the harms had been inflicted, a parliamentary investigation committee was appointed by the Dutch parliament in July 2020" — not through the individual complaints affected families had already brought. It supports this question only in part, and the limit is stated: it is a non-governmental organisation's report on a public-sector scheme rather than a judicial or supervisory finding, it does not itself analyse cohort-enumeration capability, and it is cited for the shape of the remediation failure, the population figure being the report's, which draws it from parliamentary documents and media reporting.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-010 (I.4: retained records — necessary precondition for cohort
    query, but per-decision reconstruction alone does not provide cohort
    enumeration)
  - IRQ-HUM-008 (D.4: contestability — gives an individual complainant a route,
    but is not a substitute for proactive cohort identification)
  - IRQ-GOV-009 (I.4: documentation adequacy — a related but distinct artefact
    set; this IRQ concerns query capability over decision records, not system
    description)
  - IRQ-MOD-013 (B.6: change control — the point at which a defect-introducing
    version/configuration change should ideally have been flagged upstream)
```

## 20. References
```
[1] Royal Commission into the Robodebt Scheme, 2023. "Report." Vol. 1.
    Published 7 July 2023. p. v.
[2] Financial Conduct Authority. "DISP 1.1 — Purpose, Interpretation and
    Application." FCA Handbook, as at 31/07/2026 (DISP 1.1.3 last updated
    17/03/2026).
[3] Williams, Sir Wyn (Chair), 2025. "Post Office Horizon IT Inquiry Report:
    Volume 1." HC 1119. Ordered by the House of Commons to be printed
    8 July 2025.
[4] Amnesty International, 2021. "Xenophobic Machines: Discrimination through
    unregulated use of algorithms in the Dutch childcare benefits scandal."
    Index EUR 35/4686/2021. October 2021.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): FS complaint-handling practice is built around, and
  trains reviewers to think in terms of, the individual complaint as the unit
  of remediation; working backwards from a failure signature to an entire
  affected population is a product-recall concept, not a native FS
  complaints-handling one.
✓ Test 2 (Plausible Harm): Grounded in the Robodebt Royal Commission's finding
  (Vol. 1, 7 Jul 2023, p. v) that an automated decisioning scheme "neither
  produced accurate results nor complied with" its governing statute — the
  clearest available precedent for scaled, complaint-confined redress harm.
✓ Test 3 (Testable): Testable via a supplied synthetic failure signature and a
  test/staging cohort-enumeration demonstration, timed and scored for
  completeness. ★2 methodology, honestly caveated — no published protocol
  exists.
✓ Test 4 (Decision-Relevant): Outcome bears on the authorisation conditions for
  any consequential-decision system — a firm unable to identify its own
  affected cohorts cannot be relied upon to remediate systemic AI defects.

Change Log:
- v1.0 (2026-07-31): Initial publication; all four tests passed.
- v1.2.1 (2026-09-19): Field 18 — incident-register citations added in the reserved form (row 27, Robodebt, for the entry already described in this field; row 14, UK Post Office Horizon scandal, as a United Kingdom instance of the cohort-identification gap; row 13, Dutch childcare benefits scandal, in part and with its limits stated). Field 20 — entries [3] and [4] added for the Inquiry report and the Amnesty International report. Research-basis review date moved. No change to controls, test, ★2 or risk profile.
```

---
---

