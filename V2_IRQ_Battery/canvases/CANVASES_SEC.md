# FAIAS — Review Canvases: SEC (Security) Domain

Fourteen Independent Review Questions covering IRQ-SEC-001 to IRQ-SEC-014, subdomains E.1 Prompt Injection & Jailbreak, E.2 Extraction & Leakage, E.3 Supply Chain & Tool Security, E.4 Identity & Credentials, E.5 Misuse & Dual-Use, E.6 Control Efficacy Under Adversarial Evolution, E.7 Improper Output Handling. Scope per TAXONOMY.md: adversarial exploitation of the AI system at build or inference time, for the uses listed in README.md §1 — under FAIAS the reviewer never tests production systems (the non-production rule, METHODOLOGY_STANDARDS.md §3). UK spelling throughout. Security is the most evidentially mature FAIAS domain: direct injection/jailbreak and extraction testing generally rate ★3–★4 against published methodology (OWASP, MITRE ATLAS, NIST AI 100-2); MCP/tool-server compromise, non-human identity, misuse/dual-use (E.5, applicability-conditional, ★1), AI-as-control efficacy against adversarial evolution (E.6, ★2) and improper output handling (E.7, ★2) are newer disciplines and are rated honestly, per ASSURANCE_MODEL.md section 6 anchors. All controls trace to a cited regulation, standard or peer-reviewed source; where no precedent exists, the control is explicitly marked "Emerging Practice."

Boundary note (TAXONOMY.md rulings #1, #5, #12): agent workflow/tool-permission design (blast-radius limitation) is homed in AGT C.2; data-supply-chain poisoning entering via ingestion/curation is homed in DAT A.2/A.3. SEC IRQs below interrogate the adversarial-exploitation surface only and cross-link to AGT/DAT where the boundary is shared.

**A note on OWASP entry numbers (added 12 September 2026).** Every citation of the OWASP Top 10 for LLM Applications in this file is pinned to the **2025 edition** and carries the `:2025` suffix. The 2026 edition (published approximately 4 August 2026) renumbers eight of the ten entries while leaving the substance of each entry cited here intact. A reader holding the 2026 edition should read across as follows: LLM01:2025 Prompt Injection → LLM01:2026 · LLM02:2025 Sensitive Information Disclosure → LLM02:2026 · LLM03:2025 Supply Chain → LLM04:2026 · LLM05:2025 Improper Output Handling → LLM10:2026 · LLM07:2025 System Prompt Leakage → **LLM08:2026 Hidden Context Exposure** (the one entry renamed as well as renumbered) · LLM08:2025 Vector and Embedding Weaknesses → LLM09:2026. The citations here are not restated on the 2026 numbering: a rating and its sources are anchored to the edition they were written against (ASSURANCE_MODEL.md §6A.1).

---
---

## IRQ-SEC-003 — POINTER

**IRQ-SEC-003: Indirect Prompt Injection via Retrieved Content Overriding Application Intent** has a gold-standard, fully populated Review Canvas already published in `EXEMPLAR_CANVASES.md` (Canvas 1). It is not redrafted here to avoid divergent duplicate versions. Subdomain E.1; Assurance Objective AO-SEC-003; ★4 independent test confidence. See `V2_IRQ_Battery/EXEMPLAR_CANVASES.md` for the full canvas.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-SEC-001: CANVASES_SEC_001.md
- IRQ-SEC-002: CANVASES_SEC_002.md
- IRQ-SEC-004: CANVASES_SEC_004.md
- IRQ-SEC-005: CANVASES_SEC_005.md
- IRQ-SEC-006: CANVASES_SEC_006.md
- IRQ-SEC-007: CANVASES_SEC_007.md
- IRQ-SEC-008: CANVASES_SEC_008.md
- IRQ-SEC-009: CANVASES_SEC_009.md
- IRQ-SEC-010: CANVASES_SEC_010.md
- IRQ-SEC-011: CANVASES_SEC_011.md
- IRQ-SEC-012: CANVASES_SEC_012.md
- IRQ-SEC-013: CANVASES_SEC_013.md
- IRQ-SEC-014: CANVASES_SEC_014.md

