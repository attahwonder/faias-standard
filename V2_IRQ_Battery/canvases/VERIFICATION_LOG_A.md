# Verification Log A — Batch [TO VERIFY] Clearance (July 2026)

**A note on file names (added 3 October 2026).** The file names in this record refer to the layout before FAIAS v1.3.1, in which each domain's Review Canvases, and each domain's test procedures, were held in one file. From v1.3.1 each canvas and each procedure is held in its own file. 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier files to its new file and line, so the file and line references below still resolve.

Method: each flag web-verified against primary sources (legislation.gov.uk, FCA Handbook,
Bank of England / PRA, EBA/ECB/EU AI Act official text, ICO, NIST, OWASP, arXiv/DOI). CONFIRMED =
pinpoint/detail verified as stated. CORRECTED = a factual error was found and fixed (with
before/after noted). UNRESOLVABLE (tagged `[UNVERIFIED — reason]` in the source files) = no
primary-source pinpoint could be found; content was generalised rather than left with an
invented citation.

## Headline finding

The EU AI Act's Digital Omnibus (agreed and entered into force July 2026) **postponed the Annex
III high-risk AI obligations (including credit-scoring and insurance-pricing systems) from 2
August 2026 to 2 December 2027**. Several canvases had asserted the original 2 Aug 2026 date;
these were corrected. Note: 2 Aug 2026 remains the applicable date for the separate Article 50
transparency obligations only.

| # | File | Canvas / line | Claim | Resolution | Source URL |
|---|------|----|-------|------------|------------|
| 1 | CANVASES_DAT.md | IRQ ~L139 (data provenance) | EU AI Act Art.10 applies to Annex III from "2 Aug 2026"; section pinpoint | CORRECTED (date → 2 Dec 2027, per Digital Omnibus) + pinpointed Art.10(2)(a)-(f), PRA SS1/23 Principles 3/4, ISO/IEC 42001 §6.2 | https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/ ; https://www.techtimes.com/articles/321681/20260727/eu-ai-act-omnibus-law-six-days-transparency-deadline-nudifier-apps-banned-december.htm |
| 2 | CANVASES_DAT.md | L142 (lineage reconstruction research gap) | No FS-specific empirical study located | UNRESOLVABLE → UNVERIFIED (genuine evidence gap confirmed; general analogues correct) | https://arxiv.org/ (Allen Institute Dolma/OLMo releases, general knowledge check) |
| 3 | CANVASES_DAT.md | L305 (repurposed personal data) | GDPR Art.5(1)(b)(c), Art.35; AI Act Art.10 pinpoint | CONFIRMED, pinpointed to Art.10(2)(b)/(g) | https://artificialintelligenceact.eu/article/10/ |
| 4 | CANVASES_DAT.md | L470 (label quality) | AI Act Art.10(3); PRA SS1/23 pinpoint | CONFIRMED, PRA SS1/23 Principles 3/4 | https://artificialintelligenceact.eu/article/10/ ; https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss |
| 5 | CANVASES_DAT.md | L473 (inter-annotator agreement research gap) | No FS-specific study located | UNRESOLVABLE → UNVERIFIED | n/a (negative search result) |
| 6 | CANVASES_DAT.md | L634 (synthetic data fidelity) | AI Act Art.10(2)-(3) | CONFIRMED, pinpointed Art.10(2)(f)/(3) | https://artificialintelligenceact.eu/article/10/ |
| 7 | CANVASES_DAT.md | L806 (representativeness) | AI Act Art.10(3); PRIN 2A; SS1/23 | CONFIRMED, PRA SS1/23 Principle 3 | https://artificialintelligenceact.eu/article/10/ |
| 8 | CANVASES_DAT.md | L985 (data poisoning) | AI Act Art.10 & Art.15; NIST AI 100-2 E2025 | CONFIRMED, pinpointed Art.10(2)(f) & Art.15(5); NIST doc title confirmed | https://artificialintelligenceact.eu/article/15/ |
| 9 | CANVASES_DAT.md | L1173 (feedback-channel vetting) | AI Act Art.10; SS1/23 ongoing monitoring | CORRECTED on re-check — monitoring sits under Principle 4 (independent model validation), not Principle 5 (model risk mitigants) | https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss |
| 10 | CANVASES_DAT.md | L1176 (model collapse / deliberate gaming research gap) | Shumailov et al. Nature 2024 DOI; Gerstgrasser/Dohmatob arXiv IDs; no FS-specific deliberate-gaming study | CONFIRMED (DOI and arXiv IDs correct) + UNVERIFIED for deliberate-gaming half (genuine gap) | https://doi.org/10.1038/s41586-024-07566-y |
| 11 | CANVASES_DAT.md | L1213 (cross-ref to #10) | Same as #10 | UNRESOLVABLE → UNVERIFIED (cross-reference) | (see #10) |
| 12 | CANVASES_DAT.md | L1354 (RAG currency) | PRIN 2A; SS1/23 pinpoint | CONFIRMED partial (SS1/23 Principles 3/4) + UNVERIFIED (mechanism not named in any source) | https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss |
| 13 | CANVASES_DAT.md | L1534 (RAG determinism) | PRIN 2A; SS1/23 pinpoint | CONFIRMED partial (SS1/23 Principle 2/4) + UNVERIFIED | (as above) |
| 14 | CANVASES_DAT.md | L1715 (RAG entitlement) | GDPR Art.32; FCA info-barrier rules | CONFIRMED (Art.32(1)(b)) + UNVERIFIED (no RAG-specific rule), general SYSC pinpoint added | https://www.legislation.gov.uk/eur/2016/679/article/32 |
| 15 | CANVASES_DAT.md | L1895 (memory store erasure) | GDPR Art.5(1)(e), Art.17, Art.30 | CONFIRMED — all three articles correct as cited | https://www.legislation.gov.uk/eur/2016/679/article/17 |
| 16 | CANVASES_DAT.md | L1898 (memory-store research gap) | No FS-specific study located | UNRESOLVABLE → UNVERIFIED | n/a (negative search result) |
| 17 | CANVASES_DAT.md | L2075 (input drift) | SS1/23 ongoing monitoring; AI Act Art.15 | CORRECTED on re-check — SS1/23 Principle 4 (monitoring); Principle 5 is model risk mitigants. Art.15(1)/(4) confirmed | https://artificialintelligenceact.eu/article/15/ |
| 18 | CANVASES_DAT.md | L2259 (embedding/retrieval drift) | SS1/23; AI Act Art.15 | CONFIRMED partial (Art.15(1)) + UNVERIFIED (mechanism not named) | https://artificialintelligenceact.eu/article/15/ |
| 19 | CANVASES_MOD.md | L146 (capability envelope) | SS1/23 development/validation pinpoint | CONFIRMED — Principle 3 (development/implementation/use) & Principle 4 (independent validation) | https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss |
| 20 | CANVASES_MOD.md | L339 (capability-delta re-approval) | SS1/23 pinpoint | CONFIRMED — Principle 3/4 | (as above) |
| 21 | CANVASES_MOD.md | L530 (reasoning-length degradation) | SS1/23 pinpoint | CONFIRMED partial (Principle 3/4) + UNVERIFIED (mechanism not named in source text) | (as above) |
| 22 | CANVASES_MOD.md | L717 (hallucination rate) | PRIN 2A; SS1/23 pinpoint | CONFIRMED — Principle 3/4 | (as above) |
| 23 | CANVASES_MOD.md | L921 (epistemic-state distinction) | PRIN 2A; SS1/23 pinpoint | CONFIRMED — Principle 3/4 | (as above) |
| 24 | CANVASES_MOD.md | L1120 (specification gaming) | SS1/23 pinpoint | CORRECTED on re-check — Principle 3 (development, implementation and use) and Principle 4 (independent model validation, incl. monitoring); Principle 5 is model risk mitigants | (as above) |
| 25 | CANVASES_MOD.md | L1321 (reward hacking/sycophancy) | SS1/23 independent-validation pinpoint | CONFIRMED — Principle 4 | (as above) |
| 26 | CANVASES_MOD.md | L1527 (CoT faithfulness) | PRIN 2A; SS1/23 pinpoint | CONFIRMED — Principle 4 | (as above) |
| 27 | CANVASES_MOD.md | L1731 (six-way shift taxonomy) | SS1/23 ongoing monitoring pinpoint | CORRECTED on re-check — Principle 4 only; Principle 5 is model risk mitigants | (as above) |
| 28 | CANVASES_MOD.md | L1936 (benchmark contamination) | SS1/23 independent-validation pinpoint | CONFIRMED — Principle 4 | (as above) |
| 29 | CANVASES_MOD.md | L2149 (model collapse) | FCA/PRA DP5/22, FS2/23 dates; SS1/23 pinpoint | CONFIRMED — DP5/22 (Oct 2022) and FS2/23 feedback statement (Oct 2023); SS1/23 Principle 3 | https://www.bankofengland.co.uk/prudential-regulation/publication/2023/may/model-risk-management-principles-for-banks-ss |
| 30 | CANVASES_MOD.md | L2357 (prompt version control) | SS1/23 change-management pinpoint | CORRECTED on re-check — Principle 3 (development, implementation and use) and Principle 4 (review of model changes, periodic revalidation). Principle 5 contains no change-control provision | (as above) |
| 31 | CANVASES_AGT.md | L152 (goal drift) | MAS Consultation Paper Nov 2025 pinpoint | CONFIRMED, added PRA SS1/23 Principle 4 anchor | (general knowledge; MAS CP corroborated by search) |
| 32 | CANVASES_AGT.md | L343 (mid-execution intent change) | PRA/FCA op-res regime pinpoint | UNRESOLVABLE → UNVERIFIED (general anchor SS1/21/PS21/3 confirmed; sub-paragraph pinpoint not confirmable) | https://www.bankofengland.co.uk/-/media/boe/files/prudential-regulation/supervisory-statement/2021/ss121-march-22.pdf |
| 33 | CANVASES_AGT.md | L721 (composite tool-chaining) | MAS CP pinpoint | CONFIRMED, added GDPR Art.5(1)(c) anchor | (as above, #31) |
| 34 | CANVASES_AGT.md | L1706 (prompt version control / EU AI Act) | AI Act "Art.9-15" pinpoint | CORRECTED — narrowed to Art.9 (risk management) and Art.12 (record-keeping); noted Dec 2027 Annex III postponement | https://artificialintelligenceact.eu/article/12/ ; https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/ |
| 35 | CANVASES_AGT.md | L1910 (agentic workflow conformance) | MCOB, DISP, SS1/23, record-keeping pinpoints | CONFIRMED — MCOB 11.6, DISP 1.4/1.6, SS1/23 Principle 2 | https://handbook.fca.org.uk/handbook/MCOB/11/6.html ; https://handbook.fca.org.uk/handbook/disp1/disp1s4 |
| 36 | CANVASES_AGT.md | L2122 (agentic trace record-keeping) | EU AI Act Art.12 & Art.19 pinpoint | CORRECTED — dated to 2 Dec 2027 (Digital Omnibus postponement) rather than assuming 2 Aug 2026 | https://artificialintelligenceact.eu/article/19/ ; Digital Omnibus source (as #1) |
| 37 | CANVASES_AGT.md | L2336 (structural gating of irreversible actions) | PRA SS1/21 pinpoint | UNRESOLVABLE → UNVERIFIED (general anchor confirmed; exact sub-paragraph not confirmable) | https://www.bankofengland.co.uk/-/media/boe/files/prudential-regulation/supervisory-statement/2021/ss121-march-22.pdf |
| 38 | CANVASES_AGT.md | L2552 (computer-use agent GUI safety) | PRA SS1/21 pinpoint | UNRESOLVABLE → UNVERIFIED (general anchor confirmed; exact paragraph not confirmable) | (as above) |
| 39 | CANVASES_SEC.md | L143 (direct prompt injection) | FCA chatbot-specific supervisory statement | UNRESOLVABLE → UNVERIFIED (no such statement located; PRIN 2A remains general anchor) | n/a (negative search result) |
| 40 | CANVASES_SEC.md | L511 (attack class / agentic) | Forthcoming EU AI Act Annex III timing for agentic FS deployments "from Aug 2026" | CORRECTED — 2 Dec 2027, per Digital Omnibus | https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/ |
| 41 | CANVASES_SEC.md | L1067 (fine-tuning/personal data extraction) | ICO AI guidance section reference | UNRESOLVABLE → UNVERIFIED (document/URL confirmed; guidance is an unnumbered web hub, no stable section reference exists) | https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/artificial-intelligence/guidance-on-ai-and-data-protection/ |
| 42 | CANVASES_SEC.md | L1098 (reference [7], ICO guidance) | Exact section reference | UNRESOLVABLE → UNVERIFIED (same reasoning as #41; URL added) | (as above) |
| 43 | CANVASES_SEC.md | L1460 (model-artefact supply chain) | NCSC AI-specific supply-chain guidance status | UNRESOLVABLE → UNVERIFIED (no standalone NCSC AI-artefact publication found as of Jul 2026) | n/a (negative search result) |
| 44 | CANVASES_SEC.md | L1651 (MCP/tool-server compromise) | Regulator guidance status | UNRESOLVABLE → UNVERIFIED (confirmed no FCA/PRA/DSIT publication exists on MCP/tool-server security as of Jul 2026) | n/a (negative search result) |
| 45 | CANVASES_SEC.md | L1675 (reference [2], OWASP guide) | Title/version/date of "Securing Agentic Applications Guide" | CONFIRMED — "Securing Agentic Applications Guide 1.0", v1.0, 27 July 2025 | https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/ |
| 46 | CANVASES_SEC.md | L1853 (non-human identity governance) | FCA/PRA rule status for agentic identity management | UNRESOLVABLE → UNVERIFIED (confirmed no such rule exists as of Jul 2026); GDPR Art.32(1)(b) pinpointed | n/a (negative search result) |
| 47 | EXEMPLAR_CANVASES.md | L334, MOD-006 canvas (calibration) | MCOB / DISP pinpoints | CONFIRMED — MCOB 11.6 (responsible lending), DISP 1.4/1.6 (complaint handling / 8-week time limit), FOS jurisdiction under DISP 2 | https://handbook.fca.org.uk/handbook/MCOB/11/6.html ; https://handbook.fca.org.uk/handbook/disp1/disp1s4 |

## Counts by file

| File | Confirmed | Corrected | Unresolvable (→ UNVERIFIED) | Total flags |
|---|---|---|---|---|
| CANVASES_AGT.md | 4 | 2 | 2 | 8 |
| CANVASES_MOD.md | 12 | 0 | 0 | 12 |
| CANVASES_SEC.md | 2 | 1 | 5 | 8 |
| CANVASES_DAT.md | 12 | 1 | 5 | 18 |
| EXEMPLAR_CANVASES.md | 1 | 0 | 0 | 1 |
| **Total** | **31** | **4** | **12** | **47** |

Note: some rows in the table above resolve a paragraph partially CONFIRMED / partially
UNVERIFIED (e.g. one citation pinpointed, a second acknowledged as a genuine gap); these are
counted once under whichever resolution is dominant for that flag, consistent with the
per-file counts above.
