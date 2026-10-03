# QA LOG — Batch 2: CANVASES_SEC.md (10 canvases + SEC-003 pointer) & CANVASES_DAT.md (13 canvases)

**A note on file names (added 3 October 2026).** The file names in this record refer to the layout before FAIAS v1.3.1, in which each domain's Review Canvases, and each domain's test procedures, were held in one file. From v1.3.1 each canvas and each procedure is held in its own file. 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier files to its new file and line, so the file and line references below still resolve.

**QA reviewer:** FAIAS QA
**Date:** 2026-07
**References applied:** REVIEW_QUESTION_TEMPLATE.md; ASSURANCE_MODEL.md (§5 L1–L5, §6 ★ anchors, §7 five axes); METHODOLOGY_STANDARDS.md §§3a–3d; EXEMPLAR_CANVASES.md; IRQ_REGISTER.md; IRQ_CLAIM_MATRIX.md; TAXONOMY.md (rulings 1, 2, 5, 12); V1 source registers (academic, labs, incidents); V5 regulatory register.

---

## 1. Checks performed and results

| Check | Method | Result |
|---|---|---|
| IRQ wording verbatim vs register | Scripted diff of every "Register question" line (both file formats) | **Pass — 23/23 exact matches** |
| Subdomain assignment | Footer Subdomain lines vs TAXONOMY.md | **Pass** (SEC E.1×4, E.2×3, E.3×2, E.4×1; DAT A.1×5, A.2×2 incl. DAT-013, A.3×3, A.4×1, A.5×2) |
| 21 fields present | Scripted heading count per canvas | **SEC pass (21/21 × 10). DAT FAIL — fixed:** all 13 DAT canvases were missing the `## 1. IRQ ID & Title` field (20/21), see §2.1 |
| Failure-mode anchoring | All 23 field-4 statements extracted and reviewed | **Pass** — every canvas anchors on an unsafe boundary crossing; failure chains run technical cause → business/regulatory impact with breakpoints |
| ★ honesty per anchors | All 23 ratings + justifications reviewed | **Pass — no downgrades required.** SEC-001 ★4 is anchor-consistent (published, multi-institution jailbreak testing methodology); SEC ★3s (002, 005, 006, 007) and DAT ★3s (001, 002, 005, 007, 008, 009, 011) all cite multi-group published methods with no benchmark; ★2s honestly justified. Two preamble ★-claims corrected (§2.4) |
| ★4 phrases in DAT justification prose | All eight ★4/★5 string occurrences inspected in context | **No ambiguity requiring rewrite** — every DAT occurrence is comparative ("keeping this short of ★4" / "★2, not ★3+"), unmistakably not the canvas's own rating. SEC-005/-006 similarly compare to SEC-001/-003 ratings. Left as drafted |
| L1–L5 tagging + reporting flags | Field 10/14 extracts | **Pass with 1 fix:** L1 items flagged throughout; every Pass paragraph carries the ★-level disclosure except DAT-001 — caveat added (§2.2) |
| Controls traced | Field 9 extracts | **Pass** — every control cites regulation/standard/published research or links a homed IRQ; honest gap statements where literature is absent (SEC-008, SEC-011, DAT-003, DAT-010, DAT-013) rather than invented citations — exemplary practice |
| Citation spot-check vs registers | All arXiv IDs, lab/incident/regulatory citations cross-checked | **Pass with 1 flag:** all traced (PoisonedRAG, Carlini 2021/22/23, Nasr, Shokri, BadNets, Wan, Crescendo, PAIR, Many-shot, Constitutional Classifiers, WildJailbreak, AgentHarm, GTG-1002, Shumailov/Gerstgrasser/Alemohammad/Dohmatob, WILDS, D'Amour, Gama, Rabanser, Barnett, RAGAS, RGB, Magesh, Chen 2023, SIO/LAION, OLMo/Dolma, DSIT Code, OWASP, ATLAS) **except** the OWASP "Securing Agentic Applications Guide" (SEC-010) — not in any register; flagged [TO VERIFY], not removed (§2.3). ISO/IEC TS 4213 (DAT-003) accepted as Tier-1 standards common knowledge. **No fabrications found; nothing removed** |
| 5-axis weighting | Scripted table check | **Pass** — 5 axes × 1–4 with one-line justifications in all 23; no composite scores |
| Boundary discipline (batch-2 focus) | SEC-004 and SEC-005 controls/related-IRQ review vs TAXONOMY rulings 1/5/12; DAT-006 mirror check | **Pass** — SEC-004 interrogates the adversarial untrusted-content-to-action surface only and defers blast-radius/tool-scoping/gating to linked AGT-003/-004/-005/-012; SEC-005 is explicitly the write-path/access-control variant cross-linked to SEC-003 (model-side) and DAT-006/DAT-007 (lifecycle-side); DAT-006 reciprocally cross-links SEC-005 as "the adversarial-injection variant, SEC-homed". The SEC file carries an explicit boundary note in its header. No scope absorption |
| SEC test safety | Grep for exploit strings, credentials, keys; review of all 10 Independent Tests | **Pass** — tests are procedural descriptions only; SEC-010 explicitly states "benign, procedurally described payloads only"; no working payloads or plaintext secrets anywhere |
| Non-production testing | All 23 tests reviewed | **Pass** — all isolated staging/replica environments, no production data or systems |
| UK spelling / board tone | Scripted US-spelling scan; reporting-language review | **Pass** — no US spellings; op-res, board-ready tone throughout |
| Pointer consistency | SEC-003 pointer vs MOD-006 pointer | SEC's dedicated "— POINTER" section is the better pattern; **MOD-006 pointer harmonised to match** (§2.5) |
| Cross-file consistency | AO ID format; every referenced IRQ ID validated against register | **Pass** — 0 invalid IRQ references; AO format uniform; DAT header/canvas-heading format normalised to the batch standard (§2.1) |

---

## 2. Material changes made

### 2.1 CANVASES_DAT.md — missing field 1 in all 13 canvases (template breach) + header format
- **Defect:** Every DAT canvas opened with `# IRQ-DAT-NNN: Title` as the page heading and had no `## 1. IRQ ID & Title` field — 20 of the mandatory 21 fields — and diverged from the `# CANVAS: IRQ-…` heading convention used by AGT/MOD/SEC.
- **Fix:** Scripted restructure of all 13 canvases to `# CANVAS: IRQ-DAT-NNN` + `## 1. IRQ ID & Title` + bold `**IRQ-DAT-NNN: Title**` (titles preserved verbatim; all remain failure-mode-anchored). Field counts now 21/21 × 13, verified by re-count.

### 2.2 IRQ-DAT-001 — missing ★ disclosure in Pass reporting language
- **Defect:** The only canvas in the batch whose Pass reporting paragraph omitted the ★-level disclosure required by METHODOLOGY_STANDARDS §3c practice (its test is ★3).
- **Fix:** Appended "Conclusions rest on ★3 methodology — a credible standards-based method with no agreed pass/fail benchmark — and should be read as professional assessment."

### 2.3 IRQ-SEC-010 — citation not traceable to source registers
- **Defect:** [OWASP GenAI Security Project, "Securing Agentic Applications Guide", v1.0/1.1, Jul 2025] cited in fields 9, 11, 18 and 20 but absent from V1/V5 registers. Plausibly genuine (OWASP GenAI Security Project publication), so not treated as fabrication.
- **Fix:** Reference-list entry annotated [TO VERIFY — not itemised in the V1/V5 source registers; confirm title, version and date before external issue]. Citation retained.

### 2.4 Preamble accuracy corrections (★ claims and arithmetic)
- **CANVASES_DAT.md Domain Preamble:** "Fourteen of the thirteen DAT IRQs" corrected to "The thirteen DAT IRQs"; "★3–★4 testable methodology" corrected to "★3" (no DAT test is rated ★4); "often ★1–★2" for memory/feedback corrected to "rated ★2" (no DAT test is ★1).
- **CANVASES_SEC.md header:** removed an inappropriate in-text reference to QA_LOG_BATCH1 (internal QA artefact cited inside a board-facing standard document); replaced with a citation of ASSURANCE_MODEL.md §6.

### 2.5 CANVASES_MOD.md — pointer style harmonised (cross-batch consistency)
- **Defect:** MOD-006 pointer was a header paragraph; SEC-003 pointer is a dedicated `## IRQ-SEC-00N — POINTER` section stating subdomain, AO ID and ★ rating.
- **Fix:** MOD-006 pointer converted to the matching `## IRQ-MOD-006 — POINTER` section (subdomain B.3; AO-MOD-006; ★3).

---

## 3. Items reviewed and deliberately NOT changed

- **SEC-001 ★4:** anchor-honest — direct jailbreak testing has published, partially standardised methodology adopted across ≥2 institutions (OWASP LLM01, HarmBench/PAIR-class automation, ATLAS); consistent with the exemplar's ★4 for SEC-003.
- **Comparative ★4 mentions in ★3 justifications (SEC-005/-006; DAT-005/-007/-008/-010-area/-011):** clearly comparative phrasing ("short of ★4"); no reader could mistake them for the canvas rating. No tidy-up needed beyond review.
- **Honest evidence-gap statements** in SEC-008, SEC-011, DAT-003, DAT-010, DAT-013 (explicitly declining to paper gaps with unrelated citations): retained as model practice.
- **DAT canvas ordering (…006, 013, 007…):** follows the IRQ_REGISTER row order and A.2 subdomain grouping; acceptable.

---

## 4. Residual [TO VERIFY] items

- **CANVASES_SEC.md: 8** — 7 pre-existing (regulatory section pinpoints and equivalent honesty flags) + 1 added in this QA batch (SEC-010 Securing Agentic Applications Guide reference).
- **CANVASES_DAT.md: 18** — all pre-existing and appropriate: regulatory section pinpoints (UK GDPR/DPA, EU AI Act, SS1/23 paragraph references) and honest research-gap flags (DAT-003 FS labelling-practice literature; DAT-010 memory-erasure literature; DAT-013 FS feedback-channel-gaming literature).

None indicates fabrication; all are disclosure flags to clear before external issue.

---

## 5. Defect count by category

| Category | Fixed |
|---|---|
| Template/field completeness (structural) | 1 systemic (13 canvases: missing field 1 + heading format, scripted fix) |
| Reporting-language ★ disclosure | 1 (DAT-001) |
| Citation traceability | 1 flagged [TO VERIFY] (SEC-010); 0 removed |
| Preamble accuracy (★ claims, arithmetic, internal-artefact citation) | 3 (DAT preamble ×1 multi-part, SEC header ×1, plus MOD pointer harmonisation ×1) |
| ★ downgrades | 0 (all 23 ratings anchor-honest) |
| Fabrications removed | 0 |
| Wording/subdomain/anchoring/controls/weighting/boundary/spelling/tone/safety defects | 0 |

## 6. Verdict

**The batch meets the exemplar bar after the structural fix.** Substantively — failure-mode anchoring, ★ honesty, evidence tagging, control tracing, boundary discipline (notably the SEC-004/AGT and SEC-005/DAT-006 splits), test safety and tone — both files are at or above the exemplar standard; the DAT file's honest evidence-gap statements exceed it. The one significant defect was mechanical (DAT's systematic omission of field 1), now remediated and verified 21/21 across all 13 canvases.
