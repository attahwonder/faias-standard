# ASSURANCE ARCHITECTURE — FAIAS Structural Standard

## Governance

This document describes four assurance layers that support one use of the FAIAS baseline: an evidence-based opinion on a financial AI deployment. Together with ASSURANCE_MODEL.md and the 7-component structure, these layers cover pre-deployment and lifecycle assurance.

**Document Custodian:** the maintainer  
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  

---

## LAYER 2: Assurance Claims & Opinion

### The Opinion Model

The engagement output is an **OPINION**, not a findings list. FAIAS draws on the conclusion forms of ISAE 3000 (Revised); it does not make an engagement ISAE-conformant, and a practitioner who reports under ISAE 3000 must meet that standard in full.

**Four Opinion Categories:**

1. **Should Proceed** — Reasonable or limited assurance, as the assurance-level rule below allows: the AI system's controls are sufficient for deployment under the stated operating envelope; residual risks are within risk appetite; all material claims are supported by strong evidence (predominantly L4–L5).

2. **Should Proceed With Conditions** — Reasonable or limited assurance, as the assurance-level rule below allows, subject to conditions: deployment is recommended if specified conditions are met (e.g., enhanced monitoring, restricted envelope, mandatory training, vendor SLA). Conditions are measurable, time-bound, and testable.

3. **Should Not Proceed** — Recommendation against deployment: Material risks cannot be assured; evidence is insufficient or contradictory; claims are not supportable; risk appetite would be breached. Deployment should not occur until remediation is demonstrated.

4. **Unable to Form Opinion** — No conclusion formed: Scope is too narrow, evidence base too weak, or technology is immature enough that assurance is not feasible with current methods. Used when frontier research has not yet provided testable frameworks.

### Assurance Level by Opinion Category

**The assurance-level rule.** Reasonable assurance is available only where every material claim rests on tests rated ★4 or above (ASSURANCE_MODEL.md §6), in addition to the evidence requirements above. No reasonable assurance rests on a material test rated ★1–★3. Where a material claim can be tested only at ★1–★3, the test still runs, its rating is disclosed at the point of the conclusion (PLAYBOOK_OVERVIEW.md §8), and the opinion is given at limited assurance. An alternative rule, under which L4–L5 evidence with a disclosed ★2–★3 test method could support reasonable assurance, is not adopted in this version: no evidence test for it has yet been stated.

The four categories are deployment recommendations, not ISAE 3000 conclusion types. Should Proceed With Conditions is not a qualified conclusion: ISAE 3000 reserves a qualified conclusion for a material scope limitation or a material misstatement (ISAE 3000 (Revised), para 74).

| Opinion Category | Assurance Level | Reporting Implication |
|---|---|---|
| Should Proceed | Reasonable or limited, under the assurance-level rule | Low risk; proceed with normal governance |
| Should Proceed With Conditions | Reasonable or limited, under the assurance-level rule | Conditions must be satisfied; monitor closely |
| Should Not Proceed | Reasonable or limited, under the assurance-level rule | Do not deploy; material deficiencies present |
| Unable to Form Opinion | None: no conclusion is formed | Insufficient evidence; reassess when methods mature |

### Claims-Argument-Evidence Chain

The architecture follows **Claims-Argument-Evidence (CAE)** and **Goal Structuring Notation (GSN)** from safety-critical industries (cite: GSN Community Standard, UL 4600, ISO/IEC 15026-2).

**Structure:**

```
CLAIM (proposition that must be true for deployment)
  ↓ supported by
ARGUMENT (chain of reasoning linking evidence to claim)
  ↓ grounded in
EVIDENCE (IRQ assessments, test results, monitoring data)
```

**Examples of Claims:**

- "The AI system only accesses information sources it is authorised to retrieve."
- "The AI system behaves consistently within its approved operating envelope (scope, customer segment, product type, geographic region)."
- "Human reviewers remain genuinely accountable; they are not subjected to automation bias that undermines independent judgment."
- "Vendor updates and model changes cannot silently alter production behaviour; all changes are versioned and tested."
- "The system fails safely: degradation does not cascade into customer harm or regulatory breach."
- "Confidence estimates reflect actual accuracy; miscalibration is detected and escalated."

**Chain Example:**

```
CLAIM: "Hallucinated information does not influence material customer decisions."

ARGUMENT:
  1. Hallucination detection identifies confabulated outputs (IRQ-MOD-005, IRQ-MOD-004)
  2. Escalation rules route uncertain outputs to human review (IRQ-HUM-004, IRQ-HUM-001)
  3. Human reviewers challenge system output and maintain independent judgment (IRQ-HUM-001, IRQ-HUM-003)
  4. Monitoring and audit trails confirm no customer harms traced to hallucination (IRQ-RES-005, IRQ-GOV-010)

EVIDENCE:
  - IRQ-MOD-005: Staging test shows 95% hallucination detection (L3, ★3)
  - IRQ-MOD-004: Staging test flags high-confidence hallucinations before use (L4, ★3)
  - IRQ-HUM-004: Escalation workflow tested; 100% low-confidence outputs escalated (L3, ★2)
  - IRQ-HUM-001: Reviewer training logs; disagreement rate 12% (target >5%) (L5)
  - IRQ-RES-005: 90-day production logs; no customer complaints traced to hallucination (L5)
  (★ rates test methods only; operational records carry an evidence level and no ★ rating.)

CONCLUSION: Claim is well-supported by multi-source evidence. Limited assurance: the material tests are rated ★2–★3, so reasonable assurance is not available under the assurance-level rule.
```

### Claim-Level Weighting

**Material IRQ Rule:** A failed IRQ is material according to which claim(s) it undermines. An IRQ deficiency cascades to claim deficiency if:
1. The IRQ is mapped to the claim (one-way link: IRQ → Claim)
2. No alternative evidence supports the claim if the IRQ fails
3. The claim's failure breaches risk appetite or regulatory obligation

**Impact Stratification:**

- **Critical:** IRQ deficiency undermines a core safety claim (e.g., hallucination detection); no workaround control exists.
- **High:** IRQ deficiency weakens a claim but other evidence partially mitigates (e.g., confidence calibration is off but escalation workflow is strong).
- **Medium:** IRQ deficiency affects a secondary claim or applies only to a subset of operating envelope.
- **Low:** IRQ deficiency is minor, easily remediated, or applies to an optional feature.

### Mandatory Completeness Rule

**Two-Way Matrix, No Orphans:**

- **Every IRQ** maps to ≥1 Claim (IRQ is evidence for something material)
- **Every Claim** is supported by ≥1 IRQ (Claim has demonstrable evidence; not just policy assertion)

**Audit Procedure:**
1. Create IRQ ↔ Claim matrix (rows = IRQs, columns = Claims)
2. Verify every row has ≥1 cell marked (every IRQ is evidence)
3. Verify every column has ≥1 cell marked (every claim is tested)
4. Flag any orphaned IRQs (evidence for nothing material) or orphaned Claims (asserted but untested)

---

## LAYER 3: Materiality Screening

Every IRQ finding is screened against **ten materiality lenses**. Reviewers chase material business consequences, not interesting AI behaviour.

**Ten Materiality Dimensions:**

| Dimension | Question | Example |
|-----------|----------|---------|
| **Customer Outcomes** | Could failure harm a customer (financially, materially, emotionally)? | Hallucination leading to incorrect loan decision; discriminatory denial; data breach |
| **Financial Statements** | Could failure distort regulatory capital, provisions, or audit line items? | Model-driven provisions underestimated; loss given default miscalculated; regulatory relief improperly claimed |
| **Prudential Safety** | Could failure threaten solvency, liquidity, or capital adequacy? | Model concentration risk; hidden leverage; correlated failures across portfolio |
| **Consumer Duty** | Could failure breach FCA Consumer Duty (fair value, needs-based advice, vulnerability protection)? | Inappropriate product recommendation; unsuitable pricing; inadequate disclosure |
| **Operational Resilience** | Could failure disrupt critical business services or breach RPO/RTO? | Model unavailability; silent degradation; cascading failures across dependent systems |
| **Market Integrity** | Could failure distort market prices, insider information, or fair dealing? | Model-driven market manipulation (e.g., pricing algorithms colluding); information asymmetry exploitation |
| **Financial Crime** | Could failure enable money laundering, fraud, sanctions evasion, or transaction patterns that evade detection? | AML model missing typologies; fraud detector disabled; sanctions screening bypassed |
| **Data Protection** | Could failure breach GDPR/Data Protection Act (rights, consent, minimisation, security)? | Unauthorised data access; inference of protected attributes; retention overage; breach disclosure requirement |
| **Reputation** | Could failure cause reputational damage that materially affects market confidence or shareholder value? | Public disclosure of AI failure; media coverage of bias or harm; customer trust erosion |
| **Third-Party Dependency** | Could failure of vendor, cloud provider, or embedded AI silently degrade institution's assurance posture? | Silent vendor model update; supplier concentration; undisclosed capability change; exit strategy unavailable |

**Materiality symmetry.** A gap is material where a deployment could be **wrongly authorised or wrongly refused**. The lenses above imply over-refusal harm in one example (discriminatory denial) but the symmetry is stated here explicitly: unjustified refusal, exclusion or over-restriction is a Consumer Duty outcome failure of the same standing as wrongful authorisation.

**Materiality Screen Procedure:**

1. For each IRQ finding (Pass / Fail / Partial / **Not Testable**):
   - Map to all applicable dimensions (≥1 typical)
   - Assess if failure has **material** business consequence (not theoretical; not reversible in hours; not covered by compensating controls)
   - **Not Testable — presumption.** Not Testable applies where the evidence needed cannot be obtained within FAIAS's scope (the reviewer does not test production: METHODOLOGY_STANDARDS.md §3). For a **Critical** claim, an untestable IRQ presumptively yields **Unable to Form Opinion** on that claim. The presumption is defeated **only** by a scope restriction that eliminates reliance on the missing evidence — **never** by a commitment to future work. High and Medium claims' Not Testable findings route through ordinary materiality screening.
2. If finding is material on ≥1 dimension:
   - Escalate to OPINION conclusions
   - Tag in reporting as materialityThreshold
   - Include in conditions (if remediable) or adverse opinion (if not)
3. If finding is immaterial on all dimensions:
   - Document for completeness
   - Use for lifecycle monitoring, not deployment decision

**Example:**
- IRQ-MOD-005 (epistemic-state handling; hallucination-driven decline example): Material on Customer Outcomes (customer harm) + Consumer Duty (inappropriate decision) + Financial Statements (complaint provision) + Operational Resilience (complaint-handling surge) → **MATERIAL finding, escalates to Opinion**
- IRQ-RES-002 (Graceful Degradation During Outage): Material on Operational Resilience (service continuity) + Reputation (customer impact) → **MATERIAL, escalates to Opinion**
- IRQ-MOD-003 (Reasoning Degradation on Long Inputs): Immaterial on all dimensions (system is not designed for long inputs; no customer use case affected) → **Immaterial, documented for roadmap, not escalated**

---

## LAYER 4: AI Safety Case

A **per-deployment structured argument** ("acceptably safe, not perfectly safe"), borrowing best practice from aviation, nuclear, medical devices (cite: ARP 4761, IEC 61508, ISO/IEC 15026-2).

### Components

**1. System Description & Scope**
- What the system does (e.g., "Supports credit decisioning for retail mortgages")
- How it is used (e.g., "LLM-assisted application assessment; human final authority")
- Who operates it (e.g., "Credit team; trained on bias and escalation protocols")
- Where/when it operates (e.g., "UK market; English-language applicants; business hours + 24h monitoring")

**2. Operating Envelope Declaration**

**DESIGNED FOR (explicit yes-list):**
- Customer segments: Retail mortgages, prime lending, employed income
- Languages: English-language applications (UK residents)
- Products: 5-35 year term; £50k–£750k loan amount; standard amortisation
- Use case: Initial triage; escalates 10% to human underwriter for final decision
- Stress scenarios: Interest rate volatility, inflation, employment churn

**NOT DESIGNED FOR (explicit no-list):**
- Commercial mortgages, buy-to-let, bridging
- Complex income (self-employed, dividend, foreign source)
- Vulnerable customers (COBS 2.1R protections required)
- Non-English applicants; multiple-language documents
- Outsourced credit decisions (human authority must be retained)
- Real-time pricing (model outputs static prices; does not respond to market rates)
- Subprime, high-risk populations (model not validated on this cohort)

**3. Envelope Drift as Named Concept**

ENVELOPE DRIFT occurs when actual use expands beyond designed-for scope **without re-assurance**. Common vectors:

- **Business Process Drift:** System is designed as "triage tool"; business quietly changes to "decision tool" (human review becomes rubber-stamp)
- **User Behaviour Drift:** System designed for English-language; teams upload translations or multilingual documents
- **Tool/Integration Drift:** System designed standalone; integrated with downstream systems (decisions cascade through pricing, approval, credit limit)
- **Prompt Drift:** Model designed with specific system prompts; business users modify prompts ("be more permissive") without re-testing
- **Customer Segment Drift:** Model designed for prime retail; business targets self-employed or international applicants
- **Capability Drift (silent):** Vendor updates model weights; capability silently expands; institution unaware

**Mitigation:**
- Operating envelope declaration is explicit, documented, and monitored
- Envelope changes trigger re-assurance (no silent drift)
- Monitoring alerts on envelope boundary violations (e.g., anomalous customer segment, unusual prompt use)

**4. Hazards & Controls Summary**

Mapped from IRQs (not invented). Example structure:

| Hazard | Control(s) | Evidence | Status |
|--------|-----------|----------|--------|
| Hallucinated information influences lending decision | IRQ-MOD-005 (detection), IRQ-HUM-004 (escalation), IRQ-HUM-001 (reviewer training) | Staging test ★3, production monitoring L5 | Pass |
| Confidence miscalibration hides failures | IRQ-MOD-006 (calibration), IRQ-RES-005 (monitoring) | Validation L4, operational logs L5 | Pass |
| Envelope expands without re-assurance | IRQ-GOV-004 (approval tiering), IRQ-GOV-003 (conditions of use) | Policy document L2, audit logs L4 | Pass With Conditions |

**5. Assurance Lifecycle**

An opinion under this architecture is **a conclusion under conditions, not a verdict for all time**: every phase below exists to keep the conditions true, or to withdraw the conclusion when they stop being true.

**Design Phase:**
- System specification (what it does, who uses it, operating envelope)
- Claim definition (what must be true for safety)
- IRQ population (what evidence will we need)
- Test planning (how will we validate claims)
- **Parity Declaration** — a firm-produced, assurance-reviewed structured statement of the tested environment against the intended production configuration: model version and endpoint; prompts; corpus snapshot and its currency; tool set and permissions; guardrail and threshold configuration. Divergences are listed explicitly. Where no Parity Declaration exists, production alignment is **not** assumed, and its absence is recorded as a scope limitation carried into every L3 caveat and into the opinion. Produced and priced at scoping; no production testing is involved.

**Architecture Review Phase:**
- Review ASSURANCE_CLAIMS and their evidence chain (IRQ → Argument → Claim)
- Assess control design (are controls traced to research/standards?)
- Identify orphaned claims (untested) or orphaned IRQs (evidence for nothing)
- Revise envelope declaration; flag anticipated drift vectors

**Independent Testing Phase:**
- Execute TESTING_PLAYBOOK (all IRQs, per FAIAS component 5)
- Tag all evidence with L1–L5 levels and ★1–★5 confidence ratings
- Populate REVIEW_CANVAS for each IRQ
- Chain results into claims argument

**Deployment Opinion Phase:**
- Synthesise claims assessment
- Screen findings against materiality (10 lenses)
- Apply claim-level weighting (failed IRQ → failed claim?)
- Issue OPINION (Should Proceed / With Conditions / Should Not Proceed)

**Early Life Monitoring Phase (Weeks 1–12 post-deployment)**
- Confirm system behaves as tested (model performance, escalation patterns, confidence distribution)
- Monitor for envelope drift (user behaviour, process changes, prompt variations)
- Log all material incidents (customer harms, regulatory questions, control failures)
- Trigger re-assurance if envelope boundary is violated or incident pattern emerges

**Periodic Assurance Phase (Annual + Major Change)**
- Revisit claims: are they still valid?
- Audit envelope: has drift occurred uncontrolled?
- Review monitoring data: are residual risks within appetite?
- Re-test IRQs sampling (1 year → may re-test 20% of IRQs; 3 years → material re-test needed)
- Publish an updated opinion — the OPINION_TEMPLATE form with a new basis date (confidence in continued safety)

**Major Change Review Phase**
- Model update, new customer segment, new tool integration, new business process
- Triggered by: vendor update, envelope expansion, significant incident, regulatory change
- Light re-assurance or full re-test depending on change scope
- Publish a Pass-With-Conditions conclusion (per the concluding forms) or hold deployment

**Dated Forward Obligation Trigger.** An opinion issued while a dated future legal obligation is already enacted carries that obligation as a **dated condition** — a calendar trigger, not a monitoring trigger — with re-assurance against that obligation scheduled at or before the date it becomes applicable, independent of other triggers. Worked examples (dates verified at drafting): EU AI Act Art 50 obligations → 2 Aug 2026 · EU AI Act Annex III high-risk obligations → 2 Dec 2027 (deferring instrument Reg (EU) 2026/1744) · UK Data (Use and Access) Act 2025 s.80 automated-decision regime → commenced 5 Feb 2026 (SI 2026/82 reg 2(j)) · AMLR (EU) 2024/1624 → applies 10 Jul 2027.

**Retirement Phase**
- System is deprecated or replaced
- Archive all evidence, claims history, monitoring data
- Publish a retirement-stage opinion — the OPINION_TEMPLATE form scoped to the transition (residual risks in transition period, closure of material incidents)

**6. Mini Assurance Cases for Significant Risks**

For each critical claim, develop a one-page **mini assurance case** (argument chain, evidence, confidence):

**Example: "Hallucinated Information Does Not Influence Material Decisions"**

```
CLAIM: Hallucinated information does not influence material customer decisions.

CONTEXT:
  - Deployment: Retail mortgage decisioning
  - Operating envelope: English-language, UK residents, prime lending
  - Materiality: Customer harm (loan decline/approval on false info), Consumer Duty breach, regulatory breach

HAZARD: Model hallucinates customer data (e.g., "no recent account activity") with high confidence; human accepts output; customer is incorrectly declined.

CONTROLS (from IRQs):
  1. Hallucination Detection (IRQ-MOD-005, IRQ-MOD-004)
     Evidence: Staging test detects 95% of hallucinated facts; precision 90% (L3, ★3)
     Evidence: Production logs show 0 undetected hallucinations in first 90 days (L5)
  
  2. Confidence Calibration (IRQ-MOD-006)
     Evidence: Confidence estimates within ±5% of actual accuracy (L4, ★3)
     Evidence: Calibration is stable across customer cohorts; no distribution shift (L5)
  
  3. Escalation Workflow (IRQ-HUM-004)
     Evidence: 100% of low-confidence outputs routed to human review (L3, ★2)
     Evidence: SLA met; no escalation backlog (L5)
  
  4. Human Reviewer Competence (IRQ-HUM-001, IRQ-HUM-003)
     Evidence: Training logs show all reviewers certified on bias and hallucination risks (L2)
     Evidence: Disagreement rate 12% (exceeds target of 5%; shows active questioning) (L5)
     Evidence: Reviewer audit shows independent judgment (re-assignments when disagreement occurs) (L4, ★3)
  
  5. Monitoring & Incident Response (IRQ-RES-005, IRQ-GOV-010)
     Evidence: Monitoring dashboard tracks hallucination rate, escalation volume, customer complaints (L3, ★3)
     Evidence: 90-day production logs: zero customer complaints traced to hallucination (L5)
     Evidence: Incident response plan exists; tested (L2, ★3)
  (★ rates test methods only; operational records carry an evidence level and no ★ rating.)

ARGUMENT:
  Hallucination is detectable with high confidence (controls 1–2).
  Detected hallucinations are escalated to human review (control 3).
  Humans remain accountable and question system output (control 4).
  Monitoring detects any breakdowns; incident response is in place (control 5).
  Therefore, hallucinated information is unlikely to influence material decisions.

RESIDUAL UNCERTAINTY:
  - Hallucination detection may miss novel attack vectors (unmeasured risk)
  - Model updates (future versions) may not retain calibration; re-validation required
  - Reviewer training degradation over time (annual refresher planned)

CONFIDENCE: Limited assurance. Controls are well-evidenced (predominantly L4–L5), but the material tests are rated ★2–★3, so reasonable assurance is not available under the assurance-level rule. Residual risks are acceptable given human escalation layer and monitoring.

APPROVAL CONDITION: Annual reviewer competence re-certification; quarterly monitoring review.
```

---

## FINAL LAYER: Review Confidence

After the engagement, the assurance team assesses: **"How confident are we that we have identified the material AI risks?"**

**Three Levels:**

| Level | Definition | Indicators | Implication |
|-------|-----------|-----------|-----------|
| **HIGH** | Mature research methods, established benchmarks, strong multi-source evidence (L4–L5), methodical coverage, multiple independent validators | ★4–★5 tests; L4–L5 evidence dominant; peer-reviewed methods; repeatable; similar systems previously assured | Opinion is robust; low re-assurance frequency (annual or 18-month) |
| **MEDIUM** | Emerging techniques, some evidence gaps, judgement reliance, single-source evidence, frontier AI behaviours | Mix of ★3–★4 tests; L3 evidence mix; professional judgment required; expert variability; limited precedents | Opinion is credible but limited; use for deployment gate but require closer monitoring; annual re-assurance mandatory |
| **LOW** | Frontier capability, limited methodology, sparse or no incident history, extrapolation from research, untested controls | ★1–★2 tests; L1–L2 evidence; no benchmark; expert elicitation only; theoretical framework | Opinion carries significant uncertainty; use only if risk mitigated by other means; high re-assurance frequency (quarterly or per change) |

**Review Confidence Statement (internal assessment — informs the narrative forms below; per the owner's decision of 1 August 2026 it is never issued to the addressee as a grade or scale):**

Example: "Our review confidence in this assurance is **LOW**. Hallucination and confidence-calibration testing use credible research methods with no agreed benchmark (★3), and production monitoring is L5. However, reviewer competence assessment relies on training logs (L2) and a single 90-day sample (L3); we rely on professional judgment that 12% disagreement rate indicates independence. Envelope drift detection is emerging practice (★2). Under the tie to testing confidence below, a mean ★ rating below 3.2 gives Low review confidence. Recommend re-assurance at each material change and quarterly monitoring review to validate assumptions."

**Tie to Testing Confidence (★1–★5):**

Aggregate testing confidence across all IRQs:
- If mean ★ rating ≥ 4.2 and L4–L5 evidence is >70% → High Review Confidence
- If mean ★ rating 3.2–4.1 and L3–L5 evidence is >70% → Medium Review Confidence
- If mean ★ rating < 3.2 or L1–L2 evidence is >30% → Low Review Confidence

*Note: testing practice for AI in financial services is still emerging, and no test in the current battery is rated above ★4, so on the current battery no engagement reaches High Review Confidence. The threshold is kept so that it applies once settled benchmarks exist.*

**How review confidence reaches the report — the statement on the basis of the review.** The internal assessment above informs the engagement; it is never expressed to the addressee as a grade or scale. In the issued report it takes one of exactly **two narrative forms**, stated separately from the conclusion: *(A) review conducted on the full evidential basis sought* — the evidence sought at scoping was substantially obtained, the tested environment demonstrated representative to the extent recorded, conclusions resting principally on artefact and test, residual limits enumerated; or *(B) review conducted on a qualified evidential basis* — each respect in which the basis was narrower than scoped is named, together with what would have strengthened it, and the conclusion is read with those limits. **The minimum-basis rule:** where the review's own evidential basis cannot support either statement, no conclusion is signed — the outcome is Unable to Form Opinion, and the statement records what a conclusion would require. The basis statement is therefore never available as a means of qualifying a signed conclusion. The ★ scale grades test-method maturity within the methodology and does not appear in the statement.

---

## References & Standards

- ISAE 3000 (Revised): International Standard on Assurance Engagements, *Assurance Engagements Other than Audits or Reviews of Historical Financial Information* (IAASB, December 2013; effective for assurance reports dated on or after 15 December 2015)
- GSN Community Standard, Version 2 (2018); Goal Structuring Notation for Safety Cases
- UL 4600: Standard for Safety for Autonomous Vehicles and Automated Driving Systems (Underwriters Laboratories)
- ISO/IEC 15026-2: Systems and Software Assurance — Part 2: Assurance Case
- ARP 4761: Guidelines and Methods for Conducting the Safety Assessment Process on Civil Airborne Systems and Equipment (SAE International)
- IEC 61508: Functional Safety of Electrical/Electronic/Programmable Electronic Safety-Related Systems (IEC)

---

