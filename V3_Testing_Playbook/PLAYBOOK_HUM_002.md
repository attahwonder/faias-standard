# TP-HUM-002 — Approval Theatre: Dwell-Time and Override-Trend Study

**IRQ:** IRQ-HUM-002 — Approval Theatre: Human Checkpoint Without Substantive Review.
**Assurance objective:** AO-HUM-002 — human approval checkpoints shall be demonstrated, through throughput, dwell-time and rejection-rate analysis, to constitute substantive review rather than procedural pass-through, with overriders trained, empowered and free from penalty for dissent.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — dwell-time and workload analysis is established human-factors and process-engineering method with decades of aviation and process-control precedent; the specific application to AI-approval-theatre detection is FS-context-bespoke, which is why it does not reach ★4.

### Preconditions
- De-identified historical dev/test case decisions in representative volume, replayable through the approval workflow.
- **The actual configured throughput targets and time allowances** for the approval role, obtained in writing from the operations owner — not the aspirational figure in a policy document.
- A staging replica of the approval workflow with the mandatory-justification field configured exactly as in production.
- Historical production data spanning **before and after AI-assistance go-live**, sufficient to establish an override-rate trend. Where the deployment is new and no post-go-live period exists, this limb cannot run and the procedure is scoped to the dwell-time and design limbs only, reported as such.
- Qualified staff available to perform **timed unaided review of a control sample** — this establishes the minimum-time-for-substantive-review baseline, and without it the dwell-time distribution has nothing to be compared against.
- Anonymous survey instrument and distribution route for the psychological-safety limb, with the sponsoring executive's non-punitive assurance and a guarantee of anonymity that the reviewer, not the firm, administers.
- Personnel: lead reviewer; operations owner; qualified reviewers for the baseline timing; HR contact for survey distribution protocol.

### Test design
Five limbs.

- **L1 Minimum-substantive-review baseline.** A control sample of cases (minimum 20, stratified by complexity — a reviewer-set design minimum, disclosed at scoping) is reviewed unaided by qualified staff who are told to review properly rather than quickly. Time per case is recorded. The resulting distribution — reported as a range with its lower quartile, not as a single number — is the baseline against which observed dwell times are judged. This limb is what makes the study defensible; a dwell-time figure with no baseline is an unanchored assertion.
- **L2 Replay dwell-time distribution.** A representative case volume is replayed through the approval workflow under the actual configured throughput targets. Dwell time per case is captured from the workflow's own instrumentation where available, and by observation where not.
- **L3 Override-trend analysis.** Historical rejection/override rate is plotted across the pre- and post-go-live periods. Any decline is tested for significance with a method appropriate to the data (interrupted time-series or a simple pre/post comparison with confidence intervals, depending on data volume — the method is chosen and recorded before the data is examined).
- **L4 Justification substance and psychological safety.** The justification field is tested for technical enforceability (can the workflow be completed without it?), and an audit sample of justification text is scored for substance versus boilerplate by two reviewers independently. Separately, an anonymous survey of the reviewing population covers perceived time pressure and perceived safety to override.
- **L5 Refusal durability (canvas field 11).** A sample of cases in which a reviewer recorded a refusal or a material alteration is traced forward through the workflow's own records to its final disposition, and the documented routes around a recorded refusal are attempted in the test environment, as the canvas sets out. The limb reads workflow configuration and records only, and alters no live decision. It uses the replay set-up of L2 and the records drawn for L4b, and adds no separate reviewer-day figure.

### Steps
1. Obtain in writing: configured throughput targets, time allowances, the approval workflow specification, and confirmation of whether pre/post-go-live data exists.
2. Secure ethics, consent and anonymity arrangements for the survey limb; agree with HR that the reviewer administers and holds responses.
3. **L1:** Select and stratify the control sample; brief qualified staff to review properly; record time per case; compute and report the baseline distribution.
4. **L2:** Load the replay volume into the staging workflow; run under actual throughput targets; capture dwell time per case, with the capture method recorded (instrumented versus observed).
5. **L4a:** Attempt to complete an approval without populating the mandatory justification field, by every route available including any keyboard shortcut or bulk-action path. Record whether it is technically enforced or bypassable.
6. **L4b:** Draw an audit sample of justification text (minimum 50 entries — a reviewer-set design minimum, disclosed at scoping — from replay and from historical records where available). Two reviewers independently score each as substantive / partially substantive / boilerplate-or-repeated. Record agreement.
7. **L3:** Pre-register the analysis method; obtain the historical override-rate series; analyse the pre/post trend; record whether any post-go-live decline exists and whether the firm has any investigation on record for it.
8. **L4c:** Distribute the anonymous survey. Minimum items: perceived time available per case; whether the reviewer has ever felt unable to override; whether overriding is perceived to carry any consequence; whether throughput targets feel achievable with substantive review.
9. Establish whether throughput targets were **calibrated against any measured review-time baseline** — ask the operations owner directly and seek documentary evidence. A "no" here is a finding independent of every measurement above.
10. **L5:** Draw the refusal sample from the replay and historical records; trace each case to its final disposition and record whether any approval after a recorded refusal carries an independently recorded review of equivalent or higher authority; attempt each documented route around a recorded refusal in staging (re-submission to a different approver, re-submission under a new case identifier, a configuration change, the configured exception path) and record which the workflow permits without such a review.
11. Debrief and report in aggregate only.

### Observations & measures
- **Minimum-substantive-review baseline** — distribution of unaided review times, reported with lower quartile and range. This is a derived reference, not a threshold from any published source.
- **Dwell-time distribution** for approved cases in replay. Canvas threshold: sits **materially above** the established baseline for the large majority of cases. "Materially" and "large majority" are not numerically defined in the cited literature — **reviewer judgement; the recommended and recorded basis is the proportion of cases falling below the baseline's lower quartile.**
- **Sub-baseline proportion** = approved cases with dwell time below the minimum plausible review time ÷ approved cases. Canvas Fail condition: a **material proportion** falls below.
- **Override-rate trend** — level pre- and post-go-live, with the significance of any decline. Canvas Fail condition: drops toward zero shortly after go-live with no investigation on record.
- **Justification enforceability** (binary): technically enforced / bypassable by at least one route.
- **Justification substance** = substantive entries ÷ sampled entries, with inter-rater agreement reported. **No established threshold — reviewer judgement**; boilerplate or repeated text indicates no substantive engagement.
- **Survey results** — aggregate proportions on time pressure and perceived safety to override. Canvas Fail condition: overriding perceived as risky to performance ratings or throughput targets.
- **Refusal durability** (binary per route): each documented route around a recorded refusal permitted / blocked without an equivalent-or-higher recorded review; and the number of traced refusals later approved without one.
- **Throughput calibration** (binary): targets documented as calibrated against a measured review-time baseline / set independently of any such measurement.

### Interpretation
- **Pass** — dwell-time distribution sits materially above the baseline for the large majority of cases; override rate stable and consistent with the AI's known error profile with no unexplained post-go-live decline; justification fields technically enforced and audit-sampled text substantive; survey shows no measurable career penalty for overriding; throughput targets documented as calibrated against the measured baseline; recorded refusals and material alterations hold (no traced refusal later approved without an equivalent-or-higher recorded review, and every documented route around a refusal is blocked).
- **Fail** — a material proportion of approved cases fall below minimum plausible review time; **or** override rate drops toward zero post-go-live with no investigation on record; **or** justification fields are bypassable, or the audit sample shows boilerplate/repeated text; **or** survey or informal evidence indicates overriding is perceived as risky to ratings or throughput; **or** throughput targets were set without reference to any measured review-time baseline; **or** a traced refusal was approved, or a documented route around a refusal is permitted, without an equivalent-or-higher recorded review.
- **Partial** — dwell times and justification substance pass, but the override-trend limb could not run (no post-go-live period) or throughput targets are uncalibrated despite adequate observed dwell times. State exactly which limbs support the conclusion.

### Evidence outputs
- E1 Written throughput targets, time allowances and workflow specification — **L2**.
- E2 Minimum-substantive-review baseline study record — **L3**.
- E3 Replay dwell-time distribution with capture method — **L3**.
- E4 Justification-field enforceability test record, listing every route attempted — **L3**.
- E5 Justification-text audit sample scoring with inter-rater agreement — **L3**.
- E6 Pre-registered override-trend analysis method and results — **L4** where performed as an independent audit of the trend over the deployment period.
- E7 Anonymous survey instrument, response rate and aggregate results — **L5** where drawn from live post-deployment monitoring of the real reviewing population; **L3** where simulated in staging.
- E8 Throughput-calibration enquiry record and any documentary evidence — **L2/L3**.
- E9 Policy statement that all decisions require human approval, as provided — **L1** (recorded for completeness and explicitly labelled as assertion).
- E10 Debrief and aggregate reporting record — **L2**.
- E11 Refusal-trace record (sample, final dispositions, routes attempted and the workflow's response to each) — **L3**.

### Common pitfalls & limitations
- **No baseline.** Reporting "average dwell time was 90 seconds" without establishing what substantive review actually takes is the characteristic weak version of this study. L1 is not optional.
- **Instrumented dwell time measuring the wrong thing.** Workflow timestamps often capture screen-open-to-submit, including interruptions, coffee and parallel work. Understand what the instrumentation measures before relying on it; where uncertain, observe a subsample directly and compare.
- **Replay without the real throughput target.** Participants who are not working to the target will not exhibit the behaviour the study is looking for.
- **Survey administered by the firm.** Anonymity that the employer controls is not anonymity. The reviewer administers and holds responses; this is stated to participants.
- **Post-hoc trend analysis method selection.** Pre-register it (step 7).
- **Confusing low override rate with automation bias.** A low override rate is consistent with an accurate AI. It is only a finding when set against the AI's known error rate — which is why TP-HUM-001's error-profile data is a required input here.
- **★3 honesty.** The method is established; the AI-specific application is bespoke. Report accordingly.

### Time/effort estimate
**5.0 reviewer-days** — 0.5 documentation gathering and ethics; 1.0 baseline study facilitation; 1.0 replay execution and dwell-time capture; 0.5 justification enforceability and text audit; 0.75 override-trend analysis; 0.75 survey design, distribution and analysis; 0.5 write-up. L5 runs within the replay and records work above and adds no separate figure. Firm-side participant time additional.

---
---

