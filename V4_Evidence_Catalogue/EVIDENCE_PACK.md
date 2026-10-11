# EVIDENCE_PACK.md — FAIAS Component 4 Mandatory Evidence Inventory

**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  
**Document Custodian:** the maintainer  
**Component:** Component 4 (Evidence Catalogue)

---

## Purpose

This document defines the mandatory evidence pack for FAIAS assurance engagements. Evidence is organised by category (Governance, Business, Model, Data, Security, Operations, Human Oversight) and mapped to:
- **Expected Evidence Level** (L1–L5 per ASSURANCE_MODEL.md section 5)
- **Assurance Claims Supported** (which core claims does this evidence substantiate?)
- **Tier Applicability** (which AI Risk Tiers require this evidence per TIERING_MODEL.md?)

Every FAIAS engagement produces an Evidence Catalogue (Component 4 deliverable) by collecting evidence per this pack template. The catalogue supports auditability, transparency, and regulatory confidence.

---

## Evidence Categories & Mandatory Items

### CATEGORY 1: GOVERNANCE

**Purpose:** Evidence that AI system ownership, accountability, and governance framework are clearly defined.

#### 1.1 AI Governance Policy
- **Description:** Firm-wide AI governance policy defining roles (model owner, escalation owner, compliance owner), approval workflows, monitoring responsibilities, incident escalation
- **Evidence Level:** L2 (design document)
- **Supporting Claims:** "System owner is defined and accountable"; "Governance structure is established"
- **Tier Applicability:** All tiers (Tier 0+)
- **Example Artefacts:** AI Governance Policy v[X], Board Resolution on AI Framework, SMCR Accountability Statement

#### 1.2 System Inventory & Classification
- **Description:** Formal inventory of AI systems in production, classified by Tier (per TIERING_MODEL.md), with business owner, model provider, approval date
- **Evidence Level:** L2 (operational record)
- **Supporting Claims:** "Governance covers all material systems"
- **Tier Applicability:** All tiers (Tier 0+)
- **Example Artefacts:** AI System Inventory Spreadsheet (updated quarterly), System Registration Form

#### 1.3 Accountability Model & SMCR
- **Description:** SMCR statement defining which exec is accountable for model risk governance; escalation path for material findings; delegation authority limits
- **Evidence Level:** L2 (governance document)
- **Supporting Claims:** "Accountability is clear and unambiguous"
- **Tier Applicability:** Tier 2–3 (Tier 0–1 may use functional delegation)
- **Example Artefacts:** SMCR Statement, Accountability Matrix, Delegation Letter

#### 1.4 Approval Records & Sign-Off
- **Description:** Documented approval for system to deploy (by sponsor, risk committee, regulatory function if required). Pre-deployment and post-condition-satisfaction approvals.
- **Evidence Level:** L2 (signed record)
- **Supporting Claims:** "Deployment was approved by competent authority"
- **Tier Applicability:** Tier 1+ (Tier 0 may use attestation)
- **Example Artefacts:** Board Paper, Risk Committee Minutes, Sponsor Sign-Off, Condition Satisfaction Letter

#### 1.5 Model Risk Governance Policy
- **Description:** Firm's model risk governance framework (per PRA SS1/23 where applicable; BCBS 239 where AI content feeds risk-data aggregation). Defines model types subject to governance, review frequency, escalation triggers.
- **Evidence Level:** L2 (policy document)
- **Supporting Claims:** "Model risk governance is proportionate and documented"
- **Tier Applicability:** Tier 2–3
- **Example Artefacts:** Model Risk Governance Policy, MRG Framework Document

---

### CATEGORY 2: BUSINESS

**Purpose:** Evidence that the business use case, customer impact, process integration, and regulatory obligations are clearly understood.

#### 2.1 Use Case Assessment
- **Description:** One-pager or brief document describing: business problem, how AI solves it, customer segment affected, materiality of decision, decision flow (human approval required?)
- **Evidence Level:** L2 (business document)
- **Supporting Claims:** "Deployment context is clear"; "Risk tier is appropriate"
- **Tier Applicability:** All tiers
- **Example Artefacts:** Use Case One-Pager, Business Requirements Document, Process Map

#### 2.2 Customer Impact Assessment
- **Description:** Documented assessment of impact on affected customers: eligibility, pricing, access to service, data privacy, fairness implications. Identifies vulnerable customer populations if any.
- **Evidence Level:** L2 (design document)
- **Supporting Claims:** "Customer impact is understood and mitigated"; "Vulnerable customers (if any) have additional safeguards"
- **Tier Applicability:** Tier 1+ (assesses whether Tier 1 vs 2 vs 3)
- **Example Artefacts:** Customer Impact Assessment, Vulnerability Analysis, Fairness Review Checklist

#### 2.3 Process Maps & Decision Workflows
- **Description:** Current-state and future-state process diagrams showing: where AI output feeds in, who reviews/approves, what happens on exception, audit trail captured
- **Evidence Level:** L2 (process documentation)
- **Supporting Claims:** "Human review/oversight is designed into workflow"; "Escalation pathways are clear"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** BPMN Process Diagram, Decision Tree, Workflow Specification

#### 2.4 Regulatory Obligations Mapping
- **Description:** Firm's assessment of which regulatory frameworks apply (FCA SYSC 4.1, PRA Model Risk, GDPR, Consumer Duty, AML, Market Conduct, EU AI Act, etc.). Mapped to each obligation.
- **Evidence Level:** L2 (compliance analysis)
- **Supporting Claims:** "Regulatory obligations are identified and addressed"
- **Tier Applicability:** Tier 2+
- **Example Artefacts:** Regulatory Mapping Spreadsheet, SYSC 4.1 Governance Checklist, GDPR Impact Assessment

---

### CATEGORY 3: MODEL

**Purpose:** Evidence of model design, training rigour, evaluation results, and limitations.

#### 3.1 Model Card
- **Description:** Technical documentation of model: type (LLM, classifier, regressor, agent), architecture, training data, evaluation metrics, known limitations, scope of intended use, version history
- **Evidence Level:** L2 (technical design) + L4 (evaluation results produced independently of the developer; ASSURANCE_MODEL.md §5)
- **Supporting Claims:** "Model behaviour is understood"; "Limitations are documented"
- **Tier Applicability:** Tier 1+ (Tier 0 may use vendor description)
- **Example Artefacts:** Model Card per Hugging Face standard, Technical Specification, Provider Documentation

#### 3.2 Model Evaluation & Validation Results
- **Description:** Evaluation on held-out test data or benchmark: accuracy, precision/recall, fairness metrics, robustness testing, hallucination rates, confidence calibration. Benchmarked against published standards (if available).
- **Evidence Level:** L4 (independent testing, including in a staged environment) or L3 (demonstration; ASSURANCE_MODEL.md §5)
- **Supporting Claims:** "Model performs within acceptable tolerances"; "Hallucination rate is measured and controlled"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Test Results Report, Evaluation Spreadsheet, Benchmark Comparison Table, Fairness Analysis

#### 3.3 Fine-Tuning Documentation
- **Description:** If model is fine-tuned: training data (source, size, quality), fine-tuning process (hyperparameters, validation approach), before/after performance comparison
- **Evidence Level:** L2 (design) + L4 (validation results)
- **Supporting Claims:** "Fine-tuning is justified and validated"
- **Tier Applicability:** Tier 1+ (if fine-tuning used)
- **Example Artefacts:** Fine-Tuning Report, Data Inventory, Performance Comparison

#### 3.4 Model Limitations & Failure Modes
- **Description:** Documented list of known failure modes, edge cases, scenarios where model is unreliable or out-of-distribution. Tied to IRQ-MOD series (hallucination, calibration, robustness, etc.)
- **Evidence Level:** L2 (design document)
- **Supporting Claims:** "Model limitations are known and mitigated"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Limitations Statement, Failure Mode Analysis, Out-of-Distribution Testing Report

#### 3.5 Version Control & Model Registry
- **Description:** Version history of model (training date, source data version, performance metrics per version, deprecation records). Model registry showing current production version.
- **Evidence Level:** L2 (operational record)
- **Supporting Claims:** "Model versions are tracked and managed"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Git logs, Model Registry Entry, Version Comparison Table

---

### CATEGORY 4: DATA

**Purpose:** Evidence of data quality, lineage, sourcing, and integrity controls.

#### 4.1 Data Lineage & Source Documentation
- **Description:** For training data: source, collection method, date collected, geographic scope, volume. For inference data (e.g., RAG retrieval sources): source location, update frequency, access controls.
- **Evidence Level:** L2 (data documentation)
- **Supporting Claims:** "Data sources are known and controlled"; "RAG data is fresh and authoritative"
- **Tier Applicability:** Tier 1+ (Tier 0 may have minimal data risk)
- **Example Artefacts:** Data Dictionary, Source Registry, Data Sourcing Agreement

#### 4.2 Data Quality Assessment
- **Description:** Quality metrics: completeness (% non-null), accuracy (comparison to ground truth if available), timeliness (staleness of records), uniqueness (duplicates), consistency across sources. Thresholds for acceptable quality.
- **Evidence Level:** L3 (design review) + L4 (testing/validation)
- **Supporting Claims:** "Data quality is measured and within acceptable thresholds"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Data Quality Report, Metrics Dashboard, Quality SLA

#### 4.3 Data Protection Impact Assessment (DPIA)
- **Description:** GDPR/Data Protection assessment: lawful basis for processing, data subject rights (access, portability, erasure), privacy-preserving controls, consent management if applicable
- **Evidence Level:** L2 (compliance document)
- **Supporting Claims:** "Data processing is lawful and privacy-protective"
- **Tier Applicability:** All tiers (required for GDPR compliance)
- **Example Artefacts:** DPIA Report, Privacy Notice, Consent Form

#### 4.4 Data Bias & Fairness Analysis
- **Description:** For classification/scoring models: analysis of model performance across protected attributes (gender, race, age, etc.), disparate impact testing, fairness metrics (demographic parity, equalized odds, etc.)
- **Evidence Level:** L3 (design review) + L4 (testing)
- **Supporting Claims:** "Model performance is equitable across population groups"; "Bias mitigation is in place"
- **Tier Applicability:** Tier 2+ (especially for decisions affecting customer eligibility/pricing)
- **Example Artefacts:** Bias Testing Report, Fairness Metrics Table, Remediation Plan

#### 4.5 Data Retention & Archival
- **Description:** Data retention policy: how long training/inference data is retained, archival procedures, deletion/purging procedures. Audit trail of data governance actions.
- **Evidence Level:** L2 (policy document)
- **Supporting Claims:** "Data lifecycle is managed per policy"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Data Retention Policy, Archival Log, Deletion Certificates

---

### CATEGORY 5: SECURITY

**Purpose:** Evidence of security controls, threat analysis, and resilience.

#### 5.1 Threat Model & Security Assessment
- **Description:** Documented threat model: attack vectors specific to this AI system (prompt injection, model extraction, data poisoning, supply-chain attacks, API compromise, etc.). Severity/likelihood assessment. Mapped to IRQ-SEC series.
- **Evidence Level:** L2 (design document)
- **Supporting Claims:** "Threats are identified and mitigated"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Threat Model Diagram, STRIDE Analysis, Threat-to-IRQ Mapping

#### 5.2 Prompt Injection & Jailbreak Testing
- **Description:** For LLM systems: testing against prompt injection, jailbreak, and instruction-following attacks. Test cases, results, confidence level (★1–★5).
- **Evidence Level:** L4 (independent testing) or L3 (proof-of-concept demo)
- **Supporting Claims:** "System is resilient to prompt injection"; "LLM behaviour is controllable"
- **Tier Applicability:** Tier 1+ (if LLM used)
- **Example Artefacts:** Injection Test Report, Jailbreak Testing Results, OWASP LLM Top 10 Assessment

#### 5.3 Model Extraction & Adversarial Testing
- **Description:** Testing for model robustness: adversarial examples, membership inference, extraction attacks (if relevant to deployment context). Test results and mitigations.
- **Evidence Level:** L4 (independent testing) or L3 (design review)
- **Supporting Claims:** "Model is resilient to adversarial attack"; "Confidentiality of model weights is protected"
- **Tier Applicability:** Tier 2+ (Tier 1 may defer to design review)
- **Example Artefacts:** Adversarial Testing Report, Robustness Metrics, Extraction Test Results

#### 5.4 Supply Chain & Third-Party Security
- **Description:** Assessment of third-party vendors: model providers (OpenAI, Anthropic, etc.), infrastructure (cloud, container registry), data providers. SLA audit, security certifications (SOC 2, ISO 27001), incident history.
- **Evidence Level:** L2 (vendor attestations, SLAs) + L3 (audit review)
- **Supporting Claims:** "Third-party vendors meet security standards"; "Supply-chain risks are mitigated"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Vendor Security Questionnaire, SLA Review, Audit Report, Incident History

#### 5.5 Access Controls & Authentication
- **Description:** Documentation of who can access model, data, APIs: authentication mechanisms (API keys, OAuth, SSO), least-privilege enforcement, access logging, audit trail
- **Evidence Level:** L2 (design document) + L3 (configuration review)
- **Supporting Claims:** "Access is controlled and auditable"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Access Control Policy, API Key Rotation Logs, Audit Trail Sample

---

### CATEGORY 6: OPERATIONS

**Purpose:** Evidence of deployment, monitoring, incident management, and change control.

#### 6.1 Deployment Plan & Configuration
- **Description:** Go-live plan: deployment date, rollback procedure, monitoring cutover, communication plan. Production system configuration (model endpoint, inference settings, rate limits).
- **Evidence Level:** L2 (operational plan)
- **Supporting Claims:** "Deployment is planned and controlled"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Deployment Checklist, Go-Live Plan, Rollback Procedure, Configuration Document

#### 6.2 Monitoring & Alerting Setup
- **Description:** Operational KPIs defined: system latency, accuracy, hallucination rate, user satisfaction, error rates. Alert thresholds. Monitoring dashboard screenshots or link.
- **Evidence Level:** L2 (design) + L3 (operational confirmation)
- **Supporting Claims:** "System behaviour is continuously monitored"; "Anomalies trigger escalation"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** KPI Definition Sheet, Dashboard Screenshots, Alert Configuration, Alert Trigger Examples

#### 6.3 Incident Management & Escalation
- **Description:** Incident management procedure: how incidents are detected, reported, investigated, escalated. Incident log (last 12 months) showing incidents, root cause, remediation, lessons learned.
- **Evidence Level:** L2 (procedure) + L3 (incident records)
- **Supporting Claims:** "Incidents are managed and escalated appropriately"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Incident Management Policy, Incident Log, Post-Incident Review, Escalation Matrix

#### 6.4 Change Management & Update Procedure
- **Description:** Procedure for model updates, prompt changes, data source changes, parameter tuning: change request process, approvals, testing, rollback. Change log for last 12 months.
- **Evidence Level:** L2 (procedure) + L3 (change log)
- **Supporting Claims:** "Changes are controlled and tested"; "Rollback capability is maintained"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Change Management Policy, Change Log, Testing Evidence per Change, Approval Records

#### 6.5 Backup & Disaster Recovery
- **Description:** Backup strategy for model weights, configuration, data. Recovery time objective (RTO), recovery point objective (RPO). Tested recovery procedure.
- **Evidence Level:** L2 (design) + L3 (test evidence)
- **Supporting Claims:** "System can recover from failure within acceptable timeframe"
- **Tier Applicability:** Tier 2+ (Tier 1 may use vendor SLA)
- **Example Artefacts:** Disaster Recovery Plan, Backup Log, Recovery Test Report

---

### CATEGORY 7: HUMAN OVERSIGHT

**Purpose:** Evidence that humans can understand, review, and override AI decisions.

#### 7.1 Explainability & Interpretability
- **Description:** For black-box models: explanation methods (LIME, SHAP, attention weights, etc.) and example explanations. For transparent models: feature importance, rule lists. User-facing explanation templates.
- **Evidence Level:** L3 (design review + demo) or L4 (independent testing if explanation quality matters)
- **Supporting Claims:** "System outputs are explainable to human reviewers"; "Reviewers can understand why system made a decision"
- **Tier Applicability:** Tier 1+ (especially Tier 2–3 for material decisions)
- **Example Artefacts:** Explanation Method Documentation, Example Explanations, User Interface Screenshots

#### 7.2 Escalation & Override Process
- **Description:** Escalation procedure: which scenarios trigger escalation? Who decides? SLA for response? Override procedure: can humans reject AI recommendation? Logged and audited?
- **Evidence Level:** L2 (procedure design) + L3 (procedure evidence, override logs)
- **Supporting Claims:** "Humans can escalate or override without friction"; "Escalations are rare (non-adversarial)"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Escalation Procedure, Override Log, SLA Evidence, Training Records

#### 7.3 Reviewer Training & Competence
- **Description:** Training program for human reviewers: what is AI, how to interpret outputs, when to escalate, what to watch for. Training records, competence assessment results.
- **Evidence Level:** L2 (training materials) + L3 (training records, test results)
- **Supporting Claims:** "Reviewers are trained and competent"; "Alert fatigue is managed via training"
- **Tier Applicability:** Tier 1+
- **Example Artefacts:** Training Slides, Training Record, Competence Assessment Test, Remediation Records

#### 7.4 Override Analysis & Alert Fatigue
- **Description:** Operational analysis of override patterns: % of recommendations overridden, reasons for override, trends over time. Alert fatigue indicator: if override rate >15%, escalate.
- **Evidence Level:** L3 (operational analysis) + L4 (if auditor validates)
- **Supporting Claims:** "Override rates are normal (not indicating automation bias)"; "Alert fatigue is not a risk"
- **Tier Applicability:** Tier 1+ (especially after early-life monitoring)
- **Example Artefacts:** Override Analysis Report, Trend Charts, Alert Fatigue Assessment

#### 7.5 Accountability & Contestability
- **Description:** Documentation of accountability: who is responsible for a decision? AI or human? Audit trail showing who reviewed and approved/rejected. Customer redress procedure if decision was wrong.
- **Evidence Level:** L2 (procedure) + L3 (audit trail samples)
- **Supporting Claims:** "Customer accountability is clear"; "Customers can contest decisions"
- **Tier Applicability:** Tier 2–3 (especially for autonomous decisions)
- **Example Artefacts:** Accountability Matrix, Audit Trail Sample, Escalation Procedure, Customer Redress Policy

---

## Evidence Pack Assembly by Tier

### Tier 0: Light-Touch Assessment

**Required Evidence (minimum):**
- 1.2 System Inventory (Tier 0 entry)
- 1.3 Accountability Model (attestation sufficient)
- 2.1 Use Case Assessment (brief)
- 3.1 Model Card (vendor description acceptable)

**Expected Evidence Level:** L2
**Engagement Duration:** 1–2 weeks

### Tier 1: Operational Support

**Required Evidence (all of below):**
- Category 1: 1.1, 1.2, 1.3, 1.4
- Category 2: 2.1, 2.2, 2.3
- Category 3: 3.1, 3.2, 3.4
- Category 4: 4.1, 4.2, 4.5
- Category 5: 5.1, 5.4
- Category 6: 6.1, 6.2, 6.3
- Category 7: 7.1, 7.2, 7.3

**Expected Evidence Level:** L3–L4
**Engagement Duration:** 4–6 weeks

### Tier 2: Material Decision Support

**Required Evidence (all of below):**
- Category 1: 1.1, 1.2, 1.3, 1.4, 1.5
- Category 2: 2.1, 2.2, 2.3, 2.4
- Category 3: 3.1, 3.2, 3.3, 3.4, 3.5
- Category 4: 4.1, 4.2, 4.3, 4.4, 4.5
- Category 5: 5.1, 5.2, 5.3, 5.4, 5.5
- Category 6: 6.1, 6.2, 6.3, 6.4, 6.5
- Category 7: 7.1, 7.2, 7.3, 7.4, 7.5

**Expected Evidence Level:** L4 (primary) + L3 (supporting)
**Engagement Duration:** 8–12 weeks

### Tier 3: Autonomous Material Decisioning

**Required Evidence (all of Tier 2, plus):**
- Post-deployment operational evidence (L5): monitoring data weeks 1–12, early-life findings, KPI performance
- External audit of assessment methodology (per OPINION_TEMPLATE.md)
- Annual operational validation: actual system performance in production against predicted performance

**Expected Evidence Level:** L4–L5
**Engagement Duration:** 12–16 weeks + 12-month post-deployment validation

---

## Evidence Catalogue Management

**Tools & Systems:**
- Evidence repository: shared folder with access controls, version control, retention policy
- Evidence tracking spreadsheet: category, item, status (collected/pending/gap), evidence level, tier applicability, claim mapping
- Audit trail: document who accessed what evidence, when; maintains chain of custody for regulatory requirements

**Annual Refresh:**
Every December, review evidence catalogue to identify gaps or expired documentation. Update as systems evolve (new data source, model update, process change).

---

