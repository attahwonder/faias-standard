# CANVAS: IRQ-MOD-004

## 1. IRQ ID & Title
**IRQ-MOD-004: Unmeasured Hallucination Rate Against Task-Representative FS Tolerance**

Register question: "Has the frequency and severity of hallucinated facts, figures or citations been measured on tasks representative of the intended FS use, with documented tolerance thresholds?"

## 2. Business Activities Affected
- **Customer-facing advice/servicing chatbot:** Generates responses citing product terms, fees or rights; a fabricated figure or rule is presented with the same fluency as an accurate one.
- **AML SAR drafting assistant:** Synthesises investigation narratives from case data; fabricated transaction details or entity relationships can misdirect the investigation or, if unchecked, enter the regulatory filing itself.
- **Claims summarisation:** Summarises medical reports, correspondence and policy wording; a fabricated detail (an invented diagnosis, an incorrect policy exclusion) can drive a wrong liability or settlement decision.

## 3. AI Behaviour(s)
- Generates fluent natural-language output, including facts, figures and citations, as a by-product of next-token prediction rather than verified retrieval.
- Produces confabulated content indistinguishably from correct content in tone and structure.
- Hallucination rate varies materially by task type, prompt structure and domain — a rate measured on a generic benchmark does not transfer to the firm's specific FS task.

## 4. Failure Mode
> The system fabricates facts, figures or citations at a rate and severity that has not been measured on tasks representative of the firm's actual FS use case, so no evidenced tolerance threshold exists against which "acceptable" hallucination risk can be judged before deployment.

## 5. Potential Consequences
- **Customer:** Reliance on fabricated product terms, claim facts or AML case details leading to wrong decisions, mis-sold products, or unjust treatment.
- **Institution:** No defensible basis for having approved the system's deployment, since risk tolerance was never quantified against the actual use case; FOS/regulatory findings of unsupported decisions (cf. Air Canada, CNET, Mata v. Avianca incidents).
- **Regulator/market:** Evidence that the firm approved a generative system for customer-facing or regulatory-facing use without measuring its core failure mode — an SS1/23 and Consumer Duty gap.

## 6. Failure Chain
```
Model generates output without task-representative hallucination measurement
  ↓ (IRQ-GOV-007: independent validation relies on vendor/generic benchmark claims, not
     firm-specific testing)
Deployment approved with no documented tolerance threshold
  ↓ (IRQ-MOD-004 — THIS IRQ: no measured confabulation rate for this task/domain)
Model fabricates a fact, figure or citation in a live customer/AML/claims interaction
  ↓ (IRQ-MOD-005: model does not behaviourally flag missing/uncertain evidence)
No detection signal reaches the reviewer or downstream system
  ↓ (IRQ-HUM-001: automation bias; fluent fabricated content is accepted)
Wrong decision, mis-statement, or flawed regulatory filing issued
  ↓
Complaint/FOS or regulatory discovery → finding that hallucination risk was never
quantified before deployment → remediation, reputational damage

Control Breakpoints:
  • IRQ-GOV-007: independent validation demands firm-relevant, task-representative testing
  • IRQ-MOD-004: hallucination rate measured and tolerance threshold documented pre-deployment
  • IRQ-MOD-005: behavioural distinction of missing/uncertain evidence (abstention over fabrication)
  • IRQ-HUM-001/002: reviewer challenge and disagreement-rate monitoring
```

## 7. Why a Domain Expert May Miss It
- FS SMEs are used to model validation reporting a single accuracy number; they may accept a vendor's generic benchmark hallucination rate (e.g. from a public leaderboard) as sufficient, not realising it does not transfer to the firm's specific documents, terminology and task framing.
- The assumption "the system either works or it doesn't" is inapposite — hallucination is probabilistic and task-dependent; a rate acceptable for internal drafting assistance may be wholly unacceptable for customer-facing fact statements.
- Fabricated content is stylistically indistinguishable from correct content, so spot-checking by non-specialists tends to catch only implausible errors, not plausible-but-wrong ones (cf. Mata v. Avianca, CNET incidents).
- Vendor-reported hallucination benchmarks are typically measured on public, English-language, general-knowledge tasks — not on the firm's proprietary product terms, jurisdiction-specific rules, or house style, which is exactly where task-representative measurement diverges from vendor claims.

## 8. Assurance Objective
**AO-MOD-004:** The frequency and severity of hallucinated facts, figures and citations shall be measured on tasks representative of the intended FS use, and a documented tolerance threshold shall be established and approved before deployment.

## 9. Expected Controls (Traced)
- **Task-representative hallucination measurement** — [Ji et al., 2023, "Survey of Hallucination in Natural Language Generation", ACM Comput. Surv., arXiv:2202.03629; Huang et al., 2023/25, ACM TOIS survey, arXiv:2311.05232] — hallucination rate is measured on FS-domain-specific prompts and documents, not generic benchmarks.
- **Atomic-fact precision scoring** — [Min et al., 2023, "FActScore", arXiv:2305.14251] — outputs are decomposed into atomic factual claims and each independently verified against source documents.
- **Zero-resource/black-box detection where logits are unavailable** — [Manakul et al., 2023, "SelfCheckGPT", arXiv:2303.08896] — sampling-consistency-based hallucination detection usable for hosted/API models where internal probabilities are inaccessible.
- **Documented tolerance threshold approved by governance** — [PRA SS1/23, May 2023, development/validation principles; linked IRQ-GOV-006 risk appetite] — a measured, explicit tolerance (e.g. maximum acceptable rate of material factual error per task class) is set and approved, not assumed.
- **Independent, firm-relevant validation rather than reliance on vendor/public benchmark claims** — [linked IRQ-GOV-007, IRQ-MOD-011] — validation uses the firm's own documents and task framing, contamination-checked.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor-reported hallucination benchmark score (public leaderboard) — **L1** (assertion; not task-representative; flag explicitly).
- Design documentation defining the task-representative test methodology (FActScore-style atomic fact-checking, SelfCheckGPT sampling) and the approved tolerance threshold — **L2**.
- Staging test results: hallucination rate measured on a representative FS task sample (e.g. n≥150 customer queries or claims summaries, the design minimum used in §11), with atomic-fact precision and severity classification — **L3**.
- Independent validation report confirming the measurement methodology and result set, performed by a function independent of development — **L4**.
- Production monitoring/complaint-analysis data showing post-deployment hallucination incidence and severity trends — **L5**.

## 11. Independent Test
> In a non-production environment, assemble a representative sample of the firm's actual task type (e.g. n≥150 customer-facing product queries, claims summaries, or AML narrative drafts) with verifiable ground truth drawn from source documents. Run the pipeline and apply atomic-fact decomposition and verification (FActScore-style) to each output, classifying each hallucination by severity (cosmetic vs material/decision-relevant). Where model-internal probabilities are unavailable (hosted API), corroborate with a sampling-consistency check (SelfCheckGPT-style: multiple independent generations compared for factual consistency). Compare the measured rate against the documented tolerance threshold. Executed entirely on synthetic/anonymised or historical non-live data in staging. Methodology per Min et al. (2023) and Manakul et al. (2023) — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (credible, peer-reviewed measurement methods with multiple independent research groups; no single canonical hallucination-rate benchmark exists for FS-specific tasks, so test design and severity classification rest on professional judgement).

## 12. Pass Indicators
- Measured hallucination rate on the task-representative sample is at or below the approved tolerance threshold, with material/decision-relevant hallucinations at or near zero.
- Severity classification distinguishes cosmetic from material errors; only cosmetic errors occur at any meaningful rate.
- Tolerance threshold is documented and was formally approved by governance before deployment, not asserted after the fact.
- Production monitoring shows no material divergence from the staging-measured rate over time.

## 13. Fail Indicators
- No task-representative measurement was performed; only a generic or vendor-reported benchmark score is cited.
- Material/decision-relevant hallucinations occur at a non-trivial rate in the representative sample (e.g. fabricated policy terms, invented case facts).
- No documented, governance-approved tolerance threshold exists — "acceptable" hallucination risk was never explicitly decided.
- Production complaint or QA data reveals hallucination-driven customer harm with no corresponding staging measurement having anticipated the risk.

## 14. Reporting Language
**Pass:** "Hallucination rate has been measured on a task-representative sample using atomic-fact verification, with material/decision-relevant errors at or near zero and within the governance-approved tolerance threshold. Conclusions rest on ★3 methodology — credible peer-reviewed measurement, no industry benchmark — and represent professional assessment, to be revalidated periodically and on material task or model change."

**Fail:** "No task-representative hallucination measurement exists; the only evidence available is a generic vendor benchmark score, which does not reflect the firm's specific documents, terminology or task framing. Independent staging testing on a representative sample found [n]% material/decision-relevant fabrications, with no governance-approved tolerance threshold ever set. This is a foundational assurance gap for any generative system used in customer-facing or regulatory-facing FS tasks; deployment should not proceed until task-representative measurement and an approved tolerance are in place."

**Partial:** "Task-representative measurement exists for [use case A] but not for [use case B], despite both drawing on the same underlying model and prompt family. The assurance objective is not met for use case B; deployment should be restricted to measured use cases pending equivalent testing."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (multiple customers/cases exposed to fabricated material facts; regulatory
              notice risk under Consumer Duty)
  Likelihood: 2 (measurement and tolerance-gating should catch material fabrication before
              deployment; residual risk requires drift beyond the tested distribution)
  Detectability: 2 (atomic-fact QA sampling and complaint monitoring surface issues within
              days-to-weeks)
  Recoverability: 2 (affected outputs traceable via logs; correction and customer remediation
              feasible)
  Novelty: 3 (FS SMEs understand "the system can be wrong" but not that fabrication rate is
              probabilistic, task-dependent and requires bespoke measurement rather than a
              single accuracy figure)

Interpretation: acceptable residual risk with task-representative measurement and an approved
tolerance in place; highest concern is Novelty — measurement discipline must be sustained as
task mix evolves, not treated as a one-off approval gate.

If controls are absent or degraded:
  Severity: 4 (systemic fabrication across customer-facing or regulatory-facing output with
              no quantified risk basis for the deployment decision at all)
  Likelihood: 4 (well-documented base rate of hallucination in generative models under
              standard operating conditions, not an edge case)
  Detectability: 4 (fluent fabrication is indistinguishable from correct content to
              non-specialist reviewers; silent until complaint or audit)
  Recoverability: 3 (requires full retrospective review of affected output population)
  Novelty: 3
Residual risk: Critical. Deployment gate should not be passed without task-representative
measurement.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Fabricated material facts affect multiple customers/cases; Consumer Duty and FOS exposure by analogy with documented incidents (Air Canada, CNET, Mata v. Avianca), one in finance journalism and two outside financial services. |
| **Likelihood** | 3 | Probable absent task-representative measurement: hallucination is a well-documented, near-universal property of current generative models, not a rare edge case. |
| **Detectability** | 3 | Fabricated content is stylistically indistinguishable from correct content; detection requires deliberate atomic-fact verification, not casual review. |
| **Recoverability** | 2 | Once identified, affected interactions are traceable via logs and correctable through customer communication and process remediation. |
| **Novelty** | 3 | FS SMEs are unfamiliar with hallucination as a probabilistic, task-dependent property requiring bespoke measurement rather than a single pass/fail accuracy check. |

## 17. Regulatory Basis
> [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] — the products & services and consumer understanding outcomes require that customer-facing communications and decisions are accurate and not foreseeably harmful; fabricated facts breach this directly. [PRA SS1/23, May 2023, effective 17 May 2024, Principle 3/4] — development/validation principles require that model risk (including generative fabrication) is identified, measured and mitigated before use. No regulation names "hallucination rate measurement" explicitly; this IRQ operationalises the above via task-representative testing. (verified 29 Jul 2026)

## 18. Research Basis
> [Ji, Z., et al., 2023, "Survey of Hallucination in Natural Language Generation", ACM Computing Surveys (arXiv:2202.03629)] — canonical taxonomy of intrinsic/extrinsic hallucination. [Huang, L., et al., 2023/25, "A Survey on Hallucination in Large Language Models", ACM TOIS (arXiv:2311.05232)] — comprehensive causes/detection/mitigation taxonomy. [Min, S., et al., 2023, "FActScore", arXiv:2305.14251] — atomic-fact precision metric enabling quantitative measurement. [Manakul, P., et al., 2023, "SelfCheckGPT", arXiv:2303.08896] — zero-resource, black-box-compatible hallucination detection. [Incident register: Air Canada tribunal ruling (Feb 2024); CNET AI-written finance articles (Jan 2023); Mata v. Avianca (Jun 2023); Deloitte Australia report refund (Oct 2025)] — real, documented hallucination-driven harm, one instance in finance journalism and three outside financial services.
>
> **RAGBench addition (v1.0.3).** [Friel, Belyi, Sanyal, 2024 (latest version January 2025), "RAGBench: Explainable Benchmark for Retrieval-Augmented Generation Systems", arXiv:2407.11005] — TRACe Adherence is an explicit, benchmark-scaled groundedness/faithfulness measure ("synonymous with answer faithfulness, groundedness, and attribution"), applied at 100k-example scale including a finance domain. Materially for evaluator design, the paper shows LLM-judge evaluation underperforms fine-tuned smaller evaluators on these tasks — a direct caution against the common practice of measuring hallucination with an unvalidated LLM judge. **What the test can now do:** quantify confabulation as an Adherence score against a published metric definition with domain-relevant (finance) reference data; and justify — with a citable finding — requiring the firm to validate its evaluator rather than accept LLM-as-judge scores at face value (links IRQ-MOD-011 evaluation-integrity concerns). No ★ change arises from this addition; the ★3 rating above is unaffected.
>
> **[FAIAS Incident Register, row 45, "Roadzen / The Motley Fool analyst-estimate misstatement", 2025]**, citing [Roadzen Inc., 2025, "Roadzen Addresses Inaccurate Reporting of Analyst Expectations in Q1 FY2026 Results", 18 August 2025; The Motley Fool, 2025, "Roadzen Posts 22% Q1 Revenue Gain", corrected article, updated 18 August 2025, and its pre-correction text as syndicated by AOL on 13 August 2025, read at the Internet Archive capture of 18 August 2025] — a market-facing article produced by a publisher's own generative system misstated the analyst consensus revenue expectation for a listed company. The company's statement records that the article "incorrectly stated analyst revenue expectations for Roadzen's Q1 were more than $21 million", implying that it "had missed estimates by over 50%", and that "[t]hese figures were not issued by Roadzen's covering analysts and had no factual basis"; on the company's figures actual revenue of $10.9 million was "modestly below estimates of $11.4 million (a 4.8% variance)", and the publisher's corrected article puts the shortfall at about 4.4%. What the publisher amended was the numbers — "A previous version of this article used incorrect analyst estimates. Numbers have been updated" — beside a standing disclosure that "JesterAI is a Foolish AI, based on a variety of Large Language Models (LLMs) and proprietary Motley Fool systems. All articles published by JesterAI are reviewed by our editorial team, and The Motley Fool takes ultimate responsibility for the content of this article." The pre-correction wording survives in the article's syndicated copy, which reported that revenue "missed consensus estimates by nearly half, with GAAP revenue of $10.9 million coming in 48.7% below the analysts' estimate of $21.26 million". A figure that the subject company states had no factual basis, in generated market commentary, is syndicated and read before any correction reaches the same readers — whether the system generated it or carried an incorrect input is not stated by either party — which is the condition a measured tolerance for this use is set against.
>
> **Research basis last reviewed:** 19 September 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-MOD-005 (B.2: behavioural distinction of missing/uncertain evidence — the abstention
    counterpart to this IRQ's measurement focus)
  - IRQ-MOD-006 (B.3: calibration — whether expressed confidence tracks the measured
    hallucination-driving accuracy)
  - IRQ-MOD-011 (B.5: evaluation integrity — measurement must be contamination-checked and
    firm-relevant, not vendor/public benchmark)
  - IRQ-GOV-007 (I.3: independent validation must use firm-relevant evaluations)
  - IRQ-CON-004 (H.2: customer-facing content accuracy under Consumer Duty)
  - IRQ-HUM-001 (D.1: reviewer challenge of fluent but fabricated output)
```

## 20. References
```
[1] Ji, Z., Lee, N., Frieske, R., et al., 2023. "Survey of Hallucination in Natural Language
    Generation." ACM Computing Surveys. arXiv:2202.03629.
[2] Huang, L., Yu, W., Ma, W., et al., 2023 (rev. 2025). "A Survey on Hallucination in Large
    Language Models: Principles, Taxonomy, Challenges, and Open Questions." ACM Transactions
    on Information Systems. arXiv:2311.05232.
[3] Min, S., Krishna, K., Lyu, X., et al., 2023. "FActScore: Fine-grained Atomic Evaluation
    of Factual Precision in Long Form Text Generation." arXiv:2305.14251.
[4] Manakul, P., Liusie, A., Gales, M., 2023. "SelfCheckGPT: Zero-Resource Black-Box
    Hallucination Detection for Generative Large Language Models." arXiv:2303.08896.
[5] FCA, 2022. "PS22/9: A New Consumer Duty." PRIN 2A in force 31 July 2023.
[6] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023, effective
    17 May 2024.
[7] Civil Resolution Tribunal (British Columbia), 2024. Moffatt v. Air Canada, 2024 BCCRT
    149. Ruling 14 Feb 2024.
[8] Roadzen Inc., 2025. "Roadzen Addresses Inaccurate Reporting of Analyst
    Expectations in Q1 FY2026 Results." GlobeNewswire, 18 August 2025.
[9] The Motley Fool, 2025. "Roadzen Posts 22% Q1 Revenue Gain." Corrected
    article, updated 18 August 2025; pre-correction text as syndicated by
    AOL on 13 August 2025, Internet Archive capture of 18 August 2025.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: B.2 (Model domain, Hallucination)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): FS SMEs accept vendor/generic benchmark hallucination rates as
  sufficient, not realising fabrication rate is task- and domain-dependent and requires
  bespoke, firm-relevant measurement.
✓ Test 2 (Plausible Harm): Grounded in peer-reviewed hallucination research (Ji et al.,
  Huang et al., Min et al., Manakul et al.) and multiple real incidents (Air Canada, CNET,
  Mata v. Avianca, Deloitte Australia).
✓ Test 3 (Testable): Fully testable in staging via atomic-fact verification on
  task-representative samples; no production data required. ★3 methodology.
✓ Test 4 (Decision-Relevant): Outcome directly gates deployment approval and sets the
  governance-approved tolerance threshold condition of use.

Change Log:
- v1.0 (2026-07): Initial publication; four tests passed.
- v1.2.0 (2026-09-12): Field 10 — the illustrative sample size harmonised to the design minimum already used in §11 ("e.g. n=200 customer queries or claims summaries" → "e.g. n≥150 …, the design minimum used in §11"), attributed to this standard's own test design and not to the FActScore paper, which states no such recommendation. No change to controls, test, ★3 or risk profile.
- v1.2.1 (2026-09-19): Field 18 — incident-register citation added in the reserved form (row 45, Roadzen / The Motley Fool analyst-estimate misstatement), carrying both parties' own figures and the pre-correction wording as the article's syndicated copy preserves it; reference entries [8] and [9] added at Field 20. Field 18 — erratum: the four incidents cited from the register are no longer described as FS-adjacent; three are outside financial services and one is finance journalism. Field 16 — erratum: the three incidents cited as documenting Consumer Duty and FOS exposure are now cited by analogy, one in finance journalism and two outside financial services. Research-basis review date moved. No change to controls, test, ★3 or any five-axis rating.
```

---
---

