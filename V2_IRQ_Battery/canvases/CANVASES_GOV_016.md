# CANVAS: IRQ-GOV-016

## 1. IRQ ID & Title
**IRQ-GOV-016: AI Output Entering Risk-Data Aggregation and Regulatory Reporting Without BCBS 239 Discipline**

Register question: "Where AI-generated or AI-assisted output feeds the firm's risk-data aggregation estate, capital or provisioning calculations, or supervisory/regulatory returns, is that output subject to the same accuracy, completeness, timeliness, adaptability and traceability discipline the firm applies to its risk data under BCBS 239 — and is the AI origin of any contributing output flagged and reconstructable within the aggregation record?"

## 2. Business Activities Affected
- **Risk-data aggregation and reporting processes** feeding capital and provisioning calculations, where AI systems increasingly assist in producing, summarising or reconciling contributing content.
- **Supervisory and regulatory returns** compiled in part from AI-generated or AI-assisted narrative, summarisation or reconciliation content.
- **Internal risk reporting to governance bodies**, where AI-assisted content is not currently distinguishable from system-sourced data within the aggregation record.

## 3. AI Behaviour(s)
- Generates or assists in producing narrative risk commentary, exposure summarisation, or reconciliation of source-system data that feeds into the risk-data aggregation estate.
- Produces content that is not inherently distinguishable, once entered into the aggregation record, from data pulled directly from a source system.

## 4. Failure Mode
> AI-generated or AI-assisted content enters the firm's risk-data aggregation estate, capital or provisioning calculations, or supervisory/regulatory returns without being subject to the same accuracy, completeness, timeliness, adaptability and traceability discipline applied to other risk data, and without being flagged as AI-originated, so its accuracy is assumed rather than controlled and its contribution is not reconstructable within the aggregation record.

## 5. Potential Consequences
- **Institution:** capital, provisioning or regulatory-return figures rest in part on unflagged AI-originated content whose accuracy has not been controlled to the same standard as the rest of the risk-data estate, creating a data-integrity exposure inside a regulator-mandated framework.
- **Regulator/market:** a supervisory finding that risk-data aggregation and reporting has not extended its own established data-quality discipline to AI-originated contributions invites broader scrutiny of the firm's risk-reporting integrity.
- **Market (indirect):** capital and provisioning figures that do not reliably reflect underlying risk undermine the prudential purpose the aggregation framework exists to serve.

## 6. Failure Chain
```
Generative or agentic AI is used to produce narrative risk commentary,
summarise exposures, or reconcile source-system data feeding the risk-data
aggregation estate
  ↓ (existing data-domain controls govern data flowing into models, not model
  output flowing into risk reporting — a different direction)
AI-originated content enters the aggregation record alongside system-sourced
data, with no flag distinguishing its origin
  ↓ (IRQ-GOV-016 — THIS IRQ: no mechanism applies the accuracy, completeness,
  timeliness, adaptability and traceability discipline data aggregation
  already requires, specifically to this content)
Content is treated as though it carries the same assurance as system-sourced
data, without having been controlled to that standard
  ↓ (IRQ-GOV-011: regulatory obligation mapping may not itself flag that
  aggregation obligations extend to AI-originated content)
Capital, provisioning or a regulatory return incorporates unflagged,
uncontrolled AI-originated content
  ↓
Inaccuracy or untraceability surfaces via audit, supervisory review or a
later reconciliation exercise → finding that risk-data aggregation
discipline was not extended to AI-originated content → supervisory/
reputational consequence

Control Breakpoints:
  • Data-domain controls (input side): govern data flowing into the model,
    not in scope of this IRQ
  • IRQ-GOV-016: AI-originated content in the aggregation chain is flagged
    and held to the same data-quality discipline as other risk data
  • IRQ-GOV-011: regulatory obligation mapping confirms aggregation
    obligations extend to AI-originated content
  • IRQ-MOD-004: accuracy/hallucination controls supply part of the accuracy
    assurance this IRQ requires be actually applied at the aggregation point
```

## 7. Why a Domain Expert May Miss It
- Data-aggregation governance was built for structured, system-sourced risk data; the assumption that AI-generated narrative or summarisation content needs the same discipline as a number pulled from a source system is not yet a common one among risk-data specialists.
- AI-assisted content (a summarised exposure paragraph, a reconciled narrative) does not look like "data" in the conventional sense the aggregation framework was designed to govern, so a reviewer checking framework compliance against system feeds may not think to ask whether AI-assisted narrative content is even in scope.
- "The model summarised, it didn't decide" is an intuitive but incomplete basis for treating AI-assisted content as lower-risk than a decisioning output, missing that inaccurate summarisation or reconciliation content can still corrupt a capital or provisioning figure exactly as a data error would.
- Existing input-side data controls elsewhere in the standard are easily, but wrongly, read as covering AI and data comprehensively, obscuring that they govern data flowing into the model, not model output flowing into the firm's own risk-reporting estate — a different direction entirely.

## 8. Assurance Objective
**AO-GOV-016:** Where AI-generated or AI-assisted output feeds the firm's risk-data aggregation estate, capital or provisioning calculations, or supervisory/regulatory returns, that output shall be subject to the same accuracy, completeness, timeliness, adaptability and traceability discipline as other risk data, and its AI origin shall be flagged and reconstructable within the aggregation record.

## 9. Expected Controls (Traced)
- **Risk-data aggregation and reporting principles — accuracy and integrity, completeness, timeliness, adaptability, and the surrounding governance, infrastructure and reporting-practice principles — extended to apply to AI-originated contributions to the aggregation estate** — [Basel Committee on Banking Supervision, "Principles for effective risk data aggregation and risk reporting" (BCBS 239), January 2013; 14 principles across governance and infrastructure, risk data aggregation capabilities, risk reporting practices, and supervisory review; initially binding on global systemically important banks from 1 January 2016]. The principles were written for system-sourced risk data; this control is their explicit extension to AI-originated content, which is **reasoned analogy rather than settled practice** — stated as such, not as an existing requirement of the framework itself.
- **Flagging or tagging mechanism identifying AI-originated content at the point it enters the aggregation chain, distinguishing it from system-sourced data** — [Emerging Practice] — no published standard defines this mechanism specifically for AI content; it follows from the traceability principle within the cited framework rather than from a prescriptive external standard.
- **Accuracy control applied to AI-originated content equivalent to that applied to system-sourced data, not assumed because the content is a summary or reconciliation rather than a raw figure** — [Emerging Practice, extending the cited framework's accuracy and integrity principle].
- **Traceability through the aggregation record back to the AI system, version, and any human sign-off that produced or approved the content** — [Emerging Practice, extending the cited framework's traceability expectation].
- **Named ownership for extending aggregation discipline to AI-originated content, distinct from ownership of the aggregation framework generally** — [linked IRQ-GOV-001 ownership principle, extended].

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the firm complies with its risk-data aggregation framework" — **L1** (asserts general compliance; does not evidence AI-content coverage specifically).
- Documentation of the flagging/tagging mechanism for AI-originated content in the aggregation estate, and of the accuracy, completeness, timeliness and adaptability controls applied to it — **L2**.
- Configuration or process review confirming the flagging mechanism is actually implemented and applied at the point of entry — **L3**.
- Sample trace from a regulatory return or capital/provisioning calculation back through the aggregation record, confirming AI-originated inputs are identifiable and their accuracy was controlled — **L3**.
- Internal audit or independent review of aggregation-framework coverage specifically for AI-originated content — **L4**.
- Evidence from an actual historical instance showing AI-originated content was correctly flagged, controlled and traced through to a regulatory return or calculation — **L5**.

## 11. Independent Test
> Documentation and sample-trace review: reviewer selects a sample of AI-originated content contributing to the risk-data aggregation estate (a narrative risk commentary, an exposure summarisation, a reconciliation output) and traces it through the aggregation record to confirm it is flagged as AI-originated, that accuracy, completeness, timeliness and adaptability controls equivalent to those applied to system-sourced data were applied to it, and that the chain is reconstructable back to the AI system, version and any human sign-off. The review runs in both directions: the forward sample above, and a reverse trace from a regulatory return or capital/provisioning calculation back through the aggregation record, confirming AI-originated inputs are identifiable and their accuracy was controlled — the reverse trace is what catches AI-originated content the forward sample's inventory did not know about, and is the L3 sample trace field 10 expects. No published testing methodology exists specific to AI content in risk-data aggregation and regulatory reporting — stated plainly, not implied; this is a documentation and traceability review against an existing regulatory standard (BCBS 239), not a new empirical test. The extension of BCBS 239's principles to AI-generated content is reasoned analogy, not settled practice, and is stated as such. Conducted entirely against documentation and sample tracing; no production system access required. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (the standard being extended — BCBS 239 — is mature and regulator-mandated, but no established methodology or precedent yet exists for how its principles apply specifically to AI-generated contributions, so the extension itself rests on reasoned analogy rather than settled practice).

## 12. Pass Indicators
- Sampled AI-originated content in the aggregation chain is flagged as such and traceable back to the producing system, version and sign-off.
- Accuracy, completeness, timeliness and adaptability controls equivalent to system-sourced data are evidenced for the sampled content, not assumed.
- At least one historical instance evidences AI-originated content correctly flagged, controlled and traced through to a regulatory return or capital/provisioning calculation.
- Named ownership exists for extending aggregation discipline to AI-originated content.
- The flagging mechanism covers narrative, summarisation and reconciliation content, not only one type of AI contribution.

## 13. Fail Indicators
- Sampled AI-originated content in the aggregation chain has no flag distinguishing it from system-sourced data.
- Accuracy or traceability controls applied to AI-originated content are assumed rather than evidenced.
- No mechanism exists to trace AI-originated content back through the aggregation record to the producing system, version or sign-off.
- No historical instance can be produced showing the flagging or control mechanism actually operating.
- Ownership for extending aggregation discipline to AI-originated content is undefined or defaults to the general aggregation-framework owner with no AI-specific consideration.

## 14. Reporting Language
**Pass:** "Sample tracing confirms AI-originated content contributing to the risk-data aggregation estate is flagged, subject to accuracy, completeness, timeliness and adaptability controls equivalent to system-sourced data, and traceable back through the aggregation record to the producing system, version and sign-off. Conclusions rest on ★2 methodology — a documentation and traceability review extending BCBS 239 to AI content by reasoned analogy, not settled practice — and should be read as professional assessment of the sample reviewed."
**Fail:** "Sample tracing found AI-originated content entering the risk-data aggregation estate with no flag distinguishing its origin and no accuracy control evidenced beyond the assumption that summarisation carries lower risk than decisioning. The content is not traceable back through the aggregation record to the producing system or version. This is a material gap in the discipline the firm already applies to its risk data generally, and should be reported as a finding requiring remediation before AI-originated content is relied upon in capital, provisioning or regulatory-return calculations."
**Partial:** "Narrative risk commentary is flagged and traceable, but reconciliation output produced by the same AI system is not distinguished from system-sourced data in the aggregation record. The assurance objective is not yet met for reconciliation content; remediation should extend the flagging mechanism to cover all AI-originated content types within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (an isolated flagging or accuracy gap in aggregation content is
              unlikely alone to produce a materially wrong capital or
              provisioning figure, given other aggregation controls remain
              in place)
  Likelihood: 2 (plausible given aggregation frameworks were built for
              system-sourced data, but reduces materially once AI-originated
              content is deliberately brought into scope and flagged)
  Detectability: 3 (a flagging mechanism and periodic sample tracing surface
              gaps on a defined cycle, though routine reporting activity
              gives no natural signal absent a dedicated check)
  Recoverability: 2 (correcting a flagging or accuracy gap is a governance
              and process fix, but a regulatory return already submitted
              incorporating unflagged content cannot be retrospectively
              corrected without a formal restatement)
  Novelty: 4 (very likely to be missed: RDARR discipline has no established
              tradition of distinguishing AI-originated content, and
              input-side data controls elsewhere in the standard are easily,
              but wrongly, assumed to already cover this)

Interpretation: acceptable residual risk once AI-originated content is
deliberately brought within aggregation-framework discipline and flagged;
the principal concern is that, absent this IRQ, a firm may reasonably
believe its existing BCBS 239 compliance programme already covers
AI-assisted content, when the framework predates that content type
entirely.

If controls are absent or degraded:
  Severity: 3 (unflagged, uncontrolled AI-originated content contributing to
              capital, provisioning or a regulatory return is a
              data-integrity exposure inside a regulator-mandated framework,
              with consequences extending beyond the immediate content
              itself)
  Likelihood: 3 (foreseeable wherever generative or agentic AI is used to
              produce narrative, summarisation or reconciliation content
              feeding risk reporting, an increasingly common use case)
  Detectability: 4 (silent by construction — the aggregation record gives no
              signal that any given entry is AI-originated absent a
              deliberate flagging mechanism)
  Recoverability: 3 (a regulatory return found to rest on unflagged,
              uncontrolled AI-originated content may require restatement and
              triggers supervisory scrutiny not undone by fixing the
              flagging mechanism after the fact)
  Novelty: 4
Residual risk: Moderate-to-high while unflagged; this IRQ tests for a
genuinely uncovered direction in the standard's existing input-side data
controls and aggregation-framework controls.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | An isolated flagging or accuracy gap is unlikely alone to produce a materially wrong capital/provisioning figure while other aggregation controls remain in place. |
| **Likelihood** | 3 | Probable given RDARR frameworks were built for system-sourced data and generative/agentic AI use in risk reporting is an increasingly common, largely ungoverned use case. |
| **Detectability** | 4 | Silent by construction — the aggregation record gives no signal that an entry is AI-originated absent a deliberate flagging mechanism. |
| **Recoverability** | 3 | A regulatory return resting on unflagged, uncontrolled AI-originated content may require restatement; supervisory scrutiny triggered is not undone by a later fix. |
| **Novelty** | 4 | RDARR discipline has no established tradition of distinguishing AI-originated content; existing input-side data controls are easily but wrongly assumed to already cover this output-side gap. |

## 17. Regulatory Basis
> [Basel Committee on Banking Supervision, "Principles for effective risk data aggregation and risk reporting" (BCBS 239), January 2013] sets 14 principles across governance and infrastructure, risk data aggregation capabilities, risk reporting practices, and supervisory review, initially binding on global systemically important banks from 1 January 2016. The principles' accuracy and integrity, completeness, timeliness, adaptability and traceability requirements were written for system-sourced risk data; no provision within the framework, and no subsequent regulatory instrument identified in the verified source set, explicitly extends these principles to AI-generated or AI-assisted content. This IRQ's control objective therefore rests on reasoned analogy — that content contributing to the same aggregation estate should meet the same discipline regardless of how it was produced — rather than a settled regulatory requirement specific to AI, and this is stated openly rather than an AI-specific anchor being invented.

## 18. Research Basis
> No peer-reviewed literature specifically evaluating the application of risk-data aggregation principles to AI-generated content in financial-services risk reporting was identified in the source registers; this control area is regulatory-instrument-led (the Basel Committee's aggregation and reporting principles) rather than research-led, extended by reasoned analogy rather than incident-evidenced, consistent with the honest confidence rating given at Independent Test.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-009 (I.4: documentation adequacy — a related but distinct
    artefact set; this IRQ concerns data-quality discipline over aggregation
    content, not system description)
  - IRQ-GOV-011 (I.4: regulatory obligation mapping — confirms whether
    aggregation obligations are identified as extending to AI-originated
    content)
  - IRQ-MOD-004 (B.2: hallucination/accuracy controls — supplies part of the
    accuracy assurance this IRQ requires be actually applied at the
    aggregation point)
```

## 20. References
```
[1] Basel Committee on Banking Supervision, 2013. "Principles for effective
    risk data aggregation and risk reporting" (BCBS 239).
    Published: January 2013. Initially binding on global systemically
    important banks from 1 January 2016.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): RDARR governance was built for structured,
  system-sourced risk data; the assumption that AI-generated narrative or
  summarisation content needs the same discipline as a number pulled from a
  source system is not yet a common one, and existing input-side data
  controls are easily mistaken for already covering this output-side gap.
✓ Test 2 (Plausible Harm): grounded in BCBS 239, a mature, regulator-mandated
  framework whose accuracy, completeness, timeliness, adaptability and
  traceability principles are extended here to AI-originated content by
  reasoned analogy, stated as such rather than as settled practice.
✓ Test 3 (Testable): testable via a flagging-mechanism and sample-trace
  review against the aggregation record. ★2 methodology, honestly caveated —
  no published protocol specific to AI content exists.
✓ Test 4 (Decision-Relevant): outcome bears on the integrity of capital,
  provisioning and regulatory-return figures independent of whether the
  underlying AI system itself passes every other IRQ.

Change Log:
- v1.0 (2026-07-31): Initial publication; all four tests passed.
```

