# FAIAS — Review Canvases: DAT (Data) Domain

**Domain:** DAT — Data (subdomains A.1–A.5)
**IRQs covered:** IRQ-DAT-001 … IRQ-DAT-014 (14 of 14)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md, 21 fields per canvas
**Quality bar:** EXEMPLAR_CANVASES.md
**Spelling:** UK throughout

## Domain Preamble

The Data domain governs the integrity, provenance, representativeness, privacy and lifecycle of every dataset feeding a financial-services AI system — training corpora, fine-tuning sets, RAG knowledge stores, persisted memory, and the statistical distributions those systems observe in production. Failure here is upstream of almost every other domain: a poisoned training record, a stale RAG document or an undetected drift event surfaces later as a hallucination (MOD), an unfair outcome (CON) or an exploited security gap (SEC), which is why TAXONOMY.md homes RAG poisoning, memory and drift by originating vector rather than by consequence. The fourteen DAT IRQs split across A.1 Training Data Provenance (DAT-001–005, DAT-014), A.2 Data Poisoning (DAT-006, DAT-013), A.3 Retrieval Data (DAT-007–009), A.4 Memory (DAT-010) and A.5 Data Drift (DAT-011–012). Evidence maturity is markedly uneven: lineage reconstruction, licence auditing and drift statistics are established engineering disciplines with ★3 testable methodology; poisoning-resistance evaluation, synthetic-data fidelity validation and RAG-corpus integrity checks are ★2–★3 — credible research exists but firm-specific test design dominates; memory-scoping and feedback-channel vetting are the least mature, rated ★2, and this canvas set says so plainly rather than inflating confidence to match the exemplar tone. No control is invented: every Expected Controls entry traces to a cited regulation, standard or peer-reviewed source, or is explicitly labelled Emerging Practice.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

IRQ-DAT-013 was held in this file between IRQ-DAT-006 and IRQ-DAT-007. Its file is named by its identifier, so it now follows IRQ-DAT-012.

The canvases, in order:

- IRQ-DAT-001: CANVASES_DAT_001.md
- IRQ-DAT-002: CANVASES_DAT_002.md
- IRQ-DAT-003: CANVASES_DAT_003.md
- IRQ-DAT-004: CANVASES_DAT_004.md
- IRQ-DAT-005: CANVASES_DAT_005.md
- IRQ-DAT-006: CANVASES_DAT_006.md
- IRQ-DAT-007: CANVASES_DAT_007.md
- IRQ-DAT-008: CANVASES_DAT_008.md
- IRQ-DAT-009: CANVASES_DAT_009.md
- IRQ-DAT-010: CANVASES_DAT_010.md
- IRQ-DAT-011: CANVASES_DAT_011.md
- IRQ-DAT-012: CANVASES_DAT_012.md
- IRQ-DAT-013: CANVASES_DAT_013.md
- IRQ-DAT-014: CANVASES_DAT_014.md

---
---
