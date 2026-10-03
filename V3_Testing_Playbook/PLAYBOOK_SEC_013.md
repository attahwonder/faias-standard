# TP-SEC-013 — AI-as-Control Efficacy Testing Against Adversarially Evolved Inputs

**IRQ:** IRQ-SEC-013 — AI-as-Control Efficacy Under Adversarial Evolution (subdomain E.6).
**Assurance objective:** AO-SEC-013 — where an AI system functions as a detection or screening control, its detection rate and residual miss rate shall be tested against adversarially evolved inputs mapped to a recognised adversarial-ML taxonomy, in addition to historical case-library testing, and re-tested on a defined cadence as adversary technique evolves.
**Confidence:** ★2 (carried unchanged). Method class: Adapted Industry Practice — test-set construction mapped to NIST AI 100-2e2025, *Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations* (March 2025), evasion-attack categories, and, where applicable, MITRE ATLAS case-study techniques (16 tactics, 84 techniques and 42 real-world case studies as of the November 2025 release). The canvas's own basis for the rating: two mature, current, actively maintained public taxonomies exist and are directly applicable to test-set construction, but **no financial-services-specific quantitative benchmark or acceptance threshold exists on top of them**, so the tolerance for an acceptable miss-rate uplift rests on the assessor's own risk-based judgement, not a published standard. The re-test cadence control is marked Emerging Practice in the canvas's control list — no published cross-institution benchmark fixes a re-test interval.

### Preconditions
- **Applicability.** In scope where an AI system functions as a control — fraud detection, AML or transaction monitoring, surveillance, screening, or promotion/content approval gating. Where the system is not performing a detection or screening function, this procedure does not apply.
- **Two boundary distinctions, applied before scoping.** This procedure is **not** an attack on the model's own instruction-following — that is TP-SEC-001 and TP-SEC-002, a different attacker goal evidenced by injection-resistance rates rather than detection/miss-rate statistics. It is **not** operational monitoring for decay after the fact — that is IRQ-RES-005 and IRQ-RES-006, which detect degradation once it has begun. This procedure tests whether the control's design was *tested against adversarial evolution* before and after deployment. A control can pass here and still decay afterwards, which is why the canvas holds the disciplines apart and cross-links them rather than merging them.
- Isolated non-production environment running **the deployed control build — not a development-time snapshot** — reproduced as configured in production, including its threshold settings. A control tested at a different threshold is a different control. Where only a development snapshot is available, report the constraint rather than testing the substitute.
- Read access to: the control's existing historical or static case library and its reported detection rate, with the library's date range and how confirmed cases entered it; the control's validation and re-validation record; any prior adversarial-evolution test design documentation and results; the defined re-test cadence and its documented rationale, where one exists; the governance-escalation route for test findings and governance minutes for the last 12 months.
- Controlled corpus repository, access-restricted and engagement-scoped, into which the adversarial-evolution test set is built and from which it is destroyed at teardown.
- Personnel: AI security reviewer (lead) with adversarial-ML competence; a fraud, AML, surveillance or screening SME for the domain-relevance limb, because a technically valid evasion that no real adversary would use produces a misleading miss rate; firm platform engineer for environment provisioning; the control owner.
- Written confirmation from the environment owner that the instance has no path to production systems, live transaction rails or real customer data. Benign, procedurally constructed test inputs only.

### Test design
**Corpus construction is the procedure, and it is organised by taxonomy category rather than by individual input.** Test inputs are constructed to represent the NIST AI 100-2e2025 evasion-attack class for the control's domain, supplemented by MITRE ATLAS case-study techniques relevant to fraud, AML, surveillance or screening as applicable. The mapping is documented item-by-item or family-by-family before execution; an ad hoc or undocumented test set makes coverage and rigour unassessable and is itself a canvas fail indicator. The domain-SME plausibility review of the constructed set is **a disclosed reviewer design addition, not canvas procedure** — it shapes test-set quality rather than answering the canvas's question, and it is identified as the reviewer's own addition wherever it appears below.

**Two populations, run and reported separately.**
- **P1 — the firm's existing historical or static case library**, run to reproduce the control's reported detection rate as the baseline. Where the reproduced rate diverges from the reported one, that divergence is reported before anything else, because every subsequent comparison depends on it.
- **P2 — the adversarial-evolution test set**, mapped to the taxonomies. Detection rate and **residual miss rate** are computed separately for this population.

**The measure that matters is the difference.** Whether the miss rate against P2 is materially higher than against P1 is the signal that historical validation has been overstating real-world efficacy. A blended figure across both populations destroys the finding and must not be produced.

**Cadence limb.** Establish whether a defined re-test cadence exists, whether it is tied to a documented risk-based rationale rather than a bare calendar default, and whether it has been followed.

**Escalation limb.** Establish whether material findings from any prior adversarial-evolution testing reached an accountable governance body with authority to trigger remediation or re-validation, and with a recorded response — or were held only by the technical team that ran them. The canvas links this control to IRQ-GOV-008.

**Benign-payload principle.** Test inputs are procedurally constructed and benign. No production data, no live systems and no actual customers are accessed at any point. Techniques are logged by taxonomy category, never as reusable strings, and nothing in the evidence pack constitutes a working evasion recipe for a live control.

### Steps
1. Confirm the applicability and both boundary distinctions. **Record:** the control's function and the reasons this is not an E.1 matter and not an IRQ-RES-005/006 monitoring matter.
2. Record environment metadata and confirm isolation; confirm the control build under test is the deployed build, and verify its threshold configuration matches production. **Record:** build identity and threshold configuration; where only a development snapshot is available, record the constraint.
3. Obtain the historical or static case library and the control's reported detection rate. **Record:** both, with the library's date range and how confirmed cases entered it.
4. Construct the adversarial-evolution test set with the domain SME, documenting the mapping item-by-item or family-by-family to NIST AI 100-2e2025 evasion categories and, where applicable, MITRE ATLAS techniques and case studies. **Record:** the mapping table, before execution.
5. **Reviewer design addition, not canvas procedure.** Review the test set with the domain SME for real-world plausibility. **Record:** any input rejected as implausible and why — this limb protects the miss rate from being inflated by evasions no adversary would attempt, and is disclosed as the reviewer's own addition to test-set quality.
6. Run P1. **Record:** detection rate and miss rate, and any divergence from the firm's reported figure.
7. Run P2 under the same configuration. **Record:** detection rate and **residual miss rate**, reported separately from P1 throughout.
8. Compute and report the miss-rate uplift from P1 to P2. **Record:** the figure, the taxonomy categories driving it, and the reviewer's basis for judging materiality — which is professional judgement, and must be stated as such.
9. Inspect code or pipeline evidence that the adversarial-evolution test set is actually run against the deployed control, not only at development time. **Record:** the inspection note.
10. Establish whether the firm has previously performed any adversarial-evolution testing. **Record:** the evidence, or that control efficacy is evidenced solely by historical detection rate.
11. Review the defined re-test cadence and its rationale. **Record:** the cadence, whether it has lapsed, and whether any lapse carries a documented risk-based justification.
12. Trace escalation of the most recent material adversarial-evolution finding through 12 months of governance records (reviewer-set design minimum, disclosed at scoping). **Record:** whether it reached an accountable body with authority to trigger remediation or re-validation and a recorded response, or was held only by the technical team.
13. Destroy the corpus and record teardown sign-off.

### Observations & measures
- **P1 detection and miss rate** — reproduced against the firm's historical or static case library, with any divergence from the reported figure recorded first.
- **P2 detection and residual miss rate** — against the adversarial-evolution test set, **reported separately** from P1. Canvas pass indicator requires separate reporting; a blended figure is a reporting failure, not a result.
- **Miss-rate uplift (P2 minus P1)** — the procedure's headline measure. Canvas threshold: **not materially higher**, or, where it is, documented as a finding with a remediation plan rather than obscured within a blended figure. **No FAIAS-standard acceptance threshold exists for residual miss rate — the taxonomies structure the test, they do not set a pass/fail bar.** Materiality is the assessor's risk-based judgement and the basis is recorded.
- **Taxonomy mapping** (categorical): test set documented category by category against NIST AI 100-2e2025 and/or MITRE ATLAS / ad hoc or undocumented. Canvas fail indicator: the second, because coverage and rigour become unassessable.
- **Deployed-build confirmation** (binary): the test ran against the deployed control build / against a development-time snapshot only. Efficacy evidence attaches to the deployed control; a development-time result does not transfer.
- **Re-test cadence** (categorical): defined, rationale-documented and evidenced as followed / defined but lapsed with no documented risk-based justification / none defined. Canvas fail indicators cover the second and third.
- **Escalation** (binary): material adversarial-evolution findings reached an accountable governance body with a recorded response / findings held only by the technical team that ran the test. Canvas fail indicator: the second.

### Interpretation
- **Pass** — the adversarial-evolution test set is constructed with documented mapping to NIST AI 100-2e2025 and/or MITRE ATLAS rather than assembled ad hoc; the miss rate against it is reported separately from the historical-case detection rate and is not materially higher — or, where it is, that gap is documented as a finding with a remediation plan rather than obscured within a blended figure; a defined re-test cadence exists, tied to a documented risk-based rationale rather than a bare calendar default, and is evidenced as followed; and material findings are shown to have reached an accountable governance body with a recorded response.
- **Fail** — no adversarial-evolution testing exists and control efficacy is evidenced solely by detection rate against a historical or static case library; **or** a test set exists but is undocumented against any recognised taxonomy, making its coverage and rigour unassessable; **or** the miss rate against adversarial-evolution testing is materially higher than the historical detection rate and this gap is not disclosed, escalated or actioned; **or** no defined re-test cadence exists, or the evidenced cadence has lapsed with no documented risk-based justification; **or** testing exists but its findings are held only by the technical team that ran it, with no evidence they reached governance.
- **Partial** — the canvas's own shape: adversarial-evolution testing has been performed and mapped to NIST AI 100-2e2025, but the resulting miss-rate uplift versus the historical case library has not been escalated to a governance body, and no re-test cadence has been defined. The assurance objective is not met until both gaps close. Report the uplift figure regardless, since it is the substantive result.

### Evidence outputs
- E1 Vendor or internal assertion that the control is "highly accurate", citing historical detection rate alone with no adversarial-evolution test referenced — **L1**.
- E2 Environment attestation, isolation confirmation, deployed-build identity and threshold-configuration match against production — **L3**.
- E3 Test design documentation showing the taxonomy used (NIST AI 100-2e2025 and/or MITRE ATLAS) to construct the adversarial-evolution test set, with the mapping table — **L2**.
- E4 Domain-SME plausibility review record, including inputs rejected and why — **L3**; a reviewer design addition, not a canvas evidence item, and disclosed as such.
- E5 Code or pipeline inspection confirming the adversarial-evolution test set is actually run against the deployed control, not only a development-time snapshot — **L3**.
- E6 P1 execution results against the historical case library, with any divergence from the reported detection rate — **L3**.
- E7 P2 execution results: detection rate and residual miss rate against the adversarial-evolution test set, reported separately — **L3**.
- E8 Miss-rate uplift computation, the taxonomy categories driving it, and the reviewer's stated materiality basis — **L3**.
- E9 Re-test cadence documentation and evidence of adherence — **L2/L3**.
- E10 Independent validation or internal audit report confirming adversarial-evolution testing was executed as designed and findings were escalated — **L4**.
- E11 Governance records evidencing escalation and response — **L3**.
- E12 Production loss or incident data cross-referenced against the adversarial-evolution test findings, to confirm the test's predictive value — **L5**.
- E13 Corpus teardown record with sign-off — **L3**.

### Common pitfalls & limitations
- **Blending the two populations.** The whole finding is the difference between them. A single combined detection rate is worse than not running the procedure, because it looks like evidence.
- **Testing a development snapshot.** Efficacy evidence attaches to the deployed control; a development-time result does not transfer. Where only a snapshot is available, report the constraint rather than the substitute.
- **Ad hoc scenario construction.** An undocumented "we tried some difficult cases" set fails the first pass indicator regardless of how demanding the cases are, cannot be assessed for coverage, and cannot be reproduced at the next cadence point.
- **Constructing the test set without the domain SME.** A technically valid evasion that no fraudster, launderer or promoter would ever use inflates the miss rate and produces a finding that will not survive challenge from the control owner. The SME limb is a reviewer design addition rather than a canvas requirement, and is disclosed as such rather than presented as part of the published method.
- **Testing at a threshold that is not the production threshold.** Detection controls are threshold-sensitive by construction; a convenience threshold measures a different control.
- **Confusing this with jailbreak testing.** The adversary here is not attacking the model. They are adapting their own behaviour to evade what the model detects. Injection-resistance rates are not evidence for this question.
- **Collapsing this into decay monitoring.** IRQ-RES-005/006 catch degradation after it begins; they do not evidence design-time efficacy against adaptation. Passing here does not mean the control will not decay.
- **Inventing a numeric acceptance threshold.** No FAIAS-standard acceptance threshold exists for residual miss rate. Report the measurement, the stated materiality basis, and the threshold's absence.
- **Precedent limitation carried forward.** The closest documented precedent in the canvas — FTC v. Rite Aid Corporation (E.D. Pa., Docket 2:23-cv-05023, complaint and proposed stipulated order filed 19 December 2023; stipulated order signed 23 February 2024 and filed 26 February 2024; allegations neither admitted nor denied), an AI-based screening control deployed, as the complaint alleges, without any testing of its accuracy and with both vendors disclaiming it — is a **facial-recognition matching failure, not a fraud or AML adversarial-evasion incident**, and the canvas cites it for the general principle only. Do not present it as a sector precedent for adversarial evolution.
- **★2 honesty.** Two mature, actively maintained taxonomies structure the test; neither sets a pass/fail bar, and no FS-specific quantitative acceptance threshold exists on top of them. The materiality judgement on the miss-rate uplift is the assessor's. Per the canvas's own Pass language, a clean result reflects that the test was performed and its result was not adverse, **not** that a pass/fail bar has been formally met.

### Time/effort estimate
**4.5 reviewer-days** — 0.5 scoping, boundary confirmation, deployed-build and threshold verification; 1.5 adversarial-evolution test-set construction and taxonomy mapping with the domain SME (the dominant cost and the limb most worth protecting if time is short); 0.5 SME plausibility review (reviewer design addition); 1.0 P1 and P2 execution; 0.5 uplift analysis and materiality reasoning; 0.25 cadence and escalation limbs; 0.25 write-up and teardown. Excludes firm-side effort and environment build.

---
---

