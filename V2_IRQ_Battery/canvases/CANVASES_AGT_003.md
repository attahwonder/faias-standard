# CANVAS: IRQ-AGT-003

## 1. IRQ ID & Title
**IRQ-AGT-003: Excessive Tool Access Beyond Approved Task Scope**

Register question: "Does each tool exposed to the agent carry an explicit business justification, or does the agent hold capabilities beyond what its approved tasks require?"

## 2. Business Activities Affected
- **Customer service agents:** A support agent scoped to answer product queries may retain access to account-modification or payment-initiation tools left over from a broader pilot configuration, unused in normal operation but exploitable if the model is manipulated.
- **Internal operations copilots:** An agent built for document drafting may be granted broad file-system, email or database query tools "for convenience," each individually low-risk, expanding the blast radius of any single failure or injection.
- **Trading/markets support tools:** Research or analytics agents may retain execution-adjacent tool access (order staging, position amendment) never required for their approved analytical task.

## 3. AI Behaviour(s)
- Invokes whatever tools are exposed to it in its runtime environment when the model judges them relevant to the current request, regardless of whether that tool was intended for this task.
- Does not itself distinguish "tools I have because my task needs them" from "tools I have because they were never removed."
- Under adversarial or erroneous conditions, uses available tools opportunistically to satisfy the immediate objective, including tools unrelated to its documented purpose.

## 4. Failure Mode
> The agent holds tool capabilities beyond what its approved business task requires, with no explicit, current, per-tool business justification on record — so the system's effective blast radius under error, injection or misuse is materially larger than its intended function, and no one has assessed or approved that larger surface.

## 5. Potential Consequences
- **Customer:** Unintended account or payment actions taken by an agent whose stated purpose was informational; data exposure via unused-but-present retrieval/query tools.
- **Institution:** Incident investigation reveals the agent could have taken actions no one had approved or even realised were possible; remediation cost; loss of confidence in tool governance.
- **Regulator/market:** Evidence that AI systems operate with unreviewed, unbounded capability surfaces undermines the "approved use case" basis of the firm's AI governance framework.

## 6. Failure Chain
```
Agent deployed with tool set inherited from pilot/template configuration,
not re-scoped to the approved production task
  ↓ (IRQ-GOV-003: approval conditions not technically enforced at the tool layer)
Tool inventory contains capabilities with no current business justification
  ↓ (IRQ-AGT-003 — THIS IRQ: least-privilege not verified or recertified)
An error, injection (IRQ-SEC-004) or manipulated instruction causes the
agent to invoke an out-of-scope tool
  ↓ (IRQ-AGT-005: tool-call validation does not check task-relevance)
Unintended or unauthorised action executes using a capability the business
never intended this agent to exercise
  ↓
Customer/data harm → incident investigation reveals unreviewed capability
surface → governance and audit finding

Control Breakpoints:
  • IRQ-GOV-003: technical enforcement of approved tool scope, not policy-only
  • IRQ-AGT-003: periodic least-privilege recertification of the tool inventory
  • IRQ-AGT-012: irreversibility gates on any high-materiality tool regardless of scope
  • IRQ-SEC-011: credential/identity scoping tied to the same least-privilege boundary
```

## 7. Why a Domain Expert May Miss it
- Traditional access-control review (user entitlements, role-based access) is a mature discipline for human users; SMEs may not realise an AI agent's "entitlements" are its tool list, which is often configured by engineers rather than reviewed through the same access-governance process.
- Assumption that "the system prompt tells it what to do, so it won't use other tools" — false, since prompts constrain intended behaviour but do not remove the underlying capability, which remains exploitable under error or manipulation.
- Pilot-to-production transitions frequently carry over a broader tool set "just in case," and no formal step exists to strip it down — this is a governance process gap, not a technical one, and easily missed by a technically-focused review.
- Testing gap: functional testing confirms the agent can do its job with the tools given; it rarely asks whether it should have fewer tools than it has.

## 8. Assurance Objective
**AO-AGT-003:** Every tool exposed to an agent shall carry an explicit, current, documented business justification tied to its approved task scope, verified at deployment and recertified periodically, with no tool retained beyond what the approved task requires.

## 9. Expected Controls (Traced)
- **Least-privilege tool inventory with explicit per-tool business justification** — [OWASP Top 10 for LLM Applications 2025, LLM06 Excessive Agency; OWASP Agentic AI: Threats and Mitigations, Feb 2025, tool-misuse category] — a documented, current mapping of tool to approved task, reviewed as a governance artefact.
- **Technical enforcement of tool scope at the orchestration/platform layer, not prompt-only restriction** — [linked IRQ-GOV-003; NIST AI 600-1, Jul 2024] — the runtime environment, not the system prompt alone, restricts which tools are callable.
- **Periodic recertification of tool access, aligned to access-review cycles for human entitlements** — [ISO/IEC 27001, access control domain, applied by analogy to non-human identities; PRA SS1/23 governance principle] — tool grants expire or require re-approval on a defined cycle.
- **Non-human identity scoping consistent with least privilege** — [linked IRQ-SEC-011; NIST AI 100-2 E2025] — the agent's credentials are themselves scoped no more broadly than its justified tool set.
- **Change control triggering re-review when tool inventory changes** — [linked IRQ-GOV-012 envelope drift; IRQ-MOD-013] — adding a tool is treated as a material change requiring re-approval, not a routine engineering update.
- **Default-deny network position for the agent's environment, with connectivity allowed only where required** — [NCSC, "Managing the cyber risk of agentic AI", blog post, 20 August 2026 (page metadata: modified 24 August 2026), item 4, "Control the AI agent's environment with a robust sandbox", of the post's "Key considerations" list, sub-item c "Restrict network access"] — the public body's stated position is to "deny all inbound and outbound network traffic to the AI agent's environment by default. Then, only allow connections that are required, using allowlists", within a general instruction to "Always run AI agents within a sandboxed environment that controls and manages what resources can and cannot be communicated with, both locally and over a network", addressed to system designers and operators. The same post sets out **two distinct four-level maturity models — one at sub-item c (network access) and one at sub-item d, "Strengthen compute and host isolation" — which are separate scales and must be cited separately, never conflated.** Interim blog guidance, which NCSC states will be superseded by formal guidance.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the agent only has the tools it needs" with no inventory attached — **L1**.
- Documented tool inventory with stated business justification per tool, dated and owned — **L2**.
- Configuration/platform inspection confirming only the documented tools are technically callable in production (no residual pilot tools) — **L3**.
- Staging test attempting invocation of tools outside the documented scope (via crafted prompts) and confirming they are unavailable or blocked — **L3**.
- Independent audit or access-review report confirming least-privilege and recertification cadence — **L4**.
- Production telemetry: tool-invocation logs showing no calls to undocumented or de-scoped tools over the review period — **L5**.

## 11. Independent Test
> In a non-production replica of the deployment, enumerate all tools technically callable by the agent (via platform configuration inspection and adversarial prompting attempting to elicit unlisted tool use). Cross-reference against the documented business-justification inventory. For each tool present but unjustified, attempt invocation via both a direct request and a crafted/injected instruction to determine whether it is reachable and what action it permits. Methodology follows OWASP (2025) LLM06 (Excessive Agency) test guidance and the OWASP Agentic AI Threats and Mitigations tool-misuse test pattern. No production credentials or data used. — **★2 Confidence — as at FAIAS v1.2.0 (12 September 2026)** (published practitioner guidance exists — OWASP (2025) LLM06 and the Agentic Security Initiative paper — but no standardised benchmark for "least-privilege verification" exists; test design and materiality judgement are assessor-specific).

## 12. Pass Indicators
- 100% of technically callable tools have a current, dated, documented business justification tied to the agent's approved task.
- No unjustified tool is reachable in staging testing, including via adversarial prompting.
- Tool inventory recertification has occurred within the firm's defined cycle, with evidence of at least one tool removed or justified at each cycle (demonstrating the process is live, not rubber-stamped).
- Production telemetry over the review period shows zero calls to any tool outside the documented inventory.

## 13. Fail Indicators
- Tools are present and callable with no documented justification, discovered via configuration review or adversarial testing.
- Tool scope is enforced only via system-prompt instruction, with no platform-layer restriction — the tool remains callable if the prompt is bypassed.
- Recertification process exists on paper but produces no changes over multiple cycles (indicator of rubber-stamping).
- Production logs show tool invocations outside the documented inventory that were not investigated.

## 14. Reporting Language
**Pass:** "The agent's tool inventory is fully documented with current business justification per tool, technically enforced at the platform layer, and recertified on a [n]-monthly cycle. Adversarial staging tests found no reachable tool outside the documented scope. This is a ★2 assessment — credible practitioner guidance (OWASP), bespoke verification — and should be re-tested at each tool-inventory change."

**Fail:** "Configuration review and adversarial testing found [n] tools callable by the agent with no documented business justification, including [describe, e.g. account-modification capability retained from a prior pilot]. Because tool scope is enforced only through prompt instruction rather than platform restriction, this capability remains exploitable under injection or model error. This is an unreviewed and unapproved blast-radius expansion and should be remediated before continued deployment."

**Partial:** "Tool inventory documentation and platform enforcement are current for [x]% of deployed agents; [y]% (mostly pilot-derived configurations) have not been re-scoped for production. Remediation should prioritise the highest-materiality agents first."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (bounded blast radius; unauthorised action limited to justified,
              least-privilege tool set)
  Likelihood: 2 (requires both an unjustified tool to exist and a trigger to invoke it)
  Detectability: 2 (recertification cycle and telemetry surface anomalies periodically)
  Recoverability: 2 (scoped tool set limits action reversibility concerns to a known,
                     bounded set)
  Novelty: 3 (requires recognising AI tool access as an entitlement-governance problem,
              not just an engineering configuration)

Interpretation: acceptable with enforced least-privilege and live recertification;
highest concern is process capture — recertification becoming a rubber-stamp exercise.

If controls are absent or degraded:
  Severity: 4 (unbounded blast radius: any residual tool, including payment or
              account-modification capability, becomes exploitable)
  Likelihood: 3 (pilot-to-production tool carryover is a common, foreseeable pattern,
               not a rare occurrence)
  Detectability: 3 (silent until an incident or targeted audit surfaces it)
  Recoverability: 3 (depends entirely on which unjustified tool is exploited; could be
                     severe if payment-adjacent)
  Novelty: 3
Residual risk: High. Tool inventory governance should be a deployment gate condition.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unjustified tools can include payment- or account-adjacent capability; consequence severity depends on what remains reachable. |
| **Likelihood** | 3 | Pilot-to-production tool carryover without formal re-scoping is a common, documented pattern in agent deployments. |
| **Detectability** | 3 | Requires deliberate configuration audit or adversarial testing; not visible through normal functional testing. |
| **Recoverability** | 2 | Once identified, de-scoping a tool is a straightforward configuration change; harm from prior exploitation depends on the tool's nature. |
| **Novelty** | 3 | Requires treating AI tool grants as an access-governance discipline, which most engineering teams do not natively apply. |

## 17. Regulatory Basis
> No regulation names "AI tool least privilege" explicitly. [PRA SS1/23, May 2023] requires governance and control of model risk drivers, extending by principle to agentic tool configuration. [FCA AI Update, Apr 2024] confirms AI risk is governed through existing SYSC and Consumer Duty frameworks, applicable to unreviewed capability surfaces affecting customer outcomes. [OWASP Top 10 for LLM Applications 2025, LLM06 Excessive Agency] and [OWASP Agentic AI: Threats and Mitigations, Feb 2025] are cited as accepted industry practice rather than binding regulation. [MAS Consultation Paper on AI Risk Management, Nov 2025] explicitly proposes agentic tool-governance expectations, the closest emerging regulatory analogue.

## 18. Research Basis
> [OWASP, 2025, "Agentic AI: Threats and Mitigations," OWASP Agentic Security Initiative v1.0] — first structured threat model for agentic systems, naming tool misuse and excessive-permission patterns as core agentic risks. [OWASP, 2025, "Top 10 for LLM Applications 2025," LLM06 Excessive Agency] — defines excessive functionality, permissions and autonomy as a named vulnerability class. [Chan et al., "Harms from Increasingly Agentic Algorithmic Systems," FAccT 2023, arXiv:2302.10329] — establishes that harm scales with the agent's action space, not merely its intelligence, supporting least-privilege as a primary control.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Fast (6 months)
>
> **URO-1 (resolved 12 September 2026): OWASP Top 10 for LLM Applications, 2026 edition (published approximately 4 August 2026), renumbering eight of ten entries, with the re-baselining of the OWASP Agentic Security Initiative's agentic threat list. Flagged 25 August 2026 — examined against its LLM06 Excessive Agency anchoring (LLM03:2026) and resolved under §6A.2 resolution form 1: the substance behind each cited entry survives the renumbering, the Agentic Security Initiative list is cited here by category rather than by threat number and its categories are carried into v1.1 (December 2025) unchanged, and no standardised benchmark has been published for the verification this canvas's ★ rests on. The ★2 is affirmed and published under the v1.2.0 anchor.** The v1.1.0 position stands as register history; ratings issued under different anchors are not comparable numbers (§6A.1).

## 19. Related IRQs
```
  - IRQ-AGT-004 (C.2: composite-action risk from chained tool permissions — direct extension)
  - IRQ-AGT-005 (C.2: tool-call/output validation — the invocation-integrity control layer)
  - IRQ-SEC-010 (E.3: compromised/malicious tool servers — supply-chain analogue)
  - IRQ-SEC-011 (E.4: non-human identity least privilege — the credential-side mirror control)
  - IRQ-GOV-003 (I.2: technical enforcement of approval conditions — the governance mechanism)
```

## 20. References
```
[1] OWASP, 2025. "Agentic AI: Threats and Mitigations." OWASP Agentic Security
    Initiative, v1.0, February 2025.
[2] OWASP, 2024/2025. "OWASP Top 10 for LLM Applications 2025." LLM06:2025
    Excessive Agency.
[3] Chan, A., et al., 2023. "Harms from Increasingly Agentic Algorithmic Systems."
    Proc. FAccT 2023. arXiv:2302.10329.
[4] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
[5] FCA, 2024. "AI Update." April 2024.
[6] MAS, 2025. "Consultation Paper: Proposed Guidelines on Artificial Intelligence Risk
    Management." November 2025.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: C.2 (Agentic domain, Tool Use)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional entitlement review targets human users; engineers
  configuring agent tool access are not typically subject to the same access-governance
  discipline, and SMEs may not think to ask for a tool inventory at all.
✓ Test 2 (Plausible Harm): Grounded in OWASP's Agentic Security Initiative and OWASP (2025) LLM06
  Excessive Agency, both naming this as a primary agentic vulnerability class.
✓ Test 3 (Testable): Fully testable via configuration audit and adversarial prompting in
  a non-production replica. ★2 methodology, honestly caveated.
✓ Test 4 (Decision-Relevant): Gates deployment approval and defines the recertification
  cadence as a condition of use.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): URO-1 resolved (§6A.2 form 1). OWASP Top 10 for LLM Applications
  2026 edition and the OWASP Agentic Security Initiative list examined against this
  canvas's anchors. LLM06:2025 Excessive Agency is LLM03:2026 in the 2026 edition, with
  root causes and examples unchanged; the Agentic Security Initiative's "Agentic AI:
  Threats and Mitigations" now stands at v1.1 (December 2025), the tool-misuse category
  carried unchanged, and this canvas cites it by category rather than by threat number.
  No standardised benchmark for least-privilege verification has been published.
  ★2 affirmed under the v1.2.0 anchor; the v1.1.0 position stands as register history.
- v1.2.0 (2026-09-12): Expected Controls — NCSC's default-deny network position for an
  agent's environment added, with its two separate four-level maturity models (network
  access; compute and host isolation) cited as distinct scales. Interim blog guidance,
  to be superseded. No change to test, ★ or risk profile.
```

---
---

