# Correction log — 3 October 2026 (v1.3.0 and v1.3.2)

Changes made in v1.3.0 to text signed at v1.2.1. This version prepares FAIAS for open publication: it publishes the standard under CC BY 4.0, presents the standard as a baseline that supports several uses, makes the opinion layer and its templates illustrative and aligned with ISAE 3000 rather than conformant to it, states the non-production rule once, states governance roles as functions held by the maintainer, and corrects errata found in preparing the release. Format follows CORRECTION_LOG_2026-09-19.md. An entry that rests on a published source names that source; the other entries rest on the owner's decisions of 3 October 2026 and on the standard's own text. The change histories of the affected canvases and playbooks carry their own v1.3.0 (2026-10) lines.

## 1. Licence and ownership

- `00_Admin/OWNERSHIP_AND_LICENCE.md`, `README.md` §2A, `LICENSE` (new): FAIAS is published under the Creative Commons Attribution 4.0 International licence; the licence text is added as `LICENSE`. The ownership document states copyright, the licence, the requested form of credit, a name and integrity notice that is not part of the licence, how to contribute (issues or pull requests, under the Developer Certificate of Origin 1.1), and third-party material. Before this version, no licence, exclusive or otherwise, had been granted to any party. Basis: the owner's decisions of 3 October 2026; Primary: CC BY 4.0 legal code.

## 2. The opinion layer and its templates

- `00_Admin/OPINION_TEMPLATE.md`: marked non-normative; states that FAIAS draws on ISAE 3000's conclusion forms and does not make an engagement ISAE-conformant; adds an intended-use paragraph and limits classification and distribution to the addressee and named recipients; the dashboard and conclusions read as recommendations to the firm, whose own approval authority decides; pre-deployment conclusions speak to control design and to performance in non-production testing, with operating effectiveness in production left to post-deployment re-assurance; the review-confidence grade is removed from the cover and the risk table, and Part G's grade is labelled internal; reasonable assurance is not available where a material claim rests on a ★1–★3 test; escalation at one materiality lens; ★5 glosses corrected; example tables brought within the register and the ★ distribution.
- `00_Admin/VOLUME_TEMPLATES.md`: Components 4, 6 and 7 marked non-normative; the ISAE alignment sentence replaces the compliance and Big Four wording; the opinion's audience is the commissioning firm; escalation at one lens; conclusions as recommendations; the issued confidence grade replaced by the statement on the basis of the review; professional responsibilities no longer require an ISAE compliance statement.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: the ISAE alignment sentence; the assurance-level rule (no reasonable assurance on a material ★1–★3 test), with the ISAE mapping table replaced by an assurance-level table; "safe for deployment", "regulatory reliance" and the licence metaphor removed; worked examples re-rated to the battery, ★ removed from operational records, the IRQ-MOD-004 label corrected; the ISAE 3000 reference dated correctly.
- `00_Admin/ASSURANCE_MODEL.md`: the ★5 anchor states the settled financial-services benchmark condition; anchor examples corrected (no ★5 example in the standard; the non-existent NIST procedures removed).
- `00_Admin/TIERING_MODEL.md`: Tier 2 and Tier 3 opinion types follow the assurance-level rule; Tier 1 names ★1–★2 disclosure; the Tier 3 audit no longer names a class of firm.
- `00_Admin/ENGAGEMENT_MODEL.md`: test-confidence expectations follow the assurance-level rule; the review-confidence step is internal and the deliverable is the statement on the basis of the review.
- `00_Admin/IRQ_TEMPLATE.md`: the field-11 example no longer cites a risk list as a test method and is rated ★3.
- `00_Admin/METHODOLOGY_STANDARDS.md`: an example no longer presents the OWASP Top 10 as a test method.
- `00_Admin/DEVELOPMENT_APPROACH.md`: comparative claims removed; the honesty commitment describes the basis of the review rather than a confidence grade.
- `README.md`: the opinion states the basis of the review and never grades it; ISAE wording aligned; Components 4, 6 and 7 marked non-normative.
- `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: tier ★ minimums follow the assurance-level rule; Tier 1's disclosure covers ★1 as well as ★2 procedures; the friction note carries the as-at ★ count and its consequence.
- `V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md`: the ISAE 3000 row records alignment, not compliance.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: a note after the review-confidence thresholds states that, on the current battery, no engagement reaches High Review Confidence, because no test is rated above ★4. Basis: the ★ ratings in the battery.

## 3. Framing and wording

- `README.md`: §1 presents FAIAS as a baseline that supports several uses, states the production rule's location, and states the release's status as emerging thinking open to contribution; the canvas size claim removed.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: the opening describes the opinion as one use of the baseline; the uncited comparison table removed; custodian stated as the maintainer.
- `00_Admin/IRQ_TEMPLATE.md`: canvas size claims removed.
- `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`, `00_Admin/ENGAGEMENT_MODEL.md`, `00_Admin/TIERING_MODEL.md`: engagement-pricing wording made neutral.
- `00_Admin/METHODOLOGY_STANDARDS.md`, `00_Admin/ID_SCHEME.md` and ten other documents: governance roles stated as functions held by the maintainer; engagement gates name the reviewing team's own roles.

## 4. Rules and citations

- `00_Admin/METHODOLOGY_STANDARDS.md`: the non-production rule stated once: the reviewer never tests production; read-only records and the firm's own controlled resilience exercises are admissible evidence, identified as such; a staging replica is a test environment; the inclusion criterion follows the rule; FAIAS's name and the ATT&CK name corrected; the research and incident citation examples replaced with a real source and an illustrative placeholder.
- `00_Admin/IRQ_TEMPLATE.md`: the example citations corrected (NIST AI RMF MEASURE 2.4; PoisonedRAG; Ji et al.; the AI RMF 1.0 URL); the failure-chain example names IRQ-MOD-006 for calibration.
- `00_Admin/OPINION_TEMPLATE.md`: the AI RMF entry gives its four functions; the PRA citation becomes FS2/23, a feedback statement; the ECB row becomes a placeholder; Component 1 described as the taxonomy, with regulation in the regulatory crosswalk.
- `00_Admin/VOLUME_TEMPLATES.md`: Component 1 is the taxonomy; regulation is referred to the regulatory crosswalk; the opinion's limitations state the non-production rule; component labels corrected.
- `00_Admin/TIERING_MODEL.md`: Tier 0 names its five governance questions.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: the Not Testable presumption points to the non-production rule.
- `README.md`: the evidence catalogue described as carrying supporting claim statements; the outcome of the four ★ questions from the July correction log stated.
- `V2_IRQ_Battery/TAXONOMY.md`, `V2_IRQ_Battery/canvases/CANVASES_SEC.md`: the scope sentence points to the non-production rule.
- `V2_IRQ_Battery/REGISTER_STATS.md`: the production-testing gap points to the non-production rule; a disclosure of the field-16 likelihood distribution added.
- `V2_IRQ_Battery/IRQ_REGISTER.md`: eight rows moved into subdomain order; no row changed.
- `V2_IRQ_Battery/canvases/CANVASES_RES.md`: IRQ-RES-001, -005, -006, -007 — SYSC 15A.5.3R for scenario testing; DORA Art. 10(2) for threshold-triggered response; the AI RMF 1.0 URL; the controlled live exercise is the firm's own. No rating moves.
- `V2_IRQ_Battery/canvases/CANVASES_GOV.md`: IRQ-GOV-010 — a cross-reference identifier corrected.
- `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: two evidence routes from production, not three exceptions; the reviewer does not run the live exercise; the regulatory crosswalk named for regulation.
- `V3_Testing_Playbook/PLAYBOOK_RES.md`: TP-RES-001 cites SYSC 15A.5.3R and takes the firm's own live exercise as evidence only.
- `V3_Testing_Playbook/PLAYBOOK_DAT.md`: the preamble follows the non-production rule.

## 5. IRQ-AGT-014 and its sources

- **IRQ-AGT-014, fields 9, 10, 11, 18, 20 and 21; TP-AGT-014; SOURCE_REGISTER_REGULATORY.md, the Inspect Sandboxing Toolkit row.** The configuration-responsibility qualification was recorded as press-reported only and absent from the toolkit's own text; AISI's technical guidance for the toolkit, in the toolkit repository since 7 August 2025 and linked from the launch post, carries it at p.1 ("Note that it is up to users to make the ultimate decision as to the correct level of security and sandboxing for the evaluation they run"), and all four sites now cite it; the rating stays with reasons (b) and (c). Field 9's second fact attributed the allowlist of the August 2026 episode to the configuration Inspect generates for its Docker sandbox; the Inspect sandboxing documentation gives that configuration as `network_mode: none`, and Frontier Security's account describes the allowlist as the sandbox's, and field 9 now says so. Worked example (iii) placed the risk report's second quotation in the same sentence as the first; it opens the next sentence. Worked example (iv) now uses the letter's words, "not given access". In field 18, the limb counting occurrences of the candidate name is removed: the name is withheld from the standard, so the limb could not be tested, and its two sibling limbs carry the finding. URO-2 placed the previously unknown vulnerability at the root access within the parent VM; the technical report places it at the agents' move beyond the sandbox and states no mechanism for the root access. Titles styled as their publishers give them: the toolkit launch post ("Scalable"), OpenAI's research-acceleration page ("The view"), AEF-1 ("Third Party"), with AEF-1 dated to "Version 1, updated December 4, 2025". Primaries: AISI, "Technical guidance: sandboxing configurations for agentic evaluations", p.1; Inspect, "Sandboxing" documentation; Frontier Security, 7 August 2026 (updated 8 August); Anthropic, Risk Report, August 2026 (redacted), p.83; Office of Senator Josh Hawley, letter of 9 September 2026; OpenAI–Hugging Face Incident Technical Report, §IV.A; AI Evaluator Forum, AEF-1.
- **REGISTER_STATS.md, URO-2.** As for IRQ-AGT-014 field 18 (above), in both cells.
- **SOURCE_REGISTER_LABS.md, the entry of 30 July 2026.** The entry's unquoted "a lab–evaluator scope-of-work failure, not a model-control failure" is replaced with the page's own hedged classification and the lab's 9 September 2026 addition.

## 6. Document version headers

- Eighteen documents: their own version and date headers are replaced by a pointer to the release version in `README.md` and the signed manifest.

## 7. Corrections found on verification before release

- `README.md`: the uncited framework comparison table removed with the §1 rewrite.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: the opening sentence completed as ruled.
- `00_Admin/METHODOLOGY_STANDARDS.md`, `00_Admin/ID_SCHEME.md`, `V4_Evidence_Catalogue/EVIDENCE_PACK.md`, `00_Admin/VOLUME_TEMPLATES.md`: remaining governance roles stated as the maintainer; the change-log rule describes release versions.
- `00_Admin/VOLUME_TEMPLATES.md`: the Component 1 pointer no longer claims that taxonomy entries refer to the crosswalk.
- `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: a change log added.
- `00_Admin/DEVELOPMENT_APPROACH.md`: the opinion is described as drawing on ISAE 3000 conclusion forms.
- `00_Admin/OPINION_TEMPLATE.md`: the professional-responsibilities line names the quality standard of the 2013 text (ISQC 1 or its successor). Primary: ISAE 3000 (Revised), para 31(a) and para 69(i).
- `00_Admin/VOLUME_TEMPLATES.md`, `00_Admin/ENGAGEMENT_MODEL.md`, `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: the evidence catalogue and Phase 4 are owned by the Testing Lead, a role the engagement model defines, in place of an Evidence Manager it does not define.
- `00_Admin/OPINION_TEMPLATE.md`, `00_Admin/ENGAGEMENT_MODEL.md`, `V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md`: the quality-control review's fourth element includes the evaluation of the conclusions reached in formulating the report. Primary: ISAE 3000 (Revised), para 36(b)(iv).
- `00_Admin/OPINION_TEMPLATE.md`: the example basis for a positive conclusion reads "regulatory alignment assessed", not "confirmed".
- `00_Admin/ASSURANCE_ARCHITECTURE.md`, `00_Admin/VOLUME_TEMPLATES.md`, `00_Admin/OPINION_TEMPLATE.md`, `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: the assurance-level sentence names a material test; the claim of comprehensive assurance removed (`ASSURANCE_ARCHITECTURE.md`).
- `V2_IRQ_Battery/TAXONOMY.md`, `V2_IRQ_Battery/canvases/CANVASES_SEC.md`: the scope sentence refers to the uses listed in `README.md` §1.
- `00_Admin/OWNERSHIP_AND_LICENCE.md`, `README.md` §2A: the licence summary refers to section 3 of the licence for the conditions in full; the scope of the licensed rights is cited to §1(g) with §2(b)(2). Primary: CC BY 4.0 legal code.
- `V2_IRQ_Battery/canvases/CANVASES_AGT.md`: reference [9] gives AEF-1's date in the PDF's form.

## 8. Corrections in v1.3.2

Changes made in v1.3.2 to text signed at v1.3.1, after a full read of the standard before publication. Each correction against a source was checked at the primary. No Independent Review Question, claim, ★ rating, risk profile or procedure's reviewer-day figure changes. One under-research observation is opened (URO-6). v1.3.2 is a signing batch under `00_Admin/ASSURANCE_MODEL.md` §6A.2: it amends a test procedure and a rule and opens an observation.

### 8.1 Titles, dates, links and quotations

- Quoted titles corrected to the title of the cited version: "Hallucination-Free?" (`V2_IRQ_Battery/canvases/CANVASES_DAT_007.md`, `V1_Research_Compendium/SOURCE_REGISTER_ACADEMIC.md`); ToolEmu and AgentHarm (`CANVASES_AGT_005.md`, `CANVASES_SEC_004.md`, the academic register); "Sycophancy to Subterfuge" (`CANVASES_MOD_008.md`, the academic register); "Underspecification Presents Challenges for Credibility in Modern Machine Learning" (`CANVASES_MOD_001.md`, `CANVASES_MOD_010.md`, `CANVASES_DAT_005.md`, the academic register); "NLP Evaluation in Trouble" and "Time Travel in LLMs" (`CANVASES_MOD_011.md`, the academic register); the GSM1k paper, "To the Cutoff... and Beyond?", PoisonedRAG (also `CANVASES_SEC_005.md`) and "Does the Whole Exceed its Parts?" (the academic register); "Sleeper Agents" (`V1_Research_Compendium/SOURCE_REGISTER_LABS.md`); the Vaccaro et al. subtitle (`CANVASES_HUM_006.md`, `CANVASES_HUM_008.md`); the Stanford Internet Observatory article (`CANVASES_DAT_001.md`).
- OWASP entry names: ML06:2023 ML Supply Chain Attacks (`CANVASES_TPR_005.md`); LLM03:2025 Supply Chain (`CANVASES_SEC_009.md`); IRQ-DAT-009 cites LLM08:2025 Vector and Embedding Weaknesses as control guidance (`CANVASES_DAT_009.md`, `V3_Testing_Playbook/PLAYBOOK_DAT_009.md`).
- Dates: the EU AI Act was published in the Official Journal on 12 July 2024 (IRQ-HUM-001, -002, -004, -005, -007 and -008); IRQ-HUM-004 pairs the Knight Capital incident year and the SEC order correctly and numbers the Amershi et al. guideline G9.
- Links that no longer reach the document named are replaced: FCA FG22/5 (IRQ-CON-001, -002, -003, -004, -005, -008 and -009) and PS21/5 (IRQ-CON-006); the FCA AI update and the Bank of England and PRA response of 22 April 2024 (`CANVASES_TPR_003.md`); the OWASP Machine Learning Security Top 10 (`CANVASES_TPR_005.md`); the Mobley v. Workday docket (`CANVASES_TPR_009.md`); the FCA speeches index (the regulatory register). An archived copy is added beside the Stanford Internet Observatory link (`CANVASES_DAT_001.md`, `V1_Research_Compendium/INCIDENT_REGISTER.md`); incident register row 28 gains its source URL; the Mistral AI row of the labs register links to the source that supports it.
- Quotations and figures: "AI washing" as the SEC writes it (the incident register); figures from a paper's replication on exploited production code are labelled as such (the academic register); the GSM1k score drops are stated as the paper's maxima (`CANVASES_MOD_011.md`, the academic register).
- Readings of sources: Shi et al. study irrelevant context (`CANVASES_MOD_003.md`); Anthropic ranks Incident 1 as the most serious impact it identified (`CANVASES_AGT_014.md`, `V3_Testing_Playbook/PLAYBOOK_AGT_014.md`); the Zac et al. paper has been read at the primary (`CANVASES_CON_010.md`).

### 8.2 Regulatory text and source notes

- FCA SUP 15.3.1R restated to the rule's trigger and limbs (`CANVASES_GOV_014.md`).
- DORA: Art. 9 is "Protection and prevention" (`CANVASES_TPR_004.md`); Art. 10(2) reads "trigger and initiate" (`CANVASES_RES_005.md`); Art. 28(8) requires exit strategies, and exit plans that are documented and sufficiently tested (`CANVASES_TPR_008.md`); Art. 30(2)(d) provides for access, recovery and return of data (`CANVASES_TPR_009.md`).
- PRIN 2A's outcomes named as the Handbook names them (`CANVASES_MOD_014.md`); the DISP 1.1.3R quotation labelled limb (1) (the regulatory register); PS21/3 attributed to the FCA alone (IRQ-HUM-003, IRQ-HUM-005).
- EBA/GL/2019/02 remains applicable; the EBA's final report of 18 September 2026 on guidelines that will repeal it, from a date not yet set, is noted (`CANVASES_TPR_001.md`, the regulatory register).
- PRA SS1/23: a currency note at the register row records the April 2026 version, which leaves the principles the canvases cite unchanged; IRQ-GOV-008 gives the May 2023 version's effective date as 17 May 2024 (`CANVASES_GOV_008.md`).
- Field-20 reference entries are added for the sources that field 10 relies on (IRQ-GOV-007, -009, -014 and -015); an unlocated reference to ECB supervisory statements is removed (`CANVASES_GOV_012.md`).
- The academic register's head note gains a dated note on which rows record a check at the primary record. A regulatory register row no longer names the secondary sources searched.

### 8.3 Internal consistency

- `V2_IRQ_Battery/IRQ_REGISTER.md`: IRQ-DAT-011's related IRQs include IRQ-RES-006, as the canvas states.
- `V3_Testing_Playbook/PLAYBOOK_HUM.md`: the case-set reuse saving is roughly 3 reviewer-days, as the procedures give.
- `00_Admin/ASSURANCE_MODEL.md`: the IRQ-MOD-005 profile example gives the canvas's field-16 profile, with the Detectability (3) the scale requires; "never a reason to skip" in place of the licence metaphor (also `CANVASES_CON_010.md`).
- `00_Admin/DEVELOPMENT_APPROACH.md`: the subdomain and claim counts of the development stage carry their later values; the citation sentence states the [UNVERIFIED] tag.
- `00_Admin/ASSURANCE_ARCHITECTURE.md`: the IRQ-MOD-003 example label. `00_Admin/VOLUME_TEMPLATES.md`: summary cards per subdomain; an identifier that is not an IRQ removed; five of the six envelope-drift vectors; the confidence column marked as internal. `00_Admin/IRQ_TEMPLATE.md`: a detection rate, not precision. `00_Admin/ID_SCHEME.md`: three-letter domain codes.
- `00_Admin/OPINION_TEMPLATE.md`: the High paragraph cites ★4 and the limit of the current battery; the J.3 example states that it covers 90 of the 109 IRQs.
- `V3_Testing_Playbook/PLAYBOOK_TPR.md`: TP-TPR-003, -007 and -008 in subdomains F.1, F.3 and F.3; `PLAYBOOK_TPR_002.md` states what the canvas carries.
- IRQ-MOD-007 field 6 names IRQ-HUM-002, as field 19 does; IRQ-CON-010's two cross-references name the item file.
- `README.md`: the status line refers to the limits stated in §3; the version line reads 1.3.2.

### 8.4 Rules and roles

- `00_Admin/METHODOLOGY_STANDARDS.md` §3: calling a third-party model's generally available API from the firm's non-production environment, with synthetic inputs, within the provider's published usage terms and under the firm's own contract, is ordinary use of the service and not testing of a production system. `V3_Testing_Playbook/PLAYBOOK_TPR.md` states TP-TPR-004's use of the provider's endpoint on that basis.
- `00_Admin/ENGAGEMENT_MODEL.md`: the Sponsor receives the opinion and owns the deployment decision; Phase 5's gate issues the opinion to the sponsor; three phase and gate owners are marked as firm-side roles.
- `00_Admin/TIERING_MODEL.md`: Tier 3's requirement that secondary controls are rated ★3 or above is stated as an addition to the assurance-level rule.
- `V3_Testing_Playbook/PLAYBOOK_HUM_002.md`: TP-HUM-002 gains the refusal-durability limb that IRQ-HUM-002's field 11 sets out, with no separate reviewer-day figure; its Pass and Fail rules and its evidence outputs include the limb.

### 8.5 Canvas footers and observations

- Each canvas footer (107 canvases, the two exemplars in `V2_IRQ_Battery/EXEMPLAR_CANVASES.md`, and `00_Admin/IRQ_TEMPLATE.md`) gives the release version in `README.md` in place of a canvas version and date, and the "Validated by" line is removed; `00_Admin/METHODOLOGY_STANDARDS.md` states the convention. Each canvas's change log keeps its history.
- URO-6 is opened on IRQ-DAT-009 (`V2_IRQ_Battery/REGISTER_STATS.md`; the canvas's field 18). The ★3 stands while the observation is open. Its wording states that the OWASP 2025 list names no access-control test method: LLM01:2025 asks for penetration testing of access controls without giving a method.
- `V2_IRQ_Battery/REGISTER_STATS.md`: URO-2 to URO-5 passed their signing-batch limit unresolved; each stays open to its date bound.

### 8.6 Further corrections before signing

- `V3_Testing_Playbook/PLAYBOOK_HUM.md`: TP-HUM-002, -005 and -007 in subdomains D.1, D.3 and D.4, as the register gives them; the read-only rule names the refusal-durability limb. `PLAYBOOK_HUM_002.md`: the routes attempted include a configuration change, as the canvas lists.
- `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: version alignment follows the release version. `00_Admin/ID_SCHEME.md`: subdomains are named by the domain's letter and a number. `00_Admin/VOLUME_TEMPLATES.md`: one or more IRQs per subdomain, in the second place it is stated. `00_Admin/ENGAGEMENT_MODEL.md`: the High grade cites ★4 tests. `00_Admin/OPINION_TEMPLATE.md`: the signature block names the Engagement Lead and the QA Lead, roles the engagement model defines.
- `00_Admin/IRQ_TEMPLATE.md`: the worked example gives Detectability 3 for detection within days, as the scale defines. `00_Admin/METHODOLOGY_STANDARDS.md`: the release correction log records changes made to every canvas at once.
- `V2_IRQ_Battery/canvases/CANVASES_CON_002.md`: Consumer Duty outcomes monitoring, as FG22/5 describes the outcomes. `CANVASES_MOD_011.md`: GSM1k as a short name, not a title. `V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md`: the SS1/23 note names the paragraph the canvases cite.
- `README.md`: the errata record lists the v1.3.2 corrections. The domain playbooks whose procedures changed record v1.3.2 in their change logs.
- `00_Admin/ENGAGEMENT_MODEL.md`: the Role Definitions define the firm-side owners. `CANVASES_DAT_014.md`: PRIN 2A cited by its cross-cutting obligations and price and value outcome. `CANVASES_TPR_004.md`: DORA Art. 6 for the ICT risk management framework and Art. 9(4)(e) for change management; the call to the provider's endpoint carries the limits of METHODOLOGY_STANDARDS.md §3. `CANVASES_HUM_002.md`: field 11 names the four routes. `CANVASES_MOD_003.md`: the four-test note and the research basis state what Liu et al. and Shi et al. show. `CANVASES_MOD_002.md` and `V3_Testing_Playbook/PLAYBOOK_MOD_002.md`: the call to the vendor's latest version carries the limits of METHODOLOGY_STANDARDS.md §3. `CANVASES_TPR_005.md`: the OWASP entry names were corrected on 3 October 2026. `00_Admin/OPINION_TEMPLATE.md`: the distribution line cites ★4 tests. `00_Admin/ASSURANCE_ARCHITECTURE.md`: the IRQ-MOD-003 example states no token figure. `V3_Testing_Playbook/PLAYBOOK_OVERVIEW.md`: version alignment states where the release version is given.
