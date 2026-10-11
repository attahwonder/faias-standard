# FAIAS REVIEW CANVAS — IRQ Template

## Purpose

The Review Canvas is **one artefact per IRQ**, structured outcome-first per ASSURANCE_MODEL.md. It is the authoritative source for one IRQ's assurance case: what could go wrong, why, what evidence is needed, and at what confidence level.

---

## Canvas Fields (In Order)

### 1. IRQ ID & Title
**Type:** Required string  
**Format:** `IRQ-<DOM>-<NNN>: [Title]`  
**Example:** `IRQ-MOD-004` (Model domain — hallucination; see IRQ_REGISTER.md for the canonical title)

Unique identifier and descriptive title anchored on the failure mode.

---

### 2. Business Activities Affected
**Type:** Required list (bullet points; 1–3 sentences per activity)  
**Scope:** Which customer-facing or regulatory-material processes depend on this system.

**Example:**
- **Lending decision:** System supports credit assessment; incorrect decline (via hallucinated customer data) denies legitimate loan.
- **AML review:** System assists transaction screening; missed indicator (via fabricated confidence) allows typology slip-through.
- **Customer service:** System drafts responses; factually incorrect response damages customer trust and incurs complaint-handling cost.

---

### 3. AI Behaviour(s)
**Type:** Required list (neutral, observable actions; 1–2 sentences per behaviour)  
**Scope:** What the system does; not evaluation of safety.

**Example:**
- Generates customer-context responses without source citation
- Estimates confidence scores as byproduct of generation
- Delegates data validation to retrieval system; trusts staleness detection

---

### 4. Failure Mode
**Type:** Required string (1–2 sentences; the unsafe boundary crossing)  
**Scope:** How behaviour becomes unsafe; the primary anchor of this IRQ.

**Example:**
> "Model confidently presents hallucinated customer information as verified fact during material lending decision, despite data recency uncertainty."

**Note:** This is the failure mode (unsafe state), not behaviour (what system does) or consequence (impact on customer).

---

### 5. Potential Consequences
**Type:** Required list (business/regulatory impact; 2–3 per IRQ)  
**Scope:** Stakeholder-level harms if failure mode occurs.

**Example:**
- **Customer:** Legitimate applicant denied credit opportunity; complaint escalation to FOS.
- **Institution:** Regulatory breach (Consumer Duty); reputational damage; capital impact from FOS remediation.
- **Market:** Customer confidence in automated lending erodes; competitive positioning weakens.

---

### 6. Failure Chain
**Type:** Required (text or simple diagram; single page max)  
**Scope:** Causal sequence from technical cause to business/regulatory consequence. Identify control breakpoints.

**Example:**
```
RAG Corpus Stale
  ↓ (IRQ-DAT-007: Retrieval data curation)
Model Uncertain About Customer Status
  ↓ (IRQ-MOD-004: Hallucination measurement)
Model Hallucinates "No Recent Activity" + High Confidence
  ↓ (IRQ-MOD-006: Confidence calibration NOT linked)
No Escalation Triggered (Confidence threshold intact)
  ↓ (IRQ-HUM-001: Automation bias)
Human Reviews Output, Accepts ("System confident; must be current")
  ↓ (IRQ-HUM-004: Escalation design)
Customer Declined
  ↓
FOS Complaint → FCA Consumer Duty Breach → Remediation Cost

Control Breakpoints (can interrupt chain):
  • IRQ-DAT-007: Staleness detection → flag stale corpus
  • IRQ-MOD-004: Hallucination detection → low-confidence flag
  • IRQ-MOD-006: Confidence calibration → detect miscalibration
  • IRQ-HUM-004: Escalation rule → trigger on uncertainty
```

---

### 7. Why a Domain Expert May Miss It
**Type:** Required list (2–4 bullet points)  
**Scope:** Blind spots unique to AI behaviour; traditional banking SME would overlook.

**Example:**
- Assumption: "LLM only retrieves if confident about source availability" (false; hallucinates when retrieval fails)
- Process gap: Credit reviewers trained on stale data accuracy, not on model confidence miscalibration
- Tool misunderstanding: RAG staleness detection fails silently; retrieval "succeeds" with old data
- Testing gap: Staged testing with fresh data masks retrieval staleness risk (production data is weeks old)

---

### 8. Assurance Objective
**Type:** Required string (technology-neutral "shall" statement with ID)  
**Format:** `AO-<DOM>-<NNN>: The AI system shall [outcome] [under conditions].`  
**Example:** `AO-MOD-004: The system shall not present hallucinated information as verified fact during material customer decision support.`

**Purpose:** Decouple safety intent from implementation. Multiple controls may satisfy one objective.

---

### 9. Expected Controls (Traced)
**Type:** Required list (each traced to regulation/standard/research; 3–6 per IRQ)  
**Format per control:** `[IRQ ID / Control Name] — [Regulation/Standard/Research cite] — [Brief description]`

**Important:** Every control must trace per METHODOLOGY_STANDARDS; no invented controls. If a plausible control has no published precedent, mark as **Emerging Practice** and document rationale.

**Example:**
- **IRQ-DAT-007 (Retrieval Data Staleness Detection)** — [NIST AI RMF, MEASURE-2, January 2023] — Detect when retrieval corpus exceeds age threshold; flag to escalation workflow.
- **IRQ-MOD-004 (Hallucination Detection & Filtering)** — [OWASP Top 10 for LLM Applications, 2025] — Apply output fact-checking against known knowledge base; low-confidence filter.
- **IRQ-MOD-006 (Confidence Calibration Validation)** — [ISO/IEC 42001:2023, section 6.2] — Periodic validation of confidence estimates against held-out ground truth; detect drift.
- **IRQ-HUM-004 (Escalation for Uncertainty)** — [FCA, Handbook SYSC 4.1.1R — robust governance arrangements, current at 26 June 2026] — Route low-confidence outputs to human review with SLA.
- **IRQ-HUM-001 (Automation Bias Training)** — [NIST AI RMF, MANAGE-4, January 2023] — Train human reviewers to challenge system output; measure disagreement rates.

---

### 10. Expected Evidence (Tagged L1–L5)
**Type:** Required list (each tagged with evidence level per ASSURANCE_MODEL.md)  
**Format per item:** `[Evidence Description] — L[1–5]`

**Example:**
- Design specification for retrieval staleness detection (threshold, update frequency) — L2
- Code review of retrieval update pipeline; validation that staleness detection logic is invoked pre-model — L3
- Staging test results: 50 queries with stale corpus; system correctly flags 48/50 (96% detection rate) — L3
- Internal audit report (Q3 2026): retrieval staleness detection confirmed operational in production, tested monthly — L4
- Production monitoring data (last 90 days): staleness detection triggered 127 times; 100% resulted in human escalation — L5
- Hallucination filtering test results: 20 synthetic hallucinations; filter caught 18/20 (90% detection rate) — L3
- Confidence calibration audit (last month): expected calibration (±5%) achieved on held-out test set — L4

---

### 11. Independent Test
**Type:** Required (non-production; methodology cited with ★ confidence rating)  
**Format:** `[Test Procedure Description] — [Methodology cite] — ★[1–5] Confidence`

**Example:**
> "Inject 30 hallucinated customer records into staging RAG corpus; run 50 customer queries designed to surface hallucination. Measure: (1) system flags hallucination, (2) confidence score is well-calibrated, (3) escalation workflow triggers. Compare against the internal confidence validation baseline. Test executed in isolated staging environment; no production data or live systems accessed. — ★3 Confidence (credible research methods, no agreed benchmark; staging realism to production not assumed without a Parity Declaration)"

---

### 12. Pass Indicators
**Type:** Required list (observable, measurable evidence of control working)  
**Scope:** What success looks like.

**Example:**
- Staging test: ≥90% of hallucinations detected and flagged
- Confidence calibration: validation accuracy ±5% across held-out cohorts
- Escalation workflow: 100% of low-confidence outputs routed to human within SLA
- Production monitoring: staleness detection triggered, acted upon, and logged for ≥95% of stale retrievals
- Human reviewer audit: agreement rate with system ≥85% (disagreements logged and reviewed)

---

### 13. Fail Indicators
**Type:** Required list (red flags control is absent, ineffective, or degraded)  
**Scope:** What failure looks like.

**Example:**
- Staging test: <80% hallucination detection rate; false negatives observed
- Confidence calibration validation fails: model confidence ≠ actual accuracy (e.g., claims 95% confident on 60% accuracy items)
- Escalation workflow absent or non-functional; low-confidence outputs passed to downstream decision without review
- Production monitoring shows staleness detection disabled or not triggered despite stale data ingestion
- Customer complaints indicate hallucinated information influenced decisions; post-hoc investigation finds no corresponding flag in audit logs

---

### 14. Reporting Language
**Type:** Required (1–2 sentences per finding state; executive-ready phrasing)  
**Scope:** How to communicate findings (pass/fail/partial) to sponsor and regulators.

**Example (Pass):**
> "Hallucination detection and escalation controls are operational across all production RAG code paths. Staging validation confirms ≥90% detection accuracy; confidence calibration is within ±5% on held-out data. Escalation SLA is met; no escalation backlog observed in last 90 days of production logs."

**Example (Fail):**
> "Hallucination detection is absent from production RAG pipeline. Staging testing confirms hallucinated customer information directly influences model output without filtration. No escalation workflow exists for high-uncertainty scenarios. This control gap represents critical risk of customer harm and regulatory breach."

**Example (Partial):**
> "Hallucination detection is deployed in primary API endpoint (90% of queries) but missing from mobile app variant (10% of queries). Staging tests identify control coverage gap; equivalence not demonstrated. Remediation plan targets parity within 60 days."

---

### 15. Residual Judgement
**Type:** Required (risk profile across 5 axes; 1–4 ordinal per ASSURANCE_MODEL.md)  
**Format:** 
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (multiple customers harmed; regulatory notice risk)
  Likelihood: 2 (unlikely given strong escalation; requires control degradation)
  Detectability: 3 (detected via customer complaint within days; not real-time)
  Recoverability: 3 (reversible within days; moderate business/regulatory cost)
  Novelty: 4 (domain expert very likely to miss; requires AI knowledge)

Residual risk interpretation: Acceptable if controls remain strong and monitored. Highest concern: Novelty (easy to become complacent given AI expertise scarcity); prioritise ongoing monitoring and team competence.

If controls are absent or degraded:
  Severity: 4 (systemic harm; financial loss; regulatory breach highly probable)
  Likelihood: 4 (near-certain without escalation)
  Detectability: 3 (customer complaints; forensic discovery of hallucinated decisions)
  Recoverability: 4 (years-long remediation; FCA enforcement)
  Novelty: 4 (domain expert unaware)

Residual risk: Critical. Immediate remediation required.
```

---

### 16. Risk Weighting Profile (5 Axes, 1–4)
**Type:** Required (simple table; one assessment; use anchors from ASSURANCE_MODEL.md section 7)

**Format:**
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Multiple customers harmed; regulatory notice risk (Consumer Duty) |
| **Likelihood** | 3 | Probable if RAG staleness control absent; demonstrated in staged tests; data recency gaps common in production |
| **Detectability** | 3 | Detected within days via customer complaint; not in real-time monitoring; detection requires log forensics |
| **Recoverability** | 3 | Reversible within days via FOS handling; customer compensation; moderate business cost |
| **Novelty** | 4 | Domain expert very likely to miss; requires AI hallucination + confidence miscalibration knowledge; outside traditional credit risk model |

---

### 17. Regulatory Basis
**Type:** Required (specific citations; explicit if none)  
**Format:** [Regulator, Document, Version, Date, Section]

**Example with regulation:**
> "[FCA, Handbook SYSC 4.1.1R, current at 26 June 2026] requires robust governance arrangements, including effective risk processes and control and safeguard arrangements for information processing systems. [NIST AI 100-1 (AI RMF 1.0), January 2023, MEASURE 2.4] expects the functionality and behaviour of the AI system and its components to be monitored when in production."

**Example without direct regulation:**
> "No explicit regulatory requirement for hallucination detection identified. This IRQ addresses prudential risk under general governance expectations (the applicable governance instrument — fetched and verified at drafting)."

---

### 18. Research Basis
**Type:** Required (peer-reviewed research, frontier labs, incident reports)  
**Format:** [Author(s), Year, "Title", Venue]

**Example:**
> "[Zou et al., 2024, 'PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models', arXiv:2402.07867] shows that a few malicious texts injected into a RAG knowledge database can make the model return an attacker-chosen answer. [Ji et al., 2023, 'Survey of Hallucination in Natural Language Generation', ACM Computing Surveys] reviews how hallucinated text is measured and mitigated in natural language generation. [Published FS incident, 2023] detailed customer complaint arising from LLM-generated incorrect account summary."

**Incident-register citations.** Where the research basis rests on an incident carried in `V1_Research_Compendium/INCIDENT_REGISTER.md`, the citation takes a reserved form, in this field by default, or in the field where the incident is used, keeping the shape above: `**[FAIAS Incident Register, row N, "Short incident name", YEAR]** — what the incident evidences for this IRQ.` Where the canvas also cites the incident's primary, the primary's bracket follows the register bracket, either at once — `**[FAIAS Incident Register, row N, "Short incident name", YEAR]**, citing [primary] — what the incident evidences for this IRQ.` — or after the quotation or statement from the primary that it supports, later in the same citation. `YEAR` is the year, stated in the row's Date cell, of the event or report on which the citing field relies. The link is two-way and resolves in both directions: a register row cited in this form names this IRQ in its `IRQ(s) supported` cell, and every IRQ named in a row's `IRQ(s) supported` cell cites that row on its own canvas — in this form or, for a citation made before the form was introduced on 19 September 2026, by naming the incident in the canvas's own text. An incident not carried in the register is not cited in this form — either the row is added, or the underlying source is cited in its own right.

---

### 19. Related IRQs
**Type:** Required (cross-domain linkages with brief explanation)  
**Format:** `IRQ-<DOM>-<NNN> ([Subdomain]: [Link rationale])`

**Example:**
```
Related IRQs:
  - IRQ-DAT-007 (A.3 Retrieval Data: staleness detection prerequisite control)
  - IRQ-MOD-004 (B.2 Hallucination: hallucination measurement upstream)
  - IRQ-MOD-006 (B.3 Calibration: confidence calibration component)
  - IRQ-HUM-004 (D.3 Escalation & Override Design: escalation workflow)
  - IRQ-HUM-001 (D.1 Automation Bias: human reviewer challenge behaviours)
```

---

### 20. References
**Type:** Required (with publication dates/versions)  
**Format per METHODOLOGY_STANDARDS.md**

**Example:**
```
[1] Zou, W., Geng, R., Wang, B. and Jia, J., 2024. "PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models." arXiv:2402.07867.
    Published: February 2024
    URL: https://arxiv.org/abs/2402.07867

- [2] Financial Conduct Authority. "Handbook SYSC 4: General organisational requirements." https://www.handbook.fca.org.uk/handbook/SYSC/4/ (an earlier illustrative entry here attributed invented content to SYSC 19D, the Remuneration Code; corrected 25 August 2026)
    Accessed: 2026-08-26
    URL: https://www.handbook.fca.org.uk/handbook/SYSC/4/

[3] NIST, 2023. "Artificial Intelligence Risk Management Framework (AI RMF) Version 1.0."
    Published: January 2023
    URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf

[4] Ji, Z., Lee, N., Frieske, R., et al., 2023. "Survey of Hallucination in Natural Language Generation." ACM Computing Surveys 55(12).
    URL: https://doi.org/10.1145/3571730
```

---

### 21. Four-Test Validation Footer
**Type:** Required (confirmation per METHODOLOGY_STANDARDS.md section 3a)

**Format:**
```
---
**Version:** the release version in `README.md`  
**Subdomain:** B.2 (Model domain, Hallucination)  
**Status:** Active | Deprecated | Emerging Practice  

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Credit reviewers would overlook hallucination risk because LLM behaviour is unfamiliar; confidence scores appear objective.
✓ Test 2 (Plausible Harm): Grounded in research (Ji et al., 2023; Zou et al., 2024) and incident reports documenting hallucination-driven customer harm.
✓ Test 3 (Testable): Answerable via staging test (synthetic hallucination injection); confidence calibration audit (historical accuracy validation).
✓ Test 4 (Decision-Relevant): Outcome informs deployment gate (proceed only if hallucination detection ≥90% accurate + escalation SLA confirmed).

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed; Review Canvas structure adopted
```

---

## Instantiation & Validation Rules

- All 21 fields are mandatory; no omissions.
- One canvas per IRQ in final form; its length follows the evidence.
- Failure Mode is the anchor; Behaviour and Consequence are attributes only.
- Every Expected Control traces to regulation/standard/research; no invented controls.
- Every Expected Evidence is tagged L1–L5; conclusions resting on L1–L2 are explicitly flagged.
- Every Independent Test has a ★ confidence rating with defined anchors.
- Risk Weighting uses 5 axes, each 1–4 ordinal, with justification; no composite score.
- FOUR-TEST Validation footer confirms IRQ is admissible.

---

