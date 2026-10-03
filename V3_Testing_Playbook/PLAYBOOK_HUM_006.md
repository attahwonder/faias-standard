# TP-HUM-006 — Accountability Tracing Through Delegated and Multi-Agent Workflows

**IRQ:** IRQ-HUM-006 — Accountability Gap Through Delegated and Multi-Agent Workflows.
**Assurance objective:** AO-HUM-006 — every AI-influenced decision shall be traceable to a named, accountable individual, with accountability explicitly mapped through each stage of any delegated or multi-agent workflow, and evidenced in attributable approval records.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — decision-trace sampling is a recognisable extension of established internal-audit methodology, but its application to multi-agent AI delegation chains is FS-context-bespoke, with professional judgement required to assess what "genuinely attributable" means for a given workflow; no agreed benchmark exists.

### Preconditions
- The firm's **decision-level accountability map** for each in-scope workflow, if one exists. Where accountability documentation exists only at system level ("Senior Manager X owns the AI system"), that is a Fail indicator recorded at the outset — but the trace sampling still runs, because it evidences the practical consequence.
- A set of de-identified dev/test decisions that passed through each in-scope delegated or multi-agent workflow, in sufficient number to sample meaningfully.
- Access to approval records, workflow logs, agent invocation records including agent instance and version identifiers, and human touchpoint records.
- **Architecture and change-control records** covering the review period, so that the accountability map's update history can be tested against the workflow's change history. This is the limb most often missing and most often decisive.
- The firm's SM&CR mapping documentation.
- Records of any real historical incident or complaint investigation for this workflow.
- Personnel: lead reviewer; second reviewer for independent scoring; firm workflow and governance owners.

### Test design
**Trace sampling.** A representative sample of dev/test decisions — minimum 20 per in-scope workflow (reviewer-set design minimum, disclosed at scoping), stratified to include both straightforward and complex paths — is traced end to end. For each decision, the reviewer reconstructs the **full contributing chain**: every agent, every automation step, every human touchpoint, in order, and attempts to identify a single named individual genuinely accountable for the final decision per the documented map.

**Three-point scoring.** Each traced case is scored:
- **Clearly attributable** — a single named individual is identifiable, their contribution is recorded, and the accountability is substantive rather than nominal.
- **Attributable with ambiguity** — an individual can be identified but their relationship to the material determinants of the decision is unclear, or more than one individual could plausibly be the accountable party.
- **Not attributable** — no named individual can be identified as accountable for the decision as made.

Scoring is performed **independently by two reviewers**, with disagreements adjudicated and inter-rater agreement reported. Because "genuinely attributable" is the judgement on which the whole procedure turns, the scoring rubric is agreed and documented before tracing begins, with worked examples of each category.

**Change-control limb.** Independently of tracing, the reviewer reconstructs the workflow's architecture change history over the review period — every point at which an intermediate agent, automation step or delegation was added or altered — and tests whether the accountability map was updated at each. A map that has not moved while the workflow has is a direct Fail indicator.

**Record-granularity limb.** Approval records are examined for whether they capture the identity of each **material contributing step** — human and specific agent instance/version — or only the final sign-off.

### Steps
1. Obtain the accountability map, SM&CR mapping and workflow documentation. Record whether accountability is documented at decision level, workflow-stage level, or system level only.
2. Agree and document the three-point scoring rubric with worked examples, before tracing begins.
3. Select the decision sample per workflow, stratified as designed.
4. Trace each decision end to end. For each, record the full contributing chain in order, with the evidence source for each link (log entry, approval record, agent invocation record).
5. Score each case independently by two reviewers; adjudicate disagreements; record inter-rater agreement.
6. For every case scored "not attributable" or "attributable with ambiguity", record precisely where in the chain attribution broke down — this converts a score into an actionable finding.
7. **Change-control limb:** reconstruct the workflow architecture change history from change-control records. For each material change, determine whether the accountability map was updated, and on what date relative to the change. Record the gap.
8. **Record-granularity limb:** for the sampled decisions, record whether approval records capture each material contributing step with agent instance and version identifiers, or only the final human sign-off.
9. Review SM&CR mapping: does it reference specific decision types and workflow stages, or only the system as a whole?
10. Where a real historical incident or complaint investigation exists for this workflow, review whether it was able to identify an accountable individual, and how long that took.
11. Report per workflow.

### Observations & measures
- **Attribution score distribution** per workflow — proportions clearly attributable / attributable with ambiguity / not attributable. Canvas thresholds: the **large majority** clearly attributable, and **no** sampled decision scored "not attributable". The "large majority" figure is not numerically defined in any cited source — **reviewer judgement**, basis recorded; the zero-tolerance on "not attributable" is explicit in the canvas.
- **Inter-rater agreement** on scoring — reported so the reliability of the central judgement is visible.
- **Breakdown-point analysis** — where in the chain attribution fails, by frequency. Diagnostic; no threshold.
- **Change-control alignment** = material workflow changes with a corresponding accountability-map update ÷ material workflow changes. Canvas threshold: the map has been **demonstrably updated at every** material architecture change in the review period.
- **Record granularity** (binary): approval records capture each material contributing step including agent instance/version / final sign-off only. Canvas Fail condition: the latter.
- **SM&CR specificity** (categorical): references specific decision types and workflow stages / system level only. Canvas Fail condition: system level only, with no decision-level or workflow-stage mapping.
- **Historical incident outcome** (where applicable, binary): an accountable individual was identified / was not. Canvas Fail condition: a real investigation was unable to identify one.

### Interpretation
- **Pass** — the large majority of sampled decisions are clearly attributable; no decision is scored "not attributable"; the accountability map was updated at every material workflow architecture change in the review period; approval records capture each material contributing step including specific agent instance and version, not only the final sign-off; SM&CR mapping references specific decision types and workflow stages. Report with the ★2 caveat that "genuinely attributable" is an assessor judgement and the scoring rubric should be published alongside the result.
- **Fail** — a material proportion of sampled decisions score "not attributable" or "attributable with ambiguity"; **or** the accountability map has not been updated despite one or more material workflow changes; **or** approval records capture only the final sign-off with no attribution for intermediate agent/automation contributions; **or** accountability documentation exists only at system level; **or** a real historical incident investigation for this workflow could not identify an accountable individual.
- **Partial** — tracing scores well and records are granular, but the accountability map lags one recent architecture change, or SM&CR mapping is decision-specific for the primary workflow only. State the gap and the specific workflow affected.

### Evidence outputs
- E1 Governance paper naming a senior manager accountable for "the AI system", as provided — **L1** (system-level only; explicitly labelled).
- E2 Decision-level accountability map for each in-scope workflow — **L2**.
- E3 Scoring rubric with worked examples, documented before tracing — **L3**.
- E4 Trace records: full contributing chain per sampled decision with evidence source per link — **L3**.
- E5 Scored results with inter-rater agreement and adjudication record — **L3**.
- E6 Breakdown-point analysis — **L3**.
- E7 Workflow architecture change history reconstructed from change-control records, with accountability-map update alignment — **L3**.
- E8 Record-granularity findings — **L3**.
- E9 SM&CR mapping specificity assessment — **L2**.
- E10 Independent audit tracing real historical decisions through the actual multi-agent workflow, where performed — **L4**.
- E11 Historical SM&CR-related enforcement or internal-investigation outcome referencing this workflow — **L5**.

### Common pitfalls & limitations
- **Tracing on paper rather than in the logs.** The accountability map says who *should* be accountable. The trace establishes whether the records actually support it. Where the two diverge, the records govern.
- **No pre-agreed rubric.** "Genuinely attributable" without a documented rubric is an unexaminable judgement, and the ★2 rating becomes ★1 in substance. Agree it and publish it.
- **Single-reviewer scoring.** The central judgement of this procedure needs an inter-rater check.
- **Skipping the change-control limb.** It is the limb that catches the common real-world pattern: a correct map, drafted at go-live, that has not moved while three agents were added to the workflow.
- **Accepting agent-level attribution as accountability.** "The triage agent decided" is not a named individual. Note also that agent instance and version identifiers are required *in addition to* human attribution, not instead of it.
- **Sampling only clean paths.** Stratify to include complex and exception paths, which is where attribution breaks.
- **Confusing this with TP-HUM-004.** That procedure asks whether the human checkpoint is positioned effectively; this asks whether, after the fact, a named person is accountable. A workflow can pass one and fail the other.
- **★2 honesty.** Trace sampling is established audit practice; applying it to multi-agent delegation chains is not. Report as professional assessment.

### Time/effort estimate
**4.0 reviewer-days** — 0.5 documentation review and rubric agreement; 1.5 trace execution across the sample (the dominant cost; scales with workflow count and chain length); 0.5 dual scoring and adjudication; 0.75 change-control reconstruction; 0.25 record-granularity and SM&CR review; 0.5 historical-incident review and write-up. Add 1.0 day per in-scope workflow beyond two.

---
---

