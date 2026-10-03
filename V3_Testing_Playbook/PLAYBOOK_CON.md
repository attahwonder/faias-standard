# FAIAS — Component 5 Testing Playbook: CON (Conduct & Fairness)

**Domain:** CON — Conduct & Fairness
**Procedures:** TP-CON-001 … TP-CON-010 (10 of 10; 1:1 with IRQ-CON-001 … IRQ-CON-010)
**Compiled:** 2026-07
**Authority:** CANVASES_CON.md is authoritative on assurance objective, pass/fail/partial interpretation and ★ confidence. This playbook adds execution detail only; where the two appear to conflict, the canvas governs.
**Universal preconditions:** PLAYBOOK_OVERVIEW.md §3 (non-production rule, benign payloads, test-data handling) applies to every procedure below and is not repeated in each sheet.
**Spelling:** UK throughout.

---

## Domain Testing Posture

CON is the least externally standardised domain in this playbook and the playbook says so at the outset: seven of ten procedures carry ★2, one carries ★3 and two carry ★1. TP-CON-009's ★2 is **pending formal adoption of a candidate benchmark methodology**, which is the canvas's own qualifier and part of the rating rather than a footnote to it. There is a substantial and growing research literature on fairness measurement, and there is mature UK conduct regulation — Consumer Duty, FG21/1 on vulnerable customers, the general insurance pricing intervention — but there is no regulator-mandated fairness test suite, no agreed FS fairness benchmark, and no canonical threshold above which a subgroup disparity becomes a finding. Every CON procedure therefore requires the reviewer to *choose* metrics, *set* thresholds and *justify* both, and every CON report must disclose that those choices were made by the reviewer.

This has three practical consequences for test design:

1. **Metric choice must precede the test and be recorded.** Fairness metrics are mathematically incompatible in the general case: a system that satisfies demographic parity will typically violate equalised odds, and vice versa. Selecting the metric after seeing the results is the single most serious methodological failure available in this domain. The reviewer records the chosen metrics, and the reason, before any computation.
2. **Test data is the binding constraint.** Every CON procedure **except TP-CON-009 and TP-CON-010** needs protected-characteristic labels that the production model does not and must not use. Obtaining a labelled non-production dataset that is genuinely representative — and handling it lawfully — is usually the longest step in the procedure, and where representativeness cannot be evidenced the entire result must be labelled as synthetic-proxy-based. **TP-CON-009 needs none:** its prompt set is drawn from the ordinary-use task distribution and scored against a harm taxonomy, with no protected-characteristic dimension. **TP-CON-010's core limbs likewise need none:** its paired profiles differ on tenure, product value, retention-propensity band or channel. Where the reviewer additionally probes whether generated friction correlates with a protected characteristic, the domain's special-category precondition engages for that limb alone. (The statement was already qualified in substance elsewhere in this playbook — TP-CON-005's segments of interest are frequently not protected characteristics, and TP-CON-008's participant panel runs on its own separate lawful basis.)
3. **Disparity found is not discrimination proven.** These procedures measure outcome distributions and feature correlations. They do not establish unlawfulness. Reporting language must present findings as disparities requiring justification, remediation or formal acceptance — the framing the canvases use — rather than as legal conclusions.

**Data-protection note applying to all CON procedures that process protected-characteristic labels.** Protected-characteristic labels are special category data under UK GDPR. Before any such CON procedure begins, the reviewer must confirm with the firm's data protection officer that a lawful basis and a DPIA exist for processing those labels for equality-monitoring/testing purposes, that the labelled dataset is held separately from production model inputs, and that the labels are deleted or returned at engagement close. Where no such basis can be established, the procedures run on synthetic proxy data only and every conclusion is qualified accordingly.

**TP-CON-009 processes no special-category data, so this precondition does not engage for it.** Its own data handling is the de-identification of an ordinary-use prompt set derived from the real task distribution, with the derivation basis recorded.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-CON-001: PLAYBOOK_CON_001.md
- TP-CON-002: PLAYBOOK_CON_002.md
- TP-CON-003: PLAYBOOK_CON_003.md
- TP-CON-004: PLAYBOOK_CON_004.md
- TP-CON-005: PLAYBOOK_CON_005.md
- TP-CON-006: PLAYBOOK_CON_006.md
- TP-CON-007: PLAYBOOK_CON_007.md
- TP-CON-008: PLAYBOOK_CON_008.md
- TP-CON-009: PLAYBOOK_CON_009.md
- TP-CON-010: PLAYBOOK_CON_010.md

---
---

## Domain Summary — CON

| Procedure | IRQ | ★ | Reviewer-days | Test data requirement |
|---|---|---|---|---|
| TP-CON-001 Subgroup & intersectional disparity | IRQ-CON-001 | ★3 | 6 | Labelled held-out dataset |
| TP-CON-002 Proxy feature probing | IRQ-CON-002 | ★2 | 5 | Labelled dataset + full feature dictionary |
| TP-CON-003 Vulnerable-customer scenario set | IRQ-CON-003 | ★2 | 5 | Labelled transcript corpus |
| TP-CON-004 Content accuracy probe | IRQ-CON-004 | ★2 | 4 | Query set + versioned ground truth |
| TP-CON-005 Matched-cohort exclusion testing | IRQ-CON-005 | **★1** | 5 | Deep dataset for matching |
| TP-CON-006 Price decomposition | IRQ-CON-006 | ★2 | 5 | Pricing model internals |
| TP-CON-007 Feedback-loop simulation | IRQ-CON-007 | ★2 | 6 | Multi-cycle historical data |
| TP-CON-008 Disclosure comprehension | IRQ-CON-008 | ★2 | 4 | Participant panel |
| TP-CON-009 Ordinary-use harmful-output testing | IRQ-CON-009 | ★2 (pending adoption) | 4 | Ordinary-use prompt set from the real task distribution, scored against a harm taxonomy |
| TP-CON-010 Engineered journey friction | IRQ-CON-010 | **★1** | 5 | Test/staging journey instance + layer configuration + synthetic matched profiles |
| **Domain total** | **10 IRQs** | **1×★3, 7×★2, 2×★1** | **49** | — |

**Tier applicability:** CON procedures are out of scope at Tier 0. At Tier 1 they run only where the system has customer proximity — typically TP-CON-003 and TP-CON-004. TP-CON-009 runs at Tier 1 wherever **any** of its covered channels is deployed — customer-facing chat, collections correspondence **or staff-facing copilot tools** — a channel-presence rule rather than the customer-proximity rule above, because the third channel is not customer-proximate and a straight customer-proximity rule would under-scope it. TP-CON-010 runs at Tier 1 wherever an AI layer mediates a customer journey that includes any PRIN 2A.6.2R(4) lifecycle action — making a general enquiry, amending or switching, transferring provider, accessing a benefit, submitting a claim, making a complaint, or cancelling, the rule's list being illustrative rather than exhaustive — a journey-scope rule rather than the customer-proximity rule, because an AI layer sitting only on the complaints intake path is in scope while not being the firm's customer-facing front door. All ten run at Tier 2 and Tier 3. The vulnerable-customer override trigger in TIERING_MODEL.md means that any system processing vulnerable-customer requests attracts a tier upgrade and therefore the full CON set. See PLAYBOOK_OVERVIEW.md §5.

**Disclosure requirement:** Seven of ten CON procedures carry ★2 and two (TP-CON-005 and TP-CON-010) carry ★1. Any opinion relying on the CON domain must state that fairness metric selection, threshold-setting and materiality judgements were made by the reviewer in the absence of an agreed FS benchmark, per ASSURANCE_MODEL.md §6; the two ★1 procedures carry the stronger caveat that the methodology is novel and unvalidated and that result quality depends entirely on assessor expertise. **For TP-CON-010 that caveat has a specific content that must not be softened into generic immaturity:** the harm mechanism is named in a binding rule, and it is the *method* that is absent — no published study audits a live conversational or agentic system's per-customer, dynamically generated friction, and the materiality threshold for an asymmetry is reviewer-set because PRIN 2A.6.3G(2) places the appropriate-friction / unreasonable-barrier boundary in the assessor's judgement. In the opinion itself that caveat is written in PLAYBOOK_OVERVIEW.md §8's prescribed ★1 form of words with the clause 'and is named in binding rule (PRIN 2A.6)' added, per canvas field 14; §8's form of words is not amended to carry the clause. **Any opinion relying on TP-CON-009 must additionally state its pending-adoption qualifier** — that the candidate methodology is not FS-certified and has not been formally adopted into FAIAS methodology — because that qualifier is part of the rating, not a technicality attached to it. Where a procedure ran on synthetic proxy data rather than a representative held-out set, that substitution must appear in the opinion, not only in the working papers.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Eight CON procedures derived 1:1 from CANVASES_CON.md; ★ ratings carried over unchanged; no new citations introduced.
v1.1 (2026-08-25) — TP-CON-009 (ordinary-use harmful-output testing) added, derived 1:1 from the IRQ-CON-009 canvas; evaluation-harm-evidence caveats applied to TP-CON-005 and the preamble; domain totals move to nine procedures and 44 reviewer-days (one ★3, seven ★2, one ★1); tolerance ownership and TP-CON-009's Tier 1 rule assigned at signing.
v1.2 (2026-09-12) — TP-CON-010 (engineered journey friction in AI-mediated customer journeys) added, derived 1:1 from the IRQ-CON-010 canvas; posture, test-data, tier and disclosure paragraphs updated for a second ★1; domain totals move to ten procedures and 49 reviewer-days (one ★3, seven ★2, two ★1). Erratum: TP-CON-010's Tier-1 scope rule enumerated six of the seven PRIN 2A.6.2R(4) lifecycle actions; (a) general enquiries added, matching CANVASES_CON.md's own enumeration. No scope change: the rule's list is illustrative and the qualifier already stood.
v1.2.1 (2026-09-19) — Erratum to TP-CON-005's ★ confidence statement, carried from CANVASES_CON.md, which is authoritative on ★ confidence: the statement that no outside party has had algorithm access is corrected: the FCA, in the work the canvas cites, lacked full access to the algorithms and EIOPA's questionnaire-based review did not examine them, and the published work located that did obtain access to deployed credit models — among it a US supervisor's examinations of credit card lenders' credit scoring models, including models built with AI or ML, and one fair-lending monitorship of a machine-learning consumer-lending model — measured disparity by protected characteristic, not exclusion by data sparsity, by different methods. ★1, method classification, preconditions, test design, tier applicability, reviewer-days and the disclosure requirement are unchanged. TP-CON-001 — the perception-component limb added to IRQ-CON-001's Independent Test reflected in the §1 objective statement and carried into the preconditions, the test design, a new step 13, the measures table, the Pass and Fail interpretation and the evidence outputs: where identity verification, liveness checking, voice authentication or speech transcription sits upstream of a customer outcome, that component's error rates are computed for each subgroup, the measure stated per component type and the deployed-threshold rule confined to components that apply a decision threshold; where no subgroup-labelled evaluation set in the component's modality is available, the component is recorded as untestable, a coverage gap and not a pass; the step-13 evaluation set's source, subgroup composition and representativeness recorded, conclusions from a set not confirmed as representative marked proxy-based, and the personnel line extended to step 13. The time estimate is stated as excluding step 13, whose manual-equivalent effort, where it applies, is estimated at scoping, disclosed and added to the six days as the procedure's upper bound for that engagement. ★3, method classification, tier applicability and the six-day base estimate are unchanged; no new citations introduced beyond those the canvas carries.
