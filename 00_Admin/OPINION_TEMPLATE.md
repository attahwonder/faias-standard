# OPINION_TEMPLATE.md — FAIAS Independent Assurance Opinion Skeleton

**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  
**Document Custodian:** the maintainer

---

## Purpose

This document is a skeleton template for preparing an **Independent Assurance Opinion** on whether an AI system should proceed to deployment, using FAIAS. The template is non-normative: it illustrates one use of FAIAS and is not a requirement of the standard. FAIAS draws on the conclusion forms of ISAE 3000 (Revised); it does not make an engagement ISAE-conformant, and a practitioner who reports under ISAE 3000 must meet that standard in full.

Each FAIAS engagement produces an opinion that answers: *"Should this AI system proceed to deployment?"* with one of four conclusions:
1. **Should Proceed** — No material deficiencies; proceed with ongoing monitoring
2. **Should Proceed With Conditions** — Conditions must be satisfied within specified timelines
3. **Should Not Proceed** — Material control gaps require substantial remediation
4. **Unable to Form Opinion** — Insufficient evidence or access; extended review needed

---

## Opinion Template: Full Structure

### FRONT MATTER

**Cover Page**
- Title: "Independent Assurance Opinion — [System Name & Version]"
- Opinion Date: [YYYY-MM-DD]
- Classification: [Confidential — addressee and named recipients]
- Addressee: [Commissioning Firm]
- Distribution List: [Named recipients, e.g. Sponsor, Board, Audit Committee; any wider distribution on the issuer's terms]
- Preparer: [Assurance Firm / Internal Team Name]
- Basis of Review: [(A) full evidential basis sought / (B) qualified evidential basis] (Part G)

**Intended Use (Model Paragraph)**

> This opinion is addressed to [Commissioning Firm], which commissioned the review, to inform its own deployment decision. Any wider distribution is on [Preparer]'s terms. The conclusion is [Preparer]'s, on the terms of this engagement. FAIAS, the standard used to prepare it, confers no right of reliance on any party and is not a certification or approval scheme.

---

**Opinion Statement (Headline)**

[1–2 paragraph executive conclusion. Example:]

> We have completed an independent assurance review of [System Name] using the FAIAS standard, at [reasonable / limited] assurance. We assessed [X] Independent Review Questions (IRQs) across [Y] domains, executed non-production testing per the FAIAS Testing Playbook, and evaluated control design, and how controls performed in non-production testing, against [Z] core assurance claims.
>
> **Our Opinion:** [System Name] **Should Proceed With Conditions** to production deployment. We have identified [N] material findings; conditions specified in Section E below must be satisfied within stated timelines before the firm's deployment decision. Provided conditions are met, we have [reasonable / limited] assurance that control design is sufficient to manage identified risks within the declared operating envelope, and that those controls performed as designed in non-production testing. Operating effectiveness in production is assessed at post-deployment re-assurance.

---

**Board Dashboard (Executive Summary Visual)**

**Deployment Recommendation:**

| Recommendation | Meaning | Opinion Category |
|---|---|---|
| 🟢 **Proceed** | **Deployment recommended.** No material deficiencies identified. The firm's own approval authority decides; routine monitoring follows. | Should Proceed |
| 🟡 **Proceed With Conditions** | **Deployment recommended subject to conditions.** Conditions below are to be satisfied within stated timelines before deployment; the firm's own approval authority decides. | Should Proceed With Conditions |
| 🔴 **Do Not Proceed** | **Deployment not recommended.** Material control gaps require substantial remediation before re-assessment. | Should Not Proceed |
| ⚪ **Unable to Form Opinion** | Insufficient evidence or access. Extended review or scope clarification needed. | Unable to Form Opinion |

**Your System:** 🟡 [**Proceed With Conditions**] — Conditions due [Date]; estimated condition satisfaction timeline [X weeks]

---

**Key Residual Risks (After Control Implementation)**

| Risk Theme | Domain | Severity | Mitigation |
|---|---|---|---|
| [Theme 1: e.g., Hallucination in edge cases] | Model (B.2) | High | Condition: escalation threshold tuning; monitored 12 weeks |
| [Theme 2: e.g., Data source freshness] | Data (A.3) | Medium | SLA enforcement; automated alert if >30-day staleness |
| [Theme 3: e.g., Human override fatigue] | Human Oversight (D.1) | Medium | Governance: quarterly override rate audit; alert if >15% |

---

**Executive Summary Tone Note:**

The Independent Assurance Opinion reads like an **operational resilience assessment**, not a penetration test report. It focuses on control design, and on how controls performed in non-production testing within the system's declared operating envelope — answering "can we trust this system?" — rather than documenting every theoretical attack vector.

**Model Paragraph (Operational Resilience Tone):**

> Our assessment evaluated the controls in place to manage [System Name]'s performance within the approved operating envelope for [use case]. We reviewed governance structures, monitoring protocols, human oversight design, and technical controls supporting the core assurance claim: "[Key Claim]." Testing demonstrated that [key control] functions as designed in representative scenarios. Residual risk of [specific failure mode] is bounded by [mitigating control], with automatic escalation to human review if conditions deteriorate. We are satisfied that the system's control environment and operational discipline are appropriate for the [Tier level] materiality profile of this deployment.

---

**Table of Contents**

---

### PART A: SCOPE & LIMITATIONS

#### A.1 Scope

**Systems Reviewed:**
- [System name, version, deployment date, business activities]
- [Technology stack: model type, input sources, output channels, integrations]
- [Customer/regulatory materiality: business activities affected]

**Review Period:**
- [Assessment dates: YYYY-MM-DD to YYYY-MM-DD]
- [System operational history: live for X weeks before review]

**IRQs Assessed:**
- Total IRQs in FAIAS standard: 109 (as at v1.2.0)
- IRQs selected for this engagement: [X] (reason for sampling, if applicable)
- Domains covered: [e.g., Data, Model, Human Oversight, Security, Governance]
- Subdomains covered: [e.g., B.2 Hallucination, D.1 Automation Bias, E.3 Supply Chain]

**Assurance Claims Evaluated:**
- [List 5–10 core claims assessed, e.g., "System accesses only authorised sources"]

**Materiality Threshold:**
- Findings escalated to opinion if material against ≥1 materiality lens (per ASSURANCE_ARCHITECTURE.md, Layer 3: Materiality Screening)
- [Additional materiality guidance specific to this engagement]

#### A.2 Limitations

**Environment:**
- Review testing executed only in non-production environments; any evidence derived from the firm's own controlled resilience exercises or from read-only production records is expressly identified as such
- Test environment may not be fully representative of production data volumes, response latency, or edge-case distribution
- Results are indicative of control design; ongoing operational effectiveness monitoring required post-deployment

**Methodology:**
- Emerging practice controls are identified and flagged; no published gold-standard testing exists
- Frontier risks (novel attack vectors with sparse published research) assessed via expert judgment; confidence is limited
- Third-party dependencies (vendor model providers, data brokers) assessed via vendor attestations and audited SLAs; direct testing not feasible

**Scope Boundaries:**
- Governance and monitoring pre-deployment assessed; post-deployment governance effectiveness cannot be guaranteed
- Operating envelope declared as of review date; future business/technical changes may require re-assessment
- Testing focused on material IRQs; lower-priority questions deferred to lifecycle monitoring

**Time-Bound:**
- Opinion valid for [X months] from issue date
- Major changes (code, model weights, data sources, user segments, vendor relationships) trigger re-assessment requirement
- Annual reassessment recommended per FAIAS assurance lifecycle

#### A.3 Basis Date — the Opinion Speaks as at Its Date

This opinion is a statement of position **as at the opinion date, against the version of the FAIAS standard cited on the cover page**. Every ★ rating reproduced in it carries its own version anchor, in the form `★n — as at FAIAS vX.Y (date)`, so that a rating quoted out of this report still carries the basis on which it was given.

Research into AI failure modes and into the methods available to test them continues to move, and the standard's ratings move with it. **Subsequent movement does not revise this opinion.** Later research, a newer edition of a cited framework, or a re-rating of an Independent Review Question in a later version of the standard is a non-adjusting event by construction: it does not make a conclusion reached here incorrect, and it is not of itself a basis for reopening one. This follows the established treatment of subsequent events in an assurance opinion (ISA 560; IAS 10), under which the opinion stays anchored to conditions as at its date and a later event adjusts it only where it evidences a condition that existed at that date.

Where the standard has moved since issue, **the register's version-anchor history and its open Under Research Observations are the context in which this opinion is read** — not a correction to it. A re-review under a newer anchor is the ordinary product of that mechanism rather than a revision of this one, and is the appropriate step where currency of method is material to the decision in hand.

This paragraph fixes the basis date; it does not extend the validity period stated above, and it does not alter the reliance terms of the engagement.

---

### PART B: ASSESSMENT APPROACH & BASIS

#### B.1 Methodology

We applied the FAIAS independent assurance standard, which comprises 7 interlinked components:

1. **Component 1 (AI Taxonomy):** Common language of 9 domains and 44 subdomains, with single-homing rules and boundary rulings — the classification for all risk identification; regulation is mapped separately in the regulatory crosswalk (`V5_Regulatory_Crosswalk/`)
2. **Component 2 (IRQs Battery):** Independent Review Questions taxonomy across 9 domains, 44 subdomains — defines what to assess
3. **Component 3 (Assurance Claims):** Claims-Argument-Evidence chains; claims-IRQ mapping; materiality screening — structures the assurance case
4. **Component 4 (Evidence Catalogue):** Centralised inventory of design documents, test results, policies, monitoring data — supports auditability
5. **Component 5 (Testing Playbook):** Non-production test procedures, success criteria, evidence collection — implements FOUR-TEST discipline
6. **Component 6 (Safety Case):** Structured safety argument (GSN), envelope declaration, envelope drift mitigation, 8-phase assurance lifecycle
7. **Component 7 (Independent Assurance Opinion):** This document; four-box conclusion drawing on the conclusion forms of ISAE 3000 (reasonable / limited assurance)

**Assurance Type:** [Reasonable Assurance / Limited Assurance]
- **Reasonable Assurance:** Comprehensive control review, majority L4–L5 evidence, and every material claim resting on tests rated ★4 or above. No reasonable assurance rests on a material test rated ★1–★3 (ASSURANCE_ARCHITECTURE.md, Layer 2: the assurance-level rule)
- **Limited Assurance:** Selective control review, a mix of evidence levels, or any material claim resting on a test rated ★1–★3, each such rating disclosed at the point of the conclusion (PLAYBOOK_OVERVIEW.md §8)

**Where the engagement is classified Limited Assurance, the issued report states both of the following, in the summary of the work performed and not only in an internal working paper:** that the procedures performed in a limited assurance engagement vary in nature and timing from, and are **less in extent** than for, a reasonable assurance engagement; and that consequently the level of assurance obtained is **substantially lower** than the assurance that would have been obtained had a reasonable assurance engagement been performed. Where it assists the reader, the summary may also indicate procedures that were **not** performed which would ordinarily be expected in a reasonable assurance engagement; that indication is not required to be exhaustive, because "a complete identification of all such procedures may not be possible" where the practitioner's required understanding and consideration of engagement risk is itself less than in a reasonable assurance engagement. *(IAASB, International Standard on Assurance Engagements (ISAE) 3000 (Revised), *Assurance Engagements Other than Audits or Reviews of Historical Financial Information*, final pronouncement, December 2013 (IAASB; published by IFAC), effective for assurance reports dated on or after December 15, 2015, para 69(k)(i)–(ii), with para A175; ifac.org, accessed 2026-09-11.)*

#### B.2 Evidence Sources

**Design Review:**
- Architecture documents, design rationale, control specifications
- IRQ Canvas dossiers (per IRQ_TEMPLATE.md) — 21-field structure per IRQ
- Regulatory/research basis documented; evidence levels tagged L1–L5

**Testing:**
- Non-production test execution per Component 5 Testing Playbook
- Test procedures cite published benchmarks or are flagged as emerging practice
- Testing confidence ratings (★1–★5) assigned per defined anchors
- [X] IRQs tested; [Y] passed; [Z] passed with conditions; [W] inconclusive

**Interviews:**
- [Number] interviewees across [roles]: model developers, risk officers, compliance, operations
- Semi-structured question bank per FAIAS assessment guide
- Notes recorded and triangulated against documented processes

**Regulatory Alignment:**
- Cross-walk against FCA SYSC (systems and controls) expectations, PRA SS1/23, EU AI Act, NIST AI RMF
- [List major regulatory sources cited]

---

### PART C: ASSURANCE CLAIMS ASSESSMENT SUMMARY

**Table: Core Claims Status**

| # | Core Claim | Material? | Test Status | Evidence Level | Confidence (★) | Residual Risk | Opinion Impact |
|---|---|---|---|---|---|---|---|
| 1 | [Claim text; e.g., "System accesses only authorised data sources"] | Yes | Passed | L4–L5 | ★4 | Low | Supports Proceed |
| 2 | [Claim text] | Yes | Passed | L4 | ★4 | Low | Supports Proceed |
| 3 | [Claim text] | Yes | Inconclusive | L2–L3 | ★2 | Medium | Condition required |
| 4 | [Claim text] | Yes | Passed | L3–L4 | ★4 | Low–Med | Supports Proceed |
| 5 | [Claim text] | No | [Minor finding] | L2 | ★2 | Low | Lifecycle monitoring |

**Interpretation:**
- **Passed:** IRQs supporting this claim passed testing; control design verified, and controls performed as designed in non-production testing; no conditions required
- **Passed w/ Conditions:** IRQs supporting this claim passed with caveats; condition specified in Section E (e.g., "confirm threshold tuning")
- **Inconclusive:** Insufficient evidence or emerging practice; no published benchmark; condition specified or escalated to lifecycle monitoring
- **Evidence Level:** L4–L5 = independent testing; L2–L3 = design/documentation; L1 = assertion only
- **Confidence (★):** maturity of the test method (ASSURANCE_MODEL.md §6). ★5 = published, widely adopted methodology with a settled financial-services benchmark (no FAIAS test is rated ★5); ★3 = credible research methods, no agreed benchmark; ★1 = expert judgment only
- **Residual Risk:** After control implementation, what risk remains? Scale: Low / Medium / High

---

### PART D: MATERIALITY-SCREENED FINDINGS SUMMARY

#### D.1 High-Impact Material Findings

**Finding 1: [Title & IRQ]**
- **Materiality Lenses Affected:** [e.g., Customer Outcomes, Operational Resilience]
- **Control Gap:** [Describe deficiency]
- **Business Impact:** [Risk narrative; e.g., "System may fail to escalate failed decisions, resulting in customer denial/complaint"]
- **Evidence:** [Test results, design review findings, interview notes]
- **Remediation:** [Recommended action and timeline]
- **Status in Opinion:** [Condition / Finding for escalation]

**Finding 2: [Title & IRQ]**
- [Same structure]

#### D.2 Medium-Impact Material Findings (with Mitigant)

**Finding 3: [Title & IRQ]**
- **Materiality Lens Affected:** [e.g., Data Protection]
- **Control Gap:** [Describe]
- **Mitigant:** [Existing compensating control; why risk is bounded]
- **Evidence:** [Test results; policy evidence]
- **Status in Opinion:** [Disclosed finding; no condition if mitigant validated]

#### D.3 Low-Impact Findings (Non-Material)

**Finding 4–N: [Titles & IRQs]**
- **Materiality Assessment:** No material impact (assessed against all 10 lenses; below threshold)
- **Recommendation:** Relay to lifecycle monitoring; no escalation to deployment decision
- **Rationale:** [Briefly explain why finding does not undermine core claims]

---

### PART E: CONDITIONS (IF ANY)

**If opinion is "Should Proceed With Conditions," list each condition:**

**Condition 1: [Title]**
- **Scope:** [Which claim(s) this addresses]
- **Requirement:** [Specific action; not vague]
- **Success Criteria:** [Measurable; e.g., "escalation workflow test results show >99% accuracy in triggering alerts"]
- **Target Date:** [YYYY-MM-DD; within X days of opinion date]
- **Evidence to Provide:** [What artifacts demonstrate satisfaction]
- **Gating:** [The firm's deployment decision should be contingent on this condition]

**Condition 2: [Title]**
- [Same structure]

**Condition 3: [Title]**
- [Same structure]

---

### PART F: INDEPENDENT ASSURANCE OPINION (FOUR-BOX CONCLUSION)

**[SELECT ONE CONCLUSION BELOW]**

State the assurance level obtained in the conclusion. Reasonable assurance is available only where no material claim rests on a test rated ★1–★3 (Part B.1). Where the engagement is at limited assurance, phrase the conclusion to convey whether any matter has come to the reviewer's attention that causes the reviewer to believe the stated proposition is not so, and carry the Part B.1 disclosure.

#### Option 1: SHOULD PROCEED

> We have [reasonable / limited] assurance that [System Name] is designed with controls sufficient to manage the identified risks within the declared operating envelope, and those controls performed as designed in non-production testing. Operating effectiveness in production is assessed at post-deployment re-assurance. No material deficiencies were identified. We recommend deployment, with ongoing operational monitoring per the FAIAS assurance lifecycle (early-life monitoring weeks 1–12, then annual assurance); the firm's own approval authority decides.

**Basis for Conclusion:**
- Material claims supported predominantly by L4–L5 evidence; for reasonable assurance, no material claim rests on a test rated ★1–★3 (Part B.1)
- [X] out of [Y] IRQs passed testing without exception
- Regulatory alignment assessed against FCA, PRA, [other regulators]
- No material control gaps; minor findings delegated to lifecycle monitoring

**Conditions:** None

**Monitoring Requirements:**
- [Specific KPIs to track in production weeks 1–12: e.g., hallucination rate <2%, escalation accuracy >99%]
- [Escalation triggers: e.g., hallucination rate exceeds 5%, or alert fatigue detected in >10% of overrides]

---

#### Option 2: SHOULD PROCEED WITH CONDITIONS

> We have [reasonable / limited] assurance that [System Name] can proceed to deployment, provided the following conditions are satisfied within stated timelines. The conditions address gaps in control design or evidence sufficiency that, if remediated, will bring residual risk within acceptable tolerance. The firm's deployment decision should be contingent on condition satisfaction.

**Core Conclusion:** [System Name] exhibits control design sufficient to manage material risks, subject to conditions.

**Conditions (see Section E for detail):**
1. [Condition 1 title; target date]
2. [Condition 2 title; target date]
3. [Condition 3 title; target date]

**Gating:** Sponsor must provide evidence of condition satisfaction before production deployment. Failure to meet condition timeline requires re-assessment.

**Monitoring Requirements:**
- [KPIs and escalation triggers post-condition satisfaction]

---

#### Option 3: SHOULD NOT PROCEED

> We are unable to provide [reasonable / limited] assurance that [System Name] is ready for deployment in its current form. Material control gaps exist that require substantial remediation before independent assessment can be completed. We recommend suspension of deployment plans and comprehensive remediation effort.

**Basis for Conclusion:**
- [Major Finding 1]: [Describe control deficiency and business risk]
- [Major Finding 2]: [Describe control deficiency and business risk]
- [Major Finding 3]: [Describe control deficiency and business risk]

**Why Conditions Are Insufficient:**
- Gaps are architectural, not operational (require code/design changes, not tuning)
- OR multiple critical claims are undermined with no single-point mitigant
- OR evidence base is too sparse to form reasonable assurance despite remediation efforts

**Recommended Remediation Scope:**
- [Redesign component X, per rationale...]
- [Implement emerging-practice control Y, and test it at the highest ★ rating available for that control]
- [Restructure escalation workflow to address alert fatigue findings]

**Path to Re-Assessment:**
- After remediation complete, resubmit for Component 5 Testing and Component 7 Opinion

---

#### Option 4: UNABLE TO FORM OPINION

> Insufficient evidence or access prevented completion of independent assurance review. We are unable to form reasonable or limited assurance on whether [System Name] should proceed to deployment.

**Reasons:**
- [Access blocked to test environment; testing cannot proceed]
- OR [Critical IRQ evidence unavailable; vendor not providing attestations]
- OR [Scope boundaries prevent assessment of material claims]

**Path Forward:**
- [Extend review timeline to X weeks; address access/evidence barriers]
- OR [Accept limited assurance scope covering only [subset of claims]]

---

### PART G: REVIEW CONFIDENCE STATEMENT

**Overall Review Confidence (internal working judgment; never issued as a grade):** [High / Medium / Low]

*The three paragraphs below are working notes for the engagement file. They are not reproduced in the issued report, which carries the statement on the basis of the review in form (A) or (B), set out below.*

> [High] We have high confidence that we have identified all material AI risks in this deployment. Assessment methodology is mature (published benchmarks, established standards), evidence base is primarily L4–L5 (independent testing, operational data), testing confidence is high (★4 ratings; on the current battery no engagement reaches High, ASSURANCE_ARCHITECTURE.md), and coverage spans all material IRQs. Residual uncertainty is low and attributable to inherent frontier risks without published defences.
>
> [Medium] We have medium confidence in our risk identification. Assessment includes some emerging-practice controls (no published gold standard), evidence is mixed (L2–L3 design review plus L4 testing), testing methodology is partially novel (★2–★3 ratings), and time constraints prevented comprehensive coverage of lower-priority IRQs. Residual risk may exist in untested areas.
>
> [Low] We have limited confidence in our risk identification. Assessment methodology is sparse (few published benchmarks for this risk domain), evidence is primarily L1–L2 (design documentation, expert assertion), testing confidence is low (★1–★2 ratings), or time/scope constraints severely restricted coverage. Residual risk is likely; repeat assessment recommended within [X] months.

**Factors Contributing to Confidence Level:**
- Maturity of testing methods used (established benchmark vs. emerging practice vs. expert judgment)
- Evidence profile (proportion L1–L2 vs. L3–L5)
- Testing confidence distribution (how many ★1–★2 vs. ★4 tests)
- Coverage (% of risk domains tested; % of IRQs assessed; sampling vs. comprehensive)
- Frontier capability risks (novel attack vectors with sparse published research)

**Limitations on Confidence:**
- [Specify if testing environment differs materially from production]
- [Specify if third-party dependencies not directly tested]
- [Specify if emerging-practice controls dominate risk profile]

**Expression in the issued report — the statement on the basis of the review.** The High/Medium/Low assessment above is the engagement's internal working judgement; it is never expressed to the addressee as a grade or scale. In the issued report it takes one of exactly two narrative forms, stated separately from the conclusion: **(A) review conducted on the full evidential basis sought** — the evidence sought at scoping was substantially obtained; the tested environment was demonstrated representative to the extent recorded; conclusions rest principally on artefact and test; residual limits are enumerated; or **(B) review conducted on a qualified evidential basis** — each respect in which the basis was narrower than scoped is named, together with what would have strengthened it, and the conclusion is read with those limits. **The minimum-basis rule:** where the review's own evidential basis cannot support either statement, no conclusion is issued — the outcome is Unable to Form Opinion, and the statement records what a conclusion would require. The basis statement is never available as a means of qualifying a signed conclusion. The ★ scale grades test-method maturity within the methodology and does not appear in the statement.

**The coverage sentence — mandatory in the issued statement, under both forms.** What Part G bars from the issued statement is the High/Medium/Low assessment expressed as a grade or scale. **Coverage is not a grade**, and the coverage field this section already requires as an internal factor — the proportion of risk domains tested, the proportion of IRQs assessed, and whether the examination was by sampling or comprehensive — is stated in the issued statement, not only held internally. Whichever of (A) or (B) applies, the statement names: the proportion or tier of the IRQ battery actually examined; that the conclusion is drawn by inference from the examined subset to the system's wider control environment and is not a census of it; and which domains or questions were not examined and why, recorded in the report's coverage statement. A statement in form (A) — "review conducted on the full evidential basis sought" — speaks to the basis *sought being obtained*, and is available to an engagement that examined a small proportion of the battery; without the coverage sentence beside it, the addressee cannot tell which.

---

### PART H: REGULATORY ALIGNMENT & GOVERNANCE

#### H.1 Compliance Status Summary

**Table: Regulatory Alignment** *(illustrative structure only — instruments, requirements and statuses are engagement-specific; every citation in a real table is verified against the primary instrument at the engagement, never carried from this template)*

| Regulator | Jurisdiction | Key Requirements | Compliance Status | FAIAS IRQs Addressing |
|---|---|---|---|---|
| FCA | UK | [instrument and provision — verified at engagement]: governance framework expectations | Compliant | IRQ-GOV-001, -002, -003 |
| FCA | UK | [instrument and provision — verified at engagement]: pre-deployment testing expectations | Compliant | IRQ-MOD-005, IRQ-SEC-009 |
| PRA | UK | Operational Resilience: Availability & Recovery | Compliant | IRQ-RES-001 through -004 |
| ECB | Eurozone | [instrument and provision — verified at engagement]: AI risk management expectations | Conditionally compliant | [Explain gaps if any] |
| EU AI Act | EU | High-risk AI: Transparency & Human Oversight | Compliant | IRQ-HUM-007, -008 |

**Interpretation:**
- **Compliant:** Regulatory requirement fully addressed by control and verified via testing or design review
- **Conditionally Compliant:** Requirement will be met upon condition satisfaction (Section E)
- **Non-Compliant:** Requirement not met; requires remediation or exception escalation

#### H.2 Recommended Governance & Monitoring

**Deployment Governance:**
- **Deployment Approval Authority:** [Sponsor + [other approval bodies]]
- **Condition Approval Authority:** [Who signs off on condition satisfaction]
- **Escalation Path:** If post-deployment monitoring detects material drift or control failure, escalate to [Risk Committee / EXCO]

**Ongoing Assurance:**
- **Early-Life Monitoring (Weeks 1–12):** Weekly KPI dashboard; escalation alerts if thresholds breached
  - [KPI 1]: Hallucination rate; escalate if >5%
  - [KPI 2]: Escalation accuracy; escalate if <95%
  - [KPI 3]: Alert fatigue (override rate); escalate if >15%

- **Periodic Assurance (Annual or Post-Major-Change):** Full re-assessment required if
  - Code/model weights updated materially
  - Data sources changed
  - Operating envelope expanded (new customer segments, use cases)
  - Material incident occurs
  - Major vendor/third-party change
  - New regulatory guidance issued affecting material claims

---

### PART I: BASIS OF OPINION

#### I.1 Assurance Standards & Frameworks

- **ISAE 3000 (Revised):** International standard for assurance engagements. FAIAS draws on the conclusion forms of ISAE 3000 (Revised); it does not make an engagement ISAE-conformant, and a practitioner who reports under ISAE 3000 must meet that standard in full.
  - Reasonable assurance: available under FAIAS only where no material claim rests on a test rated ★1–★3 (Part B.1)
  - Limited assurance: the level at which the engagement concludes where any material claim rests on a test rated ★1–★3
  - Where an engagement is classified Limited Assurance, the report carries the para 69(k)(i)–(ii) disclosure: procedures "less in extent" than for a reasonable assurance engagement, and assurance "substantially lower" than reasonable assurance would have obtained (Part B.1)
  
- **FAIAS:** Financial AI Independent Assurance Standard
  - 7-component architecture: Taxonomy, IRQs, Claims, Evidence, Testing, Safety Case, Opinion
  - Claims-Argument-Evidence (CAE) structure per ISO/IEC 15026-2 Goal Structuring Notation
  - Assurance lifecycle: 8 phases from design through retirement

- **NIST AI Risk Management Framework 1.0 (NIST AI 100-1, January 2023)**
  - Four core functions: GOVERN, MAP, MEASURE and MANAGE

- **Financial Regulatory Standards:** FCA SYSC (systems and controls), PRA SS1/23 model risk management, EU AI Act high-risk classification

#### I.2 Professional Responsibilities

**Auditor Independence:**
- We [have / have not] identified conflicts of interest in this engagement
- [If conflicts exist, explain mitigation: e.g., "Senior partner review; no financial interest in deployment outcome"]
- We conducted this engagement with appropriate professional skepticism

**Quality Standards:**
- Review was conducted per FAIAS Quality Standards (METHODOLOGY_STANDARDS.md). These are methodology standards, not a system of quality management; a practitioner who reports under ISAE 3000 also states the firm-level quality standard it applies (ISQC 1 or its successor) and the independence and ethical requirements it applies, as that standard requires.
- All evidence tagged for credibility level (L1–L5); all tests rated for confidence (★1–★5)
- FOUR-TEST validation applied to all IRQs (SME blind spot, plausible harm, testable, decision-relevant)
- Claims-IRQ mapping validated; mandatory completeness rule (two-way traceability) satisfied
- Where an engagement quality control review was performed, its scope followed the four elements at ISAE 3000 (Revised) para 36(b)(i)–(iv) — discussion of significant matters with the engagement partner, review of the subject-matter information and the proposed report, review of selected engagement documentation relating to the significant judgements and conclusions, and evaluation of the conclusions reached in formulating the report and of whether the proposed report is appropriate — the reviewer was independent of the engagement team, the report was not dated before the review completed, and the reviewer's concurrence is recorded as an independent check rather than restated as corroborating evidence for the conclusion (ENGAGEMENT_MODEL.md Gate 5; ASSURANCE_MODEL.md §7A)

**Limitations of Assurance:**
- Assurance provides reasonable (or limited, if specified) basis for opinion, but not absolute certainty
- Future events or undisclosed information may change risk profile; re-assessment required if material changes occur
- Assurance is bounded to defined scope (systems, IRQs, time period, environment); findings outside scope not addressed

#### I.3 Key Assumptions

- Test environment is representative of production in material ways (data distribution, model behaviour, infrastructure load)
- Monitoring infrastructure will be deployed and operated as designed
- Operating envelope as declared will be enforced through governance controls
- Third-party vendors will maintain SLAs and control effectiveness as represented

---

### PART J: APPENDICES

#### J.1 Glossary

- **Assurance Claim:** Assertion about system safety (e.g., "Hallucination is controlled")
- **Evidence Level (L1–L5):** Credibility rating of evidence piece
  - L1 (Assertion): Unvalidated claim; design document only
  - L2 (Documentation): Policy/procedure exists; not tested
  - L3 (Demonstration): Design review or staging test shows concept works
  - L4 (Independent Testing): Standardised test by independent team; published benchmark
  - L5 (Operational): Live production data demonstrates control effectiveness
- **Failure Mode:** How behaviour becomes unsafe (e.g., "confident hallucination")
- **IRQ (Independent Review Question):** Unit of assurance; one IRQ per failure mode per domain
- **Operating Envelope:** Designed-for (explicit yes-list) and NOT-designed-for (explicit no-list) operating conditions
- **Testing Confidence (★1–★5):** Maturity of testing method
  - ★5 = Published, widely adopted methodology with a settled financial-services benchmark; no FAIAS test is rated ★5
  - ★3 = Credible research methods; no agreed benchmark
  - ★1 = Early research; expert elicitation; no published precedent
- **FOUR-TEST Validation:** Every IRQ passes SME blind spot, plausible harm, testable, decision-relevant criteria

#### J.2 Detailed Findings (Expanded)

For each material finding:
- **Finding ID & Title**
- **IRQ(s) & Subdomain(s)**
- **Materiality Lenses Affected**
- **Description:** Control gap, failure mode, business impact
- **Evidence:** Test results, policy review, interview findings
- **Root Cause:** Why gap exists (design omission, emerging practice, resource constraint, etc.)
- **Remediation Recommendation:** Specific action, not generic
- **Timeline & Owner:** Who fixes this, by when
- **Acceptance Criteria:** How we verify fix
- **Escalation Flag:** [High / Medium / Low] criticality

#### J.3 IRQ Status Summary (by Domain; illustrative engagement with 90 of the 109 IRQs in scope)

| Domain | # IRQs Assessed | Passed | Passed w/ Conditions | Inconclusive | Failed | Comments |
|---|---|---|---|---|---|---|
| Data (DAT) | 12 | 11 | 1 | 0 | 0 | 1 condition: data freshness SLA |
| Model (MOD) | 16 | 14 | 2 | 0 | 0 | 2 conditions: confidence tuning, monitoring |
| Agentic (AGT) | 10 | 10 | 0 | 0 | 0 | No gaps identified |
| Human Oversight (HUM) | 9 | 7 | 0 | 2 | 0 | 2 inconclusive: alert fatigue, escalation timing |
| Security (SEC) | 9 | 9 | 0 | 0 | 0 | No gaps identified |
| Third-Party (TPR) | 6 | 6 | 0 | 0 | 0 | Vendor attestations sufficient |
| Resilience (RES) | 7 | 6 | 1 | 0 | 0 | 1 condition: failover testing |
| Conduct & Fairness (CON) | 9 | 9 | 0 | 0 | 0 | No gaps identified |
| Governance (GOV) | 12 | 12 | 0 | 0 | 0 | No gaps identified |
| **TOTAL** | **90** | **84** | **4** | **2** | **0** | **4 conditions; 2 lifecycle monitor** |

#### J.4 Test Results Summary (by Testing Confidence)

| Confidence Level | # Tests | Method | Benchmark Used? | Pass Rate | Notes |
|---|---|---|---|---|---|
| ★5 (Settled financial-services benchmark) | 0 | — | — | — | No FAIAS test is rated ★5 |
| ★4 (Published, partially standardised) | 2 | Published methodology, partially standardised | Partial | 100% (2 of 2) | Rating stated without additional caveat |
| ★3 (Credible research, no agreed benchmark) | 36 | Research-grounded method; reviewer-designed metrics and thresholds | No | 97% (35 of 36) | Professional-assessment caveat at each conclusion |
| ★2 (Bespoke method) | 46 | Institution-specific design; professional judgment dominant | No | 91% (42 of 46) | Caveat at each conclusion; conditions specified |
| ★1 (Very early research) | 6 | Expert review only; novel or unvalidated method | No | 83% (5 of 6) | Expert opinion, not evidence; escalation flags recommended |

#### J.5 Regulatory Documents Cited

- [FCA Handbook, SYSC (Senior Management Arrangements, Systems and Controls)]
- [Bank of England (including the PRA) and FCA, FS2/23 — Artificial Intelligence and Machine Learning, feedback statement, October 2023]
- [NIST AI Risk Management Framework v1.0, January 2023]
- [OWASP Top 10 for LLM Applications, 2025]
- [EU AI Act Regulation (EU) 2024/1689, June 2024]

---

## Sign-Off

**Prepared By:**
- [Assurance Lead Name, Title, Firm]
- [Date]

**Reviewed By:**
- [QA Lead Name, Title]
- [Date]

**Approved For Issue By:**
- [Engagement Lead Name, Title, Firm]
- [Date]

**Recipient Acknowledgement:**
- [Sponsor Name, Title, Institution]
- [Date of receipt]

---

