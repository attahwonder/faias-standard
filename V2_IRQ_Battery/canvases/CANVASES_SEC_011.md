# CANVAS: IRQ-SEC-011

## 1. IRQ ID & Title
**IRQ-SEC-011: Non-Human Agent Identity and Credentials Lacking Least Privilege, Short Lifetime, or Rapid Revocation**

Register question: "Are the agent's credentials and identity distinct from human identities, least-privileged, short-lived, and revocable — or would credential theft grant broad standing access?"

## 2. Business Activities Affected
- **Agentic systems with backend/API access:** Any agent that authenticates to internal systems (case management, payments rails, customer databases) does so via some credential; how that credential is scoped determines the blast radius of any compromise.
- **Composite multi-tool agentic workflows:** Where an agent chains several permitted tool calls to achieve a broader outcome (linked IRQ-AGT-004), the underlying identity/credential architecture determines whether that composite action is even possible or is blocked at the identity layer.
- **Computer-use and GUI agents:** Agents operating under a shared or impersonated human identity (e.g. logged in "as" a staff member) create audit and accountability gaps distinct from those with genuinely non-human, attributable identity.

## 3. AI Behaviour(s)
- Authenticates to backend systems and tools using a credential — which may be a dedicated non-human identity, a shared service account, or (in poorly designed systems) a human user's own credentials.
- Retains and reuses that credential across a session or, in weaker designs, across an extended or indefinite period rather than per-task or short-lived issuance.
- Executes actions under whatever standing permissions the credential carries, regardless of whether the specific task at hand requires that full permission set.

## 4. Failure Mode
> The agent's operating identity is not distinct from human identities, is not scoped to least privilege for the task at hand, is not short-lived, and/or cannot be rapidly revoked — such that theft or misuse of the agent's credential (via prompt injection, tool-server compromise, or direct credential exfiltration) grants an attacker broad, standing, hard-to-revoke access rather than narrow, time-bounded, immediately revocable access.

## 5. Potential Consequences
- **Institution:** A single compromised agent credential becomes a high-value target granting broad access, materially amplifying the impact of any other successful attack in this domain (e.g. IRQ-SEC-004, IRQ-SEC-010); slow revocation extends the exposure window.
- **Customer:** Downstream harm from whatever the broad standing access enabled (data access, transactions) during the period before revocation.
- **Market/regulator:** Identity and access management is a well-established regulatory expectation (SMCR-adjacent accountability, access-control requirements); failure to extend it to non-human/agentic identities is a foreseeable gap regulators will expect closed as agentic adoption grows.

## 6. Failure Chain
```
Agent's operating identity is under-scoped: shared service account, human
credential reuse, or standing (non-short-lived) broad permissions
  ↓ (IRQ-SEC-011 — THIS IRQ: no least-privilege, short-lived, distinct
     non-human identity design)
Agent credential is compromised via a separate attack (injection, tool-server
compromise, direct exfiltration) — see IRQ-SEC-004, IRQ-SEC-010, IRQ-SEC-006
  ↓ (IRQ-AGT-004: no composite-action guardrail limits what the broad
     permission set can be chained into)
Attacker (or the misdirected agent itself) exercises broad standing access
  ↓ (revocation is slow or requires disabling a shared account affecting
     other legitimate users/processes)
Extended exposure window; broad, hard-to-attribute unauthorised access
  ↓
Data/financial loss compounding whatever the initial compromise vector
achieved → incident response complicated by shared-identity attribution gap

Control Breakpoints:
  • IRQ-SEC-011: distinct non-human identity, least privilege, short-lived
    credentials, rapid revocation capability
  • IRQ-AGT-004: composite-action guardrails bounding what any given
    permission set can be chained into
  • IRQ-GOV-003: enforcement, not just policy statement, of least-privilege
    identity design
```

## 7. Why a Domain Expert May Miss it
- Identity and access management SMEs have deep expertise in human identity lifecycle (joiners/movers/leavers, SMCR mapping) but non-human/machine identity for autonomous agents is a distinct and newer discipline, often bolted onto existing IAM tooling not designed for it.
- The path of least resistance in early agent deployments is frequently to reuse an existing service account or, worse, a developer's own credentials during prototyping — a shortcut that can persist into production if not specifically audited for.
- "The agent is just calling our API" reads, to a non-specialist, as no different from any other internal service integration, missing that the agent's behaviour is directed by a model whose output can be adversarially influenced (linking this IRQ's severity directly to the success of IRQ-SEC-001/-004/-010), unlike a conventional deterministic service.
- Revocation speed is rarely tested end-to-end for non-human identities; an IAM team may confirm a credential "can be revoked" without validating how long that actually takes in the specific agentic platform's architecture.

## 8. Assurance Objective
**AO-SEC-011:** Every agent shall operate under an identity and credential distinct from any human user's, scoped to least privilege for its approved task set, issued with the shortest practicable lifetime, and revocable within a defined, tested time bound.

## 9. Expected Controls (Traced)
- **Distinct non-human identity per agent (or per agent class)** — [linked IRQ-AGT-004, IRQ-GOV-001; general IAM practice, ISO/IEC 27001 Annex A access-control controls applied to machine identities] — no agent operates under a shared service account or a reused human credential; identity is attributable to the specific agent/deployment.
- **Least-privilege permission scoping** — [linked IRQ-AGT-003, IRQ-AGT-004] — the agent's credential carries only the permissions its approved task set requires, directly bounding the blast radius of any credential compromise.
- **Short-lived, task-scoped credential issuance** — [DSIT, AI Cyber Security Code of Practice, Jan 2025; general secure-by-design credential-management practice] — credentials issued per-session or per-task rather than as long-standing static secrets, reducing the exposure window of any single compromise.
- **Tested rapid revocation** — [linked IRQ-RES-003; general IAM incident-response practice] — revocation capability is validated end-to-end for time-to-effect, not merely confirmed to exist in principle.
- **Composite-action guardrails at the identity/authorisation layer** — [linked IRQ-AGT-004] — even a legitimately scoped permission set is checked against transaction-level guardrails before a materially consequential composite action is permitted, providing defence-in-depth beyond identity scoping alone.
- **AI keys and agent integrations administered to the same standard as production credentials, and obtained only through authorised channels** — [Anthropic, *Detecting and countering misuse of AI: September 2026*, 10 September 2026, printed p.30] — stated by the publisher as an expected control: "Organizations should treat AI keys and agent integrations with the same level of seriousness as they do production credentials—because attackers treat them with the same level of seriousness, too"; and "AI access should be purchased only through authorized channels." The report's stated reason is that the integrations built around a model — "sandboxes, proxies, and resellers" — are themselves part of the attack surface, so the scope of this IRQ's credential questions extends to the intermediaries through which access is bought. *(A vendor threat report, not a regulator's instrument: cited as a publisher-stated expected control.)*
- **A distinct, class-differentiated identity per agent** — [NCSC, "Managing the cyber risk of agentic AI", blog post, 20 August 2026 (page metadata: modified 24 August 2026), item 4, "Control the AI agent's environment with a robust sandbox", of the post's "Key considerations" list, sub-item e "Assign and limit an agent's access to credentials"] — "All agents should be assigned their own unique identity in a class which differentiates them from human or individual systems." Interim guidance, which NCSC states will be superseded by forthcoming formal guidance. This is the first UK public-body statement of the expectation §9 bullet 1 presently traces only to general IAM practice and ISO/IEC 27001 Annex A by analogy.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "the agent has its own credentials" with no scoping/lifetime detail — **L1**.
- IAM architecture documentation showing the agent's identity model, permission scope, and credential lifetime policy — **L2**.
- Code/config inspection confirming the agent's credential is distinct from any human identity, is scoped as documented, and has the stated lifetime enforced (not merely configured) — **L3**.
- Staging test: attempt to use the agent's credential outside its documented scope, and time a revocation request end-to-end — **L3**.
- Independent IAM/security assessment of the agent identity architecture — **L4**.
- Operational evidence (comparable deployment) of credential rotation/revocation events and time-to-effect — **L5**.

**Dated worked example, added at the September 2026 refresh — an agent architecture in which the agent never holds the credential.** A published vendor architecture runs the agent's tooling in an isolated cell and issues it only a substitute token: "code in the runtime cell or a worker only ever sees a 'surrogate' token, minted by authd. After the concrete network request is authorized, Sentinel will replace any surrogate tokens with the real credential, obtained from authd, at the network boundary", with "Root inside the runtime cell … mapped to an unprivileged host user" [Meta, "How We Built Safety Into Muse", Meta AI Research, 8 September 2026]. It is a worked example of the limiting case of this IRQ's least-privilege and short-lifetime questions — the credential's blast radius bounded by the agent never possessing it — and a comparator for a firm assessing its own design. Limits: a vendor engineering disclosure is the only source; no model or system card covers the agent product launched 8 September 2026 or this gateway component; and the egress authorisation it describes resolves either to a narrowly bounded auto-allow or to a user-approval dialog, not to per-action human approval.

## 11. Independent Test
> In an isolated non-production environment: (1) inspect the agent's operating credential and confirm it is distinct from any human user's identity and from any other agent's identity; (2) attempt an action outside the credential's documented permission scope and confirm it is rejected; (3) issue a revocation request for the credential and measure end-to-end time-to-effect (i.e. the point at which the credential genuinely ceases to function, not merely the point the revocation request was submitted); (4) confirm credential lifetime — whether short-lived/task-scoped or long-standing — against the documented policy. Methodology per DSIT AI Cyber Security Code of Practice (2025) secure-by-design principles and general IAM/access-control testing practice (ISO/IEC 27001 Annex A control testing analogues). Benign, procedurally described test actions only; no production credentials or systems used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (general IAM/access-control testing is mature practice, but its specific application to autonomous agent identity is new enough that no AI-agent-specific standardised benchmark exists; rated to reflect that the identity/revocation testing itself is solid while the "is this the right model for agent identity" question remains a matter of professional judgement).

## 12. Pass Indicators
- Agent credential confirmed distinct from any human identity and from other agents' identities.
- Out-of-scope action attempts are rejected at the credential/permission layer.
- Revocation confirmed effective within the firm's defined time-bound target, tested end-to-end (not merely requested).
- Credential lifetime matches documented policy (short-lived/task-scoped where designed as such).

## 13. Fail Indicators
- Agent found to be operating under a shared service account or a reused human credential.
- Out-of-scope actions succeed, indicating the credential carries broader permission than its documented task set.
- Revocation takes materially longer than the defined target, or requires disabling a shared account affecting other legitimate users/processes.
- Credential has no defined lifetime (static, indefinite) with no compensating short-lived-issuance design.

## 14. Reporting Language
**Pass:** "Testing confirms the agent operates under a distinct non-human identity, scoped to least privilege, with revocation demonstrated effective within [n] minutes end-to-end. Testing rated ★2, reflecting the newness of agent-specific identity assurance practice relative to mature general IAM testing; recommend this control be re-validated whenever the agent's tool/permission set changes materially."

**Fail:** "Testing found the agent operates under [a shared service account / reused human credentials], with out-of-scope actions succeeding in [n] of [m] tested cases and revocation taking [x] to become effective — materially exceeding any reasonable containment window. This means credential compromise via any other successful attack in this domain (e.g. injection or tool-server compromise) would grant broad, hard-to-revoke standing access; remediation to a dedicated, least-privilege, short-lived identity design is required before continued deployment."

**Partial:** "The agent's identity is distinct and least-privilege scoped, but revocation was found to take [x], exceeding the firm's defined containment target of [y]. The assurance objective is not met until revocation speed is remediated and re-tested."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (broad standing access if compromised; amplifies severity of any linked
              successful attack — injection, tool-server compromise, credential extraction)
  Likelihood: 2 (plausible if identity design reverts to convenience shortcuts under delivery
              pressure; mitigated by least-privilege and short-lived credential design)
  Detectability: 2 (credential-use monitoring, where present, surfaces out-of-scope attempts
              in real time)
  Recoverability: 2 (rapid, tested revocation limits exposure window materially)
  Novelty: 3 (non-human/agentic identity is a newer IAM discipline; a general IAM SME without
              agent-specific exposure may assume standard service-account practice suffices)

Interpretation: acceptable with distinct, least-privilege, short-lived, rapidly-revocable
identity design and tested revocation speed; this IRQ functions as a severity multiplier for
several other SEC IRQs, so its control quality has outsized importance relative to its
standalone likelihood.

If controls are absent or degraded:
  Severity: 4 (a compromised shared/broad credential converts any single successful attack
              elsewhere in the SEC domain into broad, standing, hard-to-attribute access)
  Likelihood: 3 (convenience-driven credential-sharing shortcuts are a common early-stage
              agentic deployment pattern)
  Detectability: 3 (attribution is specifically degraded by shared-identity design, making
              even detected misuse harder to trace to cause)
  Recoverability: 3 (revoking a shared credential affects other legitimate users/processes,
              complicating and slowing containment)
  Novelty: 3
Residual risk: Critical as a severity multiplier — this control's absence materially worsens
the consequence of several other SEC IRQs, not only its own standalone likelihood.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Broad standing access if compromised; functions as a severity multiplier for injection, tool-server-compromise, and extraction IRQs elsewhere in the SEC domain. |
| **Likelihood** | 2 | Plausible if convenience shortcuts (shared service accounts, reused credentials) persist from prototyping into production, but well-mitigated by standard least-privilege/short-lived-credential design once applied deliberately. |
| **Detectability** | 3 | Shared or reused identity specifically degrades attribution, making even detected misuse harder to trace to a specific cause or actor. |
| **Recoverability** | 3 | Revoking a shared credential risks affecting other legitimate users/processes, complicating and slowing containment relative to a dedicated agent identity. |
| **Novelty** | 3 | Non-human/agentic identity is a distinct, newer IAM discipline; a general IAM specialist without agent-specific exposure may reasonably assume standard service-account practice is sufficient when it is not. |

## 17. Regulatory Basis
> [FCA SYSC, general systems-and-controls requirements on access management] and [SMCR accountability framework, by extension where a named individual is accountable for the agent's actions per IRQ-HUM-006] — non-human identity governance is a natural extension of existing access-control and accountability expectations, though not yet explicitly agent-specific in FCA/PRA rulebooks. [DSIT, AI Cyber Security Code of Practice, Jan 2025] — secure-by-design credential-management principles. [UK GDPR Art. 32(1)(b)] — security of processing, engaged where broad standing access enables personal-data compromise. [UNVERIFIED — confirmed as of Jul 2026: no FCA/PRA rule yet explicitly addresses non-human/agentic identity management; monitor for supervisory statements as agentic adoption grows] (verified 29 Jul 2026).

## 18. Research Basis
> [OWASP Foundation, 2025, "Agentic Security Initiative — Agentic AI: Threats and Mitigations", Feb 2025] — identifies privilege compromise and identity-related risks as a core agentic threat category, of which credential scoping is the primary mitigation. [DSIT, "AI Cyber Security Code of Practice", January 2025] — UK-specific secure-by-design credential-management principles applicable to non-human identities. No dedicated peer-reviewed academic paper specifically addresses non-human agentic identity management as a distinct research topic at time of writing; this control area rests primarily on general IAM practice and emerging agentic-security guidance rather than a mature academic literature — noted as a comparative evidentiary gap, consistent with the ★2 rating.
>
> For the form of an access-control assessment, the standards-body method is [Joint Task Force, 2022, "Assessing Security and Privacy Controls in Information Systems and Organizations", NIST Special Publication 800-53A Revision 5, January 2022, section 2.4 and procedure AC-03(08)]. Section 2.4 defines an assessment procedure as a set of assessment objectives, each with potential assessment methods (examine, interview, test) and assessment objects. Procedure AC-03(08) asks whether rules governing the timing of revocations of access authorisations are defined, and whether access authorisations are revoked under those rules when the security attributes of subjects or objects change. It sets no time limit and does not state a measurement of the time at which a revocation takes effect, which is what step (3) of field 11 measures. The publication does not mention artificial intelligence or autonomous agents. It is cited for the form of the assessment only. No ★ change follows from this addition.
>
> **[FAIAS Incident Register, row 84, "Exposing a GitHub token in a public repository", 2026]** — the developer's own report records that an internally deployed agent running on a researcher's GitHub credential "published a researcher's GitHub token in the public openai/codex repository", and that the response was to deactivate all the users' keys and then all employees' keys. The agent acted under a person's credential, so its misbehaviour exposed that person's access, and the revocation was wholesale. The developer is an AI laboratory, not a financial-services firm.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-AGT-003 / IRQ-AGT-004 (C.2: least-privilege tool scoping and composite-action
    guardrails — the permission-design counterpart to identity scoping)
  - IRQ-SEC-004 (E.1: untrusted-content-to-action — a compromise vector this IRQ's identity
    scoping bounds the impact of)
  - IRQ-SEC-010 (E.3: tool-server compromise — another compromise vector this IRQ bounds)
  - IRQ-HUM-006 (D.4: named accountable owner — accountability mapping for agent actions
    depends on distinct, attributable identity)
  - IRQ-RES-003 (G.2: tested containment/kill-switch capability — revocation speed is a
    specific instance of this broader containment requirement)
  - IRQ-AGT-012 (C.7: irreversible-action gating — credential design and gate design
    are the two halves of a funds gate; a credential bound to one merchant and one
    amount is an identity-layer implementation of that gate)
  - IRQ-AGT-014 (C.7: evaluation-environment containment — an evaluation harness
    holding production credentials is this IRQ's question asked of the test estate)
```

## 20. References
```
[1] OWASP Foundation, 2025. "Agentic Security Initiative — Agentic AI: Threats and
    Mitigations." v1.0, February 2025.
[2] DSIT, 2025. "AI Cyber Security Code of Practice." January 2025.
[3] UK GDPR, retained EU law, Article 32.
[4] FCA Handbook, SYSC (Systems and Controls); Senior Managers and Certification Regime
    (SMCR) framework.
[5] Joint Task Force, 2022. "Assessing Security and Privacy Controls in Information Systems
    and Organizations." NIST Special Publication 800-53A Revision 5, January 2022; section 2.4
    and procedure AC-03(08). https://doi.org/10.6028/NIST.SP.800-53Ar5
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.4 (Security domain, Identity & Credentials)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): General IAM SMEs have deep human-identity-lifecycle expertise but
  treat "the agent calling our API" as an ordinary service integration, missing that its
  behaviour is directed by an adversarially-influenceable model, unlike a deterministic
  service account.
✓ Test 2 (Plausible Harm): Grounded in the OWASP Agentic Security Initiative (Feb 2025)
  privilege-compromise threat category and DSIT AI Cyber Security Code of Practice (2025)
  secure-by-design principles; functions as a documented severity multiplier for several
  other named agentic threat classes.
✓ Test 3 (Testable): Fully testable in staging via credential-scope and revocation-timing
  tests; ★2 methodology, honestly rated given the newness of agent-specific identity practice.
✓ Test 4 (Decision-Relevant): Outcome gates the identity architecture required before any
  agent may be granted backend/API access, and sets the tested revocation-speed condition
  of use.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-12): Expected Controls — two sources added: a publisher-stated
  expectation that AI keys and agent integrations be administered as production
  credentials and access bought only through authorised channels (10 Sep 2026), and
  NCSC's per-agent class-differentiated identity expectation (20 Aug 2026, interim).
  Expected Evidence — surrogate-credential worked example added (8 Sep 2026). Related
  IRQs — AGT-012 and AGT-014 added. ★2 unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 84, OpenAI report on a GitHub token exposed in a public repository, an internal deployment of an AI laboratory). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — NIST SP 800-53A Rev. 5 cited for the form of
  an access-control assessment, with its limits stated (no mention of AI agents; revocation
  timing left to organisation-defined rules). Field 20 References — entry [5] added.
  Research-basis review date moved. ★2 unchanged.
```

---
---

