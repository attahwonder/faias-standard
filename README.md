# FAIAS — Financial AI Independent Assurance Standard

**Version:** 1.3.2 · **Status:** Components 1–3 and 5 complete and verified, with the limits stated in §3; Components 4, 6–7 seeded (see §3) · **Last updated:** October 2026

---

## 1. What FAIAS is

FAIAS is a baseline for reviewing generative, agentic and predictive AI systems in financial institutions. It provides a common language for how these systems fail (the taxonomy); a map of those failure modes as 109 Independent Review Questions, each with a review canvas; and tests for each question, rated ★1–★4 for how established their method is. No test is rated ★5, because no settled financial-services benchmark exists yet.

The baseline supports several uses: design review, pre-production testing, independent validation, internal audit, model risk review, and an Independent Assurance Opinion before go-live. The opinion and engagement templates illustrate that last use; they are not requirements of the standard. The reviewer never tests production systems; the rule, and the evidence it admits, are stated once in `00_Admin/METHODOLOGY_STANDARDS.md` §3.

**Status.** This version is published as emerging thinking, not finished work. Its limits are stated in §3, and contributions are welcome (`00_Admin/OWNERSHIP_AND_LICENCE.md` §5). FAIAS is intended to be read alongside the FINOS AI Governance Framework and the OWASP AI Testing Guide.

### The core design ideas

1. **The primary unit is the Independent Review Question (IRQ), not the "risk".** Risks overlap; auditable questions do not. Each of the 109 IRQs (`IRQ-<DOM>-NNN`) is a precisely phrased question answerable through evidence, safe non-production testing, and interviews.
2. **Outcome-first review hierarchy.** Business Outcome → Decision → AI Behaviour → Failure Mode → Technical Cause → Assurance Objective → Expected Controls → Evidence → Independent Test → Residual Judgement. The control sits near the bottom: the reviewer asks *"can this system be trusted to perform this business activity safely?"*, not *"does the control exist?"*
3. **Behaviour / Failure Mode / Consequence separation.** Every IRQ anchors on a failure mode; behaviours and consequences are attributes. This is the deduplication mechanism.
4. **Claims-based argumentation.** 28 Assurance Claims (CLM-01…28) sit between the IRQs and the opinion, following Claims-Argument-Evidence / GSN practice from safety-critical industries. Every IRQ supports ≥1 claim; every claim is supported by ≥1 IRQ (verified two-way, zero orphans). A failed test matters according to which claim it undermines.
5. **Proportionality by tier.** A four-tier materiality classification (Tier 0 light-touch → Tier 3 maximum assurance) driven by customer/financial/regulatory impact plus autonomy and complexity scores. A bank does not review 10,000 copilot assistants the way it reviews one lending system.
6. **Honest assurance.** Evidence carries confidence levels (L1 assertion → L5 operational evidence); every independent test carries an anchored Testing Confidence rating (★1 frontier/no methodology → ★5 established benchmark); and the final opinion states the basis on which the review was conducted, and never grades it. Where no established test exists, the standard says "none established" rather than inventing one.
7. **AI Safety Case and operating envelope.** Each deployment argues it is *acceptably* safe within a declared operating envelope (designed-for / not-designed-for). Envelope drift — the effective use changing while the model does not — is a named, flagship review question (IRQ-GOV-012).

### The seven components

1. **AI Taxonomy** — a common language: 9 domains, 44 subdomains, single-homing rules and 16 boundary rulings.
2. **Independent Review Questions** — the 109-IRQ battery, each with one Review Canvas (21 fields).
3. **Assurance Claims** — the 28 propositions that must be supported before deployment, with the IRQ↔claim matrix.
4. **Evidence Catalogue** — the artefacts an institution must produce, tagged by evidence level and tier, each with supporting claim statements.
5. **Testing Playbook** — recognised, safe, repeatable non-production tests: 109 standalone procedures, one per IRQ, complete as of 12 September 2026.
6. **Safety Case** — the structured argument that a deployment is acceptably safe within its envelope.
7. **Independent Assurance Opinion** — the four-box conclusion (Should Proceed / With Conditions / Should Not Proceed / Unable to Form Opinion), drawing on the conclusion forms of ISAE 3000, with a Board Dashboard and a statement on the basis of the review.

### The nine domains

| Prefix | Domain | Subdomains | IRQs |
|---|---|---|---|
| DAT | Data | A.1–A.5 (provenance, poisoning, retrieval, memory, drift) | 14 |
| MOD | Model | B.1–B.7 (capability, hallucination, calibration, gaming, shift, updates, output stability) | 16 |
| AGT | Agentic | C.1–C.7 (planning/goal drift, tools, recursion, multi-agent, memory, hidden reasoning, action safety) | 14 |
| HUM | Human Oversight | D.1–D.4 (automation bias, skill atrophy, escalation, accountability) | 9 |
| SEC | Security | E.1–E.7 (injection/jailbreak, extraction, supply chain, identity, misuse, control efficacy, output handling) | 14 |
| TPR | Third Party | F.1–F.3 (diligence, change management, dependencies, vendor standing) | 9 |
| RES | Operational Resilience | G.1–G.4 (fallback, containment, monitoring, mapping) | 7 |
| CON | Conduct & Fairness | H.1–H.3 (discrimination, outcomes, feedback/transparency, ordinary-use harm) | 10 |
| GOV | Governance | I.1–I.4 (inventory, approval/tiering, validation, records) | 16 |

---

## 2. File map

All paths relative to the `FAIAS\` folder.

### 00_Admin — the standard's own governance
| File | Purpose |
|---|---|
| `METHODOLOGY_STANDARDS.md` | Research and quality rules: primary sources first, no invented controls, "none established" labelling, versioned citations, evidence-tagging and ★-disclosure rules, four-test inclusion discipline |
| `ASSURANCE_MODEL.md` | The core model: review hierarchy, behaviour/failure-mode/consequence separation, failure chains, assurance objectives, Evidence Levels L1–L5, Testing Confidence ★1–★5 anchors, 5-axis risk weighting |
| `ASSURANCE_ARCHITECTURE.md` | The upper layers: assurance claims and opinion logic (drawing on ISAE 3000 conclusion forms), materiality lenses, AI Safety Case, operating envelope and envelope drift, assurance lifecycle, review-confidence statement |
| `ID_SCHEME.md` | Identifier rules: IRQ, AO, CLM formats; domain/subdomain allocation; TAXONOMY.md declared authoritative |
| `IRQ_TEMPLATE.md` | The 21-field FAIAS Review Canvas template with four-test validation footer |
| `TIERING_MODEL.md` | AI Materiality Classification: Tiers 0–3, five-factor scoring, per-tier scope, evidence minimums and re-review frequency |
| `ENGAGEMENT_MODEL.md` | The reviewer's handbook: six engagement phases from intake (AI Deployment Profile) to continuous assurance |
| `OPINION_TEMPLATE.md` | Independent Assurance Opinion report skeleton, including Board Dashboard and review-confidence statement |
| `VOLUME_TEMPLATES.md` | Structural outlines for all seven components |
| `DEVELOPMENT_APPROACH.md` | How this standard was developed (companion to this README) |

### V1_Research_Compendium — the evidence base
| File | Purpose |
|---|---|
| `SOURCE_REGISTER_LABS.md` | 100 frontier-lab publications (Anthropic, OpenAI, DeepMind, Microsoft, Meta, Amazon, Mistral, Cohere, AI2), 2022–2026 |
| `SOURCE_REGISTER_ACADEMIC.md` | 139 academic papers organised by FAIAS domain, with links and assurance relevance |
| `INCIDENT_REGISTER.md` | 46 publicly documented incidents with transferable failure modes for financial services — AI incidents and two labelled automation analogues (rows 2 and 14) — with the IRQs whose canvases cite each row named against it |

### V2_IRQ_Battery — the core methodology (Component 2 + 3)
| File | Purpose |
|---|---|
| `TAXONOMY.md` | **Authoritative** domain → subdomain hierarchy with inclusion/exclusion rules and 16 boundary rulings |
| `IRQ_REGISTER.md` | All 109 IRQs: ID, subdomain, question, applicability (Gen/Agentic/Predictive), control objective, related IRQs |
| `REGISTER_STATS.md` | Counts, four-test dispositions, deliberate gaps with rationale |
| `CLAIMS_REGISTER.md` | 28 Assurance Claims with rationale, materiality lenses, criticality |
| `IRQ_CLAIM_MATRIX.md` | Two-way IRQ↔claim mapping with no-orphan verification |
| `EXEMPLAR_CANVASES.md` | The two gold-standard canvases (IRQ-SEC-003, IRQ-MOD-006) that set the quality bar |
| `canvases\CANVASES_DAT.md` … `CANVASES_GOV.md`, with `CANVASES_<DOM>_<nnn>.md` | The 109 completed Review Canvases — 107 in their own files, one per canvas, each listed in its domain file, plus IRQ-SEC-003 and IRQ-MOD-006 in `EXEMPLAR_CANVASES.md` |
| `canvases\QA_LOG_BATCH1–3.md` | Independent quality-assurance logs for every drafting batch |
| `canvases\VERIFICATION_LOG_A.md` / `_B.md` | Source-verification logs: every [TO VERIFY] flag traced to a primary source or honestly retagged |

### V4_Evidence_Catalogue
| File | Purpose |
|---|---|
| `EVIDENCE_PACK.md` | Mandatory evidence inventory in seven categories, tagged by evidence level and tier applicability, with supporting claim statements |

### V5_Regulatory_Crosswalk
| File | Purpose |
|---|---|
| `SOURCE_REGISTER_REGULATORY.md` | 163 register entries across 32 sections, verification status stated per entry (UK — PRA, FCA, Bank of England, DSIT, NCSC, industry bodies (CMORG); EU — AI Act/Commission, ECB, EBA/ESAs, EIOPA, national data protection authorities; US federal and state; Americas — Colombia; APAC — MAS, HKMA, Korea, Australia, Japan, Taiwan; international — BIS/Basel Committee, FSB, ESRB, IOSCO, IAIS, IAASB; standards — NIST, ISO/IEC, OWASP, MITRE, AI Evaluator Forum, CEN-CENELEC; frameworks — CIS, COBIT (ISACA); plus watch items counted per the register's own convention) |

### Reading order for a new reviewer
1. This README → 2. `ASSURANCE_MODEL.md` → 3. `ASSURANCE_ARCHITECTURE.md` → 4. `TIERING_MODEL.md` → 5. `ENGAGEMENT_MODEL.md` → 6. `TAXONOMY.md` + `IRQ_REGISTER.md` → 7. the domain canvas files relevant to the engagement → 8. `OPINION_TEMPLATE.md`.

---

## 2A. Ownership and licence

FAIAS is © 2026 Wonder Attah and is published under the **Creative Commons Attribution 4.0 International licence (CC BY 4.0)**; see `LICENSE`. You may share and adapt it, including for commercial purposes, if you give appropriate credit, provide a link to the licence and indicate any changes you make (in summary; section 3 of the licence sets out the conditions in full). The requested form of credit is in `00_Admin/OWNERSHIP_AND_LICENCE.md`.

**Separately from the licence, and not a condition of it:** only text that matches a signed manifest in `ownership/` is FAIAS, and each version is identified by its manifest root. The licence grants no rights in the name "FAIAS" (it licenses copyright and similar rights only; CC BY 4.0, §1(g) and §2(b)(2)); please do not present an adapted version as FAIAS, or as endorsed by its author (§2(a)(6)). FAIAS is not a certification or approval scheme: no one is authorised to certify, accredit or approve anything against it. It is published as is, without warranty; see `LICENSE`, section 5. An opinion prepared with FAIAS is the issuing practitioner's, on that engagement's terms. Quotations from regulators, standards bodies and other publications remain under their owners' terms. See `00_Admin/OWNERSHIP_AND_LICENCE.md`.

---

## 3. Status and known limitations

- Components 1–3 (taxonomy, IRQ battery, claims) are complete, QA'd and source-verified. Component 5 (testing playbook) is complete as of 12 September 2026: 109 standalone step-by-step procedures, one per IRQ (see `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`). Components 4, 6 and 7 are seeded but not fully built (evidence catalogue is a seed; safety case and opinion exist as templates without a worked example). Components 4, 6 and 7 are non-normative: they illustrate one use of FAIAS and are not requirements of the standard.
- **A regulatory correction pass was completed on 29 July 2026** — 104 edits, covering the EBA outsourcing section structure, PRA SS1/23 principle attribution and currency, the EU AI Act timeline, and ten verification-log rows that had recorded wrong pinpoints as confirmed. See `00_Admin/CORRECTION_LOG_2026-07-29.md`, which also lists four ★-rating questions left open for the owner's decision. They were resolved at v1.1.0 (25 August 2026): IRQ-CON-005 was re-rated ★1, and IRQ-CON-003, -006 and -008 kept ★2, as each canvas's Independent Test states (`V2_IRQ_Battery/canvases/CANVASES_CON.md`).
- Later errata are recorded in `00_Admin/CORRECTION_LOG_2026-08-01.md` (v1.0.3), `00_Admin/CORRECTION_LOG_2026-09-19.md` (v1.2.1, errata to text signed at v1.2.0, each entry naming what it was checked against) and `00_Admin/CORRECTION_LOG_2026-10-03.md` (v1.3.0, the changes made for open publication and the errata found in preparing it; and its §8, v1.3.2, corrections to text signed at v1.3.1). `00_Admin/MIGRATION_2026-10-03.md` maps the v1.3.1 file layout, in which each canvas and each test procedure has its own file and the text is unchanged.
- **Prescribed procedures are a ceiling, not a floor.** Effort figures assume manual execution and describe the maximal Tier 3 form; depth is calibrated per engagement and automated execution reduces effort on mechanical test classes substantially without changing ★ confidence. See `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md` §5A.
- Residual `[UNVERIFIED — reason]` tags remain where a sub-clause pinpoint could not be confirmed against a primary source; the citation is generalised conservatively rather than asserted. See the verification logs.
- Testing Confidence ratings are anchored on a ★1–★5 scale; no test in the standard is rated ★5. This is deliberate: no AI assurance test yet has a settled financial-services benchmark.
- Regulatory content is time-stamped and will age; notably, the EU AI Act Digital Omnibus (July 2026) moved Annex III high-risk obligations to 2 December 2027. Maintain via the versioning rules in `METHODOLOGY_STANDARDS.md`.
