# CANVAS: IRQ-GOV-006

## 1. IRQ ID & Title
**IRQ-GOV-006: Absent or Unmeasurable Board-Approved AI Risk Appetite**

Register question: "Has the firm articulated a board-approved risk appetite for AI, with measurable indicators, against which individual deployments are demonstrably assessed?"

## 2. Business Activities Affected
- **Every deployment decision:** without a defined appetite, individual approval decisions (IRQ-GOV-003/-004) have no reference point for what level of AI risk the firm is actually willing to accept, leaving each decision to ad hoc judgement.
- **Board and senior management oversight:** the board's statutory risk-oversight responsibility for AI cannot be discharged meaningfully if appetite is not articulated in measurable terms it can actually monitor against.
- **Customer outcome-sensitive deployments (credit, pricing, claims):** these are precisely where an unarticulated appetite is most consequential, since it is here that risk/reward trade-offs in AI adoption are sharpest.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns whether the firm has a governance reference point against which any AI system's risk profile is judged acceptable, not the system's own outputs.

## 4. Failure Mode
> The board has not articulated an AI-specific risk appetite in measurable terms, or has approved a generic/qualitative statement with no indicators that can actually be monitored, so individual deployment decisions cannot be demonstrably tested against a defined boundary of acceptable risk — approval effectively defaults to each deployment team's or committee's ad hoc judgement.

## 5. Potential Consequences
- **Customer:** Deployments proceed based on inconsistent, team-by-team risk tolerance rather than a coherent firm-wide standard, producing uneven customer protection across otherwise similar AI use cases.
- **Institution:** The board cannot demonstrate active oversight of AI risk (a core governance expectation), and cannot identify when the firm's aggregate AI risk exposure is trending toward or beyond what it is willing to bear until a materialised incident forces the question.
- **Regulator/market:** Absent, unmeasurable risk appetite is a foundational governance gap that supervisors (PRA/FCA, per DP5/22's framing of governance adequacy) would treat as evidence the board's oversight of AI is not yet operating at the standard expected for a material and growing risk category.

## 6. Failure Chain
```
Board approves a generic AI policy statement ("we will use AI responsibly") without
measurable appetite indicators
  ↓ (IRQ-GOV-006 — THIS IRQ: no defined, measurable boundary exists)
Individual deployment approvals (IRQ-GOV-003/-004) have no appetite reference point to
test against; each committee/team applies its own implicit tolerance
  ↓ (IRQ-CON-005/-006: customer access/pricing risk assessed inconsistently across
  deployments with no common appetite standard)
Aggregate AI risk exposure across the firm's growing AI estate is never measured against
a defined boundary
  ↓ (IRQ-GOV-008: no aggregate signal exists for governance bodies to act on even if
  monitoring data is technically available)
Firm exceeds its true (but never articulated) risk tolerance without anyone able to say so
  ↓
Concentration of AI-related customer harm or a systemic incident crystallises the exposure →
post-incident review finds no board-approved, measurable appetite ever existed →
governance oversight finding

Control Breakpoints:
  • IRQ-GOV-006: board-approved, measurable AI risk appetite with defined indicators
  • IRQ-GOV-004: individual deployment tiering tested against the appetite boundary
  • IRQ-GOV-008: aggregate monitoring data reported against appetite indicators to governance
  • IRQ-CON-005/-006: customer-outcome-specific appetite indicators (access, fair value)
```

## 7. Why a Domain Expert May Miss It
- Boards are accustomed to articulating risk appetite for credit, market and operational risk in quantitative terms (e.g., capital thresholds, loss limits); a governance SME reviewing board papers may see "AI risk appetite" listed as a topic covered without checking whether the statement is actually measurable or merely aspirational prose.
- Because AI risk cuts across many traditional risk categories (credit, conduct, operational, reputational), it is easy to assume it is implicitly captured within each category's existing appetite statement, without anyone drafting an AI-specific cross-cutting appetite that captures AI's distinct risk drivers (autonomy, novelty, scale of reach).
- "Responsible AI" statements and ethics principles are often mistaken for risk appetite; they express values, not measurable boundaries a deployment decision can be tested against.
- The absence of appetite is not visible from reviewing any single deployment approval — it only becomes apparent when asking "against what standard was this approved?" across multiple deployments and finding no common answer.

## 8. Assurance Objective
**AO-GOV-006:** The board shall approve an AI-specific risk appetite statement with measurable indicators, and individual deployment decisions shall be demonstrably assessed against it.

## 9. Expected Controls (Traced)
- **Board-approved AI risk appetite statement with defined, measurable indicators (e.g., maximum autonomy tier permitted without board sign-off, maximum customer-facing deployment scale without enhanced controls, tolerance thresholds for bias/error metrics)** — [PRA, SS1/23, May 2023, governance principle; FCA, "AI Update," Apr 2024, confirming board-level accountability for AI within existing SYSC governance] — Emerging Practice: no regulator has yet prescribed the specific form of an AI risk appetite statement; firms must construct one by analogy to existing quantitative risk appetite frameworks (credit, market, operational).
- **Appetite indicators reported to the board on a defined cadence, tied to aggregate monitoring data** — [linked IRQ-GOV-008; ISO/IEC 42001:2023, clause 9 (performance evaluation)] — appetite is monitored, not merely stated once.
- **Individual deployment approval papers explicitly referencing and testing against the appetite indicators** — [linked IRQ-GOV-004; MAS Information Paper ID 18/24, Dec 2024, materiality/proportionality good practice] — closes the loop between stated appetite and actual decisions.
- **EU AI Act risk-management-system alignment for in-scope high-risk systems, providing an external reference for what "acceptable risk" means for specific named use cases** — [Regulation (EU) 2024/1689, Art. 9] — supports (but does not substitute for) a firm's own board-approved appetite.
- **NIST AI RMF Govern function as structural reference for embedding risk appetite/tolerance into organisational AI governance** — [NIST AI RMF 1.0, Jan 2023, Govern function, GOVERN 1.1–1.3 on risk tolerance and policies] — provides an accepted, non-prescriptive structural framework for what a risk-tolerance articulation should cover.
- **Explicitly prohibited uses as a named appetite dimension, stated alongside the permitted-autonomy boundary** — [BIS Financial Stability Institute, Occasional Paper No 28, Annex A, Table A.3 (printed under the annex section heading "A.4 Comparison of guidance relevant to frontier AI models…", to which the body cross-refers as "Annex A.4"), printed p.23 — FSI staff's synthesis, which records that a board "sets CIRR objectives and aligns AI adoption with strategy and risk appetite, including boundaries for autonomy and prohibited uses"] — Emerging Practice: an appetite statement that defines only how much autonomy is permitted leaves the complementary question — which uses are ruled out altogether, irrespective of controls — unstated, so a deployment can be assessed against the appetite and still fall outside what the board would sanction. **Source status, stated:** the cited text is the Financial Stability Institute's own synthesis of standard-setters' guidance — the table's own source note reads "Source: FSI staff.", and the citation line inside the table's FSB column reads "FSB (2020, 2026)"; it is **not** the FSB instrument, and no expectation is attributed to the FSB on this basis. The autonomy limb of the same sentence is already covered by the first control above and is not restated.

## 10. Expected Evidence (Tagged L1–L5)
- Board minutes/papers referencing "AI risk appetite" — **L1** (reference alone is not evidence of a measurable statement).
- Board-approved AI risk appetite document with defined indicators and thresholds — **L2**.
- Sample deployment approval papers showing explicit testing against the appetite indicators (not merely a checkbox referencing the policy's existence) — **L3**.
- Board or risk committee reporting pack showing appetite indicators tracked over time against actual aggregate AI risk exposure — **L3/L5** depending on reporting maturity.
- Internal audit or board effectiveness review confirming the appetite statement is measurable and actually used in deployment decisions, not decorative — **L4**.
- Record of at least one deployment decision (approval, restriction or decline) demonstrably driven by an appetite threshold, evidencing the control functions in practice — **L5**.

## 11. Independent Test
> Obtain the board-approved AI risk appetite statement (if any) and assess whether it contains defined, measurable indicators (as distinct from qualitative/aspirational statements) using a structured rubric derived from how the firm's existing credit/market/operational risk appetite statements are constructed for comparison. For a sample of individual deployment approval decisions across risk tiers, test whether the approval paper explicitly references and tests against the appetite indicators, or whether approval reasoning is silent on appetite. Interview board/risk-committee members on their ability to describe the current level of AI risk exposure relative to appetite. Methodology follows standard board-effectiveness and risk-appetite-framework review practice (as applied to traditional risk categories), extended to the AI-specific object with no AI-specific benchmark for what a measurable AI appetite statement must contain. Conducted against board papers, approval records and interviews only. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (regulatory expectation that board-level AI accountability exists is well-established, but no published methodology or benchmark defines what a "measurable" AI risk appetite statement must contain; the rubric and adequacy judgement are bespoke to the firm and rely heavily on reviewer professional judgement, informed by comparison to the firm's own traditional risk-appetite frameworks).

## 12. Pass Indicators
- A board-approved AI risk appetite statement exists with defined, quantifiable or otherwise measurable indicators (not solely qualitative prose).
- A sample of deployment approval papers across tiers explicitly references and tests against the appetite indicators.
- Board/risk-committee reporting tracks appetite indicators over time against actual exposure.
- At least one deployment decision is evidenced as having been shaped by an appetite threshold (approval, restriction or decline).
- Interviewed board/risk-committee members can describe current AI risk exposure relative to appetite in broadly consistent terms.

## 13. Fail Indicators
- No board-approved AI risk appetite statement exists, or the only statement is a generic "responsible AI" values statement with no measurable indicators.
- Deployment approval papers make no reference to appetite; approval reasoning is silent on any appetite boundary.
- No reporting mechanism tracks aggregate AI risk exposure against appetite over time.
- Board/risk-committee members, when interviewed, cannot describe current AI risk exposure relative to any defined appetite, or give materially inconsistent answers.
- Appetite statement exists but was approved once and never revisited despite significant AI estate growth.

## 14. Reporting Language
**Pass:** "A board-approved AI risk appetite statement with defined, measurable indicators exists and is demonstrably applied: a sample of deployment approvals across tiers explicitly tests against appetite thresholds, and board reporting tracks aggregate exposure over time. At least one deployment decision is evidenced as appetite-driven. Conclusions rest on ★2 methodology — a bespoke, professional-judgement-led assessment with no published benchmark for AI risk appetite adequacy — and should be read as a reasonable but not exhaustive assurance."
**Fail:** "No board-approved AI risk appetite statement with measurable indicators was identified; the only AI-related board-level statement found is qualitative and not testable against individual deployment decisions. A sample of [n] deployment approvals made no reference to appetite in their reasoning. Board and risk-committee members interviewed gave materially inconsistent descriptions of current AI risk exposure. Individual deployment decisions cannot currently be demonstrated to be assessed against a defined, board-endorsed boundary of acceptable risk."
**Partial:** "A board-approved AI risk appetite statement exists with some measurable indicators (e.g., autonomy-tier thresholds) but lacks indicators for customer-outcome dimensions (fair access, fair pricing) linked to IRQ-CON-005/-006. The assurance objective is not yet fully met; remediation should extend the appetite statement to cover customer-outcome indicators within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (an unmeasurable appetite is a governance-foundation gap; realised severity
              depends on what inconsistent deployment decisions actually permit through)
  Likelihood: 2 (plausible while AI risk appetite frameworks remain an emerging discipline
              across the industry; less likely once a measurable statement is board-approved
              and embedded in approval papers)
  Detectability: 2 (found via a dedicated board-effectiveness or governance review; not
              visible from reviewing any single deployment approval in isolation)
  Recoverability: 1 (reversible by drafting and board-approving a measurable appetite
              statement, though decisions made during the gap period cannot be retrospectively
              re-tested)
  Novelty: 3 (a governance SME experienced with traditional risk-appetite frameworks would
              likely assume the same discipline has been applied to AI without checking; the
              AI-specific indicators themselves — autonomy tiers, novelty, scale of reach — are
              not obvious analogues of credit/market/operational appetite metrics)

Interpretation: acceptable residual risk once a measurable, board-endorsed appetite exists and
is embedded in approval papers; the material concern is that this IRQ underpins the coherence
of every individual deployment decision across the firm — without it, IRQ-GOV-003/-004
approvals proceed against no common standard.

If controls are absent or degraded:
  Severity: 3 (inconsistent deployment decisions across the firm's AI estate, with no common
              boundary, can allow aggregate risk exposure to exceed what the board would
              actually tolerate if asked directly)
  Likelihood: 3 (foreseeable and currently common across the industry — AI risk appetite
              frameworks are a genuinely emerging discipline, not yet standard practice)
  Detectability: 3 (requires a dedicated governance review to surface; invisible from routine
              deployment-level oversight)
  Recoverability: 2 (a measurable statement can be drafted and approved reasonably quickly,
              but retrospectively re-testing decisions already made against the newly defined
              appetite is a substantial undertaking)
  Novelty: 3
Residual risk: High while unmeasured; foundational to the coherence of the whole approval
framework rather than a single-deployment risk.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Absent appetite is a governance-foundation gap; realised severity is inherited from whatever inconsistent deployment decisions it permits through, rather than causing harm directly. |
| **Likelihood** | 3 | Probable given AI risk appetite frameworks are a genuinely emerging discipline across the industry, not yet standard practice comparable to credit/market/operational appetite. |
| **Detectability** | 3 | Requires a dedicated board-effectiveness or governance review to surface; invisible from reviewing any single deployment approval. |
| **Recoverability** | 2 | A measurable statement can be drafted and board-approved relatively quickly, but decisions made without it during the gap period cannot be retrospectively re-tested. |
| **Novelty** | 3 | AI-specific appetite indicators (autonomy tiers, scale of reach, novelty of failure mode) are not obvious analogues of traditional credit/market/operational appetite metrics, even to an experienced risk-governance SME. |

## 17. Regulatory Basis
> [PRA, SS1/23, May 2023] establishes governance principles requiring senior management/board oversight of model risk, extending to AI/ML per PRA's April 2024 mapping, but does not prescribe a specific AI risk appetite methodology. [FCA, "AI Update," Apr 2024] confirms board-level accountability for AI sits within existing SYSC governance requirements. [Bank of England/PRA/FCA, DP5/22, Oct 2022] explicitly raised whether existing governance frameworks — including board risk appetite processes — in fact extend meaningfully to AI, the empirical question this IRQ tests. No regulator has yet published a prescriptive AI risk appetite template; this remains a firm-constructed control area.

## 18. Research Basis
> No peer-reviewed academic literature specifically evaluates board-level AI risk appetite frameworks in financial services; this control area is governance/board-effectiveness practice rather than a research literature, consistent with this domain's evidentiary profile. [NIST AI RMF 1.0, Govern function, GOVERN 1.1–1.3] is treated as the most credible available structural reference for what a risk-tolerance articulation should contain, being a voluntary but widely referenced framework rather than empirical research.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-004 (I.2: tiering methodology — deployment tiering should be tested against
    appetite thresholds)
  - IRQ-GOV-003 (I.2: conditions of use — should reflect appetite-driven restrictions)
  - IRQ-CON-005 / IRQ-CON-006 (H.2: fair access and fair pricing — customer-outcome-specific
    appetite indicators)
  - IRQ-GOV-008 (I.3: monitoring signals to governance — reports aggregate exposure against
    appetite over time)
  - IRQ-GOV-001 (I.1: named ownership — the individual who tests deployment decisions against
    appetite must be identifiable)
```

## 20. References
```
[1] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[2] FCA, 2024. "AI Update." April 2024.
[3] Bank of England/PRA/FCA, 2022. "Artificial Intelligence and Machine Learning." Discussion
    Paper DP5/22. October 2022.
[4] NIST, 2023. "AI Risk Management Framework (AI RMF 1.0)." Govern function,
    GOVERN 1.1-1.3. January 2023.
[5] Monetary Authority of Singapore, 2024. "Information Paper: Artificial Intelligence Model
    Risk Management — Observations from a Thematic Review." ID 18/24. December 2024.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.2 (Governance domain, Approval, Tiering & Policy)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Governance SMEs may see "AI risk appetite" referenced in board
  papers and assume the same measurable discipline used for credit/market/operational risk
  has been applied, without checking whether the statement is actually testable.
✓ Test 2 (Plausible Harm): Grounded in the PRA/FCA's own DP5/22 question of whether governance
  frameworks genuinely extend to AI; without measurable appetite, individual deployment
  decisions have no common standard, risking inconsistent customer protection at scale.
✓ Test 3 (Testable): Testable via structured rubric assessment of the appetite statement,
  sampled approval-paper review and board-member interview. ★2 methodology, honestly caveated.
✓ Test 4 (Decision-Relevant): Outcome determines whether the board can demonstrate genuine
  oversight of AI risk and whether individual deployment approvals rest on a coherent,
  firm-wide standard rather than ad hoc judgement.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 9 — "explicitly prohibited uses" added as a named appetite dimension alongside the existing permitted-autonomy boundary, anchored to BIS FSI Occasional Paper No 28, Table A.3 (printed p.23) and marked SECONDARY-ONLY for what the standard-setters expect (FSI staff's synthesis, not the FSB instrument). The autonomy limb was already this field's lead example and is unchanged. ★2 unchanged.
```

---
---

