# TP-TPR-008 — AI Provider Concentration Risk Measurement Review

**IRQ:** IRQ-TPR-008 — Excessive Model/Cloud/GPU Provider Concentration Risk.
**Assurance objective:** AO-TPR-008 — the firm shall measure aggregate concentration of AI-related dependence on model, cloud and GPU providers across its full AI inventory, compare this against a board-stated risk appetite, and maintain credible, tested substitution options where concentration exceeds appetite.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — DORA's critical-ICT-provider concentration concept provides regulatory grounding, but firm-level aggregate AI-specific concentration measurement has no standardised calculation approach; professional judgement dominates the aggregation methodology, and the method used must therefore be stated explicitly so it can be challenged.

### Preconditions
- The **full AI inventory** (per IRQ-GOV-002), enlarged by TP-TPR-003's findings. This procedure is only as good as the inventory it aggregates, so the inventory's completeness — established at the start of the domain — is a stated dependency and a stated limitation.
- The firm's **risk appetite statement**, and specifically whether it contains measurable concentration indicators or thresholds specific to AI providers.
- For each AI-dependent business activity: the model provider, the hosting cloud, and — where the firm operates its own inference — the GPU/compute provider.
- Substitution and exit strategy documentation, and evidence of any testing of it.
- Board or risk committee MI over the last 12 months showing concentration reporting.
- Personnel: lead reviewer; firm third-party risk manager; enterprise architect for the shared-dependency tracing limb; risk function contact for appetite and MI.

### Test design
**Aggregation limb.** Using the AI inventory, the reviewer independently aggregates provider dependency across **three layers**: model, cloud and GPU/compute. Concentration is calculated as the canvas suggests — the proportion of AI-dependent business activities reliant on a single provider at each layer — and compared against the stated appetite.

Because no standardised method exists, the reviewer **states the aggregation method explicitly**: the unit of analysis (business activity, not system, per the canvas's formulation), how a business activity dependent on multiple providers is counted, and how materiality weighting (if any) is applied. Two defensible methods can yield materially different figures; publishing the method is what makes the result challengeable rather than assertive.

**Shared-dependency tracing limb — the analytical core.** Apparently diversified choices frequently collapse to a common underlying dependency: two "different" model providers both hosted on the same cloud; two clouds both dependent on the same GPU supply; a specialist vendor that is itself an API wrapper over a frontier provider already counted elsewhere. The reviewer traces each apparently independent dependency to its underlying infrastructure and re-computes concentration on the traced basis. The difference between the naive and traced figures is usually the finding.

**Appetite limb.** Establish whether the risk appetite statement contains a **measurable** concentration indicator specific to AI providers, or only a qualitative statement. A qualitative appetite cannot be breached, which means it cannot trigger escalation — a distinct finding from the concentration level itself.

**Substitution limb.** For at least the most concentrated dependency, establish whether a substitution or exit strategy exists and whether it has been **tested** — even at desk-based walkthrough level. The canvas Fail condition is a documented strategy never tested even at walkthrough level, so the bar here is low and failing it is telling.

**MI limb.** Review board or risk committee MI over 12 months: is concentration measured and reported against appetite on a regular cadence, and were any breaches escalated with a remediation plan?

### Steps
1. Obtain the AI inventory and confirm its completeness basis, including TP-TPR-003's findings. Record the inventory's known limitations as a stated constraint on everything that follows.
2. Obtain the risk appetite statement; record whether it contains measurable AI-specific concentration indicators or thresholds, and what they are.
3. Define and document the aggregation method before computing: unit of analysis, multi-provider treatment, materiality weighting. Record the rationale.
4. Build the dependency table: for each AI-dependent business activity, record model provider, cloud, and GPU/compute provider.
5. Compute naive concentration at each layer.
6. **Shared-dependency tracing:** for each apparently independent dependency, trace to its underlying infrastructure with the enterprise architect. Record the trace for each. Identify model providers hosted on shared cloud, specialist vendors reselling frontier APIs, and shared GPU supply.
7. Re-compute concentration on the traced basis. Report both figures and the difference.
8. Compare both figures against the stated appetite thresholds. Record any breach and whether it has been escalated.
9. **Substitution limb:** for the most concentrated dependency, obtain the substitution/exit strategy and any test evidence. Assess whether it is credible — is the substitute technically viable, contractually available, and dimensioned for the volume?
10. **MI limb:** review 12 months of board/risk committee MI for concentration reporting against appetite and any breach escalations.
11. Report the concentration profile by layer, with the method stated.

### Observations & measures
- **Naive concentration by layer** — proportion of AI-dependent business activities reliant on the largest single provider at model, cloud and GPU layers.
- **Traced concentration by layer** — the same, after shared-dependency tracing. The difference between naive and traced is reported explicitly.
- **Appetite comparison** — traced concentration versus stated threshold per layer. Canvas threshold: **no single provider at any layer exceeds the stated concentration threshold**, or breaches are escalated with a remediation plan. Where no measurable threshold exists, no comparison is possible and that is the finding.
- **Appetite measurability** (binary): risk appetite statement contains a measurable concentration indicator specific to AI providers / qualitative only. Canvas Fail condition: no measurable indicator.
- **Aggregate measurement existence** (binary): aggregate concentration measured and reported / risk assessed only per-system. Canvas Fail condition: no aggregate measurement; assessment per-system only.
- **Substitution testing** (categorical): substitution/exit strategy exists and has been tested / exists but never tested even at desk-based walkthrough level / does not exist. Canvas Fail condition: documented but never tested even at walkthrough level.
- **Shared-dependency check** (binary): the firm itself checks "diversified" choices for shared underlying dependencies / assumes independence. Canvas pass indicator requires the firm to perform this check, not merely the reviewer.
- **MI cadence** = periods with concentration reported against appetite ÷ periods in the 12-month window.

*No FAIAS numeric threshold applies to concentration itself — the threshold is the firm's own board-stated appetite, and where none exists that absence is the finding.*

### Interpretation
- **Pass** — aggregate concentration is measured and reported against a board-approved appetite on a regular cadence; no single provider at model, cloud or GPU layer exceeds the stated threshold, or breaches are escalated with a remediation plan; substitution/exit strategies exist and have been tested for at least the most concentrated dependency; the firm itself checks apparently diversified provider choices for shared underlying dependencies rather than assuming independence. Report with the ★2 caveat that the aggregation method is professional judgement and must be read alongside the stated method.
- **Fail** — no aggregate concentration measurement exists and risk assessment is conducted only per-system; **or** the risk appetite statement contains no measurable concentration indicator specific to AI providers; **or** a dominant provider exceeds any reasonable concentration threshold with no escalation or remediation plan on record; **or** the substitution/exit strategy, where documented, has never been tested even at desk-based walkthrough level.
- **Partial** — aggregate measurement exists and is reported, but the firm does not trace shared underlying dependencies (so its reported figure understates concentration by a stated margin), or substitution testing has been performed for the model layer only. Quantify the understatement where the tracing limb established it.

### Evidence outputs
- E1 Assertion that "we use multiple providers so we are diversified" with no supporting data — **L1** (explicitly labelled).
- E2 Risk appetite statement with measurability assessment — **L2**.
- E3 AI inventory completeness basis and stated limitations — **L2/L3**.
- E4 Documented aggregation method with rationale, recorded before computation — **L3**.
- E5 Dependency table across model, cloud and GPU layers for each AI-dependent business activity — **L3**.
- E6 Naive and traced concentration computations with the difference — **L3**.
- E7 Shared-dependency trace records per apparently independent dependency — **L3**.
- E8 Appetite comparison and breach/escalation findings — **L3**.
- E9 Substitution/exit strategy documentation and test evidence — **L2/L3**.
- E10 Independent audit or second-line review confirming the concentration measurement methodology and its accuracy against a sample of the inventory, where held — **L4**.
- E11 Board or risk committee MI showing concentration measured and reported against appetite over the last 12 months, including breach escalations — **L5**.

### Common pitfalls & limitations
- **Aggregating an incomplete inventory.** This procedure inherits every gap in the AI inventory, and TP-TPR-003 exists partly to bound that. State the limitation prominently; a concentration figure computed on a partial inventory understates concentration systematically, because undiscovered embedded AI tends to sit with the same dominant vendors.
- **Not stating the aggregation method.** Without it the figure is an assertion. State it, and state that a different defensible method would yield a different number.
- **Counting systems rather than business activities.** The canvas's formulation is business activities, which is the risk-relevant unit — ten low-materiality systems on one provider is a different exposure from one critical service.
- **Stopping at the naive figure.** The shared-dependency trace is the analytical value of the procedure and is where the "we are diversified" assertion usually fails.
- **Assessing concentration against the reviewer's own view of what is excessive.** The threshold is the firm's board-stated appetite. Where none exists, report the absence as the finding rather than substituting a number FAIAS has no basis to set.
- **Desk-based substitution walkthroughs treated as adequate.** They meet the canvas's minimum bar, but a walkthrough that has never considered volume, contractual availability or technical viability is thin — note the quality, not just the existence.
- **★2 honesty.** DORA grounds the concept; the AI-specific firm-level aggregation is emerging practice. Report as professional assessment with the method exposed.

### Time/effort estimate
**3.0 reviewer-days** — 0.25 inventory and appetite review; 0.25 aggregation method definition; 0.75 dependency table construction; 0.75 shared-dependency tracing with the enterprise architect (the analytical core, and the limb most worth protecting if time is short); 0.25 appetite comparison; 0.5 substitution and MI limbs; 0.25 write-up.

---
---

