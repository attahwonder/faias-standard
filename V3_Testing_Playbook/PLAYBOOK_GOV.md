# FAIAS — Component 5 Testing Playbook: GOV (Governance & Accountability)

**Domain:** GOV — Governance & Accountability
**Procedures:** TP-GOV-001 … TP-GOV-016 (16 of 16; 1:1 with IRQ-GOV-001 … IRQ-GOV-016)
**Compiled:** 2026-07
**Authority:** CANVASES_GOV.md is authoritative on assurance objective, pass/fail/partial interpretation and ★ confidence. This playbook adds execution detail only; where the two appear to conflict, the canvas governs.
**Universal preconditions:** PLAYBOOK_OVERVIEW.md §3 applies to every procedure below and is not repeated in each sheet.
**Spelling:** UK throughout.

---

## Domain Testing Posture

GOV procedures are structured audit programmes. Their methodological foundation is mature — sample tracing, walkthrough, configuration reconciliation, independent re-determination and evidentiary-sufficiency testing are established internal-audit disciplines with decades of practice behind them. What is *not* established is the AI-specific object each is applied to: what constitutes "genuine" rather than nominal ownership of an AI system, what completeness means for an AI inventory that includes shadow and embedded use, what a complete envelope-drift vector set looks like. That split is why nine of the original twelve GOV procedures carry ★3 (credible established audit method, AI-specific adequacy judgement rests on the reviewer) and three carry ★2 (TP-GOV-002 and TP-GOV-006, where the test design itself is bespoke, and TP-GOV-012, where the drift-vector taxonomy is FAIAS-native). With TP-GOV-013 to TP-GOV-016 added, the distribution across sixteen procedures is **9×★3 and 7×★2**.

Four disciplines govern the whole domain:

1. **Sample before you look.** Every GOV procedure draws a risk-based sample weighted to Tier 2–3 systems under TIERING_MODEL.md. The sample basis, size and weighting are recorded before fieldwork begins. A sample selected after the reviewer has formed a view is not evidence.
2. **Independent determination, then comparison.** The strongest GOV procedures (TP-GOV-004, TP-GOV-011, TP-GOV-012) work by having the reviewer independently derive an answer — a tier, an obligation mapping, an effective operating envelope — and only then compare it to the firm's own record. Reading the firm's record first anchors the reviewer to it.
3. **Existence is not operation.** A register, a policy, a threshold, an escalation path or an owner can all exist on paper and never have operated. Every GOV procedure requires at least one piece of evidence that the control has actually *done something*: a decision made, a discovery found, a rejection exercised, a drift detected. Three of the additions carry explicit exemplars — TP-GOV-013's historical trigger activation, TP-GOV-015's historical drift catch, TP-GOV-016's historical flagged-and-traced instance.
4. **GOV depends on GOV-002.** Almost every other procedure in this domain samples from the AI inventory. If the inventory is incomplete, every sample is drawn from a biased frame. TP-GOV-002 is therefore sequenced first in the domain and its result qualifies every subsequent finding. **TP-GOV-014 is the exception among the additions:** it samples the incident taxonomy's category list, not the inventory, and is not qualified by GOV-002's result in the same way.

**Production access.** Most GOV procedures require no production system access at all — they run against governance records, configuration exports, logs and interviews. Three (TP-GOV-003, TP-GOV-012 and TP-GOV-013) include a staging boundary-exercise or demonstration component that must be performed in a staging replica, never against production; TP-GOV-013's cohort-enumeration demonstration runs in test or staging with no production data and no live customer contact. The other three additions — TP-GOV-014, TP-GOV-015 and TP-GOV-016 — require no system access at all.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-GOV-001: PLAYBOOK_GOV_001.md
- TP-GOV-002: PLAYBOOK_GOV_002.md
- TP-GOV-003: PLAYBOOK_GOV_003.md
- TP-GOV-004: PLAYBOOK_GOV_004.md
- TP-GOV-005: PLAYBOOK_GOV_005.md
- TP-GOV-006: PLAYBOOK_GOV_006.md
- TP-GOV-007: PLAYBOOK_GOV_007.md
- TP-GOV-008: PLAYBOOK_GOV_008.md
- TP-GOV-009: PLAYBOOK_GOV_009.md
- TP-GOV-010: PLAYBOOK_GOV_010.md
- TP-GOV-011: PLAYBOOK_GOV_011.md
- TP-GOV-012: PLAYBOOK_GOV_012.md
- TP-GOV-013: PLAYBOOK_GOV_013.md
- TP-GOV-014: PLAYBOOK_GOV_014.md
- TP-GOV-015: PLAYBOOK_GOV_015.md
- TP-GOV-016: PLAYBOOK_GOV_016.md

---
---

## Domain Summary — GOV

| Procedure | IRQ | ★ | Reviewer-days | Sequence note |
|---|---|---|---|---|
| TP-GOV-001 Accountable ownership trace | IRQ-GOV-001 | ★3 | 3 | After GOV-002 |
| TP-GOV-002 Inventory completeness sweep | IRQ-GOV-002 | ★2 | 5 | **First in domain** |
| TP-GOV-003 Conditions-of-use enforcement | IRQ-GOV-003 | ★3 | 4 | Feeds GOV-012 |
| TP-GOV-004 Independent tiering re-score | IRQ-GOV-004 | ★3 | 3 | After GOV-002 |
| TP-GOV-005 Policy suite gap analysis | IRQ-GOV-005 | ★3 | 3 | Independent |
| TP-GOV-006 Risk appetite test | IRQ-GOV-006 | ★2 | 3 | Independent |
| TP-GOV-007 Validation independence review | IRQ-GOV-007 | ★3 | 4 | After GOV-002 |
| TP-GOV-008 Escalation path reconciliation | IRQ-GOV-008 | ★3 | 4 | After TP-RES-005 |
| TP-GOV-009 Documentation answerability | IRQ-GOV-009 | ★3 | 3 | Before GOV-012 |
| TP-GOV-010 Decision reconstruction walkthrough | IRQ-GOV-010 | ★3 | 5 | Independent |
| TP-GOV-011 Obligation mapping re-determination | IRQ-GOV-011 | ★3 | 4 | After GOV-002 |
| TP-GOV-012 Envelope-drift reconciliation | IRQ-GOV-012 | ★2 | 6 | **Last; after 003 and 009** |
| TP-GOV-013 Synthetic-signature cohort enumeration | IRQ-GOV-013 | ★2 | 4 | After GOV-010 |
| TP-GOV-014 AI failure-class coverage in incident taxonomy | IRQ-GOV-014 | ★2 | 3 | After RES-005/006 |
| TP-GOV-015 External capability claim reconciliation | IRQ-GOV-015 | ★2 | 3 | After GOV-009; uses MOD-001 evidence |
| TP-GOV-016 AI content in risk-data aggregation | IRQ-GOV-016 | ★2 | 4 | After GOV-011; uses MOD-004 evidence |
| **Domain total** | **16 IRQs** | **9×★3, 7×★2** | **61** | — |

**Sequence placements for the four additions, assigned at v1.1.0 from the canvas dependency observations.** TP-GOV-013 runs after TP-GOV-010, whose per-decision reconstruction is its precondition. TP-GOV-015 runs after TP-GOV-009, which supplies the documented envelope, and consumes TP-MOD-001's validation evidence. TP-GOV-016 runs after TP-GOV-011 (whether aggregation obligations were mapped as extending to AI content) and consumes TP-MOD-004's accuracy-assurance evidence. TP-GOV-014 runs after TP-RES-005/006 upstream and feeds TP-GOV-008/011 downstream.

**Tier applicability:** GOV is the only domain in scope at Tier 0, where a light-touch subset runs — TP-GOV-001, TP-GOV-002, TP-GOV-005, TP-GOV-009 and TP-GOV-014, at documentary depth with L2 evidence. TP-GOV-014 joined the subset at v1.1.0: it is the only one of the four additions that is purely documentary with no sampling and no staging component, which is the profile the subset shares; TP-GOV-013, TP-GOV-015 and TP-GOV-016 do not join it. All sixteen run at Tiers 1, 2 and 3, with sample sizes and evidence-level expectations scaling per TIERING_MODEL.md. TP-GOV-012 is a Tier 2–3 procedure in full six-vector form; at Tier 1 it runs on vectors V2, V3 and V4 only. See PLAYBOOK_OVERVIEW.md §5.

**Disclosure requirement:** Nine GOV procedures carry ★3 with an explicit professional-judgement caveat on the AI-specific adequacy question; seven carry ★2. Reports must state, per ASSURANCE_MODEL.md §6, that the audit method is established while the AI-specific adequacy judgement rests on the reviewer. TP-GOV-012 additionally requires disclosure that its six-vector drift taxonomy is FAIAS-native rather than externally benchmarked.

All four additions require the ★2 form of words, together with their own disclosures. **TP-GOV-013:** a bespoke capability demonstration with no published protocol and no established sampling frame for cohort-identification completeness. **TP-GOV-014:** one failure class is exercised per walk-through and the residual three are assessed on documentation alone, and testing is scoped to the DORA/SUP 15.3 UK/EU framework. **TP-GOV-015:** the control follows from an enforcement pattern anchored to the incident register, and no UK/EU instrument was identified. **TP-GOV-016** requires an additional disclosure of the same kind as TP-GOV-012's FAIAS-native taxonomy disclosure, though not identical to it: the extension of BCBS 239's principles to AI-originated content is reasoned analogy rather than settled practice, and no provision of the framework or any subsequent instrument extends them explicitly.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Twelve GOV procedures derived 1:1 from CANVASES_GOV.md; ★ ratings carried over unchanged; no new citations introduced.
v1.1 (2026-08-25) — TP-GOV-013 to TP-GOV-016 added, derived 1:1 from their canvases; domain totals move to sixteen procedures and 61 reviewer-days (nine ★3, seven ★2); sequence, Tier 0 and disclosure placements for the four additions assigned at signing.
v1.2.1 (2026-09-19) — TP-GOV-015: the note that the canvas cites the SEC enforcement pattern with no pinpoint given is corrected, the canvas now naming register row 15 and the two settled Investment Advisers Act orders of 18 March 2024, and register row 46 and the FTC's final order against DoNotPay, Inc. (a consent order, allegations neither admitted nor denied). The second limb of that note — that no UK/EU instrument requiring reconciliation between AI-capability claims and a validated capability envelope was identified — is unchanged, as are the procedure, ★2 and the reviewer-day estimate.
