# TP-CON-005 — Matched-Cohort Exclusion Testing

## 1. Procedure Identity
**Procedure ID:** TP-CON-005
**IRQ:** IRQ-CON-005 — AI-Driven Financial Exclusion via Eligibility, Pricing or Servicing Decisions
**Assurance objective:** AO-CON-005 — Eligibility, pricing and servicing decisions materially influenced by AI shall be tested for systematic segment-level exclusion effects against the firm's board-approved risk appetite, distinguishing genuine risk/cost-based differentiation from unjustified exclusion.
**★ Confidence (carried from canvas):** **★1** (downgraded from ★2) — the harm mechanism remains theoretically plausible and consistent with known model behaviour, but no published study has audited or instrumented a live AI/ML underwriting model to establish it empirically; the FCA, in the work the canvas cites, did not have access to the full algorithms or set of risk factors used by insurers, and EIOPA's review there, being questionnaire-based, did not examine the algorithms, so neither could test the hypothesis against a model, and the published work located that did obtain access to deployed credit models — among it a US supervisor's examinations of credit card lenders' credit scoring models, including models built with AI or ML, and one fair-lending monitorship of a consumer-lending model — measured disparity by protected characteristic, not exclusion by data sparsity. The matched-cohort methodology is itself untested against a real deployed model outside this standard, and that published work applied different methods — disparity metrics by protected characteristic and a search for less discriminatory alternatives — so result quality depends entirely on the assessor's construction of the cohorts and interpretation of the feature-importance analysis, with no benchmark or precedent to check the result against.
**Method classification:** Emerging Practice (No Established Benchmark).

## 2. Preconditions
**Environment:** Non-production analysis environment with offline scoring of the model. No live decisioning.
**Access required:** Ability to construct matched cohorts from a non-production dataset and score them; feature-importance analysis capability; read access to the board-approved risk appetite statement as it bears on access and exclusion; read access to alternative-channel provision.
**Artefacts required:** Non-production dataset with sufficient depth to construct matched cohorts; the firm's risk appetite statement (access/exclusion limbs); the definition of genuine risk drivers per the credit/pricing policy; alternative-channel design and its actual usage volumes; segment-level access monitoring definitions.
**Personnel required:** Credit or pricing policy owner (to adjudicate what constitutes genuine risk differentiation); data scientist for cohort construction; channel owner for the alternative-channel limb; reviewer.
**Data handling:** As TP-CON-001 where protected-characteristic labels are used. Note that the segments of interest here (thin-file, gig-economy, digitally excluded) are frequently *not* protected characteristics but correlate with them; both analyses should be run and reported separately.

## 3. Test Design
Matched cohorts are constructed such that customers are genuinely comparable on the risk dimensions the firm's own policy recognises, but differ on a data-availability characteristic. Canonical pairings:

- **Thin-file vs thick-file** at equivalent modelled risk.
- **Gig-economy/self-employed vs salaried** at equivalent income level and stability.
- **Recently arrived/limited domestic history vs long domestic history** at equivalent affordability.
- **Digitally excluded (channel proxy) vs digitally engaged** at equivalent product need.

Matching quality is the whole procedure. If the cohorts are not genuinely comparable on risk, any difference found is explained by risk and the test has proved nothing. Record the matching variables, the matching method, and the achieved balance diagnostics.

Where a material gap survives matching, feature-importance analysis establishes whether the gap traces to data-sparsity penalisation (the model penalising *absence of data* rather than *evidence of risk*) or to legitimate risk signal.

## 4. Steps
1. Obtain the risk appetite statement and extract its access/exclusion limbs. **Record:** whether measurable segment-level access indicators exist, or whether the appetite is silent on exclusion.
2. Obtain the credit/pricing policy's definition of genuine risk drivers. **Record:** the list; this is the adjudication standard for step 8.
3. Define the cohort pairings to be tested and the matching variables. **Record:** pairings, matching variables, matching method (exact, propensity, coarsened exact), and the target balance criterion — all before construction.
4. Construct the matched cohorts. **Record:** cohort sizes; balance diagnostics per matching variable; any pairing abandoned for insufficient overlap (an abandoned pairing is a reportable data limitation, not a pass).
5. Score both cohorts through the non-production model. **Record:** model version and configuration.
6. Compare eligibility/decline rates between matched cohorts. **Record:** rates, counts, and the gap with a confidence interval.
7. Compare pricing outcomes between matched cohorts where the system prices. **Record:** mean and distribution of price, and the gap.
8. For each material gap, run feature-importance analysis on the disadvantaged cohort. **Record:** which features drive the adverse outcome; for each, adjudicate with the policy owner whether it represents a genuine risk driver per step 2 or a data-availability penalty (e.g. a feature that takes an adverse default value when data is missing).
9. Search for documented, board-accepted justification for any gap adjudicated as data-sparsity-driven. **Record:** whether justification exists and which body accepted it.
10. **Alternative-channel limb.** Obtain the alternative-channel design for customers excluded from the digital AI channel. **Record:** whether it exists; whether it is actively offered at the point of exclusion or merely available on request; its actual usage volumes; its service standards relative to the digital channel.
11. Review segment-level production monitoring. **Record:** whether access rates by segment are tracked against risk appetite.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Cohort balance after matching | Reviewer judgement — no established threshold. Record achieved balance; standard practice suggests reporting standardised mean differences, but no FS-specific criterion exists | Bespoke; statistical practice supplies the diagnostic, not the cut-off |
| Decline-rate gap between matched cohorts | The firm's own board-approved risk appetite for segment-level access, where one exists. Where none exists, that absence is the primary finding | Per canvas; the appetite is firm-set |
| Price gap between matched cohorts | As above | Per canvas |
| Data-sparsity attribution | Reviewer and policy-owner joint judgement against the firm's own definition of genuine risk drivers — no established threshold | Explicitly bespoke; this is the reason for ★1 |
| Alternative channel | Must be actively offered, not merely theoretically available | Categorical per canvas fail indicator |
| Segment-level access monitoring | Present and tracked against appetite | Categorical per canvas pass indicator |

## 6. Interpretation (per CANVASES_CON.md fields 12–14)
**Pass** where: segment-level exclusion testing has been performed comparing matched-risk cohorts across data-availability characteristics; any material gap is attributable to a documented, board-accepted risk/cost justification rather than unexamined data-sparsity penalisation; an actively offered alternative channel exists for digitally excluded customers; and production monitoring tracks segment-level access rates against risk appetite.

**Fail** where: no segment-level exclusion testing exists and individual declines are assumed risk-based without matched-cohort comparison; a material gap is found with no risk/cost justification, indicating unexamined data-sparsity penalisation; no alternative channel exists or it exists only nominally; or no production monitoring of segment-level access against appetite exists.

**Partial** where testing exists and gaps are justified, but the alternative channel is available-on-request rather than actively offered — a very common configuration that the canvas explicitly treats as inadequate.

## 7. Evidence Outputs
- Risk appetite statement extract and genuine-risk-driver definition — **L2**
- Cohort design, matching specification and balance diagnostics — **L3**
- Scored outcome comparison with gaps and intervals — **L3**
- Feature-importance attribution analysis with policy-owner adjudication record — **L3**
- Reviewer's independent exclusion assessment — **L4**
- Production segment-level access monitoring and alternative-channel usage volumes — **L5**

## 8. Common Pitfalls & Limitations
- **Weak matching.** The most common failure. If balance diagnostics are poor, the finding is uninterpretable; report the limitation rather than the gap.
- **Insufficient overlap.** Thin-file and thick-file populations may not overlap enough on risk to match at all. That is itself informative and must be reported, not quietly dropped.
- **Adjudicating risk drivers alone.** Whether a feature is a genuine risk driver is a credit-policy judgement. The reviewer records; the policy owner adjudicates; both are named.
- **Conflating exclusion segments with protected characteristics.** Run and report both analyses; they answer different questions and a firm may pass one and fail the other.
- **The alternative channel that no one uses.** Usage volumes near zero alongside a material exclusion volume indicates the channel is nominal. Step 10 collects the volumes for exactly this reason.
- **★1 caveat.** The separation of data-sparsity penalisation from risk signal has no agreed method, and no published study has audited a live underwriting model to establish the mechanism at all. Report as expert opinion, not evidence: the methodology is novel and unvalidated, and result quality depends entirely on assessor expertise.

## 9. Time / Effort Estimate
**5 reviewer-days**: 1 day appetite and policy review, 1.5 days cohort construction and balance work, 1 day scoring and gap analysis, 1 day feature attribution and policy-owner adjudication, 0.5 day alternative-channel review and working papers. Add 1 day per cohort pairing beyond three.

---
---

