# FAIAS — IRQ ↔ Assurance Claim Matrix

Two-way mapping between the 109 IRQs (IRQ_REGISTER.md) and the 28 assurance claims (CLAIMS_REGISTER.md). The first listed claim is the IRQ's primary claim; further claims receive supporting evidence.

## Table 1 — IRQ → Claims

| IRQ | Claims supported |
|---|---|
| IRQ-DAT-001 | CLM-02 |
| IRQ-DAT-002 | CLM-02, CLM-10 |
| IRQ-DAT-003 | CLM-02, CLM-08 |
| IRQ-DAT-004 | CLM-02, CLM-08 |
| IRQ-DAT-005 | CLM-02, CLM-23 |
| IRQ-DAT-006 | CLM-02, CLM-09 |
| IRQ-DAT-007 | CLM-05, CLM-02 |
| IRQ-DAT-008 | CLM-05 |
| IRQ-DAT-009 | CLM-01 |
| IRQ-DAT-010 | CLM-03, CLM-01 |
| IRQ-DAT-011 | CLM-04, CLM-19 |
| IRQ-DAT-012 | CLM-04, CLM-05 |
| IRQ-DAT-013 | CLM-02, CLM-09 |
| IRQ-DAT-014 | CLM-23, CLM-02 |
| IRQ-MOD-001 | CLM-04 |
| IRQ-MOD-002 | CLM-04, CLM-21 |
| IRQ-MOD-003 | CLM-04 |
| IRQ-MOD-004 | CLM-05 |
| IRQ-MOD-005 | CLM-05, CLM-06 |
| IRQ-MOD-006 | CLM-06 |
| IRQ-MOD-007 | CLM-07 |
| IRQ-MOD-008 | CLM-07 |
| IRQ-MOD-009 | CLM-07, CLM-25 |
| IRQ-MOD-010 | CLM-04 |
| IRQ-MOD-011 | CLM-08 |
| IRQ-MOD-012 | CLM-08, CLM-02 |
| IRQ-MOD-013 | CLM-27 |
| IRQ-MOD-014 | CLM-04 |
| IRQ-MOD-015 | CLM-08 |
| IRQ-MOD-016 | CLM-08, CLM-04 |
| IRQ-AGT-001 | CLM-12 |
| IRQ-AGT-002 | CLM-12 |
| IRQ-AGT-003 | CLM-12 |
| IRQ-AGT-004 | CLM-12, CLM-01 |
| IRQ-AGT-005 | CLM-12, CLM-11 |
| IRQ-AGT-006 | CLM-14 |
| IRQ-AGT-007 | CLM-14 |
| IRQ-AGT-008 | CLM-03 |
| IRQ-AGT-009 | CLM-27 |
| IRQ-AGT-010 | CLM-14, CLM-13 |
| IRQ-AGT-011 | CLM-13, CLM-25 |
| IRQ-AGT-012 | CLM-12, CLM-18 |
| IRQ-AGT-013 | CLM-12, CLM-18 |
| IRQ-AGT-014 | CLM-12, CLM-13 |
| IRQ-HUM-001 | CLM-15 |
| IRQ-HUM-002 | CLM-15 |
| IRQ-HUM-003 | CLM-16 |
| IRQ-HUM-004 | CLM-15, CLM-13 |
| IRQ-HUM-005 | CLM-15, CLM-19 |
| IRQ-HUM-006 | CLM-25, CLM-15 |
| IRQ-HUM-007 | CLM-15, CLM-17 |
| IRQ-HUM-008 | CLM-17 |
| IRQ-HUM-009 | CLM-17, CLM-25 |
| IRQ-SEC-001 | CLM-09 |
| IRQ-SEC-002 | CLM-09 |
| IRQ-SEC-003 | CLM-09 |
| IRQ-SEC-004 | CLM-09, CLM-12 |
| IRQ-SEC-005 | CLM-09, CLM-02 |
| IRQ-SEC-006 | CLM-10 |
| IRQ-SEC-007 | CLM-10 |
| IRQ-SEC-008 | CLM-10, CLM-01 |
| IRQ-SEC-009 | CLM-11 |
| IRQ-SEC-010 | CLM-11, CLM-12 |
| IRQ-SEC-011 | CLM-01, CLM-12 |
| IRQ-SEC-012 | CLM-09, CLM-24 |
| IRQ-SEC-013 | CLM-09, CLM-19 |
| IRQ-SEC-014 | CLM-09, CLM-11 |
| IRQ-TPR-001 | CLM-22 |
| IRQ-TPR-002 | CLM-22, CLM-21 |
| IRQ-TPR-003 | CLM-26, CLM-22 |
| IRQ-TPR-004 | CLM-21 |
| IRQ-TPR-005 | CLM-11, CLM-22 |
| IRQ-TPR-006 | CLM-22, CLM-19 |
| IRQ-TPR-007 | CLM-10, CLM-22 |
| IRQ-TPR-008 | CLM-22, CLM-20 |
| IRQ-TPR-009 | CLM-22, CLM-20 |
| IRQ-RES-001 | CLM-20 |
| IRQ-RES-002 | CLM-18 |
| IRQ-RES-003 | CLM-18, CLM-19 |
| IRQ-RES-004 | CLM-19 |
| IRQ-RES-005 | CLM-19 |
| IRQ-RES-006 | CLM-19 |
| IRQ-RES-007 | CLM-20 |
| IRQ-CON-001 | CLM-23 |
| IRQ-CON-002 | CLM-23 |
| IRQ-CON-003 | CLM-24 |
| IRQ-CON-004 | CLM-24, CLM-05 |
| IRQ-CON-005 | CLM-23, CLM-24 |
| IRQ-CON-006 | CLM-23, CLM-24 |
| IRQ-CON-007 | CLM-23 |
| IRQ-CON-008 | CLM-24, CLM-17 |
| IRQ-CON-009 | CLM-24, CLM-23 |
| IRQ-CON-010 | CLM-24, CLM-17, CLM-23 |
| IRQ-GOV-001 | CLM-26 |
| IRQ-GOV-002 | CLM-26 |
| IRQ-GOV-003 | CLM-27, CLM-26 |
| IRQ-GOV-004 | CLM-26 |
| IRQ-GOV-005 | CLM-26 |
| IRQ-GOV-006 | CLM-26 |
| IRQ-GOV-007 | CLM-08, CLM-26 |
| IRQ-GOV-008 | CLM-19, CLM-26 |
| IRQ-GOV-009 | CLM-25, CLM-26 |
| IRQ-GOV-010 | CLM-25 |
| IRQ-GOV-011 | CLM-26 |
| IRQ-GOV-012 | CLM-04, CLM-27 |
| IRQ-GOV-013 | CLM-25, CLM-17 |
| IRQ-GOV-014 | CLM-26, CLM-19 (cross-reference: a silent bias event under IRQ-GOV-014 also bears on CLM-23 at assessment) |
| IRQ-GOV-015 | CLM-26, CLM-08 |
| IRQ-GOV-016 | CLM-28, CLM-25 |

## Table 2 — Claim → IRQs (reverse index)

| Claim | Supporting IRQs | Count |
|---|---|---|
| CLM-01 Authorised information only | IRQ-DAT-009, IRQ-DAT-010, IRQ-AGT-004, IRQ-SEC-008, IRQ-SEC-011 | 5 |
| CLM-02 Fit and lawful data | IRQ-DAT-001, -002, -003, -004, -005, -006, -007, -013, -014; IRQ-MOD-012; IRQ-SEC-005 | 11 |
| CLM-03 Memory and context integrity | IRQ-DAT-010, IRQ-AGT-008 | 2 |
| CLM-04 Envelope-consistent behaviour | IRQ-DAT-011, IRQ-DAT-012, IRQ-MOD-001, -002, -003, -010, -014, -016, IRQ-GOV-012 | 9 |
| CLM-05 Evidence-grounded outputs | IRQ-DAT-007, IRQ-DAT-008, IRQ-DAT-012, IRQ-MOD-004, IRQ-MOD-005, IRQ-CON-004 | 6 |
| CLM-06 Reliable expressed confidence | IRQ-MOD-005, IRQ-MOD-006 | 2 |
| CLM-07 Intent-aligned optimisation | IRQ-MOD-007, IRQ-MOD-008, IRQ-MOD-009 | 3 |
| CLM-08 Trustworthy evaluation evidence | IRQ-DAT-003, IRQ-DAT-004, IRQ-MOD-011, IRQ-MOD-012, IRQ-MOD-015, IRQ-MOD-016, IRQ-GOV-007, IRQ-GOV-015 | 8 |
| CLM-09 Adversarial resistance | IRQ-DAT-006, IRQ-DAT-013, IRQ-SEC-001, -002, -003, -004, -005, -012, -013, -014 | 10 |
| CLM-10 No confidential leakage | IRQ-DAT-002, IRQ-SEC-006, IRQ-SEC-007, IRQ-SEC-008, IRQ-TPR-007 | 5 |
| CLM-11 Component integrity | IRQ-AGT-005, IRQ-SEC-009, IRQ-SEC-010, IRQ-SEC-014, IRQ-TPR-005 | 5 |
| CLM-12 Bounded agency | IRQ-AGT-001, -002, -003, -004, -005, -012, -013, -014; IRQ-SEC-004, -010, -011 | 11 |
| CLM-13 Observable agency | IRQ-AGT-010, IRQ-AGT-011, IRQ-AGT-014, IRQ-HUM-004 | 4 |
| CLM-14 Controlled delegation | IRQ-AGT-006, IRQ-AGT-007, IRQ-AGT-010 | 3 |
| CLM-15 Genuine human oversight | IRQ-HUM-001, -002, -004, -005, -006, -007 | 6 |
| CLM-16 Sustained human competence | IRQ-HUM-003 | 1 |
| CLM-17 Contestable decisions | IRQ-HUM-007, IRQ-HUM-008, IRQ-HUM-009, IRQ-CON-008, IRQ-CON-010, IRQ-GOV-013 | 6 |
| CLM-18 Fails safely | IRQ-AGT-012, IRQ-AGT-013, IRQ-RES-002, IRQ-RES-003 | 4 |
| CLM-19 Detectable and recoverable malfunction | IRQ-DAT-011, IRQ-HUM-005, IRQ-TPR-006, IRQ-RES-003, -004, -005, -006, IRQ-SEC-013, IRQ-GOV-008, IRQ-GOV-014 | 10 |
| CLM-20 Service continuity | IRQ-TPR-008, IRQ-TPR-009, IRQ-RES-001, IRQ-RES-007 | 4 |
| CLM-21 No silent vendor alteration | IRQ-MOD-002, IRQ-TPR-002, IRQ-TPR-004 | 3 |
| CLM-22 Managed third-party dependency | IRQ-TPR-001, -002, -003, -005, -006, -007, -008, -009 | 8 |
| CLM-23 Fair outcomes across groups | IRQ-DAT-005, IRQ-DAT-014, IRQ-CON-001, -002, -005, -006, -007, -009, -010 | 9 |
| CLM-24 Informed and protected customers | IRQ-CON-003, -004, -005, -006, -008, -009, -010, IRQ-SEC-012 | 8 |
| CLM-25 Reconstructable decisions | IRQ-MOD-009, IRQ-AGT-011, IRQ-HUM-006, IRQ-HUM-009, IRQ-GOV-009, IRQ-GOV-010, IRQ-GOV-013, IRQ-GOV-016 | 8 |
| CLM-26 Complete and accountable governance | IRQ-TPR-003, IRQ-GOV-001, -002, -003, -004, -005, -006, -007, -008, -009, -011, -014, -015 | 13 |
| CLM-27 Controlled behavioural change | IRQ-MOD-013, IRQ-AGT-009, IRQ-GOV-003, IRQ-GOV-012 | 4 |
| CLM-28 Regulatory-reporting integrity | IRQ-GOV-016 | 1 |

## Verification — no-orphan check

- **IRQ coverage:** 109 of 109 IRQs map to ≥1 claim (Table 1 has 109 rows; every row lists at least one claim). Orphan IRQs: **0**.
- **Claim coverage:** 28 of 28 claims are supported by ≥1 IRQ (Table 2; minimum support is CLM-16 and CLM-28 with 1 IRQ each). Orphan claims: **0**.
- Table 1 mapping entries total 169; Table 2 reverse-index entries total 169 — the two directions reconcile. (The CLM-23 cross-reference on IRQ-GOV-014 is an assessment note, not a mapping entry, and is excluded from the count.)
- **Gap closed, 25 August 2026:** IRQ-GOV-016 now maps to the dedicated CLM-28 (regulatory-reporting integrity) as primary claim, with CLM-25 retained as secondary support for the reconstruction/traceability overlap. CLM-08 is dropped from this mapping as no longer the closest available substitute.
- Note: CLM-16, CLM-28 (single-IRQ support) and CLM-03/CLM-06 (two IRQs each) are flagged as thin-evidence claims: an opinion on these rests on few IRQs, so their canvases warrant priority depth in Phase 3.
