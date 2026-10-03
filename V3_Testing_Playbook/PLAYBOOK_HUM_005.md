# TP-HUM-005 — Suspension Authority Under Commercial Pressure: Tabletop Simulation

**IRQ:** IRQ-HUM-005 — Untested Suspension Authority Against Commercial Pressure.
**Assurance objective:** AO-HUM-005 — authority to suspend or constrain the AI system shall be assigned to named, senior individuals with documented, rehearsed criteria, and the organisation shall hold evidence — through simulation or historical exercise — that this authority would be exercised against genuine commercial or operational pressure.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — safety-culture and crisis-decision simulation is a long-established methodology in aviation and nuclear safety-critical decision training, but its application to AI-suspension-authority testing in FS is bespoke and relies heavily on scenario design and assessor judgement; no FS-specific benchmark exists.

### Preconditions
- Identification of the **named individual(s)** holding suspension authority, from governance documentation, and confirmation of their availability for an unannounced-content exercise of 60–90 minutes (reviewer-set design minimum, disclosed at scoping).
- The documented **suspension trigger criteria** and escalation procedure. Where none exist, that is a finding recorded before the exercise, and the exercise is then run to establish what the individual would do absent criteria — which is itself informative.
- The firm's SM&CR mapping for the suspension role.
- Sponsor authorisation at a level above the participant, so that the exercise cannot be perceived as line-management assessment; and an explicit written statement that exercise performance will not be used in performance management.
- Records of any prior simulation cycles, and of any **real** historical suspension or near-suspension event.
- Personnel: lead reviewer (facilitator); a second reviewer as observer/scribe; optionally a firm-side actor to play the commercial-pressure role, briefed but not scripted verbatim.
- **This is a governance exercise only.** No live system is affected, no real suspension is triggered, and this is stated to the participant at the outset.

### Test design
**Scenario construction.** A realistic scenario in which early warning signs of AI degradation are:
- **Ambiguous** — the signal is consistent with degradation and also with normal variation.
- **Incomplete** — key diagnostic data is unavailable and would take days to obtain.
- **Accompanied by explicit counter-pressure** — the canvas names three archetypes: a stated quarter-end revenue target, a regulatory deadline dependent on the system remaining live, and a senior stakeholder arguing for delay pending "more data". At least two of the three are present (reviewer-set design minimum, disclosed at scoping).

The scenario is calibrated so that it **does** meet the firm's documented trigger criteria on a careful reading — otherwise the exercise cannot distinguish appropriate restraint from inappropriate deferral. The reviewer determines and records this calibration before the exercise, and has it checked by the second reviewer.

**Unannounced content.** The participant knows an exercise is scheduled; they do not know its content. Advance notice of the scenario allows preparation and destroys the measure.

**Realistic time pressure.** The scenario unfolds with injects on a timeline. The participant is not given open-ended time to deliberate.

**Escalating-pressure injects.** Counter-pressure escalates over the exercise — a further stakeholder intervention, a revised revenue impact figure, a suggestion that a decision can wait until the next committee. What is measured is not only the decision but the point at which it is made and what moved it.

### Steps
1. Obtain governance documentation identifying the named individual(s), the trigger criteria, the escalation procedure, and the SM&CR mapping.
2. Assess and record whether the trigger criteria are specific enough to be operable, or vague enough that "genuine ambiguity" could serve as a standing justification for inaction. This assessment stands independently of the exercise outcome.
3. Construct the scenario. Record the calibration analysis showing it meets the documented criteria, and have the second reviewer verify.
4. Secure sponsor authorisation above the participant and the written non-punitive statement; communicate the latter to the participant when scheduling.
5. **Pre-exercise interview (short, before the scenario is revealed):** does the participant know they hold this authority personally? Do they believe it sits with them or with a committee? Can they state the trigger criteria unprompted? Record verbatim. This is frequently the most revealing part of the whole procedure — the canvas names unawareness of holding the authority as a Fail indicator, and it is not rare.
6. Run the exercise with timed injects and escalating counter-pressure. The scribe records: every decision point, the time elapsed, the reasoning offered, what information the participant requested, and what specifically moved them.
7. At the decision point (or at scenario end if no decision is made), record the outcome: suspend, constrain, defer with defined conditions, or defer indefinitely.
8. Assess the decision against the documented trigger criteria, and against the time bound those criteria imply.
9. Assess whether the recorded rationale references the objective criteria or the presented counter-pressure.
10. Debrief the participant fully, including the calibration (that the scenario did meet criteria). The debrief is a required step and has training value in its own right.
11. Separately, review: the exercise programme's cadence and documented outcomes across cycles; any real historical suspension or near-suspension event and how it was handled; and any evidence of adverse consequence following a real exercise of suspension authority or the raising of a suspension concern.

### Observations & measures
- **Decision outcome** (categorical): suspends / constrains / defers with defined conditions and a short review point / defers indefinitely or declines.
- **Time-to-decision** measured against the time bound implied by the documented trigger criteria. Canvas threshold: **decision within the implied time bound, despite the counter-pressure.**
- **Rationale basis** (categorical, from the scribe record): references objective trigger criteria / references the commercial counter-pressure / references neither.
- **Pre-exercise awareness** (categorical): knows they hold the authority personally / believes it sits with a committee / unaware. Canvas Fail condition: unaware, or believes it sits with a committee rather than personally.
- **Criteria operability** (reviewer assessment): specific and operable / vague enough that ambiguity becomes a standing justification for inaction. Canvas Fail condition: the latter.
- **Programme maturity** (categorical): recurring cadence with documented outcomes tracked over cycles / one-off / never conducted.
- **SM&CR currency** (binary): mapping current and the individual confirms awareness of and comfort with the accountability / not.
- **Retaliation evidence** (binary): none / documented or anecdotal evidence of adverse consequence following a prior exercise of suspension authority or raising of a concern.

*No numeric thresholds apply anywhere in this procedure. Every measure is reviewer judgement against the firm's own documented criteria — which is precisely why the calibration analysis in step 3 must be recorded and checkable.*

### Interpretation
- **Pass** — the named individual suspends or constrains within the time bound implied by the trigger criteria despite the counter-pressure; the documented rationale references objective criteria rather than deferring to pressure; the exercise programme runs on a defined recurring cadence with outcomes tracked; SM&CR mapping is current and the individual confirms awareness and comfort with the accountability; no evidence of retaliation following any historical real exercise.
- **Fail** — the individual delays or declines to suspend despite the scenario meeting the documented criteria, citing the commercial pressure; **or** no trigger criteria exist, or they are vague enough that ambiguity becomes a standing justification for inaction; **or** no simulation or tabletop exercise has ever been conducted; **or** the individual is unaware they hold the authority or believes it sits with a committee; **or** evidence exists of a prior instance where raising a suspension concern affected the individual's standing.
- **Partial** — the individual decides correctly but outside the implied time bound; or decides correctly but the exercise programme is a one-off with no recurring cadence; or criteria are operable but SM&CR mapping is out of date. State the specific gap.

### Evidence outputs
- E1 Governance chart naming the individual with suspension authority, as provided — **L1** (existence of the role only; explicitly labelled).
- E2 Documented suspension trigger criteria and escalation procedure — **L2**.
- E3 Exercise programme design specification and cadence — **L2**.
- E4 Scenario construction record including the calibration analysis and second-reviewer verification — **L3**.
- E5 Sponsor authorisation and non-punitive statement — **L2**.
- E6 Pre-exercise interview record (verbatim on authority awareness and criteria recall) — **L3**.
- E7 Exercise scribe record: decision points, timings, reasoning, information requested, what moved the participant — **L3**.
- E8 Decision assessment against criteria and implied time bound — **L3**.
- E9 Criteria operability assessment — **L3**.
- E10 Independent review of any real historical suspension or near-suspension event — **L4**.
- E11 Trend data across multiple simulation cycles where the programme has run repeatedly — **L5**.
- E12 Debrief record — **L2**.

### Common pitfalls & limitations
- **A scenario that does not actually meet the trigger criteria.** Then a decision not to suspend is correct, and the exercise measures nothing. The calibration analysis is the control against this and must be verified independently.
- **Advance notice of scenario content.** Destroys the measure entirely.
- **Toothless counter-pressure.** If the commercial pressure is nominal, the participant suspends easily and the exercise produces a false pass. The pressure must be as real as the firm's culture makes it — which is why a firm-side actor who genuinely occupies that role is more effective than a reviewer reading a script.
- **Line-management perception.** If the participant believes this feeds their appraisal, they will perform to the expected answer. The sponsor authorisation above them and the written non-punitive statement are the mitigations; without both, do not run the exercise.
- **Single participant, single scenario.** One exercise measures one person's response to one scenario on one day. Report as such; the ★2 rating exists partly for this reason.
- **Simulation-to-reality gap.** A tabletop decision is not a real decision with real consequences. This is the fundamental limitation of the method and must be stated in reporting; historical real-event evidence (E10) carries materially more weight where it exists.
- **Skipping the pre-exercise interview** in the interest of time. It frequently produces the strongest finding in the procedure.

### Time/effort estimate
**3.0 reviewer-days** — 0.5 governance documentation and criteria operability review; 1.0 scenario construction and calibration verification; 0.5 exercise facilitation including pre-interview and debrief (two reviewers for a 90-minute exercise plus preparation); 0.5 historical-event and programme-cadence review; 0.5 assessment and write-up. Add 0.5 day per additional named individual exercised.

---
---

