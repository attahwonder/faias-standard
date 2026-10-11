# QA LOG — Batch 1: CANVASES_AGT.md (13 canvases) & CANVASES_MOD.md (12 canvases + MOD-006 pointer)

**A note on file names (added 3 October 2026).** The file names in this record refer to the layout before FAIAS v1.3.1, in which each domain's Review Canvases, and each domain's test procedures, were held in one file. From v1.3.1 each canvas and each procedure is held in its own file. 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier files to its new file and line, so the file and line references below still resolve.

**QA reviewer:** FAIAS QA
**Date:** 2026-07
**References applied:** REVIEW_QUESTION_TEMPLATE.md (21-field spec); ASSURANCE_MODEL.md (L1–L5, ★ anchors, 5-axis rule); METHODOLOGY_STANDARDS.md §§3a–3d; EXEMPLAR_CANVASES.md; IRQ_REGISTER.md; IRQ_CLAIM_MATRIX.md; TAXONOMY.md; V1 source registers (academic, labs, incidents); V5 regulatory register.

---

## 1. Checks performed and results

| Check | Method | Result |
|---|---|---|
| IRQ wording verbatim vs register | Scripted diff of every "Register question" line against IRQ_REGISTER.md | **Pass — 25/25 exact matches** |
| Subdomain assignment | Footer Subdomain lines vs TAXONOMY.md homes | **Pass** (AGT C.1–C.7 and MOD B.1–B.6 all correct, incl. C.7 × 4 and B.4/B.5 × 3) |
| 21 fields present and substantive | Scripted count of `## N.` headings per canvas; sampled full-canvas reads (AGT-001…004, AGT-009, AGT-011, AGT-012; MOD field extracts across all 12) | **Pass — 21/21 fields in all 25 canvases; no placeholder text found** |
| Failure-mode anchoring | All 25 field-4 statements and all titles extracted and reviewed | **Pass** — every canvas anchors on an unsafe boundary crossing, not behaviour/consequence; failure chains run technical cause → business/regulatory impact with control breakpoints |
| ★ rating honesty | All 25 test ratings + written justifications reviewed against ASSURANCE_MODEL §6 anchors | **1 downgrade** (AGT-012, see §2.1); remainder honest — MOD ★3 ratings (MOD-004, -005, -010, -011) match the ★3 anchor (multi-group research methods, no benchmark); AGT-008/-013 ★1 correctly rated with "no standardised benchmark" stated |
| L1–L2 flagging / reporting caveats | Field 10 + 14 extracts | **Pass** — L1 items carry "flag: assertion only"-style caveats; every Pass reporting paragraph discloses the ★ level with 3b/3c-compliant language; ★1/★2 conclusions labelled professional judgement |
| Controls traced | Field 9 extracts, all canvases | **Pass** — every control cites regulation/standard/published research or is labelled emerging practice; no invented controls found |
| Citation spot-check vs registers | All arXiv IDs, lab publications, incidents and regulatory instruments in fields 9/17/18/20 cross-checked against SOURCE_REGISTER_ACADEMIC/LABS, INCIDENT_REGISTER, SOURCE_REGISTER_REGULATORY | **Pass with 1 date correction** (see §2.2). All arXiv IDs match register entries; incidents (Replit AIID #1152, Knight Capital, Grok, Air Canada, CNET, Mata v. Avianca, Deloitte Australia, GTG-1002) all in INCIDENT_REGISTER; Willison "Lethal Trifecta" blog is register-sanctioned. No fabricated citations detected — none removed |
| Risk weighting | All 25 five-axis tables extracted | **Pass** — 5 axes, 1–4 ordinal, one-line justifications, no composite scores anywhere |
| Boundary discipline | Grep for injection/jailbreak scope bleed in AGT; AGT-009 vs MOD-013 comparison per TAXONOMY ruling 13; memory rulings 2 & 5 | **Pass** — AGT canvases reference SEC IRQs only as linked controls/breakpoints; AGT-009 (agent reasoning artefacts) and MOD-013 (change-control discipline) are differentiated and cross-linked, not duplicated |
| Non-production testing | All 25 Independent Tests reviewed | **Pass** — every test states isolated staging/non-production execution, no live data |
| UK spelling / tone | Scripted US-spelling scan; reporting-language tone review | **Pass** — no US spellings; reporting language is board-ready op-res tone throughout |
| Cross-file consistency | AO ID format, related-IRQ validity, headers, duplication | AO IDs uniform (`AO-<DOM>-NNN` bold, "shall" statements); **every IRQ ID referenced in either file validates against the register (0 invalid)**; MOD file header defect fixed (§2.3); no duplicated canvas content between files |

---

## 2. Material changes made

### 2.1 IRQ-AGT-012 — ★ rating downgraded ★3 → ★2 (rating inflation)
- **Defect:** Independent Test rated ★3, but the canvas's own justification conceded "test design remains bespoke to the firm's specific action classes and gate architecture" with a single vendor worked example (OpenAI Operator card). ASSURANCE_MODEL §6 ★3 requires methodology used by multiple independent research groups; bespoke institution-specific design with judgement dominant is the ★2 anchor. Internally inconsistent with sibling canvases: AGT-013's ★1 justification explicitly states the Operator card is "a single published worked example rather than a general methodology", and AGT-003/-005 (comparable OWASP-informed adversarial tests) are rated ★2. Incident evidence (Replit) supports harm plausibility (Test 2), not test-methodology maturity.
- **Fix:** Field 11 rating and justification rewritten to ★2 anchor language; field 14 Pass reporting caveat updated to ★2 with "professional assessment" wording; Residual Judgement "even at ★3" → ★2; footer Test 3 → "★2 methodology, honestly caveated"; change-log entry v1.0.1 added recording the downgrade. Risk profile and controls unchanged.

### 2.2 IRQ-AGT-011 — citation date correction
- **Defect:** Field 18 in-text cited "[Anthropic, 2025, 'Sabotage Evaluations for Frontier Models']" while the reference list ([3]) and SOURCE_REGISTER_LABS both date it October 2024.
- **Fix:** In-text date corrected to 2024.

### 2.3 CANVASES_AGT.md — Domain Preamble ★ claims corrected (consequential to 2.1)
- **Defect:** Preamble stated tests "sit at ★2–★3 confidence" and that AGT-008/-013 are "rated ★1–★2"; after the AGT-012 downgrade the file contains only ★2 and ★1 ratings, and AGT-008/-013 are both ★1.
- **Fix:** Preamble amended to "★2 confidence", "inflating agentic test confidence to ★3+", and "rated ★1" for the two least-mature IRQs.

### 2.4 CANVASES_MOD.md — header inaccuracy and cross-file format inconsistency
- **Defect:** Header claimed "This file contains Review Canvases for all 13 MOD IRQs" (it contains 12; MOD-006 is a pointer to EXEMPLAR_CANVASES.md), and the file lacked the structured header metadata block used by CANVASES_AGT.md.
- **Fix:** Header rewritten to the AGT-format metadata block (Domain / IRQs covered / Compiled / Structure / Spelling) with accurate coverage statement "12 of 13; IRQ-MOD-006 maintained in EXEMPLAR_CANVASES.md", and the descriptive paragraph retitled as a Domain Preamble.

---

## 3. Items reviewed and deliberately NOT changed

- **IRQ-AGT-011 Severity 4:** Borderline against the §7 anchor, but defensible — inability to reconstruct any consequential decision undermines the evidential basis of the whole agentic control estate and record-keeping breaches carry enforcement exposure; justification is explicit. Retained.
- **Willison "Lethal Trifecta" (blog) citations (AGT-004):** Blogs are normally excluded under METHODOLOGY_STANDARDS §1, but this source is expressly admitted in SOURCE_REGISTER_ACADEMIC ("blog, widely cited"). Retained with register sanction. **Note (added 10 October 2026).** The register entry now reads "blog". The words "widely cited" were removed from it in v1.3.3.
- **SS1/21 / PS21/3 and UK GDPR citations:** Not itemised in the V5 register but are common-knowledge UK instruments also used by the exemplar canvases (Canvas 1, field 17). Retained.
- **AGT-009 vs MOD-013 overlap:** Both address prompt change discipline; content is differentiated per TAXONOMY boundary ruling 13 (agent reasoning artefacts vs generic configuration change control) and cross-linked. No dedup required.

---

## 4. Residual [TO VERIFY] items (pre-existing, correctly flagged; not resolved in this QA batch)

20 instances across both files, all of the same class: **regulatory section/paragraph pinpoints** ("Section pinpoints [TO VERIFY] before external issue") in field 17 of:
- AGT: 001, 002, 011, 012 (and equivalent phrasing in several other AGT canvases).
- MOD: 001, 002, 003, 004, 005, 007, 008, 009, 010, 011, 012, 013 (all twelve).

These are appropriate honesty flags — the instruments cited (PRA SS1/23, FCA PRIN 2A, NIST AI 600-1, EU AI Act Arts. 12/19, MAS AIRG consultation) are register-verified; only exact section pinpoints remain to be confirmed before external issue. No citation was found to be untraceable or fabricated; nothing was removed.

Additional register-side caveat carried through: MAS AIRG consultation reference number is marked [UNVERIFIED ref no.] in the V5 register itself.

---

## 5. Defect count by category

| Category | Fixed |
|---|---|
| ★ rating inflation (downgrade) | 1 (AGT-012 ★3→★2, plus consequential preamble correction) |
| Citation error (date) | 1 (AGT-011 Sabotage Evaluations 2025→2024) |
| Header/cross-file consistency | 1 (MOD header inaccuracy + format harmonisation) |
| Fabricated citations removed | 0 |
| Register-wording, subdomain, field-completeness, controls, risk-weighting, boundary, spelling, tone defects | 0 |

## 6. Verdict

**The batch meets the exemplar bar.** Both files match the EXEMPLAR_CANVASES.md quality standard in structure, failure-mode anchoring, evidence-level discipline, control traceability, citation hygiene and reporting tone. The only material quality defect was a single inflated ★ rating (AGT-012), now corrected; all other findings were minor consistency issues. The 20 residual [TO VERIFY] pinpoint flags must be cleared before external issue but are correctly disclosed in-text.
