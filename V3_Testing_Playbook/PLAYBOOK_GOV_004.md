# TP-GOV-004 — Independent Tiering Re-Score

## 1. Procedure Identity
**Procedure ID:** TP-GOV-004
**IRQ:** IRQ-GOV-004 — Tiering Methodology Fails to Capture Generative and Agentic Risk Drivers
**Assurance objective:** AO-GOV-004 — The firm's risk-based tiering methodology shall explicitly and demonstrably weight generative and agentic risk drivers — autonomy, tool access and irreversible-action capability, and customer proximity — such that control depth is proportionate to the deployment's actual risk profile, not only its underlying model type.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established control-adequacy review methodology, strengthened by cross-referencing the published EU AI Act risk-tier structure as an external reference; no single canonical AI tiering methodology exists, so the independently-derived tier itself involves professional judgement.
**Method classification:** Adapted Industry Practice — control-design-adequacy review (criteria walkthrough, independent re-scoring, benchmark cross-reference).

## 2. Preconditions
**Environment:** Governance records only. No production system access required.
**Access required:** Read access to the firm's tiering methodology and criteria; tiering decisions and their supporting rationale for sampled systems; the control set actually applied per tier; system design documentation sufficient to assess autonomy, tool permissions and customer proximity independently.
**Artefacts required:** Tiering methodology document; per-system tiering decisions with scoring detail; control-depth definitions per tier; system architecture and tool-permission documentation; re-tiering trigger definition and any re-tiering events; EU AI Act Annex III classification logic as the external reference point.
**Personnel required:** Model risk or governance function owning the methodology; system owners for the sampled systems (to confirm actual autonomy and tool access, which documentation often understates); reviewer.
**Data handling:** Governance records only; no customer data.

## 3. Test Design
The reviewer independently re-scores each sampled system against the firm's own stated tiering criteria, and separately assesses whether three specific drivers were captured at all: autonomy level, tool/action permissions including irreversibility, and customer proximity. The independently derived tier is then compared with the tier actually assigned and — crucially — with the control depth actually applied, since a correct tier with the wrong controls attached fails the objective just as surely.

The sample must span three system classes, because the failure mode is class-specific: static predictive models (usually tiered adequately, since traditional model risk covers them), generative non-agentic assistants, and agentic systems with tool access (usually under-tiered). Minimum two systems per class (reviewer-set design minimum, disclosed at scoping).

EU AI Act Annex III classification is used as an external cross-reference — not as the firm's obligation, but as an independently published risk-tier structure against which the firm's tier can be sanity-checked. Where the firm tiers low a system that Annex III logic would place in a high-risk category, that divergence is reportable regardless of whether the Act applies to the firm.

Order matters: derive the independent tier *before* reading the firm's assigned tier.

## 4. Steps
1. Obtain the tiering methodology and extract the scored criteria. **Record:** the criteria list; specifically whether autonomy, tool/action permissions (including irreversibility) and customer proximity appear as scored criteria, are implicit, or are absent.
2. Draw and record the sample across the three system classes. **Record:** basis, class distribution.
3. For each sampled system, gather the evidence needed to score independently — architecture documentation, tool permission grants, user population, decision materiality — **without** viewing the assigned tier. **Record:** the evidence gathered and confirmation the assigned tier was not consulted.
4. Interview the system owner on actual autonomy and tool access. **Record:** what the system can actually do, as against what documentation states; discrepancies are themselves findings.
5. Independently score each system against the firm's own criteria. **Record:** the reviewer's score per criterion and derived tier.
6. Separately assess each system against the three specific drivers, noting where the firm's criteria provide no way to capture them. **Record:** driver-by-driver assessment.
7. Cross-reference each system against EU AI Act Annex III classification logic. **Record:** the Annex III analogue category, if any, and whether the firm's tier is proportionate to it.
8. **Now** obtain the assigned tier and its rationale. Compare. **Record:** agreement / firm higher / firm lower; and for every divergence, the specific criterion driving it.
9. Compare the control depth actually applied against the control depth the firm's own methodology prescribes for the assigned tier. **Record:** any system where the prescribed controls were not applied.
10. Review the re-tiering trigger. **Record:** whether one exists; whether it has ever been exercised; specifically whether any system underwent a material tool or autonomy change without re-tiering.
11. Review the tiering decision process. **Record:** whether tiers are self-assigned by the deployment team or independently challenged.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Autonomy, tool permissions and customer proximity present as scored criteria | All three present and explicit | Categorical per canvas pass indicator |
| Independent re-score agrees with assigned tier | Consistent across the sample, with no systematic under-tiering of agentic or customer-facing systems; an isolated divergence outside any pattern is a judged finding, not a Fail | Categorical per canvas pass indicator |
| Proportionality to EU AI Act Annex III analogue | Reviewer judgement — no established threshold; the Annex III structure is a cross-reference, not a mandated mapping | Per canvas; external reference point only |
| Re-tiering trigger exists and has been exercised | ≥1 exercise following a material tool/autonomy change | Categorical per canvas pass indicator |
| Independent challenge to tiering decisions | Present; self-assignment alone is L1/L2 evidence and a fail indicator | Categorical per canvas |
| Correct tier derivation itself | Reviewer judgement — no established threshold. No canonical AI tiering methodology exists; the independently derived tier is professional judgement and must be labelled so | Explicitly bespoke |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: the methodology explicitly includes autonomy, tool/action permissions and customer proximity as scored criteria; independent re-scoring produces tiers consistent with those assigned with no systematic under-tiering of agentic or customer-facing systems, an isolated divergence outside any pattern being a judged finding rather than a Fail; agentic/customer-facing systems are tiered proportionately to their Annex III analogue where applicable; a re-tiering trigger exists and has been exercised; and tiering decisions are independently challenged.

**Fail** where: criteria weight only data sensitivity and decision materiality with autonomy, tool access and customer proximity absent or implicit; re-scoring finds systematic under-tiering of agentic systems; no re-tiering trigger exists and tiers are set once and never revisited despite subsequent tool/autonomy expansion; tiering is self-assigned with no independent challenge; or a customer-facing high-volume but individually low-materiality system is tiered low purely on materiality grounds, missing customer-proximity risk.

**Partial** where the criteria are adequate but the re-tiering trigger has never operated, or where tiers are correct but the prescribed control depth was not applied.

## 7. Evidence Outputs
- Tiering methodology and per-system decisions as obtained — **L2**
- Independent re-scoring working paper, with the confirmation that assigned tiers were not consulted first — **L3**
- Driver-by-driver assessment and Annex III cross-reference — **L3**
- Tier comparison matrix with divergence analysis — **L4**
- Records of real re-tiering events following capability change — **L5**

## 8. Common Pitfalls & Limitations
- **Reading the assigned tier first.** Anchoring destroys the independence of the re-score. Step 3's confirmation exists to make the ordering evidenced.
- **Documentation understating actual autonomy.** Step 4's interview routinely finds that a system described as "advisory" auto-executes a class of low-value actions.
- **Treating Annex III as an obligation.** It is used here as an external reference structure. Whether the Act applies is TP-GOV-011's question.
- **Ignoring control depth.** A correct tier with the wrong control set attached is still a failure of the objective.
- **The low-materiality high-volume trap.** The canvas names this explicitly: a broad-reach chat interface tiered low on per-interaction materiality. Test for it deliberately.

## 9. Time / Effort Estimate
**3 reviewer-days**: 0.5 day methodology review and sampling, 1 day independent re-scoring across the sample, 0.5 day owner interviews, 0.5 day Annex III cross-reference, 0.5 day comparison and working papers.

---
---

