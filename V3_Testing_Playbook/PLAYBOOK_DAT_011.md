# TP-DAT-011 — Injected Drift Detection Across Three Drift Classes

**Procedure ID:** TP-DAT-011
**IRQ:** IRQ-DAT-011 — Undetected Statistical, Semantic and Source Drift in Model Inputs
**Assurance objective:** AO-DAT-011 — statistical, semantic and source drift in model inputs shall be detected against defined baselines, including unannounced upstream reference-data changes, before performance degradation accumulates to a material level.
**★ Confidence:** ★3 (carried from canvas — statistical and concept-drift detection methods are published, well-established and used by multiple independent groups; source-change/schema-drift detection specifically is less standardised, keeping the combined test just short of ★4)
**Method classification:** Established/Adapted — two-sample-test shift detection (Rabanser et al., 2019) and the concept-drift taxonomy (Gama et al., 2014), both as cited in the canvas; source-change detection is tested against whatever contractual/technical notification mechanism exists and is **bespoke**.

## Preconditions

- **Environment:** non-production replica of the input pipeline and the drift-monitoring stack, with the firm's live baselines and alerting configured. Alerts must route to a test destination, not to the production on-call rota.
- **Access needed:** monitoring configuration and baselines; input stream replica; alerting configuration; drift response playbooks; upstream data-provider contracts.
- **Artefacts requested in advance (2 weeks):** the drift-monitoring design (which features, which statistics, which thresholds); documented time-to-alert SLA; drift response playbook; historical drift events with detection and remediation timelines; upstream provider contract clauses on schema/definition change notification.
- **Personnel:** reviewer (lead); monitoring/platform engineer; the model owner who would receive an alert (for the response-path step); vendor management for contract clauses.

## Test design

- **Three drift classes injected (per canvas):**
  - **(a) Statistical** — a distribution shift in a key feature, injected gradually (e.g. a progressive population-mix change over simulated time) and, separately, abruptly. Gradual injection is the harder and more realistic case.
  - **(b) Semantic/concept** — a categorical field's meaning silently changes with no schema-level signal (e.g. a code that previously meant one thing now means another, same values, different referent).
  - **(c) Source** — an upstream reference feed changes units or scale (e.g. a value expressed in a different denomination), with no announcement.
- **Magnitude tiers:** inject each class at three magnitudes (subtle, moderate, obvious) — a reviewer-set design minimum, disclosed at scoping. Detection at the obvious tier only is a meaningful partial finding, not a pass.
- **Measures:** detection latency (queries processed and elapsed time to alert) and false-negative rate per class per tier.
- **Control:** a no-drift period run through the same monitoring, to measure false-positive alerting.
- **Benign-payload principles:** all injected data is synthetic; no production feeds are altered; alerting is routed to a test destination.

## Steps

1. Confirm the replica monitoring stack matches production configuration (features monitored, statistics, thresholds, baselines). **Record:** configuration diff, and any monitoring component not replicated.
2. Record the documented time-to-alert SLA. Where none exists, record *no SLA defined*.
3. Run the no-drift control period. **Record:** any alerts raised (false positives) and the baseline alert volume.
4. Inject statistical drift at each magnitude tier, gradually and abruptly. **Record:** injection start, magnitude, alert raised yes/no, time and query count to alert.
5. Inject semantic/concept drift at each tier. **Record:** as above. Note specifically whether **any** signal fires — the canvas fail indicator anticipates that semantic drift is commonly uncovered entirely.
6. Inject source drift (units/scale change) at each tier. **Record:** as above, plus whether the change would have been caught by a schema check rather than a statistical one.
7. For each alert raised, follow the response path: does it trigger the documented playbook, or is it a passive dashboard entry? **Record:** the routing outcome, the recipient, and whether an action was defined.
8. Review historical drift events: for each, record time-to-detection and time-to-remediation, and whether detection came from monitoring or from a complaint/outcome audit. **Record:** the event timeline table.
9. Review upstream provider contracts for schema/definition-change notification obligations. **Record:** clause references or absence, per provider.
10. Reset the replica; confirm removal of injected data.

## Observations & measures

| Measure | Threshold | Basis |
|---|---|---|
| Detection of each drift class | All three classes detected within the documented time-to-alert SLA (canvas pass indicator) | Canvas; firm-defined SLA |
| Detection latency per class per tier | Against the firm's SLA; **reviewer judgement — no established cross-industry threshold** | Canvas |
| False-negative rate per class | Report per class and tier; **no established threshold** | Bespoke |
| False-positive rate (control period) | Report as context; **no established threshold** | Bespoke |
| Alert leads to a defined governance response | Documented playbook invoked, not a passive dashboard entry (canvas pass indicator) | Canvas |
| Upstream providers contractually/technically obliged to notify changes | Obligation present (canvas pass indicator) | Canvas |

## Interpretation

- **Pass** — all three drift classes detected within the documented SLA in staging; alerts trigger a defined governance response; any historical drift event shows acceptable time-to-detection and time-to-remediation; upstream providers are obliged to notify schema/definition changes.
- **Fail** — one or more classes (commonly semantic or source) undetected or detected only after material lag; monitoring covers statistical drift only; no defined response playbook, alerts logged but not acted upon; a historical drift event shows a long undetected period before discovery via complaint or outcome audit rather than monitoring.
- **Partial** — the canvas-anticipated shape: statistical drift well covered, semantic and source drift covered weakly or not at all. Report by class and magnitude tier. Detection only at the obvious tier is partial, not pass.

## Evidence outputs

| Output retained | Evidence level |
|---|---|
| Monitoring configuration diff vs production | L3 |
| Injection plan (class × tier × timing) and injected data manifest | L3 |
| Alert logs with timestamps and query counts | **L4** |
| Detection latency and false-negative/false-positive tables | L4 |
| Response-path trace per alert (routing, recipient, action) | L4 |
| Historical drift event timeline table | L5 (operational evidence from production history) |
| Upstream provider contract extracts | L2 |

## Common pitfalls & limitations

- **Injecting only abrupt drift.** Gradual drift is both more realistic and much harder to detect; an abrupt-only test overstates capability.
- **Alerts routed to production on-call.** Operationally disruptive and reputationally damaging to the review. Confirm test routing before injection.
- **Semantic drift injected with a schema signal attached.** If the field type or name changes, it is no longer a silent semantic drift. Keep values and schema constant; change only meaning.
- **Stopping at alert generation.** The canvas fail indicator is about alerts that are logged but not acted upon — step 7 is not optional.
- **Canvas limitation carried forward:** source-change/schema-drift detection is materially less standardised than statistical drift detection, which is precisely why the combined test sits just short of ★4. Report the source-drift conclusion with more caution than the statistical one.
- **Replica fidelity.** Monitoring stacks are frequently simpler in staging than production; any component not replicated limits the conclusion.

## Time/effort estimate

**4 reviewer-days** (0.5 configuration confirmation; 0.5 injection design; 1.5 injection and observation across three classes and three tiers; 0.5 response-path and historical review; 0.5 contract review; 0.5 analysis and reporting).

---
---

