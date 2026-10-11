# FAIAS — Testing Playbook: MOD (Model) Domain

**Component:** V3 Testing Playbook
**Domain:** MOD — Model (subdomains B.1–B.7)
**Procedures:** TP-MOD-001 … TP-MOD-016 (16, 1:1 with IRQ-MOD-001 … IRQ-MOD-016)
**Source canvases:** `V2_IRQ_Battery/canvases/CANVASES_MOD.md` (15 canvases) and `V2_IRQ_Battery/EXEMPLAR_CANVASES.md` Canvas 2 (IRQ-MOD-006)
**Governing documents:** `00_Admin/ASSURANCE_MODEL.md` (★ anchors, L1–L5 evidence levels), `00_Admin/METHODOLOGY_STANDARDS.md` (source hierarchy, testing-method labelling, non-production rule)
**Compiled:** 2026-07
**Spelling:** UK throughout

---

## Domain Testing Overview

### Purpose and scope of this playbook

Each procedure expands the summary-level Independent Test in the corresponding Review Canvas into an executable sheet. **★ confidence ratings are carried over unchanged from the canvases** — six procedures at ★3 (MOD-004, 005, 006, 010, 011, 015) and ten at ★2. No MOD procedure reaches ★4 or ★5, and none is inflated to match the tone of the exemplar. Where the canvas cites a methodology, the procedure names it; where the canvas records that no benchmark exists, the measure is labelled *reviewer judgement — no established threshold* per METHODOLOGY_STANDARDS §3. **No new citations are introduced.**

Note on IRQ-MOD-006: its canvas is maintained in `EXEMPLAR_CANVASES.md` (Canvas 2), not in `CANVASES_MOD.md`. TP-MOD-006 derives from the exemplar and carries its ★3 rating.

### Non-production rule (applies to all sixteen procedures)

Per METHODOLOGY_STANDARDS §3, every procedure executes **only in a development, test or staging environment isolated from production**. Model calls use non-production API keys or staging endpoints; no live customer data, no production traffic, no production retraining, no production configuration changes. Where a procedure requires realistic cases, the reviewer uses synthetic, anonymised or historical non-live case files approved for test use. Anything that cannot be tested without production access is recorded as *not testable in scope* and reported as an evidence gap.

### Shared test-environment setup (build once, reuse across MOD)

MOD is the most economical domain to instrument: thirteen of the sixteen procedures run against the same staging pipeline with different case sets — eleven of the original thirteen, joined by TP-MOD-014, which requires the staging replica with its decision-extraction layer, and by TP-MOD-016, whose paired-framing limb runs the firm's own task set against the replica at a pinned configuration. TP-MOD-015's object is the judge model rather than the pipeline, so it sits outside the count; TP-MOD-016's remaining limbs are documentation review and analysis of records the firm already holds.

| Component | Purpose | Used by |
|---|---|---|
| **Full staging replica of the deployed pipeline** (prompt templates, retrieval, model endpoint, post-processing, workflow gating) — not a bare model endpoint. For TP-MOD-014 the replica must include the **decision-extraction layer** (parsing, classification, schema validation), which that procedure tests as a component rather than as plumbing; a bare model endpoint cannot run it | The failure modes in this domain frequently live in the surrounding pipeline, not the model | Nearly all; TP-MOD-014 specifically requires the extraction layer |
| **Version-pinned model access**, plus access to at least one alternate version | Capability-delta and configuration-change testing | TP-MOD-002, 013 |
| **Historical output archive** for a fixed prompt set | Where the vendor does not permit version selection | TP-MOD-002 |
| **Ground-truth case library** — synthetic/anonymised FS cases with documented correct outcomes, structured by task type | Almost every measurement procedure | TP-MOD-001, 003, 004, 005, 006, 007, 009, 010, 012 |
| **Perturbation harness** — programmatically removes/alters/injects evidence in a case file and re-runs the pipeline | Calibration, faithfulness and shift testing | TP-MOD-005, 006, 009, 010 |
| **Independent evaluator pool** (human raters and/or a scoring model) with **no connection to any reward model used in fine-tuning** | Avoiding circular validation | TP-MOD-004, 008, 015 |
| **Regression suite runner** with retained pass/fail criteria | Release and configuration governance | TP-MOD-002, 013 |
| **Deployment-pathway inventory** (every route by which a prompt or parameter can change) | Governance-bypass testing | TP-MOD-013 |
| **Evidence store** (write-once or checksum-controlled) | All | All |

**Determinism discipline (applies throughout):** record the decoding configuration (temperature, top-p, seed where available) for every run, and hold it fixed within a procedure. Where the endpoint is non-deterministic, use a fixed repetition count per case and report the variance. Failing to do this is the single most common source of uninterpretable MOD results. **In TP-MOD-014 the same discipline serves the opposite purpose:** run-to-run variance is the object of study rather than a nuisance to be controlled for, so the configuration is pinned and held not to suppress variance but to make what remains attributable.

### Sequencing advice

**Wave 1 — establish what is being tested and against what.** TP-MOD-011 (evaluation-evidence contamination) runs **first**. If the evaluation evidence underpinning approval is contaminated, every downstream performance measure is being compared against a compromised baseline. TP-MOD-002 (capability delta) runs alongside it to establish which model version is actually in scope — testing the wrong version is a wasted engagement.

**Wave 2 — boundaries and behaviour.** TP-MOD-001 (capability envelope) defines the strata the later procedures reuse. Then TP-MOD-004 (hallucination rate), TP-MOD-005 (epistemic-state discrimination) and TP-MOD-006 (calibration). These three are deeply complementary: MOD-004 asks *how often does it fabricate*, MOD-005 asks *does it distinguish the reasons it might not know*, MOD-006 asks *does its expressed confidence track its accuracy as evidence degrades*. Run them as a single campaign on a shared case library.

**Wave 3 — reasoning and incentives.** TP-MOD-003 (multi-constraint degradation), TP-MOD-009 (chain-of-thought faithfulness), TP-MOD-007 (specification gaming), TP-MOD-008 (reward hacking). TP-MOD-003 and TP-MOD-009 share the constraint-annotated case set. TP-MOD-007 and TP-MOD-008 share the independent-evaluator pool.

**Wave 4 — robustness and change control.** TP-MOD-010 (six shift types), TP-MOD-012 (recursive collapse), TP-MOD-013 (prompt/parameter change control). TP-MOD-013 is best run late, because by then the reviewer knows which prompt elements are behaviourally load-bearing and can select a meaningful test change rather than an arbitrary one.

TP-MOD-015 runs in wave 1, alongside TP-MOD-011 — its own canvas names it the evaluator-side twin — and **TP-MOD-016 runs in the same wave with both**, the three forming the evaluation-evidence-integrity set: what the evidence contains (011), who scored it (015) and what setting produced it (016). TP-MOD-014 runs in wave 4, with TP-MOD-013 — its canvas names TP-MOD-013 as its pair, a pinned configuration being the baseline TP-MOD-014 measures against and TP-MOD-013 covering what happens when the pin moves.

**Cross-domain:** TP-MOD-011 pairs naturally with TP-DAT-004 (synthetic fidelity) and TP-DAT-003 (label quality) — all three attack the reliability of the evidence behind an accuracy claim, and a single reviewer holding all three produces a far stronger combined finding. TP-MOD-012 shares its collapse-mechanism grounding with TP-DAT-004 and its feedback-path inventory with TP-DAT-013; do not build that inventory twice.

### Cross-IRQ dataset reuse opportunities

1. **Ground-truth case library** — one library of representative FS cases with documented correct outcomes serves TP-MOD-001, 003, 004, 005, 006, 007, 009, 010 and 012. Build it once, annotate it progressively: add constraint annotations for MOD-003/009, epistemic-state variants for MOD-005/006, rare-event tagging for MOD-012.
2. **Perturbed variant sets (TP-MOD-006)** — the evidence-removed, conflicting-evidence and unanswerable variants built for calibration testing are, with minor extension, the five epistemic-state sets required by TP-MOD-005 (add an ambiguous-question set) and the perturbation basis for TP-MOD-009.
3. **Capability strata (TP-MOD-001)** — the core/adjacent/out-of-scope strata are directly reusable as the temporal and population shift conditions in TP-MOD-010 and as the "outside the tested envelope" cases in TP-MOD-003.
4. **Fixed regression prompt suite** — one suite serves TP-MOD-002 (vendor version delta) and TP-MOD-013 (firm configuration delta). These are the same measurement applied to two different change sources; build one instrument.
5. **Rare-event/minority-subgroup test set (TP-MOD-012)** — reusable as the tail-performance probe in TP-MOD-010's population-shift condition and as the real-holdout comparator in TP-DAT-004.
6. **Independent evaluator pool** — the same raters, briefed once on the firm's domain, serve TP-MOD-004 severity classification, TP-MOD-007 outcome-quality scoring, TP-MOD-008 sycophancy scoring and TP-MOD-015's human-agreement study. Their independence from the fine-tuning reward signal must be documented once and relied on throughout. **TP-MOD-015 requires a wider independence condition than the others:** independence must also run to the team that selected the judge model, which is not established by the pool's existing documentation and must be confirmed separately.

### Domain-level evidence maturity caveat (state in every MOD report)

MOD divides cleanly. Measurement of hallucination, calibration, epistemic-state discrimination, distribution shift and benchmark contamination rests on peer-reviewed methods used by multiple independent research groups — ★3, credible but with no canonical FS benchmark, so thresholds and severity classification rest on professional judgement. LLM-as-judge validation joins the ★3 group on the same basis: a peer-reviewed, widely cited measurement method exists, and the acceptance threshold does not. Everything concerning capability envelopes, specification gaming, reward hacking, reasoning faithfulness, recursive collapse in the firm's own pipeline, configuration change control, and decision-flip-rate measurement at pinned configuration is ★2 — the harm mechanism is well evidenced in research, but test design is bespoke and assessor judgement dominates. All ★2 conclusions carry the judgement-based labelling required by METHODOLOGY_STANDARDS §3c.

### Indicative total effort

**72 reviewer-days** across the sixteen procedures, excluding environment build (allow 5–8 reviewer-days for first-time staging pipeline and case-library establishment) and non-reviewer support effort.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-MOD-001: PLAYBOOK_MOD_001.md
- TP-MOD-002: PLAYBOOK_MOD_002.md
- TP-MOD-003: PLAYBOOK_MOD_003.md
- TP-MOD-004: PLAYBOOK_MOD_004.md
- TP-MOD-005: PLAYBOOK_MOD_005.md
- TP-MOD-006: PLAYBOOK_MOD_006.md
- TP-MOD-007: PLAYBOOK_MOD_007.md
- TP-MOD-008: PLAYBOOK_MOD_008.md
- TP-MOD-009: PLAYBOOK_MOD_009.md
- TP-MOD-010: PLAYBOOK_MOD_010.md
- TP-MOD-011: PLAYBOOK_MOD_011.md
- TP-MOD-012: PLAYBOOK_MOD_012.md
- TP-MOD-013: PLAYBOOK_MOD_013.md
- TP-MOD-014: PLAYBOOK_MOD_014.md
- TP-MOD-015: PLAYBOOK_MOD_015.md
- TP-MOD-016: PLAYBOOK_MOD_016.md

---
---

## Effort Summary — MOD Domain

| Procedure | IRQ | ★ | Reviewer-days |
|---|---|---|---|
| TP-MOD-001 | IRQ-MOD-001 Capability envelope | ★2 | 4 |
| TP-MOD-002 | IRQ-MOD-002 Capability delta on release | ★2 | 3 |
| TP-MOD-003 | IRQ-MOD-003 Multi-constraint degradation | ★2 | 4 |
| TP-MOD-004 | IRQ-MOD-004 Hallucination rate | ★3 | 6 |
| TP-MOD-005 | IRQ-MOD-005 Epistemic-state discrimination | ★3 | 5 |
| TP-MOD-006 | IRQ-MOD-006 Calibration (exemplar canvas) | ★3 | 5 |
| TP-MOD-007 | IRQ-MOD-007 Specification gaming | ★2 | 4 |
| TP-MOD-008 | IRQ-MOD-008 Reward hacking | ★2 | 4 |
| TP-MOD-009 | IRQ-MOD-009 CoT faithfulness | ★2 | 5 |
| TP-MOD-010 | IRQ-MOD-010 Six-type shift robustness | ★3 | 6 |
| TP-MOD-011 | IRQ-MOD-011 Evaluation contamination | ★3 | 4 |
| TP-MOD-012 | IRQ-MOD-012 Recursive collapse | ★2 | 5 |
| TP-MOD-013 | IRQ-MOD-013 Prompt/parameter change control | ★2 | 3 |
| TP-MOD-014 | IRQ-MOD-014 Decision-flip rate at pinned config | ★2 | 4 |
| TP-MOD-015 | IRQ-MOD-015 LLM-as-judge validation | ★3 | 5 |
| TP-MOD-016 | IRQ-MOD-016 External validity of pre-deployment evidence | ★2 | 5 |
| **Total** | **16 procedures** | — | **72 reviewer-days** |

Excludes first-time staging pipeline and case-library build (5–8 reviewer-days, largely reusable) and non-reviewer support effort (evaluators, annotators, ML and platform engineers, compute), costed separately.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Thirteen MOD procedures derived 1:1 from CANVASES_MOD.md (twelve) and EXEMPLAR_CANVASES.md Canvas 2 (IRQ-MOD-006); ★ ratings carried over unchanged; no new citations introduced.
v1.1 (2026-08-25) — TP-MOD-014 (pinned-configuration decision-flip rate and extraction-layer isolation) and TP-MOD-015 (LLM-as-judge validation) added, derived 1:1 from the IRQ-MOD-014 and IRQ-MOD-015 canvases; subdomains extend to B.7 (Output Stability & Determinism); domain totals move to fifteen procedures and 67 reviewer-days; ★ distribution becomes six ★3 and nine ★2.
v1.2 (2026-09-12) — TP-MOD-016 (evaluation-to-deployment external validity) added, derived 1:1 from the IRQ-MOD-016 canvas; ★2 carried over unchanged; domain totals move to sixteen procedures and 72 reviewer-days; ★ distribution becomes six ★3 and ten ★2. No new citations introduced beyond those carried on the canvas.
v1.3.2 (2026-10-03) — TP-MOD-002's call to the vendor's latest version stated under the non-production rule (METHODOLOGY_STANDARDS.md §3; 00_Admin/CORRECTION_LOG_2026-10-03.md §8). No ★ rating or reviewer-day figure changes.
v1.3.3 (2026-10-09) — TP-MOD-014's ★ summary, method classification and carried limitation brought into line with the canvas: two published repeat-run methods, both workshop papers, replace the statement that no published methodology exists, with their limits. No ★ rating or reviewer-day figure changes.
