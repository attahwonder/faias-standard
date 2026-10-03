# CANVAS: IRQ-SEC-013

## 1. IRQ ID & Title
**IRQ-SEC-013: AI-as-Control Efficacy Under Adversarial Evolution**

Register question: "Where an AI system functions as a control — fraud detection, AML/transaction monitoring, surveillance, screening or promotion approval — has its detection rate and residual miss rate been measured against adversarially evolved inputs, mapped to a recognised adversarial-ML taxonomy, rather than only against historical or static case libraries; and is control efficacy re-tested on a defined cadence as adversary technique evolves?"

## 2. Business Activities Affected
- **Fraud and payments monitoring:** A model scoring transactions for fraud is validated against historical confirmed-fraud cases; adversaries who have already adapted to what the model catches are, by construction, under-represented in that evidence.
- **AML/transaction monitoring:** Typology detection tuned to known laundering patterns can show strong historical accuracy while missing structuring or layering techniques adapted specifically to evade the deployed model.
- **Surveillance and screening (market abuse, sanctions, conduct):** Behavioural-surveillance models trained on past confirmed cases face the same evidential blind spot — an adversary aware of what triggers an alert has every incentive to route around it.
- **Promotion or approval screening (financial promotions, content moderation gates):** Any AI control gating what reaches a customer or the market is subject to adversarial probing by parties seeking to get disallowed material past it.

## 3. AI Behaviour(s)
- Scores or classifies inputs against patterns learned from historical, largely static case libraries, with detection performance reported against that same historical distribution.
- Produces a stable detection threshold that, once observed or inferred by a motivated counterparty, becomes a target to be evaded rather than a fixed defence.
- Is validated and re-validated on a cadence set by internal model-risk calendars, not by evidence of how adversary technique has moved since the last test.

## 4. Failure Mode
> An AI system deployed as a detection control (fraud, AML, surveillance, screening) is validated only against historical or static case libraries, so its reported detection rate is structurally backward-looking; its real-world miss rate against adversaries who have already adapted to the control's known behaviour is high and unmeasured, and this gap is invisible in the firm's own evidence because that evidence cannot, by construction, contain cases of adaptation not yet caught.

## 5. Potential Consequences
- **Customer/market:** Fraud, laundering or market-abuse activity that has adapted to the deployed control proceeds undetected, causing direct financial loss or market-integrity harm to those the control exists to protect.
- **Institution:** A control reported internally and to the board as effective, on the strength of historical-case accuracy alone, materially understates true residual risk; when the gap surfaces — typically via a loss event or supervisory finding — the firm's own validation record becomes evidence the control's efficacy claim was never properly tested.
- **Market/regulator:** Supervisory review increasingly expects evidence that detection controls are tested against evolving, not only historical, threat behaviour; an institution unable to produce this presents an assurance picture that looks complete on paper but has not been adversarially stress-tested.

## 6. Failure Chain
```
AI-based control (fraud, AML, surveillance, screening) is deployed and
validated against a historical or static case library
  ↓ (IRQ-SEC-013 — THIS IRQ: no testing against adversarially evolved inputs
     mapped to a recognised threat taxonomy)
Adversary observes or infers what the control catches and adapts technique
  ↓ (control's reported detection rate remains high; it is measuring the
     wrong, backward-looking population)
Adapted activity passes the control undetected; miss rate is real but
unmeasured because no adversarial-evolution test set exists
  ↓ (IRQ-RES-005 / IRQ-RES-006: monitoring for decay in existing controls
     is not designed to catch technique the control was never tested against)
Harm crystallises (fraud loss, undetected laundering, market abuse,
disallowed material reaching the public) before any internal signal fires
  ↓
Discovered via loss event, external tip-off or supervisory finding, not the
firm's own control-efficacy evidence → remediation and reputational cost

Control Breakpoints:
  • IRQ-SEC-013: adversarially constructed test sets mapped to a recognised
    taxonomy, with a defined re-test cadence
  • IRQ-RES-005 / IRQ-RES-006: behavioural monitoring for drift once a
    control's efficacy has already begun to degrade
  • IRQ-GOV-008: monitoring signals, once generated, reach an accountable
    governance body with authority to trigger re-validation
```

## 7. Why a Domain Expert May Miss It
- Model validation practice for detection controls conventionally benchmarks against historical case libraries — the same evidential convention used for credit-risk and other traditional models — which is structurally incapable of containing evidence of adaptation that has not yet been caught.
- A control that reports a stable, high historical detection rate reads as evidence of effectiveness; the reviewer has no natural prompt to ask what the rate would be against inputs the adversary has not yet been observed to produce.
- Adversarial-ML testing is a security discipline, not a model-validation one, so it sits outside the toolkit of a model-risk reviewer trained on statistical accuracy and calibration, and outside the toolkit of a fraud/AML SME trained on typology libraries rather than attacker adaptation.
- The distinction between "was the control evaded via a jailbreak of the model itself" (a different failure mode, tested elsewhere) and "did the control's design account for an adversary who adapts their own behaviour to what the control catches" is easy to elide, and the second is the one most detection-control reviews never separately ask.

**Boundary note.** This IRQ is deliberately not folded into E.1 (Prompt Injection & Jailbreak): E.1 concerns attacks on the AI system's own instruction-following — a different attacker goal (defeat the model) and a different evidence base (injection-resistance rates). This IRQ concerns the AI system's efficacy *as a detection control* against adversaries who are not attacking the model at all, but adapting their own behaviour to evade what it detects — a control-efficacy question, evidenced by detection and miss-rate statistics rather than injection-resistance rates. It is also deliberately not homed in the monitoring subdomain that covers detection of control decay once it has already occurred: that subdomain tests whether decay is *detected after the fact*; this IRQ tests whether the control's design was *tested against adversarial evolution* before and after deployment — a security-testing discipline, not an operational-monitoring one. The two are cross-linked, not merged, because a control can pass this IRQ's pre-deployment test and still decay afterward, which the monitoring subdomain exists to catch.

## 8. Assurance Objective
**AO-SEC-013:** Where an AI system functions as a detection or screening control, its detection rate and residual miss rate shall be tested against adversarially evolved inputs mapped to a recognised adversarial-ML taxonomy, in addition to historical case-library testing, and re-tested on a defined cadence as adversary technique evolves.

## 9. Expected Controls (Traced)
- **Adversarial-evolution test set construction mapped to a recognised taxonomy** — [NIST AI 100-2e2025, "Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations", March 2025] — evasion-class attacks against predictive AI are catalogued and defined; test inputs constructed to represent this class, not only historical confirmed cases.
- **Technique- and case-study-informed red-team scenario design** — [MITRE ATLAS (Adversarial Threat Landscape for AI Systems), atlas.mitre.org] — 16 tactics, 84 techniques and 42 real-world case studies (as of the November 2025 release) provide a structured base against which a firm can map its own control-evasion testing, rather than constructing scenarios ad hoc.
- **Separate reporting of miss rate against adversarial-evolution test sets, not only detection rate against historical cases** — [linked IRQ-RES-005, IRQ-RES-006] — a control's headline detection-rate metric is supplemented, not replaced, by a distinct miss-rate figure against the adversarial test population.
- **Defined re-test cadence tied to observed or inferred adversary adaptation** — **Emerging Practice** — no published cross-institution benchmark fixes a re-test interval for this discipline; the cadence is the firm's own documented, risk-based judgement, reviewed rather than benchmarked.
- **Governance escalation on adversarial-evolution test findings** — [linked IRQ-GOV-008] — a material miss-rate finding against the adversarial test set reaches an accountable governance body with authority to trigger remediation or re-validation, not only the technical team that ran the test.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor or internal assertion that the control is "highly accurate" citing historical detection rate alone, with no adversarial-evolution test referenced — **L1**.
- Test design documentation showing the taxonomy used (NIST AI 100-2e2025 and/or MITRE ATLAS) to construct the adversarial-evolution test set — **L2**.
- Code/pipeline inspection confirming the adversarial-evolution test set is actually run against the deployed control, not only a development-time snapshot — **L3**.
- Test execution results: detection rate and miss rate reported separately for the historical case library and the adversarial-evolution test set — **L3**.
- Independent validation or internal audit report confirming the adversarial-evolution testing was executed as designed and findings were escalated per section 9 — **L4**.
- Production loss or incident data (where available) cross-referenced against the adversarial-evolution test findings to confirm predictive value of the test — **L5**.

## 11. Independent Test
> In an isolated non-production environment, construct a test set of adversarially evolved inputs mapped to NIST AI 100-2e2025 evasion-attack categories and, where applicable, MITRE ATLAS case-study techniques relevant to the control's domain (fraud, AML, surveillance, screening). Run the deployed control against both this adversarial-evolution test set and its existing historical case library, and report detection rate and miss rate separately for each. Measure whether the miss rate against the adversarial-evolution set is materially higher than against the historical set — the signal that historical validation has been overstating real-world efficacy. Benign, procedurally constructed test inputs only; no production data, live systems, or actual customers accessed. **No FAIAS-standard acceptance threshold exists for residual miss rate; the taxonomies structure the test, they do not set a pass/fail bar.** — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (two mature, current, actively maintained public taxonomies — NIST AI 100-2e2025 and MITRE ATLAS — exist and are directly applicable to test-set construction; no financial-services-specific quantitative benchmark or acceptance threshold exists on top of them, so the tolerance for an acceptable miss-rate uplift rests on the assessor's own risk-based judgement, not a published standard).

## 12. Pass Indicators
- Adversarial-evolution test set constructed with documented mapping to NIST AI 100-2e2025 and/or MITRE ATLAS, not an ad hoc or undocumented sample.
- Miss rate against the adversarial-evolution test set is reported separately from, and is not materially higher than, the historical-case detection rate — or, where it is materially higher, this is documented as a finding with a remediation plan rather than obscured within a blended figure.
- A defined re-test cadence exists and is evidenced as followed, tied to a documented rationale (not a bare calendar default).
- Material findings from adversarial-evolution testing are shown to have reached an accountable governance body, with a recorded response.

## 13. Fail Indicators
- No adversarial-evolution testing exists; control efficacy is evidenced solely by detection rate against a historical or static case library.
- An adversarial-evolution test set exists but is undocumented against any recognised taxonomy, making its coverage and rigour unassessable.
- Miss rate against adversarial-evolution testing is materially higher than the historical detection rate, and this gap is not disclosed, escalated, or actioned.
- No defined re-test cadence exists, or the evidenced cadence has lapsed with no documented risk-based justification.
- Adversarial-evolution testing exists but its findings are held only by the technical team that ran it, with no evidence they reached governance.

## 14. Reporting Language
**Pass:** "Detection efficacy of this AI-based control has been tested against adversarially evolved inputs mapped to NIST AI 100-2e2025 and MITRE ATLAS in addition to historical case-library testing. The miss rate against the adversarial-evolution test set is not materially higher than the historical detection rate, and a defined re-test cadence is in place. No FAIAS-standard acceptance threshold exists for residual miss rate (★2); this finding reflects that the test was performed and its result was not adverse, not that a pass/fail bar has been formally met."

**Fail:** "This AI-based control has been validated only against a historical or static case library; no testing against adversarially evolved inputs has been performed. Given that detection controls of this type are a documented target for adversary adaptation, the reported detection rate should not be relied upon as representative of real-world efficacy until adversarial-evolution testing, mapped to a recognised taxonomy, is completed."

**Partial:** "Adversarial-evolution testing has been performed and mapped to NIST AI 100-2e2025, but the resulting miss-rate uplift versus the historical case library has not been escalated to a governance body, and no re-test cadence has been defined. The assurance objective is not met until both gaps close."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (fraud, laundering, market-abuse or promotion-screening
              failure affecting customers or market integrity; regulatory
              notice risk where the control supports a regulated obligation)
  Likelihood: 2 (plausible but requires an adversary with the sophistication
              to adapt to a known control; mitigated where adversarial-
              evolution testing and re-test cadence are genuinely embedded)
  Detectability: 3 (a control passing this IRQ's testing still relies on
              behavioural monitoring — IRQ-RES-005/006 — to catch further
              decay after deployment; not real-time by this IRQ's evidence alone)
  Recoverability: 2 (reversible within weeks via re-testing and control
              retuning once a gap is identified; moderate cost)
  Novelty: 4 (the distinction between control-decay monitoring and
              pre-emptive adversarial-evolution testing is not intuitive to
              either fraud/AML SMEs or model-risk reviewers)

Interpretation: acceptable residual risk where adversarial-evolution testing
is genuinely embedded and re-tested on a defined cadence. Highest concern:
Novelty combined with the immaturity of the testing discipline itself
(★2) — this control area depends more on the assessor's own test-design
judgement than on a benchmarked pass/fail standard.

If controls are absent or degraded:
  Severity: 4 (systemic undetected fraud, laundering or market-abuse
              exposure; capital, customer and regulatory consequences)
  Likelihood: 4 (near-certain over time: adversaries adapt to any static
              control, and no test exists to catch it until a loss event does)
  Detectability: 4 (silent by construction — the control's own reported
              metrics look healthy because they measure the wrong population)
  Recoverability: 3 (requires forensic reconstruction of the exposure
              window and full re-validation once the gap is found)
  Novelty: 4
Residual risk: Critical where no adversarial-evolution testing exists for a
materially important detection control.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Fraud, laundering, market-abuse or screening failure affecting customers or market integrity; regulatory notice risk where the control supports a regulated obligation. |
| **Likelihood** | 3 | Probable over time absent this testing: static detection controls are a known adaptation target, and the taxonomy base (NIST, MITRE) shows the technique space is active and catalogued. |
| **Detectability** | 3 | The control's own historical-accuracy metrics look healthy by construction; a genuine miss-rate gap is invisible without the dedicated adversarial-evolution test this IRQ requires. |
| **Recoverability** | 2 | Reversible within weeks via re-testing and retuning once identified; moderate cost absent a crystallised loss event. |
| **Novelty** | 4 | The distinction between monitoring for decay after the fact and testing for adversarial evolution before and after deployment is unfamiliar to both fraud/AML SMEs and conventional model-risk reviewers. |

## 17. Regulatory Basis
> No regulation names adversarial-evolution testing of AI-based detection controls explicitly. [PRA SS1/23 Model Risk Management, May 2023] — ongoing monitoring and periodic validation expectations apply to detection controls built on AI/ML techniques, and this IRQ tests a specific, currently unaddressed dimension of that validation (evolving, not only historical, threat representativeness). [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] and financial-crime obligations under the Money Laundering Regulations engage where a degraded fraud or AML control causes foreseeable customer or market harm. Cited as governing expectations; no adversarial-evolution-specific rule exists.

## 18. Research Basis
> [NIST, 2025, "Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations", NIST AI 100-2e2025, March 2025] — a 400-plus-reference taxonomy distinguishing predictive-AI attacks (evasion, poisoning, privacy) from generative-AI attacks (supply chain, direct/indirect injection, misuse, agent security); the evasion-attack category is the direct anchor for this IRQ's control-evasion failure mode. [MITRE ATLAS (Adversarial Threat Landscape for AI Systems), atlas.mitre.org, accessed 2026] — 16 tactics, 84 techniques and 42 real-world case studies as of the November 2025 release, modelled on the MITRE ATT&CK framework, providing case-study grounding for test-scenario design. [FTC v. Rite Aid Corporation, E.D. Pa., Docket 2:23-cv-05023, complaint and proposed stipulated order filed 19 December 2023; stipulated order for permanent injunction and other relief signed 23 February 2024 and filed 26 February 2024] — as the Commission's complaint alleges, which Rite Aid neither admitted nor denied in consenting to the stipulated order (ECF No. 19, ¶5): an AI-based surveillance/screening control (facial-recognition matching) generating false-positive identifications acted on as ground truth, deployed without any testing of its accuracy before or after deployment, both vendors having disclaimed the technology's accuracy (complaint ¶¶50–51, 56, 74); cited as the closest documented precedent of an AI-as-control failing in a way that harmed the people it was meant to protect, illustrating why an untested residual miss rate is a live and consequential risk rather than a theoretical one. This is a facial-recognition matching failure, not a fraud/AML adversarial-evasion incident specifically, and is cited for the general principle — an AI security/screening control deployed and acted on without any measured real-world error rate — rather than as a direct adversarial-evolution precedent.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-SEC-001 (E.1: direct jailbreak — the model-instruction-attack
    boundary this IRQ is distinguished from; different attacker goal)
  - IRQ-SEC-002 (E.1: multi-turn jailbreaks — same boundary distinction)
  - IRQ-RES-005 (G.3 Monitoring & Alerting: behavioural drift/decay
    detection once a control's efficacy has already begun to degrade)
  - IRQ-RES-006 (G.3 Monitoring & Alerting: slow-decay detection
    specifically — the operational-monitoring counterpart to this IRQ's
    pre-emptive testing discipline)
  - IRQ-GOV-008 (I.3: monitoring and test-finding signals must reach an
    accountable governance body with authority to trigger remediation)
```

## 20. References
```
[1] National Institute of Standards and Technology, 2025. "Adversarial Machine
    Learning: A Taxonomy and Terminology of Attacks and Mitigations."
    NIST AI 100-2e2025. Published March 2025.
    URL: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2025.pdf
[2] MITRE, ongoing. "ATLAS — Adversarial Threat Landscape for AI Systems."
    atlas.mitre.org. 16 tactics, 84 techniques, 42 case studies as of the
    November 2025 release. Accessed 2026.
[3] Federal Trade Commission v. Rite Aid Corporation, E.D. Pa., Docket
    2:23-cv-05023. Complaint and proposed stipulated order filed
    19 December 2023; stipulated order for permanent injunction and other
    relief signed 23 February 2024 and filed 26 February 2024.
    URL: https://www.ftc.gov/legal-library/browse/cases-proceedings/2023190-rite-aid-corporation-ftc-v
[4] PRA, 2023. "SS1/23 — Model risk management principles for banks."
    May 2023.
[5] FCA, 2022. "PS22/9: A New Consumer Duty"; PRIN 2A in force 31 July 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.6 (Security domain, Control Efficacy Under Adversarial
  Evolution) — NEW subdomain
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Fraud/AML SMEs and model-risk reviewers alike
  validate detection controls against historical case libraries, which are
  structurally incapable of evidencing adaptation not yet caught; the
  adversarial-testing discipline sits outside both toolkits.
✓ Test 2 (Plausible Harm): Evidenced by two mature, actively maintained
  public taxonomies (NIST AI 100-2e2025; MITRE ATLAS) that catalogue the
  exact attack class, and by a documented precedent (FTC v. Rite Aid;
  allegations neither admitted nor denied under a stipulated order) of an
  AI-based screening control deployed and acted on without any measured
  real-world error rate.
✓ Test 3 (Testable): Testable in a non-production environment via
  adversarially constructed test sets mapped to a recognised taxonomy;
  ★2 methodology, honestly rated given the absence of a financial-services
  quantitative acceptance threshold.
✓ Test 4 (Decision-Relevant): Outcome determines whether a detection
  control's reported efficacy can be relied upon for the risk appetite it
  was approved against, and sets the re-test cadence condition of use.

Change Log:
- v1.0 (2026-08-01): Initial publication as part of the v1.0.3 batch.
  New subdomain E.6. Four tests passed.
- v1.2.1 (2026-09-19): Fields 18, 20 and 21 — erratum. The FTC v. Rite Aid
  citation gave one date, 19 December 2023, for both the complaint and the
  order; the docket shows the complaint and a proposed stipulated order
  filed on that date and the stipulated order for permanent injunction
  and other relief signed on 23 February 2024 and filed on 26 February
  2024, and both entries now say so. The Commission's case-page URL is
  added to the reference entry. Research-basis review date moved. The
  precedent's characterisation is corrected at Fields 18 and 21: the
  complaint alleges that accuracy was never tested and that both vendors
  disclaimed it, and the stipulated order records the allegations as
  neither admitted nor denied; the canvas no longer describes a real-world
  error rate diverging from a reported accuracy, and states the pleading
  grade. Its stated limits, ★2 and the risk profile are unchanged.
```

---
---

