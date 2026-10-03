# FAIAS — Testing Playbook: AGT (Agentic) Domain

**Component:** V3 Testing Playbook
**Domain:** AGT — Agentic (subdomains C.1–C.7)
**Procedures:** TP-AGT-001 … TP-AGT-014 (14, 1:1 with IRQ-AGT-001 … IRQ-AGT-014)
**Source canvases:** `V2_IRQ_Battery/canvases/CANVASES_AGT.md`
**Governing documents:** `00_Admin/ASSURANCE_MODEL.md` (★ anchors, L1–L5 evidence levels), `00_Admin/METHODOLOGY_STANDARDS.md` (source hierarchy, testing-method labelling, non-production rule)
**Compiled:** 2026-07
**Spelling:** UK throughout

---

## Domain Testing Overview

### Purpose and scope of this playbook

Each procedure expands the summary-level Independent Test in the corresponding Review Canvas into an executable sheet. **★ confidence ratings are carried over unchanged** — twelve procedures at ★2 and **two at ★1** (TP-AGT-008 memory poisoning, TP-AGT-013 computer-use GUI safety), exactly as the canvas set records. **No AGT procedure reaches ★3 or above**, and none is inflated. The domain preamble in CANVASES_AGT.md is explicit that agentic AI safety research is roughly 2023–2026 vintage and that almost none of it has matured into a benchmarked, widely-adopted testing standard; this playbook preserves that honesty rather than dressing bespoke procedures in borrowed authority. **No new citations are introduced** — every method reference traces to a canvas entry.

**The domain's ★ uniformity is a consistency observation, not a ground for any individual rating.** Every rating here is assigned against the anchors in `00_Admin/ASSURANCE_MODEL.md` §6 and defended against those anchors in its own canvas. That the ratings then cluster at ★2 is an *outcome* of applying the anchors to an immature evidence base — it is not an input to any rating, and no procedure's rating may be justified by reference to the distribution of its neighbours.

Practical consequence for reporting: **every AGT conclusion is judgement-based** under METHODOLOGY_STANDARDS §3c and must be labelled as such — "conclusion should be interpreted as professional assessment, not standardised evidence" — with the two ★1 procedures carrying the stronger caveat that the methodology is novel and results depend entirely on assessor expertise.

### Non-production rule (applies to all fourteen procedures)

Per METHODOLOGY_STANDARDS §3, every procedure executes **only in a development, test or staging environment isolated from production**. This rule bites harder here than in any other domain, because agentic systems *act*. Specifically, across all AGT procedures: **no production credentials; no live funds, trades, payments or transfers; no production records; no live customer communications; no production GUI systems; no live external APIs.** Every tool the agent can reach in the test environment must be a sandboxed emulation or a non-production endpoint, and this must be **verified by the reviewer before the first agent run**, not assumed from a configuration document. An agent that reaches a real endpoint during an assurance test is an incident, not a finding.

### Shared test-environment setup (build once, reuse across AGT)

The agentic test harness is the largest single investment in the FAIAS programme and is reused by all fourteen procedures.

| Component | Purpose | Used by |
|---|---|---|
| **Sandboxed agent runtime** — the firm's actual orchestration framework, with the model, prompts, scaffolds and tool definitions as deployed | Every failure mode in this domain lives in the orchestration, not the model | All |
| **Emulated tool endpoints** for every tool the agent can call (payments, account servicing, compliance lookup, external APIs, record deletion, communications), returning realistic responses and recording every call | Tool-use, chaining, validation, gating | TP-AGT-003, 004, 005, 006, 012 |
| **Verified isolation boundary** — an egress control proving no call can reach a production or live external endpoint | Mandatory precondition | All |
| **Full trace capture** at maximum verbosity: every model call, tool call, parameter, response, retry, abandoned branch, sub-agent invocation, timestamp | The instrument for most procedures, and the object of study in TP-AGT-011 | All |
| **Synthetic FS case library** — AML investigations, claims settlements, complaint cases, payment instructions, counterparty analyses, with documented ground-truth correct outcomes | Scenario substrate | TP-AGT-001, 002, 004, 007, 010, 012 |
| **Multi-session memory store replica** with provenance metadata | Memory-poisoning testing | TP-AGT-008 |
| **Sub-agent delegation replica** with configurable depth and cost ceilings | Recursion and permission-tree testing | TP-AGT-006, 007 |
| **Replica legacy GUI environment** with the ability to inject UI events (pop-ups, delays, duplicate elements) and capture screenshots | Computer-use testing | TP-AGT-013 |
| **Documented process maps** for the workflows the agent executes | Conformance reconciliation | TP-AGT-010 |
| **Change-management/prompt-configuration replica** | Governance-bypass testing | TP-AGT-009 |
| **Evidence store** (write-once or checksum-controlled) | All | All |

**Determinism and repetition discipline:** agentic trajectories are far more variable than single model calls. Every procedure must fix and record the decoding configuration and run each scenario a fixed number of times (n≥5, preferably n≥10 for consequential-action scenarios — reviewer-set design minima, disclosed at scoping). A single successful gate hold proves nothing. Report rates, not anecdotes.

### Sequencing advice

Run in five waves. The ordering is driven by dependency: several procedures are uninterpretable without the trace quality that TP-AGT-011 establishes.

**Wave 0 — foundation.** **TP-AGT-011 (trace completeness) runs first.** Ten of the other thirteen procedures measure something by reading traces. If abandoned branches and retried tool calls are not recoverable from logs, those procedures cannot measure what they claim to measure, and the reviewer needs to know that before designing around it. A trace failure found in wave 0 changes the whole engagement plan; found in wave 4, it invalidates completed work.

**Wave 1 — surface and permissions.** TP-AGT-003 (tool inventory versus justification) and TP-AGT-009 (prompt/scaffold configuration control). These establish what the agent can actually do and what actually governs its behaviour — both prerequisites for designing meaningful scenarios later.

**Wave 2 — tool-use integrity.** TP-AGT-005 (tool-call validation), then TP-AGT-004 (composite actions), then TP-AGT-006 (delegation bounds). This order matters: TP-AGT-005 establishes whether individual calls are validated, which is the baseline against which TP-AGT-004's composite finding is meaningful.

**Wave 3 — trajectory and process.** TP-AGT-001 (long-horizon goal fidelity), TP-AGT-002 (mid-execution intent change), TP-AGT-010 (workflow conformance), TP-AGT-007 (multi-agent error reinforcement). All four run long, realistic workflows and share the synthetic case library; run them as one campaign to amortise scenario construction, which is the dominant cost.

**Wave 4 — highest-consequence and least-mature.** TP-AGT-012 (irreversible-action gating), TP-AGT-008 (memory poisoning, ★1), TP-AGT-013 (computer-use GUI, ★1). TP-AGT-012 is placed late deliberately: by then the reviewer knows the agent's tool surface, its trace quality and its validation behaviour, and can construct genuinely adversarial gate-bypass vectors rather than obvious ones. The two ★1 procedures are placed last so that the weakest-methodology findings are made by the most context-rich reviewer.

**Cross-domain:** TP-AGT-008 shares its memory-store substrate with TP-DAT-010 (memory governance) — build the synthetic multi-tenant conversational corpus once. TP-AGT-009 is the agentic sibling of TP-MOD-013 (prompt change control); run them together with a single pathway enumeration. TP-AGT-003's adversarial tool-elicitation overlaps the SEC-domain injection testing (IRQ-SEC-003); coordinate so the agent is not being probed by two reviewers with incompatible environment states.


TP-AGT-014's place: with the domain series in Stage 4c (PLAYBOOK_OVERVIEW.md §6); its canvas records no intra-domain dependency, so it schedules on environment readiness.
### Cross-IRQ dataset reuse opportunities

1. **Synthetic FS case library with ground truth** — the 15–25 step AML investigations and multi-stage claims settlements built for TP-AGT-001 serve directly as the substrate for TP-AGT-002 (intent-change injection points), TP-AGT-010 (conformance reconciliation) and TP-AGT-007 (error seeding at decision points). Build once, annotate three times.
2. **Drift traps (TP-AGT-001)** — the misleading intermediate signals constructed for goal-drift testing are reusable as the ambiguity pressure in TP-AGT-010's edge-case set, where they tempt step omission rather than goal divergence.
3. **Tool inventory (TP-AGT-003)** — the enumerated set of technically callable tools is the input to TP-AGT-004's composite-combination space and to TP-AGT-006's aggregate-permission-tree ceiling. Enumerating it three times independently is waste; enumerating it once badly is the single most consequential error in this domain.
4. **Fault-injection harness (TP-AGT-005)** — the apparatus for injecting malformed parameters and spoofed API responses is reused for TP-AGT-012's error-injection vector (an agent believing clearance was given when it was not) and for TP-AGT-008's poisoned-memory injection.
5. **Trace-reconstruction scenario (TP-AGT-011)** — the deliberately-engineered run containing an abandoned branch, a retried call and a sub-agent delegation is a compact regression case reusable as a smoke test at the start of every subsequent procedure, confirming trace capture is still functioning.
6. **Multi-session memory corpus** — shared with TP-DAT-010 as noted above.
7. **Consequential-action scenario set** — payment confirmation, record deletion and external communication scenarios built for TP-AGT-012 are reused as the high-materiality GUI workflows in TP-AGT-013.

### Domain-level evidence maturity caveat (state in every AGT report)

Per the canvas domain preamble: the control catalogue draws on Anthropic's Agentic Misalignment and Project Vend work, OpenAI's Practices for Governing Agentic AI Systems and Operator/Deep Research system cards, Microsoft's Taxonomy of Failure Modes in Agentic AI Systems, the OWASP Agentic Security Initiative's *Agentic AI: Threats and Mitigations* (February 2025), NIST AI 600-1, METR's autonomous-task evaluation work, and the multi-agent risk research of Hammond et al. and Motwani et al. — but almost none of this has matured into a benchmarked testing standard. Public incidents used as failure-chain analogues (Knight Capital, the Replit production-database deletion, the xAI Grok code-path update that unexpectedly incorporated deprecated instructions into a production bot, and Anthropic's disclosure of an agentic cyber-espionage campaign it attributes, with high confidence, to a state-sponsored actor) are the closest available real-world evidence, since documented FS-sector agentic incidents remain sparse. Expect ★2 throughout, ★1 for memory poisoning and computer-use safety. Inflating these ratings would misrepresent the state of the art.

### Safety rules specific to this domain

Beyond the non-production rule, three additional disciplines apply to every AGT procedure:

- **Benign payloads only.** Where a procedure injects content designed to manipulate the agent (injected instructions, spoofed responses, poisoned memory entries), the content is **benign in effect**: it directs the agent toward a *detectable, harmless* sandbox action, never toward genuinely harmful behaviour. Payloads are documented in the evidence pack **by technique category and structure**, never as reusable working strings, and never containing credentials, secrets, real personal data or exploit code.
- **Pre-run endpoint verification.** Before each procedure's first run, the reviewer independently confirms that every tool the agent can reach resolves to a sandbox endpoint. Recorded as an attestation.
- **Kill-switch readiness.** The reviewer holds an out-of-band means of halting the agent for every run, and confirms it works before starting. This is separate from testing the firm's own containment mechanism (TP-AGT-012), which is a finding, not a safety net.

### Indicative total effort

**64 reviewer-days** across the fourteen procedures, excluding harness build (allow 10–15 reviewer-days for first-time agentic harness establishment — materially more than DAT or MOD, and the largest single setup cost in the FAIAS programme) and non-reviewer support effort.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-AGT-001: PLAYBOOK_AGT_001.md
- TP-AGT-002: PLAYBOOK_AGT_002.md
- TP-AGT-003: PLAYBOOK_AGT_003.md
- TP-AGT-004: PLAYBOOK_AGT_004.md
- TP-AGT-005: PLAYBOOK_AGT_005.md
- TP-AGT-006: PLAYBOOK_AGT_006.md
- TP-AGT-007: PLAYBOOK_AGT_007.md
- TP-AGT-008: PLAYBOOK_AGT_008.md
- TP-AGT-009: PLAYBOOK_AGT_009.md
- TP-AGT-010: PLAYBOOK_AGT_010.md
- TP-AGT-011: PLAYBOOK_AGT_011.md
- TP-AGT-012: PLAYBOOK_AGT_012.md
- TP-AGT-013: PLAYBOOK_AGT_013.md
- TP-AGT-014: PLAYBOOK_AGT_014.md

---
---

## Effort Summary — AGT Domain

| Procedure | IRQ | ★ | Reviewer-days |
|---|---|---|---|
| TP-AGT-001 | IRQ-AGT-001 Long-horizon goal fidelity | ★2 | 6 |
| TP-AGT-002 | IRQ-AGT-002 Mid-execution intent change | ★2 | 4 |
| TP-AGT-003 | IRQ-AGT-003 Tool access / least privilege | ★2 | 3 |
| TP-AGT-004 | IRQ-AGT-004 Composite actions | ★2 | 5 |
| TP-AGT-005 | IRQ-AGT-005 Tool-call validation | ★2 | 5 |
| TP-AGT-006 | IRQ-AGT-006 Delegation bounds | ★2 | 4 |
| TP-AGT-007 | IRQ-AGT-007 Multi-agent error reinforcement | ★2 | 5 |
| TP-AGT-008 | IRQ-AGT-008 Memory poisoning | **★1** | 4 |
| TP-AGT-009 | IRQ-AGT-009 Prompt/scaffold configuration control | ★2 | 3 |
| TP-AGT-010 | IRQ-AGT-010 Workflow conformance | ★2 | 5 |
| TP-AGT-011 | IRQ-AGT-011 Trace completeness | ★2 | 4 |
| TP-AGT-012 | IRQ-AGT-012 Irreversible-action gating | ★2 | 6 |
| TP-AGT-013 | IRQ-AGT-013 Computer-use GUI safety | **★1** | 5 |
| TP-AGT-014 | IRQ-AGT-014 Evaluation-environment containment | ★2 | 5 |
| **Total** | **14 procedures** | — | **64 reviewer-days** |

Excludes first-time agentic harness build (10–15 reviewer-days — the largest setup cost in the FAIAS programme), GUI replica provisioning, and non-reviewer support effort (platform engineers, SMEs, second reviewer time), costed separately.

**Reporting reminder:** all fourteen AGT conclusions are judgement-based under METHODOLOGY_STANDARDS §3c. The two ★1 procedures (TP-AGT-008, TP-AGT-013) carry the additional caveat that the methodology is novel, no standard evaluation exists, and result quality depends entirely on assessor expertise.

---

**Document control**
Version: the release version in `README.md` | Status: Active
Change Log: v1.0 (2026-07) — Initial publication. Thirteen AGT procedures derived 1:1 from CANVASES_AGT.md; ★ ratings carried over unchanged (eleven ★2, two ★1); no new citations introduced.
v1.1 (2026-08-25) — TP-AGT-014 (evaluation-environment containment testing) added, derived 1:1 from the IRQ-AGT-014 canvas; domain totals move to fourteen procedures and 64 reviewer-days; ★ distribution becomes twelve ★2 and two ★1. The domain's ★ uniformity is recorded in the preamble as a consistency observation, expressly not a ground for any individual rating.
v1.2.1 (2026-09-19) — Domain Testing Overview: two of the public incidents used as failure-chain analogues re-described as the canvas domain preamble now describes them — the xAI Grok incident as xAI's statement of 12 July 2025 gives it, a code-path update that unexpectedly incorporated deprecated instructions into a production bot, where it had been called an un-gated system-prompt change, which the statement does not say; and the campaign Anthropic disclosed as one it attributes, with high confidence, to a state-sponsored actor, where it had been called a state-actor campaign. TP-AGT-014's method classification counts AISI's stated post-incident lessons as three, not four, as the canvas's Independent Test now does. No test step, ★ rating, method class or reviewer-day estimate changes, and no new citations.
v1.3.0 (2026-10) — TP-AGT-014's ★ summary places AISI's statement that the toolkit's isolation is evaluator-configured in AISI's technical guidance for the toolkit as well as in its August 2026 dispute, as the canvas's Independent Test now does. No test step, ★ rating, method class or reviewer-day estimate changes.
v1.3.2 (2026-10-03) — TP-AGT-014 corrected (00_Admin/CORRECTION_LOG_2026-10-03.md §8). No ★ rating or reviewer-day figure changes.
