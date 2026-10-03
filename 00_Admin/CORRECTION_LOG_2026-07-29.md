# Correction pass — 29 July 2026

Independent re-verification of the standard's regulatory pinpoints against primary sources, following an audit that found a systematic pattern: correct documents, plausible-sounding section numbers, wrong locations — with several recorded as CONFIRMED in the verification logs.

**104 edits applied.** Every correction below was checked against the primary source before it was made, not accepted from the audit report.

---

## 1. EBA Guidelines on outsourcing arrangements (EBA/GL/2019/02)

The section structure was wrong in every place it was cited. Verified against the published Guidelines.

| Cited as | Actual |
|---|---|
| Title II, Section 5 — pre-outsourcing assessment | **Title IV, Section 12 — Pre-outsourcing analysis**, incl. 12.3 Due diligence |
| Section 11 — criticality assessment | **Title II, Section 4 — Critical or important functions** |
| Title II, Section 13 — outsourcing agreement | **Title IV, Section 13 — Contractual phase**, incl. 13.3 access/audit rights, 13.4 termination |

Sections 5 and 11 are *Sound governance arrangements and third-party risk* and *Documentation requirements*, both in Title III. A third-party opinion citing the original mapping would have pointed a supervisor at the wrong obligations.

## 2. PRA SS1/23 — Principle 5 used as a catch-all

Verified: the five principles are (1) model identification and risk classification, (2) governance, (3) model development, implementation and use, (4) independent model validation, (5) model risk mitigants.

Monitoring and change control were repeatedly attributed to Principle 5. **Principle 5 contains neither.** Monitoring and review of model changes sit under Principle 4; restriction and withdrawal outcomes then engage Principle 5. Corrected in seven canvas locations across DAT, MOD, GOV and TPR, and in five verification-log rows.

*Note on discipline:* the audit proposed a sub-clause pinpoint (§4.4) for monitoring. I could not confirm the sub-clause against the primary text, so the corrections cite the principle and its title only. Asserting an unverified pinpoint is the error being fixed.

## 3. PRA SS1/23 — two further corrections

- **Currency.** The register treated the May 2023 version as current. SS1/23 was amended by **LIAF01/26, published and effective 23 April 2026**. Register updated.
- **Vendor models.** A verification-log row recorded as "unresolvable" that SS1/23 does not address vendor models, treating applicability as a FAIAS extension. The PRA states the principles apply to models whether developed in-house or externally, **including vendor models**. A false negative that weakened the standard unnecessarily. Corrected, with only the AI-specific application still flagged as an extension.

## 4. EU AI Act timeline

The regulatory register still asserted Annex III high-risk obligations from **2 August 2026**, with "the binding-compliance clock now running" — while the standard's own verification log correctly recorded the postponement. The register was compiled the day after the Digital Omnibus entered into force and was never reconciled.

Corrected to: **Annex III high-risk postponed to 2 December 2027** by the Digital Omnibus, Regulation (EU) 2026/1744, in force 27 July 2026. Two GOV canvases carrying the superseded date also corrected.

**One audit finding rejected.** The audit claimed the standard was wrong to say Article 50 transparency still applies from 2 August 2026. On checking, that is right: Article 50 was not deferred. The only refinement needed is the transitional window — **Art 50(2) marking for systems placed on the market before 2 August 2026 applies from 2 December 2026** — which has been added in the two places the claim appears.

## 5. Dates, titles and flags

- Commission GPAI scope guidelines: **18 July 2025**, not 24 July (24 July was a commentary date).
- BoE/FCA survey title: **"Artificial intelligence in UK financial services – 2024", 21 November 2024** — the series was renamed from "Machine learning in UK financial services".
- Prohibited-practices guidelines **C(2025) 884 final, 4 February 2025** — `[UNVERIFIED]` flag cleared; confirmable on a single search.
- **OWASP Securing Agentic Applications Guide v1.0, 27 July 2025** — flag cleared; the verification log had already confirmed it but the register was never updated.
- Obsolete project name **FAIRM** replaced with FAIAS throughout — 67 occurrences, including six in a client-facing canvas file.

## 6. Verification-log integrity

Ten rows across Logs A and B recorded "CONFIRMED" against pinpoints that are wrong, and one recorded "unresolvable" against a provision that exists. All have been restated as corrected, with the right position given.

This matters beyond the individual citations. A verification log that launders unchecked assertions into confirmed ones is worse than no log, because it transfers unearned confidence to everyone downstream — and it is precisely the failure mode this standard exists to detect in others.

---

## Recommended, not applied — for the owner's decision

**Testing Confidence on four Conduct canvases.** IRQ-CON-003, -005, -006 and -008 are rated ★2, whose anchor requires published research showing the harm is plausible. Each one's own Research Basis records that no research was located; the rating rests on regulatory material instead. On the standard's own anchors these are **★1**.

This is a judgement on the standard rather than a factual correction, so it has not been applied. Two ways to resolve it: downgrade the four, or add an anchor dimension for **established professional and regulatory practice** — which would also fix a wider issue, since roughly 27 GOV, RES and TPR canvases currently rate audit and compliance procedures on a scale defined purely in terms of research maturity.

**Also outstanding:** IRQ-MOD-009 and IRQ-AGT-007 are rated ★2 while sitting alongside the model's own canonical ★1 examples; the TPR and RES independent tests are the weakest in the battery and read as nested document review; and 73 residual `[UNVERIFIED]` tags remain as disclosed debt.

---

*Corrections verified and applied 29 July 2026.*

---

## Addendum · 25 August 2026

Two rows above record flags as "cleared" that the register, correctly, still carries: the C(2025) 884 row and the OWASP Securing Agentic Applications Guide row each retain an [UNVERIFIED — …] marker in `V5_Regulatory_Crosswalk/SOURCE_REGISTER_REGULATORY.md`, narrowed but not removed, because the residual point (the document number itself; the exact incremental version) was not independently confirmed. The register's standing flags are the accurate state; this log's "cleared" wording overstated the correction. Found by the 25 August 2026 post-signing audit; recorded here as a dated addendum per the history convention.
