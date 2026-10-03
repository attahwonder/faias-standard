# COMPONENT TEMPLATES — FAIAS Assurance Architecture

## Governance

This document outlines the structure for each of FAIAS's 7 assurance components. The templates for Components 4, 6 and 7 are non-normative: they illustrate one use of FAIAS and are not requirements of the standard. FAIAS draws on the conclusion forms of ISAE 3000 (Revised); it does not make an engagement ISAE-conformant, and a practitioner who reports under ISAE 3000 must meet that standard in full.

FAIAS comprises 7 interlinked components that together support an independent assurance opinion on whether an AI system should proceed to deployment. Components are published as distinct volumes but function as an integrated system.

---

## General Publication Standards

- **Page layout:** A4 (210 × 297 mm), 12pt body text, 1.5 line spacing
- **Margins:** 20mm top/bottom, 25mm left/right
- **Headers/Footers:** Component title, chapter, page number
- **Cross-references:** Hyperlinked (internal) and numbered references between components
- **Table of Contents:** Auto-generated with page numbers
- **Bibliography:** Centralised per component, alphabetical with access dates
- **Figures & Tables:** Numbered sequentially, with captions and source attribution
- **Tone:** Professional, concise, analytical; no marketing language
- **Language:** UK English

---

## Component 1: AI Taxonomy (Research-Backed Standard)

**Ownership:** the maintainer  
**Audience:** adopters, sponsors, regulators  
**Length:** 60–80 pages  

### Purpose
Component 1 establishes the authoritative taxonomy of AI risks — the domains and subdomains under which every IRQ is classified — grounded in industry standards and frontier research findings. Regulation is not part of the taxonomy: it is mapped in the regulatory crosswalk (`V5_Regulatory_Crosswalk/`). The taxonomy is the foundation for all downstream assurance work.

### Structure

#### Front Matter
- Cover page (title, version, date, custodian, classification)
- Executive summary (1 page; key findings from frontier lab and incident research)
- Table of Contents

#### Part A: Regulation (by reference)
Not restated in this volume. Regulation is mapped in the regulatory crosswalk (`V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md`).

#### Part B: Industry Standards & Frameworks
1. **NIST AI Risk Management Framework (v1.0, Jan 2023; NIST's stated review point no later than 2028)**
   - Core functions (GOVERN, MAP, MEASURE, MANAGE)
   - Alignment with NIST Cybersecurity Framework
   - Adoption by financial institutions

2. **ISO/IEC Standards**
   - ISO 27001:2022 (Information Security Management)
   - ISO 42001:2023 (AI Management System)
   - ISO 31000:2018 (Risk Management)
   - ISO/IEC 24029 series (assessment of the robustness of neural networks)

3. **OWASP**
   - Top 10 for LLM Applications (2025)
   - API Security Testing Guide (adapted for AI/LLM)
   - Threat modeling frameworks

4. **Industry Working Groups**
   - IEEE AI Governance (IEEE 7000 series standards)
   - Cloud Security Alliance (CSA AI governance)
   - Financial Stability Board (FSB) recommendations

#### Part C: Frontier Research & Threat Landscape
1. **Frontier Lab Publications**
   - Anthropic, DeepMind, OpenAI, Meta research papers (2023–2025)
   - Key findings on prompt injection, model robustness, alignment
   - Emerging attack vectors and defences

2. **Academic Research**
   - Peer-reviewed research on adversarial attacks, model poisoning, extraction
   - Conferences: NeurIPS, ICML, ICLR, EMNLP, ACL (AI security/robustness tracks)
   - Key authors and research groups

3. **Public Incident Reports**
   - NTSB, MITRE ATLAS incident database
   - Published security advisories (CVE, CWE)
   - Financial institution public disclosures (SEC, FCA filings)
   - Case studies: what went wrong, technical root causes, control failures

#### Part D: Synthesis & Gaps
1. **Convergence Points**
   - Regulatory expectations vs. frontier research (alignment and gaps)
   - Standards maturity vs. practice readiness
   - High-risk domains where regulation lags research (or vice versa)

2. **Open Questions**
   - Where no published standard exists yet
   - Emerging risks without established testing methods
   - Regulatory ambiguities and how institutions interpret them

3. **FAIAS Response**
   - How FAIAS taxonomy and IRQs address these gaps
   - Emerging practice controls (explicitly flagged)
   - Forecast: where research/standards likely to move

#### Back Matter
- Full Bibliography (alphabetical, with access dates; sourced from Parts B–C)
- Abbreviations & Glossary
- Document history / version control

---

## Component 2: IRQs (Independent Review Questions Battery)

**Ownership:** the maintainer  
**Audience:** Risk committee, compliance, internal audit  
**Length:** 60–80 pages  

### Purpose
Component 2 is the complete IRQ Battery: all Independent Review Questions (109 as at v1.2.0) formatted as Review Canvases per IRQ_TEMPLATE.md. It serves as the operational definition of FAIAS assurance scope and materiality.

### Structure

#### Front Matter
- Cover page
- Executive summary (key IRQ threat landscape ranked by regulatory/business impact and frequency)
- Table of Contents
- IRQ taxonomy overview (diagram linking to ID_SCHEME domains → subdomains → IRQs)
- Metrics: 9 domains, 44 subdomains, 109 IRQs, 300–500+ primary sources

#### Part A: IRQ Taxonomy by Domain & Subdomain
One section per domain (9 sections), subdivided by subdomain (44 total):

**Template per domain section:**
1. **Domain Overview** (e.g., "Model Risks in AI Systems [MOD Domain]")
   - Definition and scope
   - Why this domain matters (regulatory, operational, financial impact)
   - Typical deployment contexts in financial services
   - List of subdomains within this domain (e.g., B.1 Capability Uncertainty, B.2 Hallucination, B.3 Calibration, etc.)

2. **Per-Subdomain Threat Hierarchy** (visual: threat → consequence)
   - List of threats specific to subdomain (what can go wrong)
   - Common failure modes
   - Cascading effects (e.g., fine-tuning drift → escalation failure → regulatory sanction)

3. **Subdomain IRQ Summary Cards** (one or more per subdomain; 109 total as at v1.2.0)
   - **IRQ ID & Subdomain** (e.g., "IRQ-MOD-004 [B.2]: Hallucination-Driven Customer Decline")
   - **Review Question** (1–2 sentences; auditable phrasing)
   - **Why This Matters** (regulatory/business context)
   - **Failure Modes** (bullet list)
   - **Regulatory Basis** (citation to FCA, NIST, Basel, ISO, etc.)
   - **Research Basis** (frontier lab or peer-reviewed research citation)
   - **Related IRQs** (links to other subdomains/domains that share dependencies or consequences)

#### Part B: Cross-Domain/Subdomain IRQ Scenarios
1. **System Failure Cases**
   - Example: RAG system manipulated via data poisoning → Model output biased → Leads to discriminatory lending decisions → Regulatory breach + reputational damage
   - Chains IRQs from A.3 (Data, Retrieval Data) → B.2 (Model, Hallucination) → H.1 (Conduct, Discrimination & Proxy Bias) → I.2 (Governance, Approval, Tiering & Policy)

2. **Third-Party Compromises**
   - Scenario: SaaS model provider hacked → Model weights extracted/corrupted → Agentic system fails to escalate → Governance breakdown
   - Links IRQs: F.1 (Third Party, Due Diligence, Contracts & Licensing) → E.3 (Security, Supply Chain & Tool Security) → C.2 (Agentic, Tool Use) → I.3 (Governance, Validation & Oversight)

#### Part C: IRQ Prioritisation Matrix
- **Heat map:** Business Impact (y-axis) vs. Regulatory Materiality (x-axis)
- Domains/Subdomains colour-coded
- Callout: highest-priority IRQs (typically Tier 1 test priorities in Component 5)

#### Back Matter
- Risk rating definitions (Impact, Likelihood scale)
- Bibliography (references to regulatory/research sources for each threat)
- Related controls mapping (which Component 5 controls address each risk)

---

## Component 3: Assurance Claims

**Ownership:** Assurance Lead  
**Audience:** Audit committee, compliance, regulators  
**Length:** 30–50 pages  

### Purpose
Component 3 documents the Claims-Argument-Evidence (CAE) chains that form the backbone of the independent assurance opinion. It translates IRQ findings into structured claims about system safety and control effectiveness, which support the opinion in Component 7.

### Structure

#### Front Matter
- Cover page
- Executive summary (key assurance claims ranked by criticality; preliminary opinion category)
- Table of Contents

#### Part A: Assurance Claims Framework
1. **Core Assurance Claims** (5–10 major claims)
   - Example claim: "The system only accesses authorised information sources within the designed operating envelope."
   - Example claim: "Human reviewers maintain genuine independent review capacity without automation bias."
   - Example claim: "Escalation failures are detected and prevent customer-impacting decisions."

2. **Claim-to-IRQ Mapping Matrix**
   - Two-way mapping: every claim is supported by ≥1 IRQ; every IRQ supports ≥1 claim
   - Mandatory completeness: no orphan claims, no orphan IRQs
   - Example:
     | Core Claim | Supporting IRQs | Test Status | Materiality |
     |---|---|---|---|
     | System accesses only authorised sources | IRQ-DAT-003, IRQ-DAT-006, IRQ-SEC-004 | Passed | Core |
     | Escalation prevents wrong decisions | IRQ-HUM-007, IRQ-HUM-008 | Passed | Core |

3. **Claim Weighting Rule**
   - A failed IRQ is material (impacts opinion) only if it undermines a core claim with no alternative control
   - Example: "IRQ-MOD-004 (hallucination detection) failed → Undermines claim 'System confidence calibration prevents false acceptance.' → Remediation required before deployment opinion."
   - Example: "IRQ-MOD-015 (capability uncertainty) flagged as inconclusive → Does not undermine claim, because escalation controls (IRQ-HUM-007) compensate → Opinion includes condition."

#### Part B: Materiality-Screened Findings

**10 Materiality Lenses** (per ASSURANCE_ARCHITECTURE.md section 3):
1. Customer Outcomes — does finding risk customer harm or service denial?
2. Financial Statements — does finding impact financial reporting accuracy or reserve adequacy?
3. Prudential Safety — does finding risk capital adequacy, liquidity, or systemically unsafe behaviour?
4. Consumer Duty — does finding breach transparency, suitability, or fair value obligations?
5. Operational Resilience — does finding risk system availability, recovery time, or incident response?
6. Market Integrity — does finding risk front-running, market manipulation, or information asymmetry?
7. Financial Crime — does finding risk AML/CFT effectiveness or sanctions screening?
8. Data Protection — does finding breach subject rights, consent, or lawful processing?
9. Reputation — does finding risk brand, regulatory trust, or public confidence?
10. Third-Party Dependency — does finding risk vendor continuity, SLA compliance, or supply-chain breach?

For each IRQ finding:
- Assess against all 10 lenses
- Flag findings that are material on ≥1 lens, and escalate them to the opinion
- Non-material findings → relay to lifecycle monitoring; do not escalate to opinion

**Evidence:** Materiality-screening procedure checklist and findings summary table.

#### Part C: Conditions & Exceptions
1. **Conditional Passes** (systems recommended to proceed, subject to conditions)
   - Example: "Deployment recommended subject to conditions: confirm escalation threshold tuning within 30 days and monitor alert rates for 12 weeks. The firm's own approval authority decides."

2. **Major Exceptions** (control gaps with mitigants)
   - Example: "Confirm testing infrastructure availability. Mitigant: weekly monitoring dashboard in place until infrastructure stabilized."

#### Back Matter
- Claim definitions (1-paragraph description of each core claim)
- IRQ → Claim traceability matrix (full detail)
- Definitions: reasonable assurance vs. limited assurance

---

## Component 4: Evidence Catalogue

**Ownership:** Testing Lead  
**Audience:** Audit teams, compliance, institutional repository  
**Length:** 20–40 pages (plus attachments)  

### Purpose
Component 4 is the centralised repository and inventory of all evidence collected during the assurance engagement. It supports transparency, auditability, and ongoing lifecycle monitoring.

### Structure

#### Front Matter
- Cover page
- Guide to using the catalogue (how evidence is organised, access protocols)
- Table of Contents

#### Part A: Evidence Categories
1. **Policy & Governance Documents**
   - AI governance policy, approval workflows, roles
   - Risk appetite statement for AI
   - Third-party vendor assessment policy

2. **Technical Design & Architecture**
   - System architecture diagrams (model, data, integrations)
   - Deployment configuration (staging, production)
   - Security controls architecture

3. **Training & Competence**
   - Training records for AI governance roles
   - Competence assessments (regulators may require demonstrated understanding)

4. **Testing & Validation**
   - Test plans, test cases, test execution logs
   - Test results summary (pass/fail rates, remediation status)
   - Peer review evidence (test method reviewed and approved)

5. **Monitoring & Incident Response**
   - Monitoring alerts and thresholds (drift detection, anomaly detection)
   - Incident logs (last 12 months)
   - Post-incident reviews and corrective actions

6. **Vendor Management**
   - Third-party risk assessments (model providers, data brokers, SaaS tools)
   - SLA compliance tracking
   - Supply-chain security validation

#### Part B: Evidence Inventory
Structured table (per IRQ or per subdomain):

| IRQ ID | Subdomain | Evidence Type | Evidence Title | Location/Reference | Last Updated | Status (Complete/Gap) | Evidence Level |
|---|---|---|---|---|---|---|---|
| IRQ-MOD-004 | B.2 | Test Plan | Hallucination Rate Test Suite | /path/to/test_plan.docx | 2026-07-15 | Complete | L4 |
| IRQ-MOD-004 | B.2 | Test Results | Hallucination Validation (Run 2026-07-14) | /audit/results/hallucination_2026-07-14.xlsx | 2026-07-14 | Complete | L4 |
| IRQ-MOD-004 | B.2 | Architecture | Model Confidence Filtering Design | /systems/model_design_v3.pdf | 2026-06-01 | Complete | L2 |
| IRQ-DAT-007 | A.3 | Policy | Retrieval Data Curation & Staleness Policy | /governance/data_sourcing_v2.docx | 2026-05-30 | Complete | L2 |

#### Part C: Evidence Gaps
- Identify missing evidence against IRQs (per subdomain and domain)
- Prioritise remediation by regulatory materiality (linked to remediation plan in Component 7)

#### Back Matter
- File directory / access log
- Data retention policy for evidence (how long archived)
- Bibliography (if evidence sources cited)

---

## Component 5: Testing Playbook

**Ownership:** the maintainer  
**Audience:** Internal audit, external audit, testing teams  
**Length:** 100–150 pages  

### Purpose
Component 5 is the complete specification of all testing procedures, test environments, success criteria, and evidence collection protocols. It implements the FOUR-TEST discipline and testing-confidence framework (★1–★5).

### Structure

#### Front Matter
- Cover page
- Executive summary (testing approach, methodology governance, FOUR-TEST discipline)
- Table of Contents
- Non-Production Assurance Covenant (statement that testing executes only in non-production environments; where evidence derives from the firm's own controlled resilience exercises or from read-only production records, the report states so expressly)
- IRQ Testing Roadmap (phased testing schedule by domain/subdomain priority)

#### Part A: Testing Governance
1. **Testing Principles**
   - Isolation (test environment separated from production)
   - Non-invasiveness (synthetic data, no live customer data)
   - Repeatability and auditability
   - FOUR-TEST discipline (every IRQ must pass plausibility gate before testing)
   - Escalation procedures (if test uncovers production issue)

2. **Test Environment Setup**
   - Architecture (staging, sandboxed model instances, synthetic retrieval sources)
   - Data requirements (data use policy, anonymisation, retention)
   - Access controls (who runs tests, approval workflows)
   - Documentation requirements (test plans, results logging, FOUR-TEST validation records)

3. **Testing Roles & Responsibilities**
   - Test planner (IRQ test case design, acceptance criteria per IRQ)
   - Test executor (runs tests, documents observations, validates FOUR-TEST criteria)
   - Peer reviewer (validates test method, results interpretation, FOUR-TEST discipline)
   - Sponsor approval (sign-off before escalation to production team)

#### Part B: Domain/Subdomain-Specific Test Playbooks (9 sections, 44 subdomains)

**Template per subdomain playbook:**

1. **Domain & Subdomain Overview & Testing Strategy** (e.g., "Model Domain [MOD] > Hallucination [B.2]")
   - Why these IRQs matter in this subdomain (regulatory, operational impact)
   - High-risk areas (e.g., task drift in fine-tuning subdomain)
   - Testing limitations for this subdomain (e.g., reward drift detection has no published gold standard)
   - FOUR-TEST applicability (which criteria are strongest/weakest for this subdomain)

2. **IRQs & Test Cases** (one or more IRQs per subdomain)
   - One subsection per IRQ (IRQ-MOD-015, IRQ-MOD-016, etc.)
   - **IRQ ID, Subdomain & Title**
   - **Review Question** (1–2 sentences)
   - **Applicable Systems** (generative/agentic/predictive)
   - **Test Method** (cite benchmark if available; mark as Emerging if not)
   - **Testing Confidence Rating** (★1–★5 per ASSURANCE_MODEL.md section 6)
   - **Test Environment Requirements**
     - Staging systems needed
     - Synthetic data / test fixtures required
     - Model variants (base model, fine-tuned, etc.)
   - **Test Execution** (step-by-step procedure)
     - Preconditions (test setup, baseline)
     - Test steps (actions, inputs, expected behaviour)
     - Postconditions (cleanup, logging)
   - **Success Criteria** (quantitative thresholds)
     - Example: "Detection system must identify >95% of injection test cases with <5% false positive rate"
   - **Pass/Fail Indicators** (per IRQ template)
   - **Failure Modes & Troubleshooting**
     - What to do if test environment is unavailable
     - How to adapt test if system component is missing
   - **Evidence Collection** (logs, screenshots, outputs to archive per IRQ; tag with L1–L5 evidence level)
   - **Time & Resource Estimate** (hours, personnel, infrastructure cost)
   - **FOUR-TEST Validation** (confirm all four tests pass for this IRQ)

3. **Test Data Sets**
   - Synthetic test fixtures for this subdomain
   - Example payloads (prompt injections, adversarial inputs, malformed data)
   - Expected model responses (baseline)
   - Rationale for each test vector (why it matters per IRQ)

4. **Test Reporting Template**
   - Test execution date, tester name, system/version tested
   - Per-IRQ result (pass/fail/inconclusive)
   - Evidence summary (attached logs, screenshots, trace per IRQ)
   - Testing confidence assessment (was benchmark available or was methodology bespoke?)
   - FOUR-TEST validation record (re-confirm at execution time)
   - Residual findings (if control is partially working, what's the gap per IRQ?)

#### Part C: Cross-Subdomain/Domain Test Scenarios
1. **End-to-End Testing**
   - Example: Deploy system with all controls → Run integrated attack simulation → Verify escalation chain (A.3 Data Retrieval Data → B.2 Model Hallucination → D.3 Escalation & Override Design → I.3 Validation & Oversight)
   - Measures control interaction and completeness across IRQs

2. **Failure Injection**
   - Disable one IRQ's control → Test how other IRQs' controls compensate
   - Identifies single points of failure and control dependencies

#### Back Matter
- Test environment architecture diagram
- Data use policy for testing
- Test tool inventory (frameworks, libraries, scanners)
- Bibliography (citations to OWASP, NIST testing guides, research methods)

---

## Component 6: Safety Case

**Ownership:** the maintainer  
**Audience:** Governance committee, regulators, deployment decision-makers  
**Length:** 40–60 pages  

### Purpose
Component 6 presents the structured safety argument (per ISO/IEC 15026-2, Goal Structuring Notation) that underpins the independent assurance opinion. It declares the operating envelope, names key risk vectors, and documents the assurance lifecycle.

### Structure

#### Front Matter
- Cover page
- Executive summary (safety case top-level claim; envelope declaration; lifecycle stage)
- Table of Contents

#### Part A: System Description & Operating Envelope
1. **System Scope**
   - What the AI system is (model type, inputs, outputs, integrations)
   - Deployment context (business activities, decision type, human roles)
   - Technology stack and dependencies

2. **Operating Envelope: Designed-For Declaration**
   - Explicit list of conditions the system is designed to operate within
   - Example: "Designed for: lending decisions on credit applications from UK residents, using bank-supplied credit files dated <30 days, customer-provided employment history, and publicly available regulatory databases. Model accepts applications with >50% documented customer data."

3. **Operating Envelope: NOT-Designed-For Declaration**
   - Explicit list of conditions outside system scope
   - Example: "NOT designed for: real-time fraud detection, continuous monitoring of >10,000 simultaneous transactions, use of third-party credit data with <7-day refresh cycles, or autonomous escalation without human review."

4. **Envelope Drift as Risk Vector**
   - Named risk: operating envelope gradually expands through business process change, vendor update, or user behaviour drift
   - Five of the six envelope-drift vectors (ASSURANCE_ARCHITECTURE.md also names capability drift):
     1. **Business Process Drift** — firm adds new use case without governance re-approval (e.g., model now used for salary verification)
     2. **User Behaviour Drift** — users override system recommendations more frequently, reducing effective control
     3. **Tool Integration Drift** — third-party tool connecting to system adds unapproved data source
     4. **Prompt Drift** — operational prompts modified without architecture review; system behaviour changes
     5. **Customer Segment Drift** — system deployed to customer segment with different risk profile than design assumption

#### Part B: Structured Safety Argument (Goal Structuring Notation)

**Top-Level Claim:** "This AI system is safe to deploy for [specific business activity] within the declared operating envelope, subject to stated conditions and monitoring protocols."

**Sub-claims (5–10 major claims):**
1. "System capability is bounded within tested limits"
2. "Human reviewers maintain independent decision authority without automation bias"
3. "Failure modes are detectable before customer impact"
4. "Escalation and override mechanisms prevent escalation failures"
5. "Monitoring alerts will detect operating envelope drift"

**Per claim: Argument chain**
```
Claim: System hallucination is sufficiently controlled
  ├─ Evidence 1: L4 independent testing shows <2% hallucination rate in scope
  ├─ Evidence 2: Confidence filtering deployed; L4 test validates >95% precision
  ├─ Evidence 3: Escalation workflow tested; L4 confirms no false acceptance
  ├─ Evidence 4: L2 policy; human reviewers trained; attendance audited
  └─ Assumption: Testing environment representative of production; data source freshness maintained
```

#### Part C: Assurance Lifecycle

**Eight-phase assurance lifecycle:**

1. **Design Phase** — AI system architecture and controls specified; IRQs scoped; testing plan drafted
2. **Architecture Review** — independent review of design against IRQs; design-phase controls validated; risk profile established
3. **Independent Testing** — non-production testing executed per Component 5 playbook; evidence collected (L4 where possible)
4. **Deployment Opinion** — this assurance engagement; opinion formed; conditions (if any) documented
5. **Early Life Monitoring** (Weeks 1–12 post-deployment) — control effectiveness monitored; key metrics tracked; envelope drift detected
6. **Periodic Assurance** (Annual or post-major-change) — full reassessment or refresh assessment; escalation procedure tested; monitoring data reviewed
7. **Major Change Review** — any material change to operating envelope, controls, or data sources triggers new assurance cycle
8. **Retirement** — system decommissioned; evidence archived; lessons learned documented

**Per phase: Gate criteria, decision-makers, evidence required, escalation triggers**

#### Part D: Mini Assurance Cases (Per Critical Claim)

For each core claim (e.g., "Hallucination is controlled"):

1. **Hazard** — What could go wrong? (hallucination + high confidence)
2. **Failure Modes** — How could hazard manifest? (confident hallucination of customer data; confident hallucination of transaction rules)
3. **Control** — What prevents it? (confidence filtering; human review escalation)
4. **Evidence** — How do we know? (test results; policy documents; training records)

**Hazard-Control-Evidence chain (per ISO 15026-2 structured argument)**

#### Back Matter
- Definitions: "reasonable assurance" (comprehensive controls, L4–L5 evidence, and no material claim resting on a test rated ★1–★3) vs. "limited assurance" (selective controls, emerging practice, mixed evidence, or a material claim resting on a test rated ★1–★3)
- Lifecycle monitoring dashboard specification (KPIs to track post-deployment)
- Envelope drift detection triggers (thresholds for re-assessment)

---

## Component 7: Independent Assurance Opinion

**Ownership:** Engagement Lead  
**Audience:** The commissioning firm (sponsor, board, audit committee); others only as named recipients, on the issuer's terms  
**Length:** 15–30 pages (concise, high-level; backed by Components 1–6)  

### Purpose
Component 7 is the formal Independent Assurance Opinion; it draws on the conclusion forms of ISAE 3000 (Revised), as the Governance note above states. It is the output that decision-makers use to evaluate deployment readiness.

### Structure

#### Front Matter
- Cover page (addressee, classification, distribution list, intended use, opinion date)
- Opinion Statement (1–2 paragraphs; headline conclusion)
- Table of Contents

#### Part A: Scope & Limitations
1. **Scope**
   - System(s) reviewed, deployment dates, versions
   - Review period and assessment dates
   - IRQs assessed (total count, domains)
   - Materiality threshold applied ("findings material on ≥1 materiality lens escalated to opinion")

2. **Limitations**
   - Reviewer testing in non-production environments only; any evidence from read-only production records or the firm's own controlled resilience exercises identified as such
   - Emerging practice controls flagged (methodology not yet standardised)
   - Third-party dependencies not directly tested (vendor attestations used)
   - Time-bound (opinion valid for X months; major changes trigger re-assessment)

#### Part B: Assessment Approach & Basis
1. **Methodology** — Reference FAIAS components; do not repeat detail
   - "We applied FAIAS standard, involving use of the taxonomy (Component 1), IRQ battery assessment (Component 2), claims evaluation (Component 3), evidence catalogue (Component 4), testing execution (Component 5), safety case review (Component 6), with regulation mapped through the regulatory crosswalk (`V5_Regulatory_Crosswalk/`)."

2. **Evidence Sources**
   - Design review findings (Component 3)
   - Testing results (Component 5)
   - Interviews
   - Regulatory alignment (regulatory crosswalk, `V5_Regulatory_Crosswalk/`)

#### Part C: Assurance Claims Assessment Summary

**Table: Claims Status**

| Core Claim | Material? | Test Status | Evidence Level | Confidence (internal working judgement; the issued report states ★) | Residual Risk | Opinion Impact |
|---|---|---|---|---|---|---|
| "System accesses only authorised sources" | Yes | Passed | L4 | High | Low | Supports "Should Proceed" |
| "Hallucination is detected before use" | Yes | Passed | L4 | High | Low | Supports "Should Proceed" |
| "Human reviewers maintain independent authority" | Yes | Inconclusive | L2–L3 | Medium | Medium | Condition: escalation threshold tuning |
| "Monitoring detects envelope drift" | Yes | Passed | L3 | Medium | Medium–Low | Supports "Should Proceed" |

#### Part D: Materiality-Screened Findings Summary
- High-impact material findings (linked to material claims)
- Medium-impact material findings (control gaps with mitigants)
- Low-impact findings (non-material; relegated to lifecycle monitoring)

#### Part E: Conditions (If Any)
- **Condition 1:** [Specific requirement and target date]
- **Condition 2:** [Specific requirement and target date]
- Example: "Confirm escalation threshold tuning within 30 days and provide evidence of 12-week monitoring data before expanding to customer segment B."

#### Part F: Independent Assurance Opinion (Four-Box Framework)

**Opinion Category:** One of four conclusions:

1. **Should Proceed** — Controls are designed sufficiently, and performed as designed in non-production testing; operating effectiveness in production is assessed at post-deployment re-assurance. No material deficiencies. Deployment recommended; the firm's own approval authority decides. Ongoing monitoring to continue per lifecycle plan.

2. **Should Proceed With Conditions** — System demonstrates sufficient control design. Conditions specified above are to be satisfied within stated timelines before deployment; the firm's own approval authority decides.

3. **Should Not Proceed** — System exhibits material control gaps that cannot be remediated pre-deployment without material redesign. Recommend suspension pending remediation and reassessment.

4. **Unable to Form Opinion** — Insufficient evidence or access prevented complete assessment. Recommend extended review period or enhanced testing scope.

**Per opinion category:**
- **Basis:** 1–2 sentences explaining key findings that drove the conclusion
- **Assurance level:** reasonable or limited; no reasonable assurance rests on a material test rated ★1–★3

#### Part G: Review Confidence Statement

**Form:** The statement on the basis of the review, in one of two narrative forms, (A) review conducted on the full evidential basis sought or (B) review conducted on a qualified evidential basis, with the coverage sentence (OPINION_TEMPLATE.md Part G). The internal High / Medium / Low assessment is never issued as a grade.

**Factors:**
- Maturity of testing methods (established benchmark vs. emerging practice)
- Evidence profile (L1–L2 assertion only vs. L4–L5 independent testing)
- Coverage (100% of risk domains tested vs. sampling)
- Frontier capability risks (novel attack vectors with no published defence)

#### Part H: Regulatory Alignment & Governance
1. **Compliance Status** (per major regulator)
   - Summary table: FCA / PRA / ECB / EU AI Act — compliant / conditionally compliant / non-compliant
   - Explanation (brief, 1–2 sentences per jurisdiction)

2. **Recommended Governance**
   - Frequency of re-assessment (annual, post-major-change, etc.)
   - Roles for ongoing monitoring
   - Board reporting cadence

#### Part I: Basis of Opinion
- Assurance methodology and standards applied
- Key assumptions (e.g., test environment representative of production; no major code changes post-testing)
- Professional responsibilities (auditor independence; conflict-of-interest statement; where the practitioner reports under ISAE 3000, the statements that standard requires)

#### Back Matter
- Acknowledgements (interviewees, design review participants)
- Limitations & Caveats (test environment only, emerging practice disclosed, scope boundaries)
- Appendix A: Glossary
- Appendix B: Detailed Findings (expanded deficiency narratives with evidence references)
- Appendix C: Regulatory Mapping (cross-reference to the regulatory crosswalk, `V5_Regulatory_Crosswalk/`)
- Appendix D: IRQ Status Summary (pass/fail/inconclusive per domain)
- Appendix E: Test Results Summary (reference to Component 5 playbook execution)

---

## Cross-Component Navigation

All components include **hyperlinked cross-references** to related content:
- Component 1 (Taxonomy) → Component 2 (IRQs) — "IRQs classified under this domain and subdomain"
- Component 2 (IRQs) → Component 5 (Testing Playbook) — "See test procedures for this IRQ"
- Component 3 (Claims) → Component 4 (Evidence Catalogue) — "Store evidence supporting this claim"
- Component 5 (Playbook) → Component 4 (Catalogue) — "Store test results and FOUR-TEST validation records here"
- Component 6 (Safety Case) → Component 2 (IRQs) — "IRQ status and control effectiveness mapped to safety claim"
- Component 7 (Opinion) → Component 3 (Claims) — "Opinion based on claims assessment; see summary table"

---

