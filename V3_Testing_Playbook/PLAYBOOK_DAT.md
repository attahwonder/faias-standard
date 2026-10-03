# FAIAS — Testing Playbook: DAT (Data) Domain

**Component:** V3 Testing Playbook
**Domain:** DAT — Data (subdomains A.1–A.5)
**Procedures:** TP-DAT-001 … TP-DAT-014 (14, 1:1 with IRQ-DAT-001 … IRQ-DAT-014)
**Source canvases:** `V2_IRQ_Battery/canvases/CANVASES_DAT.md`
**Governing documents:** `00_Admin/ASSURANCE_MODEL.md` (★ anchors, L1–L5 evidence levels), `00_Admin/METHODOLOGY_STANDARDS.md` (source hierarchy, testing-method labelling, non-production rule)
**Compiled:** 2026-07
**Spelling:** UK throughout

---

## Domain Testing Overview

### Purpose and scope of this playbook

Each procedure below expands the summary-level Independent Test in the corresponding Review Canvas into an executable sheet that a competent reviewer — a data-governance or model-validation practitioner with working ML literacy — can follow without further design work. **The ★ confidence rating is carried over unchanged from the canvas.** Where the canvas cites a recognised methodology, the procedure names it with its version or publication year; where the canvas states that no benchmark exists, the procedure says so plainly and labels the relevant measure *reviewer judgement — no established threshold*, per METHODOLOGY_STANDARDS §3. **No new citations are introduced in this playbook**; every method reference traces back to a canvas or register entry.

### Non-production rule (applies to all fourteen procedures)

Per METHODOLOGY_STANDARDS §3, every procedure in this playbook executes **only in a development, test or staging environment isolated from production systems**. No procedure permits testing of production systems, live customer data, probing of production endpoints, or exposure of real personal data. Where a procedure requires realistic data, the reviewer uses synthetic, anonymised or historical non-live extracts approved for test use. Any step that cannot be executed without testing in production is recorded as *not testable in scope* and reported as an evidence gap — it is never substituted with a production action.

### Shared test-environment setup (build once, reuse across DAT)

A single DAT test environment supports eleven of the original thirteen procedures. Establish it before the first procedure runs:

| Component | Purpose | Used by |
|---|---|---|
| **Read-only mirror of the data lineage/registry system** | Lineage reconstruction, synthetic-data tagging checks, feedback-path inventory | TP-DAT-001, 004, 013 |
| **Isolated fine-tuning sandbox** (compute + a small representative base model the firm actually uses) | Canary-extraction and poisoning-persistence testing | TP-DAT-002, 006 |
| **Staging replica of the RAG knowledge store + retriever + generation pipeline**, seedable and resettable to a known baseline | All retrieval procedures | TP-DAT-007, 008, 009, 012 |
| **Staging replica of the persisted memory / conversation store**, including derived embeddings, caches and a representative backup | Memory scoping and erasure tracing | TP-DAT-010 |
| **Replica ingestion pipeline** with all secondary paths wired (vendor feed, crowdsourced labelling, bulk upload) | Poisoning and feedback-gaming tests | TP-DAT-006, 013 |
| **Replica input-monitoring/drift-detection stack** with the firm's live baselines and alerting configured | Drift injection | TP-DAT-011 |
| **Synthetic customer-book snapshot** (statistical composition only — segment, product, vintage, geography — no identifiers) | Representativeness comparison | TP-DAT-005 |
| **Evidence store** (write-once or checksum-controlled) for retained prompts, outputs, configs and scoring sheets | All | All |

Environment reset discipline: any procedure that seeds adversarial or poisoned content (TP-DAT-006, 007, 008, 013) must run against a snapshot that is destroyed and restored afterwards. Record the snapshot ID and destruction confirmation in the evidence pack.

TP-DAT-014 adds **no new shared component**: it reuses the stratified sampling frame built for TP-DAT-001, and needs a held-out or historical non-live sample together with an independent measure of the true construct where one exists. It counts as environment-supported for the purposes of the count above: it reuses the frame already built and adds no new shared component.

### Sequencing advice

Run in four waves. Later waves depend on artefacts and access secured earlier.

**Wave 1 — documentary and structural (no model execution):** TP-DAT-001 (lineage), TP-DAT-005 (representativeness), TP-DAT-004 (synthetic-data tagging portion). These establish what data exists, which is the input to everything else, and surface access/artefact gaps early enough to escalate.

**Wave 2 — corpus and label quality:** TP-DAT-003 (label quality), TP-DAT-004 (fidelity portion), TP-DAT-002 (canary extraction). TP-DAT-002 and TP-DAT-006 both require the fine-tuning sandbox; schedule them adjacently to amortise environment cost.

**Wave 3 — pipeline integrity:** TP-DAT-006 (poisoning), TP-DAT-013 (feedback loops), TP-DAT-011 (input drift). All three exercise the ingestion/monitoring stack.

TP-DAT-014 runs in wave 2, with the corpus-and-label-quality group: TP-DAT-003 and TP-DAT-014 are the label-accuracy and label-construct halves of the same question, and the canvas is explicit that they are distinct.

**Wave 4 — retrieval and memory:** TP-DAT-007 (currency), TP-DAT-008 (conflict determinism), TP-DAT-012 (retrieval/embedding drift), TP-DAT-009 (entitlements), TP-DAT-010 (memory). Run TP-DAT-007 before TP-DAT-008 — the stale/current document pair seeded for 007 is the natural starting corpus for 008's conflicting-pair set. Run TP-DAT-009 last of the retrieval group, because an entitlement failure found earlier would otherwise require re-running the other three under changed configuration.

Cross-domain: TP-DAT-009 should be scheduled alongside the SEC-domain indirect-injection testing (IRQ-SEC-003) if both are in scope, since both seed the same staging knowledge store. TP-DAT-012 and the MOD-domain evaluation-integrity work (TP-MOD-011) share a contamination/holdout mindset and benefit from the same reviewer.

### Cross-IRQ dataset reuse opportunities

Building test data is the largest cost in this domain. Six reuse opportunities materially reduce it:

1. **Stratified dataset sample (TP-DAT-001)** — the sampling frame built for lineage reconstruction is the same frame used to select labelled sets for TP-DAT-003, synthetic-augmented sets for TP-DAT-004 and the subgroup strata for TP-DAT-014's target-label analysis. Build one stratification, use it four times.
2. **Real held-out reference sample (TP-DAT-004)** — the real-distribution reference used for synthetic fidelity comparison doubles as the "current book" comparator baseline in TP-DAT-005 and as the clean-feedback baseline in TP-DAT-013.
3. **Seeded stale/current document pair (TP-DAT-007)** — extends directly into TP-DAT-008's conflicting-pair set (add draft/final and regional-variant pairs) and provides the pre-drift corpus baseline for TP-DAT-012.
4. **Representative query set** — one FS-realistic query set (customer-facing product queries, policy lookups) serves TP-DAT-007, 008, 009 and 012. Version it once; annotate per-procedure additions (adversarial paraphrases for 009, topically-skewed additions for 012).
5. **Canary sequence library (TP-DAT-002)** — synthetic personal-data-shaped strings built for extraction testing are reusable as traceable markers in TP-DAT-010's DSAR-erasure trace, where the question is whether a known synthetic subject's data survives deletion.
6. **Synthetic multi-tenant conversational corpus (TP-DAT-010)** — reusable as the session-history substrate for the AGT-domain memory-poisoning procedure (TP-AGT-008), avoiding a second corpus build.

### Domain-level evidence maturity caveat (state in every DAT report)

Per the canvas set's own preamble, DAT test confidence is uneven and deliberately not levelled up: lineage, drift and representativeness testing sit at ★3 (credible standards-based methods, no agreed FS pass/fail benchmark); poisoning, synthetic fidelity, label quality, memory erasure, feedback-channel vetting and construct-validity testing of the modelled target variable sit at ★2 (research exists, test design is bespoke, professional judgement dominant). No DAT procedure reaches ★4 or ★5. Reports must carry the ★1–★2 judgement-based labelling required by METHODOLOGY_STANDARDS §3c wherever a ★2 procedure underpins a conclusion.

### Indicative total effort

**54 reviewer-days** across the fourteen procedures, excluding environment build (allow a further 5–10 reviewer-days for first-time environment establishment, largely reusable across subsequent engagements).

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-DAT-001: PLAYBOOK_DAT_001.md
- TP-DAT-002: PLAYBOOK_DAT_002.md
- TP-DAT-003: PLAYBOOK_DAT_003.md
- TP-DAT-004: PLAYBOOK_DAT_004.md
- TP-DAT-005: PLAYBOOK_DAT_005.md
- TP-DAT-006: PLAYBOOK_DAT_006.md
- TP-DAT-007: PLAYBOOK_DAT_007.md
- TP-DAT-008: PLAYBOOK_DAT_008.md
- TP-DAT-009: PLAYBOOK_DAT_009.md
- TP-DAT-010: PLAYBOOK_DAT_010.md
- TP-DAT-011: PLAYBOOK_DAT_011.md
- TP-DAT-012: PLAYBOOK_DAT_012.md
- TP-DAT-013: PLAYBOOK_DAT_013.md
- TP-DAT-014: PLAYBOOK_DAT_014.md

---
---

## Effort Summary — DAT Domain

| Procedure | IRQ | ★ | Reviewer-days |
|---|---|---|---|
| TP-DAT-001 | IRQ-DAT-001 Lineage | ★3 | 3 |
| TP-DAT-002 | IRQ-DAT-002 Lawful basis / extraction | ★3 | 4 |
| TP-DAT-003 | IRQ-DAT-003 Label quality | ★2 | 5 |
| TP-DAT-004 | IRQ-DAT-004 Synthetic fidelity | ★2 | 4 |
| TP-DAT-005 | IRQ-DAT-005 Representativeness | ★3 | 3 |
| TP-DAT-006 | IRQ-DAT-006 Poisoning | ★2 | 5 |
| TP-DAT-007 | IRQ-DAT-007 RAG currency | ★3 | 3 |
| TP-DAT-008 | IRQ-DAT-008 Retrieval determinism | ★3 | 3 |
| TP-DAT-009 | IRQ-DAT-009 Entitlements | ★3 | 4 |
| TP-DAT-010 | IRQ-DAT-010 Memory governance | ★2 | 4 |
| TP-DAT-011 | IRQ-DAT-011 Input drift | ★3 | 4 |
| TP-DAT-012 | IRQ-DAT-012 Retrieval/embedding drift | ★2 | 4 |
| TP-DAT-013 | IRQ-DAT-013 Feedback loops | ★2 | 4 |
| TP-DAT-014 | IRQ-DAT-014 Construct validity of target | ★2 | 4 |
| **Total** | **14 procedures** | — | **54 reviewer-days** |

Excludes first-time test-environment build (5–10 reviewer-days, largely reusable) and non-reviewer support effort (annotators, platform and ML engineers), which are costed separately.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Thirteen DAT procedures derived 1:1 from CANVASES_DAT.md; ★ ratings carried over unchanged; no new citations introduced.
v1.1 (2026-08-25) — TP-DAT-014 (construct-to-target mapping review and subgroup label analysis) added, derived 1:1 from the IRQ-DAT-014 canvas; domain totals move to fourteen procedures and 54 reviewer-days; ★ distribution becomes seven ★3 and seven ★2.
v1.3.0 (2026-10) — Domain preamble: the statement that no procedure permits production system access now reads that no procedure permits testing of production systems, in line with the non-production rule (METHODOLOGY_STANDARDS.md §3), under which read-only records retrieved through the firm's normal channels are admissible evidence. No procedure, ★ rating or reviewer-day estimate changes.
v1.3.2 (2026-10-03) — TP-DAT-009's method class names the OWASP limb as control guidance, under review as URO-6 (00_Admin/CORRECTION_LOG_2026-10-03.md §8). No ★ rating or reviewer-day figure changes.
