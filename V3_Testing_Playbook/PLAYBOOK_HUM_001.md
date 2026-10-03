# TP-HUM-001 — Automation Bias: Seeded-Error Detection Study

**IRQ:** IRQ-HUM-001 — Undetected Automation Bias in Human Review of AI Outputs.
**Assurance objective:** AO-HUM-001 — human reviewers of AI-assisted decisions shall demonstrably discriminate between correct and incorrect AI outputs at a measured rate, with disagreement and error-detection rates monitored on an ongoing basis to detect degradation into automation bias.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — the accountability/automation-bias seeded-error paradigm established in Skitka et al. (1999, 2000) and applied in Goddard, Roudsari & Wyatt's (2012) systematic review of automation bias in clinical decision support, adapted to an FS review workflow. Multi-decade converging evidence across aviation, clinical and process-control domains; no agreed FS-specific benchmark, so case-set design and seeding ratio rest on professional judgement.

### Preconditions
- **Case set with known ground truth.** A body of historical, fully anonymised dev/test underwriting, claims or AML decisions where the correct outcome is independently established (subsequent outcome data, quality-assurance re-review, or expert adjudication). Without genuine ground truth the study measures agreement, not accuracy, and is worthless.
- **A working staging replica of the actual review workflow** — same interface, same information layout, same explanation presentation, same queue mechanics. Reviewers behave differently in a spreadsheet than in their tool.
- Participant cohort: a representative sample of the actual reviewing population, spanning tenure and seniority. Minimum 8 participants; 12–15 preferred (reviewer-set design minimum, disclosed at scoping). Fewer than 8 gives an estimate too noisy to support a threshold judgement, and this should be said in the report rather than papered over.
- **Ethics and consent pack** signed off: informed consent, non-punitive assurance from the sponsoring executive, anonymisation protocol, debrief plan.
- Blinding arrangement: participants know a study is running; they do not know which cases are seeded, the seeding ratio, or that catch rate is the primary measure.
- The AI system's **known error rate** on comparable unseeded cases — required to interpret production disagreement rates.
- The firm's defined minimum catch-rate threshold, if one exists, obtained in writing **before** results are known.
- Personnel: lead reviewer (human-factors competent); second reviewer for blinded scoring; firm workflow owner; HR/L&D contact.

### Test design
**Structure.** A case set of realistic size — minimum 60 cases per participant (reviewer-set design minimum, disclosed at scoping), sized so that a full sitting matches a realistic shift segment — routed through the normal review workflow. A defined proportion, **15–20% per the canvas**, carry a deliberately incorrect AI recommendation. The remainder carry the AI's genuine recommendation, correct or otherwise.

**Seeded-error construction is the craft of this study.** Seeded errors must be *individually plausible*: fluent, well-reasoned, internally consistent, and wrong. An implausible error (an obvious arithmetic slip, a contradictory statement) tests attentiveness, not automation bias, and inflates catch rate. Each seeded case is constructed with a business SME and peer-reviewed for plausibility by the second reviewer, who scores it blind on a simple plausibility rubric; cases failing the rubric are rebuilt. Errors are distributed across error *types* — wrong conclusion from correct evidence, correct conclusion from misread evidence, omitted material factor, over-confident framing of a genuinely uncertain case — so that catch rate can be decomposed.

**Realism conditions.** The session runs under the throughput expectation the participant normally works to. No extra time. No signalling from the reviewer that accuracy is being measured. Where the workflow includes interruptions and parallel queues, these are reproduced.

**Measurement arms.** A single arm suffices for the primary measure. Where budget allows, a **volume/time-pressure arm** — the same participants, a later session, at a materially higher throughput expectation within normal operating range — supports the canvas pass indicator about degradation under pressure. This second arm is what turns a point estimate into a statement about the workflow's operating envelope.

### Steps
1. Agree and document, before construction: seeding ratio, case-set size, participant cohort, blinding protocol, the firm's minimum catch-rate threshold, and the AI's known error rate. Timestamp the record — thresholds agreed after results are known are not thresholds.
2. Secure the ethics and consent pack; brief participants on the fact of the study without disclosing the seeded-error design.
3. Build the case set with the business SME. Verify ground truth independently for every case.
4. Construct seeded errors across the four error types; second reviewer scores plausibility blind; rebuild any that fail.
5. Load the set into the staging workflow replica; verify the interface matches production, including explanation presentation.
6. Run session 1 under normal throughput. Record per case: participant ID (pseudonymised), case ID, seeded/unseeded, participant decision, whether the AI recommendation was accepted, challenged or overridden, free-text rationale where the workflow captures it, and dwell time.
7. Run the volume/time-pressure arm where in scope.
8. Score catch rate: a seeded case counts as caught where the participant flagged, challenged or overrode the incorrect recommendation. Ambiguous cases are adjudicated by both reviewers independently; record inter-rater agreement.
9. Analyse the relationship between catch rate and dwell time, and between catch rate and case complexity (complexity graded by the SME in advance).
10. Separately, obtain and analyse **production disagreement/override-rate data** for the live workflow: its level, its trend, and whether it is plausible against the AI's known error rate. Record whether anyone at the firm has investigated the level, and who owns the monitoring.
11. Review reviewer training records: is there automation-bias-specific content, or only generic AI-literacy material? Record content and refresh cadence.
12. Debrief participants fully. Confirm to them what was measured and how results will be used.

### Observations & measures
- **Seeded-error catch rate** = seeded cases caught ÷ seeded cases presented, aggregate and by error type. Canvas threshold: **meets or exceeds the firm's defined minimum, e.g. ≥80%**. Where the firm has no defined threshold, that absence is a finding and the measured rate is reported against the canvas's illustrative 80% with the reasoning made explicit.
- **Unseeded acceptance behaviour** — the AI's actual error rate on unseeded cases versus the rate at which participants caught those genuine errors. This is the honest comparator and is often more revealing than the seeded measure.
- **Catch rate versus dwell time** — correlation, reported with the caveat that this is observational within a small sample. **No established threshold — reviewer judgement.**
- **Catch rate versus complexity grade.** Same caveat.
- **Degradation under pressure** = catch rate in the higher-throughput arm − catch rate in the normal arm. Canvas pass indicator: catch rate does not degrade **materially** as volume or time pressure increases within normal operating conditions. "Material" is not numerically defined in the cited literature — **reviewer judgement**, basis recorded.
- **Production disagreement/override rate** — level and trend, judged against the AI's known error profile. Canvas Fail condition: at or near zero despite a known non-zero AI error rate, with no investigation on record.
- **Monitoring ownership** (binary): disagreement-rate monitoring live in production and reviewed by a named accountable function on a defined cadence / not.
- **Training content** (binary): automation-bias-specific content present / generic AI-literacy module only.
- **Inter-rater agreement** on ambiguous catch adjudications — reported so readers can judge scoring reliability.

### Interpretation
- **Pass** — catch rate meets or exceeds the defined threshold; production disagreement/override rate is non-zero, stable and consistent with the AI's known error profile; catch rate does not degrade materially under realistic volume/time pressure; training records show completion and periodic refresh of automation-bias-specific content; disagreement monitoring is live and owned by a named function on a defined cadence.
- **Fail** — catch rate materially below threshold or approaching zero; **or** production disagreement/override rate at or near zero despite a known non-zero AI error rate with no investigation; **or** catch rate collapses under realistic pressure, indicating the review step cannot function at production throughput; **or** no seeded-error or equivalent testing has ever been performed and reviewer effectiveness is asserted rather than measured; **or** training exists only as a generic AI-literacy module.
- **Partial** — catch rate meets threshold in the normal arm but the pressure arm was not run, or production monitoring exists in design but is not yet live, or training content is automation-bias-specific for new joiners but has no refresh cycle. State the specific gap.

### Evidence outputs
- E1 Pre-registered study protocol (thresholds, ratio, cohort, blinding), timestamped before construction — **L3**.
- E2 Ethics/consent pack and non-punitive assurance — **L2**.
- E3 Case set manifest with ground-truth verification records — **L3**.
- E4 Seeded-error construction log with blind plausibility scores — **L3**.
- E5 Workflow-replica fidelity confirmation — **L3**.
- E6 Session results: per-case decisions, dwell times, catch determinations, inter-rater agreement — **L3**.
- E7 Pressure-arm comparison where run — **L3**.
- E8 Production disagreement/override-rate analysis with trend — **L5** (operational data) where drawn from live monitoring.
- E9 Monitoring ownership and cadence evidence — **L2** (design spec) or **L3** (dashboard walkthrough).
- E10 Reviewer training curriculum review — **L2**.
- E11 Debrief record — **L2**.
- E12 Independent human-factors audit of reviewer challenge behaviour, where the firm holds one — **L4**.

### Common pitfalls & limitations
- **Implausible seeded errors** — the single most common design failure. They inflate catch rate and produce a comfortable, false pass. The blind plausibility rubric exists to stop this.
- **Weak ground truth.** "The QA team agreed with it" is not ground truth if the QA team saw the AI output first. Establish it independently.
- **Hawthorne effects.** Participants who know accuracy is measured perform above their working baseline. Blinding limits but does not eliminate this; the report should state that measured catch rate is likely an **upper bound** on real-world performance.
- **Small samples.** Eight participants gives a wide interval. Report the interval, not a point estimate presented as precise.
- **Removing time pressure** for practical convenience, which measures a workflow that does not exist.
- **Threshold selection after results.** Step 1 timestamps the threshold for exactly this reason.
- **Treating this as a staff performance assessment.** It is an assessment of the *system*, including the workflow, the interface, the throughput target and the training. Individual results stay anonymous, and the non-punitive assurance is a precondition, not a nicety.
- **★3 honesty.** The paradigm is well-established; its FS calibration is not. Report as professional assessment.

### Time/effort estimate
**6.0 reviewer-days** — 0.5 protocol pre-registration and ethics; 1.5 case-set build and ground-truth verification with SME; 1.0 seeded-error construction and blind plausibility scoring; 1.0 session facilitation (normal arm); 0.5 pressure arm; 0.5 production disagreement-data analysis; 0.25 training review; 0.75 analysis, inter-rater work and write-up. Firm-side participant time is additional: approximately 0.5–1.0 day per participant.

---
---

