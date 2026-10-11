# TP-RES-007 — AI Dependency Mapping and Scenario Library Sweep

## 1. Procedure Identity
**Procedure ID:** TP-RES-007
**IRQ:** IRQ-RES-007 — AI Dependencies Absent from IBS Mapping and Scenario Testing
**Assurance objective:** AO-RES-007 — The firm shall explicitly map AI dependencies into its important business service resilience documentation and include severe-but-plausible AI-specific scenarios (provider outage, model behavioural drift, agentic misbehaviour, correlated concentration events, disruption by externally originated synthetic media) within its scenario testing programme.
**Subdomain:** G.4 Resilience Mapping
**★ Confidence (carried from canvas, unchanged):** ★3 — IBS mapping and scenario testing methodology is an established, regulator-mandated discipline; the specific extension to AI-specific scenario content is less standardised across the industry, moderating confidence from ★4.
**Method classification:** Adapted Industry Practice — FCA SYSC 15A / PRA SS1/21 mapping and scenario-testing review, extended to AI dependency types.

## 2. Preconditions
**Environment:** Documentary review; no system access required. This is the least environment-dependent RES procedure and can run in parallel with the others.
**Access required:** Read access to the IBS register and full current mapping documentation; read access to the complete scenario testing library and the last two cycles of scenario test reports (reviewer-set design minimum, disclosed at scoping); read access to the AI inventory (ideally the version verified under TP-GOV-002) and to the concentration assessment produced under the TPR domain.
**Artefacts required:** IBS register; IBS mapping documents for the sampled services; scenario testing library and test reports; AI inventory; third-party concentration assessment (IRQ-TPR-008 output); the operational resilience self-assessment.
**Personnel required:** Op-res lead; the mapping owner for each sampled IBS; reviewer.
**Data handling:** Mapping and scenario documents may contain vendor-confidential terms; handle under the engagement confidentiality regime. No customer data involved.

## 3. Test Design
A two-directional reconciliation plus a library-content assessment:

- **Direction 1 (inventory → mapping):** take known AI systems from the inventory and check whether each appears as an identified dependency in the mapping of every IBS it supports. This catches AI dependencies invisible to op-res.
- **Direction 2 (mapping → inventory):** take the mapping's technology dependency lists and check whether any entry is in fact AI-based but recorded generically as "technology" or "vendor platform". This catches AI hidden inside an existing mapping entry.
- **Library assessment:** test the scenario library against the five AI-specific severe-but-plausible scenario types named in the assurance objective — the fifth being at least one scenario in which an important business service is disrupted by externally originated synthetic media, scoped to the firm's own response, communications and impact-tolerance position; and assess the design and results of any that have been exercised.

Sampling: all IBSs where the AI inventory indicates a material AI dependency, or a risk-based sample of at least five (reviewer-set design minimum, disclosed at scoping) where more exist.

## 4. Steps
1. Obtain the AI inventory and the IBS register. **Record:** inventory version and whether it has been completeness-verified (per TP-GOV-002) or is self-declared — a self-declared inventory materially weakens Direction 1.
2. For each sampled IBS, obtain the current mapping documentation. **Record:** mapping version and date; whether AI is a recognised dependency category in the mapping schema at all.
3. **Direction 1.** For each AI system in the inventory, identify which IBSs it supports (from the inventory's own use-case field and from interview). Check the mapping of each such IBS for an explicit entry. **Record:** every AI dependency present in the inventory and absent from the relevant mapping.
4. **Direction 2.** For each sampled IBS mapping, review every technology/vendor dependency entry and determine whether it is AI-based. Where an entry is generic ("case management platform"), interview the mapping owner to establish whether that platform contains embedded AI. **Record:** every mapping entry that is AI-based but not identified as such.
5. Obtain the scenario testing library. **Record:** full list of scenario types currently in the library.
6. Test the library against the first four of the five AI-specific types named in the assurance objective: provider outage; model behavioural drift; agentic misbehaviour; correlated concentration event. Test it also for the fifth, a scenario in which an important business service is disrupted by externally originated synthetic media — a fabricated image, recording or video concerning the firm, its executives, or a market in which it operates. The scenario tests the completeness of the firm's own resilience programme; the firm's resistance to the fabrication itself lies outside FAIAS under the scope exclusion stated in TAXONOMY.md. **Record:** present / absent for each; where present, the scenario's date of last exercise; for the synthetic-media scenario, whether it is scoped to the firm's own response, communications and impact-tolerance position, not to preventing the fabrication.
7. For each AI-specific scenario that has been exercised, review the test design and results. **Record:** whether the scenario was severe *and* plausible; whether it was exercised against an actual impact tolerance; whether results were reported to a governance body; what remediation followed.
8. Cross-reference the severity/plausibility assumptions in any exercised scenario against the measured concentration assessment (IRQ-TPR-008). **Record:** whether the scenario assumed diversification that the concentration data contradicts — e.g. assuming an alternative provider exists when concentration analysis shows single-provider dependency.
9. Review the operational resilience self-assessment. **Record:** whether AI dependency is addressed; whether the self-assessment's resilience claims for the sampled IBSs are supported by the AI-specific scenario evidence found in steps 6–7.
10. Interview the op-res lead. **Record:** whether AI dependencies are treated as a distinct dependency class in the mapping methodology, or subsumed within general technology.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| AI dependencies in inventory but absent from relevant IBS mapping | Zero | Categorical per canvas fail indicator |
| Mapping entries that are AI-based but generically recorded | Reviewer judgement — no established threshold. Any material instance is reportable; the canvas treats AI subsumed within "technology" as a fail indicator | Per canvas |
| Coverage of the first four AI-specific scenario types named in the assurance objective | Provider outage, model behavioural drift and agentic misbehaviour present (the canvas's pass indicator); correlated concentration event recorded as present or absent | Reviewer judgement against the canvas's stated scenario list, whose fifth type is the next row; no external standard enumerates AI scenario types |
| Scenario of disruption by externally originated synthetic media | At least one present, scoped to the firm's own response, communications and impact-tolerance position | Per canvas independent test |
| At least one AI-specific scenario exercised in the current cycle | Required per canvas pass indicator | Per canvas; the underlying obligation to test derives from [PRA SS1/21] |
| Severity/plausibility assumptions vs measured concentration | Assumptions must be supported by measured concentration data, not assumed diversification | Reviewer judgement |

## 6. Interpretation (per CANVASES_RES.md fields 12–14)
**Pass** where: sampled IBS mapping explicitly identifies AI components as dependencies consistent with the AI inventory; the scenario library includes at least provider outage, model behavioural drift and agentic misbehaviour types, and at least one scenario in which an important business service is disrupted by externally originated synthetic media, scoped to the firm's own response, communications and impact-tolerance position; at least one AI-specific scenario has been exercised in the current review cycle with results reported to governance; and severity/plausibility assessment is informed by measured concentration rather than assumed diversification.

**Fail** where: mapping does not identify AI as a distinct dependency category and AI is subsumed generically within "technology"; the scenario library contains no AI-specific types; the scenario library holds none of the provider outage, model behavioural drift and agentic misbehaviour types, whatever other AI-specific scenarios it holds; a materially AI-dependent IBS has never had an AI-specific scenario exercised; the cross-check against the AI inventory reveals known dependencies missing from the mapping; or the scenario library holds no scenario of disruption by externally originated synthetic media, or scopes such a scenario to preventing the fabrication rather than to the firm's own response.

**Partial** where mapping is complete and the library holds a synthetic-media disruption scenario scoped as step 6 requires, but holds only one or two of the provider outage, model behavioural drift and agentic misbehaviour types (provider outage is the most commonly present type); without the synthetic-media scenario, or with none of the three types, the result is Fail. Where mapping and the scenario library meet the Pass limbs, but AI-specific scenarios have been exercised only in an earlier review cycle, or the severity/plausibility assessment assumes diversification that the measured concentration does not support (step 8), the result is Partial, and the report names the gap.

**Correlated concentration event.** This scenario type, the fourth that the assurance objective names, is recorded at step 6 as present or absent and reported in the scenario library coverage assessment (§7). It is not graded: its presence or absence does not change the Pass, Fail or Partial result. The Pass limb on measured concentration (step 8) is a separate requirement and still applies.

## 7. Evidence Outputs
- IBS mapping documents and scenario library as obtained — **L2**
- Bi-directional reconciliation matrix (inventory ↔ mapping) — **L3**
- Scenario library coverage assessment against the five AI-specific types, the fifth being the synthetic-media disruption scenario — **L3**
- Reviewer's independent assessment of exercised scenario design adequacy — **L4**
- Exercised scenario test reports and any real AI-related resilience incident — **L5**

## 8. Common Pitfalls & Limitations
- **A self-declared AI inventory poisons Direction 1.** If the inventory is incomplete, an AI dependency can be absent from both inventory and mapping and this procedure will not find it. Sequence TP-GOV-002 before TP-RES-007 wherever possible, and state the dependency in the report.
- **Direction 2 requires interviews, not just reading.** Embedded vendor AI is invisible in a mapping entry that names only the platform. The mapping owner often does not know either — cross-reference the TPR domain's embedded-AI findings.
- **"We have a scenario" is not "we exercised a scenario".** Step 6 records presence; step 7 records execution. Report both separately.
- **Scenario plausibility drift.** A provider-outage scenario written when the firm had two providers is no longer plausible-as-designed after consolidation to one. Step 8 exists for this.
- **Overlap with TP-RES-001.** RES-001 exercises the fallback for one IBS; RES-007 assesses whether the *programme* covers AI at all. Do not substitute one for the other.

## 9. Time / Effort Estimate
**3 reviewer-days**: 1 day bi-directional reconciliation across the sample, 0.5 day scenario library coverage assessment, 1 day review of exercised scenario design and concentration cross-reference, 0.5 day interviews and working papers. Add 0.25 day per IBS beyond five.

