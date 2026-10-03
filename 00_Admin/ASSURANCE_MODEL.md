# ASSURANCE MODEL — FAIAS Conceptual Core

## Governance

This document establishes FAIAS's assurance philosophy: outcome-first, failure-mode-centric, evidence-based review of AI deployment safety. Every IRQ dossier is structured as a Review Canvas (see IRQ_TEMPLATE.md) following this model.

**Document Custodian:** the maintainer  
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.  

---

## 1. Review Hierarchy: Outcome-First Structure

The fundamental posture: **"Can this AI system be trusted to perform this business activity safely?"** — not "does the control exist?"

This is the aircraft-accident-investigator posture: work *backwards* from harm combinations, not *forwards* from installed controls.

**Hierarchy (top to bottom):**

```
Business Outcome
  ↓ (supported by)
Decision (human or delegated to AI)
  ↓ (influenced by)
AI Behaviour (what the system does)
  ↓ (can fail as)
Failure Mode (how behaviour becomes unsafe)
  ↓ (caused by)
Technical Cause (root cause: data, model, code, process)
  ↓ (mitigated by)
Assurance Objective (technology-neutral "shall" statement)
  ↓ (implemented via)
Expected Controls (recognised practices; each traced to regulation/standard/research)
  ↓ (validated by)
Evidence (collected per level; tagged L1–L5)
  ↓ (tested via)
Independent Test (non-production; confidence rated ★1–★5)
  ↓ (results in)
Residual Judgement (risk profile across 5 axes; no single score)
```

**Rationale:** Reviewers who start at "control" layer rarely discover architectural failures (e.g., a system that hallucinates confidently is not fixed by better logging). Reviewers who start at outcome ask: "What could go wrong?" → "How would we know?" → "What practice addresses it?"

---

## 2. Three-Way Separation: Behaviour, Failure Mode, Consequence

### Definitions

**Behaviour:** What the AI system does (observable actions or outputs).
- Examples: hallucinates, plans multi-step actions, delegates to tool, retrieves context, writes to memory, ranks candidates, estimates confidence, generates SQL.
- Behaviours are **neutral** — they are not inherently good or bad.

**Failure Mode:** How behaviour becomes unsafe; the boundary between acceptable and unacceptable system state.
- Examples: fabricates evidence and presents as verified fact, over-delegates to tool without validation, leaks confidential data in response, executes wrong tool due to injection, creates disparate impact despite good intent.
- A failure mode is **a deviation from safe operation** triggered by behavioural misalignment, miscalibration, or architectural gap.

**Consequence:** Business or regulatory impact if failure mode occurs.
- Examples: wrong lending decision, AML typology missed, fraud payment processed, data breach disclosed, customer regulatory violation, regulatory sanction, reputational damage, service outage.
- Consequences are **stakeholder-level harms** (customer, institution, market, regulator).

### Dedup Rule

**An IRQ is anchored on a FAILURE MODE; behaviours and consequences are attributes, not separate IRQs.**

Consequence-only framing ("How do we avoid regulatory sanctions?") is too broad. Behaviour-only framing ("Does the model hallucinate?") lacks business tether. 

Failure-mode framing is precise: "Does the system present hallucinated information as verified fact?" anchors the IRQ to an **unsafe boundary crossing**, not mere technical presence/absence.

---

## 3. Failure Chains

**Every IRQ dossier must include one: a single-page causal chain from technical cause to business/regulatory impact.**

**Purpose:** Make visible the full path from AI failure to harm; identify where controls can break the chain; clarify consequence severity.

**Format:** Text or simple diagram. Nodes are cause → intermediate effect → ... → consequence. Label each node with IRQ ID if it maps to another IRQ (cross-reference).

### Worked Example

**IRQ: Weak RAG Retrieval Enabling Hallucination-Driven Customer Decline**

```
Technical Cause (data layer)
  ↓ RAG corpus outdated; customer's most recent transaction omitted
  
AI Behaviour (model layer)
  ↓ Model uncertain about customer status; hallucinates "no recent activity"
  
Failure Mode (model + oversight layers)
  ↓ Model confidence remains high despite hallucination
  ↓ No escalation rule triggered (confidence threshold not breached)
  
Human Decision Layer
  ↓ Human reviewer accepts output ("system confident, data is recent")
  ↓ Decision: decline customer application
  
Business Consequence
  ↓ Customer denied legitimate lending opportunity
  ↓ Customer complaint to FOS
  
Regulatory Consequence
  ↓ FOS investigation: decision not supported by evidence
  ↓ FCA Consumer Duty breach finding
  ↓ Reputational damage; potential capital impact

Control Breakpoints (where intervention stops the chain):
  • A.3 (Retrieval Data): Implement staleness detection; flag stale corpus
  • B.3 (Calibration): Validate confidence calibration; detect miscalibration
  • D.3 (Escalation & Override Design): Escalation rule for low-confidence contexts
  • D.1 (Automation Bias): Training for human reviewer to challenge confident outputs
```

Each chain identifies **which IRQs' controls** can interrupt the failure sequence. This drives prioritisation: IRQs in high-impact chains get higher weight.

---

## 4. Assurance Objectives

**Technology-neutral "shall" statements** describing the required safe state.

**Format:** `The AI system shall [outcome] under [conditions].`

**Purpose:** Decouple safety intent from implementation. One objective may have multiple satisfactory control implementations.

### Examples

- "The AI system shall not present fabricated information as verified fact during material decision support."
- "The AI system shall maintain confidence calibration within ±5% across held-out populations and in-production drift scenarios."
- "The AI system shall escalate tool invocations that lack explicit approval to a human decision-maker."
- "The AI system shall detect and quarantine inferences affected by data drift exceeding statistical thresholds."

### Important Amendment

**Objectives do NOT replace the control layer.** Beneath each objective sits a mapped **Expected Controls** list. Per METHODOLOGY_STANDARDS, every control must trace to regulation, recognised standard, or accepted engineering practice. No invented controls.

- **Objective** = what must be true (safety intent)
- **Expected Controls** = recognised ways to make it true (implementation options)
- **Multiple implementations** may satisfy one objective

Example:
- Objective: "System shall not present hallucinated data as verified."
- Expected Controls (options):
  - Confidence filtering + human review (B.3 + D.3)
  - RAG source attribution + retrieval validation (A.3 + IRQ-SEC-003)
  - Output fact-checking against knowledge base (emerging practice)

---

## 5. Evidence Levels: L1–L5 Worth Scale

Every piece of evidence collected has intrinsic credibility. Tag each Expected Evidence item with its level. A conclusion resting only on L1–L2 must be labelled as such in reporting.

| Level | Definition | Worth | Examples | Reporting Caveat |
|-------|-----------|-------|----------|------------------|
| **L1** | Assertion | Near-worthless | "System has safeguards" (no detail); vendor claim; internal email | "Conclusion based on assertion only; no independent validation" |
| **L2** | Documentation | Low | Policy document exists; architecture diagram; vendor SLA; GitHub README | "Supported by design documentation; not independently verified" |
| **L3** | Demonstration | Moderate | Design review walkthrough; staging test execution (non-production); code inspection; config audit | "Demonstrated in staging environment; a **Parity Declaration** exists covering model version/endpoint, prompts, corpus snapshot, tool set and guardrail thresholds; any divergence from production is listed and carried into the opinion as a stated limitation. Where no Parity Declaration exists, production alignment is **not** assumed and the finding is reported as staging-only, untested for production fidelity" |
| **L4** | Independent Evidence | High | Internal audit findings; security assessment; third-party red team report; independent validation report | "Validated by independent assessment"; use confidence rating (★) for test methodology |
| **L5** | Operational Evidence | High | Monitoring data from production or production-like system; historical incident log; drift detection report from similar prior deployment; customer complaint analysis | "Based on operational data; external validity may be limited to similar systems/cohorts" |

**Operational Evidence (L5) in Pre-Production Context:** A system may be pre-production for the current institution but operational elsewhere. Evidence from "similar" deployments (same model, same domain, different customer) is credible L5. Evidence from internal staging runs that replicate production scenarios is L3–L4 depending on realism.

---

## 6. Testing Confidence Scale: ★1–★5 with Defined Anchors

**Mandatory — every independent test must be assigned a confidence rating.** No undefined star ratings.

Purpose: Communicate to sponsors and regulators which conclusions are evidence-backed vs expert-judgment-based.

| Rating | Definition | Anchors | Examples |
|--------|-----------|---------|----------|
| **★5** | Published, widely adopted methodology with benchmark | Methodology documented in peer-reviewed standard, NIST/ISO/OWASP guide, or ≥3 independent implementations with consensus results; test results reproducible; variants documented; for a test in this standard, a settled financial-services benchmark exists for the risk tested | None in this standard: no AI assurance test yet has a settled financial-services benchmark (README.md §3). For comparison outside AI: NIST SP 800-53A Rev. 5 assessment procedures for security and privacy controls |
| **★4** | Published methodology, partial standardisation | Methodology published (IEEE, academic conference, major firm), adopted by ≥2 independent institutions, some variance in implementation allowed | MITRE ATT&CK-based adversary emulation plans; academic adversarial robustness benchmarks (e.g. RobustBench, NeurIPS 2021 Benchmarks and Datasets Track) |
| **★3** | Credible research methods, no agreed benchmark | Methodology grounded in peer-reviewed research; multiple independent research groups use similar approach; no single "canonical" version; professional judgement needed for test design | Hallucination measurement approaches (multiple papers, different metrics); fairness audit procedures (emerging consensus, no standard audit template) |
| **★2** | Research exists, method is bespoke, professional judgement dominant | Evidence from published research that harm is plausible; testing approach is institution- or system-specific; relies heavily on expert design and interpretation | Agent goal-drift detection; multi-step planning robustness; reward-hacking susceptibility assessment |
| **★1** | Very early research, no standard evaluation, assurance relies on expert review | Harm mechanism is theoretically plausible or anecdotal; testing methodology is novel or unvalidated; result quality depends entirely on assessor expertise | Emergent multi-agent coordination failure modes; hidden reasoning dependency detection; novel adversarial attack vectors not yet published |

**In Reporting:** "This IRQ's test is based on ★3 methodology (credible research, no benchmark); conclusions should be interpreted as professional assessment, not standardised evidence."

**★1 is a statement about the field, never a reason to skip.** A ★1 rating records that the assurance field has not yet produced a settled method for the question — it does not diminish the question's materiality, and it never justifies omitting the test. The lower the ★, the more the result depends on assessor expertise, and the more clearly the report must say so.

---

## 6A. Rating Currency: Version Anchors, Observation Flags and Review Cadence

A ★ rating is a **dated statement about the state of published testing methodology**, never a standing promise about it. Research maturity moves, and over the last year it has moved quickly across every domain in this register. This section exists so that movement is noticed, is visibly flagged, is resolved within a bounded period, and does not retrospectively falsify a report that was correct when it was issued.

### 6A.1 Version-anchored ratings

**Every ★ rating carries its anchor inside the rating artefact**, in the form **`★n — as at FAIAS vX.Y (date)`**. The anchor sits in the rating itself, not in surrounding prose or a document header, so that a rating quoted out of context still carries its basis. This follows CVSS practice, where the specification version is embedded in the vector string rather than held alongside it, and the NVD practice of preserving scores computed under different specification versions side by side rather than silently restating an older score on a newer scale.

`REGISTER_STATS.md` carries the ★ distribution across the register under the same as-at line.

**Ratings are never rewritten in place.** Where research moves and a canvas is re-rated, the new rating is published under a new anchor and the previous rating becomes register history. The register records a sequence of dated positions, not a single current value that overwrites its predecessors. A report issued under an earlier anchor remains true as what it was.

**Non-comparability — a standing statement.** *Ratings issued under different anchors are not comparable numbers.* Wherever ratings under different anchors could be placed side by side — register history, or a report comparing engagements — that sentence is stated explicitly. This is the documented confusion mode in the CVSS user population, where scores computed under different specification versions were read as a single trend.

### 6A.2 "Under Research Observation" (URO)

Between scheduled reviews, publisher and standards monitoring surfaces developments that could change a canvas's research basis: a new benchmark, a new edition of a cited framework, a methodology paper. Where one is identified, the canvas gains a dated flag:

> **URO: [source, date] — [what it could change] — resolve by [date]**

**The standing ★ is untouched while a URO is open.** The flag records that the basis for a rating is under examination; it is not itself a re-rating and does not qualify the existing one. This follows Fitch's **Under Criteria Observation** designation, of which the agency states: "Under Criteria Observation (UCO) is not a credit review and does not affect the rating level or Outlook/Watch …" (Fitch Ratings, *Rating Definitions*, Special Report, 11 June 2024, Cross-Sector/Global, p.8; the sentence continues "and does not satisfy the minimum annual review requirement", which FAIAS does not borrow — it has no annual-review obligation of that kind).

**Resolution is bounded: the next signing batch or six months, whichever is first.** The six-month bound is taken from two sources that set the same period. **Fitch's own definitions state it of the mechanism FAIAS is borrowing:** "The status of UCO will be resolved after the application of the new or revised criteria, which must be completed within six months from the publication date of the new or revised criteria" (*Rating Definitions*, 11 June 2024, p.8). The supervisory form of the same period is **Regulation (EC) No 1060/2009 on credit rating agencies, Article 8(6)**: on a change to rating methodologies, models or key rating assumptions, an agency shall "immediately … disclose the likely scope of credit ratings to be affected" (Art 8(6)(a)) and shall "review the affected credit ratings as soon as possible and no later than six months after the change, in the meantime placing those ratings under observation" (Art 8(6)(b)). The point FAIAS borrows is the shape: a bounded review period during which the existing ratings stand under observation, rather than lapsing. *Provenance of the Fitch pinpoints in this section: a legislature-archived copy of the publisher's own report, page attribution taken from the printed folios; the publisher-hosted file requires a subscriber login.*

**What counts as a "signing batch" for this bound.** A signing batch is a version release that changes the standard's substance — a new or amended question, a rating movement, a register addition, a mechanism. A **same-label replacement signing whose substantive content is confined to the correction of errata** is not a signing batch for the purposes of this bound: re-signing to repair a defect is the mechanism working, and a bound that is consumed by the repair would penalise correction. The date limb is unaffected and continues to run from the date the observation was flagged. The date limb is enforced mechanically, as this section states below ('The guard the precedent demands'). The signing-batch limb is enforced on the signing record; where the record does not state a signing's class, that is recorded as an open item rather than read as a pass.

Resolution takes one of exactly two forms:

1. **Re-rating under a new anchor** — the rating changes, or is affirmed, and is published under the current version anchor.
2. **Observation removed, with the reason recorded** — the development is examined and found not to move the rating. Fitch's own term for the equivalent action is **"Criteria Observation Removed"**, taken "where a rating action has not been taken … if it has been determined that the rating would not change due to the application of the new criteria" (*Rating Definitions*, 11 June 2024, p.8). The mechanism is borrowed, so its vocabulary is quoted as the source writes it rather than approximated.

**The guard the precedent demands.** A soft signal without follow-through decays into decoration. The bound is therefore enforced mechanically — an open URO past its resolve-by date fails the corpus check — and not by intention. The supervisory record supports the discipline without, on the evidence located, establishing a timing-specific precedent for it: **no enforcement action for missing the Article 8(6) six-month deadline itself was located on either the ESMA or the SEC register.** The adjacent enforcement — ESMA's 2017 methodology-disclosure fines against Moody's entities, and the **SEC's** 2018 **$16.25m internal-controls fine** — indicates supervisory attention to ratings-process discipline without confirming that the timing obligation itself has been enforced. *Two qualifications travel with that citation wherever it is used: the $16.25m is an **SEC** action under US internal-controls obligations, not an **ESMA** action under the EU timing provision, and the two must not be run together; and the figure is **secondary-sourced**, the SEC primary having been unretrievable at the time of writing.*

An **open-URO table** sits in `REGISTER_STATS.md` so that the flag population is visible at a glance rather than distributed across the canvases.

### 6A.3 Research-basis currency and calibrated review cadence

Each canvas Research Basis carries a currency line:

> **Research basis last reviewed:** [date] · **review cadence:** [tier]

**Precedents, each cited to its own source.**

- **WHO** — review-by dates are set at approval and "calibrated to how fast the evidence in the topic area is expected to change" (*WHO Handbook for Guideline Development*, 2nd ed., Ch.12.5.1, p.163). *Retrieval caveat: the WHO institutional repository returned 403 and the handbook was read via a mirror; the copy is page-numbered and internally consistent, but mirror fidelity has not been independently re-verified.*
- **Cochrane** — the date-of-search anchor, with the 12-month search-currency rule for updates (*Cochrane Handbook*, Ch.IV.4).
- **The documented failure of blanket "living" status**, three findings:
  - Zheng, Q., Xu, J., Gao, Y., Liu, M., Cheng, L., Xiong, L., Cheng, J., Yuan, M., OuYang, G., Huang, H., Wu, J., Zhang, J. & Tian, J., 2022, "Past, present and future of living systematic review: a bibliometrics analysis", *BMJ Global Health* 7(10), DOI 10.1136/bmjgh-2022-009378 — "more than half of the LSR series had not yet been updated".
  - McFarlane, E., et al., 2024, "Lifespan of COVID-19 living guideline recommendations: A survival analysis" — 1,182 recommendations across 26 WHO living guidelines; median lifespan approximately 739 days overall and approximately 335 days for pharmacological recommendations; concludes that blanket "living" treatment over-taxes surveillance and argues for a flexible, responsive model. Provenance: medRxiv preprint 2023.06.08.23291123, later in *Clinical and Public Health Guidelines*, 2024.
  - Alderson, L.J., Alderson, P. & Tan, T., 2014, "Median life span of a cohort of National Institute for Health and Care Excellence clinical guidelines was about 60 months", *Journal of Clinical Epidemiology* 67(1):52–55, DOI 10.1016/j.jclinepi.2013.07.012 — median life span 60 months (95% CI 51, 69), with approximately 86% of guidelines still up to date three years after publication, in a body operating a standing surveillance programme.
- **PRA SS1/23**, *Model risk management principles for banks*, **April 2026 version** (dated **16 April 2026**; amendment published 23 April 2026; the policy itself in force since 17 May 2024 (para 1.5) — Low Impact Amendments Finalisation) — **Principle 1.2(c)(iv)**, under which the model inventory records "the dates when validation was last performed, and the frequency of future validation", and **Principle 4.5(b)**, under which periodic revalidation "should be carried out with a frequency that is consistent with the model tier". **Scope, stated wherever this is cited:** SS1/23 para 1.2 does not apply to firms without permission to use internal models to calculate regulatory capital, or to third-country firms operating in the UK through a branch, and **credit unions, insurers and reinsurers are not in scope**. It is borrowed here as a **design precedent for cadence**, not as a requirement FAIAS's readership generally sits under.

**Cadence is calibrated to domain velocity, expressly not blanket-living.** Two tiers:

| Cadence tier | Domains | Review-by |
|---|---|---|
| **Fast** | SEC, AGT, MOD | 6 months |
| **Standard** | DAT, CON, HUM, RES, TPR, GOV | 12 months |

`[ASSUMPTION — validate]`: the cadence assignments above are proposals, not an empirical derivation. **Their whole evidential basis is one three-week observation cycle** (1–24 August 2026, in which SEC and AGT sources moved materially and GOV sources were taken to move on regulatory timescales) — a thin basis for a 6-versus-12-month split, stated here so the tiers are not read as derived from measured velocity. **GOV carries a recorded tension:** it was originally assigned a slow-moving tier on the rationale that regulatory timescales are slow, yet the same cycle's review of regulatory sources produced more GOV-relevant movement than any other domain. GOV therefore sits at **Standard (12 months)**, and the slow-moving tier is removed until a domain earns it on evidence. Cadences move on measured velocity at future reviews.

Publisher and standards monitoring is the standing trigger feed between scheduled reviews. **A triggered URO always outranks the schedule.**

### 6A.4 Practice maturity: the P-scale

A subset of the GOV, RES and TPR canvases rates **audit and compliance procedures** on research-anchored ★s — a stretch, because the ★ scale grades the maturity of published *testing methodology* and an audit procedure's maturity is a different property. Those canvases carry a **second marking alongside, and never replacing, the research ★**:

| Marking | Meaning | Anchor |
|---|---|---|
| **P1** | Novel | The procedure is newly constructed for this question; no established professional practice addresses it, and execution quality depends on the practitioner's design. |
| **P2** | Emerging professional practice | The procedure is recognisable to practitioners and used by more than one institution, but form, scope and acceptance criteria vary materially between them. |
| **P3** | Established professional practice | The procedure is settled professional practice — audit, validation or compliance-testing technique that two competent practitioners would execute comparably without further specification. |

The research ★ continues to mean exactly what its anchors in §6 say. The P marking says what the ★ scale cannot: that a procedure may be routine professional practice while the *research* underpinning the question it answers is thin, and the reverse.

The three-level P-scale and its anchor wording were confirmed by the owner at the v1.1.0 signing. The affected population is **23 of the 32 canvases those three domains hold in total** (GOV 15 of 16, RES 2 of 7, TPR 6 of 9), derived mechanically at the 25 August 2026 register audit re-run: each of the 32 was adjudicated on one question — is the procedure the ★ rates predominantly an audit or compliance procedure (documentary review, sampling, interview, reconciliation, contract or file review) rather than an empirical or technical test exercised against the AI system. **P-level assignments were made at that re-run and confirmed at signing** — P3 ×14, P2 ×8, P1 ×1 — carried on each affected canvas alongside its ★ (never replacing it) and summarised in `V2_IRQ_Battery/REGISTER_STATS.md`. Five RES canvases rate genuinely empirical exercises whose ★ *justifications* appeal to practice maturity rather than research; they sit outside this population as defined. Two of the five — IRQ-RES-004 and IRQ-RES-006 — carried that justification defect and were re-anchored to named research primaries at the v1.2.0 anchor (12 September 2026), both ★ values held unchanged at ★2; for the remaining three the justification defect is recorded as an open item rather than absorbed here.

**Two vocabularies, kept distinct.** Where a procedure's *method class* reads "None established", that is a statement about the field: no published testing methodology exists for the question. Where a canvas marks a *control* "Emerging Practice", that is a statement about precedent: the control is proposed on reasoned grounds without settled cross-institution practice behind it. The phrases grade different objects — one the test, one the control — and neither implies the other. The words "none established" also appear as a *finding* (the firm has no capability in an area where none is established industry-wide); PLAYBOOK_OVERVIEW.md §8 states which sense is meant at the point of use.

### 6A.5 Reports are opinions as at their date

A report's ratings and conclusions are statements as at the report date against the standard version cited. Later research movement is a non-adjusting event by construction: it does not revise a report already issued. Where the standard has since moved, the URO and anchor history is the context in which the earlier report is read, and a re-review under a newer anchor is the ordinary product of this mechanism rather than an admission against the earlier one. The doctrine is stated in full, in the form it takes in an issued report, in `OPINION_TEMPLATE.md` Part A.

The precedent is the auditing treatment of subsequent events (ISA 560 / IAS 10): the opinion stays anchored to conditions as at its date, later events adjust it only where they evidence conditions that existed at that date, and there is no retrospective revision. The counter-precedent is deliberately not borrowed: the ISO/IAF accreditation model's hard transition cliff, under which certifications "shall expire or be withdrawn" at the end of a transition period (IAF Resolution 2017-13). That is cited **as historical** — IAF merged with ILAC into Global Accreditation Cooperation Incorporated ("GLOBAC"), in full operation from 1 January 2026, and the iaf.nu documents are archived, IAF Mandatory Documents remaining in force under the new body until superseded. *Two qualifications: whether GLOBAC has reissued IAF MD 26:2023 was not checked, and the merger is corroborated at search level rather than from a GLOBAC primary.*

### 6A.6 Capability-envelope notes

§6A.2 observes movement in **published testing methodology**. This section observes movement in the **capability environment the assured system sits in** — a different object, and one that moves on a different clock.

A **capability-shift event** is a dated, first-party, published statement by a frontier model developer, or by a named public authority, that changes the capability envelope rather than reporting an increment within it. Exactly four forms qualify:

1. a named capability threshold declared crossed under the developer's own named safety framework;
2. a version change to such a framework;
3. a declared pause, restriction or withdrawal of a capability line, or its staged restart;
4. a change to the access tier on which a capability is supplied.

A model performing better at a task is not a capability-shift event. A third party's benchmark result is not a capability-shift event; it may be evidence within one.

Where a capability-shift event bears on **two or more** canvases, the register gains a dated **capability-envelope note** in `REGISTER_STATS.md`, carrying eight fields — the event as the head sentence plus seven labelled fields — and no others, including the **date flagged**, from which the bound below is computed:

> **CEN-n — [event, in one sentence] — source: [first-party primary, pinpoint, accessed date] — date flagged: [date] — in-scope limb: [what in FAIAS this bears on] — out-of-scope limb: [what it does not, and where that is routed] — re-baselines: [the IRQ class, by the stated membership rule, naming every IRQ ID] — re-test trigger: [the engagement class and the date before which it applies] — resolve by [date]**

A note is recorded in that form — as the note itself, not as a row of a register table. The seven labelled fields are named in the note and the event is its head sentence, so that a reader and the corpus check read the same eight things from the same place.

**Every note names the edition of the framework it rests on.** Where a note is opened on form 1 or form 2 above, the source field states the **named version or edition, and its own date, as printed on the framework document itself** — not the developer's unqualified reference to "our framework". A note whose framework edition has not been fetched and pinned is not opened; it is held, and the fact that the pinpoint is unreached is recorded. A declaration made under an edition that cannot be identified is not a dated statement about the capability envelope, which is the only thing this mechanism records.

**The standing ★ is untouched while a note is open, and no note moves a rating.** The rule is §6A.2's, for the same reason: a note records that a basis is under examination, and is not itself a re-rating. Resolution takes the two forms §6A.2 states — re-rating under a new anchor, or the observation removed with the reason recorded. A resolved note is retained and gains a dated `resolved:` field recording which form was taken and why; it is not deleted, because the record of what the capability envelope was taken to be is the thing this section exists to keep.

**Where the direction of the effect on a rating is already known, a note is not opened.** The re-rating is proposed instead. The precedent is Fitch's, which assigns a Rating Watch "in lieu of the UCO" where the application of new criteria has a "heightened probability of … resulting in a rating change in a particular direction" (Fitch Ratings, *Rating Definitions*, Special Report, 11 June 2024, p.8). A note is for an effect whose existence is established and whose direction is not. It is not a place to park work.

**Where the event bears on exactly one canvas, a note is not opened**: that is a research-basis edit, or a URO under §6A.2. The two-canvas floor is what keeps this section from becoming a second changelog.

**The in-scope and out-of-scope limbs are both stated, always.** Most capability-shift events carry a large limb that is **out of FAIAS scope under the scope decision recorded at v1.0.3** — the resistance of the firm's controls, other than its own AI systems, to attack by external parties, including its identity, authentication and payment-authorisation controls, whether or not the attack uses AI. Recording that limb, and where it was routed, is how the note stays inside the standard's scope instead of widening it. A note with no out-of-scope limb stated is incomplete, and fails the corpus check.

**Bound.** Six months from the date flagged, stated in the literal form `resolve by <date>` and machine-checked, as §6A.2 requires of a URO. A note is **not** bounded by "the next signing batch": a capability-shift event is typically recorded in the same batch that creates the note, and a bound that expires on creation is not a bound.

**How many notes may stand at once.** The limit on this mechanism is a stock ceiling of three open notes; no separate annual inflow limit is set. A fourth open note is a finding about the review cadence rather than about the events, and is answered by re-deriving the §6A.3 cadence, not by opening it.

**Precedent for the trigger, cited to its own source.** The observation form is Fitch's (§6A.2). The *trigger* is the event-driven reauthorisation of **NIST SP 800-37 Rev. 2** (December 2018), under which reauthorisation is "an event-driven action … in response to an event that results in security and privacy risk above the level of risk previously accepted", and the authorising official may "initiate a targeted review based on the type of event that triggered the reauthorization" (Appendix F, p.140); the published trigger list includes "New threat, vulnerability, privacy risk, or impact information" and "Significant changes to the system, common controls, or the environments of operation" (Appendix F, p.153). **Scope, stated wherever this is cited:** SP 800-37 is a US federal risk-management framework and does not apply to FAIAS's readership. It is borrowed as a design precedent for an environment-triggered, event-scoped targeted review — the same posture this section's neighbour takes with PRA SS1/23 at §6A.3.

**Interaction with version anchors (§6A.1).** A note changes no anchor and rewrites no rating. Where a note resolves into a re-rating, the new rating is published under the current anchor and the previous rating becomes register history, exactly as §6A.1 requires. A note's date is **not** an anchor and is never quoted as one.

**Interaction with opinions as at their date (§6A.5).** A report issued before a note was opened is not revised by it, and the note is not an admission against it. The note is the context in which that report is read.

**The re-test trigger is advisory and creates no obligation.** It identifies a class of engagement whose commissioning firm may wish to have work re-run. It creates **no obligation on the reviewer to revisit an issued opinion, no entitlement in any reader or third party to have one revisited, and no undertaking by the reviewer to perform further work.** Re-testing is performed only where the engagement terms provide for it; those terms govern, and this section confers nothing. A re-test trigger is not a warranty, not a recall, and not a representation that an earlier opinion was deficient. **Before any note is cited to a commissioning firm, the engagement letter states the same thing in the same terms** — that is a condition of the mechanism, not a courtesy, and a note cited to a client without it is cited outside this section.

**Capability-envelope notes are part of the report's context, not part of its scope.** A report cites the notes open at its date so that a later reader can see what the capability envelope was taken to be. That citation is a statement of context and nothing more.

---

## 7. Risk Weighting: Five Independent Axes (1–4 Ordinal, Defined Anchors)

**No composite single risk score.** Report the profile: five independent 1–4 assessments, each with behavioural anchors.

Purpose: Avoid false precision (e.g., 6.7/10 risk score); enable nuanced prioritisation (high severity + low likelihood + high detectability ≠ same priority as medium everywhere).

| Axis | 1 (Lowest) | 2 (Low) | 3 (High) | 4 (Highest) |
|------|-----------|---------|---------|------------|
| **Severity** | Inconvenience; reversible customer impact; no regulatory consequence | Single customer materially harmed or delayed; internal process disruption; low-value fraud | Multiple customers harmed; significant financial loss or data breach; regulatory notice; reputational damage | Systemic harm (widespread customer base); material financial loss (>£10M); regulatory enforcement action; market confidence loss |
| **Likelihood** | Unlikely under foreseeable operating conditions; attack requires sophisticated adversary + rare confluence | Plausible if controls are absent; requires moderate effort or niche user action | Probable if controls degrade; foreseeable failure mode under stress or drift; does not require sophisticated attack | Highly probable; demonstrated in research or incident reports; degrades gracefully (fails even with partial controls) |
| **Detectability** | Failure is visible in real-time monitoring; user or system immediately reports anomaly | Detected within 1 business day via monitoring or customer report; leaves clear audit trail | Detected within 1 week via log analysis or periodic audit; detection requires specialist review | Difficult to detect; silent failure; detected only post-hoc via complaint or incident; monitoring has high false-negative rate |
| **Recoverability** | Harm is immediately reversible (e.g., customer reverses transaction); system auto-recovers; no lasting impact | Reversible within hours (customer service override, manual correction, rollback); some operational cost | Reversible within days (complex exception handling, multi-team coordination, customer communication); moderate business impact | Irreversible or years-long recovery (reputational damage, regulatory remediation, system redesign required); material ongoing cost |
| **Novelty** | Banking domain expert (credit risk, AML, ops) would flag this risk; no AI-specific knowledge needed | Domain expert would flag risk with AI domain context (knows hallucination is possible); standard enterprise AI controls would catch it | Domain expert might miss because it is AI-specific (e.g., reasoning integrity, multi-step delegation); requires AI research knowledge | Domain expert very likely to miss; risk is emergent (e.g., multi-agent coordination, hidden reasoning dependencies); outside traditional banking risk model |

**Profile Example:**
```
IRQ-MOD-005 (fabricated resolution of missing or conflicting evidence)
  Severity: 3 (decisions on unresolvable or conflicting evidence affect multiple customers; regulatory notice risk)
  Likelihood: 3 (probable absent engineered controls: sparse, ambiguous or conflicting evidence is routine in underwriting, AML and claims)
  Detectability: 3 (fabricated resolution is fluent and internally consistent; detection requires deliberate evidential-state audit, not casual review)
  Recoverability: 2 (affected decisions are traceable via retrieval and evidence logs and correctable through re-review)
  Novelty: 4 (the five-way epistemic-state distinction is AI-specific; a domain expert's assumption that the system would say if it did not know does not hold)

Profile Interpretation:
  High severity + high novelty → prioritise this IRQ
  Low detectability → invest in monitoring rules
  Moderate recoverability → acceptable residual risk if controls are strong
```

---

## 7A. Multi-Rater and Panel Agreement: A Reliability Measure, Not a Validity Measure

Wherever this standard or its playbooks rely on multiple reviewers, graders, annotators or an expert panel reaching, or being reported to have reached, agreement — whether as FAIAS's own test evidence (dual scoring, blind reconstruction, annotator studies) or as the AI system's own human-oversight control (a grading panel, an adjudication committee, human re-scoring of an AI judge) — that agreement is evidence of consistency, not of correctness, and is reported as such.

**The distinction, and why it matters.** Inter-rater reliability (IRR) analysis is distinct from validity analysis: "IRR analysis is distinct from validity analysis, which assesses how closely an instrument measures an actual construct rather than how well coders provide similar ratings" [Hallgren, K.A., 2012, "Computing Inter-Rater Reliability for Observational Data: An Overview and Tutorial", *Tutorials in Quantitative Methods for Psychology* 8(1), p.24, DOI 10.20982/tqmp.08.1.p023]. Raters can agree strongly while the agreement reflects a shared misconception rather than the state of the thing rated: "an instrument may have good IRR but poor validity if coders' scores are highly similar and have a large shared variance" [Hallgren, 2012, p.24], the source continuing that the instrument may nonetheless fail to represent the construct it is intended to measure. High agreement is a necessary check, never a sufficient one.

**Three conditions attach wherever agreement is used as evidence:**

1. **Chance-corrected measurement.** Raw percent agreement is not reported as the reliability statistic on its own: percentages of agreement "do not correct for agreements that would be expected by chance and therefore overestimate the level of agreement" [Hallgren, 2012, p.25], and the same source concludes that "[r]esearchers should use validated IRR statistics when assessing IRR rather than using percentages of agreement or other indicators that do neither account for chance agreement nor provide information about statistical power" [Hallgren, 2012, p.32, Conclusion]. Cohen's or Fleiss' kappa, or an equivalent chance-corrected statistic, is used wherever the design allows it. **No threshold is prescribed.** FAIAS sets no acceptance level for any agreement statistic, and no figure appearing illustratively anywhere in this standard or its playbooks is an acceptance level — the DAT domain's annotator-agreement example included, which its own playbook states is an example only and records that no FS-specific consensus threshold exists.
2. **Independence of the raters, stated.** Every use of multiple raters or a panel states what independence was secured: of each other's initial judgement (raters neither see nor discuss another's score before their own is recorded), and of any party with a stake in the outcome.
3. **Shared blind spots, considered.** Independence between raters does not rule out a blind spot shared by all of them — the same training, the same rubric, the same institutional assumption. Where a panel's members share a common source of judgement, that source is named, and agreement is read as consistency within it rather than as external validation of it.

**Where this applies.** This section governs, without duplicating them: the dual-scoring and adjudication procedures across the HUM, DAT, CON, AGT and MOD playbooks; IRQ-MOD-015's human-agreement limb; and any control of an assured system that itself rests on multiple human graders or panel consensus. It creates no new question and moves no rating; it states a cross-cutting evidentiary standard the canvases and playbooks already assume.

---

## Integration with REVIEW CANVAS

Every IRQ Review Canvas includes:
- Assurance Objective (with ID, e.g., AO-MOD-005)
- Expected Controls (each traced to regulation/standard)
- Expected Evidence (each tagged L1–L5)
- Independent Test (with ★ rating)
- Risk Weighting profile (5 axes, 1–4 each, with anchors for this assessment)

The Review Canvas is the **single source of truth** for one IRQ's assurance case. See IRQ_TEMPLATE.md for structure.

---

## References & Citations

This model draws on:
- Aircraft accident investigation (work backwards from consequences)
- Medical safety (failure mode and effects analysis, FMEA)
- NIST AI RMF (MAP/MEASURE/MANAGE taxonomy)
- ISO 31000 Risk Management (multi-axis assessment)
- Fault tree analysis (causal chains)
- Evidence-based assessment (credibility levels per academic research, ISO 27035)

---

