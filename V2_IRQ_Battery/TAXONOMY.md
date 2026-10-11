# FAIAS — Canonical Taxonomy: Domains, Subdomains and IRQ Discipline

Financial AI Independent Assurance Standard. Scope: independent assurance of generative, agentic and predictive AI in financial institutions, for the uses listed in README.md §1. Under FAIAS the reviewer never tests production systems (the non-production rule, METHODOLOGY_STANDARDS.md §3).

**Scope exclusion — the institution's own AI only.** FAIAS assures the institution's own AI systems. The resistance of the institution's controls, other than its own AI systems (an AI system that itself performs an identity, authentication, fraud-control or payment-authorisation function is one of its own AI systems and is in scope: IRQ-SEC-013), to attack by external parties — including the resistance of its identity, authentication and payment-authorisation controls, and whether or not the attack uses AI — is excluded from the standard's scope. That risk is served by existing, regulator-mandated security testing regimes — CBEST (Bank of England, 2014–present), TIBER-EU (ECB, 2018, updated 2024 for DORA alignment), STAR-FS (Bank of England/PRA, FCA and CREST) and DORA threat-led penetration testing — and institutions are directed to those regimes for it. Review questions of that class are held outside the standard as a strategic option, not carried within it.

## Structuring principle

The primary unit is the **Independent Review Question (IRQ)** — not a risk label. IDs follow IRQ-<DOM>-NNN within nine domains, each decomposed into subdomains (44 total). Threats, vulnerabilities, controls, consequences and governance failures are never mixed in one item: the IRQ interrogates a failure mode; its control objective states what a well-controlled institution can demonstrate.

**Four-test inclusion discipline.** An IRQ is admitted only if: (1) a domain SME would likely overlook it because it stems from AI behaviour; (2) it has a plausible mechanism of harm supported by research, regulation or documented incidents; (3) it is answerable through evidence and safe testing in dev/test environments; (4) its outcome informs a governance or deployment decision. Items failing any test were dropped or merged (see REGISTER_STATS.md).

**Homing rule.** An IRQ lives in the domain of its primary failure surface (where the defect originates or the assurance evidence sits), not its consequence. Cross-cutting concerns are placed once and cross-referenced via Related IRQs.

**AI trust is not a domain.** `TRUST_VIEW.md` lists the GOV, SEC and RES questions, and the claims of the Security, Resilience and Governance themes, in one place. Each question keeps its one home under the homing rule.

---

## Domain → subdomain hierarchy

### DAT — Data (prefix IRQ-DAT, subdomains A.1–A.5)
Integrity, provenance, representativeness, privacy and lifecycle of all data feeding an AI system.
- **A.1 Training Data Provenance** — lawful origin, licence compatibility, copyright, provenance recording, synthetic data identification, label quality, representativeness, lineage reproducibility; construct validity of the modelled target variable. (IRQ-DAT-001…005, IRQ-DAT-014)
- **A.2 Data Poisoning** — corruption entering via the data supply chain: ingestion, labelling, curation; unvetted or gameable feedback-to-training loops. (IRQ-DAT-006, IRQ-DAT-013)
- **A.3 Retrieval Data** — RAG corpus curation, staleness override, conflicting documents, retrieval determinism, confidentiality exposure at retrieval. (IRQ-DAT-007…009)
- **A.4 Memory** — memory stores as data assets: scoping, tenant separation, deletion, obsolete memory. (IRQ-DAT-010)
- **A.5 Data Drift** — explicitly separated into statistical / semantic / source drift (inputs) and retrieval / embedding / document drift (retrieval layer). (IRQ-DAT-011…012)

**Belongs elsewhere:** inference-time poisoning attacks → SEC E.1; agent-written operational memory corruption → AGT C.5; fairness outcomes of data gaps → CON; vendor pre-training data opacity → TPR.

### MOD — Model (prefix IRQ-MOD, subdomains B.1–B.7)
Intrinsic behavioural properties of the model: correctness, calibration, capability boundaries, stability, evaluation integrity.
- **B.1 Capability Uncertainty** — boundaries defined and tested outside scope; unexpected capabilities; releases expanding capability without approval; reasoning degradation at length. (IRQ-MOD-001…003)
- **B.2 Hallucination** — measured confabulation rates; behavioural distinction of uncertainty vs ambiguity vs missing evidence vs conflicting evidence vs impossible requests. (IRQ-MOD-004…005)
- **B.3 Calibration** — confidence tracking accuracy across expected production operating conditions. (IRQ-MOD-006)
- **B.4 Specification Gaming & Reasoning Integrity** — metric satisfied while business intent violated; reward hacking; unfaithful chain-of-thought. (IRQ-MOD-007…009)
- **B.5 Distribution Shift & Evaluation Integrity** — population/covariate/concept/label/temporal/policy shift; benchmark leakage and eval contamination; model collapse; evaluator/judge validity. (IRQ-MOD-010…012, IRQ-MOD-015, IRQ-MOD-016)
- **B.6 Model Updates & Configuration** — prompts and decoding parameters as behaviour-bearing configuration under change control. (IRQ-MOD-013)
- **B.7 Output Stability & Determinism** — run-to-run and near-identical-input decision stability at a pinned configuration; decision-extraction validity separate from generation. (IRQ-MOD-014)

**Belongs elsewhere:** operational drift detection → RES G.3; vendor silent changes → TPR F.2; validation governance → GOV I.3; explainability to deciders → HUM D.4.

### AGT — Agentic (prefix IRQ-AGT, subdomains C.1–C.7)
Failure modes that exist only because the system plans, acts, uses tools, delegates, or persists state.
- **C.1 Planning & Goal Drift** — plan fidelity on long horizons; objective evolution; intermediate goals replacing originals; optimisation continuing after intent changes. (IRQ-AGT-001…002)
- **C.2 Tool Use** — tool selection least-privilege; permission escalation via chaining; invocation integrity (parameter manipulation, output validation bypass, external API influence, tool hallucination). (IRQ-AGT-003…005)
- **C.3 Recursive Agents** — spawning, uncontrolled recursion, unbounded cost. (IRQ-AGT-006)
- **C.4 Multi-Agent Systems** — error reinforcement, consensus hiding wrong reasoning, ambiguous responsibility. (IRQ-AGT-007)
- **C.5 Operational Memory** — distinct from DAT A.4: inherited poisoned context and past failures influencing future decisions. (IRQ-AGT-008)
- **C.6 Hidden Reasoning Dependencies** — undocumented intermediate reasoning artefacts; prompt changes altering behaviour without code change; prompt versioning as controlled configuration. (IRQ-AGT-009)
- **C.7 Workflow & Action Safety** — workflow divergence, hidden chains, irreversible-action gating, computer-use GUI safety, evaluation-environment containment. (IRQ-AGT-010…014)

**Belongs elsewhere:** attacker-injected instructions in agent-read content → SEC E.1; MCP/tool-server compromise → SEC E.3; human approval of agent actions → HUM D.3.

### HUM — Human Oversight (prefix IRQ-HUM, subdomains D.1–D.4)
Whether humans function as an effective control layer.
- **D.1 Automation Bias** — acceptance without challenge; disagreement-rate monitoring; approval theatre; override training. (IRQ-HUM-001…002)
- **D.2 Skill Atrophy** — task performance without AI; periodic AI-free competency assessment. (IRQ-HUM-003)
- **D.3 Escalation & Override Design** — intervention positioning, suspension authority, oversight capacity. (IRQ-HUM-004…005)
- **D.4 Accountability & Contestability** — named owners; traceability through delegated workflows; attributable approvals; explanation adequacy; contest routes; evidential standard for AI-triggered adverse action. (IRQ-HUM-006…008, IRQ-HUM-009)

### SEC — Security (prefix IRQ-SEC, subdomains E.1–E.7)
Adversarial exploitation of the AI system at build or inference time — extended by three adjacent classes: the system's legitimate capability repurposed by an authorised user (E.5); the system's efficacy *as* a control against adversaries who evade rather than attack it (E.6); and the system's own output crossing a trust boundary into downstream execution contexts (E.7).
- **E.1 Prompt Injection & Jailbreak** — direct, multi-turn/obfuscated, indirect via retrieved content, untrusted-content-to-action paths, inference-time RAG poisoning. (IRQ-SEC-001…005)
- **E.2 Extraction & Leakage** — system-prompt/secrets extraction; training-data extraction, membership inference, inversion; confidential egress. (IRQ-SEC-006…008)
- **E.3 Supply Chain & Tool Security** — model artefact integrity; MCP/tool-server and plugin compromise. (IRQ-SEC-009…010)
- **E.4 Identity & Credentials** — non-human identity, credential theft, least privilege. (IRQ-SEC-011)
- **E.5 Misuse & Dual-Use** — the system operating as designed, its legitimate capability repurposed by an authorised user against a third party; applicability-conditional. (IRQ-SEC-012)
- **E.6 Control Efficacy Under Adversarial Evolution** — where the AI system *is* the control (fraud, AML, surveillance, screening): detection and residual miss rates against adversarially evolved inputs, taxonomy-mapped, on a defined re-test cadence. (IRQ-SEC-013)
- **E.7 Improper Output Handling** — model output crossing a trust boundary into an interpreter, renderer, query engine or execution context, validated as untrusted input. (IRQ-SEC-014)

### TPR — Third Party (prefix IRQ-TPR, subdomains F.1–F.3)
Risks arising because critical AI components are externally built, hosted or controlled.
- **F.1 Due Diligence, Contracts & Licensing** — provider diligence; contractual transparency/audit/exit and usage rights; embedded vendor AI; vendor financial standing and continuity. (IRQ-TPR-001…003, IRQ-TPR-009)
- **F.2 Model Change Management** — silent vendor capability/version drift, rollback and governance-bypass prevention. (IRQ-TPR-004)
- **F.3 Dependencies, Concentration & Data Handling** — open-source provenance; embedding/vector lock-in; provider retention/training on firm data; concentration. (IRQ-TPR-005…008)

### RES — Operational Resilience (prefix IRQ-RES, subdomains G.1–G.4)
Keeping important business services within impact tolerance when AI degrades or fails.
- **G.1 Fallback & Degradation** — fallback modes; safe degradation under partial failure and stress. (IRQ-RES-001…002)
- **G.2 Containment & Recovery** — kill/containment mechanism; rollback of all behavioural components. (IRQ-RES-003…004)
- **G.3 Monitoring & Alerting** — threshold-driven monitoring; slow-decay detection. (IRQ-RES-005…006)
- **G.4 Resilience Mapping** — IBS mapping and AI-specific scenario testing. (IRQ-RES-007)

### CON — Conduct & Fairness (prefix IRQ-CON, subdomains H.1–H.3)
Fair customer and market outcomes from AI-influenced decisions.
- **H.1 Discrimination & Proxy Bias** — subgroup/intersectional outcome gaps; proxy discrimination. (IRQ-CON-001…002)
- **H.2 Customer Outcomes, Vulnerability & Access** — vulnerable customers; generative mis-statements; exclusion; pricing fairness; ordinary-use harmful output. (IRQ-CON-003…006, IRQ-CON-009, IRQ-CON-010)
- **H.3 Feedback Loops & Transparency** — performative feedback loops; AI-use disclosure. (IRQ-CON-007…008)

### GOV — Governance (prefix IRQ-GOV, subdomains I.1–I.4)
The institutional control fabric.
- **I.1 Inventory & Ownership** — accountable owners; inventory completeness including shadow and embedded AI. (IRQ-GOV-001…002)
- **I.2 Approval, Tiering & Policy** — conditions-of-use enforcement; AI-aware tiering; policy coverage; risk appetite; operating-envelope drift. (IRQ-GOV-003…006, IRQ-GOV-012)
- **I.3 Validation & Oversight** — independent validation; escalation of operational signals to governance. (IRQ-GOV-007…008)
- **I.4 Documentation, Records & Regulatory** — review-grade documentation; decision reconstruction records; regulatory obligation mapping; cohort-level identification; AI-specific incident taxonomy; external capability claims; AI output entering risk-data aggregation. (IRQ-GOV-009…011, IRQ-GOV-013…016)

---

## Boundary rulings (dedup rationale for the hard cases)

1. **RAG poisoning — DAT vs SEC.** Split by vector. Corruption entering through the data lifecycle (ingestion, curation, staleness, labelling) is DAT A.2/A.3 (IRQ-DAT-006, -007). Adversarial content planted for retrieval-time influence — including indirect injection payloads — is SEC E.1 (IRQ-SEC-003, IRQ-SEC-005). One failure surface each; cross-linked.
2. **Memory — DAT A.4 vs AGT C.5 vs SEC.** DAT A.4 governs memory *as a data asset* (scoping, tenant separation, deletion, obsolescence: IRQ-DAT-010). AGT C.5 governs memory *as a behavioural influence* — inherited poisoned context and past failures steering future decisions (IRQ-AGT-008), which can occur without an attacker. Attack-origin injection into memory is SEC E.1 (IRQ-SEC-004), cross-linked to both.
3. **Monitoring — RES vs GOV.** Capability vs consumption. Detection/alerting/response capability is RES G.3 (IRQ-RES-005, -006). Whether signals reach accountable bodies and trigger revalidation is GOV I.3 (IRQ-GOV-008). Log existence for reconstruction is GOV I.4 (IRQ-GOV-010).
4. **Drift — DAT A.5 vs MOD B.5 vs RES vs TPR.** Data-side drift (statistical/semantic/source and retrieval/embedding/document) is DAT A.5. Model robustness across shift types (population/covariate/concept/label/temporal/policy) and its validation treatment is MOD B.5 (IRQ-MOD-010). Operational detection is RES G.3. Drift caused by silent provider changes is TPR F.2 (IRQ-TPR-004).
5. **Prompt injection vs excessive agency.** The injection attack is SEC E.1; the blast radius — why an injected agent can do damage — is AGT C.2 permissions design (IRQ-AGT-003, -004). Complementary, not duplicative.
6. **Explainability — HUM vs GOV vs MOD.** Homed in HUM D.4 (IRQ-HUM-007): adequacy for the deciding human. Regulator-facing documentation is GOV I.4 (IRQ-GOV-009). Interpretability limits sit inside MOD B.1/B.4 (unfaithful reasoning, IRQ-MOD-009); no standalone MOD explainability IRQ.
7. **Feedback loops — CON vs DAT vs MOD.** Homed in CON H.3 (IRQ-CON-007) because the FS-material harm is distorted customer outcomes; recontamination mechanics cross-link to IRQ-MOD-012 (collapse) and A.1 lineage rather than being restated.
8. **Kill switch — RES vs HUM vs AGT.** Mechanism existence and tested effectiveness (including mid-plan agent termination) → RES G.2 (IRQ-RES-003). Authority and willingness to invoke → HUM D.3 (IRQ-HUM-005). No separate AGT containment IRQ.
9. **Transparency vs contestability.** Disclosure that AI influenced an outcome → CON H.3 (IRQ-CON-008). The route to a human re-decision → HUM D.4 (IRQ-HUM-008).
10. **Eval contamination — MOD vs GOV.** Contamination of evidence is MOD B.5 (IRQ-MOD-011); governance reliance on it without challenge is subsumed under IRQ-GOV-007.
11. **Shadow AI — GOV vs SEC.** Inventory completeness failure → GOV I.1 (IRQ-GOV-002); exfiltration through unsanctioned tools is covered by IRQ-SEC-008.
12. **MCP/tool supply chain — SEC vs AGT vs TPR.** Malicious/tampered tool servers and descriptions → SEC E.3 (IRQ-SEC-010). Design-side tool scoping → AGT C.2. Commercial dependence on tool providers → TPR F.1; no third item created.
13. **Prompt versioning — MOD B.6 vs AGT C.6.** The change-control discipline for prompts/config is MOD B.6 (IRQ-MOD-013, applies to any generative system). The agent-specific hazard — behaviour depending on undocumented reasoning artefacts and prompt state across a workflow — is AGT C.6 (IRQ-AGT-009). Cross-linked; distinct evidence bases.
14. **Envelope drift — GOV I.2 vs MOD B.1 vs AGT C.7 vs RES G.4.** Ruling: homed in GOV I.2 as IRQ-GOV-012. The approved operating envelope *is* the conditions-of-use record; drift in effective use (intended purpose, user behaviour, prompts, tools, integrations, surrounding process) while the model is unchanged is a divergence between operational reality and the approval basis — a governance reconciliation failure, not a model property. Distinctions: MOD B.1 (IRQ-MOD-001/-002) covers the model's *capability* envelope; AGT C.7 (IRQ-AGT-010) covers per-execution workflow divergence within one run, whereas GOV-012 covers population-level drift of the deployment's use profile over time; RES G.3/G.4 supply the detection tooling that feeds the reconciliation. Cross-links recorded on the owning canvas's side (IRQ-GOV-012 field 19); not asserted bidirectional; single home in GOV.
15. **Licensing — TPR vs DAT.** Provider/output licence rights live in TPR F.1 (IRQ-TPR-002); training-data licence compatibility and copyright live in DAT A.1 (IRQ-DAT-001). The former is contractual; the latter is corpus provenance.
16. **Misuse vs jailbreak — SEC E.5 vs E.1.** *Misuse* is the system operating **as designed**, its legitimate capability repurposed by an authorised user against a third party (→ E.5, IRQ-SEC-012). *Jailbreak* is adversarial defeat of controls (→ E.1). Distinguishing test: did any control fail? Yes → E.1; no, and harm arises from the capability working correctly against an unintended target → E.5.

## Applicability legend
G = generative, A = agentic, P = predictive. Agentic systems inherit all G IRQs where a generative model underlies the agent; register tags reflect direct applicability.
