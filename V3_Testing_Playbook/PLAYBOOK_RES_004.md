# TP-RES-004 — Behavioural-Component Rollback Rehearsal

## 1. Procedure Identity
**Procedure ID:** TP-RES-004
**IRQ:** IRQ-RES-004 — Unrehearsed Rollback of Model, Prompt, Index and Agent Memory Components
**Assurance objective:** AO-RES-004 — The firm shall be able to roll back every behavioural component of an AI system — model version, prompts, RAG index, and agent memory where applicable — to a known-good state within defined recovery time and recovery point objectives, and this restoration capability shall be rehearsed, not merely designed.
**Subdomain:** G.2 Containment & Recovery
**★ Confidence (carried from canvas, unchanged):** ★2 — the generic limb is research-anchored, not practice-asserted: partial rollback from a write-ahead log is a peer-reviewed recovery method [Mohan et al., ACM TODS 17(1):94–162, 1992] and the dependency tracing that determines which downstream state a reverted component contaminated rests on peer-reviewed program-slicing work [Weiser, IEEE TSE SE-10(4):352–357, 1984]. The AI-specific limb binds the blend at ★2: three independent groups published agent-memory rollback methods in 2026 [arXiv:2607.27773; arXiv:2608.10502; arXiv:2605.07242], one with a 150-case controlled fault-injection benchmark, but none is peer-reviewed and no agreed benchmark exists, so ★3's peer-review limb is not met. Where a firm has no agent memory rollback capability at all, this should be stated as "none established" rather than scored.
**Method classification:** Adapted Industry Practice for model/prompt/index components; Emerging Practice (No Established Benchmark) for agent memory.

## 2. Preconditions
**Environment:** Non-production environment with independent version control over each behavioural component, and a behavioural regression test suite that can be run against a restored state.
**Access required:** Write access to the staging deployment pipeline sufficient to introduce and then revert a defect in each component type; read access to version-control history for prompts, model version pins, index build configuration and memory stores; read access to the documented RTO/RPO for the system.
**Artefacts required:** Documented rollback procedure per component type; stated RTO and RPO; behavioural regression test suite and its last known-good results; version-control history for all four component types; any prior rollback rehearsal or real rollback records.
**Personnel required:** Deployment/platform engineer to execute the documented procedure (the reviewer observes; the reviewer must not perform the rollback, since the procedure under test is the firm's ability to do it); system technical owner; reviewer.
**Data handling:** Where agent memory contains representations derived from customer interactions, use a memory store populated only with synthetic session history. Never restore a production memory snapshot into a test environment.

## 3. Test Design
A defect is deliberately introduced into each behavioural component in turn, and the firm's own documented rollback procedure is executed by the firm's own staff while the reviewer times and observes. Four component types:

- **P — Prompt / system instruction:** substitute a materially altered instruction.
- **M — Model version pin:** repoint to a different model version.
- **I — RAG index:** corrupt or replace the index with a stale or partially built version.
- **A — Agent memory** (where the system uses persistent memory): inject erroneous entries into the memory store.

Success is not "the component reverted". Success is: reverted *within RTO*, verified *genuinely known-good* by behavioural regression test, and *without unacceptable loss of legitimate subsequent state*. That third criterion is what makes component A hard: rolling agent memory back to a pre-corruption snapshot typically discards all legitimate memory written since.

## 4. Steps
1. Obtain the documented rollback procedure and the stated RTO/RPO. **Record:** whether a procedure exists per component type or only for application code; the RTO and RPO values and their approval source.
2. Inspect version-control coverage. **Record:** for each of P, M, I, A — is it under version control at all; what granularity; who can change it; is change linked to a change record.
3. Run the behavioural regression suite against the current known-good state. **Record:** baseline pass results; suite coverage (how many behaviours it actually asserts).
4. **Component P.** Introduce a materially altered system prompt. Confirm the behavioural change is detectable via the regression suite. **Record:** which regression assertions fail — if none fail, the suite itself is inadequate and this is a finding.
5. Instruct the platform engineer to execute the documented rollback. Start the clock at the moment the decision to roll back is taken. **Record:** time to restore; steps that required improvisation beyond the documented procedure; whether any step required a person who was not on call.
6. Re-run the regression suite against the restored state. **Record:** full pass/fail; any assertion that passes at baseline but fails post-restore (indicating the restored state is not genuinely known-good).
7. Repeat steps 4–6 for **Component M** (model version pin) and **Component I** (RAG index). For I, additionally record whether the index rebuild is required and how long it takes, since rebuild time frequently dominates RTO.
8. **Component A** (if applicable). Inject erroneous entries into agent memory. Execute the documented rollback. **Record:** whether any defined approach exists at all; if the approach is a full reset, record what legitimate state is lost and whether that loss is a documented, risk-accepted limitation or an unexamined consequence.
9. Where no agent memory rollback capability exists, record "none established" rather than assigning a failing measurement. **Record:** the absence, and whether it is acknowledged in the system's risk documentation.
10. Review the last review cycle for evidence of a rehearsal. **Record:** date and scope of the most recent rehearsal; whether any real production rollback occurred and how long it actually took versus RTO.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Time-to-restore per component | The firm's own stated RTO | RTO/RPO are established disciplines; the value is firm-set |
| Regression suite pass rate post-restore | 100% of baseline-passing assertions must pass post-restore | Reviewer judgement against the firm's own baseline |
| Regression suite adequacy | Reviewer judgement — no established threshold. If an injected material defect produces no regression failure, the suite does not evidence "known-good" | Bespoke |
| Agent memory legitimate-state loss | Reviewer judgement — no established threshold; record as "none established" where no approach exists | The canvas is explicit that this area is unsolved |

## 6. Interpretation (per CANVASES_RES.md fields 12–14)
**Pass** where: restoration testing for model version, prompt and index meets the defined RTO in all tested cases; the restored state passes behavioural regression testing; the agent memory rollback approach (where persistent memory is used) is documented and tested with a defined accepted approach to legitimate-state preservation or an explicit risk-accepted limitation; and restoration has been rehearsed within the last review cycle.

**Fail** where: no version control exists for prompts, index configuration or agent memory (only application code is versioned); restoration has never been performed and RTO is asserted but unmeasured; agent memory rollback has no defined approach at all beyond a full reset losing all history; or a production rollback event took materially longer than the stated RTO.

**Partial** — the common pattern: P, M and I roll back cleanly within RTO while A has no approach. Report as Partial with the agent-memory gap named, and note explicitly that the absence is an industry-wide immaturity rather than a firm-specific negligence, while still requiring the firm to risk-accept it formally.

## 7. Evidence Outputs
- Documented rollback procedure and stated RTO/RPO as obtained — **L2**
- Version-control coverage matrix across P/M/I/A — **L2**
- Rehearsal execution log with per-component timings — **L3**
- Behavioural regression results, baseline and post-restore — **L3**
- Reviewer's independent assessment that restored states were genuinely known-good — **L4**
- Real production rollback records with actual elapsed time — **L5**

## 8. Common Pitfalls & Limitations
- **The reviewer performing the rollback.** The capability under test is the *firm's*. If the reviewer improvises the restore, the test measures the reviewer, not the control.
- **A regression suite that asserts nothing behavioural.** Many suites test API contract, not model behaviour. Step 4 exists to expose this: if a materially altered prompt passes the suite, the suite cannot evidence "known-good".
- **Index rebuild time excluded from RTO.** Firms frequently measure "repoint to previous index" and omit the rebuild required when the previous index is stale. Record both.
- **Agent memory scored rather than described.** Where no capability exists, the canvas directs "none established". Do not invent a measurement to fill the cell.
- **Rehearsal recency.** A rehearsal from three years ago against a since-rearchitected stack is not evidence of current capability.

## 9. Time / Effort Estimate
**4 reviewer-days**: 0.5 day artefact and version-control review, 2 days defect injection and rollback execution across all applicable components, 0.5 day regression analysis, 1 day working papers. Reduce by 0.5 day where the system has no persistent agent memory.

---
---

