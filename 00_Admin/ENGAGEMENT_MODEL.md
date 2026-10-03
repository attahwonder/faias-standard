# ENGAGEMENT_MODEL.md — FAIAS Assurance Reviewer's Handbook

**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  
**Document Custodian:** the maintainer

---

## Purpose

This document is the operational handbook for reviewers (assurance practitioners, internal audit, external auditors) conducting a FAIAS engagement. It defines six phases, deliverables per phase, governance decision-points, and tools to apply.

A FAIAS engagement produces an Independent Assurance Opinion (Component 7) backed by systematic threat analysis, evidence collection, and claims assessment.

---


> **Calibration note.** Phase durations and procedure depth in this handbook describe the maximal, Tier 3 form of the engagement and assume manual execution. They are a ceiling to calibrate down from, not a required floor. Scope, depth, sample size and repetition are set per engagement against tier, consequence, evidence availability, the named expert's direction and the depth commissioned; automated test execution reduces effort on mechanical test classes substantially without changing the ★ confidence of the method. Every reduction is recorded, and anything not tested is dispositioned with its reason and consequence rather than omitted silently. See PLAYBOOK_OVERVIEW.md §5A.

## FAIAS Engagement Model: Six Phases

```
┌─────────────────────────────────────────────────────┐
│ Phase 1: Intake & Scoping                           │
│ Output: AI Deployment Profile (1-pager)             │
│ Owner: Engagement Lead + Domain Expert              │
│ Duration: 1–2 weeks                                 │
│ Gate: Scope validated; AI Risk Tier tentative       │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ Phase 2: Materiality Assessment                     │
│ Output: AI Risk Tier + Scoped IRQ Set               │
│ Owner: Assurance Lead + Risk Architect (firm-side)  │
│ Duration: 1 week                                    │
│ Gate: Tier confirmed; engagement scope locked       │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ Phase 3: Threat & Failure Analysis                 │
│ Output: Prioritised IRQ Set + Failure Trees         │
│ Owner: Joint workshop (domain expert + AI reviewer)  │
│ Duration: 2–3 weeks                                 │
│ Gate: Failure modes validated; IRQ list finalised   │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ Phase 4: Evidence & Testing                         │
│ Output: Test Results, Evidence Catalogue            │
│ Owner: Testing Lead                                 │
│ Duration: 4–9 weeks (depends on Tier; §6 stages)    │
│ Gate: Testing complete; evidence levels assigned    │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ Phase 5: Claims Assessment & Opinion                │
│ Output: Independent Assurance Opinion               │
│ Owner: Assurance Lead + Engagement Lead             │
│ Duration: 2–3 weeks                                 │
│ Gate: Opinion reviewed by QA; issued to the sponsor │
└─────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────┐
│ Phase 6: Continuous Assurance & Lifecycle           │
│ Output: Monitoring Plan, Re-Assessment Schedule     │
│ Owner: Assurance Lead + Operations (firm-side)      │
│ Duration: Ongoing (design through retirement)       │
│ Gate: Monitoring activated; lifecycle documented    │
└─────────────────────────────────────────────────────┘
```

---

## Phase 1: Intake & Scoping

### Objective
Gather information about the AI system, its deployment context, and business/regulatory environment. Produce a one-page AI Deployment Profile for sponsor review.

### Information Gathered

#### Business Context
- **Use Case & Business Objective:** What decision or task does the AI support? What customer outcome is enabled? (e.g., "Support credit underwriting decision for SME lending")
- **Process & Workflow:** How does the AI output integrate into business process? Who reviews the AI output? Who is accountable for the decision? Is there a human-in-loop or is system autonomous?
- **Customer Impact:** Which customers are affected? What's the materiality of the decision (eligibility, pricing, access to service)? Are vulnerable customers involved (disability, elderly, financial literacy)?
- **Regulatory Obligations:** Which regulatory frameworks apply? (FCA SYSC 4.1, PRA model risk, Consumer Duty, AML/CFT, data protection, market conduct, etc.)
- **Accountable Executive:** Who owns this system end-to-end? Who is the SMCR-accountable person for model risk governance?

#### AI System Context
- **Model Type & Provenance:** Is this a large language model (LLM), supervised classifier, regression model, reinforcement learning agent, ensemble? Who built/trained it (internal, external vendor)? What version?
- **Fine-Tuning or Adaptation:** Has the base model been fine-tuned? On what data? How recently? Who owns fine-tuning decisions?
- **Retrieval-Augmented Generation (RAG):** If system uses retrieval, what are the data sources? How fresh are they? Who curates them?
- **Agents & Tool Use:** Does system have access to tools, APIs, or autonomous decision-making? What are the tools/decisions it can make?
- **Memory & State:** Does system maintain context across multiple requests? Is state persisted? Are there prompt injections/jailbreak risks?
- **Human Involvement:** What does human reviewer do? Can human override? Is override logged and audited?

#### Deployment Environment
- **Development Environment:** Where is the system built? Access controls, version control, testing protocols
- **Test/Staging Environment:** Is there a non-production environment? How representative is it of production?
- **Production Environment:** Cloud provider? Self-hosted? Data residency? Incident response procedures?
- **Third-Party Dependencies:** Model host (e.g., OpenAI API), data providers, infrastructure vendors. Who has data access? What are SLAs?
- **Monitoring & Alerting:** What KPIs are tracked? Are there automated alerts? Who responds to incidents?

### Deliverable: AI Deployment Profile (1-pager)

**Template:**

```
═══════════════════════════════════════════════════════════════
AI DEPLOYMENT PROFILE
System: [Name]  |  Version: [X.Y]  |  Date: [YYYY-MM-DD]
═══════════════════════════════════════════════════════════════

BUSINESS CONTEXT
Use Case: [One-sentence: what problem does it solve?]
Decision Supported: [Who decides? Human or autonomous?]
Customer Impact: [Materiality: eligibility / pricing / access / none]
Regulatory Framework: [FCA, PRA, GDPR, etc.]
Accountable Executive: [Name, Title]

AI SYSTEM
Model Type: [LLM / classifier / agent / ensemble / other]
Provider: [Internal / OpenAI / Anthropic / other]
Adaptation: [Fine-tuned? RAG? Custom tools?]
Human Role: [Advisory / approver / exception handler / post-audit]

DEPLOYMENT ENVIRONMENT
Staging: [Yes/No — representative of production?]
Production: [Cloud provider / data residency]
Monitoring: [KPIs tracked; alerting in place?]
Incidents: [Last 12 months: [count] incidents; escalation procedure documented]

PRELIMINARY RISK TIER (to be confirmed in Phase 2):
[ ] Tier 0  [ ] Tier 1  [ ] Tier 2  [ ] Tier 3

CRITICAL QUESTIONS FOR PHASE 2:
1. [Domain expert question e.g., "Are vulnerable customers affected?"]
2. [Reviewer question e.g., "Is RAG data source controlled?"]
3. [Regulatory question e.g., "Does PRA model risk governance apply?"]

Prepared by: [Name]  |  Sponsor Review: [ ] Approved
═══════════════════════════════════════════════════════════════
```

### Gate 1: Intake Complete
**Decision:** Proceed to Phase 2 (Materiality Assessment)
**Gate Owner:** Sponsor + Engagement Lead
**Criteria:**
- Deployment Profile complete and sponsor-reviewed
- Critical questions identified
- No blockers to proceeding (e.g., no "system not yet built" or "scope undefined")

---

## Phase 2: Materiality Assessment

### Objective
Apply TIERING_MODEL.md to determine AI Risk Tier. Tier determines scope of IRQ assessment, evidence levels, opinion type, and engagement duration.

### Process

**Step 1: Score Five Factors**
- Customer Impact (1–4)
- Financial Impact (1–4)
- Regulatory Impact (1–4)
- Autonomy Level (0–5, normalized to 1–4)
- System Complexity (0–5, normalized to 1–4)

Use TIERING_MODEL.md definitions and worked examples; involve domain expert to ground scoring.

**Step 2: Calculate Composite Risk Score**
```
Risk Score = 
  (Customer Impact × 0.25) + 
  (Financial Impact × 0.25) + 
  (Regulatory Impact × 0.25) + 
  (Autonomy normalized × 0.125) + 
  (Complexity normalized × 0.125)
```

**Step 3: Check Override Triggers**
- Vulnerable customer exposure? Bump up 1 tier.
- Regulatory feedback history? Bump up 1 tier.
- Emerging technology risk? Bump up 1 tier.
- Other? (See TIERING_MODEL.md section: Override Triggers)

**Step 4: Assign Tier**
Map Risk Score to tier (Tier 0–3 per TIERING_MODEL.md).

### Deliverable: Materiality Assessment Summary

Document:
- Five-factor scores with rationale per factor
- Composite Risk Score calculation
- Override conditions (if any)
- Final Tier assignment
- Scope of IRQ assessment (which domains in scope)
- Engagement duration estimate
- Evidence-level minimums per tier

### Gate 2: Materiality Assessment & Tier Locked
**Decision:** Proceed to Phase 3 (Threat & Failure Analysis)
**Gate Owner:** Assurance Lead (or Sponsor for urgent engagements)
**Criteria:**
- Tier assignment justified and documented
- All five factors scored with rationale
- Override triggers reviewed
- Scope of IRQs locked (no future scope changes without re-tiering)
- Engagement plan (duration, team, budget) approved

---

## Phase 3: Threat & Failure Analysis

### Objective
Conduct a joint workshop with domain expert (business owner, process subject-matter expert) and AI reviewer to build failure trees: Business Objective → AI Function → AI Behaviour → Failure Modes → Consequences. This grounds IRQ prioritisation in business risk, not technical curiosity.

### Workshop Structure

**Part A: Business Objectives (Domain Expert)**
- "What are the 5–10 key decisions this process makes?"
- "What are the worst outcomes if a decision is wrong?"
- "Which decisions are most material to the business?"
- Example: Lending: "Decisions: approve/decline/tier. Worst outcome: approve bad credit (loss). Material: yes."

**Part B: AI Functions (AI Reviewer)**
- "What does the AI do in the workflow?"
- "What does the AI output look like? (score, classification, ranking, recommendation)"
- "How does human use the output?" (override, approve, exception-handle, accept as-is)
- Example: "System outputs credit score 650–850. Underwriter approves if >700."

**Part C: AI Behaviours (Joint)**
- "What could the AI do differently than expected?"
- "Are there edge cases where behaviour diverges from training?"
- Example: "System hallucinates customer data from similar names. System lacks context on recent life events (job loss, bankruptcy)."

**Part D: Failure Modes (AI Reviewer)**
- "How does behaviour cross the unsafe boundary?"
- "What are the ways confidence becomes unsafe?"
- Example: "System confidently recommends approval for customer with recent CCJ (confident hallucination of creditworthiness)."

**Part E: Consequences (Domain Expert)**
- "What is the business/customer/regulatory impact?"
- Example: "Wrong approval → customer in unaffordable debt → regulatory breach (affordability) → FOS complaint → capital charge."

### Deliverable: Failure Trees (Per Business Objective)

**Template:**

```
BUSINESS OBJECTIVE: Approve/decline credit for SME lending
│
├─ DECISION: Approve if system score >750
│  │
│  ├─ AI BEHAVIOUR: System scores applicant based on financial history
│  │  │
│  │  ├─ FAILURE MODE: System hallucinates customer creditworthiness
│  │  │                (confident score based on fabricated data)
│  │  │  └─ CONSEQUENCE: Approve unaffordable loan → customer default
│  │  │                  → regulatory breach → FOS complaint
│  │  │                  → Tier: Customer impact 4, Financial 4, Regulatory 4
│  │  │                  → IRQs: IRQ-MOD-004 (hallucination), IRQ-DAT-003 (data quality),
│  │  │                          IRQ-HUM-004 (escalation), IRQ-CON-005 (financial exclusion)
│  │  │
│  │  └─ FAILURE MODE: System confidence miscalibrated
│  │                   (score high but reliability low)
│  │     └─ CONSEQUENCE: Approve borderline credit → customer struggle
│  │                     → complaint → reputation damage
│  │                     → IRQs: IRQ-MOD-006 (confidence calibration)
│  │
│  └─ FAILURE MODE: System over-relies on single weak signal
│                   (e.g., recent industry switch)
│     └─ CONSEQUENCE: Approve risky credit → loss → capital impact
│                     → IRQs: IRQ-DAT-006 (ingestion and curation integrity), IRQ-MOD-010 (robustness to shift)
│
└─ DECISION: Decline if system score <700
   │
   └─ FAILURE MODE: System cannot adapt to changed circumstances
                    (customer recovering after historic default)
      └─ CONSEQUENCE: Decline creditworthy applicant → customer friction
                      → regulatory fairness concern (opportunity)
                      → IRQs: IRQ-DAT-007 (retrieval currency), IRQ-CON-003 (fairness)
```

### Phase 3 Prioritisation

For each failure mode, assign **priority** based on:
1. **Severity:** Impact on customer/firm (high/medium/low)
2. **Likelihood:** How easily could this happen in production? (high/medium/low)
3. **Detectability:** How easy is it to catch (with current controls)? (easy/medium/hard)

**Priority = Severity + Likelihood − Detectability** (conceptually; use FAIAS 5-axis risk weighting if finer granularity needed)

### Deliverable: Prioritised IRQ Set

**Output:**
- List of IRQs in scope for this engagement (selected from the full FAIAS battery — 109 IRQs as at v1.2.0; see IRQ_REGISTER.md)
- IRQs ranked by priority (high → medium → low)
- Cross-domain chains identified (e.g., data poisoning → model hallucination → human accept → customer loss)

### Gate 3: Failure Analysis & IRQ Set Locked
**Decision:** Proceed to Phase 4 (Evidence & Testing)
**Gate Owner:** Domain Expert + Assurance Lead
**Criteria:**
- Failure trees documented (business objective → failure mode → consequence)
- All critical failure modes identified
- IRQ set prioritised
- Cross-domain chains documented
- No unaddressed failure modes

---

## Phase 4: Evidence & Testing

### Objective
Execute non-production testing per Component 5 Testing Playbook, collect evidence per Component 4 Evidence Catalogue, and assign evidence levels (L1–L5) and testing confidence (★1–★5).

### Process per Tier

**Tier 0:**
- Design review only (no testing)
- Governance documentation audit (policy, roles)
- Evidence level: L2

**Tier 1:**
- Staged testing for priority IRQs (not exhaustive)
- Evidence: L3 (design + demo)
- Testing confidence: ★3–★4 where available; ★1–★2 procedures run with disclosure (PLAYBOOK_OVERVIEW.md §8)

**Tier 2:**
- Comprehensive staged testing (all IRQs in scope)
- Benchmarked test methods (OWASP, NIST)
- Evidence: L4 (independent testing)
- Testing confidence: ★4 or above on material tests for reasonable assurance; a material test rated ★1–★3 runs with disclosure, and the opinion is then given at limited assurance

**Tier 3:**
- Exhaustive staged testing (all IRQs, multiple tests per IRQ)
- L4 evidence from staging
- L5 evidence post-deployment (operational validation)
- Testing confidence: ★4 or above on all material tests for reasonable assurance; otherwise as Tier 2

### Deliverable: Evidence Catalogue (Component 4)

Structured inventory of all evidence collected, per FAIAS template:
- Policy & governance documents
- Technical design
- Testing results (per IRQ, per test)
- Monitoring data
- Third-party attestations

**Evidence tagging:**
- L1 (assertion), L2 (documentation), L3 (demo), L4 (independent test), L5 (operational)
- Confidence rating (★1–★5)
- Which claim(s) does evidence support?

### Gate 4: Testing Complete & Evidence Catalogued
**Decision:** Proceed to Phase 5 (Claims Assessment & Opinion)
**Gate Owner:** QA Lead
**Criteria:**
- All priority IRQs tested
- Evidence levels assigned per METHODOLOGY_STANDARDS.md
- Testing confidence rated (★1–★5)
- No critical gaps in evidence (L1–L2 only on low-priority IRQs)
- Test results peer-reviewed

---

## Phase 5: Claims Assessment & Opinion

### Objective
Evaluate each core assurance claim against evidence and test results. Determine which claims are supported, which have conditions, which fail. Form independent assurance opinion (four-box conclusion).

### Process

**Step 1: Claims-to-IRQ Mapping**
- Every core claim must be supported by ≥1 IRQ (two-way mapping per ASSURANCE_ARCHITECTURE.md mandatory completeness rule)
- For each claim, list supporting IRQs and their test results

**Step 2: Per-Claim Assessment**
For each claim:
- Did supporting IRQs pass testing? (Yes/No/Conditional)
- Is evidence level sufficient? (L4–L5 on core claims for Tier 2–3)
- Any testing confidence concerns? (Low ★1–★2 confidence?)
- Residual risk: what risk remains after control validation?

**Step 3: Materiality Screening**
Per ASSURANCE_ARCHITECTURE.md section 3 (10 materiality lenses):
- Assess each finding against all 10 lenses
- Material findings (material on ≥1 lens, per ASSURANCE_ARCHITECTURE's escalation rule): escalate to opinion
- Non-material findings: relay to lifecycle monitoring

**Step 4: Opinion Formation**
Select one of four conclusions per OPINION_TEMPLATE.md:
1. **Should Proceed** — No material deficiencies
2. **Should Proceed With Conditions** — Conditions specified; must be met within timeline
3. **Should Not Proceed** — Material deficiencies require remediation
4. **Unable to Form Opinion** — Insufficient evidence

For conditions, document:
- Specific requirement (not vague)
- Success criteria (testable)
- Target date
- Who verifies satisfaction

**Step 5: Review Confidence Assessment**
Assign High/Medium/Low review confidence per ASSURANCE_ARCHITECTURE.md (an internal assessment, never issued as a grade; the issued report carries the statement on the basis of the review, OPINION_TEMPLATE.md Part G):
- High = mature methods, L4–L5 evidence, ★4 tests
- Medium = emerging techniques, mixed evidence
- Low = frontier capability, ★1–★2 tests

### Deliverable: Independent Assurance Opinion (Component 7)

Per OPINION_TEMPLATE.md:
- Scope & limitations
- Assessment approach
- Assurance claims summary table
- Materiality-screened findings
- Conditions (if any)
- Four-box opinion
- Statement on the basis of the review (Part G)
- Regulatory alignment
- Basis of opinion

### Gate 5: Opinion Drafted & Peer-Reviewed
**Decision:** Present to sponsor
**Gate Owner:** QA Lead + Assurance Lead
**Criteria:**
- Opinion signed by authorized auditor (independence confirmed)
- Claims-IRQ mapping complete (no orphans)
- Conditions are specific and verifiable
- Opinion conclusion is defensible (evidence supports conclusion)
- Review confidence statement aligns with evidence levels and test confidence
- **The quality-control review was performed to a stated scope**, covering each of: discussion of the significant matters with the engagement lead (the standard's engagement partner); review of the subject-matter information and the proposed report; review of selected engagement documentation relating to the significant judgements made and the conclusions reached; and evaluation of the conclusions reached in formulating the report and of whether the proposed report is appropriate to those conclusions. [Scope follows ISAE 3000 (Revised) para 36(b)(i)–(iv), pp.14–15; FAIAS applies it to every engagement, where the standard requires it only where law, regulation or the firm's own determination calls for a review.]
- **The reviewer was independent of the engagement team** whose judgements are being evaluated, and that independence is recorded in the same terms as the signing auditor's.
- **The report is not dated before the review is complete.** [ISAE 3000 (Revised) para 36(a).]
- **The reviewer's concurrence is recorded as an independent check, not as corroborating evidence for the conclusion.** Agreement between the engagement team and the reviewer is evidence of consistency, not of correctness (ASSURANCE_MODEL.md §7A).

---

## Phase 6: Continuous Assurance & Lifecycle Governance

### Objective
Establish post-deployment monitoring, define re-assessment triggers, and manage system through its operational lifecycle (Design → Build → Validate → Deploy → Monitor → Change → Retire).

### Continuous Assurance Plan

**Early-Life Monitoring (Weeks 1–12 Post-Deployment)**
For Tier 2–3 systems, weekly operational dashboards:
- Key performance indicators (KPIs per claim)
- Escalation alerts (thresholds that trigger incident response)
- Override rate analysis (is human actually able to override?)
- Monitoring data feeds into operational evidence (L5) for annual reassessment

**Periodic Assurance (Annual Minimum)**
- Full reassessment for Tier 3 (highest risk)
- Refresh assessment for Tier 2 (test subset of IRQs; review monitoring data)
- Attestation for Tier 1
- Policy review for Tier 0

**Major-Change Re-Assessment Triggers** (tied to IRQ-GOV-012 envelope drift):

1. **Model Version Change** — New base model or fine-tuning on new data → trigger re-test of model-domain IRQs (B series)
2. **Training Data Change** — New data source or rebalancing → trigger re-test of data IRQs (A series) + fairness IRQs (H series)
3. **Decision Logic Change** — Threshold adjustment, feature weighting change → trigger re-test of model + human oversight IRQs
4. **Operating Envelope Expansion** — New customer segment, new use case, increased autonomy → trigger full re-assessment (all domains)
5. **Tool/API Access Change** — New integrations, new external data sources → trigger security + third-party IRQs (E, F series)
6. **Governance Change** — Changed escalation procedure, changed accountability → trigger governance IRQs (I series)
7. **Incident Triggering Material Finding** — Incident revealing control failure → trigger immediate re-assessment of affected claims

**Lifecycle Phases:**

| Phase | Assurance Activities | Gate Criteria |
|---|---|---|
| **Design** | IRQ scoping, failure tree workshop | Threat analysis complete |
| **Build** | Architecture review, control design validation | Design meets assurance objectives |
| **Validate** | Phase 4–5 testing, evidence collection, opinion formation | Opinion issued; conditions (if any) met |
| **Deploy** | Pre-go-live confirmation, monitoring setup | Monitoring dashboard live |
| **Monitor** | Weekly KPI tracking, early-life analysis (weeks 1–12), escalation response | KPIs within expected ranges; escalations managed |
| **Change** | Re-assessment trigger evaluation; if triggered, return to Scoping (Phase 2) | Change approved against updated risk profile |
| **Retire** | Archival of evidence, lessons learned documentation | System decommissioned; knowledge captured |

### Deliverable: Continuous Assurance Plan

Document:
- KPIs to monitor (per claim)
- Escalation thresholds (what value triggers alert)
- Monitoring cadence (weekly, monthly, quarterly)
- Annual re-assessment schedule
- Major-change escalation procedures
- Roles (who monitors, who decides re-assessment need, who sponsors changes)
- Contact information for assurance updates/re-engagement

### Gate 6: Continuous Assurance & Lifecycle Active
**Decision:** Engagement closed (ongoing monitoring begins)
**Gate Owner:** Operational owner (firm-side) + Assurance Lead
**Criteria:**
- Monitoring dashboard implemented
- KPI alerts configured
- Escalation procedures documented
- Annual re-assessment scheduled
- All stakeholders briefed on re-assessment triggers

---

## Key Tools & Artefacts per Phase

| Phase | Primary Artefacts | Referenced FAIAS Components |
|---|---|---|
| **Phase 1** | AI Deployment Profile | Intake checklist (new) |
| **Phase 2** | Materiality Assessment Summary | TIERING_MODEL.md |
| **Phase 3** | Failure Trees, Prioritised IRQ Set | IRQ_TEMPLATE.md, ASSURANCE_MODEL.md (failure chains) |
| **Phase 4** | Evidence Catalogue, Test Results | Component 4, Component 5, METHODOLOGY_STANDARDS.md (evidence levels, testing confidence) |
| **Phase 5** | Independent Assurance Opinion | OPINION_TEMPLATE.md, ASSURANCE_ARCHITECTURE.md (claims, materiality) |
| **Phase 6** | Continuous Assurance Plan, Monitoring Dashboard | ASSURANCE_ARCHITECTURE.md (lifecycle) |

---

## Governance & Escalation

### Escalation Triggers (Stop & Escalate to Sponsor)
- Material control gaps that can't be remediated pre-deployment
- Inability to access test environment or critical evidence
- Regulatory feedback during engagement (change engagement scope)
- Sponsor conflict-of-interest (e.g., sponsor incentivized to downplay risk)
- Technical risk too novel to assess (insufficient research base)

### Role Definitions

- **Engagement Lead:** Overall engagement delivery, sponsor communication, timeline management
- **Assurance Lead:** Phases 2, 5; claims framework, opinion formation, review confidence
- **Testing Lead:** Phase 4; test design, execution, evidence collection
- **Domain Expert:** Phase 3; failure tree workshop; business risk interpretation
- **QA Lead:** Quality gates, peer review of assessment and opinion
- **Sponsor:** Business owner at the firm; receives the opinion and owns the deployment decision
- **Firm-side owners (Risk Architect, Operations, Operational owner):** the firm's own staff who hold a named phase or gate jointly with the Assurance Lead; they are not part of the review team

---

