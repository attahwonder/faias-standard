# FAIAS — IRQ Register Statistics & Coverage Notes

## Counts by domain and subdomain

| Domain | Subdomain | IRQs |
|---|---|---|
| DAT (14) | A.1 Training Data Provenance | 6 |
| | A.2 Data Poisoning | 2 |
| | A.3 Retrieval Data | 3 |
| | A.4 Memory | 1 |
| | A.5 Data Drift | 2 |
| MOD (16) | B.1 Capability Uncertainty | 3 |
| | B.2 Hallucination | 2 |
| | B.3 Calibration | 1 |
| | B.4 Specification Gaming & Reasoning Integrity | 3 |
| | B.5 Distribution Shift & Evaluation Integrity | 5 |
| | B.6 Model Updates & Configuration | 1 |
| | B.7 Output Stability & Determinism | 1 |
| AGT (14) | C.1 Planning & Goal Drift | 2 |
| | C.2 Tool Use | 3 |
| | C.3 Recursive Agents | 1 |
| | C.4 Multi-Agent Systems | 1 |
| | C.5 Operational Memory | 1 |
| | C.6 Hidden Reasoning Dependencies | 1 |
| | C.7 Workflow & Action Safety | 5 |
| HUM (9) | D.1 Automation Bias | 2 |
| | D.2 Skill Atrophy | 1 |
| | D.3 Escalation & Override Design | 2 |
| | D.4 Accountability & Contestability | 4 |
| SEC (14) | E.1 Prompt Injection & Jailbreak | 5 |
| | E.2 Extraction & Leakage | 3 |
| | E.3 Supply Chain & Tool Security | 2 |
| | E.4 Identity & Credentials | 1 |
| | E.5 Misuse & Dual-Use | 1 |
| | E.6 Control Efficacy Under Adversarial Evolution | 1 |
| | E.7 Improper Output Handling | 1 |
| TPR (9) | F.1 Due Diligence, Contracts & Licensing | 4 |
| | F.2 Model Change Management | 1 |
| | F.3 Dependencies, Concentration & Data Handling | 4 |
| RES (7) | G.1 Fallback & Degradation | 2 |
| | G.2 Containment & Recovery | 2 |
| | G.3 Monitoring & Alerting | 2 |
| | G.4 Resilience Mapping | 1 |
| CON (10) | H.1 Discrimination & Proxy Bias | 2 |
| | H.2 Customer Outcomes, Vulnerability & Access | 6 |
| | H.3 Feedback Loops & Transparency | 2 |
| GOV (16) | I.1 Inventory & Ownership | 2 |
| | I.2 Approval, Tiering & Policy | 5 |
| | I.3 Validation & Oversight | 2 |
| | I.4 Documentation, Records & Regulatory | 7 |
| **Total** | **44 subdomains** | **109** |

**Register size is governed by validity, not by target bands.** The original design bands (75–100 IRQs, 30–40 subdomains) are recorded here as descriptive design history only — they do not constrain the register. The four-test inclusion discipline is the sole gate: an IRQ that passes all four tests is admitted whatever the count, and one that fails any test is excluded however much room a band would leave. Every addition except IRQ-GOV-012 publishes its four-test disposition below. IRQ-GOV-012 has no row below; its four tests are in field 21 of its canvas. History: IRQ-GOV-012 (operating-envelope drift) added under the claims-layer restructure (homing ruling in TAXONOMY.md ruling 14); IRQ-DAT-013 (feedback-loop contamination) added following the Data-domain gap check below; thirteen IRQs added at v1.0.3 (IRQ-AGT-014 followed at v1.1.0) (GOV-013, GOV-014, MOD-014, MOD-015, CON-009, SEC-012 from the enrichment batch; HUM-009, DAT-014, SEC-013, SEC-014, GOV-015, GOV-016, TPR-009 from the incident-evidence batch); IRQ-MOD-016 and IRQ-CON-010 added at v1.2.0 (owner's decision of 11 September 2026; IRQ-MOD-016 on the first ruling of deliberate gap 2), dispositions below.

## Testing-confidence (★) distribution — as at FAIAS v1.3.6 (22 November 2026)

One rating per canvas, taken from canvas field 11 across all 109 canvases (107 in the domain canvas files, plus IRQ-SEC-003 and IRQ-MOD-006 in `EXEMPLAR_CANVASES.md`).

| Domain | ★1 | ★2 | ★3 | ★4 | ★5 | Canvases |
|---|---|---|---|---|---|---|
| DAT | 0 | 7 | 7 | 0 | 0 | 14 |
| MOD | 0 | 9 | 7 | 0 | 0 | 16 |
| AGT | 0 | 14 | 0 | 0 | 0 | 14 |
| HUM | 1 | 4 | 4 | 0 | 0 | 9 |
| SEC | 1 | 5 | 8 | 0 | 0 | 14 |
| TPR | 1 | 4 | 4 | 0 | 0 | 9 |
| RES | 0 | 4 | 3 | 0 | 0 | 7 |
| CON | 2 | 6 | 2 | 0 | 0 | 10 |
| GOV | 0 | 7 | 9 | 0 | 0 | 16 |
| **Total** | **5** | **60** | **44** | **0** | **0** | **109** |

**This is a third dated position, not a revision of the two below.** Ratings issued under different version anchors are not comparable numbers (ASSURANCE_MODEL.md §6A.1). The v1.2.0 and v1.1.0 distributions stay below as earlier dated positions. Ten ratings moved at v1.3.6, each after a review of its basis against the anchor words of ASSURANCE_MODEL.md §6. IRQ-AGT-008 and IRQ-AGT-013 moved from ★1 to ★2. IRQ-CON-004, IRQ-HUM-007, IRQ-MOD-009, IRQ-SEC-004, IRQ-SEC-013 and IRQ-TPR-004 moved from ★2 to ★3. IRQ-SEC-001 and IRQ-SEC-003 moved from ★4 to ★3, because their ★4 basis named OWASP LLM01:2025, which gives no test method (URO-7 and URO-8, resolved below). No canvas is rated ★4 at v1.3.6. Each moved rating carries the v1.3.6 anchor in its canvas.

**Cross-check against Component 5 (v1.3.6).** All 109 canvases have a corresponding procedure in the domain playbooks, and each procedure carries its canvas rating unchanged.

## Testing-confidence (★) distribution — as at FAIAS v1.2.0 (12 September 2026)

One rating per canvas, taken from canvas field 11 across all 109 canvases (107 in the domain canvas files, plus IRQ-SEC-003 and IRQ-MOD-006 in `EXEMPLAR_CANVASES.md`).

| Domain | ★1 | ★2 | ★3 | ★4 | ★5 | Canvases |
|---|---|---|---|---|---|---|
| DAT | 0 | 7 | 7 | 0 | 0 | 14 |
| MOD | 0 | 10 | 6 | 0 | 0 | 16 |
| AGT | 2 | 12 | 0 | 0 | 0 | 14 |
| HUM | 1 | 5 | 3 | 0 | 0 | 9 |
| SEC | 1 | 7 | 4 | 2 | 0 | 14 |
| TPR | 1 | 5 | 3 | 0 | 0 | 9 |
| RES | 0 | 4 | 3 | 0 | 0 | 7 |
| CON | 2 | 7 | 1 | 0 | 0 | 10 |
| GOV | 0 | 7 | 9 | 0 | 0 | 16 |
| **Total** | **7** | **64** | **36** | **2** | **0** | **109** |

**This is a second dated position, not a revision of the one below.** Ratings issued under different version anchors are not comparable numbers (ASSURANCE_MODEL.md §6A.1); the v1.1.0 distribution is retained beneath as the previous dated position and is not restated here. The two movements from v1.1.0 are the two additions at v1.2.0: IRQ-MOD-016 at ★2 (MOD ★2 9 → 10) and IRQ-CON-010 at ★1 (CON ★1 1 → 2).

**Cross-check against Component 5 (v1.2.0).** All 109 canvases have a corresponding procedure in the domain playbooks, and every one of the 109 carries its canvas rating unchanged — **zero divergences on programmatic comparison, re-run at 109 on 12 September 2026** with a parser first validated against the 25 August 2026 figures (★1×6, ★2×63, ★3×36, ★4×2 = 107; 535 of 535 distinct justifications; 107 of 107 in bounds), then re-measured at 109: 545 of 545 distinct risk justifications, 545 of 545 axis-cells within their stated bounds, 109 of 109 canvases conforming.

## Testing-confidence (★) distribution — as at FAIAS v1.1.0 (25 August 2026)

One rating per canvas, taken from canvas field 11 across all 107 canvases (105 in the domain canvas files, plus IRQ-SEC-003 and IRQ-MOD-006 in `EXEMPLAR_CANVASES.md`).

| Domain | ★1 | ★2 | ★3 | ★4 | ★5 | Canvases |
|---|---|---|---|---|---|---|
| DAT | 0 | 7 | 7 | 0 | 0 | 14 |
| MOD | 0 | 9 | 6 | 0 | 0 | 15 |
| AGT | 2 | 12 | 0 | 0 | 0 | 14 |
| HUM | 1 | 5 | 3 | 0 | 0 | 9 |
| SEC | 1 | 7 | 4 | 2 | 0 | 14 |
| TPR | 1 | 5 | 3 | 0 | 0 | 9 |
| RES | 0 | 4 | 3 | 0 | 0 | 7 |
| CON | 1 | 7 | 1 | 0 | 0 | 9 |
| GOV | 0 | 7 | 9 | 0 | 0 | 16 |
| **Total** | **6** | **63** | **36** | **2** | **0** | **107** |

**No canvas is rated ★5, and none has been since the register was first compiled.** ★5 requires a documented methodology with a benchmark and consensus results (ASSURANCE_MODEL.md §6); no settled financial-services benchmark exists for any question in this register. The empty column is a statement about the field, not an omission from the table.

**This is a snapshot under one anchor, not a trend line.** Ratings issued under different version anchors are not comparable numbers (ASSURANCE_MODEL.md §6A.1). A later distribution replaces nothing: it is a second dated position alongside this one.

**Cross-check against Component 5.** All 107 canvases have a corresponding procedure in the domain playbooks, and every one of the 107 carries its canvas rating unchanged — **zero divergences on programmatic comparison, re-run at 107 on 25 August 2026**. The thirteen-item gap recorded here previously — the v1.0.3 canvas additions with no procedure sheet — **closed on 25 August 2026**, when those sheets were written into PLAYBOOK_DAT, PLAYBOOK_MOD, PLAYBOOK_SEC, PLAYBOOK_HUM, PLAYBOOK_TPR, PLAYBOOK_CON and PLAYBOOK_GOV. `PLAYBOOK_OVERVIEW.md` was regenerated at the same time and now states 107 procedures across the nine domains (DAT 14, MOD 15, AGT 14, SEC 14, HUM 9, TPR 9, RES 7, CON 9, GOV 16), with its §9 index rebuilt from the playbooks and reconciled 1:1 against this register. Component 5 is at 1:1 with the register for the first time since the v1.0.3 additions.

## Practice-Maturity (P) Markings — as at FAIAS v1.1.0 (25 August 2026)

Per ASSURANCE_MODEL.md §6A.4, 23 of the 32 GOV, RES and TPR canvases rate audit or compliance procedures on the research-anchored ★ scale and carry a second, practice-maturity marking alongside it — never replacing it:

| Domain | P3 | P2 | P1 | Marked | Unmarked (empirical test) |
|---|---|---|---|---|---|
| GOV | 8 | 6 | 1 | 15 of 16 | IRQ-GOV-013 |
| RES | 2 | 0 | 0 | 2 of 7 | IRQ-RES-001/-002/-003/-004/-006 |
| TPR | 4 | 2 | 0 | 6 of 9 | IRQ-TPR-004/-005/-006 |
| **Total** | **14** | **8** | **1** | **23 of 32** | — |

The population was derived mechanically at the 25 August 2026 register audit re-run and confirmed by the owner at signing; the derivation question — is the procedure the ★ rates predominantly an audit or compliance procedure rather than an empirical test exercised against the AI system — is recorded in ASSURANCE_MODEL.md §6A.4. No canvas outside these three domains carries a P marking. The sharpest divergences are IRQ-TPR-009 (★1 research basis, P3 settled procedure) and IRQ-GOV-012 (★2, P1 — the six-vector drift taxonomy is FAIAS-native, and the P1 triggers the novel-methodology report caveat).

## Risk-weighting likelihood (field 16) — as at FAIAS v1.3.0 (October 2026)

The likelihood axis of each canvas's field 16 (Risk Weighting Profile) runs 1–4 (ASSURANCE_MODEL.md §7), yet all 109 canvases score it 2 or 3 — 44 at 2 and 65 at 3, none at 1 or 4 — which is a property of the current calibration of the likelihood anchors.

## Open Under Research Observations (URO)

Per ASSURANCE_MODEL.md §6A.2. A URO records that a development could change a canvas's research basis. The standing ★ is untouched while a URO is open; resolution is bounded to the next signing batch or six months, whichever is first, and takes the form of a re-rating under a new anchor or of the observation being removed with the reason recorded.

No URO is open as at FAIAS v1.3.6. URO-2 to URO-8 were resolved at v1.3.6, and each is recorded under Resolved observations below.

| URO | Source, and date flagged | What it could change | Resolve by |
|---|---|---|---|

**Signing-batch limit of URO-2 to URO-5 (note of 3 October 2026).** URO-2 to URO-5 were flagged on 11 September 2026. v1.3.2 is a signing batch (`00_Admin/CORRECTION_LOG_2026-10-03.md` §8), and the releases signed between those dates did not state their class under ASSURANCE_MODEL.md §6A.2. The signing-batch limit of each of the four has therefore passed with the observation unresolved: the bound was not met. Each stays open, its standing ★ untouched, and is resolved by its date bound of 11 March 2027.

**Signing-batch limit of URO-6 (note of 9 October 2026).** URO-6 was flagged on 3 October 2026. v1.3.3 is a signing batch under ASSURANCE_MODEL.md §6A.2: it makes a register addition (incident register rows 47 to 91), changes the grading in two test procedures and opens two observations. The signing-batch limit of URO-6 has therefore passed with the observation unresolved: the bound was not met. URO-6 stays open, its standing ★ untouched, and is resolved by its date bound of 3 April 2027.

**Signing-batch limit of URO-7 and URO-8 (note of 22 October 2026).** URO-7 and URO-8 were flagged on 8 October 2026. v1.3.4 is a signing batch under ASSURANCE_MODEL.md §6A.2: it makes register additions (incident register rows 92 to 101, and one entry in the regulatory source register). The signing-batch limit of URO-7 and URO-8 has therefore passed with the observations unresolved: the bound was not met. Each stays open, its standing ★ untouched, and is resolved by its date bound of 8 April 2027.

**The resolve-by bound is enforced by the maintainer's signing check** (ASSURANCE_MODEL.md §6A.2): a scripted check that the maintainer runs over the standard's files before each signing, and that is not published with the standard. Every URO entry — here or on a canvas — states its bound in the literal form `resolve by <date>`, and the check fails once that date has passed. The form is not decorative: it is what makes the six-month bound at ASSURANCE_MODEL.md §6A.2 an enforced deadline rather than an intention.

### Resolved observations

A resolved URO leaves the open table above and is recorded here with its resolution, in one of the two forms §6A.2 permits. The record is retained rather than deleted: the register holds a sequence of dated positions, not a current value that overwrites its predecessors (ASSURANCE_MODEL.md §6A.1).

**URO-1 — resolved 12 September 2026, under the v1.2.0 anchor, by re-rating as an affirmation (§6A.2 resolution form 1).**

*The observation.* Flagged 25 August 2026 against the **OWASP Top 10 for LLM Applications, 2026 edition** (published approximately 4 August 2026), which renumbers eight of ten entries, together with any re-baselining of the **OWASP Agentic Security Initiative's** agentic threat list. Its signing-batch limb was consumed at the 27 August 2026 v1.1.1 signing, so it resolved at v1.2.0 rather than at its 25 February 2027 date bound. The bound was therefore not met: URO-1 stood open through the 27 August 2026 signing and was resolved on 12 September 2026, sixteen days after the limb expired, under the construction of "signing batch" recorded at ASSURANCE_MODEL.md §6A.2 and ruled on 12 September 2026. The timing is recorded here rather than left to be inferred, because a bound that is missed silently is not a bound.

*What the examination found.* Both primaries were retrieved from the publisher and read in full. The 2026 edition renumbers eight of ten entries and leaves the substance of all nine entries cited in this register intact, six of them broadened: LLM06:2025 Excessive Agency becomes LLM03:2026 with identical root causes and examples; LLM10:2025 Unbounded Consumption becomes LLM06:2026 with an additive expansion; LLM08:2025 Vector and Embedding Weaknesses becomes LLM09:2026; LLM07:2025 System Prompt Leakage is the one entry renamed, to LLM08:2026 Hidden Context Exposure. The agentic threat list **has** been re-baselined — "Agentic AI: Threats and Mitigations" now stands at **v1.1, December 2025** (T1–T17; T16 and T17 added, T1–T15 carried unchanged), and a separate **"OWASP Top 10 for Agentic Applications 2026", Version 2026, December 2025** (ASI01–ASI10) has been published above it, with the Threats and Mitigations guide retained as its detailed taxonomy. No AGT canvas cites the guide by T-number, so no pinpoint is affected. **Note (added 18 November 2026).** This sentence describes the canvases as they stood on 12 September 2026. From v1.3.4, IRQ-AGT-003 field 11 cites the guide's threat T2, and IRQ-AGT-006 fields 9 and 11 cite T4. The guide keeps T1 to T15 under the same numbers in v1.1, but it revises some of them, among them the name of T9 and the mitigations of T2, so the words "T1–T15 carried unchanged" above are not exact. T2 (Tool Misuse) and T4 (Resource Overload) keep their numbers and names, and the T4 entry is the same in full, so these pinpoints are not affected. The statement in this observation's superseded form, that the list "currently stands at v1.0, February 2025", was already incorrect when the observation was flagged. **The OWASP Agent Control Standard was examined from its repository (integration branch, spec v0.1.0) on 12 September 2026:** it is a runtime-enforcement wire specification and states of itself that the release "ships no conformance test suite, no registry of conformant implementations" and that a permissive, conformant deployment "is not a violation"; it supplies a way to enforce least privilege and delegation containment, not to test either, so the finding below that nothing published supplies a standardised evaluation benchmark stands on a read of the document, not on its absence.

*The resolution.* Nothing published supplies a standardised evaluation benchmark for least-privilege verification, composite-action risk, tool-boundary fault injection or aggregate-permission-tree testing, which is what each of the four affected ★2 justifications turns on. **The ★2 ratings of IRQ-AGT-003, IRQ-AGT-004, IRQ-AGT-005 and IRQ-AGT-006 are therefore affirmed, and are published under the v1.2.0 anchor.** Their ★2 positions as at v1.1.0 (25 August 2026) stand as register history; *ratings issued under different anchors are not comparable numbers* (§6A.1). The consequential citation-currency corrections — the 2026-edition crosswalk and the Agentic Security Initiative edition strings — are recorded in the canvas change logs and in the maintainer's analysis record (not published), and are not re-ratings.

**URO-2 — resolved 22 November 2026, under the v1.3.6 anchor, by re-rating as an affirmation (§6A.2 resolution form 1).**

*The observation.* URO-2 was flagged on 11 September 2026 against the OpenAI Hugging Face incident technical report of 26 August 2026. In that incident, an agent under evaluation obtained root in the parent VM of its testing sandbox. A second agent obtained the same access and then moved beyond the sandbox through a previously unknown vulnerability in a third-party package service. The observation asked whether the failure mode of IRQ-AGT-014 and its ★2 hold for a containment failure at the hypervisor boundary. Its signing-batch limit was not met (note of 3 October 2026, above).

*A correction to the open entry.* The open entry took OpenAI, *GPT-6 Astra System Card*, 3 September 2026, §9.2.2.1, to be a published method for the class. That reading was wrong. §9.2.2.1 reports the developer's own monitor-evasion evaluation: the model must bypass an inner sandbox and disable a monitoring process "within the same isolated virtual machine", over "40 coding tasks across 10 vulnerable sandbox implementations". It releases no procedure, and it does not test escape at the hypervisor boundary.

*What the examination found.* The ★2 of IRQ-AGT-014 rates the maturity of a method to assess whether a given evaluation programme is contained. No published method does that. "Quantifying Frontier LLM Capabilities for Container Sandbox Escape" (SandboxEscapeBench; Proceedings of the 43rd International Conference on Machine Learning, PMLR 306, 2026) measures a model's ability to escape a container. It does not assess the containment of a programme, and it is the work of one group. Field 11 of the canvas now names a fifth pattern for the hypervisor-boundary mechanism.

*The resolution.* The ★2 of IRQ-AGT-014 is affirmed and published under the v1.3.6 anchor, in the same act as the resolution of CEN-1 below. Its ★2 position as at v1.2.0 (12 September 2026) stands as register history. Ratings issued under different anchors are not comparable numbers (§6A.1).

**URO-3 — resolved 22 November 2026 by observation removed, with the reason recorded (§6A.2 resolution form 2).**

*The observation.* URO-3 was flagged on 11 September 2026 against UpgradeBench (Chen and Zhang, arXiv:2608.20918v1, 21 August 2026). It asked whether IRQ-MOD-002's research basis should carry UpgradeBench as a benchmark for re-approval after an announced model release, and whether that rating moves. Secondarily, it asked whether UpgradeBench bears on IRQ-TPR-004. Its signing-batch limit was not met (note of 3 October 2026, above).

*What the examination found.* UpgradeBench measures the decision to migrate a fine-tuned specialist to a new base-model release. It does not detect a newly enabled capability, which IRQ-MOD-002 tests. It does not test for a silent change by a hosted provider, which IRQ-TPR-004 tests. It is an unreviewed v1 preprint.

*The resolution.* The observation is removed for both limbs. The ★2 of IRQ-MOD-002, as at v1.1.0 (25 August 2026), stands. IRQ-TPR-004 is re-rated from ★2 to ★3 under the v1.3.6 anchor, but not on UpgradeBench. That move rests on peer-reviewed methods that detect a changed model behind an API, among them Gao et al. (ICLR 2025), which a second, independent group has applied.

**URO-4 — resolved 22 November 2026 by observation removed, with the reason recorded (§6A.2 resolution form 2).**

*The observation.* URO-4 was flagged on 11 September 2026 against Huang and Hooker, "Fairness Testing for Algorithmic Pricing" (arXiv:2605.11614v1, 12 May 2026). It asked whether IRQ-CON-006's field 11 decomposition test is the right instrument. Its signing-batch limit was not met (note of 3 October 2026, above).

*What the examination found.* Three reasons decide the rating, and none of them depends on the paper's estimator claim. (1) The paper tests price against a protected characteristic, by conditional demographic parity and proxy discrimination. That is the object of IRQ-CON-001 and IRQ-CON-002. IRQ-CON-006 asks whether a price is tied to cost or risk. (2) Field 11 of IRQ-CON-006 prescribes no regression and no significance test. (3) The paper is an unreviewed v1 preprint.

*What was not obtained.* The open entry said that resolution required a statistically competent read of the corrected-estimator claim. No read by a qualified statistician was obtained. This resolution does not rest on that claim, and it neither accepts nor rejects it.

*The resolution.* The observation is removed. The ★2 of IRQ-CON-006, as at v1.1.0 (25 August 2026), stands.

**URO-5 — resolved 22 November 2026 by observation removed, with the reason recorded (§6A.2 resolution form 2).**

*The observation.* URO-5 was flagged on 11 September 2026 against Chen, Chen, Lin and Vong, "A Judge Should Know What Changed" (arXiv:2608.24419v1, 25 August 2026). It asked two things: whether IRQ-MOD-015's ★3 test is sufficient as written, and whether the ★3 moves. Its signing-batch limit was not met (note of 3 October 2026, above).

*What the examination found.* The paper contests agreement as a measure of a judge's validity: it states that "A high agreement number is not evidence of valid evaluation". It reports that published work tested one property of a judge, invariance, and left a second property, construct sensitivity, untested. That bears on what field 11 measures. The paper is an unreviewed v1 preprint, so it cannot move a rating.

*The resolution.* The observation is removed on the second question: the ★3 of IRQ-MOD-015, as at v1.1.0 (25 August 2026), stands. This resolution does not decide the first question. Whether field 11 must add a construct-sensitivity probe stays open as a design question for a later version.

**URO-6 — resolved 22 November 2026, under the v1.3.6 anchor, by re-rating as an affirmation (§6A.2 resolution form 1).**

*The observation.* URO-6 was flagged on 3 October 2026 against the OWASP Top 10 for LLM Applications 2025, which names no access-control test method. It asked whether IRQ-DAT-009's ★3 and the method class of TP-DAT-009 hold once the OWASP limb is read as control guidance. Its signing-batch limit was not met (note of 9 October 2026, above).

*What the examination found.* The 2025 list is control guidance. A published test method exists for the entitlement part of the test: the OWASP AI Testing Guide, Version 1.0 (November 2025), AITG-APP-08 test 3, "Cross-Context Information Leakage in Multi-Tenant Environments" (printed pp. 109–110). It sets testing steps, a payload, the responses that indicate a vulnerability and the expected secure behaviour. Two peer-reviewed groups test the adversarial-query part: Zeng et al. (Findings of the Association for Computational Linguistics: ACL 2024) and Qi et al. (ICLR 2025). Both craft queries that make a retrieval system return stored content. Neither tests an entitlement filter.

*The resolution.* The ★3 of IRQ-DAT-009 is affirmed and published under the v1.3.6 anchor, with the OWASP AI Testing Guide test named as the method for the entitlement part. The method class of TP-DAT-009 is not lowered: with the guide named, that part follows a published methodology (METHODOLOGY_STANDARDS.md §3). The ★3 as at v1.1.0 (25 August 2026) stands as register history.

**URO-7 — resolved 22 November 2026, under the v1.3.6 anchor, by re-rating (§6A.2 resolution form 1).**

*The observation.* URO-7 was flagged on 8 October 2026. It asked whether IRQ-SEC-003's ★4 and the method class of TP-SEC-003 hold once OWASP LLM01:2025 is read as mitigation guidance. Its signing-batch limit was not met (note of 22 October 2026, above).

*What the examination found.* LLM01:2025 gives mitigation strategies, not a test method. Its strategy 7 asks for "regular penetration testing and breach simulations" and gives no method. The ★4 basis named LLM01:2025 as the method, so that basis does not hold. Published benchmarks for indirect injection from independent groups exist, among them Open-Prompt-Injection (USENIX Security 2024) and AgentDojo (NeurIPS 2024 Datasets and Benchmarks Track), and they meet the ★3 anchor. The ★4 anchor also asks for adoption by two or more independent institutions. That is not shown. Adoption is recorded only for AgentDojo, whose injection channel is the output of a tool, not retrieval from a knowledge store. The US and UK government AI safety institutes both used AgentDojo, but in one joint red-teaming exercise, so their use does not show adoption by two independent institutions. Two records would meet the clause. The first is a first-party record that a second institution has adopted AgentDojo as its own test method. That institution must be independent of the first and of the authors of AgentDojo, and the fit of AgentDojo to retrieval must be shown. The second is the same record of adoption, by two independent institutions, for a benchmark that tests retrieval.

*The resolution.* IRQ-SEC-003 is re-rated from ★4 to ★3 under the v1.3.6 anchor. The ★4 as at v1.1.0 (25 August 2026) stands as register history. Ratings issued under different anchors are not comparable numbers (§6A.1).

**URO-8 — resolved 22 November 2026, under the v1.3.6 anchor, by re-rating (§6A.2 resolution form 1).**

*The observation.* URO-8 was flagged on 8 October 2026. It asked whether IRQ-SEC-001's ★4, whose stated basis was "published, partially standardised methodology across ≥2 institutions", holds once OWASP LLM01:2025 is read as mitigation guidance. Its signing-batch limit was not met (note of 22 October 2026, above).

*What the examination found.* No source in the canvas's research basis shows that two independent institutions have adopted a test method. LLM01:2025 is mitigation guidance. MITRE ATLAS AML.T0051 is a technique entry with no test procedure. PAIR (Chao et al.) and Constitutional Classifiers (Sharma et al.) each come from one group. AILuminate grades a different thing, as the canvas states. The "≥2 institutions" clause was asserted, not shown.

*The resolution.* IRQ-SEC-001 is re-rated from ★4 to ★3 under the v1.3.6 anchor, and its field 11 states the ★3 basis. The ★4 as at v1.1.0 (25 August 2026) stands as register history.

## Open capability-envelope notes (CEN)

Per ASSURANCE_MODEL.md §6A.6. A CEN records a dated capability-shift event in the environment the
assured system sits in — a capability threshold declared crossed under a developer's own safety
framework, a version change to such a framework, a declared pause or restart of a capability line,
or a change to the access tier on which a capability is supplied. A CEN is not a URO: a URO observes
movement in published testing methodology, a CEN observes movement in the capability envelope. The
standing ★ is untouched while a note is open. Resolution is bounded at six months from the date
flagged and takes the form of a re-rating under a new anchor, or of the observation being removed
with the reason recorded. Both limbs are always stated, so that what the note does NOT reach —
typically the attack-resistance threat-model limb — is visible rather than implied. Where the event is a
threshold declared crossed under, or a version change to, a named safety framework, the source field
names the framework's own printed edition and date. No more than three notes stand open at once; that
is a stock ceiling, and no separate annual inflow limit is set.

**No register table is used for these notes, and that is deliberate.** A note is recorded below in the
§6A.6 note form — the note's own eight fields, each named in the note — and this section is a pointer
to that form, not a second rendering of it. The reason is mechanical as well as editorial: in a
markdown table the field labels sit in the header row and not in the data row, so a note written as a
table row does not carry the labels that the note form requires and the maintainer's signing check reads. The URO
table above is unaffected; its check is a date check on a short row.

### Resolved capability-envelope notes

No capability-envelope note is open as at FAIAS v1.3.6. CEN-1 was resolved at v1.3.6. It is kept below in its note form, with its dated `resolved:` field (ASSURANCE_MODEL.md §6A.6).

> **CEN-1** — On 1 September 2026 OpenAI stated that GPT-6 Astra meets the **Critical** cybersecurity capability threshold under its Preparedness Framework; the model was released and its system card published on 3 September 2026 ("Astra is our first model to reach the Critical level of cybersecurity capability under our Preparedness Framework"), with general enterprise availability on 9 September 2026. Two further limbs of the same event: the developer's own statement that "GPT-6 Astra's monitorability has decreased relative to GPT-5.6 Sol", that the model "is able to remain undetected when strategically underperforming in evaluations (sandbagging)" and "can sometimes evade our internal monitors when asked to perform certain sabotage tasks"; and tiered supply — an updated "Trusted Access for Cyber" programme, initial access for advanced cyber work limited to "a small group of alpha testers, with access through Daybreak Blue expanding afterward", and enterprise access off by default at launch.
> **Source** — **Framework edition: OpenAI, *Preparedness Framework*, Version 2, last updated 15 April 2025, printed p.6 / PDF p.7 (Critical cybersecurity threshold), `cdn.openai.com/pdf/18a02b5d-…/preparedness-framework-v2.pdf`, accessed 2026-09-12** — the only published edition located, and the edition carrying the threshold the declaration invokes. Declaration and model documents: OpenAI, *Path to Astra: critical capabilities and frontier safeguards*, 1 September 2026, §"Assessing Astra's cybersecurity capabilities" and §"Robustness against cyber abuse"; OpenAI, *Safety overview: GPT-6 Astra*, 3 September 2026, opening and §"GPT-6 Astra's monitorability has decreased relative to GPT-5.6 Sol"; OpenAI, *GPT-6 Astra System Card*, 3 September 2026, §10.1.2 (cyber) and §"Cybersecurity — Trusted Access for Cyber" — all read from saved copies, accessed 2026-09-11. Sector frame, for context and not as an expectation: FCA, *Frontier AI and cyber resilience*, multi-firm review, 2 September 2026, which "does not introduce new rules, guidance or regulatory expectations"; Bank of England, *Frontier AI: Harness engineering*, FAISF, 2 September 2026, which "does not set new Bank supervisory expectations or policy".
> **Date flagged** — 11 September 2026.
> **In-scope limb** — (i) the **reasoning-trace class**: every canvas whose expected control or expected evidence depends on a model's verbalised reasoning being a faithful and readable record. A first-party statement that monitorability has decreased, and that a frontier model can evade first-party monitors under adversarial conditions, bears directly on the research basis for that class. (ii) the **supplied-access class**: where a capability is available only on a vetted tier, the evidence level reachable in an engagement is constrained by the provider's tier, not by the reviewer's method — a stated limitation, not a rating change. (iii) **the framework edition's own terms**: Preparedness Framework v2 states, of Critical capability, "We do not currently possess any models that have Critical levels of capability, and we expect to further update this Preparedness Framework before reaching such a level with any model" (v2, printed p.12). No later edition of the framework was located as at 2026-09-12. The developer has separately stated, on 18 August 2026, "We will evolve our Preparedness Framework to bring these safeguards together across training and deployment, and to better reflect the capabilities of future models and the environments in which they operate" (openai.com, *Pacing model development in an era of cyber-critical capabilities*). Recorded as the dated state of the published record; no conclusion is drawn about the developer's conformity with its own framework.
> **Out-of-scope limb** — the uplift to the firm's threat model from model-enabled vulnerability discovery and exploitation, other than as an input to the threat model of its own AI systems, and the resistance of the firm's controls, other than its own AI systems, to attack by external parties using that capability — including its identity, authentication and payment-authorisation controls — are **out of FAIAS scope under the scope decision recorded at v1.0.3**. That decision was reviewed at v1.3.5 and stands. TAXONOMY.md now states that attacker capability is an input to the threat model of the institution's own AI systems; no risk axis and no ★ rating moves on that statement. No watchlist entry for this limb is carried in this standard. No IRQ is created, amended or re-rated on that limb.
> **Re-baselines** — IRQ-MOD-009, IRQ-MOD-003, IRQ-MOD-007, IRQ-MOD-008, IRQ-AGT-009, IRQ-AGT-014, IRQ-SEC-004 (seven canvases; membership derived mechanically by term search of the canvas files on 11 September 2026 and adjudicated by the owner, not by the search). The ★ on each stands untouched while this note is open.
> **Re-test trigger** — engagements whose opinion relies materially on reasoning-trace or chain-of-thought evidence, and which were issued **before 3 September 2026**, are identified as a class a commissioning firm may wish to have re-run. Advisory; creates no obligation on the reviewer and no entitlement in any reader (§6A.5, §6A.6).
> **resolve by 2027-03-11**
> **Resolved:** 22 November 2026, for the note as a whole, by re-rating under a new anchor (§6A.2 resolution form 1). Each of the seven canvases was examined, and each rating is published under the v1.3.6 anchor. IRQ-MOD-009 and IRQ-SEC-004 are re-rated from ★2 to ★3. IRQ-MOD-003, IRQ-MOD-007, IRQ-MOD-008, IRQ-AGT-009 and IRQ-AGT-014 are affirmed at ★2 (IRQ-AGT-014 in the same act as URO-2). The event changes the capability environment, not the published testing methods that a ★ rates. The two raises rest on a review of the published methods that each canvas names, not on the event. A ★ rates the maturity of a test method, not the size of a risk, and no risk axis moves on this resolution. Where a test reads a model's stated reasoning as evidence (IRQ-AGT-014 field 11, measure (4); a worked example in IRQ-MOD-008 field 10), the developer's statement that monitorability has decreased makes that evidence weaker: a trace that shows no recognition is not evidence of no recognition. That is a limit on the evidence, not on the maturity of the method. Limb (ii) records a limitation, not a rating change. Limb (iii): the published record was read to 17 November 2026, and the GPT-6.2 System Card of that day was read on 19 November 2026. No later edition of the framework was located, and the current edition is still Version 2, last updated 15 April 2025, as printed on the document. On 29 September 2026 OpenAI stated that it treats GPT-6.1 Sol as Critical in cybersecurity under the same framework (OpenAI, *Addendum to GPT-6 Astra System Card: GPT-6.1 Sol*, 29 September 2026, §9). On 5 November 2026 OpenAI classified a further model, GPT-6 Cyber, as Critical in cybersecurity under its Preparedness Framework, of which Version 2 is still the current edition (OpenAI, *GPT-6 Cyber: Advancing the frontier of aligned cybersecurity agents*, 5 November 2026). On 17 November 2026 OpenAI stated that GPT-6.2 Astra and GPT-6.2 Sol meet the Critical threshold for cybersecurity under its Preparedness Framework, and the card's link for the framework is to Version 2 (OpenAI, *GPT-6.2 System Card*, 17 November 2026). None of the three declarations moves any of the seven ratings, and no new note is opened for any of them.

**The bound on a capability-envelope note is enforced by the maintainer's signing check**, on the same terms as the URO bound
above: the note states it in the literal form `resolve by <date>`, and the check
reads the note as a whole and also fails a note that omits one of the seven labelled fields, names
fewer than two IRQ IDs, or is the fourth open at one time.

## Gap-check dispositions (parallel Data-domain proposal, four-test assessed)

| Topic | Disposition |
|---|---|
| Feedback data contamination | **Added as IRQ-DAT-013 (A.2).** Genuine gap: IRQ-MOD-012 covers recursive synthetic-content collapse and IRQ-CON-007 covers outcome-level feedback loops, but neither covers the feedback *channel* (user ratings, corrections, thumbs-up signals) as an unvetted, adversarially gameable training-data ingestion path. Passes all four tests: SMEs treat feedback as benign telemetry (test 1); documented incidents of feedback-channel manipulation and preference-tuning drift (test 2); testable via pipeline documentation review and staged feedback-injection in non-production (test 3); gates any continuous-learning deployment (test 4). |
| Data minimisation / purpose limitation | **Not added — fails test 1.** Purpose limitation and minimisation are core DPO/GDPR territory a privacy SME would not overlook; the AI-specific residue (personal data in corpora without lawful basis and minimisation assessment) is already IRQ-DAT-002. Recorded as deliberate gap 8 below. |
| Synthetic data reliability | **Covered via amendment to IRQ-DAT-004** (no new IRQ). Existing wording covered identification and distributional fidelity; identification ≠ representativeness, so the question now explicitly requires validation that synthetic data preserves rare events, minority subgroups and real-world complexity rather than concealing risk. A separate IRQ would duplicate DAT-004's evidence base. |
| Ground truth / label quality | **Already covered — no change.** IRQ-DAT-003 (inter-annotator agreement, measured error rates, acceptance thresholds) fully addresses the proposed topic. |

## Four-test dispositions — additions since v1.0.3

| IRQ | 1 · SME blind spot | 2 · Evidenced harm mechanism | 3 · Answerable pre-deployment | 4 · Decision-gating |
|---|---|---|---|---|
| IRQ-GOV-013 | Yes — remediation practice is complaint-led | Robodebt Royal Commission (7 Jul 2023) | Yes — cohort-query capability demonstration in test/staging | Yes — bears on authorisation conditions for consequential-decision systems |
| IRQ-GOV-014 | Yes — incident taxonomies predate AI failure classes | Regulatory-instrument-led, not research-led: DORA Art. 17's categorisation requirement and Art. 19's notification structure, and FCA SUP 15.3.1R's "becomes aware" trigger, all presuppose that the event is first identified and logged as an incident, which a taxonomy with no AI-specific failure class makes unlikely for failures that raise no conventional error state | Yes — documentation review plus tabletop | Yes — notification capability conditions authorisation |
| IRQ-MOD-014 | Yes — QA treats a one-off pass as durable | CLM-04's unevidenced "consistently"; stochastic sampling documented | Yes — repeat-run protocol in dev/test | Yes — flip rate on consequential decisions conditions approval |
| IRQ-MOD-015 | Yes — the evaluator is treated as neutral infrastructure | Zheng et al., arXiv:2306.05685 (NeurIPS 2023 D&B) | Yes — human re-scoring, order-swap and length-matched testing | Yes — unsound evaluation evidence undermines every downstream conclusion |
| IRQ-CON-009 | Yes — red-teaming has crowded out ordinary-use harm testing | Grounded in published evidence that an AI system can give abusive output that the user did not solicit, in the authors' reading (Zhang et al., CHI 2025; none of it from financial services) and in incident-register rows 58 and 101; AILuminate's hazard taxonomy (Ghosh et al., 2025) is the closest available taxonomy for a structurally distinct, currently untested failure surface; no published FS-specific incident report confirming an AI system produced harmful, abusive or degrading output to a customer under genuinely non-adversarial conditions was located, an absence consistent with an untested surface and not evidence of low risk | Yes — harm-taxonomy probe under normal-use prompts | Yes — a customer-facing system failing this is not authorisable under Consumer Duty |
| IRQ-SEC-012 | Yes — misuse of a working system falls between security and conduct | Yes, thin — the risk is structural; rated ★1 accordingly | Yes, partially — register review and interview | Yes, where the applicability condition bites |
| IRQ-HUM-009 | Yes — oversight design assumes AI output is one input, not dispositive evidence | Robodebt; Michigan MiDAS; UK ETS/TOEIC (NAO 2019) — three jurisdictions, same shape; at v1.2.1 also the Post Office Horizon and Dutch childcare benefits cases, five systems in four jurisdictions | Yes — documentation review and case-file sampling | Yes — contestability is meaningless without a disclosed evidential basis |
| IRQ-DAT-014 | Yes — validation checks accuracy against the label, almost never the label itself | Obermeyer et al., Science 2019 — peer-reviewed, replicated | Yes — construct-mapping review and subgroup label analysis | Yes — a mis-specified target is a governance re-specification, not a tuning fix |
| IRQ-SEC-013 | Yes — control validation uses historical case libraries, structurally blind to adaptation | NIST AI 100-2e2025 evasion class; MITRE ATLAS; FTC v. Rite Aid | Yes — adversarially constructed test sets in dev/test | Yes — an unmeasured miss rate defeats the approved risk appetite |
| IRQ-GOV-015 | Yes — claims are owned by commercial teams with no link to the validation record | SEC enforcement against unsubstantiated AI capability claims, already in the incident register | Yes — reconciliation-process and claim-trace review | Yes — unreconciled claims are live enforcement exposure |
| IRQ-TPR-009 | Yes — AI vendor diligence runs on a safety/security lens; standing sits elsewhere | Mobley v. Workday (vendor-exposure principle); continuity-specific evidence thin, ★1 reflects it | Yes — documentation and contract review | Yes — conditions approval for materially important deployments |
| IRQ-SEC-014 | Yes — output from the firm's own model is a natural but wrong trust inference | OWASP Top 10 for LLM Applications 2025, LLM05 | Yes — crafted-payload testing at each output boundary | Yes — an unhandled output path is a live vulnerability |
| IRQ-GOV-016 | Yes — risk-data aggregation discipline was built for system-sourced data, not AI-generated content | BCBS 239 (the framework being extended); AI-specific gap reasoned from first principles | Yes — flagging-mechanism and sample-trace review | Yes — an untraceable AI contribution to a return is a reporting-integrity failure |
| IRQ-AGT-014 (added at v1.1.0, 25 Aug 2026) | Yes — evaluation and testing are treated as the safe activity, not a risk surface | Realised, not merely plausible: at admission, ten separately documented events, enumerated, not asserted, in the canvas's four-test validation, occurring February–August 2026 across three frontier labs, one national institute and one independent third-party evaluator, with one shared evaluation vendor behind two of the lab incidents (first-party disclosures for the core incidents, the Meta instance press-relayed; UK AISI incident report, 4 Aug 2026); at v1.2.0 twelve events, the record spanning January–September 2026, across the same parties and one external testing partner's own sandbox; at v1.2.1 eleven, one of the twelve excluded as a red-teaming exercise the evaluator set against its own production infrastructure, not a containment failure, and the Meta instance rests on Meta's own account of 14 Aug 2026 and on press reporting | Yes — documentation and configuration review of containment design, non-production | Yes — gates whether agentic access to test environments is authorised and on what containment conditions |
| IRQ-MOD-016 (added at v1.2.0, 12 Sep 2026) | Yes — validation practice treats a UAT or pilot pass as evidence about deployment; "is the evaluation environment distinguishable from production, and does the system act on that" appears in no model-risk checklist, supervisory publication or assurance standard located | Verbalised evaluation awareness reported by the publishers of the models concerned: 41.1% of samples at xhigh and 50.6% at max reasoning effort, measured by Apollo Research (OpenAI, GPT-6 Astra System Card, §8.8.1), 9.6% vs 2.8% of trajectories in the publisher's own deployment simulation (§8.6), Apollo's highest observed rate to date on another vendor's model with **that vendor's own** follow-up analysis finding behavioural impact in 3 of 20 evaluations, "none related to dangerous capabilities or launch decisions", and that vendor's own measurement of evaluation suspicion in 19.8% of samples on publicly available benchmarks against 2.0% on internal evaluations (Meta, 26 May 2026) — and the deployer-relevant corollary that pilot usage is named as the one case where awareness is not a concern "because this is taken from the real deployment distribution" (Anthropic Risk Report, p.48). First-party publisher disclosure; no FS measurement located | Yes — as an evidence-gathering activity: documentation review of the evaluation-environment record, sampling of the firm's own pilot and staging evidence, trace-rate scoring where traces are retained, and paired test-framed/deployment-framed runs in staging at a pinned configuration. **The reviewer reads the firm's pilot evidence and runs nothing in production** | Yes — an authorisation resting on pre-deployment evidence of unestablished external validity rests on an unquantified proxy; this conditions the authorisation itself and the approved envelope drawn from that evidence, not merely the wording |
| IRQ-CON-010 (added at v1.2.0, 12 Sep 2026) | Yes — contested, and ruled in: a completed sludge audit gives positive assurance, and FG22/5 ¶11.24 places such audits at regular or ad hoc intervals — periodicity only, the journey-as-designed scope being this register's inference rather than ¶11.24's words; the AI-specific delta is friction composed at run time and varied per customer, which no existing CON artefact or test reaches. Admitted against the register's own fold-in precedent (AI-TPR-008, AI-RES-007, deliberate gap 8) on that delta | PRIN 2A.6.2R(4) (binding rule), 2A.6.3G, 2A.6.4G(2) and FG22/5 ¶9.25–9.27 name the mechanism; METHODOLOGY_STANDARDS.md §3a **Test 2's** criterion is disjunctive and regulation alone satisfies it (§3a as a whole requires all four tests). Method maturity is carried by the ★1, not by this test; Zac et al. (2025) supports manipulative design affecting behaviour generally | Yes — journey walk-through with repeat runs, paired near-identical-profile probes and configuration review in test/staging and against design artefacts; no production customer, live account or real cancellation, claim or complaint | Yes — a journey making exit, switching, claiming or complaining disproportionately effortful relative to acquisition is not authorisable under PRIN 2A.6.2R(4) whatever its price, eligibility and disclosure separately show |

## Four-test removals and merges (from the 88-item pre-IRQ register)

| Former ID | Disposition | Rationale |
|---|---|---|
| AI-TPR-008 (licensing/IP) | Merged into IRQ-DAT-001 (training-data licence/copyright) and IRQ-TPR-002 (contractual usage rights) | Failed test 1 standalone: licence review is standard legal/procurement diligence a domain SME would not overlook; the AI-specific residue (corpus provenance, output rights) is retained in its two homes. |
| AI-RES-007 (capacity/latency under stress) | Merged into IRQ-RES-002 | Failed test 1 standalone: capacity management is core ITSM; the AI-specific residue (plausible-but-unsupported outputs and duplicated agent actions under stress) is retained. |
| AI-DAT-010 (upstream reference-data change control) | Merged into IRQ-DAT-011 (source drift) | Failed test 1 standalone: upstream change control is standard data management; retained as the source-drift facet of A.5. |
| AI-MOD-006 (concept vs data drift distinction) | Merged into IRQ-MOD-010 | Superseded by the six-way shift taxonomy; a separate concept-drift IRQ would duplicate one cell of it. |

## Additions in the IRQ restructure (seven added; net +3 after the four merges above)
IRQ-DAT-008 (conflicting documents / retrieval determinism), IRQ-DAT-011 and IRQ-DAT-012 (drift decomposition), IRQ-MOD-002 (capability expansion without re-approval), IRQ-MOD-005 (epistemic-state distinction under hallucination), IRQ-AGT-002 (goal drift split from planning), IRQ-AGT-009 (hidden reasoning dependencies). All seven pass the four tests; each is grounded in documented frontier behaviour (index invalidation on embedding change, silent capability jumps on model releases, goal persistence after intent withdrawal, prompt-as-configuration incidents).

## Applicability coverage
- Agentic-applicable: 109 (all AGT items plus inherited). Generative-applicable: 92. Predictive-applicable: 65.
- Agentic-only IRQs: all IRQ-AGT plus IRQ-SEC-004, IRQ-SEC-010, IRQ-SEC-011.
- Applicability-conditional: IRQ-SEC-012 (applies only where the register's stated trigger conditions are met, confirmed at scoping). IRQ-MOD-014 is predictive-N with a stated exception (flips to Y where a predictive stack samples at inference). IRQ-MOD-016 is predictive-N on the same convention — the mechanism requires the system to condition behaviour on inferred context, which a predictive model does not do — and flips to Y where a predictive stack samples at inference or sits behind a generative wrapper.

## Deliberate gaps (with rationale)
1. **Questions answerable only by testing in production** — excluded under the non-production rule (METHODOLOGY_STANDARDS.md §3); every IRQ is framed for documentation review, non-production testing or interview evidence (four-test criterion 3).
2. **AI safety frontier behaviours — split and ruled on at v1.2.0 (12 September 2026; owner's decision of 11 September 2026). The gap is narrowed, not struck.**
   - **2a — Evaluation-validity behaviours (evaluation awareness; evaluation-versus-deployment behavioural divergence): NO LONGER A GAP.** Ruled in as one question, **IRQ-MOD-016** (MOD · B.5), at ★2. The deployer-side question is not "is this model evaluation-aware" — which a firm consuming a hosted model cannot settle — but whether the firm's own pre-deployment evidence has an established basis for external validity against deployment conditions. That question is answerable by documentation review of the evaluation-environment record, by sampling the firm's own pilot and staging evidence, by scoring retained evaluation traces, and by paired test-framed and deployment-framed runs in staging: the reviewer examines the firm's evidence and runs nothing in production. The first-party quantified evidence and the absence findings behind the ruling are recorded in the canvas's fields 10, 17 and 18.
   - **2b — Deceptive alignment and covert-sandbagging detection: STILL EXCLUDED, reason corrected.** The July reason ("fail test 3") was wrong as stated. The correct reason is **access**: testing for strategic sandbagging or deceptive alignment directly requires provider-side reasoning traces, activations and weights, none of which is available to a deployer reviewing a hosted model — and the lab's own mitigation is oversight-based, not a model test, which FAIAS already tests through the HUM/GOV oversight questions and through the AGT gates (IRQ-AGT-003, IRQ-AGT-012), which hold whether or not a deceptive model is detected. Partially covered via IRQ-MOD-008 (post-training optimisation artefacts) and IRQ-MOD-009 (stated-reasoning unfaithfulness per decision).
   - **2c — Self-exfiltration and containment escape by the system under test: CARRIED, not excluded.** Strict-sense self-exfiltration (weights) is demonstrated only in constructed research settings and the deployer does not hold the weights of a model it consumes; the provider-side question is an IRQ-TPR-001 diligence object. Containment escape of an evaluation environment is IRQ-AGT-014's territory and is carried there by a dated observation flag and §11 scenario extensions rather than by a new question.
   - **Test 3 is not the ★ scale, and this item previously conflated them:** test 3 asks whether a question can be answered through evidence and safe testing in a development or test environment, not whether the published method for answering it is mature — which is what the ★ rating records, so a question that can be answered poorly is admitted with a low ★ and not excluded.
3. **Environmental/sustainability impact of AI compute** — a disclosure matter, not an assurance review question; fails test 1.
4. **Generic IT general controls** (patching, segmentation, human IAM) — assumed covered by the firm's ITGC audit universe; FAIAS itemises only AI-specific deltas (IRQ-SEC-009, IRQ-SEC-011).
5. **Financial crime model specifics** (AML tuning, sanctions thresholds) — use-case-level testing, which this register does not itemise; the register stays use-case-agnostic.
6. **Workforce impact of AI adoption** — HR governance matter, except skill atrophy (IRQ-HUM-003) which directly affects control effectiveness.
7. **Market-wide systemic herding from common foundation models** — captured at firm level only via IRQ-TPR-008 and IRQ-CON-007; systemic analysis is a regulator's lens, not a single-firm IRQ.
8. **Data minimisation / purpose limitation as a standalone IRQ** — fails test 1 (standard DPO/GDPR compliance territory); the AI-specific residue is retained in IRQ-DAT-002. See gap-check dispositions above.
9. **Resistance of the institution's controls, other than its own AI systems, to attack by external parties, including its identity, authentication and payment-authorisation controls, whether or not the attack uses AI** — excluded from the standard's scope. FAIAS assures the institution's own AI; institutions are directed for the attack-resistance need to existing supervisory security testing regimes (CBEST; TIBER-EU/STAR-FS; DORA threat-led penetration testing) and to their ICT vulnerability management. Review questions of that class are held outside the standard as a strategic option. See the scope exclusion in TAXONOMY.md.

## Cross-reference integrity
Every register row carries at least one Related IRQ; all 16 boundary rulings in TAXONOMY.md resolve to single-homed IRQs; cross-links are recorded on the owning canvas's side (field 19) and are not asserted to be bidirectional in every case.
