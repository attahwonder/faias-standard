# FAIAS — Review Canvases: CON (Conduct & Fairness) Domain

**Domain:** CON — Conduct & Fairness (subdomains H.1–H.3)
**IRQs covered:** IRQ-CON-001 … IRQ-CON-010 (10 of 10)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md, 21 fields per canvas
**Quality bar:** EXEMPLAR_CANVASES.md
**Spelling:** UK throughout

## Domain Preamble

The Conduct & Fairness domain governs whether AI-influenced customer outcomes are fair, comprehensible and contestable, and whether the system's own decisions distort the data or dynamics that shape future outcomes. This domain sits downstream of DAT (which addresses whether training/reference data is representative in the first place) and upstream of HUM (which addresses whether customers can obtain a genuine human re-decision); TAXONOMY.md is explicit that fairness *outcomes* are homed in CON while data *representativeness* is homed in DAT, and that feedback loops are homed in CON H.3 because the FS-material harm is distorted customer outcomes even though the recontamination mechanics cross-link to MOD B.5 collapse and DAT A.1 lineage. The ten CON IRQs split across H.1 Discrimination & Proxy Bias (CON-001–002), H.2 Customer Outcomes, Vulnerability & Access (CON-003–006, CON-009, CON-010) and H.3 Feedback Loops & Transparency (CON-007–008). Evidence maturity varies sharply within the domain: subgroup/intersectional fairness-metric testing on held-out, non-production datasets is a maturing practice with several published frameworks and is rated ★3; proxy-variable analysis and price-fairness testing are credible research-grounded but bespoke, rated ★2; testing generative-output mis-statement risk and feedback-loop/performative-effect detection are genuinely immature — no agreed FS benchmark exists — and are rated ★2, reflecting bespoke, professional-judgement-dominant methodology rather than a certified test suite. The domain now carries two ★1 ratings: IRQ-CON-005 (access and exclusion), downgraded on a re-review of its research basis because no published study has audited or instrumented a live AI/ML underwriting model to establish the mechanism empirically, the constraint being that no located work with access to a deployed model has examined that mechanism, rather than analytical technique, and IRQ-CON-010 (engineered journey friction), rated ★1 on admission because no published study audits a live conversational or agentic system's per-customer, dynamically generated friction and the paired-probe method is a first-principles construction — the harm mechanism itself is named in binding rule, which is why the rating turns on method and not on plausibility. Where no established practice exists for a specific AI-driven conduct failure mode, this canvas set says so plainly ("none established") rather than inflating maturity to match the exemplar tone. No control is invented; anchors not directly confirmed in this repository's source registers are marked [UNVERIFIED] (verification pass completed 29 Jul 2026 — see VERIFICATION_LOG_B.md).

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-CON-001: CANVASES_CON_001.md
- IRQ-CON-002: CANVASES_CON_002.md
- IRQ-CON-003: CANVASES_CON_003.md
- IRQ-CON-004: CANVASES_CON_004.md
- IRQ-CON-005: CANVASES_CON_005.md
- IRQ-CON-006: CANVASES_CON_006.md
- IRQ-CON-007: CANVASES_CON_007.md
- IRQ-CON-008: CANVASES_CON_008.md
- IRQ-CON-009: CANVASES_CON_009.md
- IRQ-CON-010: CANVASES_CON_010.md

