# Verification Log B — Source Verification Pass (July 2026)

**A note on file names (added 3 October 2026).** The file names in this record refer to the layout before FAIAS v1.3.1, in which each domain's Review Canvases, and each domain's test procedures, were held in one file. From v1.3.1 each canvas and each procedure is held in its own file. 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier files to its new file and line, so the file and line references below still resolve.

Scope: all `[TO VERIFY]` flags in CANVASES_HUM.md (8), CANVASES_GOV.md (10), CANVASES_TPR.md (24), CANVASES_RES.md (10), CANVASES_CON.md (15); all `[UNVERIFIED]` entries in V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md (9) and flagged items in V1_Research_Compendium registers (3). Total: 79 flags reviewed.

Resolution key: **CONFIRMED** = claim verified accurate against a live primary source, tag removed. **CORRECTED** = claim was materially wrong or overstated; fixed and verified. **UNRESOLVABLE** = no primary source could establish or refute the pinpoint/citation; retagged `[UNVERIFIED — reason]` rather than asserting an unverified pinpoint, with the general claim (module/article-level reference) confirmed accurate where applicable.

## CANVASES_HUM.md (8 flags — 0 confirmed, 0 corrected, 8 unresolvable)

| # | Location (line, pre-edit) | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | 169 | SM&CR section pinpoint for AI-assisted review control | UNRESOLVABLE — SM&CR modules (SYSC 2/4/24-25), PRIN 2A confirmed extant; no AI-specific sub-clause published | fca.org.uk/handbook |
| 2 | 383 | Section pinpoints for approval-theatre/throughput-pressure control | UNRESOLVABLE — SYSC 19D, Art. 14(4) confirmed extant; no sub-clause published for this scenario | fca.org.uk/handbook; eur-lex.europa.eu (Reg 2024/1689) |
| 3 | 599 | Section pinpoints — AI-specific fallback under SYSC 15A.6/SS1/21/PS21/3 | UNRESOLVABLE — modules confirmed extant and in force; no AI-component-specific sub-clause published | fca.org.uk; bankofengland.co.uk |
| 4 | 812 | Section pinpoints — SYSC 19D / SYSC 9 stop-mechanism control | UNRESOLVABLE — modules confirmed extant; no sub-clause specific to AI stop mechanisms | fca.org.uk/handbook |
| 5 | 1030 | Section pinpoints — PS21/3 / SS1/21 tested suspension authority | UNRESOLVABLE — documents confirmed extant; no AI-specific sub-clause | bankofengland.co.uk |
| 6 | 1247 | SM&CR application to multi-agent workflows | UNRESOLVABLE — SM&CR, SYSC 19D, SYSC 9 confirmed extant; no text addressing multi-agent attribution | fca.org.uk/handbook |
| 7 | 1460 | Section pinpoints — Art. 13/14 explanation adequacy | UNRESOLVABLE — articles confirmed extant; no sub-clause on internal decision-maker explanation adequacy | eur-lex.europa.eu |
| 8 | 1681 | Section pinpoints — DISP substantive review of AI-influenced decisions | UNRESOLVABLE — DISP, PRIN 2A, Art. 13 confirmed extant; no sub-clause on AI-contestability specifically | fca.org.uk/handbook |

## CANVASES_GOV.md (10 flags — 3 confirmed/corrected, 7 unresolvable)

| # | Location | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | 256 | MAS AIRG consultation — inventory requirement, "before external issue" | CORRECTED — consultation closed Jan 2026; final Guidelines not published as of 29 Jul 2026; no MAS reference number found | mas.gov.sg/publications/consultations/2025/... |
| 2 | 324 | MAS AIRG inventory requirement + reference number | CORRECTED — same as above; no distinct reference number exists on MAS site or secondary trackers | mas.gov.sg; linklaters/allenandgledhill trackers |
| 3 | 345 | Footnote reference number for AIRG consultation | CORRECTED — no reference number published; URL and status recorded instead | mas.gov.sg |
| 4 | 632 | MAS AIRG proportionality framework | CORRECTED — consultation status confirmed (closed Jan 2026, not finalised) | mas.gov.sg |
| 5 | 735 | Footnote reference (duplicate of #3) | CORRECTED | mas.gov.sg |
| 6 | 1511 | Section pinpoints — SS1/23 Principle 5 / ISO 42001 cl.9.3 escalation | UNRESOLVABLE — documents/clauses confirmed extant; no AI-specific sub-clause | bankofengland.co.uk; iso.org |
| 7 | 1723 | Section pinpoints — AI Act Art.11/Annex IV, SS1/23, ISO 42001 cl.7.5 | UNRESOLVABLE — articles/clauses confirmed extant; no further sub-clause specificity available | eur-lex.europa.eu |
| 8 | 1941 | Section pinpoints — AI Act Art.12/19, SYSC/DISP record-keeping | UNRESOLVABLE — confirmed extant at module level only | eur-lex.europa.eu; fca.org.uk |
| 9 | 2157 | Section pinpoints — Art.6/Annex III, SS2/21, PRIN 2A | UNRESOLVABLE — confirmed extant at module/article level only | eur-lex.europa.eu |
| 10 | 2411 | Section pinpoints — Art.9, SS1/23 envelope-drift interpretation | UNRESOLVABLE — no UK/FS text names "envelope drift"; explicitly FAIAS's own framing (already noted in text) | eur-lex.europa.eu |

## CANVASES_TPR.md (24 flags — 3 confirmed/corrected, 21 unresolvable)

| # | Location | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | header ¶ | generic "[TO VERIFY]" convention note | Convention note only — updated to reference this log | n/a |
| 2 | 74 | EBA GL/2019/02 section — materiality-tiered assessment | CORRECTED on re-check — the earlier CONFIRMED was wrong. Pre-outsourcing analysis and due diligence are Title IV, Section 12 (12.3 Due diligence); criticality is Title II, Section 4. Sections 5 and 11 are governance and documentation requirements in Title III | eba.europa.eu / bde.es PDF |
| 3 | 77 | PRA SS1/23 applicability to vendor model evaluation | RESOLVED on re-check — the earlier finding was a false negative. The PRA states the principles apply to models whether developed in-house or externally, including vendor models. Only the AI-specific application remains a FAIAS extension | bankofengland.co.uk |
| 4 | 138 | EBA GL/2019/02 clause mapping to AI criteria | CORRECTED on re-check — the due-diligence section is Title IV, Section 12 (12.3), not Sections 5/11; no AI-specific criteria exist in the Guidelines | eba.europa.eu |
| 5 | 156 | EBA GL/2019/02 current version status | CONFIRMED — no superseding outsourcing guideline identified | eba.europa.eu |
| 6 | 251 | EBA GL/2019/02 contractual content section | CORRECTED on re-check — Section 13 (Contractual phase) sits in Title IV, not Title II | eba.europa.eu |
| 7 | 314 | EBA GL/2019/02 exact clause reference (contracts) | CONFIRMED — Title IV, Section 13 (Contractual phase); 13.3 audit rights, 13.4 termination | eba.europa.eu |
| 8 | 317 | Sector-specific AI contract clause guidance (UK Finance/ISDA) | UNRESOLVABLE — no such publication located after search | n/a |
| 9 | 335 | Source access-date version status | UNRESOLVABLE — generic access-date caveat, source confirmed live | n/a |
| 10 | 424 | EBA GL/2019/02 applicability to embedded features | UNRESOLVABLE — Guidelines govern outsourced functions generally; no embedded-feature-specific text | eba.europa.eu |
| 11 | 485 | EBA GL/2019/02 applicability to feature-level embedded AI | UNRESOLVABLE — same as above; FAIAS interpretive extension | eba.europa.eu |
| 12 | 488 | Citable source on shadow/embedded AI in FS | UNRESOLVABLE — no peer-reviewed source located; industry/analyst commentary only | n/a |
| 13 | 502 | Source access-date version status | UNRESOLVABLE — generic caveat | n/a |
| 14 | 658 | PRA SS1/23 applicability to vendor-hosted model drift | UNRESOLVABLE — Principle 5 does not name vendor-hosted models; FAIAS extension | bankofengland.co.uk |
| 15 | 661 | Peer-reviewed source on silent vendor-side LLM drift | UNRESOLVABLE — no confirmed reference found; BoE FPC framing (Apr 2025) is the closest supervisory-level source | bankofengland.co.uk (FPC, Apr 2025) |
| 16 | 831 | DORA Art.9 / SS1/23 applicability to open-weight artefacts | UNRESOLVABLE — neither names open-weight models; FAIAS extension | eur-lex.europa.eu |
| 17 | 834 | Peer-reviewed research on backdoored open-source LLM fine-tunes | UNRESOLVABLE — young research area, no canonical paper confirmed | n/a |
| 18 | 998 | DORA Art.11 / SS2/21 applicability to embedding/vector-DB dependency | UNRESOLVABLE — FAIAS extension of general BC/outsourcing obligations | eur-lex.europa.eu |
| 19 | 1001 | Peer-reviewed source on "embedding-index mismatch" | UNRESOLVABLE — no such named study located | n/a |
| 20 | 1106 | ICO guidance title/date for AI-specific DPIA | CONFIRMED — ICO "Guidance on AI and data protection" (updated Mar 2023) and "Generative AI: eight questions..." (2023–24 series) | ico.org.uk |
| 21 | 1167 | ICO guidance confirming DPIA-trigger status for GenAI | CONFIRMED — ICO guidance confirms AI/ML processing frequently meets Art.35(3) high-risk criteria | ico.org.uk |
| 22 | 1170 | Comparative study of consumer vs enterprise AI ToS | UNRESOLVABLE — no comparative academic study located; pattern documented at individual-provider level only | n/a |
| 23 | 1191 | Source access-date version status | UNRESOLVABLE — generic caveat | n/a |
| 24 | 1345 | Firm-level academic study of AI concentration-risk methodology | UNRESOLVABLE — no such study located; BoE FPC remains supervisory-level evidence only | bankofengland.co.uk |

## CANVASES_RES.md (10 flags — 2 corrected, 8 unresolvable)

| # | Location | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | header ¶ | generic convention note | Updated to reference this log | n/a |
| 2 | 143 | CMORG/sector AI fallback-design guidance | CORRECTED — CMORG has published "AI Baseline Guidance Review" (Apr 2025) and AI Taskforce guidance, but neither specifies AI-component fallback design at this granularity; "none established" at this level stands | cmorg.org.uk |
| 3 | 315 | Peer-reviewed source on "unsafe degradation under partial AI-pipeline failure" | UNRESOLVABLE — no such named study located | n/a |
| 4 | 491 | Regulatory reference to agentic AI containment specifically | UNRESOLVABLE — DORA Art.11-12, SS1/21 confirmed extant; no agentic-AI-specific rule | eur-lex.europa.eu; bankofengland.co.uk |
| 5 | 494 | Peer-reviewed source on "mid-plan agent termination safety" | UNRESOLVABLE — no such named study located | n/a |
| 6 | 669 | Peer-reviewed source on "AI behavioural component rollback" | UNRESOLVABLE — no such named study located | n/a |
| 7 | 1027 | More specific regulatory text on gradual-degradation detection | UNRESOLVABLE — no such PRA/DORA text located | n/a |
| 8 | 1030 | Peer-reviewed source on "slow-decay LLM quality monitoring in FS" | UNRESOLVABLE — no such named study located | n/a |
| 9 | 1147 | CMORG AI-specific scenario library | CORRECTED — CMORG's Apr 2025 guidance is a reference compilation, not a scenario library; "still developing" stands | cmorg.org.uk |
| 10 | 1210 | CMORG AI-specific scenario-testing guidance | CORRECTED — same finding; no scenario-testing-specific guidance located | cmorg.org.uk |

## CANVASES_CON.md (15 flags — 4 confirmed/corrected, 11 unresolvable)

| # | Location | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | header ¶ | generic convention note | Updated to reference this log | n/a |
| 2 | 81 | FCA/PRA equivalent of MAS FEAT | UNRESOLVABLE — no domestic equivalent beyond Consumer Duty/PRIN 2A located | fca.org.uk |
| 3 | 144 | NYDFS Apple Card report citation/conclusions | CONFIRMED — "Report on Apple Card Investigation," NYDFS, 23 Mar 2021; found no fair-lending violation, noted opacity/difficulty proving algorithmic discrimination | dfs.ny.gov/reports_and_publications/202103_report_apple_card_investigation |
| 4 | 175 | Exact title/date/URL of NYDFS report | CONFIRMED — as above | dfs.ny.gov |
| 5 | 334 | FS-specific confirmed proxy discrimination incident report | UNRESOLVABLE — none located distinct from Apple Card (which itself found no violation) | n/a |
| 6 | 512 (x2) | NLP vulnerability-indicator research; dark-patterns citation | UNRESOLVABLE — no such study/citation located | n/a |
| 7 | 688 | FCA GenAI-specific customer-communications guidance | UNRESOLVABLE — only general "AI and the FCA: our approach" / AI Update (Apr 2024) found, nothing GenAI-communications-specific | fca.org.uk |
| 8 | 870 | FCA financial-inclusion strategy on AI-driven exclusion | UNRESOLVABLE — none located beyond FG21/1 and Consumer Duty | fca.org.uk |
| 9 | 873 (x2) | Data-sparsity penalisation research citation | UNRESOLVABLE — no such study located | n/a |
| 10 | 1051 (x2) | AI/ML price-discrimination FS research citation | UNRESOLVABLE — no such study located | n/a |
| 11 | 1161 | Direct regulatory citation for reject inference | CONFIRMED (partial) — Anderson, R., "The Credit Scoring Toolkit," OUP, ISBN 9780199226405, confirmed as the canonical practitioner text; no direct FCA/PRA mandate located (remains unresolvable on that point) | Oxford University Press catalogue |
| 12 | 1224 | FCA/PRA MRM publication on retraining-induced feedback loops | UNRESOLVABLE — none located; SS1/23 remains current with no confirmed successor | n/a |
| 13 | 1227 | Canonical citation for reject inference (Anderson) | CONFIRMED — Anderson, R. (2007), "The Credit Scoring Toolkit," Oxford University Press, ISBN 9780199226405 | Oxford University Press / Google Books |
| 14 | 1395 | FCA AI transparency/disclosure guidance | UNRESOLVABLE — none beyond Consumer Duty and general AI approach page | fca.org.uk |
| 15 | 1398 (x2) | FS customer-comprehension-of-AI-disclosure research; right-to-explanation citation | UNRESOLVABLE — no such study/canonical citation located | n/a |

## V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md (9 flags — 3 confirmed/corrected, 6 unresolvable)

| # | Entry | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | Rusu/Rathi speeches | Individual speech pages not fetched | UNRESOLVABLE — index page confirmed live, individual titles/dates not each confirmed | fca.org.uk/news/speeches |
| 2 | AIC minutes | Page structure not fetched | UNRESOLVABLE — page blocked by robots.txt; existence/URL confirmed via search only | bankofengland.co.uk/financial-stability/artificial-intelligence-consortium |
| 3 | Prohibited practices guidelines Art.5 | Reference number C(2025) 884 | UNRESOLVABLE — press page and Feb 2025 date confirmed; document number not independently confirmed against OJ/Commission register **Correction (added 10 October 2026).** The Guidelines are C(2025) 5052 final of 29 July 2025. Their content was approved as C(2025) 884 final and published on 4 February 2025. | digital-strategy.ec.europa.eu |
| 4 | EBA/ESA AI statements | Document titles/dates | UNRESOLVABLE — rolling-programme placeholder; individual documents not confirmed | eba.europa.eu |
| 5 | MAS AIRG consultation reference number | "P020-2025" placeholder | CORRECTED — no formal MAS reference number found on MAS site or secondary trackers (Linklaters, Allen & Gledhill, BABL AI, Waystone); field corrected to state this explicitly | mas.gov.sg/publications/consultations/2025/consultation-paper-on-guidelines-on-artificial-intelligence-risk-management |
| 6 | MDDI/MAS MindForge | Exact titles/dates | UNRESOLVABLE — collaboration confirmed via secondary reporting; primary document list not confirmed | mas.gov.sg |
| 7 | HKMA 2019 High-level Principles | URL pattern | UNRESOLVABLE — date/series consistent with secondary reporting; exact PDF not re-fetched | hkma.gov.hk |
| 8 | HKMA GenAI Sandbox insight reports | Specific titles | UNRESOLVABLE — programme and Aug 2024 launch confirmed; individual report titles not confirmed | hkma.gov.hk |
| 9 | HKMA AML/AI circular date | "Circular of 9 Sep 2024" | CONFIRMED — verified live: "Use of Artificial Intelligence for Monitoring of Suspicious Activities," circular of 9 Sep 2024 | hkma.gov.hk/media/eng/doc/key-information/guidelines-and-circular/2024/20240909e1.pdf |

Also corrected while in the register (not part of original 9, found during the same pass and fixed for accuracy):
- **NIST COSAIS status** — CONFIRMED: concept paper released 26 Aug 2025, programme still in development (draft use cases) — [nist.gov](https://www.nist.gov/news-events/news/2025/08/nist-releases-control-overlays-securing-ai-systems-concept-paper) **Correction (added 10 October 2026).** NIST released the concept paper on 14 August 2025, not 26 August 2025. An annotated outline followed on 8 January 2026.
- **ISO/IEC 27090 status** — CORRECTED: exact title confirmed; standard is at FDIS ballot stage (50.20), not yet published — [iso.org/standard/56581.html](https://www.iso.org/standard/56581.html)
- **OWASP AI Testing Guide status** — CORRECTED: v1.0 officially released 26 Nov 2025 (was previously listed "in progress") — [owasp.org/www-project-ai-testing-guide](https://owasp.org/www-project-ai-testing-guide/)

## V1_Research_Compendium registers (3 flags — 3 confirmed/corrected, 0 unresolvable)

| # | File | Claim | Resolution | Source |
|---|---|---|---|---|
| 1 | SOURCE_REGISTER_LABS.md | Mistral "Frontier Safety Framework," 2025 | CORRECTED — no such document exists; Mistral signed the Seoul Summit political commitment (May 2024) but has not published a named frontier safety framework as of 29 Jul 2026 (confirmed gap per independent SaferAI tracker) | mistral.ai; sladebyrd.com/ai-safety-orgs/mistral; tracker.safer-ai.org |
| 2 | SOURCE_REGISTER_ACADEMIC.md | Agent-SafetyBench: "no tested agent exceeded 60% safe" | CONFIRMED — exact abstract quote: "none of the agents achieves a safety score above 60%" (16 agents tested, 349 environments, 2,000 cases) | arxiv.org/abs/2412.14470 |
| 3 | INCIDENT_REGISTER.md | CBA redundancy-reversal — workload claims, call volumes | CORRECTED & EXPANDED — confirmed 21 Aug 2025; FSU primary account: call volumes were rising (Direct Banking demand), CBA offered overtime while pursuing 45 redundancies; CBA admitted the error | theguardian.com/australia-news/2025/aug/21/cba-reverses-ai-job-cuts-decision; fsunion.org.au/win-cba-backflips-on-customer-service-job-cuts-admits-they-got-it-wrong |

---

## Summary counts

| File | Flags | Confirmed | Corrected | Unresolvable |
|---|---|---|---|---|
| CANVASES_HUM.md | 8 | 0 | 0 | 8 |
| CANVASES_GOV.md | 10 | 0 | 5 | 5 |
| CANVASES_TPR.md | 24 | 5 | 1 | 18 |
| CANVASES_RES.md | 10 | 0 | 3 | 7 |
| CANVASES_CON.md | 15 | 3 | 1 | 11 |
| SOURCE_REGISTER_REGULATORY.md | 9 | 1 | 1 (+3 bonus corrections outside the original 9) | 7 |
| V1_Research_Compendium (3 items) | 3 | 1 | 2 | 0 |
| **Total** | **79** | **10** | **12** | **56** |

**Correction (added 10 October 2026).** The counts above do not all agree with the rows. The Corrected column sums to 13, not 12. By the first word of each row's Resolution cell, the sections hold: CANVASES_GOV.md 5 CORRECTED and 5 UNRESOLVABLE; CANVASES_TPR.md 4 CONFIRMED, 1 RESOLVED, 3 CORRECTED, 15 UNRESOLVABLE and 1 convention note; CANVASES_RES.md 3 CORRECTED, 6 UNRESOLVABLE and 1 row updated to reference this log; CANVASES_CON.md 4 CONFIRMED (one of them partial), 10 UNRESOLVABLE and 1 row updated to reference this log; SOURCE_REGISTER_REGULATORY.md 1 CONFIRMED, 1 CORRECTED and 7 UNRESOLVABLE. These counts differ from the headings of those five sections, and for CANVASES_TPR.md, CANVASES_RES.md and CANVASES_CON.md from the table. The CANVASES_HUM.md and research-register sections agree with their rows. The July 2026 record above is kept as written.

Note: the large "unresolvable" share is expected and by design for this domain — most flags are either (a) requests for a *sub-clause pinpoint* within an already-confirmed regulatory module/article (the module/article itself is accurate; no regulator has published AI-specific sub-clause text to cite more precisely), or (b) searches for a *specific peer-reviewed citation* for a named phenomenon where none was found to exist, which is itself the correct and honest finding rather than a gap in this verification pass. No substantive content was removed; no pinpoint was invented.
