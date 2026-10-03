# CANVAS: IRQ-HUM-003

## 1. IRQ ID & Title
**IRQ-HUM-003: Skill Atrophy Undermining Fallback Capability**

Register question: "Can staff still perform the critical task to standard without the AI, and is AI-free competency periodically assessed rather than assumed?"

## 2. Business Activities Affected
- **Underwriting review:** Underwriters who have relied on AI-generated affordability summaries for an extended period may lose the practised skill of independently assessing raw financial evidence when the AI is unavailable or under investigation.
- **Claims approval:** Claims handlers accustomed to AI-drafted liability assessments may be unable to construct an assessment from first principles during an outage or a period of AI suspension.
- **AML case handling:** Investigators who habitually rely on AI-generated typology summaries may lose facility with manual evidence synthesis, degrading the quality of the fallback process the firm's operational resilience plan depends on.

## 3. AI Behaviour(s)
- Performs the cognitively demanding synthesis step of a task (drafting the assessment, summarising evidence, proposing the recommendation) that staff previously performed themselves.
- Is available continuously in normal operation, such that staff have limited routine occasion to exercise the unaided version of the skill.
- Provides no built-in mechanism distinguishing staff who could still perform the task unaided from those who could not.

## 4. Failure Mode
> Staff competency to perform the critical task to standard without AI assistance has silently degraded through disuse, and this degradation is unmeasured and unknown to the organisation until an AI outage, suspension or investigation forces reliance on the fallback — at which point the fallback itself proves substandard.

## 5. Potential Consequences
- **Customer:** During an AI outage or suspension, decisions made via the "fallback" process are of materially lower quality than assumed, because the staff executing it are no longer genuinely competent at the unaided task.
- **Institution:** Operational resilience plans that assume a competent manual fallback are invalidated in practice; regulatory finding that the firm's continuity plan for a critical AI-supported service was not actually resourced with capable staff.
- **Regulator/market:** FCA/PRA operational resilience supervisory action if an important business service cannot be delivered within impact tolerance during an AI unavailability event, specifically because the human fallback was assumed rather than tested.

## 6. Failure Chain
```
AI performs the cognitively demanding synthesis step continuously in
normal operation
  ↓ (IRQ-RES-001: fallback mode is documented on paper but not
     exercised in practice)
Staff exercise the unaided skill rarely or never; competency degrades
through disuse, unmeasured
  ↓ (IRQ-HUM-003 — THIS IRQ: skill atrophy — AI-free competency
     assumed, not periodically assessed)
AI unavailability, suspension (IRQ-HUM-005) or investigation forces
reliance on the "fallback" staff
  ↓
Fallback process executes at substandard quality because the staff are
no longer genuinely competent unaided
  ↓
Important business service breaches its impact tolerance during the
AI-unavailability event → customer harm → operational resilience
supervisory finding

Control Breakpoints:
  • IRQ-HUM-003: periodic, genuinely AI-free competency assessment,
    not assumed retention of skill
  • IRQ-RES-001: fallback mode actually exercised (fire-drilled), not
    merely documented
  • IRQ-GOV-006: risk appetite for how long AI-assisted staff can
    operate before mandatory unaided refresher assessment
```

## 7. Why a Domain Expert May Miss It
- Assumption: "staff were trained on the manual process before AI was introduced, so the skill still exists" — false over time; skill decay through disuse is a well-established finding in human-factors and expertise research, distinct from initial training adequacy.
- Traditional operational-resilience fallback testing (per SYSC 15A / PS21/3) typically verifies that a documented alternative process exists and can technically be invoked; it rarely tests whether the staff executing that process retain genuine unaided competency, which is a subtler and AI-specific manifestation of the same requirement.
- Process gap: staff performance reviews assess output quality with AI assistance available, so declining unaided competency is invisible in normal-course quality metrics.
- Tool misunderstanding: management may believe "we still have the manual SOP documented" is equivalent to "our staff can still execute it to standard," conflating documentation currency with human capability currency.

## 8. Assurance Objective
**AO-HUM-003:** The organisation shall periodically and genuinely assess staff competency to perform each AI-supported critical task without AI assistance, and shall not assume retained competency based on prior training or documented procedures alone.

## 9. Expected Controls (Traced)
- **Periodic AI-free competency assessment** — [FCA, Handbook SYSC 15A.2.9R, per PS21/3, 2021; PRA SS1/21, Mar 2021] — scheduled assessment of staff performing the critical task entirely without AI assistance, scored against the same quality standard as the AI-assisted process.
- **Fallback mode fire-drilling, not documentation-only testing** — [linked IRQ-RES-001; PRA SS1/21, section on scenario testing] — the documented fallback process is periodically actually exercised end-to-end by the staff who would perform it in a real event.
- **Skill-decay-informed refresher training cadence** — [Arthur, Bennett, Stanush & McNelly, 1998, "Factors that Influence Skill Decay and Retention: A Quantitative Review and Analysis", Human Performance, 11(1)] — refresher training cadence calibrated to task-specific skill-decay rates rather than a generic annual schedule.
- **Risk-appetite threshold for maximum AI-assisted tenure before mandatory unaided reassessment** — [linked IRQ-GOV-006; Emerging Practice, no direct FS-specific published standard identified for AI-driven skill atrophy specifically] — board-approved threshold triggering reassessment, documented as emerging practice pending sector-specific research maturation.
- **Fallback capacity mapped to important business service impact tolerance** — [FCA, PS21/3, Operational Resilience, Mar 2021] — sufficient competent unaided staff capacity is available to deliver the important business service within its stated impact tolerance during an AI-unavailability event.

## 10. Expected Evidence (Tagged L1–L5)
- HR/L&D assertion that "staff are trained on the manual process" — **L1**.
- Documented refresher training schedule and fallback SOP — **L2**.
- Design specification for the AI-free competency assessment (task set, scoring rubric, pass threshold) — **L2**.
- Staging assessment results: a sample of staff completing the critical task entirely unaided, scored against the quality standard, in a controlled dev/test exercise — **L3**.
- Independent audit of fallback fire-drill execution (an actual, scheduled exercise of the AI-free process under time pressure) — **L4**.
- Historical competency-assessment trend data across multiple assessment cycles, showing whether unaided performance is stable, declining or improving — **L5**.

## 11. Independent Test
> In a non-production setting, select a representative sample of staff who perform the critical task with routine AI assistance. Assign each a set of realistic dev/test cases (underwriting files, claims, AML alerts) to complete entirely without AI assistance, under time constraints comparable to normal operating conditions. Score outputs against the same quality rubric used for AI-assisted output quality assurance. Compare results against (a) a defined minimum competency threshold and (b) where available, the same staff members' scores from a prior AI-free assessment cycle, to detect a decay trend rather than a single point-in-time snapshot. Executed on de-identified dev/test cases; no live decisions are affected. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (AI-free competency assessment is a direct application of established occupational skill-retention and training-evaluation methodology — Arthur et al.'s 1998 meta-analytic framework — to a new domain; the framework itself is well-established, though its specific calibration to AI-assisted FS roles has no agreed FS benchmark yet).

## 12. Pass Indicators
- Sampled staff meet or exceed the minimum unaided competency threshold on the dev/test case set.
- No statistically significant downward trend in unaided competency across successive assessment cycles.
- Fallback fire-drill is scheduled, actually executed (not merely documented), and delivers the important business service within its stated impact tolerance.
- Refresher training cadence is calibrated against measured skill-decay data for the specific task, not a generic schedule.
- A board-approved threshold exists for maximum AI-assisted tenure before mandatory reassessment, and staff are tracked against it.

## 13. Fail Indicators
- Sampled staff fall materially below the minimum unaided competency threshold.
- A clear downward trend in unaided competency is observed across assessment cycles with no corrective action taken.
- The fallback process has never been fire-drilled; only its documentation has been reviewed.
- No AI-free competency assessment has ever been conducted; competency is assumed from historical (pre-AI) training records.
- Staff self-report low confidence in performing the task unaided, with no organisational response.

## 14. Reporting Language
**Pass:** "AI-free competency assessment on a representative staff sample, using dev/test case files, shows unaided performance meets the defined quality threshold with no downward trend across assessment cycles. The fallback process has been fire-drilled and delivers the important business service within its impact tolerance. This is a ★3 assessment and should be repeated on the defined refresher cadence, not treated as a one-off validation."

**Fail:** "AI-free competency assessment shows sampled staff fall materially below the quality threshold when performing the critical task without AI assistance, and no such assessment had previously been conducted — competency was assumed based on historical training records that predate several years of AI-assisted operation. The documented fallback process cannot currently be relied upon to deliver the important business service within impact tolerance during an AI-unavailability event."

**Partial:** "AI-free competency assessment meets threshold for staff who joined before AI-assisted tooling was introduced, but not for staff who have only ever worked with AI assistance. The fallback capability is unevenly distributed across the team; remediation should target unaided-skill training specifically for newer staff before relying on team-wide fallback capacity."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (single-team/service disruption if fallback underperforms
    during an AI-unavailability event; not customer-facing unless the
    outage coincides with unavailability)
  Likelihood: 2 (unlikely to be exposed if periodic AI-free assessment
    and fire-drilling are active; requires an actual unavailability
    event to surface)
  Detectability: 3 (only becomes visible during an actual outage/
    suspension event or a deliberate assessment — not observable in
    normal-course operation)
  Recoverability: 2 (reversible via targeted refresher training once
    identified; days-to-weeks)
  Novelty: 3 (domain expert would assume fallback SOPs are sufficient;
    the AI-specific skill-decay-through-disuse mechanism is not
    standard operational-resilience testing practice)

Residual risk interpretation: Acceptable with active periodic testing;
the key risk driver is Detectability — this gap is invisible until an
actual AI-unavailability event, which is exactly when it matters most,
making proactive assessment disproportionately valuable relative to
its cost.

If controls are absent or degraded:
  Severity: 3 (important business service delivered below standard
    during an AI-unavailability event; multiple customers/cases
    affected)
  Likelihood: 3 (probable given known skill-decay dynamics if no
    periodic unaided practice or assessment occurs)
  Detectability: 4 (essentially undetectable until an actual
    unavailability event forces reliance on the degraded fallback)
  Recoverability: 3 (multi-week remediation; potential breach of
    stated impact tolerance requiring regulatory notification)
  Novelty: 4 (operational resilience plans assert fallback capability
    with no AI-specific competency evidence; the gap is invisible
    without today's specific unaided assessment)

Residual risk: High. Should be prioritised given the low cost of
periodic testing relative to the operational-resilience exposure if
untested.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Single important-business-service disruption if fallback underperforms; escalates to 3 only if coincident with a genuine AI-unavailability event |
| **Likelihood** | 2 | Unlikely to be exposed with active periodic assessment; skill decay is well-documented but its business impact depends on an unavailability event occurring |
| **Detectability** | 3 | Not observable in normal-course operation; only surfaces during an actual outage/suspension or a deliberate unaided assessment |
| **Recoverability** | 2 | Reversible via targeted refresher training once identified, typically within weeks |
| **Novelty** | 3 | Domain expert assumes documented fallback SOPs are sufficient; the disuse-driven skill-decay mechanism specific to continuous AI assistance is not standard operational-resilience testing practice |

## 17. Regulatory Basis
> [FCA, Handbook SYSC 15A.2.1R, 15A.2.5R and 15A.2.9R, per PS21/3, Mar 2021] and [PRA, SS1/21, "Operational Resilience: Impact Tolerances for Important Business Services", Mar 2021] require firms to identify important business services, set impact tolerances, and demonstrate they can remain within tolerance during severe-but-plausible disruption — which extends to AI-component unavailability and the human fallback's genuine capability to deliver the service. [FCA, PS21/3, Mar 2021] requires scenario testing of these fallback arrangements. Section pinpoints on AI-specific application [UNVERIFIED — SYSC 15A, SS1/21 and PS21/3 confirmed extant and in force; no AI-component-specific sub-clause published by FCA/PRA to cite beyond general IBS/impact-tolerance module reference] (verified 29 Jul 2026).

## 18. Research Basis
> [Arthur, W., Bennett, W., Stanush, P.L. & McNelly, T.L., 1998, "Factors that Influence Skill Decay and Retention: A Quantitative Review and Analysis", Human Performance, 11(1), 57–101] provides the meta-analytic basis for skill-decay rates and refresher-training calibration used in this canvas's controls. [Bainbridge, L., 1983, "Ironies of Automation", Automatica, 19(6)] is the originating account of automation degrading the operator's own capability to intervene effectively — the mechanism this IRQ addresses at the organisational-competency level rather than the single-decision level addressed by IRQ-HUM-001/002.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-RES-001 (G.1 Fallback & Degradation: fallback mode must be
    documented, resourced and exercised — this IRQ tests whether the
    "resourced" element genuinely holds)
  - IRQ-HUM-001 (D.1 Automation Bias: related disuse-driven human-
    factors mechanism, applied to review rather than performance)
  - IRQ-GOV-006 (I.2 Approval, Tiering & Policy: board-approved risk
    appetite threshold for AI-assisted tenure before reassessment)
```

## 20. References
```
[1] Arthur, W., Bennett, W., Stanush, P.L. & McNelly, T.L., 1998. "Factors that Influence Skill Decay and Retention: A Quantitative Review and Analysis." Human Performance, 11(1), 57–101.
    Accessed: 2026-07-29

[2] Bainbridge, L., 1983. "Ironies of Automation." Automatica, 19(6), 775–779.
    Accessed: 2026-07-29

[3] Financial Conduct Authority, 2021. "Handbook SYSC 15A: Operational resilience."
    Published: 2021-03-29
    URL: https://www.handbook.fca.org.uk/handbook/SYSC/15A/

[4] Prudential Regulation Authority, 2021. "Supervisory Statement SS1/21: Operational Resilience: Impact Tolerances for Important Business Services."
    Published: 2021-03-29
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/operational-resilience-impact-tolerances-for-important-business-services-ss
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.2 (Human Oversight, Skill Atrophy)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs assume documented fallback SOPs and historical training records equate to current unaided capability; disuse-driven skill decay is invisible in normal-course quality metrics.
✓ Test 2 (Plausible Harm): Grounded in Arthur et al.'s (1998) established skill-decay research and Bainbridge's (1983) "Ironies of Automation".
✓ Test 3 (Testable): Answerable via a controlled AI-free competency assessment against a defined quality rubric, repeatable across cycles.
✓ Test 4 (Decision-Relevant): Directly informs whether the firm's operational resilience fallback claim is credible, gating whether refresher training or fire-drilling investment is required.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

