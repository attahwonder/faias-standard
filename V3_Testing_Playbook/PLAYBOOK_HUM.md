# FAIAS — Testing Playbook: HUM (Human Oversight) Domain

**Volume:** V3 Testing Playbook (Component 5)
**Scope:** Nine executable test procedures, TP-HUM-001 to TP-HUM-009, one per IRQ in `V2_IRQ_Battery/canvases/CANVASES_HUM.md`.
**Document Custodian:** the maintainer
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.
**UK spelling throughout.**

---

## Domain Testing Overview (one page)

### What this playbook does

HUM procedures are **behavioural studies**, not technical tests. The object under examination is not the model but the human system wrapped around it: whether reviewers actually discriminate, whether approval is substantive, whether unaided competence survives, whether the intervention point is where it needs to be, whether suspension authority would actually be exercised, whether accountability is traceable, whether explanations do work, and whether a contest route re-derives rather than re-runs. Each procedure below expands the field 11 *Independent Test* of its canvas into a runnable study design. Assurance objectives, ★ ratings and pass/fail/partial indicators are carried across **unchanged**.

**One procedure departs from that description and does so deliberately.** TP-HUM-009 is a documentation and case-file review, not a behavioural study: it requires no participant cohort, no blinding and no deception, and the domain's research-participant rules engage only where case handlers are interviewed. Where the rules below are stated domain-wide, read them as excluding TP-HUM-009 except as noted.

### Non-negotiable operating rules

1. **No live customer decisions, ever.** Every procedure runs on de-identified dev/test case files, replayed historical data, simulation, or reviewer exercises. No procedure alters, delays, or influences a real decision affecting a real customer or colleague. Where a procedure analyses historical production data (TP-HUM-002's override-trend and refusal-durability limbs, TP-HUM-004's sign-off-ordering limb), it is **read-only retrospective analysis** of data already generated — no intervention.
2. **Human participants are research participants.** These studies involve the firm's staff. Before any procedure involving staff participation runs, the reviewer secures: informed consent covering purpose and data use; a written non-punitive assurance from the sponsoring executive that individual results will not feed performance management; anonymisation or pseudonymisation of individual-level results in all outputs; and, where the firm has an ethics, HR or works-council process for staff research, clearance through it. Individual-level data is reported only in aggregate. **TP-HUM-009 has no participant cohort;** this rule engages for it only where investigating managers or case handlers are interviewed.
3. **Blinding where the design requires it.** Seeded-error studies (TP-HUM-001, -007, -008) are invalid if participants know which cases are seeded. Blinding arrangements are agreed with the firm in writing and the reviewer holds the key. **TP-HUM-009 requires no blinding.**
4. **Deception is bounded and debriefed.** Several designs require participants not to know the full purpose in advance (seeded errors; the unannounced scenario in TP-HUM-005). This is standard behavioural-research practice and is bounded: participants are told a study is happening, are debriefed fully afterwards, and the debrief is a required step in each procedure, not an optional courtesy. **TP-HUM-009 involves no deception and therefore carries no debrief obligation arising from one.**
5. **Realism is the whole game.** A seeded-error study run without time pressure, or a competency assessment run with generous deadlines, measures a workflow that does not exist. Each design specifies the realism conditions that must hold.
6. **Honest confidence.** ★ ratings are carried from the canvases. Five of the nine HUM procedures are ★2 — bespoke designs on established foundations — and one is ★1. Results must be reported as professional assessment, not standardised evidence, per METHODOLOGY_STANDARDS.md §3c. **The ★1 is the domain's first** (TP-HUM-009), and any conclusion resting on it carries the ★1 form of words required by PLAYBOOK_OVERVIEW.md §8: "This conclusion rests on ★1 methodology — the harm mechanism is theoretically plausible and the testing approach is novel and unvalidated. Result quality depends entirely on assessor expertise. This is expert opinion, not evidence."

### Confidence and method-class distribution

| Procedure | Subdomain | ★ (carried) | Method class (METHODOLOGY_STANDARDS §3) |
|---|---|---|---|
| TP-HUM-001 Automation bias / seeded errors | D.1 | ★3 | Adapted Industry Practice (Skitka et al. 1999/2000; Goddard et al. 2012) |
| TP-HUM-002 Approval theatre | D.1 | ★3 | Adapted Industry Practice (human-factors dwell-time/workload analysis) |
| TP-HUM-003 Skill atrophy | D.2 | ★3 | Adapted Industry Practice (Arthur et al. 1998 skill-retention framework) |
| TP-HUM-004 Intervention point position | D.3 | ★2 | Emerging Practice (process-engineering/queuing concepts, bespoke application) |
| TP-HUM-005 Suspension authority | D.3 | ★2 | Emerging Practice (crisis-simulation / safety-culture assessment) |
| TP-HUM-006 Accountability tracing | D.4 | ★2 | Emerging Practice (internal-audit trace sampling, extended) |
| TP-HUM-007 Explanation adequacy | D.4 | ★2 | Emerging Practice (Doshi-Velez & Kim human-grounded evaluation) |
| TP-HUM-008 Contest route | D.4 | ★2 | Emerging Practice (seeded-error paradigm adapted to appeals) |
| TP-HUM-009 Evidential standard for AI-triggered allegations | D.4 | ★1 | None established |

### Sequencing and shared assets

**TP-HUM-001 is the anchor procedure.** Its seeded-error case set is reused by TP-HUM-007 (explanation arms) and adapted by TP-HUM-008 (appeal cases). Building it once and reusing it saves roughly 3 reviewer-days across the domain and — more importantly — makes the three results directly comparable. Run TP-HUM-001 first.

TP-HUM-002's dwell-time baseline feeds TP-HUM-007's timeliness measure. TP-HUM-004's irreversibility mapping should precede TP-HUM-006's accountability tracing, since both walk the same workflows. TP-HUM-003 and TP-HUM-005 are independent and can run in parallel.

TP-HUM-009 runs together with TP-HUM-008: its canvas states that the contest route tested in TP-HUM-008 is meaningless without the disclosure control this procedure tests. TP-HUM-009 reuses **none** of TP-HUM-001's seeded-error case set, so the anchor-procedure logic above does not extend to it.

Because five of the nine procedures require the firm's own operational staff, the binding constraint on this domain is usually **staff availability, not reviewer effort**. Book participant time before scheduling reviewer time.

### Personnel

Procedures assume a lead reviewer with human-factors or behavioural-research competence, a second reviewer for blinded scoring and inter-rater checks, and firm-side provision of: de-identified dev/test case sets with ground truth, participant time, a sponsoring executive for the non-punitive assurance, and an HR or L&D contact.

**TP-HUM-009 needs neither the human-factors competence nor the participant time.** It needs case-file access, the second reviewer for dual scoring — which this paragraph already provides for — and the owner of the adverse-action process.

### Total indicative effort

**42.0 reviewer-days** across the nine procedures, excluding report drafting and firm-side participant time (which is substantial and should be costed separately by the firm).

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-HUM-001: PLAYBOOK_HUM_001.md
- TP-HUM-002: PLAYBOOK_HUM_002.md
- TP-HUM-003: PLAYBOOK_HUM_003.md
- TP-HUM-004: PLAYBOOK_HUM_004.md
- TP-HUM-005: PLAYBOOK_HUM_005.md
- TP-HUM-006: PLAYBOOK_HUM_006.md
- TP-HUM-007: PLAYBOOK_HUM_007.md
- TP-HUM-008: PLAYBOOK_HUM_008.md
- TP-HUM-009: PLAYBOOK_HUM_009.md

---
---

## Domain effort summary — HUM

| Procedure | ★ | Reviewer-days |
|---|---|---|
| TP-HUM-001 | ★3 | 6.0 |
| TP-HUM-002 | ★3 | 5.0 |
| TP-HUM-003 | ★3 | 5.0 |
| TP-HUM-004 | ★2 | 5.0 |
| TP-HUM-005 | ★2 | 3.0 |
| TP-HUM-006 | ★2 | 4.0 |
| TP-HUM-007 | ★2 | 6.0 |
| TP-HUM-008 | ★2 | 4.0 |
| TP-HUM-009 | **★1** | 4.0 |
| **Total** | | **42.0** |

Excludes report drafting and firm-side participant time, which is material: TP-HUM-001, -003, -007 and -008 together require roughly 25–40 person-days of the firm's operational staff. **TP-HUM-009 adds no firm-side participant days**, though it adds firm-side case-file retrieval and de-identification effort, which is frequently the critical path. The estimates above already assume TP-HUM-001's case set is reused by TP-HUM-007 and TP-HUM-008 (a saving of approximately 3.0 reviewer-days in total); if those procedures are run standalone, add that back.

Scaling notes: TP-HUM-004 and TP-HUM-006 scale with the number of in-scope workflows; TP-HUM-005 scales with the number of named suspension-authority holders exercised; TP-HUM-001, -003 and -007 scale with participant cohort size in facilitation time only, not in design time.

---

**Change Log**
- v1.0 (2026-07): Initial publication. Eight procedures expanded from CANVASES_HUM.md. ★ ratings, assurance objectives and pass/fail/partial indicators carried unchanged from canvases. No new citations introduced.
- v1.1 (2026-08-25): TP-HUM-009 (evidential standard for AI-triggered adverse allegations) added, derived 1:1 from the IRQ-HUM-009 canvas; domain totals move to nine procedures and 42.0 reviewer-days; ★ distribution becomes three ★3, five ★2 and one ★1 — the domain's first ★1. The domain's behavioural-study framing, blinding, deception and participant rules are qualified in the preamble, because TP-HUM-009 is a documentation and case-file review. No new citations introduced.
- v1.2.1 (2026-09-19): TP-HUM-009 common pitfalls — the ★1 honesty note re-stated to match the IRQ-HUM-009 canvas, which now grounds the harm mechanism in five independent systems across four jurisdictions rather than three and three: the Post Office Horizon system and the Dutch childcare benefits risk-classification model are named alongside Robodebt, Michigan MiDAS and the Home Office/ETS TOEIC programme, with the canvas's qualifications of the two added cases carried. ★1, the procedure, its steps, its indicators and the domain totals are unchanged; no new citations introduced beyond those the canvas carries.
- v1.3.2 (2026-10-03): TP-HUM-002 gains the refusal-durability limb, with its Pass and Fail rules and evidence record; the case-set reuse saving and three procedure subdomains corrected (00_Admin/CORRECTION_LOG_2026-10-03.md §8). No ★ rating or reviewer-day figure changes.
