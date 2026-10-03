# TP-HUM-008 — Contest Route: Genuine Human Re-Decision Study

**IRQ:** IRQ-HUM-008 — Absence of a Genuine Human Re-Decision Contest Route.
**Assurance objective:** AO-HUM-008 — a defined contest route shall be available to affected customers and colleagues, structurally requiring a human decision-maker to independently re-derive the outcome from underlying evidence rather than re-running the same automated process, with outcomes tracked and monitored for a rate consistent with genuine independent reconsideration.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — adapts the seeded-error paradigm from TP-HUM-001 (itself ★3) to the appeal context. The FS-specific application to contestability testing is bespoke with no agreed benchmark, and the process-separation assessment relies on assessor judgement of what constitutes structural versus nominal separation.

### Preconditions
- **TP-HUM-001's seeded-error case set available for adaptation**, together with its ground truth.
- A staging replica of the **actual appeal/review workflow** — not a description of it, and not the original decisioning workflow with a different label.
- Appeal decision-makers available to participate, drawn from whoever actually performs appeals. Minimum 6 (reviewer-set design minimum, disclosed at scoping); where the appeal function is a single person, that fact is itself a finding about independence and capacity.
- Documentation of the appeal process design, specifying the decision-maker's independence from the original automated pipeline.
- Historical appeal-outcome data with divergence rates, where the process is live.
- The AI system's known error rate, for interpreting divergence rates.
- Customer-facing appeal communications, for the comprehensibility limb.
- Ethics/consent pack including blinding: appeal decision-makers must not know which cases carry seeded-incorrect original decisions.
- Personnel: lead reviewer; second reviewer; firm appeals process owner.

### Test design
**Seeded-appeal study.** A set of dev/test cases with known ground truth, a defined proportion of which carry a **deliberately incorrect original AI decision**, is routed through the firm's actual appeal workflow as if genuinely contested. The seeding ratio follows TP-HUM-001's 15–20%. Seeded-incorrect original decisions must be plausible, for the same reason and by the same construction discipline as TP-HUM-001.

**Two things are measured, and they are distinct:**
- **Overturn rate on seeded-incorrect decisions** — does the appeal catch the error?
- **Evidence engagement** — is the appeal decision-maker presented with, and do they demonstrably engage with, underlying evidence *beyond* the AI's original output and rationale? An appeal that overturns by luck, or by disagreeing with the AI's tone, is not independent re-derivation.

Evidence engagement is assessed from case notes, workflow logs, and what the workflow interface actually presents — and, on a subsample, by a short structured interview asking the decision-maker what they looked at.

**Structural-separation walkthrough.** The appeal workflow's process steps are compared, step by step, against the original decisioning workflow's, to determine whether the separation is **structural** — different system or pipeline, different organisational reporting line, different evidence access — or merely **nominal** — the same pipeline, prompt or model, relabelled. This is the assessor-judgement limb the ★2 rating flags, so the criteria used are stated explicitly and the comparison table is published as evidence.

**Divergence-rate limb.** Historical appeal-outcome divergence rate is obtained and judged against the AI's known error rate. A divergence rate at or near zero against a known non-zero error rate is a Fail indicator, mirroring the logic of TP-HUM-001's disagreement-rate measure.

**Comprehensibility limb.** Customer-facing appeal communications are assessed for whether they disclose in comprehensible terms what the appeal substantively involves — not merely that an appeal exists.

### Steps
1. Confirm TP-HUM-001's case set and ground truth are available; adapt cases so the *original* decision (rather than the recommendation under review) carries the seeded error.
2. Pre-register: seeding ratio, sample size, structural-separation criteria, and the evidence-engagement rubric. Timestamp.
3. Secure ethics/consent and the blinding arrangement with the appeals process owner.
4. Verify the staging appeal workflow is a faithful replica, including what evidence the interface presents to the decision-maker.
5. Route the case set through the appeal workflow. Record per case: seeded/unseeded, original decision, appeal outcome, case notes, workflow logs of what was accessed, and time taken.
6. Score overturn determinations; two reviewers adjudicate ambiguous cases; record agreement.
7. Score evidence engagement per case against the pre-agreed rubric, using case notes and access logs. Supplement with a structured interview on a subsample of decision-makers about what they actually examined.
8. **Structural-separation walkthrough:** build a side-by-side comparison of appeal and original workflow steps, systems, prompts, models, evidence sources and reporting lines. Apply the pre-registered criteria and record the determination with reasoning.
9. Obtain historical appeal-outcome divergence data and the AI's known error rate; compare; record whether the firm has investigated any decline.
10. Review customer-facing appeal communications for comprehensibility of what the appeal involves.
11. Debrief participants.

### Observations & measures
- **Overturn rate on seeded-incorrect decisions** = seeded-incorrect originals overturned ÷ seeded-incorrect originals routed. Canvas threshold: the appeal workflow correctly overturns the **large majority**. Not numerically defined in any cited source — **reviewer judgement**, basis recorded, with the interval reported given likely small samples.
- **False-overturn rate** on unseeded (correct) originals — recorded because an appeal process that overturns indiscriminately is not evidence of good judgement. The canvas does not name this measure; it is recorded as diagnostic context and reported as such.
- **Evidence engagement rate** = cases where the decision-maker demonstrably engaged with underlying evidence beyond the AI's output and rationale ÷ cases. **No established threshold — reviewer judgement.** Canvas Fail condition: the workflow provides only the AI's original output and rationale with no route to underlying evidence.
- **Structural separation** (categorical): structurally distinct (system, pipeline and reporting line) / partially distinct / nominal only. Canvas Fail condition: shares the same system, prompt or pipeline with no structural separation.
- **Historical divergence rate** and its trend, judged against the AI's known error rate. Canvas Fail condition: at or near zero despite a known non-zero AI error rate.
- **Communication comprehensibility** (binary): customers are told in comprehensible terms what the appeal substantively involves / told an appeal is available with no disclosure of what the review involves.

### Interpretation
- **Pass** — the appeal workflow correctly overturns the large majority of seeded-incorrect original decisions; the decision-maker demonstrably engages with underlying evidence rather than only the AI's output and rationale, evidenced in case notes or workflow logs; the appeal process is structurally distinct from the original decisioning pipeline organisationally and procedurally; production divergence rate is non-zero and consistent with the AI's known error rate; customers are told in comprehensible terms what the appeal involves.
- **Fail** — the appeal fails to overturn a material proportion of seeded-incorrect originals, indicating it reproduces the original error; **or** the decision-maker's workflow provides only the AI's original output and rationale with no route to independently examine underlying evidence; **or** the appeal shares the same system, prompt or pipeline with no structural separation; **or** production divergence rate is at or near zero despite a known non-zero AI error rate; **or** customers are told an appeal is available with no disclosure of what the review substantively involves.
- **Partial** — overturn rate and evidence engagement pass, but separation is organisational without being systemic (same pipeline, different team) or vice versa; or the divergence-rate limb could not run because the process is not yet live. State which limbs support the conclusion.

### Evidence outputs
- E1 Customer-facing documentation stating an appeal is available — **L1** (explicitly labelled as assertion).
- E2 Documented appeal-process design specifying independence from the original pipeline — **L2**.
- E3 Pre-registered study design, separation criteria and engagement rubric, timestamped — **L3**.
- E4 Appeal workflow replica fidelity confirmation, including what evidence the interface presents — **L3**.
- E5 Process walkthrough/design review confirming the appeal routes to human re-derivation rather than an automated re-run — **L3**.
- E6 Seeded-appeal execution results: overturn rate with interval, false-overturn rate, case notes and access logs — **L3**.
- E7 Evidence-engagement scores with rubric and subsample interview records — **L3**.
- E8 Structural-separation side-by-side comparison table with determination and reasoning — **L3**.
- E9 Historical appeal-outcome divergence analysis against the AI's known error rate — **L4** where performed as an independent audit of historical divergence.
- E10 Production divergence-rate trend over a sustained period with investigation records for any decline — **L5**.
- E11 Customer communication comprehensibility assessment — **L3**.
- E12 Debrief record — **L2**.

### Common pitfalls & limitations
- **Testing the appeal process as described rather than as built.** Firms describe appeals as independent; the walkthrough regularly finds the same model, the same prompt, and the same evidence set. Build the comparison table.
- **Not recording false overturns.** Without them, a process that overturns everything looks excellent. It is not independent judgement; it is a different failure.
- **Unblinded appeal decision-makers.** If they know which cases are seeded, the overturn rate is meaningless.
- **Adapting TP-HUM-001 cases carelessly.** The seeded error must sit in the *original decision*, and the appeal decision-maker must encounter the case as a genuine contest, not as a review task.
- **Nominal separation accepted.** "A different team member reviews it" using the same pipeline and the same evidence view is a re-run with a different name. State the criteria used so the judgement can be challenged.
- **Small samples.** Appeal functions are usually small. Report intervals and be explicit that the study is underpowered where it is.
- **Divergence rate without the error rate.** A low divergence rate is only a finding when set against a known non-zero AI error rate, which comes from TP-HUM-001.
- **★2 honesty.** This adapts a ★3 paradigm into a bespoke context and adds an assessor-judgement separation limb. Report as professional assessment.

### Time/effort estimate
**4.0 reviewer-days** — 0.25 case-set adaptation from TP-HUM-001 (reuse saves approximately 1.5 days); 0.25 pre-registration and ethics; 0.5 workflow replica verification; 1.0 execution; 0.5 dual scoring and engagement assessment; 0.75 structural-separation walkthrough and comparison table; 0.25 divergence and communication limbs; 0.5 write-up. Firm-side participant time additional.

---
---

