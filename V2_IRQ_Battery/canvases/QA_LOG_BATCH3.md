# QA LOG — Batch 3 (final): CANVASES_HUM.md (8), CANVASES_GOV.md (12), CANVASES_TPR.md (8), CANVASES_RES.md (7), CANVASES_CON.md (8) — 43 canvases

**A note on file names (added 3 October 2026).** The file names in this record refer to the layout before FAIAS v1.3.1, in which each domain's Review Canvases, and each domain's test procedures, were held in one file. From v1.3.1 each canvas and each procedure is held in its own file. 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier files to its new file and line, so the file and line references below still resolve.

**QA reviewer:** FAIAS QA
**Date:** 2026-07
**References applied:** REVIEW_QUESTION_TEMPLATE.md; ASSURANCE_MODEL.md §§5–7; METHODOLOGY_STANDARDS.md §§3a–3d; EXEMPLAR_CANVASES.md; IRQ_REGISTER.md; IRQ_CLAIM_MATRIX.md; TAXONOMY.md (rulings 3, 6, 8, 9, 14); ASSURANCE_ARCHITECTURE.md (Layer 4); V1 source registers; V5 regulatory register.

---

## 1. Checks performed and results

| Check | Method | Result |
|---|---|---|
| IRQ wording verbatim | Scripted diff, all 43 canvases | **Pass — 43/43 exact matches** |
| 21 fields incl. `## 1. IRQ ID & Title` | Scripted count | **Pass — 21/21 in all 43 canvases**, including all "pre-existing"-provenance files |
| Subdomains | Footer lines vs TAXONOMY | **Pass** (D.1–D.4, I.1–I.4, F.1–F.3, G.1–G.4, H.1–H.3 all correctly homed) |
| Failure-mode anchoring | All 43 field-4 statements reviewed | **Pass** — all anchor on unsafe boundary crossings (for governance-type IRQs, correctly framed as the unsafe absent-control state per the register's own framing); failure chains run cause → business/regulatory impact |
| ★ honesty (single value per test) | All 43 field-11 ratings + justifications | **Pass — every Independent Test carries a single ★ value (no blended field-11 ratings found; the reported "blends" were preamble prose — see §2.2). No downgrades required:** GOV/TPR/RES/HUM/CON ★3s all rest on established audit/op-res/human-factors/fairness methodology; ★2s honestly justified; GOV-012 explicitly self-rates ★2 because its six-vector taxonomy is FAIAS-native — model honesty |
| L1–L5 tagging + reporting flags | Fields 10/14 | **Pass** — L1 items flagged; **43/43 Pass reporting paragraphs carry the ★-level disclosure** |
| Controls traced | Field 9 across all 43 | **Pass** — regulation/standard/research or linked-IRQ tracing throughout; emerging-practice areas labelled |
| Citation traceability | All research/regulatory citations vs V1/V5 registers | **1 fabrication found and removed (CON-004, §2.1).** All others traced (DP5/22, MAS ID 18/24 + AIRG, ISO/IEC 42001, NIST AI RMF, EU AI Act, DORA, BoE FPC Apr 2025, Parasuraman & Riley, Skitka, Cummings, Arthur et al., Reason, Vaughan, Amershi, Doshi-Velez & Kim, Vaccaro CSCW, Kleinberg, Prince & Schwarcz, Perdomo, Chan FAccT 2024, Mitchell Model Cards, Gebru Datasheets, ARP 4761/IEC 61508/ISO 15026-2 via ASSURANCE_ARCHITECTURE.md) or are canonical common knowledge. TPR/RES/CON honestly flag [TO VERIFY] where no register source exists rather than inventing citations |
| 5-axis weighting | Scripted table check | **Pass** — all 43 tables complete, 1–4, justified, no composites |
| Boundary discipline | Targeted greps + related-IRQ review | **Pass** — HUM-005 covers suspension *authority/willingness* only, kill-switch *mechanism* deferred to RES-003 (ruling 8); HUM-006/-008 vs GOV-010 records split respected (ruling 3); CON canvases cite DAT-005 representativeness strictly as an upstream cross-link, never absorbing its testing scope; GOV header carries an explicit boundary note for rulings on monitoring, validation and accountability |
| GOV-012 flagship | Full-canvas review | **Pass — exceeds the bar.** Explicitly anchored to ASSURANCE_ARCHITECTURE.md Layer 4 (Operating Envelope Declaration; six named drift vectors), cross-references TAXONOMY ruling 14 by name in Related IRQs (vs MOD-001 capability envelope and AGT-010 per-run divergence), ties to EU AI Act Art. 9 and SS1/23, and honestly self-rates ★2 |
| Non-production tests | All 43 reviewed | **Pass** — staging/replica/log-and-document review only; GOV-012's reconciliation component uses historical logs/records (documentation review, permitted) with its boundary-exercise in staging |
| UK spelling / tone | Scripted scan + reading | **Pass** — no US spellings; board-ready op-res tone |
| Cross-battery checks | Scripted, all 9 files + exemplars | **Pass:** 93 unique AO IDs, **zero duplicates**; every Related-IRQ reference in every file validates against the register (0 invalid battery-wide); MOD-006 and SEC-003 POINTER entries intact and format-consistent |

---

## 2. Material changes made

### 2.1 IRQ-CON-004 — fabricated citation removed (the batch's one serious defect)
- **Defect:** Field 18, reference [4] and the Four-Test footer cited "[Ray, S. et al., 2023, 'Hallucination in Neural Text Generation', NeurIPS — cited in EXEMPLAR_CANVASES.md context]". This paper does not exist in either exemplar canvas, in any source register, or (as cited) in the literature: it is the **illustrative placeholder example from REVIEW_QUESTION_TEMPLATE.md fields 18/20**, copied into a real canvas with a false attribution to the exemplar file. Treated as fabrication per the QA brief.
- **Fix:** Removed in all three locations and replaced with register-backed sources that better support the claim: Ji et al. 2023 (ACM CSUR hallucination survey), Magesh et al. 2024 (commercial RAG tools hallucinate 17–33%), and incident-register entries Moffatt v. Air Canada 2024 and NYC MyCity 2024 — the latter also satisfying the canvas's own open [TO VERIFY: FS-sector chatbot mis-statement incident]. Change-log v1.0.1 entry added to the canvas recording the removal. Net effect: CON.md [TO VERIFY] count fell from 17 to 15.

### 2.2 Preamble ★-range overstatements (RES, TPR, CON)
- **Defect:** The reported "blended ★ ratings" are confined to domain-preamble prose, not field-11 ratings (which are all single-valued and compliant). But three preambles overstated the file's actual ratings: RES claimed containment/recovery "★3" and drift design "★2–★3" (actuals: RES-002/-003/-004/-006 are ★2); TPR claimed contractual controls "★3–★4" (file maximum is ★3); CON claimed fairness testing "★3–★4" and proxy/pricing "★2–★3" (actuals: CON-001 ★3, all others ★2).
- **Fix:** All three preamble sentences corrected to the honest single values matching the canvases, with the maturity nuance retained in prose. No field-11 rating needed changing.

### 2.3 No other edits required
GOV file (including the provenance-flagged GOV-001…007), HUM file and TPR/RES canvas bodies required no substantive correction.

---

## 3. Provenance verdict on the "pre-existing" files (GOV-001…007, all of TPR, all of RES)

**Verdict: legitimate and retainable.** Under extra scrutiny, all ~22 flagged canvases: (a) carry the full 21-field structure including field 1; (b) match register wording verbatim; (c) sit in correct subdomains with correct boundary discipline (including the GOV header's explicit boundary note); (d) use single-value, anchor-honest ★ ratings with reporting caveats; (e) cite only register-traceable or common-knowledge sources, and — distinctively — flag missing literature with explicit [TO VERIFY] statements rather than inventing citations (TPR and RES are the heaviest [TO VERIFY] users in the battery for precisely this reason, which is a marker of honest drafting, not of corner-cutting). Whatever their commissioning path, the content meets the standard; the only defects attributable to them were the preamble ★-range overstatements (§2.2), now fixed. The one fabrication in the batch (§2.1) was in CON-004, which was **not** in the provenance-flagged set.

---

## 4. Residual [TO VERIFY] items — batch 3

- CANVASES_HUM.md: 8 (regulatory pinpoints and citation-detail checks)
- CANVASES_GOV.md: 10 (pinpoints; MAS/EU AI Act article confirmations)
- CANVASES_TPR.md: 24 (pinpoints + honest research-gap flags: AI contract-clause guidance, embedded-AI commentary, vendor-drift literature, backdoored-OSS-fine-tune research, embedding-mismatch literature, provider-ToS comparative study)
- CANVASES_RES.md: 10 (pinpoints + CMORG/AI-fallback guidance, SRE-for-AI literature gaps)
- CANVASES_CON.md: 15 (pinpoints + FS-specific vulnerability-detection, exclusion, price-discrimination and disclosure-comprehension research gaps)

**Batch 3 total: 67.** All are disclosure flags (section pinpoints or genuine literature gaps); none indicates an invented source remaining in text.

---

## 5. Defect count by category — batch 3

| Category | Fixed |
|---|---|
| Fabricated citation removed | **1** (CON-004 "Ray et al., 2023" — template placeholder with false attribution; removed from 3 locations, replaced with register-backed sources, change-logged) |
| Preamble ★ accuracy | 3 (RES, TPR, CON ranges corrected to actual single values) |
| ★ downgrades (field 11) | 0 (all 43 anchor-honest; no blended field-11 ratings existed) |
| Structure / wording / subdomain / anchoring / controls / weighting / boundary / spelling / tone / test-safety defects | 0 |

---

## 6. Battery-completion statement

All nine domain files now exist and pass QA: **93 IRQ canvases total** — 91 drafted across CANVASES_{DAT,MOD,AGT,HUM,SEC,TPR,RES,CON,GOV}.md plus 2 gold-standard canvases held in EXEMPLAR_CANVASES.md and referenced by format-consistent POINTER entries (MOD-006, SEC-003). Battery-wide: 93 unique AO IDs (no duplicates), zero invalid Related-IRQ references, register-verbatim wording throughout, no composite risk scores, UK spelling and board-ready reporting language throughout.

**Residual [TO VERIFY] by file (battery-wide, post-QA):**
AGT 8 · MOD 12 · SEC 8 · DAT 18 · HUM 8 · GOV 10 · TPR 24 · RES 10 · CON 15 — **total 113**, all disclosure flags (regulatory section pinpoints or honestly declared literature gaps) to be cleared before external issue.

## 7. Verdict

**Batch 3 — and the completed battery — meets the exemplar bar.** The single serious defect (a template placeholder masquerading as a citation in CON-004) has been removed and replaced with stronger register-backed evidence; the provenance-flagged GOV/TPR/RES canvases proved sound under heightened scrutiny; all ★ ratings across the 93-canvas battery are now single-valued and anchor-honest, including one downgrade in batch 1 (AGT-012 ★3→★2). The battery is ready for the [TO VERIFY] clearance pass and custodian sign-off.
