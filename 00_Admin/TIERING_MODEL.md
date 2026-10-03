# TIERING_MODEL.md — AI Materiality Classification & Proportional Review Depth

**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  
**Document Custodian:** the maintainer

---

> **Calibration note.** Phase durations and procedure depth in this handbook describe the maximal, Tier 3 form of the engagement and assume manual execution. They are a ceiling to calibrate down from, not a required floor. Scope, depth, sample size and repetition are set per engagement against tier, consequence, evidence availability, the named expert's direction and the depth commissioned; automated test execution reduces effort on mechanical test classes substantially without changing the ★ confidence of the method. Every reduction is recorded, and anything not tested is dispositioned with its reason and consequence rather than omitted silently. See PLAYBOOK_OVERVIEW.md §5A.


## Purpose

TIERING_MODEL.md defines a proportional assurance approach: not all AI systems warrant identical scrutiny. This document establishes four tiers of materiality (Tier 0–3) based on deployment risk profile, and specifies which FAIAS components, IRQs, evidence levels, and assurance types apply to each tier.

The model prevents two extremes: wasteful over-assessment of low-risk systems (internal assistants), and inadequate under-assessment of high-stakes deployments (autonomous lending decisions).

---

## Four Tiers of AI Materiality

### Tier 0: Low Materiality — Light-Touch Assessment

**Profile:** Internal knowledge assistants, meeting summaries, document search, coding assistance, content drafting

**Characteristics:**
- No direct customer impact (output consumed internally only)
- No financial impact (no transactions, no pricing, no capital exposure)
- No regulatory impact (advisory to internal staff; not subject to Conduct, FCA/PRA, Consumer Duty)
- Autonomy 0–1 (purely informational; human decides all actions)
- Complexity 0–2 (deterministic retrieval or formatting; no novel reasoning)

**Review Scope:**
- IRQ Domains: Governance only (IRQ-GOV series)
- Evidence Level Minimum: L2 (design documentation; policy attestation)
- Opinion Type: Limited Assurance (or attestation only)
- Re-Assessment: Annual or upon major model update

**Rationale:** Risk is low and bounded by human review of every output. Assurance focuses on governance discipline (who owns the system, how is it monitored) rather than technical control validation.

---

### Tier 1: Operational Support — Standard Independent Review

**Profile:** Claims handler assistants, contact centre support, fraud analyst assistants, compliance analyst assistants, operational decision support

**Characteristics:**
- Indirect customer impact (AI informs human decision, human remains accountable; delays or minor service degradation possible)
- Low–moderate financial impact (operational cost from errors; no customer loss, no capital hit)
- Moderate regulatory impact (Consumer Duty: transparency on use; compliance support; no discretionary bias risk)
- Autonomy 1–2 (recommends; human approves all material actions)
- Complexity 2–3 (pattern matching, document extraction, prioritisation; bounded by known rules)

**Review Scope:**
- IRQ Domains: Governance, Data (sourcing), Model (hallucination, confidence), Human Oversight (escalation, override)
- Critical Claims: "System escalates failures to human review"; "Data sources are clean"; "Output confidence is calibrated"
- Evidence Level Minimum: L3 (staged testing; design review)
- Opinion Type: Limited Assurance (selective controls; emerging practice allowed)
- Re-Assessment: 12 months or upon material code change

**Rationale:** Human review provides backstop. Assurance validates that escalation pathways work and data is reliable. Testing can rely on staged environment; emerging-practice controls acceptable if documented.

---

### Tier 2: Material Decision Support — Full Assurance Review

**Profile:** Credit underwriting support, AML alert prioritisation, claims triage, investment research, insurance pricing assistance

**Characteristics:**
- Significant customer impact (affects eligibility, pricing, tiering, access to service; individual customers materially affected)
- Moderate financial impact (per-customer loss from errors; accumulated exposure; capital/reserve implications)
- High regulatory impact (FCA SYSC 4.1 governance arrangements apply; PRA model risk governance; Consumer Duty: suitability, fairness, bias screening)
- Autonomy 2–3 (system scores/ranks; human makes final decision but may over-rely on AI recommendation)
- Complexity 3–4 (multi-factor weighting, calibrated risk scoring, some model-specific behaviour)

**Review Scope:**
- IRQ Domains: All 9 domains (Data, Model, Agentic, Human Oversight, Security, Third-Party, Resilience, Conduct & Fairness, Governance)
- Critical Claims: All core claims per ASSURANCE_ARCHITECTURE.md (envelope, hallucination, fairness, escalation, monitoring)
- Evidence Level Minimum: L4 (independent testing in staged environment; benchmarked test methods; policy + operational validation)
- Opinion Type: Reasonable Assurance where every material claim rests on tests rated ★4 or above (comprehensive methodology; L4+ evidence dominant); otherwise limited assurance, with each rating disclosed (ASSURANCE_ARCHITECTURE.md, assurance-level rule)
- Re-Assessment: Annual or upon model update, new data source, changed decision logic, new customer segment

**Rationale:** Material financial and regulatory exposure demands comprehensive review. Testing must be independent and repeatable. Emerging-practice controls flagged; foundation must be published benchmarks or peer-reviewed methods.

---

### Tier 3: Autonomous Material Decisioning — Maximum Assurance + Formal Approval

**Profile:** Automated credit decisions (origination, lines adjustment), autonomous fraud actions (transaction blocks, account freezes), agents executing transactions, autonomous customer-facing advice

**Characteristics:**
- Direct, significant customer impact (system makes binding decisions; customer redress required if system fails)
- High financial impact (per-transaction loss + reputational damage + regulatory capital + complaint handling + FOS escalation)
- Critical regulatory impact (PRA model risk governance, BCBS 239; FCA SYSC 4.1, Consumer Duty, SMCR accountability, Market Conduct)
- Autonomy 4–5 (executes decisions autonomously; human review exception-only or post-facto)
- Complexity 4–5 (adaptive models, agent multi-step planning, or black-box ensemble)

**Review Scope:**
- IRQ Domains: All 9 domains (comprehensive coverage; no exceptions)
- Critical Claims: Every core claim must be supported; no workarounds
- Evidence Level Minimum: L4–L5 (independent testing + operational validation post-deployment; no L1–L2 evidence on material claims)
- Opinion Type: Reasonable Assurance where every material test is rated ★4 or above (the assurance-level rule) and, in addition at Tier 3, secondary controls are rated ★3 or above (rigorous methodology; mandatory L5 on critical claims; low uncertainty); otherwise limited assurance, with each rating disclosed (ASSURANCE_ARCHITECTURE.md, assurance-level rule)
- Independent Validation: Mandatory external audit of assessment methodology and testing
- Formal Approval: Requires CEO/Board sign-off (not delegation)
- Re-Assessment: Annual, plus mandatory re-review for any model change, data change, autonomy expansion, new customer segment, or incident

**Rationale:** Autonomous decisions are binding; customer redress and regulatory consequences are severe. Assurance must be independent, evidence-backed, and formally documented. Emerging practice is not acceptable without explicit board risk appetite exception.

---

## Five-Factor Materiality Assessment

To assign an AI system to a tier, evaluate these five factors on a calibrated scale. Tier assignment follows a rule-based algorithm; override triggers exist for edge cases.

### Factor 1: Customer Impact (1–4 Scale)

| Score | Definition | Examples |
|-------|-----------|----------|
| 1 | No direct customer impact; internal use only | Meeting summaries; internal documentation; coding assistance |
| 2 | Indirect impact; AI informs decision, human approves, limited service effect | Operational assistant; fraud analyst support; compliance scanning; service delays possible |
| 3 | Significant impact on individual customers; affects eligibility, pricing, access | Underwriting support; AML prioritisation; insurance triage; customer materially affected |
| 4 | Binding customer impact; system makes autonomous decisions affecting access, pricing, service; redress required on error | Autonomous lending, transaction blocking, account freeze, customer-facing advice |

### Factor 2: Financial Impact (1–4 Scale)

| Score | Definition | Examples |
|-------|-----------|----------|
| 1 | No financial impact or immaterial cost | Informational outputs; internal efficiency only |
| 2 | Low financial impact; per-error cost <$10K; accumulated risk <$1M/year | Operational inefficiency; processing delays; staff time |
| 3 | Moderate financial impact; per-error cost $10K–$100K; accumulated risk $1M–$10M/year | Customer pricing error; missed fraud detection; regulatory fine (minor) |
| 4 | High financial impact; per-error cost >$100K; accumulated risk >$10M/year; capital/reserve implications | Wrong lending decision; undetected financial crime; regulatory capital hit; systemic reputational damage |

### Factor 3: Regulatory Impact (1–4 Scale)

| Score | Definition | Examples |
|-------|-----------|----------|
| 1 | No regulatory impact | Internal operational tool; staff support |
| 2 | Low regulatory impact; Consumer Duty transparency only; no governance/compliance requirements | Disclosures on AI use; advisory context |
| 3 | Moderate regulatory impact; SYSC 4.1 governance arrangements apply; PRA model risk regime; Consumer Duty (suitability/fairness); bias screening required | Supporting material decisions; must demonstrate fairness controls; governance escalation required |
| 4 | Critical regulatory impact; BCBS 239 risk-data aggregation implications for capital and regulatory reporting; SMCR accountability; PRA model risk expectations (SS1/23); Consumer Duty at-risk; AML/Market Conduct implications; autonomous decisions require formal approval | Autonomous decisions; customer-facing advice; high-risk classification under EU AI Act |

### Factor 4: Autonomy Level (0–5 Scale)

| Score | Definition | Examples |
|-------|-----------|----------|
| 0 | Pure information retrieval; human must research and decide | Search, summarization, drafting |
| 1 | Advisory only; human initiates action | Recommendations on next step; scored list for manual review |
| 2 | Scoring or prioritisation; human approves before action | Risk score calculated; human decides threshold; system flags items |
| 3 | Threshold-based triggers; human exception-handling; mostly automated | System auto-approves <$50K decisions; human reviews exceptions >$50K |
| 4 | Predominantly autonomous; human reviews post-facto or exceptional conditions | System auto-approves >90% of decisions; human audit trail; rare exceptions escalated |
| 5 | Fully autonomous; no human-in-loop | Transactions execute immediately; human cannot intervene before decision |

### Factor 5: System Complexity (0–5 Scale)

| Score | Definition | Examples |
|-------|-----------|----------|
| 0 | Deterministic rules, no learning | If-then business logic; no model involved |
| 1 | Simple retrieval with ranking | Search + sorting; basic filtering |
| 2 | Single trained model, supervised learning, published benchmark | Spam classifier; sentiment analyzer; standard regression |
| 3 | Multi-model ensemble; fine-tuned models; RAG with dynamic source selection | Multiple classifiers; adapted pre-trained models; retrieval-augmented generation |
| 4 | Adaptive models; novel architectures; agents with tool use; in-context learning; prompt tuning | LLM agents; prompt injection vulnerability; adaptive systems that learn from feedback |
| 5 | Black-box ensemble; multi-agent orchestration; emergent behaviour; unpredictable failure modes | Large language models; complex agent orchestration; reward-misaligned systems |

---

## Tier-Derivation Rule

### Algorithm

**Step 1: Score each factor (1–4 or 0–5 depending on factor)**

| Factor | Score |
|--------|-------|
| Customer Impact (1–4) | _____ |
| Financial Impact (1–4) | _____ |
| Regulatory Impact (1–4) | _____ |
| Autonomy (0–5) | _____ |
| Complexity (0–5) | _____ |

**Step 2: Normalize Autonomy & Complexity to 1–4 scale**
- Autonomy normalized: (raw score ÷ 5) × 4, rounded to nearest integer (min 1, max 4)
- Complexity normalized: (raw score ÷ 5) × 4, rounded to nearest integer (min 1, max 4)

**Step 3: Calculate composite risk score**
```
Risk Score = 
  (Customer Impact × 0.25) + 
  (Financial Impact × 0.25) + 
  (Regulatory Impact × 0.25) + 
  (Autonomy normalized × 0.125) + 
  (Complexity normalized × 0.125)
```

**Step 4: Map to tier**

| Risk Score Range | Tier | Assignment |
|---|---|---|
| 1.0–1.5 | Tier 0 | Light-touch assessment |
| 1.6–2.3 | Tier 1 | Standard review |
| 2.4–3.1 | Tier 2 | Full assurance |
| 3.2–4.0 | Tier 3 | Maximum assurance + board approval |

### Override Triggers (Force Upgrade to Higher Tier)

Apply tier upgrade (move to next tier) if ANY of the following conditions met:

1. **Vulnerable Customer Exposure:** System processes requests from vulnerable customers (elderly, disability, low financial literacy, protected characteristics). Upgrade by 1 tier.

2. **Regulatory Enforcement History:** Firm has regulatory feedback or enforcement action related to this process (e.g., FCA bias finding in lending). Upgrade by 1 tier.

3. **Novel Risk:** System uses emerging technology with sparse published research (e.g., LLM agents without published safety benchmarks, new foundation model without external audit). Upgrade by 1 tier.

4. **Systemic Importance:** System processes >25% of firm's customer volume in material decisions. Upgrade by 1 tier.

5. **Reputational Criticality:** Failure would trigger media coverage or regulatory investigation. Upgrade by 1 tier.

6. **Chain of Dependency:** System output feeds multiple downstream autonomous systems (compound risk). Upgrade by 1 tier.

7. **Third-Party Sole Dependency:** System relies on single external model provider with no fallback; vendor incident would block business. Upgrade by 1 tier.

**Special Case — Mandatory Tier 3:** Any system satisfying:
- Autonomy ≥4 AND Customer Impact ≥3 (autonomous material decision by definition → Tier 3, regardless of other factors)
- Regulatory Impact = 4 AND Autonomy ≥2 (critical regulatory/autonomy combination → Tier 3)

---

## Per-Tier Scope & Governance

### Tier 0: Light-Touch Assessment

| Dimension | Specification |
|---|---|
| **IRQ Domains** | Governance only: IRQ-GOV-001, -002, -005, -009 and -014, at documentary depth (PLAYBOOK_OVERVIEW.md §5) |
| **Critical Claims** | "AI system owner defined and accountable"; "Policy documented" |
| **Evidence Level Minimum** | L2 (design document, policy) |
| **Testing Requirement** | Design review only; no staged testing required |
| **Opinion Type** | Limited assurance or attestation |
| **Engagement Duration** | 1–2 weeks |
| **Re-Assessment Trigger** | Annual or upon major model/prompt change |
| **Board Approval** | Recommended but not mandatory; functional owner sign-off sufficient |

### Tier 1: Operational Support — Standard Review

| Dimension | Specification |
|---|---|
| **IRQ Domains** | Governance, Data (A.1–A.5), Model (B.1–B.4), Human Oversight (D.1–D.4) |
| **Critical Claims** | "Escalation pathways work"; "Data is clean"; "Hallucination is detected"; "Humans can override" |
| **Evidence Level Minimum** | L3 (staged testing, design review, policy + training records) |
| **Testing Requirement** | Staged environment testing; non-invasive; FOUR-TEST validation per IRQ |
| **Test Confidence Minimum** | ★3–★4 where available; procedures rated ★1–★2 run with the disclosure in PLAYBOOK_OVERVIEW.md §8 |
| **Opinion Type** | Limited assurance (selective controls; emerging practice disclosed) |
| **Engagement Duration** | 4–6 weeks |
| **Re-Assessment Trigger** | 12 months or upon code change, new data source, changed escalation rules |
| **Board Approval** | Risk committee or compliance committee; functional executive sign-off |
| **Monitoring Post-Deployment** | Monthly KPI review; escalation alerts defined |

### Tier 2: Material Decision Support — Full Assurance

| Dimension | Specification |
|---|---|
| **IRQ Domains** | All 9 domains (comprehensive coverage) |
| **Critical Claims** | All core claims per ASSURANCE_ARCHITECTURE.md (no waivers) |
| **Evidence Level Minimum** | L4 (independent staged testing; ≥1 L4–L5 per core claim) |
| **Testing Requirement** | Non-production testing per Component 5 Playbook; benchmarked methods; FOUR-TEST discipline; cross-domain scenario testing |
| **Test Confidence Minimum** | For reasonable assurance: ★4 or above on all material tests; ★3 permitted on lower-risk subdomains. A material test rated ★1–★3 still runs, with the disclosure in PLAYBOOK_OVERVIEW.md §8, and the opinion is then given at limited assurance |
| **Opinion Type** | Reasonable assurance where the test-confidence condition above is met (comprehensive methodology; no emerging-practice exceptions); otherwise limited assurance (ASSURANCE_ARCHITECTURE.md, assurance-level rule) |
| **Engagement Duration** | 8–12 weeks |
| **Re-Assessment Trigger** | Annual, or upon model update, new data source, customer segment expansion, operating envelope change |
| **Board Approval** | Risk committee approval; regulatory affairs consulted |
| **Monitoring Post-Deployment** | Weekly KPI dashboard; early-life monitoring (weeks 1–12); quarterly assurance review |
| **Materiality Screening** | All 10 lenses; material findings escalated to opinion |

### Tier 3: Autonomous Material Decisioning — Maximum Assurance + Formal Approval

| Dimension | Specification |
|---|---|
| **IRQ Domains** | All 9 domains (exhaustive; no exceptions) |
| **Critical Claims** | Every core claim must be supported by L4–L5 evidence; no L1–L2 on material claims |
| **Evidence Level Minimum** | L4–L5 (independent testing + post-deployment operational validation) |
| **Testing Requirement** | Exhaustive staged testing; multiple independent tests per IRQ; L5 evidence required (production-equivalent conditions or live monitoring) |
| **Test Confidence Minimum** | For reasonable assurance: ★4 or above on all material tests; ★3 minimum on secondary controls only. A material test rated ★1–★3 still runs, with the disclosure in PLAYBOOK_OVERVIEW.md §8, and the opinion is then given at limited assurance |
| **Opinion Type** | Reasonable assurance where the test-confidence condition above is met (rigorous; low residual uncertainty); otherwise limited assurance (ASSURANCE_ARCHITECTURE.md, assurance-level rule) |
| **Independent Validation** | Mandatory external audit of assessment |
| **Engagement Duration** | 12–16 weeks |
| **Board Approval** | **Mandatory CEO/Board sign-off**; not delegable to committee |
| **Formal Approval Document** | Board resolution documenting risk appetite exception (if any), residual risks accepted, monitoring commitment |
| **Monitoring Post-Deployment** | Daily real-time KPI monitoring; automated escalation on threshold breach; weekly governance review; monthly model performance audit |
| **Re-Assessment Trigger** | Minimum annual; mandatory upon any: model version change, training data change, decision logic change, autonomy expansion, new customer segment, incident, or regulatory feedback |
| **Regulatory Notification** | PRA/FCA notification of major autonomous systems (if applicable); supervisory feedback incorporated into remediation |

---

## Rationale: Proportionality in Assurance

**Why proportional tiers?**

Imposing identical FAIAS assessment rigor to an internal meeting-summary assistant and an autonomous lending system wastes assurance resources and delays deployment of low-risk systems. Conversely, light-touch assessment of high-stakes autonomous systems creates false confidence.

Tiering allows:
1. **Efficient resource allocation:** Tier 0 systems assessed in weeks, not months; Tier 3 systems get the rigor they require
2. **Regulatory alignment:** Proportionality is a regulatory principle (proportionate governance, proportionate controls, proportionate monitoring)
3. **Sustainable governance:** Firms cannot scale identical rigor to 10,000 AI implementations; tiering makes assurance feasible
4. **Risk-appropriate evidence:** Tier 0 design documentation is sufficient; Tier 3 requires operational evidence post-deployment

**Firm accountability:** Tiering is not a waiver. A Tier 0 system incorrectly classified as Tier 0 when it should be Tier 2 remains the firm's accountability. Governance bodies must validate tier assignments annually.

---

## Tier Assignment Governance

**Annual Tier Review:**
Every December, re-assess all systems against the five-factor model. Flag:
- Systems with factor changes (e.g., expanded to new customer segment → Customer Impact increases)
- Regulatory feedback or incidents affecting risk profile
- New override conditions (vulnerable customer exposure, reputational risk)

**Tier Upgrade Process:**
If system tier increases mid-year (e.g., due to expanded scope), trigger fresh assurance engagement at new tier level before expanded deployment proceeds.

**Tier Downgrade Exception:**
Tier downgrade only permitted with explicit evidence review and QA Lead approval. Default posture: escalate on uncertainty, do not downgrade.

---

