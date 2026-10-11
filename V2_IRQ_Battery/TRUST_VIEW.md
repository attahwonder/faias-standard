# FAIAS — AI Trust View

This page is an index. It adds no question, claim or rule, and it changes no rating.

**Purpose.** FAIAS as a whole asks whether an AI system can be trusted to perform a business activity safely (`00_Admin/ASSURANCE_MODEL.md` §1). This view takes a narrower reading of AI trust: freedom from governance, security and resilience failures, shown by evidence. It lists the questions of three domains: Governance (GOV), Security (SEC) and Operational Resilience (RES). It also lists the claims of three themes: Security (Theme 3), Resilience (Theme 6) and Governance (Theme 9). FAIAS has no "trust" domain.

**Why trust is not a domain.** Each question lives in one domain: the domain of its primary failure surface (`TAXONOMY.md`, homing rule). A trust domain would hold the same questions a second time.

**Limits.** Under the full reading, every question in FAIAS bears on trust, including those of Data (DAT), Model (MOD), Agentic (AGT), Human Oversight (HUM), Third Party (TPR) and Conduct & Fairness (CON). This view does not list them. `IRQ_CLAIM_MATRIX.md` maps every question to the claims it supports. The page carries no ★ rating or test status; each question's rating is in its canvas.

**Source.** Each row repeats the text of `IRQ_REGISTER.md` or `CLAIMS_REGISTER.md`. Where a row and its register differ, the register governs.

## Questions

### Governance (GOV)

| IRQ ID | Subdomain | Review Question |
|---|---|---|
| IRQ-GOV-001 | I.1 Inventory & Ownership | Is there a named accountable owner, with appropriate seniority and SMCR mapping, for each AI system across its full lifecycle including third-party components? |
| IRQ-GOV-002 | I.1 Inventory & Ownership | Is the AI inventory demonstrably complete — capturing shadow AI, embedded vendor AI, spreadsheets-plus-API usage and agentic workflows — with a mechanism that finds unrecorded use? |
| IRQ-GOV-003 | I.2 Approval, Tiering & Policy | Are approval conditions and usage restrictions (approved tasks, user groups, guardrails) technically enforced and monitored, or only stated in the approval paper? |
| IRQ-GOV-004 | I.2 Approval, Tiering & Policy | Does the risk-based tiering methodology correctly capture generative and agentic characteristics (autonomy, tool access, customer proximity), driving proportionate control depth? |
| IRQ-GOV-005 | I.2 Approval, Tiering & Policy | Do firm policies address GenAI/agentic specifics — acceptable use, data entry restrictions, output reliance, agent permissions — or only legacy model risk? |
| IRQ-GOV-006 | I.2 Approval, Tiering & Policy | Has the firm articulated a board-approved risk appetite for AI, with measurable indicators, against which individual deployments are demonstrably assessed? |
| IRQ-GOV-012 | I.2 Approval, Tiering & Policy | Has the system's effective operating envelope drifted from its approved envelope — through changes in intended use, user behaviour, prompts, tools, integrations, or the surrounding business process — while the model itself remained unchanged? |
| IRQ-GOV-007 | I.3 Validation & Oversight | Was validation performed by a party independent of development, with authority to reject, using firm-relevant evaluations rather than vendor or public benchmark claims? |
| IRQ-GOV-008 | I.3 Validation & Oversight | Do monitoring results, incidents and drift signals flow to accountable governance bodies with defined triggers for revalidation, restriction or withdrawal? |
| IRQ-GOV-009 | I.4 Documentation, Records & Regulatory | Does documentation (system/model cards, data statements, intended-use and limitation statements) exist at a standard enabling effective independent review and regulatory response? |
| IRQ-GOV-010 | I.4 Documentation, Records & Regulatory | Would retained records — inputs, outputs, versions, agent traces, human decisions — allow full reconstruction of any consequential decision for audit, complaint or regulatory purposes? |
| IRQ-GOV-011 | I.4 Documentation, Records & Regulatory | Are applicable regulatory obligations (EU AI Act classification, outsourcing/CTP registers, Consumer Duty MI, model risk expectations) mapped to each system with evidenced compliance owners — and does that mapping carry dated forward obligations that are enacted but not yet applicable, so the firm is not discovering them reactively? |
| IRQ-GOV-013 | I.4 Documentation, Records & Regulatory | Given a defined failure signature (model/configuration version, prompt or logic defect, affected date range), can the institution identify the *full* affected cohort of decisions — not only reconstruct the individual decision under complaint — and does a proactive remediation process exist to reach that cohort without waiting for a complaint to arrive? |
| IRQ-GOV-014 | I.4 Documentation, Records & Regulatory | Does the firm's incident classification scheme recognise AI-specific failure classes — mass confabulation, prompt-injection compromise, agentic misaction, silent bias event — with defined severity mapping and regulator-notification paths, such that the notification clock can start on an AI failure at all? |
| IRQ-GOV-015 | I.4 Documentation, Records & Regulatory | Are the firm's external representations about AI capability — marketing, product disclosures, RFP and due-diligence responses, investor communications — substantiated by, and periodically reconciled against, the system's validated capability envelope and documented limitation statements? |
| IRQ-GOV-016 | I.4 Documentation, Records & Regulatory | Where AI-generated or AI-assisted output feeds the firm's risk-data aggregation estate, capital or provisioning calculations, or supervisory/regulatory returns, is that output subject to the same accuracy, completeness, timeliness, adaptability and traceability discipline the firm applies to its risk data under BCBS 239 — and is the AI origin of any contributing output flagged and reconstructable within the aggregation record? |

### Security (SEC)

| IRQ ID | Subdomain | Review Question |
|---|---|---|
| IRQ-SEC-001 | E.1 Prompt Injection & Jailbreak | Can a user's direct prompt override system instructions or policy constraints, and has resistance been tested with current jailbreak techniques for the deployed model version? |
| IRQ-SEC-002 | E.1 Prompt Injection & Jailbreak | Can multi-turn, encoded, cross-lingual or persona-based jailbreaks elicit prohibited behaviours that single-turn guardrail testing would not surface? |
| IRQ-SEC-003 | E.1 Prompt Injection & Jailbreak | Can indirect prompt injection originating from retrieved documents influence downstream model behaviour despite application guardrails? |
| IRQ-SEC-004 | E.1 Prompt Injection & Jailbreak | Can instructions embedded in emails, web pages, files or tool outputs processed by an agent cause unauthorised actions (data exfiltration, unintended transactions)? |
| IRQ-SEC-005 | E.1 Prompt Injection & Jailbreak | Can an adversary with write access to any retrievable source plant content specifically crafted for the system to retrieve and act upon (inference-time RAG poisoning)? |
| IRQ-SEC-006 | E.2 Extraction & Leakage | Can adversarial prompting extract the system prompt, embedded credentials, or configuration details that materially aid subsequent attacks? |
| IRQ-SEC-007 | E.2 Extraction & Leakage | Can training-data extraction, membership inference or model inversion recover personal or proprietary information from the model or embeddings? |
| IRQ-SEC-008 | E.2 Extraction & Leakage | Can confidential firm or client data leak through prompts, context windows, telemetry or logs into environments outside the firm's control? |
| IRQ-SEC-009 | E.3 Supply Chain & Tool Security | Is the model artefact supply chain — weights, checkpoints, serialisation formats, dependencies — protected against tampering and known deserialisation exploits? |
| IRQ-SEC-010 | E.3 Supply Chain & Tool Security | Could a compromised or malicious MCP/tool server, plugin, or poisoned tool description redirect agent behaviour or exfiltrate data (including rug-pull updates and confused-deputy patterns)? |
| IRQ-SEC-011 | E.4 Identity & Credentials | Are the agent's credentials and identity distinct from human identities, least-privileged, short-lived, and revocable — or would credential theft grant broad standing access? |
| IRQ-SEC-012 | E.5 Misuse & Dual-Use | [Applicability condition: customer-facing deployments whose outputs are plausibly repurposable by the user as an instrument against a third party — not relevant to all deployments. The assessor confirms applicability at scoping, guided by a non-exhaustive trigger list: free-text generative output to customers; drafting or document-production capability; guidance responsive to user-described scenarios; output that carries the institution's brand or authority outside the session.] For such deployments, has the institution assessed and bounded the risk of its own AI being used by a customer as an instrument against third parties (drafting fraudulent communications, evasion or concealment guidance, social-engineering material) — with misuse cases identified and registered, and refusal and rate controls tested against them? |
| IRQ-SEC-013 | E.6 Control Efficacy Under Adversarial Evolution | Where an AI system functions as a control — fraud detection, AML/transaction monitoring, surveillance, screening or promotion approval — has its detection rate and residual miss rate been measured against adversarially evolved inputs, mapped to a recognised adversarial-ML taxonomy, rather than only against historical or static case libraries; and is control efficacy re-tested on a defined cadence as adversary technique evolves? |
| IRQ-SEC-014 | E.7 Improper Output Handling | Is model-generated output validated, sanitised or encoded appropriately before being passed to a downstream interpreter, renderer, query engine, shell or other execution context — such that unvalidated output cannot itself become an attack vector (injection, cross-site scripting, server-side request forgery, remote code execution) against the systems consuming it? |

### Operational Resilience (RES)

| IRQ ID | Subdomain | Review Question |
|---|---|---|
| IRQ-RES-001 | G.1 Fallback & Degradation | Is there a defined, tested fallback mode delivering the important business service within impact tolerance when the AI component is unavailable or untrusted? |
| IRQ-RES-002 | G.1 Fallback & Degradation | Does the system degrade safely under partial failure and stress — retrieval down, tool timeouts, load spikes, rate limiting — rather than producing plausible but unsupported responses or duplicated stale actions? |
| IRQ-RES-003 | G.2 Containment & Recovery | Can the system be halted or constrained within a defined time bound, including mid-plan agent termination without orphaned or half-completed actions, and is this tested? |
| IRQ-RES-004 | G.2 Containment & Recovery | Can the firm roll back to a known-good state — model version, prompts, index, agent memory — within recovery objectives, and has restoration been rehearsed? |
| IRQ-RES-005 | G.3 Monitoring & Alerting | Are quality, drift, and behavioural anomaly metrics monitored continuously with thresholds that trigger defined responses, not just dashboards? |
| IRQ-RES-006 | G.3 Monitoring & Alerting | Would the alerting design surface a slow degradation (gradual quality decay, rising hallucination rate) as opposed to only hard failures? |
| IRQ-RES-007 | G.4 Resilience Mapping | Are AI dependencies mapped into the firm's important business services and scenario testing, including severe-but-plausible AI-specific scenarios? |

## Claims

| Claim | Theme | Name | Criticality |
|---|---|---|---|
| CLM-09 | Theme 3 — Security | Adversarial resistance | Critical |
| CLM-10 | Theme 3 — Security | No confidential leakage | Critical |
| CLM-11 | Theme 3 — Security | Component integrity | High |
| CLM-18 | Theme 6 — Resilience | Fails safely | Critical |
| CLM-19 | Theme 6 — Resilience | Detectable and recoverable malfunction | Critical |
| CLM-20 | Theme 6 — Resilience | Service continuity | Critical |
| CLM-25 | Theme 9 — Governance | Reconstructable decisions | Critical |
| CLM-26 | Theme 9 — Governance | Complete and accountable governance | Critical |
| CLM-27 | Theme 9 — Governance | Controlled behavioural change | High |
| CLM-28 | Theme 9 — Governance | Regulatory-reporting integrity | Critical |
