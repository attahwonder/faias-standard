# TP-HUM-007 — Explanation Adequacy: Two-Arm Catch-Rate Study

**IRQ:** IRQ-HUM-007 — Explanation Inadequacy Undermining Independent Judgement.
**Assurance objective:** AO-HUM-007 — explanations provided to human decision-makers shall be demonstrated, through testing with the actual user population, to be sufficient in content, faithfulness and timeliness to support genuine independent judgement, not merely to be present or superficially comprehensible.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — human-grounded interpretability evaluation per Doshi-Velez & Kim's framework is credible published methodology, but the specific application (comparing catch-rate impact of explanation presence and quality in an FS review context) is bespoke test design with no agreed FS benchmark, heavily dependent on case-set and explanation-variant design.

### Preconditions
- **TP-HUM-001 completed**, with its seeded-error case set available for reuse. This procedure is a two-arm extension of that study; building a fresh case set is wasteful and makes the results non-comparable.
- **TP-HUM-002's dwell-time data available**, for the timeliness measure — the question of whether the explanation fits within the reviewer's actual available decision time cannot be answered without it.
- Participant cohort drawn from the **actual reviewing population** — underwriters, claims handlers or AML investigators as applicable. Generic usability-test participants do not satisfy this IRQ; the canvas Fail indicator names testing that has never involved actual reviewing staff.
- Minimum 12 participants for a two-arm design (6 per arm), 16–20 preferred (reviewer-set design minimum, disclosed at scoping); a three-arm design requires proportionally more. Where the firm cannot provide this, run within-participant (each participant sees both conditions on different case subsets, counterbalanced) and report the design change and its confound (learning effects) explicitly.
- The ability to configure explanation variants in the staging workflow: current explanation, minimal/absent explanation, and — where feasible — a redesigned explanation.
- Access to the model's actual computational basis, where technically feasible, for the faithfulness limb.
- Ethics/consent pack as TP-HUM-001, including debrief.
- Personnel: lead reviewer; second reviewer for comprehension-interview scoring; firm workflow owner; ML engineer for the faithfulness limb.

### Test design
**Arms.**
- **Arm A** — recommendation with the **current** explanation.
- **Arm B** — recommendation with **minimal or absent** explanation.
- **Arm C (optional)** — recommendation with a **redesigned** explanation, where the firm has a candidate design worth evaluating.

Participants are randomly allocated (or counterbalanced within-participant where numbers force it). The case set is the TP-HUM-001 seeded-error set, with the same seeding ratio and the same blinding.

**Primary measure: differential catch rate.** The question this study exists to answer is not "do reviewers like the explanation" but "does the explanation help them catch wrong recommendations". If Arm A's catch rate does not exceed Arm B's, the explanation is adding no verification value however comprehensible it is.

**Secondary measures:** decision confidence (self-reported on a simple scale per case) and time-to-decision per case.

**Comprehension interview.** On a subsample (minimum 6 participants — a reviewer-set design minimum, disclosed at scoping), a structured interview after the session asks the participant to restate, in their own words, the actual basis for the AI's recommendation on three specific cases (reviewer-set design minimum, disclosed at scoping). Responses are scored by two reviewers against a rubric distinguishing:
- **Substantive restatement** — the participant identifies the actual determinants and can engage with them.
- **Surface repetition** — the participant reproduces explanation language without demonstrating engagement with the underlying basis.
- **Neither.**

This distinction is the analytical heart of the interview limb and the rubric must make it operable, with worked examples agreed in advance.

**Faithfulness limb.** Where technically feasible, the explanation's account is compared against the model's actual computational basis for a sample of cases. Where it is not feasible — which is common — the reviewer instead establishes whether the explanation carries **explicit faithfulness caveats** where the model's stated reasoning is known to be potentially unfaithful, and whether the firm treats the explanation internally as a ground-truth account of the model's reasoning (a Fail indicator).

**Timeliness limb.** Explanation delivery time and length are compared against the reviewer's actual available decision time, taken from TP-HUM-002's dwell-time data. An explanation that cannot be read in the time available is skipped in practice regardless of its quality.

### Steps
1. Confirm TP-HUM-001's case set and TP-HUM-002's dwell-time data are available; if not, those procedures are prerequisites.
2. Pre-register the design: arms, allocation, participant numbers, primary and secondary measures, and the comprehension rubric with worked examples. Timestamp.
3. Secure ethics/consent; brief participants on the fact of the study without disclosing the arm structure or the seeded-error design.
4. Configure the explanation variants in the staging workflow; verify each renders as intended and that Arm B genuinely removes the explanation rather than merely shortening it.
5. Allocate participants; run the sessions under realistic time pressure and throughput.
6. Record per case: arm, participant (pseudonymised), case ID, seeded/unseeded, decision, catch determination, self-reported confidence, time-to-decision.
7. Compute catch rate per arm and the differential, with an interval reflecting the sample size.
8. Run the comprehension interviews on the subsample; two reviewers score independently against the rubric; record agreement.
9. Run the faithfulness limb: either compare against the model's computational basis, or (where infeasible) assess the presence of faithfulness caveats and how the firm treats the explanation internally. Record which route was taken and why.
10. Run the timeliness limb: measure explanation length and delivery latency; compare against the dwell-time distribution from TP-HUM-002; assess whether the explanation fits the time actually available.
11. Establish whether any explanation-adequacy testing has previously been conducted **with the real reviewing population**, or only in generic usability testing.
12. Debrief participants fully.

### Observations & measures
- **Catch rate by arm** and **differential** (Arm A − Arm B), reported with an interval. Canvas threshold: catch rate **measurably higher** in the current-explanation arm, demonstrating genuine verification value. "Measurably" is not numerically defined in the cited framework — **reviewer judgement**, basis recorded, and the interval must be reported rather than a bare point difference.
- **Decision confidence by arm.** Diagnostic. A pattern of higher confidence *without* higher catch rate in Arm A is a particularly adverse finding — the explanation is increasing trust without increasing verification — and should be called out explicitly even though the canvas does not name it.
- **Time-to-decision by arm.** Diagnostic.
- **Comprehension scores** — proportions substantive / surface / neither, with inter-rater agreement. Canvas threshold: reviewers can **substantively and correctly restate** the actual basis, not just repeat surface language. **No numeric threshold — reviewer judgement.**
- **Faithfulness finding** (categorical): explanation verified against computational basis / not technically feasible, caveats present / not feasible, no caveats and explanation treated internally as ground truth. Canvas Fail condition: the last.
- **Timeliness finding** (binary): explanation delivery fits within actual available decision time per TP-HUM-002 data / does not, and is therefore skipped in practice.
- **Prior testing with real population** (binary). Canvas Fail condition: no testing ever conducted with actual reviewing staff; adequacy asserted by the development team.

### Interpretation
- **Pass** — catch rate measurably higher in the current-explanation arm; comprehension interviews show substantive, correct restatement of the actual basis; explanation delivery fits within the reviewer's actual available decision time per the TP-HUM-002 data; explicit faithfulness caveats present where the model's stated reasoning may be unfaithful; explanation-adequacy testing has been conducted with the real reviewing population.
- **Fail** — no meaningful catch-rate difference between arms, indicating the explanation adds no verification value despite being present; **or** comprehension interviews show participants can repeat explanation language but cannot substantively restate or engage with the actual basis; **or** explanation delivery is too slow or too lengthy for the actual available decision time and is skipped in practice; **or** no faithfulness caveats exist and the explanation is presented and treated internally as a ground-truth account of the model's reasoning; **or** no testing has ever been conducted with actual reviewing staff.
- **Partial** — catch-rate differential is positive but small relative to the interval (state it plainly rather than over-claiming), or the faithfulness limb could not run technically and caveats are present but generic. State the specific limitation.

### Evidence outputs
- E1 Pre-registered design and comprehension rubric, timestamped — **L3**.
- E2 Ethics/consent pack — **L2**.
- E3 Explanation design specification as provided — **L2**.
- E4 Variant configuration verification record — **L3**.
- E5 Session results by arm: catch rates with intervals, confidence, time-to-decision — **L3**.
- E6 Comprehension interview transcripts (pseudonymised), scores and inter-rater agreement — **L3**.
- E7 Faithfulness limb record with route taken and reasoning — **L4** where an independent assessment against the model's actual computational basis was performed; **L3** where the caveat-presence route was taken.
- E8 Timeliness analysis cross-referenced to TP-HUM-002 dwell-time data — **L3**.
- E9 Prior usability-testing results as provided — **L3**.
- E10 Production reviewer feedback or override patterns correlated with explanation quality over a sustained period, where available — **L5**.
- E11 Product documentation asserting an explanation is provided for every recommendation — **L1** (explicitly labelled as assertion).
- E12 Debrief record — **L2**.

### Common pitfalls & limitations
- **Building a fresh case set** rather than reusing TP-HUM-001's, losing comparability and burning 1.5 days.
- **Arm B that is not genuinely minimal.** Shortening the explanation is not removing it; the contrast must be real or the differential collapses toward zero for design reasons rather than substantive ones.
- **Underpowered arms.** Six per arm is a floor and produces wide intervals. Report the interval; do not present a small difference as a finding.
- **Confidence without catch rate.** Watch for it specifically; it is the interpretability failure mode that matters most in an oversight context and is easy to miss if only catch rate is analysed.
- **Comprehension interviews scored by one reviewer** against an unstated rubric — the same weakness as TP-HUM-006's attribution scoring, and the same fix.
- **Generic usability participants.** The canvas is explicit; they do not satisfy the objective.
- **Assuming faithfulness.** Where the faithfulness limb cannot run technically, say so and assess caveats instead; do not silently treat the explanation as accurate.
- **★2 honesty.** Bespoke design on a credible framework. Report as professional assessment.

### Time/effort estimate
**6.0 reviewer-days** — 0.5 design pre-registration and ethics; 0.5 case-set adaptation from TP-HUM-001 (reuse saves approximately 1.5 days); 0.5 variant configuration and verification; 1.5 session facilitation across arms; 1.0 comprehension interviews and dual scoring; 0.75 faithfulness limb; 0.25 timeliness analysis; 1.0 analysis and write-up. Firm-side participant time additional and substantial (12–20 participants).

---
---

