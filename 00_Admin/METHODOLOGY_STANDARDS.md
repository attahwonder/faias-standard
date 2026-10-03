# METHODOLOGY STANDARDS — FAIAS

## Governance

This document establishes research rigour, quality standards, and documentation disciplines for FAIAS (Financial AI Independent Assurance Standard). All review materials, evidence assessments, and control definitions must conform to these standards.

**Document Custodian:** the maintainer  
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  

---

## 1. Source Hierarchy & Primary Evidence

### Tier 1: Binding Authority (Regulatory & Standards)
- Published regulations (Basel Committee, FCA, SEC, ECB policy, EU AI Act guidance)
- Official regulatory technical standards (EBA, ESMA guidance)
- ISO/IEC standards (27001, 42001, 31000)
- NIST AI RMF, NIST Cybersecurity Framework
- BoE, Federal Reserve published positions

### Tier 2: Industry Consensus & Accepted Practice
- Peer-reviewed academic research (conference papers, journals)
- Frontier lab publications (Anthropic, DeepMind, OpenAI, Meta research)
- Industry incident reports (NTSB, MITRE ATLAS, published cybersecurity advisories)
- Published threat frameworks (OWASP, CWE/CVSS, ATT&CK frameworks)

### Tier 3: Guidance & Best Practice
- Industry working group outputs (IEEE, Cloud Security Alliance, ISACA)
- Consultant/vendor frameworks (major audit/consulting firms)
- Internal banking policies aligned with Tier 1 or 2

### Excluded Sources
- Internal email, chat, or whiteboard sketches (unless published formally)
- Vendor marketing materials (unless embedded in published research or regulation)
- Unauthenticated online forums or blog posts
- Consultant memoranda not in final published form

---

## 2. Control Definition Rules

### Every control must trace to one of:
1. **Explicit regulatory requirement** — cite regulation section, regulator guidance document, and publication date
2. **Recognised engineering standard** — cite ISO/IEC/NIST document, version, and section
3. **Accepted industry practice** — cite peer-reviewed research or multi-vendor consensus (minimum two independent sources)
4. **Frontier lab evidence** — cite published research with peer review or significant academic citation

### No invented controls. 
If a proposed control addresses a risk but has no published precedent, it is flagged as **emerging practice**, documented separately, and not included in the core battery without the maintainer's approval and documented rationale.

### Control traceability metadata:
Every control record includes:
- `Control ID` (per ID_SCHEME)
- `Derived From` (regulation/standard with version and section)
- `Publication Date` (of source document)
- `Evidence Link` (URL or internal reference to source)
- `Superseded By` (if control is deprecated)

---

## 3. Testing Method Labelling

### Test methods must be classified:
- **Established Benchmark:** The test follows a published methodology (OWASP testing guide, NIST SP 800-53 control assessment, ISO 27001 audit procedure). Cite method, publication year, and section.
- **Adapted Industry Practice:** The test adapts a published methodology to AI/LLM context. Cite original method and document adaptation rationale.
- **Emerging Practice (No Established Benchmark):** The test addresses frontier risks with no published standard. Document:
  - Why no established benchmark exists
  - Analogous non-AI testing methods (if any)
  - Design rationale and peer validation (if any)
  - Explicit caveat in review report that methodology is novel

### Non-Production Rule:
Every other statement of this rule in FAIAS refers here. The reviewer never tests production systems. Every test the reviewer performs runs in a development, test or staging environment isolated from production, on synthetic, anonymised or historical non-live data ("synthetic first", per PLAYBOOK_OVERVIEW.md §3), and no live customer data is exposed. Testing must not cause harm under any condition. Two kinds of evidence from production are admissible, and the report identifies each as such: (1) read-only records, logs and monitoring data, retrieved through the firm's normal channels without modifying production state; and (2) the results of the firm's own controlled resilience exercises, which the reviewer may observe but does not run. A production-representative staging replica is a test environment, not an exception to this rule; its fidelity to production is recorded. Calling a third-party model's generally available API from the firm's non-production environment, with synthetic inputs, within the provider's published usage terms and under the firm's own contract, is ordinary use of the service and not testing of a production system; the reviewer does not probe the provider's infrastructure. Where a firm has no non-production environment of adequate fidelity, that absence is a finding and is never grounds for testing in production.

---

## 3a. FOUR-TEST Inclusion Discipline for IRQs

Every Independent Review Question (IRQ) must satisfy all four criteria before inclusion in FAIAS. This discipline ensures each IRQ addresses a genuine, testable, decision-relevant risk rather than abstract technical curiosity.

### Test 1: SME Blind Spot
**Criterion:** A domain subject-matter expert (domain banker, risk manager, compliance officer) is likely to overlook this IRQ because it stems from AI-specific behaviour rather than domain expertise alone.

**Rationale:** Traditional banking controls (credit risk, fraud detection, AML) rely on domain SME knowledge. AI introduces novel failure modes (hallucination, prompt injection, reward drift, alignment failure) that domain experts may not anticipate without AI expertise. FAIAS must surface risks that domain experts miss.

**Validation:** IRQ template must document why domain SMEs are likely to miss this risk, with specific examples (common assumptions, process gaps, tool limitations).

### Test 2: Plausible Harm (Research/Regulation/Incident-Backed)
**Criterion:** The mechanism of harm is grounded in published research, regulation, or documented incidents—not speculation.

**Sources that satisfy this test:**
- Peer-reviewed research or frontier lab publications demonstrating the attack/failure mode
- Explicit regulatory requirement or guidance (NIST AI RMF, FCA SYSC 4.1, EU AI Act, etc.)
- Documented incident report (NTSB, MITRE ATLAS, published FS breach, disclosed vulnerability)
- Industry consensus in standards (OWASP, ISO, IEEE)

**Validation:** IRQ template must include Research Basis and/or Regulatory Basis fields citing at least one Tier 1 or Tier 2 source per Section 1 (Source Hierarchy).

**What does NOT satisfy this test:**
- Vendor marketing materials or unvalidated threat models
- Internal fear/intuition without external evidence
- Theoretical attacks with no published PoC or incident history
- Conflation of AI-general risks with financial-institution-specific risks

### Test 3: Testable in Non-Production Environment
**Criterion:** The IRQ can be answered through evidence collection and safe testing in a development or staging environment, without the reviewer testing production systems or exposing live customer data (the Non-Production Rule, §3).

**This means:**
- The question can be answered via design review, architecture analysis, staging environment testing, or log examination
- Test procedures do not require testing in production, live customer data, or invasive system probing
- Results are repeatable and auditable

**What does NOT satisfy this test:**
- Questions that can be answered only by testing in production or by exposing live data
- Purely speculative risks with no testable indicators (e.g., "could the model become sentient?")
- Questions answerable only through informal interviews or subjective assessment (no evidence trail)

**Validation:** IRQ template must include Test Procedures and Expected Evidence fields that demonstrate non-production testability.

### Test 4: Informs Governance or Deployment Decision
**Criterion:** The outcome of this IRQ informs a concrete governance, control, or deployment decision—not abstract technical curiosity.

**Examples of decision-relevant outcomes:**
- "Is this deployment safe to proceed, or do additional controls need to be implemented before launch?"
- "Does this control reduce residual risk to acceptable levels?"
- "Is this vendor's model supply chain trustworthy enough for our use case?"
- "Does the escalation workflow prevent alert fatigue from degrading human oversight?"

**Examples that do NOT satisfy this test:**
- "What is the maximum jailbreaking accuracy against our model?" (measures a property, not a decision)
- "How many hallucinations does our model produce?" (diagnostic, not decision-determinant)
- "What is the model's compression ratio for a specific dataset?" (technical curiosity)

**Validation:** IRQ template must articulate how the answer informs a specific governance, risk, or deployment decision (linked to Reporting Language and decision-maker roles).

---

### FOUR-TEST Validation Record
Every published IRQ must include an attestation:
```
FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Domain bankers/risk officers overlook this because...
✓ Test 2 (Plausible Harm): Grounded in [research/regulation/incident] — cite source(s)
✓ Test 3 (Testable): Answerable via [design review/staging test/log analysis] in non-production environment
✓ Test 4 (Decision-Relevant): Outcome informs [deployment/control/governance decision]
```

A canvas carries no version or validation line of its own: the release version in `README.md` applies; the canvas's change log records changes to its content, and the release correction log records changes made to every canvas at once.

Rejection of an IRQ (or relegation to "Emerging Practice" status without core inclusion) requires documented rationale explaining which FOUR-TEST criteria are not met and why.

---

## 3b. Evidence-Level Tagging Rule

Per ASSURANCE_MODEL.md section 5, every piece of evidence collected in an IRQ dossier is tagged with its intrinsic credibility level (L1–L5). This discipline prevents false confidence in weak evidence.

**Rule:** In Review Canvas field 10 (Expected Evidence), each evidence item is tagged: `[Evidence Description] — L[1–5]`.

**Reporting rule:** A conclusion resting **only on L1–L2 evidence** (assertion, documentation, no independent validation) must be explicitly labelled in reporting:
- "Supported by design documentation; not independently verified."
- "Conclusion based on assertion only; no independent validation."

**Why:** Regulators and sponsors must know confidence level in assurance conclusions. L1–L2 evidence is typically sufficient for **design review** (does the control exist, is it correctly configured?) but insufficient for **operational effectiveness** (is it actually working in production?).

---

## 3c. Testing-Confidence Disclosure Rule

Per ASSURANCE_MODEL.md section 6, every independent test is assigned a confidence rating (★1–★5) with defined anchors. This discipline distinguishes evidence-backed conclusions from expert-judgment conclusions.

**Rule:** In Review Canvas field 11 (Independent Test), the test procedure is followed by a confidence rating: `[Test Description] — ★[1–5] Confidence`.

**Reporting rule:** A conclusion resting on ★1–★2 tests (very early research, bespoke methodology) must be labelled in reporting as **judgement-based**:
- "Conclusion should be interpreted as professional assessment, not standardised evidence."
- "Test is based on novel methodology; results should be validated with established benchmarks if available."

**Why:** Regulators distinguish between evidence-backed findings ("control effectiveness validated against a published, partially standardised test methodology") and expert assessment ("control appears sound based on architecture review; published benchmarks do not yet exist").

---

## 3d. Failure-Mode Anchoring & Dedup Rule

Per ASSURANCE_MODEL.md section 2, every IRQ is anchored on a **failure mode** (how behaviour becomes unsafe), not on behaviour alone or consequence alone.

**Rule:** IRQ is defined by: Failure Mode (required) + Behaviour (attribute) + Consequence (attribute). Behaviours and consequences are not separate IRQs.

**Dedup principle:** Multiple failure modes from the same behaviour → separate IRQs. Same failure mode with different consequences → one IRQ (consequences are attributes).

**Examples:**
- **Separate IRQs:** (1) "Hallucinates + high confidence" (IRQ-MOD-004) vs. (2) "Hallucinates + low confidence" (different failure mode; escalation may suffice for #2) vs. (3) "Correct information + low confidence" (different failure mode; different controls required).
- **One IRQ:** Hallucination causing customer decline (loan domain) and hallucination causing AML miss (screening domain) share the same failure mode (confident hallucination), so one IRQ with two business activities listed in field 2.

**In Review Canvas:** Field 4 (Failure Mode) is the anchor. Field 3 (AI Behaviour) and Field 5 (Potential Consequences) are supporting attributes.

---

## 4. Versioning & Source Attribution

### Every risk, control, and review question carries:
- **Publication Date:** Date the source document/research was published (or `2026-Q3` for emerging practice)
- **Source Version:** Regulation version number, standard edition, or research paper version
- **Relevant Until:** If a regulatory change is scheduled, flag the sunset date
- **Lifecycle Status:** `Active`, `Deprecated`, `Superseded`, or `Emerging Practice`

### Example version record:
```
ID: IRQ-MOD-006
Subdomain: B.3 Calibration
IRQ: Model confidence calibration tracking across production operating conditions
Source: NIST AI RMF v1.0 (released January 2023), section MEASURE-2
Relevant Until: NIST's stated AI RMF review point (no later than 2028) or a superseding release
Status: Active
```

---

## 5. Citation Format

### In-text citations:
- **Regulation:** [Regulator Name, Document Title, Year, Section X.Y]  
  Example: [FCA, Handbook SYSC 4.1.1R — robust governance arrangements, current at 26 June 2026]
- **Standard:** [Org/Abbreviation, Document Title, Edition, Year, section/control code]  
  Example: [ISO/IEC 27001:2022, section 5.3]
- **Research:** [Author(s), Year, "Title", Venue]  
  Example: [Zou et al., 2024, "PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models", arXiv:2402.07867]
- **Incident Report:** [Reporting Body, Date, Case/Report ID, URL]  
  Example: [Reporting body, YYYY-MM-DD, report number as issued — illustrative placeholder, not a real report]

### Bibliography:
A centralized bibliography in each volume lists all sources with:
- Full citation (author, title, publisher, year, URL if available)
- Date accessed (for web sources)
- Superseding documents (if any)

---

## 6. Document Control & Version History

### Versioning scheme:
- **Major version** (M): Structural/governance changes (new domains, new phases)
- **Minor version** (m): Taxonomy/control updates, new review questions
- **Patch version** (p): Typos, citation corrections, clarifications (no substantive change to control definitions)
- Format: `v1.0.0`

### Change log discipline:
Every release includes, for each change:
- **Date Changed:** ISO 8601 date
- **Changed By:** the maintainer
- **Change Type:** Addition | Deprecation | Clarification | Correction
- **Rationale:** 1–2 sentences explaining why

### Change control thresholds:
- **Patch (p):** maintainer approval; no review delay
- **Minor (m):** maintainer review, recorded in the release change log
- **Major (M):** maintainer approval, recorded in the release change log, in a new signed release

---

## 7. Conflict Resolution

If a control derives from conflicting sources (e.g. regulator A requires X; regulator B prohibits X for the same institution):
1. Identify all relevant regulatory mandates (jurisdiction, effective date, sunset date)
2. Document the conflict explicitly in the control record
3. In review reports, flag the conflict and confirm institution's regulatory interpretation
4. Do not invent a compromise control; report the dilemma to sponsor

---

## 8. Audit Trail

All review materials are stored with metadata:
- Original source (URL, PDF, or document ID)
- Date retrieved
- Checksum or archival marker (to detect source changes)
- Analyst notes on interpretation

Digital documents are version-controlled in git; physical sources archived with timestamped scans.

---

## 9. Periodic Renewal

Annually (or when triggered by regulatory change):
- Audit all Tier 1 regulatory sources for updates
- Scan Tier 2 research (frontier labs, new incident reports)
- Review deprecation flags and sunset dates
- Publish change summary and updated taxonomy

---

