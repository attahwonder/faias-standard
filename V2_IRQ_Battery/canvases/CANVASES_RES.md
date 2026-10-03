# FAIAS — Review Canvases: RES (Operational Resilience) Domain

**Domain:** RES — Operational Resilience (subdomains G.1–G.4)
**IRQs covered:** IRQ-RES-001 … IRQ-RES-007 (7 of 7)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md, 21 fields per canvas
**Quality bar:** EXEMPLAR_CANVASES.md
**Spelling:** UK throughout

## Domain Preamble

The Operational Resilience domain governs the firm's ability to keep important business services (IBS) running within impact tolerance when an AI component fails, degrades, or must be deliberately stopped — and to detect that degradation, including gradual decay, before it breaches tolerance. This domain sits downstream of TPR (which addresses whether third-party AI dependencies are themselves properly managed) and upstream of GOV (which addresses whether monitoring signals reach accountable bodies); TAXONOMY.md is explicit that RES G.3 owns detection *capability* while GOV I.3 owns whether detected signals are *consumed* by governance. The seven RES IRQs split across G.1 Fallback & Degradation (RES-001–002), G.2 Containment & Recovery (RES-003–004), G.3 Monitoring & Alerting (RES-005–006) and G.4 Resilience Mapping (RES-007). This is one of the more mature domains from an established-practice standpoint: UK operational resilience regulation (FCA SYSC 15A, PS21/3; PRA SS1/21) already mandates IBS mapping, impact tolerances and severe-but-plausible scenario testing, and much of this canvas set extends that existing, tested discipline to AI-specific failure modes rather than inventing a new regime. Ratings reflect that: fallback and threshold-monitoring testing against defined scenarios are rated ★3 (established op-res and statistical-process-control practice, extended to a newer failure class); safe-degradation, containment/rollback and slow-decay detection-design testing are rated ★2, reflecting real but bespoke, less standardised methodology; where no established AI-specific kill-switch or rollback rehearsal practice exists in a firm, this canvas set says so plainly ("none established") rather than inflating maturity to match the exemplar tone. No control is invented; anchors not directly confirmed in this repository's source registers are marked [UNVERIFIED] (verification pass completed 29 Jul 2026 — see VERIFICATION_LOG_B.md).

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-RES-001: CANVASES_RES_001.md
- IRQ-RES-002: CANVASES_RES_002.md
- IRQ-RES-003: CANVASES_RES_003.md
- IRQ-RES-004: CANVASES_RES_004.md
- IRQ-RES-005: CANVASES_RES_005.md
- IRQ-RES-006: CANVASES_RES_006.md
- IRQ-RES-007: CANVASES_RES_007.md

