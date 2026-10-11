# CANVAS: IRQ-HUM-002

## 1. IRQ ID & Title
**IRQ-HUM-002: Approval Theatre — Human Checkpoint Without Substantive Review**

Register question: "Do approval throughput, dwell time and rejection-rate data indicate genuine review, or does the human checkpoint function as approval theatre — and are overriders trained and safe to override?"

## 2. Business Activities Affected
- **Underwriting review:** Underwriters processing AI-recommended decisions at volumes that leave seconds per case cannot be exercising the judgement the governance paper describes.
- **Claims approval:** Claims sign-off queues under target-driven throughput pressure may become a click-through step rather than a genuine liability check.
- **AML case handling:** Case closure approvals under caseload targets may be granted without re-reading underlying evidence, particularly for AI-recommended "no further action" outcomes.

## 3. AI Behaviour(s)
- Pre-populates a recommended decision and supporting rationale into the reviewer's workflow, reducing the reviewer's default action to a single click.
- Processes cases at a throughput materially higher than the historical unaided human rate, creating implicit organisational pressure on reviewer dwell time.
- Provides no structural friction (e.g. mandatory field entry, forced justification) distinguishing a genuine override from a pass-through approval.

## 4. Failure Mode
> The human "approval" step exists procedurally (a record is created, a named individual is attributed) but functions as approval theatre: throughput, dwell time and near-zero rejection rates are statistically inconsistent with substantive review, and reviewers who do wish to override face insufficient time, training or psychological safety to do so.

## 5. Potential Consequences
- **Customer:** Decisions attributed to "human approval" that received no meaningful scrutiny; harm indistinguishable from a fully automated decision but carrying false assurance of human accountability.
- **Institution:** SM&CR exposure for the accountable senior manager if approval theatre is later demonstrated in a regulatory or FOS investigation; loss of the legal/regulatory benefit of having a human decision-maker.
- **Market/regulator:** Supervisory finding that the firm's stated human-in-the-loop control does not exist in substance, prompting wider review of all "human-approved" AI-assisted decisions.

## 6. Failure Chain
```
AI recommendation pre-populates the decision field; reviewer's default
path is a single-click accept
  ↓ (IRQ-GOV-003: approval conditions stated in policy but not
     technically enforced — no minimum dwell time, no forced
     justification)
Throughput targets set assuming AI assistance; dwell time per case
falls below the time needed for genuine review
  ↓ (IRQ-HUM-002 — THIS IRQ: approval theatre — record exists,
     substance does not)
Rejection/override rate approaches zero; no one investigates why
  ↓ (IRQ-HUM-001: automation bias compounds — even engaged reviewers
     default to acceptance)
Decision proceeds under "human-approved" label with no independent
judgement actually exercised
  ↓
Customer/regulatory harm → investigation reveals throughput data
inconsistent with claimed review → SM&CR and Consumer Duty findings

Control Breakpoints:
  • IRQ-GOV-003: technical enforcement of minimum review conditions
    (dwell time, mandatory justification fields)
  • IRQ-HUM-002: throughput/dwell-time/rejection-rate monitoring with
    defined minimum-substantive-review thresholds
  • IRQ-HUM-005: named authority and safety to override, tested against
    commercial/throughput pressure
```

## 7. Why a Domain Expert May Miss It
- Assumption: "a named approver on the record satisfies the governance requirement" — true procedurally, but the AI-specific risk is that the record's existence says nothing about its substance, which traditional operational audit rarely interrogates statistically.
- Process gap: internal audit typically samples individual case files for correctness, not the aggregate throughput/dwell-time distribution across the whole approval queue, which is where approval theatre becomes statistically visible.
- Incentive blind spot: throughput targets are frequently set by operations management without reference to the time genuinely required for AI-output review, creating an unintentional structural pressure toward theatre that no single actor designed.
- Tool misunderstanding: reviewers may not realise (or may not be told) that override carries no career or performance penalty, so psychologically safe dissent is assumed to exist but was never tested.

## 8. Assurance Objective
**AO-HUM-002:** Human approval checkpoints for AI-assisted decisions shall be demonstrated, through throughput, dwell-time and rejection-rate analysis, to constitute substantive review rather than procedural pass-through, with overriders trained, empowered and free from penalty for dissent.

## 9. Expected Controls (Traced)
- **Throughput and dwell-time monitoring against a defined minimum-review-time baseline** — [FCA, Handbook SYSC 4.1.1R — robust governance arrangements, including effective risk processes and control arrangements for information processing systems; applied here to AI-assisted decisioning] — establish and monitor a minimum time-per-case threshold below which genuine review is not plausible, calibrated against unaided baseline review times.
- **Rejection/override-rate trend analysis with investigation triggers** — [linked IRQ-HUM-001; NIST AI RMF 1.0, MANAGE-4, Jan 2023] — a rejection rate that is statistically near zero, or that drops sharply after go-live, should trigger investigation rather than be read as a quality signal.
- **Structural friction requiring active justification for approval, not just for override** — [Emerging Practice; no direct published FS-specific standard identified] — mandatory free-text or structured justification fields designed to interrupt single-click acceptance; rationale documented as emerging practice pending sector consensus.
- **Psychological-safety and non-penalty testing for overriders** — [FCA/PRA, Senior Managers & Certification Regime, individual accountability framework] — evidence that reviewers who override AI recommendations are not disadvantaged in performance management, tested via survey or anonymised override-outcome tracking.
- **EU AI Act Article 14(4) effective-oversight design requirement** — [EU AI Act, Regulation (EU) 2024/1689, Article 14(4), Aug 2024] — human overseers must be able to decide not to use the system's output, and organisational conditions must not undermine that ability (e.g. via automation bias or throughput pressure), which this canvas's controls are designed to evidence.
- **Refusal durability: a recorded refusal or material alteration cannot be reversed or routed around without an independently recorded review of equivalent or higher authority** — [EU AI Act, Regulation (EU) 2024/1689, Article 14(4), Aug 2024 — the overseer must be able to "decide not to use" the output, which an operative reversal defeats; **complements and does not duplicate IRQ-GOV-007**, which tests whether the validation function holds and exercises reject authority pre-deployment, not whether an exercised refusal survives at case level] — the workflow records each refusal or material alteration against the case, and any subsequent approval of the same case is blocked unless it carries a named reviewer of equivalent or higher authority whose review is independently recorded; re-submission under a new case identifier, a configuration change, or a second attempt to a different approver does not clear a recorded refusal.

## 10. Expected Evidence (Tagged L1–L5)
- Policy statement that "all decisions require human approval" — **L1**.
- Documented minimum-dwell-time and mandatory-justification design specification — **L2**.
- Staging/UAT walkthrough confirming the approval workflow cannot be completed without the mandatory justification field being populated — **L3**.
- Historical throughput and dwell-time distribution analysis (dev/test replay of a representative case volume) compared against the unaided baseline review time — **L3**.
- Independent audit of override-rate trend over the deployment period, with investigation of any post-go-live decline — **L4**.
- Anonymised reviewer survey or override-outcome tracking data demonstrating no career penalty attaches to overriding the AI — **L5** (where drawn from live post-deployment monitoring; L3 if simulated in staging).

## 11. Independent Test
> In a non-production environment, replay a representative sample of historical (de-identified, dev/test) case decisions through the approval workflow under the actual configured throughput targets and time allowances. Measure the distribution of dwell time per case and compare against an independently established minimum-time-for-substantive-review baseline (derived from timed unaided review of a control sample by qualified staff). Separately, analyse the trend in rejection/override rate before and after AI-assistance go-live using historical production data, flagging any statistically significant post-go-live decline. Where feasible, survey a sample of reviewers (anonymised) on perceived time pressure and psychological safety to override. **Refusal-durability limb.** In the same non-production environment, take a sample of cases in which a reviewer recorded a refusal or a material alteration, and trace each case forward through the workflow's own records to its final disposition: establish whether any was subsequently approved, released or actioned, and if so whether that approval carries a named reviewer of equivalent or higher authority whose review is independently recorded. Separately, attempt the documented routes around a recorded refusal in the test environment — re-submission to a different approver, re-submission under a new case identifier, a configuration change, the configured exception path — and record which the workflow permits without an equivalent-or-higher recorded review. This limb examines workflow configuration and records only; it alters no live decision and creates no production effect. It does not re-examine what IRQ-GOV-007 tests, which is whether the pre-deployment validation function holds and has exercised reject authority. Executed on de-identified dev/test case files and anonymised survey data; no live decisions are altered by the test. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (dwell-time/workload analysis is an established human-factors and process-engineering method with decades of aviation/process-control precedent; the specific application to AI-approval-theatre detection is FS-context-bespoke, so full ★4 standardisation is not yet reached).

## 12. Pass Indicators
- Dwell-time distribution for approved cases sits materially above the established minimum-substantive-review baseline for the large majority of cases.
- Rejection/override rate is stable or consistent with the AI system's known error profile, with no unexplained post-go-live decline.
- Mandatory justification fields are technically enforced (cannot be bypassed) and justification text is substantive (not boilerplate/copy-pasted) on audit sample.
- Reviewer survey/override-outcome data shows no measurable career penalty associated with overriding AI recommendations.
- Throughput targets are documented as calibrated against the measured minimum-review-time baseline, not set independently of it.
- Recorded refusals and material alterations hold: no sampled case was subsequently approved or actioned without an independently recorded review of equivalent or higher authority, and the workflow blocks the documented routes around a recorded refusal.

## 13. Fail Indicators
- Dwell time for a material proportion of approved cases falls below the minimum plausible review time.
- Rejection/override rate drops toward zero shortly after go-live, with no investigation on record.
- Justification fields are technically bypassable, or audit sample shows boilerplate/repeated text indicating no substantive engagement.
- Reviewer survey or informal evidence indicates overriding the AI is perceived as risky to performance ratings or throughput targets.
- Throughput targets were set without reference to any measured review-time baseline.
- A recorded refusal or material alteration was reversed, or routed around, without an independently recorded review of equivalent or higher authority — whether by re-submission to a different approver, re-submission under a new case identifier, a configuration change, or an exception path the workflow leaves open.

## 14. Reporting Language
**Pass:** "Dwell-time and rejection-rate analysis on a representative replay of historical case decisions shows the approval checkpoint functions as substantive review: dwell times sit above the established minimum-review baseline, rejection rates are consistent with the AI system's known error profile, and reviewer survey data indicates no penalty attaches to overriding the AI. This is a ★3 assessment and should be re-tested whenever throughput targets or workflow design change."

**Fail:** "Dwell-time analysis shows the majority of approved cases receive materially less time than the independently established minimum for substantive review, and rejection rates fell to near zero within weeks of go-live with no investigation. This pattern is statistically consistent with approval theatre rather than genuine human oversight; the 'human-approved' label attached to these decisions should not be relied upon for governance or regulatory purposes until remediated."

**Partial:** "Dwell-time analysis meets the substantive-review baseline for [decision type A] but not [decision type B], where throughput targets were set without reference to review-time data. Remediation should recalibrate throughput targets for [decision type B] before continued reliance on human approval as a control for that decision type."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (multiple decisions carry false assurance of human
    review; regulatory/SM&CR exposure if discovered)
  Likelihood: 2 (unlikely to persist undetected given active dwell-
    time/rejection-rate monitoring)
  Detectability: 2 (detectable within weeks via statistical monitoring;
    requires deliberate analysis, not obvious from case files alone)
  Recoverability: 3 (reversible within days-to-weeks via workflow
    redesign and re-review of affected decisions)
  Novelty: 3 (domain expert would assume sign-off equals review;
    statistical detection of approval theatre via throughput/dwell-
    time analysis is not standard banking QA practice)

Residual risk interpretation: Acceptable with active monitoring;
priority is ensuring throughput targets are recalibrated against
measured review-time baselines rather than set independently, and
that override-rate trends are actively investigated, not just logged.

If controls are absent or degraded:
  Severity: 4 (systemic reliance on a non-functioning control across
    the full decision population processed under the same throughput
    regime)
  Likelihood: 3 (probable under commercial throughput pressure absent
    active monitoring; a well-documented organisational dynamic)
  Detectability: 3 (silent until a complaint, FOS case or internal
    audit triggers forensic dwell-time analysis)
  Recoverability: 3 (multi-week remediation; potential SM&CR
    individual-accountability finding)
  Novelty: 4 (governance papers assert a human control exists with no
    statistical basis for the claim; the gap is invisible without
    today's specific test design)

Residual risk: Critical if unmonitored, given both the ease of the
statistical test and the severity of an SM&CR/regulatory finding.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 3 | Multiple decisions carry false assurance of human review; SM&CR individual-accountability and Consumer Duty exposure |
| **Likelihood** | 3 | Probable under throughput pressure if dwell-time/rejection-rate monitoring is absent; well-documented organisational dynamic, not a rare edge case |
| **Detectability** | 2 | Detectable within weeks via statistical monitoring but requires deliberate analysis design; not visible from individual case review |
| **Recoverability** | 3 | Reversible within days-to-weeks via workflow redesign and case re-review; moderate cost |
| **Novelty** | 3 | Domain expert assumes sign-off equals review; statistical detection of approval theatre is outside standard banking QA methodology |

## 17. Regulatory Basis
> [EU AI Act, Regulation (EU) 2024/1689, Article 14(4), Aug 2024] requires that human overseers be genuinely able to decide not to use system output, which organisational conditions such as throughput pressure can structurally undermine. [FCA, Handbook SYSC 4.1.1R] requires robust governance arrangements — effective processes to identify, manage, monitor and report risks, and control arrangements for information processing systems — applied here to AI-assisted decisioning. [FCA/PRA Senior Managers & Certification Regime] creates individual accountability for the senior manager responsible; approval-theatre findings would materially undermine a defence that adequate human oversight existed. Section pinpoints [UNVERIFIED — cited modules (SYSC 4, SYSC 9, SYSC 15A, PRA SS1/21/PS21/3, EU AI Act Art. 14 — SYSC 19D removed 25 Aug 2026: it is the dual-regulated firms Remuneration Code and was mis-cited; SYSC 4.1.1R substituted, verified from the Handbook) confirmed extant on FCA Handbook/BoE/eur-lex; no AI-specific sub-clause pinpoint published by the regulator to cite beyond module level] (verified 29 Jul 2026).

## 18. Research Basis
> [Parasuraman & Riley, 1997, "Humans and Automation: Use, Misuse, Disuse, Abuse", Human Factors, 39(2)] frames complacency under workload pressure as a distinct failure mode from automation bias proper. [Cummings, M.L., 2004, "Automation bias in intelligent time critical decision support systems", AIAA 1st Intelligent Systems Technical Conference] documents how time pressure specifically compresses genuine review in automated decision-support contexts, directly informing the dwell-time methodology used here. [Bainbridge, L., 1983, "Ironies of Automation", Automatica, 19(6)] is the foundational account of how automating a task erodes the human operator's ability to perform effective oversight of it, a mechanism this IRQ's failure mode instantiates. [Santoni de Sio, F. & van den Hoven, J., 2018, "Meaningful Human Control over Autonomous Systems: A Philosophical Account", *Frontiers in Robotics and AI* 5:15, DOI 10.3389/frobt.2018.00015] supplies the **tracking** condition this limb tests — that "a decision-making system should demonstrably and verifiably be responsive to the human moral reasons relevant in the circumstances" — and the **tracing** condition, in the paper's own terms: the system's actions and states should "be traceable to a proper moral understanding on the part of one or more relevant human persons who design or interact with the system" — a person who understands, or is in a position to understand, both "the capabilities of the system and the possible effects in the world" of its use and "that others may have legitimate moral reactions toward them because of how the system affects the world". The second limb is the human's own answerability, not a general awareness of consequences, and it is the limb an operatively reversible refusal offends: the reviewer remains the person others hold answerable for a decision the workflow allowed another actor to undo. A reviewer's refusal that is operatively reversible is also not tracking the reviewer's reasons, whatever the record shows. **Scope of the borrowing, stated:** the paper is a philosophical account of control, not an account of institutional authority. The word "authority" occurs in it twice, and only once in the body text — of "the public authority" that defines the rules of traffic, a regulator rather than a holder of decision power; the second occurrence is the title of a cited work in the reference list. It is cited for the tracking and tracing conditions only, and no claim about authority design rests on it.
>
> **[FAIAS Incident Register, row 70, "Drivers v. Uber, Amsterdam Court of Appeal", 2023]** — the Amsterdam Court of Appeal held, of Uber's evidence that a person reviewed automated fraud-flag deactivations, that the documents "do not at all show that the action was much more than a purely symbolic act" (para 3.24; translation from the Dutch): one to three Risk-team staff had made a note, the three drivers concerned were not heard, Uber had not made clear the qualifications and level of knowledge of the staff, and Uber could give no examples or concrete numbers of cases in which a driver, after a first warning and a temporary block, spoke with the Risk team and a decision on deactivation then followed. For a fourth driver, who had a personal conversation before deactivation, the court found real human intervention shown (para 3.25). Uber is not a financial-services firm; the decision type, account deactivation on an automated fraud flag, is one that banks also make.
>
> **[FAIAS Incident Register, row 71, "Kisting-Leung v. Cigna", 2024]** — a class action pleads that an insurer's algorithm let physicians sign off claim denials in batches: that over two months in 2022 its doctors denied over 300,000 requests for payments by this method, spending an average of just 1.2 seconds on each (para 3), and signed off "without opening each patient's files" (ECF page 8). Each denial carried a physician's sign-off, while the pleaded throughput leaves no time for substantive review. Carried as a secondary row: a pleading, not a judgment, and the 300,000 and 1.2-second figures rest on a press report that the complaint cites.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-HUM-001 (D.1 Automation Bias: acceptance-without-challenge,
    complementary to throughput/dwell-time measurement here)
  - IRQ-GOV-003 (I.2 Approval, Tiering & Policy: technical enforcement
    of minimum review conditions)
  - IRQ-HUM-005 (D.3 Escalation & Override Design: named, empowered
    suspension authority tested against commercial pressure)
  - IRQ-CON-004 (H.2 Customer Outcomes: downstream accuracy of
    customer-facing content approved under this checkpoint)
```

## 20. References
```
[1] Parasuraman, R. & Riley, V., 1997. "Humans and Automation: Use, Misuse, Disuse, Abuse." Human Factors, 39(2), 230–253.
    Accessed: 2026-07-29

[2] Cummings, M.L., 2004. "Automation bias in intelligent time critical decision support systems." AIAA 1st Intelligent Systems Technical Conference.
    Accessed: 2026-07-29

[3] Bainbridge, L., 1983. "Ironies of Automation." Automatica, 19(6), 775–779.
    Accessed: 2026-07-29

[4] European Union, 2024. "Regulation (EU) 2024/1689 (AI Act), Article 14: Human Oversight."
    Published: 2024-07-12
    URL: https://eur-lex.europa.eu/eli/reg/2024/1689/oj

[5] Financial Conduct Authority. "Handbook SYSC 4: General organisational requirements."
    Accessed: 2026-08-26
    URL: https://www.handbook.fca.org.uk/handbook/SYSC/4/
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** D.1 (Human Oversight, Automation Bias)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): SMEs treat a named approver on the record as sufficient evidence of a working control; approval-theatre risk is invisible without throughput/dwell-time statistical analysis.
✓ Test 2 (Plausible Harm): Grounded in Bainbridge (1983), Parasuraman & Riley (1997) and Cummings (2004) on workload-driven erosion of human oversight quality.
✓ Test 3 (Testable): Answerable via dwell-time/rejection-rate replay analysis and reviewer survey; measurable, reproducible.
✓ Test 4 (Decision-Relevant): Determines whether the firm can rely on "human approval" as a governance control, directly gating whether remediation of throughput targets or workflow design is required.

**Change Log:**
- v1.0 (2026-07): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 9 — a refusal-durability control breakpoint added, anchored to EU AI Act, Regulation (EU) 2024/1689, Article 14(4), with its non-duplication of IRQ-GOV-007 stated on its face: a recorded refusal or material alteration cannot be reversed or routed around without an independently recorded review of equivalent or higher authority. Field 11 — a matching refusal-durability limb added to the independent test (sampled refusals traced through the workflow's own records to final disposition; the documented routes around a recorded refusal attempted in the test environment), examining workflow configuration and records only, altering no live decision, and expressly not re-examining what IRQ-GOV-007 tests. Fields 12 and 13 — one Pass and one Fail indicator added for that limb. Field 18 — Santoni de Sio & van den Hoven (2018, *Frontiers in Robotics and AI* 5:15, DOI 10.3389/frobt.2018.00015) added for the tracking and tracing conditions, with the scope of the borrowing stated: the paper is a philosophical account of control, not of institutional authority, and no claim about authority design rests on it. ★3 unchanged.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citations added in the reserved form (row 70, Drivers v. Uber, Amsterdam Court of Appeal, a decision type that banks also make; row 71, Kisting-Leung v. Cigna, carried as a secondary row: a pleading and not a judgment). Research-basis review date moved. No change to controls, test, ★3 or risk profile.
- v1.3.3 (2026-10-09): Fields 15 and 16 — Recoverability scored 3 in place of 2 (Field 16, and the controls-in-place case in Field 15). The canvas states recovery within days-to-weeks, which is beyond the within-hours level that ASSURANCE_MODEL.md §7 scores 2; the scale names no band between days and years, and 3 (reversible within days) is the nearest anchor. The other axes, the ★ rating and the research basis are unchanged.
```

---
---

