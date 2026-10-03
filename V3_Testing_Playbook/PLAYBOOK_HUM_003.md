# TP-HUM-003 — Skill Atrophy: AI-Free Competency Assessment

**IRQ:** IRQ-HUM-003 — Skill Atrophy Undermining Fallback Capability.
**Assurance objective:** AO-HUM-003 — the organisation shall periodically and genuinely assess staff competency to perform each AI-supported critical task without AI assistance, and shall not assume retained competency based on prior training or documented procedures alone.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — a direct application of established occupational skill-retention and training-evaluation methodology (Arthur et al.'s 1998 meta-analytic framework) to a new domain. The framework is well-established; its calibration to AI-assisted FS roles has no agreed benchmark.

### Preconditions
- Identification of the **critical task(s)** the AI supports, and of the fallback SOP for performing each without AI. Where no fallback SOP exists, that is a finding recorded before assessment begins.
- De-identified dev/test case files representative of routine and non-routine work.
- **A scoring rubric — the same one used for AI-assisted output quality assurance.** Using a different, gentler rubric for the unaided assessment is the most effective way to manufacture a pass.
- A defined minimum competency threshold, obtained in writing before results are known. Where none exists, that absence is itself a finding and the assessment is reported against expert adjudication instead.
- Participant cohort: staff who perform the task with routine AI assistance, sampled across tenure. Minimum 8 (reviewer-set design minimum, disclosed at scoping); include both long-tenured (higher decay exposure) and recent joiners (who may never have learned the unaided task at all — a distinct and frequently overlooked finding).
- **Prior-cycle results where they exist.** A single point-in-time snapshot cannot show decay; the trend limb is what the assurance objective actually asks about.
- Ethics and consent pack, including an explicit non-punitive assurance. This procedure is more sensitive than the others: staff are being assessed on competence, and without a credible assurance participation will be defensive and results unusable.
- Time constraints comparable to normal operating conditions, agreed with the operations owner.
- Personnel: lead reviewer; second reviewer or SME assessor for blind scoring; HR/L&D contact.

### Test design
**Core assessment.** Each participant completes a set of realistic dev/test cases entirely without AI assistance, under comparable time pressure, using the fallback SOP and the tools available in a genuine AI-outage scenario. Minimum 5 cases per participant (reviewer-set design minimum, disclosed at scoping), spanning routine and non-routine.

**Blind scoring.** Outputs are stripped of participant identifiers and scored against the QA rubric by an assessor who does not know whose work they are marking or whether the participant is long- or short-tenured.

**Trend limb.** Where prior-cycle results exist for the same individuals, scores are compared longitudinally. Where they do not, the reviewer substitutes a **tenure-stratified cross-sectional comparison** — comparing unaided performance across AI-assisted tenure bands — and reports it explicitly as a weaker substitute for longitudinal data, since cohort differences confound it.

**Fire-drill limb.** Separately from individual assessment, establish whether the fallback process has ever been **actually exercised** as a scheduled drill, at scale, under time pressure — as opposed to having its documentation reviewed. Where a drill has occurred, review its execution record against the important business service's stated impact tolerance. Where it has not, that is a discrete finding.

**Governance limb.** Establish whether a board-approved threshold exists for maximum AI-assisted tenure before mandatory reassessment, and whether staff are tracked against it; and whether refresher training cadence is calibrated against measured skill-decay data for this specific task or is a generic schedule.

### Steps
1. Identify critical tasks and obtain the fallback SOP; record its existence, currency and specificity.
2. Obtain in writing, before assessment: the minimum competency threshold, the QA rubric, and the time allowance.
3. Secure the ethics and consent pack with explicit non-punitive assurance from the sponsoring executive; communicate it to participants directly.
4. Select the participant cohort stratified by AI-assisted tenure; record the strata.
5. Build the case set with the SME; verify it spans routine and non-routine work.
6. Run the assessment: participants work unaided, under the agreed time allowance, with AI access removed rather than merely discouraged (verify removal technically — a participant who can still reach the tool will).
7. Anonymise outputs; blind-score against the QA rubric; second assessor scores a subsample independently for inter-rater agreement.
8. Compare scores against the minimum threshold, and run the trend limb (longitudinal where prior cycles exist, tenure-stratified cross-sectional otherwise, labelled as such).
9. **Fire-drill limb:** obtain records of any executed fallback drill; assess whether it was genuinely executed, at what scale, under what time pressure, and whether the important business service was delivered within its impact tolerance.
10. **Governance limb:** obtain the refresher training schedule and its stated calibration basis; obtain any board-approved maximum-tenure-before-reassessment threshold and the tracking against it.
11. Collect participant self-report on confidence performing the task unaided, and record whether the organisation has any mechanism that would surface such self-reports.
12. Debrief participants individually and confirm results are reported only in aggregate.

### Observations & measures
- **Unaided competency score** per participant against the QA rubric, reported in aggregate and by tenure band. Canvas threshold: **meets or exceeds the minimum unaided competency threshold** defined by the firm.
- **Sub-threshold proportion** = participants scoring below the minimum ÷ participants assessed. Canvas Fail condition: sampled staff fall **materially** below. "Materially" is not defined by any cited source — **reviewer judgement**, basis recorded.
- **Trend** — longitudinal change across assessment cycles where available. Canvas threshold: **no statistically significant downward trend**. Where only cross-sectional tenure data exists, report the tenure-band comparison and state explicitly that it does not establish a trend.
- **Inter-rater agreement** on blind scoring — reported so readers can judge reliability.
- **Fire-drill status** (categorical): scheduled and executed within impact tolerance / executed but outside tolerance / documented but never executed / no drill programme.
- **Refresher calibration** (binary): cadence calibrated against measured skill-decay data for this task / generic schedule.
- **Maximum-tenure threshold** (binary): board-approved threshold exists and staff are tracked against it / absent.
- **Self-reported confidence** and whether any organisational mechanism captures it. No threshold; qualitative.

### Interpretation
- **Pass** — sampled staff meet or exceed the minimum unaided threshold; no statistically significant downward trend across cycles; fallback fire-drill is scheduled, actually executed, and delivers the important business service within its impact tolerance; refresher cadence is calibrated against measured decay data for this task; a board-approved maximum-AI-assisted-tenure threshold exists with staff tracked against it.
- **Fail** — sampled staff fall materially below the minimum threshold; **or** a clear downward trend is observed with no corrective action; **or** the fallback process has never been fire-drilled and only its documentation has been reviewed; **or** no AI-free competency assessment has ever been conducted and competency is assumed from historical pre-AI training records; **or** staff self-report low confidence performing the task unaided with no organisational response.
- **Partial** — current competency meets threshold but no prior-cycle data exists so decay cannot be assessed; or competency and drills pass but refresher cadence is generic and no maximum-tenure threshold exists. State which limbs are unevidenced.

### Evidence outputs
- E1 Fallback SOP as provided, with currency and specificity assessment — **L2**.
- E2 Pre-agreed threshold, rubric and time allowance record, timestamped — **L2**.
- E3 Ethics/consent pack and non-punitive assurance — **L2**.
- E4 Cohort stratification record — **L3**.
- E5 Case set manifest — **L3**.
- E6 Assessment execution record including verification that AI access was technically removed — **L3**.
- E7 Blind-scored results in aggregate and by tenure band, with inter-rater agreement — **L3**.
- E8 Trend analysis (longitudinal or, labelled as such, cross-sectional) — **L5** where multiple historical assessment cycles are analysed; **L3** for a single cycle.
- E9 Fire-drill execution records and impact-tolerance assessment — **L4** where an independent audit of an actual drill is performed.
- E10 Refresher training schedule and calibration basis — **L2**.
- E11 Maximum-tenure threshold and tracking evidence — **L2/L3**.
- E12 Participant self-report summary and debrief record — **L3**.

### Common pitfalls & limitations
- **A gentler rubric for the unaided assessment.** Use the QA rubric. If the firm objects that unaided work cannot fairly be held to the same standard, that objection is itself the finding: the fallback capability does not meet the standard the business relies on.
- **AI access discouraged but not removed.** Verify technically.
- **Single snapshot presented as decay evidence.** It is not. Say so.
- **Confounded cross-sectional comparison.** Long-tenured staff differ from recent joiners in many ways besides AI exposure. Report the confound.
- **Assessment anxiety.** Without a credible non-punitive assurance, participants perform defensively or decline. This is why the assurance comes from the sponsoring executive and is communicated directly, not via line management.
- **Confusing documented fallback with exercised fallback.** The canvas is explicit: reviewing the SOP is not a drill.
- **Recent joiners who never had the skill.** Skill *atrophy* framing assumes prior competence. Where recent joiners have only ever worked AI-assisted, the finding is absent competence rather than decayed competence — a materially different remediation, and worth separating in the report.
- **★3 honesty.** The skill-retention framework is established; its FS-AI calibration is not.

### Time/effort estimate
**5.0 reviewer-days** — 0.5 task identification and SOP review; 0.5 threshold/rubric agreement and ethics; 1.0 case-set build; 1.0 assessment facilitation; 0.75 blind scoring and inter-rater work; 0.5 fire-drill and governance limb review; 0.75 trend analysis and write-up. Firm-side participant time additional (approximately 0.5 day per participant).

---
---

