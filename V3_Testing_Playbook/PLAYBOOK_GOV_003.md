# TP-GOV-003 — Conditions-of-Use Enforcement Reconciliation

## 1. Procedure Identity
**Procedure ID:** TP-GOV-003
**IRQ:** IRQ-GOV-003 — Approval Conditions Stated but Not Technically Enforced or Monitored
**Assurance objective:** AO-GOV-003 — Approval conditions and usage restrictions shall be technically enforced in the deployed platform and independently monitored for breach, such that actual use cannot silently diverge from the approved scope.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established configuration-audit methodology adapted from IT/cyber control testing; no AI-specific standard defines what "sufficient" technical enforcement looks like for GenAI conditions of use, so professional judgement determines adequacy.
**Method classification:** Adapted Industry Practice — as-designed vs as-configured configuration audit, extended to AI-specific conditions of use.

## 2. Preconditions
**Environment:** Configuration review plus a staging replica for the boundary-exercise component. The out-of-scope attempt is performed in staging only; no production data is exercised.
**Access required:** Read access to approval papers; read access to platform configuration (access control lists, system prompt and guardrail settings, tool permission grants); read access to usage logs (production or production-representative); a staging replica in which out-of-scope attempts can be made.
**Artefacts required:** Approval papers with stated conditions of use; current configuration exports; usage logs for the review period; change records for any configuration change to task-scoping; monitoring definitions for out-of-scope use detection.
**Personnel required:** Platform administrator; the system owner; reviewer.
**Data handling:** Usage logs may contain prompt content and therefore customer or confidential data. Request metadata-level extracts (task type classification, user identity, timestamp) rather than full prompt text wherever the reconciliation can be performed on metadata. Where prompt content must be inspected to classify task type, restrict to a small sample, review in situ under the firm's supervision, and do not export.

## 3. Test Design
Three limbs, in ascending order of evidential weight:

- **Limb A — as-designed vs as-configured.** Compare each stated approval condition against the corresponding platform configuration. Conditions typically fall into three classes: who may use it (ACLs/access groups), what it may be used for (system prompt, guardrails, task scoping), and what it may do (tool permission grants). Each class must be checked separately.
- **Limb B — as-configured vs as-used.** Reconcile a sample of actual usage events against the approved scope, flagging out-of-scope task types or user identities.
- **Limb C — boundary exercise.** In the staging replica, attempt an out-of-scope task type and attempt access as a non-approved user role. This tests whether the control is technical or merely declaratory — the distinction the IRQ exists to make.

Limb C is the highest-yield limb and the one most often omitted from firms' own assurance. A condition of use enforced only by staff training is L1/L2 evidence and, per the canvas, a fail indicator.

Sample: risk-based, weighted to Tier 2–3, minimum six systems (reviewer-set design minimum, disclosed at scoping).

## 4. Steps
1. Draw and record the sample. **Record:** basis, size, weighting.
2. For each sampled system, extract every stated condition of use from the approval paper and classify it as who / what-for / what-it-may-do. **Record:** the condition list per system; conditions that are unenforceable as written (vague or aspirational) are recorded as such.
3. **Limb A.** Obtain the current configuration export and compare each condition to its corresponding configuration setting. **Record:** condition-by-condition, whether configuration matches, exceeds (broader access than approved) or is absent (no corresponding control configured).
4. Specifically check access groups against the approved user population. **Record:** any group with access that was not in the approval.
5. Specifically check tool permission grants against the approved capability set. **Record:** any tool or integration granted beyond approval.
6. **Limb B.** Obtain usage logs for the review period and classify a sample of events against the approved task-type scope. **Record:** sample size and method; out-of-scope events by count and proportion; out-of-scope user identities.
7. For any material out-of-scope volume found, search governance records for awareness or action. **Record:** whether governance knew; what action followed.
8. **Limb C.** In the staging replica, attempt at least two out-of-scope actions per sampled system: one out-of-scope task type and one access attempt as a non-approved user role. Use benign, non-sensitive test content only. **Record:** whether the attempt was blocked, flagged or silently permitted; verbatim system response.
9. Review the monitoring design for conditions-of-use drift. **Record:** whether any mechanism exists to detect out-of-scope use, or whether the first indication would be an incident.
10. Search for at least one documented instance of the monitoring mechanism detecting and triggering remediation of an out-of-scope use. **Record:** the instance or its absence.
11. Review change records for task-scoping configuration. **Record:** whether changes are logged and traceable to an approved change record.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Configuration matches approval conditions | 100% of sample across access groups, task scoping and tool permissions | Categorical per canvas pass indicator |
| Staging out-of-scope attempts blocked or flagged | 100%; silent permission is a fail indicator | Categorical per canvas |
| Out-of-scope usage volume in logs | Reviewer judgement on materiality — no established threshold; any material volume with no governance awareness is a fail indicator | Per canvas; no AI-specific standard defines "sufficient" enforcement |
| Monitoring mechanism has detected a real instance | ≥1 documented instance | Categorical per canvas pass indicator |
| Configuration changes traceable to approved change records | 100% | Categorical per canvas pass indicator |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: configuration for 100% of the sample technically matches the approval paper's conditions; staging out-of-scope attempts are blocked or flagged; log reconciliation finds no material out-of-scope volume; at least one documented instance exists of monitoring detecting and triggering remediation; and task-scoping configuration changes are logged and traceable.

**Fail** where: configuration does not match the approval paper (broader access than approved, or no task-scoping guardrail actually configured); staging out-of-scope attempts succeed without block or flag; log reconciliation finds material out-of-scope use with no governance awareness; enforcement relies solely on training/policy with no technical control; or no drift-detection mechanism exists.

**Partial** where access-group conditions are technically enforced but task-scope conditions are not — the common pattern, since access control is a mature capability and task scoping for generative systems is not.

## 7. Evidence Outputs
- Approval papers and configuration exports as obtained — **L2**
- Condition-by-condition reconciliation matrix (Limb A) — **L3**
- Usage log classification results (Limb B) — **L3**
- Staging boundary-exercise log with verbatim responses (Limb C) — **L3**
- Reviewer's independent enforcement-adequacy assessment — **L4**
- Records of real out-of-scope detections and remediations — **L5**

## 8. Common Pitfalls & Limitations
- **Testing against the policy rather than the configuration.** The whole point is the gap between them.
- **Full prompt-log extraction.** Unnecessary and creates a data-handling exposure. Work on metadata where possible; inspect content in situ.
- **Omitting Limb C.** Without it, the procedure cannot distinguish a technical control from a policy statement.
- **Aggressive boundary attempts.** Use benign test content. The objective is to establish whether a boundary exists, not to breach a system.
- **Vague approval conditions.** Where a condition cannot be tested because it was written aspirationally ("used responsibly"), that is a finding about the approval process, and should be cross-referenced to TP-GOV-009.
- **Overlap with TP-GOV-012.** GOV-003 tests enforcement of stated conditions; GOV-012 tests whether the effective envelope has drifted across six vectors. Run GOV-003 first; its findings feed GOV-012.

## 9. Time / Effort Estimate
**4 reviewer-days**: 0.5 day sampling and condition extraction, 1 day configuration reconciliation, 1 day usage log classification, 1 day staging boundary exercises, 0.5 day working papers.

---
---

