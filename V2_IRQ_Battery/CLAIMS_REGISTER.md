# FAIAS — Assurance Claims Register

An assurance claim is a technology-neutral proposition about the system or organisation that must be adequately supported by IRQ evidence before deployment. Claims roll up to the four-box deployment opinion (Should Proceed / With Conditions / Should Not Proceed / Unable to Form Opinion). A failed **Critical** claim is presumptively blocking (Should Not Proceed unless the assurance board documents compelling compensating grounds); a failed **High** claim presumptively drives With Conditions; **Medium** claims inform conditions and monitoring priorities. If evidence is insufficient to assess a Critical claim, the presumptive opinion is Unable to Form Opinion.

**Criticality test.** A claim is Critical **iff** its failure's consequence pathway is **illegal, unbounded, or uncompensated**. *Assignment:* the test determines the rating. *Blocking:* a failed Critical claim blocks the deployment, per the presumptive rule above, which follows from the test rather than sitting beside it. Working definitions applied consistently below: **illegal** — the failure's direct consequence is a breach of law or a legal prohibition — including a binding rule made under statute (a Handbook or Rulebook R rule, or a statutory instrument) — and not merely a supervisory expectation (guidance, supervisory statements, non-binding materials); the construction was ruled once at the v1.1.1 batch and CLM-28's derivation is its worked anchor; **unbounded** — no structural bound limits the scale of the loss (silent invalidation of the approval basis, attacker-controlled behaviour, or uncontrolled real-world action); **uncompensated** — the harm cannot be identified and remediated after the fact, and no external redress route reaches it. Every claim below carries a one-line derivation against this test; the derivation, not the label, is the rating's authority.

**Aggregation principle.** The per-claim rules address a single claim's failure in isolation. Where multiple claims fail together within one claim theme, a cluster of High and/or Medium failures inside that theme is treated as a **systemic finding** and presented as such in the opinion — not as unrelated individual findings. This principle carries **no numeric threshold or composite score**. Whether a cluster is systemic is a reasoned board determination, informed by whether the failing claims share a common root cause, evidence source or control.

Materiality lenses: CO customer outcomes · PS prudential safety · CD Consumer Duty · OR operational resilience · MI market integrity · FC financial crime · DP data protection · RE reputation · TP third-party dependency · FS financial statements.

## Theme 1 — Data & Information Integrity

**CLM-01 · Authorised information only.** The system accesses, uses and reveals only information that the requesting user, agent or process is entitled to.
*Rationale:* AI systems collapse traditional entitlement boundaries — retrieval, agent credentials and context assembly can each bypass the access model that governs humans.
*Lenses:* DP, CO, RE, FC. **Criticality: Critical.**
*Criticality derivation:* Unauthorised access or disclosure is unlawful processing — the **illegal** limb is met directly.

**CLM-02 · Fit and lawful data.** All data feeding the system — training, fine-tuning, grounding and reference — is lawfully sourced, licence-compatible, quality-assured, representative and traceable to origin.
*Rationale:* Every downstream behaviour inherits the defects of its data; provenance failure is unremediable post-training.
*Lenses:* DP, CO, CD, RE, FS. **Criticality: Critical.**
*Criticality derivation:* Unlawfully sourced or licence-incompatible corpora make the processing itself unlawful (**illegal**), and a provenance defect cannot be untrained after the fact (**uncompensated**). Reclassified High → Critical at the criticality re-derivation decided on 31 July 2026.

**CLM-03 · Memory and context integrity.** Persisted memory and carried-forward context are accurate, scoped to the right customer/tenant, purgeable, and cannot corrupt future behaviour.
*Rationale:* Stateful systems convert one bad artefact into a persistent behavioural defect; deletion obligations extend to memory.
*Lenses:* DP, CO, OR. **Criticality: Critical.**
*Criticality derivation:* Cross-tenant leakage is unlawful disclosure and failed deletion breaches erasure obligations (**illegal**) — both are central failure modes of the claim, not edge cases. Reclassified High → Critical at the criticality re-derivation decided on 31 July 2026.

## Theme 2 — Model Behaviour

**CLM-04 · Envelope-consistent behaviour.** The system behaves consistently within its approved operating envelope, and its behaviour outside that envelope is characterised and safe.
*Rationale:* Approval is only meaningful for the envelope that was validated; jagged capabilities, shift and envelope drift silently invalidate it.
*Lenses:* PS, CO, OR. **Criticality: Critical.**
*Criticality derivation:* Behaviour outside a characterised envelope is by definition uncharacterised — the loss has no structural bound (**unbounded**).

**CLM-05 · Evidence-grounded outputs.** For material decisions, outputs are grounded in verifiable evidence, with unsupported content structurally prevented or flagged.
*Rationale:* Generative systems complete rather than abstain; ungrounded fluency is the primary mechanism converting model error into customer harm.
*Lenses:* CO, CD, PS, FC. **Criticality: Critical.**
*Criticality derivation:* Ungrounded output to material decisions is silent and scales with throughput; affected parties do not know to seek redress (**unbounded, uncompensated**).

**CLM-06 · Reliable expressed confidence.** Any confidence or certainty signal the system expresses is calibrated across expected operating conditions and safe to rely on for escalation.
*Rationale:* Oversight and escalation designs key on confidence; a miscalibrated signal disables the entire downstream control chain.
*Lenses:* CO, CD, PS. **Criticality: High.**
*Criticality derivation:* Miscalibration degrades downstream controls rather than removing them; it is measurable and correctable once found — no limb met. High.

**CLM-07 · Intent-aligned optimisation.** The system's optimisation serves the business intent, not merely its measurable proxy.
*Rationale:* Specification gaming and reward hacking produce metric success with outcome failure — invisible to KPI-based oversight.
*Lenses:* CO, CD, PS, MI. **Criticality: High.**
*Criticality derivation:* Metric/intent divergence is detectable through outcome review and accrues gradually; harm is bounded by the decision domain and remediable — no limb met. High.

**CLM-08 · Trustworthy evaluation evidence.** The evaluation evidence on which approval relies is uncontaminated, firm-relevant and independently produced.
*Rationale:* Contaminated benchmarks and vendor claims make every other assurance conclusion unsound at its foundation.
*Lenses:* PS, RE, FS. **Criticality: High.**
*Criticality derivation:* Unsound evaluation evidence corrupts authorisation decisions, but harm materialises through other claims' failures and is remediable by re-evaluation — no limb met directly. High.

## Theme 3 — Security

**CLM-09 · Adversarial resistance.** The system resists adversarial manipulation — direct and indirect prompt injection, jailbreaks and planted content — such that untrusted input cannot alter privileged instructions or cause unauthorised actions.
*Rationale:* Instructions and data share one channel in LLM systems; every externally writable surface is an attack surface.
*Lenses:* CO, DP, FC, OR, RE. **Criticality: Critical.**
*Criticality derivation:* A successful injection places behaviour under adversary control — the loss bound is the attacker's choice (**unbounded**), and exfiltration consequences are **illegal**.

**CLM-10 · No confidential leakage.** Confidential firm and customer information cannot be extracted from, or leaked through, the system, its context, telemetry or providers.
*Rationale:* Models memorise, contexts accumulate, and provider pipelines carry data outside the firm's control.
*Lenses:* DP, RE, MI, PS. **Criticality: Critical.**
*Criticality derivation:* Extraction or leakage of confidential information is a breach of confidence and of data-protection law (**illegal**).

**CLM-11 · Component integrity.** Models, weights, tools, plugins and serving components are authentic, untampered and monitored for malicious change.
*Rationale:* AI supply chains (checkpoints, MCP/tool servers, plugins) admit compromise classes that conventional software controls do not cover.
*Lenses:* OR, DP, TP, RE. **Criticality: High.**
*Criticality derivation:* Component compromise is adversary-conditional and its blast radius is bounded by the deployment's permission envelope (CLM-12); detection failure routes to CLM-09/12 pathways. No limb met independently — High. *Borderline: recorded for review.*

## Theme 4 — Agentic Control

**CLM-12 · Bounded agency.** Agent actions remain bounded by the user's intent and by least-privilege permissions, including under tool chaining, manipulation and error.
*Rationale:* Agency converts model error and adversarial influence into executed real-world actions; the permission boundary is the last structural control.
*Lenses:* CO, PS, FC, OR, DP. **Criticality: Critical.**
*Criticality derivation:* Unbounded agency executes real-world actions — payments, trades, communications — with no structural limit on scale (**unbounded**); unauthorised transactions can be **illegal**.

**CLM-13 · Observable agency.** All agent activity is observable and attributable — no consequential action occurs in hidden chains.
*Rationale:* Oversight, accountability and reconstruction all fail if actions can occur unrecorded.
*Lenses:* PS, OR, FC, FS. **Criticality: Critical.**
*Criticality derivation:* Hidden consequential actions defeat reconstruction: harms cannot be identified, attributed or remediated afterwards (**uncompensated**) — the same pathway that makes CLM-25 Critical. Reclassified High → Critical at the criticality re-derivation decided on 31 July 2026.

**CLM-14 · Controlled delegation.** Delegation across sub-agents, multi-agent workflows and recursive spawning is bounded, reconcilable to the designed process, and free of unmanaged emergent behaviour.
*Rationale:* Coordination failures (error reinforcement, false consensus, unbounded recursion) arise only at the system-of-agents level and evade single-agent testing.
*Lenses:* OR, PS, CO. **Criticality: High.**
*Criticality derivation:* Delegation failures remain inside the permission boundary CLM-12 enforces and are observable where CLM-13 holds; bounded and remediable — no limb met. High.

## Theme 5 — Human Oversight

**CLM-15 · Genuine human oversight.** Human oversight is genuinely accountable and effective: reviewers detect errors, approvals are substantive, intervention occurs before irreversible actions, and named individuals hold rehearsed suspension authority.
*Rationale:* Nominal oversight (rubber-stamping, post-hoc notification) satisfies the org chart while providing zero control effect.
*Lenses:* CO, CD, PS, OR. **Criticality: Critical.**
*Criticality derivation:* Nominal oversight silently removes the control layer across everything it covers while appearing present (**unbounded**, and the appearance defeats detection).

**CLM-16 · Sustained human competence.** The organisation sustains the human expertise and capacity needed to supervise the system and to operate without it.
*Rationale:* Skill atrophy silently converts a supervised system into an unsupervised one, and invalidates the fallback assumption.
*Lenses:* OR, PS, CO. **Criticality: Medium.**
*Criticality derivation:* Skill atrophy is gradual, observable in assessment, and remediable by training or hiring — no limb met. Medium.

**CLM-17 · Contestable decisions.** Affected customers and colleagues can contest AI-influenced decisions and obtain a genuine human re-decision.
*Rationale:* Contestability is both a regulatory expectation and the error-correction channel of last resort.
*Lenses:* CD, CO, RE. **Criticality: High.**
*Criticality derivation:* A failed firm-level contest route does not extinguish redress: DISP complaints and the Financial Ombudsman Service remain — the uncompensated limb is bounded externally. High.

## Theme 6 — Resilience

**CLM-18 · Fails safely.** When the system fails, degrades or is compromised, it fails to a safe state — no plausible-but-wrong outputs, no orphaned half-completed actions, and containment within a defined time bound.
*Rationale:* Generative failure modes are silent and fluent; safe failure must be engineered, and agents add the mid-plan termination problem.
*Lenses:* OR, CO, PS. **Criticality: Critical.**
*Criticality derivation:* Unsafe failure produces plausible-but-wrong output and orphaned actions silently, at production scale (**unbounded**).

**CLM-19 · Detectable and recoverable malfunction.** Malfunction — including slow behavioural decay — is detected in time to act, and the firm can restore a known-good state within recovery objectives.
*Rationale:* AI degrades gradually and silently; without decay-sensitive detection and full behavioural-state rollback, harm accumulates undetected.
*Lenses:* OR, CO, PS. **Criticality: Critical.**
*Criticality derivation:* Undetected decay accumulates harm without a bound until discovery, which the failure itself delays (**unbounded**).

**CLM-20 · Service continuity.** Important business services remain within impact tolerance when AI components or their dependencies fail or must be withdrawn.
*Rationale:* AI embeds new single points of failure (models, GPUs, vector stores) into services regulators require to be resilient.
*Lenses:* OR, PS, TP, CO. **Criticality: Critical.**
*Criticality derivation (re-derived under the v1.1.1 illegal-limb construction):* Remaining within impact tolerance is a binding rule, not a supervisory expectation: **SYSC 15A.2.9R** — "A firm must ensure it can remain within its impact tolerance for each important business service in the event of a severe but plausible disruption to its operations" — with the PRA imposing the identically worded obligation on dual-regulated firms (**Operational Resilience – CRR Firms, 2.5**; **Insurance – Operational Resilience, 2.5**; all effective 31 March 2022, transition ended 31 March 2025; Handbook and Rulebook fetched 26 August 2026). Failure of embedded AI components is squarely a severe-but-plausible disruption, and the claim is scoped to *important business services* — a category that exists only for firms within these regimes — so every instance of the failure mode as scoped is the state a binding R rule requires the firm to be able to prevent (**illegal**). The superseded derivation's "expectations, not per-se illegality" framing was stale post-PS21/3. Scale remains bounded by impact-tolerance design and harms are compensable, so no other limb is met. Reclassified High → Critical at the v1.1.1 re-derivation.

## Theme 7 — Third Party

**CLM-21 · No silent vendor alteration.** No third party can silently alter the system's production behaviour — model, filters, defaults or tools — without the firm detecting it and re-approving.
*Rationale:* Provider-side change is continuous and undisclosed by default; it invalidates validation without any internal change signal.
*Lenses:* TP, PS, OR, CO. **Criticality: Critical.**
*Criticality derivation:* A silent provider change invalidates the approval basis with no internal change signal — the invalidation is undetectable by design (**unbounded**).

**CLM-22 · Managed third-party dependency.** Third-party AI dependencies are understood, diligenced, contractually controlled, within concentration appetite, and substitutable.
*Rationale:* Foundation-model economics concentrate critical capability in a few external parties, with the firm's data and continuity exposed to their choices.
*Lenses:* TP, OR, PS, DP, RE. **Criticality: High.**
*Criticality derivation:* Concentration and diligence failures crystallise through visible provider events; harm is bounded and substitution is the remedy — no limb met. High.

## Theme 8 — Fair Outcomes

**CLM-23 · Fair outcomes across groups.** The system produces fair outcomes across customer groups, free of unjustified direct, proxy or feedback-amplified disparity, in access, pricing and treatment.
*Rationale:* AI discovers proxies and entrenches feedback loops at scale; disparity is an emergent property no single rule review reveals.
*Lenses:* CD, CO, RE, MI. **Criticality: Critical.**
*Criticality derivation:* Unjustified disparity on protected characteristics is unlawful discrimination under the Equality Act 2010 (**illegal**).

**CLM-24 · Informed and protected customers.** Customers — including those with characteristics of vulnerability — are accurately informed, appropriately treated, and told when AI materially influences their outcomes.
*Rationale:* Consumer Duty attaches to what the customer experiences: mis-statements, exploitation of vulnerability and undisclosed AI influence are foreseeable-harm failures.
*Lenses:* CD, CO, RE. **Criticality: Critical.**
*Criticality derivation (re-derived under the v1.1.1 illegal-limb construction):* The claim's first two limbs breach binding Consumer Duty rules on their face: a mis-statement to a retail customer breaches **PRIN 2A.5.3R** — "A firm must communicate information to retail customers in a way which is clear, fair and not misleading" — and, for designated investment business, **COBS 4.2.1R**; treatment that exploits or disregards characteristics of vulnerability breaches the cross-cutting obligations **PRIN 2A.2.1R** (act in good faith) and **PRIN 2A.2.8R** (avoid causing foreseeable harm), with the vulnerability-specific texts (PRIN 2A.2.10G(2), 2A.2.25G) supplying their application as guidance (all fetched from the Handbook 26 August 2026) (**illegal**). The third limb — disclosure of AI influence — has no per-se rule and meets the limb only derivatively, where the omission renders a communication unclear or misleading under 2A.5.3R; that qualification is stated, not smoothed. External redress routes function and per-customer harm is bounded, so no other limb is met. The superseded derivation tested only the bounded and compensated limbs and never addressed the illegal limb. Reclassified High → Critical at the v1.1.1 re-derivation.

## Theme 9 — Governance

**CLM-25 · Reconstructable decisions.** Governance can reconstruct and justify any AI-influenced decision — inputs, versions, traces, human involvement — throughout required retention periods.
*Rationale:* Complaints, FOS referrals, audits and enforcement all turn on reconstruction; an unjustifiable decision is indefensible regardless of its correctness.
*Lenses:* PS, CD, FS, RE, FC. **Criticality: Critical.**
*Criticality derivation:* An unreconstructable decision cannot be justified, attributed or remediated — harms to affected parties go **uncompensated** and the firm's position is indefensible.

**CLM-26 · Complete and accountable governance.** All AI use is known, inventoried, owned by named accountable individuals, approved on a risk basis, within stated appetite, and mapped to regulatory obligations.
*Rationale:* Shadow and embedded AI mean the control fabric silently under-covers reality; you cannot govern what you have not found.
*Lenses:* PS, RE, FS, MI. **Criticality: Critical.**
*Criticality derivation:* Unknown AI is ungoverned AI: no bound exists on what an uninventoried system may be doing (**unbounded**).

**CLM-27 · Controlled behavioural change.** Every change that can alter system behaviour — prompts, configuration, tools, integrations, effective operating envelope — passes change control and, where material, re-approval.
*Rationale:* AI behaviour changes without code changes; uncontrolled prompt, tool and usage drift bypasses every gate built for software.
*Lenses:* PS, OR, CO. **Criticality: High.**
*Criticality derivation:* Internal behavioural change leaves change-record traces and is detectable by regression discipline; the silent-invalidation limb is characteristic of vendor-side change (CLM-21), not internal change — no limb met. High. *Borderline: recorded for review.*

**CLM-28 · Regulatory-reporting integrity.** AI-generated or AI-assisted content that reaches a supervisory or regulatory return submitted by the firm is held, before submission, to the same accuracy, completeness, timeliness, adaptability and traceability discipline the firm applies to system-sourced risk data, and its AI origin is flagged and reconstructable within the submitted record.
*Rationale:* Risk-data aggregation and reporting discipline (BCBS 239 and its national implementations) was built for data flowing from source systems into the estate; generative and agentic AI reverses that direction, contributing narrative, summarisation and reconciliation content the discipline was never built to see, and which is not distinguishable from system-sourced data once it enters the record. The claim is drawn at the **submitted-return boundary** — the point at which the firm's binding reporting obligations bite and the content leaves the firm. Integrity of AI-originated content inside the aggregation estate *before* submission is carried by CLM-25's reconstruction family and is not duplicated here.
*Lenses:* PS, RE, FS, OR. **Criticality: Critical.**
*Criticality derivation:* A supervisory or regulatory return is submitted in purported compliance with **binding Handbook reporting rules made under FSMA 2000** — rules, not supervisory expectations. SUP 16.3.12G imports SUP 15.6 into periodic reporting; **SUP 15.6.1R** binds the firm to take reasonable steps to ensure that information it gives under any Handbook rule is factually accurate and complete; **SUP 15.6.2G(3)** names SUP 16 (Reporting requirements) as a chapter to which that rule is relevant; and **SUP 15.6.7G** is the FCA's own reminder that **FSMA 2000 s.398** makes it an offence for a firm knowingly or recklessly to give false or misleading information in a material particular in purported compliance with the FCA's rules. Unflagged, undisciplined AI-originated content that renders a submitted return materially inaccurate breaches SUP 15.6.1R on its face, whatever the firm's state of mind — a breach of a binding rule (**illegal**). Where the same content is given knowingly or recklessly, s.398 is additionally engaged as a criminal offence; the mens rea element is real and is not satisfied by inadvertence, but the firm's own absent control is what leaves the inaccuracy undetectable at the point of submission. s.398 is **residual by construction** (s.398(2): subsection (1) applies "only to a requirement in relation to which no other provision of this Act creates an offence in connection with the giving of information"); the search of the whole of FSMA 2000 run for this gate found no other FSMA information offence reaching a periodic Handbook return, so the residual screen passes — it must nonetheless be run per requirement before the criminal limb is asserted.[^clm28-1] **CRR 2013 (SI 2013/3115) reg 45** extends s.398 to capital-requirements obligations, reaching COREP/FINREP-class prudential returns by statute rather than by Rulebook. Enforcement reality is stated in three layers, in order: (i) the offence exists in law and is **fine-only on both routes — no custodial penalty** — the summary fine unlimited in England and Wales since **LASPO 2012 s.85** (in force 12 March 2015), so the stale "statutory maximum / £5,000" figure is never quoted; (ii) **no prosecution, conviction or published enforcement action under s.398 could be identified from public sources as at 24 August 2026** (declared limits: paywalled citators and the first-instance reporting gap — this formulation, never "there has never been one"), and neither regulator has published policy on prosecuting it; (iii) the **realised** consequence regime for materially inaccurate returns is civil and substantial — s.206 financial penalties (SCB £46.55m; GSI £34.3m, enforcing SUP 15.6.1R itself; UKI £10.6m, 2026) and s.166 skilled-person reviews. Neither the unbounded nor the uncompensated limb is met. **Critical on the illegal limb**, which on this claim's scope needs no qualification: every instance of the failure mode as scoped is a breach of a binding reporting rule.

[^clm28-1]: Two boundaries kept explicit so a hostile reader cannot collapse them. **FSA 2012 ss.89–91** (misleading statements, misleading impressions and the related offences) do **not** reach regulatory returns — each turns on an inducement element absent from periodic reporting — and they sit in a different Act, which s.398(2), limited to "this Act", cannot reach in any event. And that search's disposal of **FSMA s.191F(6)** rests on its placement under Part XII's "Offences under this Part" heading; that is a construction argument which has not been tested against case law and must not be treated as load-bearing.

---

## Summary

| Criticality | Count | Claims |
|---|---|---|
| Critical | 19 | CLM-01, 02, 03, 04, 05, 09, 10, 12, 13, 15, 18, 19, 20, 21, 23, 24, 25, 26, 28 |
| High | 8 | CLM-06, 07, 08, 11, 14, 17, 22, 27 |
| Medium | 1 | CLM-16 |

**28 claims — 19 Critical, 8 High, 1 Medium** (re-derived against the criticality test at v1.0.3, the owner's decision of 31 July 2026: CLM-02, CLM-03 and CLM-13 reclassified High → Critical; and at v1.1.1 under the ruled construction of the illegal limb: CLM-20 and CLM-24 reclassified High → Critical; derivations recorded per claim above). Coverage against all 109 IRQs is verified in IRQ_CLAIM_MATRIX.md (no orphans in either direction).
