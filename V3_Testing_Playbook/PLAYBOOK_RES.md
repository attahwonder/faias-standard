# FAIAS — Component 5 Testing Playbook: RES (Operational Resilience)

**Domain:** RES — Operational Resilience (subdomains G.1–G.4)
**Procedures:** TP-RES-001 … TP-RES-007 (7 of 7; 1:1 with IRQ-RES-001 … IRQ-RES-007)
**Compiled:** 2026-07
**Authority:** CANVASES_RES.md is authoritative on assurance objective, pass/fail/partial interpretation and ★ confidence. This playbook adds execution detail only; where the two appear to conflict, the canvas governs.
**Universal preconditions:** PLAYBOOK_OVERVIEW.md §3 (non-production rule, benign payloads, test-data handling) applies to every procedure below and is not repeated in each sheet.
**Spelling:** UK throughout.

---

## Domain Testing Posture

RES is the most methodologically mature domain in this playbook, because the UK operational resilience regime already mandates the underlying discipline: important business service (IBS) identification, impact tolerance setting, dependency mapping and severe-but-plausible scenario testing under [FCA, Handbook SYSC 15A (esp. 15A.2, 15A.4, 15A.5.1R–15A.5.3R), per PS21/3, March 2021] and [PRA, SS1/21, March 2021]. Every RES procedure is therefore an *extension of an existing, regulator-mandated test discipline to an AI-specific trigger or dependency type* — not a new methodology. That is why RES-001, RES-005 and RES-007 carry ★3 rather than ★1–★2.

Where the extension is genuinely novel — mid-plan agentic termination with in-flight side effects (TP-RES-003), agent-memory rollback (TP-RES-004), and cumulative-drift alert calibration for AI quality metrics (TP-RES-006) — the ★ rating falls to ★2 and this playbook says so plainly. Reviewers must not present ★2 procedures as though they carried the standardisation of the op-res regime that surrounds them.

Two practical consequences for test design:

1. **Reuse the firm's own op-res artefacts as the yardstick.** Impact tolerance values, IBS mapping and the scenario testing library already exist and are board-approved. The reviewer measures AI-specific test results against *the firm's own stated tolerances*, not against an external benchmark. This is what makes RES thresholds unusually concrete relative to CON and GOV.
2. **Exercise, do not read.** The recurring RES failure pattern is a documented capability that has never been performed. Every RES procedure below requires the reviewer to observe an execution (live, staged or replayed), not merely to inspect a plan. Where an execution cannot be obtained, the procedure result is Partial at best, never Pass.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-RES-001: PLAYBOOK_RES_001.md
- TP-RES-002: PLAYBOOK_RES_002.md
- TP-RES-003: PLAYBOOK_RES_003.md
- TP-RES-004: PLAYBOOK_RES_004.md
- TP-RES-005: PLAYBOOK_RES_005.md
- TP-RES-006: PLAYBOOK_RES_006.md
- TP-RES-007: PLAYBOOK_RES_007.md

---
---

## Domain Summary — RES

| Procedure | IRQ | ★ | Reviewer-days | Environment |
|---|---|---|---|---|
| TP-RES-001 Fallback mode exercise | IRQ-RES-001 | ★3 | 4 | Staging replica; the firm's own controlled exercise admissible as evidence |
| TP-RES-002 Partial-failure & stress injection | IRQ-RES-002 | ★2 | 5 | Non-production full stack |
| TP-RES-003 Mid-plan termination | IRQ-RES-003 | ★2 | 5 | Non-production agentic |
| TP-RES-004 Rollback rehearsal | IRQ-RES-004 | ★2 | 4 | Non-production with version control |
| TP-RES-005 Threshold-to-response chain | IRQ-RES-005 | ★3 | 3 | Staging alerting + historical data |
| TP-RES-006 Gradual-decay detection | IRQ-RES-006 | ★2 | 3 | Alerting replica |
| TP-RES-007 Mapping & scenario sweep | IRQ-RES-007 | ★3 | 3 | Documentary |
| **Domain total** | **7 IRQs** | **3×★3, 4×★2** | **27** | — |

**Tier applicability:** RES procedures are out of scope at Tier 0 and are run selectively at Tier 1 (TP-RES-001 and TP-RES-005 as priority procedures). All seven run at Tier 2 and Tier 3; at Tier 3, TP-RES-003 and TP-RES-004 require additional repetitions and L5 post-deployment operational validation. See PLAYBOOK_OVERVIEW.md §5.

**Disclosure requirement:** Four of seven RES procedures carry ★2. Any opinion relying on TP-RES-002, -003, -004 or -006 must state that the conclusion rests on bespoke methodology with professional judgement dominant, per ASSURANCE_MODEL.md §6.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Seven RES procedures derived 1:1 from CANVASES_RES.md; ★ ratings carried over unchanged; no new citations introduced.
v1.1 (2026-08-25) — No procedure changes; document-control block added for uniformity across the nine domain playbooks.
v1.2.1 (2026-09-19) — TP-RES-007: the scenario-completeness step added to IRQ-RES-007's Independent Test reflected in the §1 objective statement and carried into the test design, step 6, the measures table, the Pass and Fail interpretation and the evidence outputs — the library assessment now also confirms at least one scenario in which an important business service is disrupted by externally originated synthetic media, scoped to the firm's own response, communications and impact-tolerance position, not to preventing the fabrication. Step 6 and the evidence outputs count that scenario as the fifth of the five AI-specific types the objective names, and step 6 states that the firm's resistance to the fabrication itself lies outside the standard's scope. The coverage row for the first four types, whose threshold required all four present, now requires the three types the canvas's pass indicator names — provider outage, model behavioural drift and agentic misbehaviour — and records the correlated concentration event as present or absent. The Partial interpretation now applies only where the library holds the synthetic-media scenario the new Fail limb requires. ★3, method classification, preconditions, tier applicability and reviewer-days are unchanged; no new citations introduced.
v1.3.0 (2026-10) — Domain Testing Posture: the SYSC 15A reference for the testing discipline reads 15A.5.1R–15A.5.3R, the testing-plan rule and the scenario-testing rule. TP-RES-001: the method classification cites SYSC 15A.5.3R, the scenario-testing rule, in place of 15A.5.1R; the environment no longer includes a reviewer-run controlled live exercise — the reviewer may observe the firm's own controlled live exercise or take its records as evidence, identified as such under the non-production rule (METHODOLOGY_STANDARDS.md §3), as the canvas's Independent Test now states, and the domain summary table's environment entry for TP-RES-001 reads the same way. ★3, steps, tier applicability and reviewer-days are unchanged.
