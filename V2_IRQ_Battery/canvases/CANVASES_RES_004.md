# CANVAS: IRQ-RES-004

## 1. IRQ ID & Title
**IRQ-RES-004: Unrehearsed Rollback of Model, Prompt, Index and Agent Memory Components**

Register question: "Can the firm roll back to a known-good state — model version, prompts, index, agent memory — within recovery objectives, and has restoration been rehearsed?"

## 2. Business Activities Affected
- **Any AI system subject to configuration or content change (model version, prompt template, RAG index, agent memory):** if a change introduces a defect, the business activity it supports needs a genuine, rehearsed path back to the last known-good state within a recovery time objective, not just a theoretical rollback plan.
- **RAG-grounded services following a corpus or embedding-model change:** if a re-index introduces a quality regression, rollback must cover the index itself, not only code/model version.
- **Persistent agent memory-dependent workflows:** where agent memory accumulates over time (case history, learned preferences), rollback must address memory state specifically, which is qualitatively different from rolling back stateless code.

## 3. AI Behaviour(s)
- System behaviour is determined by a combination of components that can each independently change: model version, system prompt/template, decoding parameters, RAG index, and (for agentic systems) accumulated memory state.
- A defect introduced by any one of these components (e.g. a prompt change causing systematic errors) requires reverting that specific component to its prior known-good state without necessarily reverting the others.
- Rollback of some components (e.g. agent memory that has since accumulated new, valid entries) is more complex than a simple version revert, because naive rollback could also discard legitimate subsequent state.

## 4. Failure Mode
> The firm cannot roll back one or more of its AI system's behavioural components (model version, prompts, RAG index, agent memory) to a known-good state within its defined recovery objectives, because restoration has not been version-controlled, tested or rehearsed for that component type — so a defect introduced by a change cannot be reliably or promptly undone.

## 5. Potential Consequences
- **Institution:** A defective change (prompt regression, bad re-index, corrupted agent memory) persists in production longer than necessary because rollback is improvised rather than rehearsed, extending customer harm and remediation cost.
- **Customer:** Continued exposure to a known defect while the firm attempts an unrehearsed recovery, potentially compounding the original harm.
- **Regulator:** Failure to meet recovery time/point objectives (RTO/RPO) is a direct operational resilience gap under DORA and the UK operational resilience regime, and undermines the credibility of change management controls generally.

## 6. Failure Chain
```
A behavioural component is changed (prompt update, model version
bump, corpus re-index, agent memory update) without full version
control or a tested rollback path for that specific component type
  ↓ (IRQ-MOD-013: prompt/config changes not subject to change control
     with behavioural regression testing)
The change introduces a defect (accuracy regression, tone drift,
retrieval quality drop, corrupted memory state), detected in
production
  ↓ (IRQ-RES-004 — THIS IRQ: no rehearsed rollback path exists for
     the affected component; recovery is improvised)
Recovery takes materially longer than the firm's stated RTO;
customers remain exposed to the defect throughout
  ↓
Extended customer harm; post-incident review finds rollback was
never rehearsed and its actual recovery time was unknown before
the incident

Control Breakpoints:
  • IRQ-RES-004: version-controlled, rehearsed rollback for every
    behavioural component type, tested against defined RTO/RPO
  • IRQ-MOD-013: prompt/config version control and regression testing
    reduces the frequency defects reach production in the first place
  • IRQ-TPR-006: index rebuild/rollback specifically for embedding/
    vector infrastructure dependencies
```

## 7. Why a Domain Expert May Miss It
- Traditional IT disaster recovery planning is built around infrastructure and code rollback (deploy the previous release); prompts, RAG indices and agent memory are less obviously "versioned artefacts" requiring the same rollback discipline, especially where they are managed by a different team (data science) than infrastructure (platform engineering).
- Agent memory rollback is uniquely tricky and easy to overlook: naive rollback to a prior memory snapshot discards legitimate interactions that occurred since, creating a new problem (lost valid context) while solving the original one.
- "We use version control for our code" is treated as sufficient evidence of rollback capability, without verifying that prompts, index configuration and memory state are equally version-controlled and equally rehearsed for restoration.
- Recovery time objectives are typically set and tested for infrastructure failure scenarios; they are rarely re-tested specifically for "roll back a bad prompt change" or "roll back a bad re-index," which can have materially different recovery mechanics and timeframes.

## 8. Assurance Objective
**AO-RES-004:** The firm shall be able to roll back every behavioural component of an AI system — model version, prompts, RAG index, and agent memory where applicable — to a known-good state within defined recovery time and recovery point objectives, and this restoration capability shall be rehearsed, not merely designed.

## 9. Expected Controls (Traced)
- **Version control for all behavioural components** — [linked IRQ-MOD-013] — [established software configuration management practice, extended to prompts/config per ISO/IEC 5338:2023 lifecycle configuration management] — every component that affects system behaviour is versioned, not only application code.
- **Defined RTO/RPO per component type, tested** — [Regulation (EU) 2022/2554, DORA, Art. 11 (ICT business continuity policy) and Art. 12(6) (recovery time and recovery point objectives)] — recovery objectives are set and tested for each behavioural component, not only infrastructure.
- **Index rebuild/rollback procedure** — [linked IRQ-TPR-006] — specific rollback mechanism for RAG index state, tested against RTO.
- **Agent memory rollback with legitimate-state preservation** — Emerging Practice — no published FS-sector standard exists for safely rolling back accumulated agent memory without discarding subsequent legitimate state; this is an active, largely unsolved engineering problem addressed here as an assurance objective pending mature tooling.
- **Restoration rehearsal / disaster recovery testing** — [PRA SS1/21, March 2021, recoverability expectation] — periodic testing that restoration actually meets the stated RTO/RPO, not a paper exercise.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "everything is version controlled" with no restoration test evidence — **L1**.
- Version control and rollback design specification for each component type (model, prompt, index, memory) — **L2**.
- Staging restoration test: roll back each component type from a simulated defective state to a known-good state; measure time taken against RTO — **L3**.
- Independent audit confirming restoration testing was performed to the documented standard, including agent memory rollback specifically — **L4**.
- Records of an actual production rollback event (if one occurred), including time taken and any residual issues (e.g. lost legitimate memory state) — **L5**.

## 11. Independent Test
> In a non-production environment, deliberately introduce a defect into each behavioural component type (prompt, model version pin, RAG index, agent memory where applicable) and execute the firm's documented rollback procedure. Measure time-to-restore against the stated RTO, and verify the restored state is genuinely known-good (behavioural regression test passes) without unacceptable loss of legitimate subsequent state, particularly for agent memory. — **★2 Confidence — as at FAIAS v1.2.0 (12 September 2026)** (the generic limb is research-anchored, not practice-asserted: partial rollback from a write-ahead log is a published, peer-reviewed recovery method [Mohan et al., ACM TODS 17(1):94–162, 1992], and the dependency tracing that determines which downstream state a reverted component contaminated rests on peer-reviewed program-slicing work [Weiser, IEEE TSE SE-10(4):352–357, 1984] — ★3 on §6's "grounded in peer-reviewed research; multiple independent research groups" limbs, with ★4's "adopted by ≥2 independent institutions" limb plausible but not evidenced here. The AI-specific limb sits at ★2 and binds the blend: three independent groups published agent-memory rollback methods in 2026 [arXiv:2607.27773; arXiv:2608.10502; arXiv:2605.07242], one with a 150-case controlled fault-injection benchmark measuring recovery against benign-state preservation, but **none is peer-reviewed and none carries a journal reference or DOI**, so ★3's peer-review limb is not met. No agreed benchmark exists: the first of these describes itself as the first open-source system and benchmark for systematic global memory rollback. Published method also stops short of the canvas's full question — rollback repairs agent-maintained memory and trace state and "cannot undo an irreversible external side effect" [arXiv:2608.10502 §3], which is the limit a firm's own RTO claim must be tested against. Where a firm has no agent memory rollback capability at all, this is stated as "none established" rather than scored.)

## 12. Pass Indicators
- Restoration testing for model version, prompt and index components meets defined RTO in all tested cases.
- Restored state passes behavioural regression testing, confirming it is genuinely known-good.
- Agent memory rollback approach (if the system uses persistent memory) is documented and tested, with a defined, accepted approach to legitimate-state preservation or an explicit, risk-accepted limitation.
- Restoration has been rehearsed within the last review cycle, not only designed.

## 13. Fail Indicators
- No version control exists for prompts, index configuration or agent memory; only application code is versioned.
- Restoration testing has never been performed; RTO is asserted but unmeasured.
- Agent memory rollback, where applicable, has no defined approach at all — the system has no way to recover from a corrupted memory state other than a full reset losing all history.
- A production rollback event took materially longer than the stated RTO.

## 14. Reporting Language
**Pass:** "Restoration testing across model version, prompt and index components meets defined RTO with behavioural regression confirming known-good state; agent memory rollback approach is documented, tested and accepted. Conclusions rest on ★2 methodology — infrastructure rollback testing is mature, agent memory rollback is genuinely immature — and should be read with that asymmetry in mind."

**Fail:** "No rollback capability has been tested for prompts, index or agent memory; only application code deployment rollback has been rehearsed. This is a material operational resilience gap: a defect introduced via any of these components cannot be reliably or promptly undone, extending customer exposure indefinitely."

**Partial:** "Model version and prompt rollback are tested and meet RTO; RAG index rollback exists but has not been rehearsed at production corpus scale; agent memory rollback has no established approach. Remediation should prioritise index-scale testing and explicitly document the accepted limitation on memory rollback pending mature tooling."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (defects are correctable within a tested recovery window, limiting cumulative exposure)
  Likelihood: 2 (component changes introducing defects are a normal, if infrequent, occurrence)
  Detectability: 2 (a defective change is typically caught by monitoring or complaint within the recovery window, if monitoring per RES-005/006 is functioning)
  Recoverability: 2 (rehearsed rollback restores known-good state within defined objectives, by design)
  Novelty: 3 (prompt/index/memory rollback as distinct disciplines from code rollback is genuinely AI-specific)

If controls are absent or degraded:
  Severity: 3 (a defective change persists for an extended, unbounded period; customer harm accumulates)
  Likelihood: 2 (plausible given change frequency in actively developed AI systems, though not every change introduces a defect)
  Detectability: 2 (the defect itself is usually detectable; the gap here is in remediation speed, not detection)
  Recoverability: 4 (agent memory rollback in particular may have no established recovery path at all, making this the single hardest-to-recover component in the entire AI stack)
  Novelty: 3 (requires deliberate extension of standard software rollback discipline to non-code artefacts)

Residual risk interpretation: Recoverability is the standout concern for the agent memory sub-case specifically; firms should explicitly flag "no established rollback" for memory rather than implying a false equivalence with mature code/model rollback.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Contained where recovery is genuinely rehearsed; escalates where rollback is untested and remediation is improvised |
| **Likelihood** | 2 | Component-level defects are a normal, periodic occurrence in actively developed AI systems |
| **Detectability** | 2 | Defects are usually caught by existing monitoring; the gap is remediation speed, not detection |
| **Recoverability** | 3 | Weighted up specifically because agent memory rollback is genuinely immature/unsolved in many deployments |
| **Novelty** | 3 | Extending rollback discipline from code to prompts/index/memory is a non-obvious extension for traditional DR planning |

## 17. Regulatory Basis
> [Regulation (EU) 2022/2554, DORA, Art. 11 and Art. 12(6)] requires an ICT business continuity policy, with recovery time and recovery point objectives set under Art. 12(6), extended here to all behavioural components of an AI system, not only underlying infrastructure/code. [PRA, SS1/21, March 2021] establishes the general recoverability testing expectation this IRQ applies to model version, prompt, index and memory rollback specifically.

## 18. Research Basis
> No peer-reviewed research addresses "AI behavioural component rollback" as a named discipline, and a targeted search on 12 September 2026 located no venue-published primary on agent-memory rollback at all [UNVERIFIED — searched; none found]. The generic limb is nonetheless peer-reviewed and long settled: [Mohan, C., Haderle, D., Lindsay, B., Pirahesh, H., Schwarz, P., 1992, "ARIES: a transaction recovery method supporting fine-granularity locking and partial rollbacks using write-ahead logging", ACM Transactions on Database Systems 17(1):94–162, https://doi.org/10.1145/128765.128770] specifies partial rollback to a known-good state formally, and [Weiser, M., 1984, "Program Slicing", IEEE Transactions on Software Engineering SE-10(4):352–357, https://doi.org/10.1109/TSE.1984.5010248] supplies the dependency-tracing basis for deciding which downstream state a reverted component has contaminated — both cited as the generic foundation by the 2026 agent-memory work below.
>
> The AI-specific limb is now evidenced, and its evidence is preprint-only. Three independent author groups published agent-memory rollback methods in 2026, with no author overlap: [Su, Y., Xu, W., Zuo, C., Bertino, E., 2026, "ChronoMem: Version Control and Semantic Rollback for Large Language Model Agent Memory", arXiv:2607.27773v2] implements commit-on-write whole-memory snapshots with natural-language rollback inside Google's Agent Development Kit, and measures that prompt-based "undo" effectively fails — 0.0–1.2% task-specific accuracy on the MemoryAgentBench Accurate Retrieval subset, against 44.6–55.1% for snapshot restoration; [Yu, C., Wang, Y., Zhang, J., Duan, Y., Zheng, M., Wu, Z., Shi, K., Cai, T., 2026, "From Faulty Memories to Corrected Actions: Dependency-Guided Rollback Repair for Memory-Augmented Agents", arXiv:2608.10502v1] evaluates recovery on a 150-case controlled benchmark over four injected memory-fault classes (poisoned, stale, wrong-user, summary-drift) and reports both faulty-memory removal and benign-memory preservation as separate metrics; [Zhao, Y., Dai, C., Kou, M., Xiu, Y., 2026, "MEMOREPAIR: Barrier-First Cascade Repair in Agentic Memory", arXiv:2605.07242v1] formalises the cascade-update problem in which descendants of an invalidated record "remain visible and steer future actions with stale support". **None of the three carries a journal reference, a non-arXiv DOI or a recorded acceptance**, so none supports a rating above ★2 under §6.
>
> Two limits are load-bearing and are recorded rather than smoothed. First, rollback in this literature repairs agent-maintained memory and execution state and "cannot undo an irreversible external side effect" [arXiv:2608.10502 §3] — so a firm's rollback RTO claim is only as good as the compensating action behind each side-effecting tool call. Second, legitimate-state preservation remains unsolved in the implementations themselves: ChronoMem maintains "a linear version history and truncates versions after a rollback (Git 'reset'-style)", with branching "not implemented or evaluated in this work", and concludes that its results "demonstrate the architectural soundness and robustness of semantic rollback under controlled long-horizon settings, rather than claiming a complete characterization of rollback behavior in production-scale agent deployments" [arXiv:2607.27773v2, Limitations]. The risk framing — that memory corruption compounds across consolidation cycles rather than staying local — is set out in [Lam, C., Li, J., Zhang, L., Zhao, K., 2026, "Governing Evolving Memory in LLM Agents: Risks, Mechanisms, and the Stability and Safety Governed Memory (SSGM) Framework", arXiv:2603.11768v2], a conceptual governance survey with no empirical evaluation, cited here for the risk taxonomy only and **not** as a rollback method.
>
> **Research basis last reviewed:** 12 September 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-MOD-013 (B.6 Model Updates & Configuration: version control and regression testing of prompts/config)
  - IRQ-TPR-006 (F.3 Dependencies: index rebuild/rollback specific to embedding/vector infrastructure)
  - IRQ-RES-003 (G.2 Containment & Recovery: rollback complements time-bound containment)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 11.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] Prudential Regulation Authority, 2021. "SS1/21 — Operational resilience: Impact tolerances for important business services."
    Published: March 2021
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss

[3] International Organization for Standardization, 2023. "ISO/IEC 5338:2023 — AI system life cycle processes."
    Published: 2023
    URL: https://www.iso.org/standard/81118.html

[4] Mohan, C., Haderle, D., Lindsay, B., Pirahesh, H., Schwarz, P., 1992. "ARIES: a transaction recovery method supporting fine-granularity locking and partial rollbacks using write-ahead logging." ACM Transactions on Database Systems 17(1):94–162.
    Published: March 1992
    URL: https://doi.org/10.1145/128765.128770

[5] Weiser, M., 1984. "Program Slicing." IEEE Transactions on Software Engineering SE-10(4):352–357.
    Published: July 1984
    URL: https://doi.org/10.1109/TSE.1984.5010248

[6] Su, Y., Xu, W., Zuo, C., Bertino, E., 2026. "ChronoMem: Version Control and Semantic Rollback for Large Language Model Agent Memory." arXiv:2607.27773v2 (preprint; not peer-reviewed).
    Published: 5 August 2026 (v1: 30 July 2026)
    URL: https://arxiv.org/abs/2607.27773

[7] Yu, C., Wang, Y., Zhang, J., Duan, Y., Zheng, M., Wu, Z., Shi, K., Cai, T., 2026. "From Faulty Memories to Corrected Actions: Dependency-Guided Rollback Repair for Memory-Augmented Agents." arXiv:2608.10502v1 (preprint; not peer-reviewed).
    Published: 11 August 2026
    URL: https://arxiv.org/abs/2608.10502

[8] Zhao, Y., Dai, C., Kou, M., Xiu, Y., 2026. "MEMOREPAIR: Barrier-First Cascade Repair in Agentic Memory." arXiv:2605.07242v1 (preprint; not peer-reviewed).
    Published: 8 May 2026
    URL: https://arxiv.org/abs/2605.07242

[9] Lam, C., Li, J., Zhang, L., Zhao, K., 2026. "Governing Evolving Memory in LLM Agents: Risks, Mechanisms, and the Stability and Safety Governed Memory (SSGM) Framework." arXiv:2603.11768v2 (preprint; not peer-reviewed; conceptual survey, cited for the risk taxonomy only).
    Published: 19 May 2026 (v1: 12 March 2026)
    URL: https://arxiv.org/abs/2603.11768
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** G.2 (Operational Resilience domain, Containment & Recovery)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): DR planning assumes code rollback covers restoration; prompts, index and memory are non-obvious versioned artefacts requiring separate rollback discipline.
✓ Test 2 (Plausible Harm): Grounded in DORA business continuity RTO/RPO obligations, applied to AI-specific components.
✓ Test 3 (Testable): Answerable via staged defect-and-restore testing per component type.
✓ Test 4 (Decision-Relevant): Outcome gates whether stated RTO/RPO commitments can be trusted for AI-driven services.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): ★2 justification rewritten at an unchanged rating (no ★ movement) — the generic limb re-anchored from "established practice" to peer-reviewed primaries (Mohan et al., ACM TODS 17(1), 1992; Weiser, IEEE TSE SE-10(4), 1984) and the AI-specific limb to three independent 2026 agent-memory rollback methods (arXiv:2607.27773; arXiv:2608.10502; arXiv:2605.07242), each recorded as not peer-reviewed; field 18 rewritten, six references added at §20; the TP-RES-004 playbook sheet carries the same basis.
```

---
---

