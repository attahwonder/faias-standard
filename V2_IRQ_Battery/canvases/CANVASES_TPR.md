# FAIAS — Review Canvases: TPR (Third Party) Domain

**Domain:** TPR — Third Party (subdomains F.1–F.3)
**IRQs covered:** IRQ-TPR-001 … IRQ-TPR-009 (9 of 9)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md, 21 fields per canvas
**Quality bar:** EXEMPLAR_CANVASES.md
**Spelling:** UK throughout

## Domain Preamble

The Third Party domain governs the firm's dependence on external foundation-model and API providers, cloud/GPU infrastructure, open-source model publishers, embedding and vector-database vendors, and software vendors who embed AI inside procured tools. Financial-services firms rarely build frontier models in-house; almost every AI capability reviewed elsewhere in this register (MOD, AGT, SEC) ultimately traces back to a third-party relationship whose diligence, contractual terms, change-control visibility and concentration profile determine whether the firm can evidence control at all. TAXONOMY.md rules that silent vendor-side model drift is homed here (F.2, not MOD) because the failure is a governance-visibility gap in the third-party relationship, not a model property in isolation, and that embedded vendor AI (CRM, HR, surveillance tools) is discovered and governed here even when the firm never directly procured "an AI system". The nine TPR IRQs split across F.1 Due Diligence, Contracts & Licensing (TPR-001–003, TPR-009), F.2 Model Change Management (TPR-004) and F.3 Dependencies, Concentration & Data Handling (TPR-005–008). Evidence maturity is mixed: contractual and due-diligence controls are established practice (EBA outsourcing guidelines, DORA, PRA SS2/21) rated ★3 where tested against a defined checklist; detecting silent vendor-side drift is genuinely immature — no published benchmark exists for "did the provider change the model under us" — and is rated ★2, reflecting that this is largely bespoke canary-testing rather than a certified methodology. No control is invented; anchors not directly confirmed in this repository's source registers are marked [UNVERIFIED] (verification pass completed 29 Jul 2026 — see VERIFICATION_LOG_B.md).

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-TPR-001: CANVASES_TPR_001.md
- IRQ-TPR-002: CANVASES_TPR_002.md
- IRQ-TPR-003: CANVASES_TPR_003.md
- IRQ-TPR-004: CANVASES_TPR_004.md
- IRQ-TPR-005: CANVASES_TPR_005.md
- IRQ-TPR-006: CANVASES_TPR_006.md
- IRQ-TPR-007: CANVASES_TPR_007.md
- IRQ-TPR-008: CANVASES_TPR_008.md
- IRQ-TPR-009: CANVASES_TPR_009.md

