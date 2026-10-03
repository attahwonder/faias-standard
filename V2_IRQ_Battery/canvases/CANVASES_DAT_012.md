# CANVAS: IRQ-DAT-012

## 1. IRQ ID & Title
**IRQ-DAT-012: Unmanaged Retrieval, Embedding and Document Drift**

Register question: "Are retrieval, embedding and document drift managed — e.g. embedding-model changes silently invalidating index geometry, or corpus composition shifting what the system retrieves?"

## 2. Business Activities Affected
- **RAG-grounded advisory and customer service:** Any silent embedding-model update by a vendor, or gradual corpus composition change, alters what gets retrieved for a given query without any code change triggering review.
- **Compliance and policy assistants:** As the underlying document corpus grows or is reorganised, retrieval behaviour for the same query can drift even if no individual document changed.
- **Claims and underwriting copilots:** Embedding-index rebuilds after a model or infrastructure change can silently degrade retrieval precision for niche or rare query types.

## 3. AI Behaviour(s)
- Retrieves based on vector-similarity scoring against an embedding index that assumes a fixed embedding geometry; if the embedding model changes, old and new vectors may no longer be comparable.
- Retrieval results shift as the underlying corpus composition changes (new documents added, old ones removed, relative topic balance shifting), even where no single document is itself wrong.
- Provides no inherent signal that retrieval quality has degraded — outputs look equally fluent whether grounded in high- or low-quality retrieval.

## 4. Failure Mode
> Retrieval, embedding and document-corpus drift are not managed — an embedding-model change silently invalidates index geometry, or corpus composition shifts what the system retrieves for a given query — so retrieval quality degrades without any code-level trigger for review, and this is invisible in generation fluency alone.

## 5. Potential Consequences
- **Customer:** Receives responses grounded in lower-quality or less-relevant retrieved content following an unmanaged embedding or corpus change, without any visible signal of degraded reliability.
- **Institution:** A vendor-side embedding-model update (a third-party change, per IRQ-TPR-004) silently degrades retrieval across the estate without triggering the firm's own change-control process.
- **Regulator:** PRA SS1/23 and EU AI Act Art. 15 ongoing-robustness obligations extend to retrieval-layer components, not only the generative model itself.

## 6. Failure Chain
```
Embedding model is updated (by vendor or internally) or the document
corpus composition shifts materially, without a re-indexing/
re-validation trigger
  ↓ (IRQ-DAT-012 — THIS IRQ: retrieval/embedding/document drift unmanaged)
Index geometry becomes stale relative to the current embedding model,
or retrieval relevance shifts as corpus composition changes
  ↓ (IRQ-TPR-004: if vendor-driven, the firm's silent-provider-change
     detection did not catch the embedding update specifically)
Retrieval quality degrades for a subset of query types; generated
responses remain fluent, masking the degradation
  ↓ (IRQ-MOD-004/-005: hallucination/evidence-grounding controls,
     if not retrieval-drift-aware, do not catch this specific cause)
Customers receive lower-quality grounded responses over an extended
period before discovery
  ↓
Complaint pattern or targeted audit surfaces the degradation;
remediation requires re-indexing and root-cause investigation

Control Breakpoints:
  • IRQ-DAT-012: re-indexing/re-validation triggers on embedding or corpus change
  • IRQ-TPR-004: vendor-side embedding-model version pinning and canary detection
  • IRQ-MOD-004/-005: hallucination/grounding monitoring includes retrieval-quality signals
```

## 7. Why a Domain Expert May Miss It
- RAG SMEs (and even many technical teams) think of the generative model as the component requiring version control, without extending the same discipline to the embedding model and index — a genuinely separate, silently-changeable component.
- A vendor updating an embedding API "under the hood" (a common SaaS pattern) can invalidate index geometry without any visible error — old and new vectors remain the same dimensionality, so nothing breaks loudly, it just retrieves worse.
- Corpus composition drift (organic growth or reorganisation of the document store) is a gradual, unremarkable-seeming process; nobody treats "we added 500 more documents" as a retrieval-validation trigger.
- Because generation remains fluent regardless of retrieval quality, there is no natural signal — a human reviewer sees a well-written answer and has no basis to suspect the underlying retrieval degraded.

## 8. Assurance Objective
**AO-DAT-012:** Retrieval, embedding and document-corpus drift shall be managed through defined re-indexing and re-validation triggers, such that embedding-model changes or corpus composition shifts do not silently degrade retrieval quality.

## 9. Expected Controls (Traced)
- **Embedding-model version pinning and change detection** — [linked IRQ-TPR-004, IRQ-TPR-006; Chen et al., 2023, "How Is ChatGPT's Behavior Changing over Time?"] — the embedding model in use is version-pinned, with canary testing to detect silent vendor-side changes.
- **Re-indexing trigger on embedding-model change** — [general vector-database engineering practice; no single published FS standard] — any embedding-model version change triggers a full or partial re-index, not a mixed-geometry index.
- **Retrieval-quality monitoring independent of generation fluency** — [Es et al., 2023, "RAGAS: Automated Evaluation of RAG"; Chen et al., 2023, "Benchmarking Large Language Models in Retrieval-Augmented Generation" (RGB)] — retrieval precision/recall metrics are monitored directly, not inferred from downstream generation quality.
- **Corpus-composition drift review on material corpus growth or reorganisation** — [Emerging Practice — grounded in general information-retrieval index-maintenance discipline] — material corpus changes trigger a retrieval-quality re-validation, analogous to a data-drift check.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "our RAG system is regularly updated" with no version-control or re-indexing detail — **L1**.
- Embedding-model version-pinning and re-indexing trigger documentation — **L2**.
- Code/config inspection confirming re-indexing actually executes on embedding-model change, and retrieval-quality metrics are actually computed (not merely defined) — **L3**.
- Staging test results: a simulated embedding-model version change or corpus composition shift, with retrieval precision/recall measured before and after — **L3**.
- Independent audit of the retrieval-quality monitoring pipeline and a sample historical re-indexing event traced from trigger to completion — **L4**.
- Production retrieval-quality metrics tracked over time, correlated against known embedding-model or corpus-composition change events — **L5**.

## 11. Independent Test
> In a non-production replica of the retrieval pipeline, (a) simulate an embedding-model version change by re-embedding a subset of the corpus with a different model version while leaving the rest on the original vectors (mixed-geometry index), and measure retrieval precision/recall degradation on a representative query set; (b) simulate corpus composition drift by adding a substantial volume of topically-skewed new documents and re-measuring retrieval relevance for existing query types. Compare against RAGAS-style faithfulness/relevance metrics (Es et al., 2023) and RGB robustness benchmarking (Chen et al., 2023). No production data used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (RAG evaluation tooling like RAGAS is published and used by multiple groups, but "retrieval/embedding drift" specifically as a monitored, benchmarked phenomenon is newer and less standardised than generation-quality evaluation; test design for the mixed-geometry and corpus-drift scenarios is largely bespoke).

## 12. Pass Indicators
- No mixed-geometry index exists in production; embedding-model changes trigger full re-indexing before the new model is used for live retrieval.
- Staging simulation of corpus composition drift shows retrieval precision/recall within the firm's documented tolerance versus the pre-drift baseline.
- Retrieval-quality metrics are monitored directly and independently of generation-fluency signals.
- A sample historical re-indexing event, if any occurred, shows complete and timely execution.

## 13. Fail Indicators
- Staging testing shows a simulated embedding-model change produces a mixed-geometry index with measurable retrieval-quality degradation, undetected by current monitoring.
- No retrieval-quality metric is monitored independently of generation output; degraded retrieval is invisible until a complaint pattern emerges.
- Corpus composition changes occur with no re-validation trigger, regardless of scale.
- Vendor-side embedding-model updates are not detected (no version pinning or canary testing).

## 14. Reporting Language
**Pass:** "Simulated embedding-model version change and corpus composition drift testing found retrieval precision/recall within documented tolerance following the firm's re-indexing and re-validation triggers; no mixed-geometry index risk exists in production. This is ★2 professional-judgement testing given the emerging, bespoke nature of retrieval-drift benchmarking."

**Fail:** "Simulated embedding-model version change produced a measurable retrieval-quality degradation consistent with a mixed-geometry index, which current monitoring did not detect because retrieval quality is not measured independently of generation fluency. Vendor-side embedding-model changes are not version-pinned or canary-tested. This represents a credible, currently-undetectable path to silent retrieval-quality degradation across the customer-facing estate and requires remediation."

**Partial:** "Re-indexing triggers exist for internally-managed embedding-model changes but not for vendor-side (API) embedding updates, which account for [x]% of the retrieval stack. Extend version-pinning/canary detection to vendor components before the assurance objective is met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (degraded but not absent retrieval grounding; correctable via re-indexing)
  Likelihood: 2 (plausible on vendor-side embedding updates specifically, a foreseeable but
                 not universal gap)
  Detectability: 3 (requires dedicated retrieval-quality monitoring, independent of
                    generation-fluency signals, to surface promptly)
  Recoverability: 2 (remediable via re-indexing once identified)
  Novelty: 4 (embedding-geometry invalidation and corpus-drift effects on retrieval are
              deep RAG-engineering-specific knowledge, invisible to most SMEs and even
              many generalist technical reviewers)

If controls are absent or degraded:
  Severity: 3 (sustained retrieval-quality degradation across the customer-facing estate,
              masked by fluent generation)
  Likelihood: 3 (vendor-side silent embedding changes and organic corpus growth are both
                 common, foreseeable, unmanaged-by-default events)
  Detectability: 4 (structurally invisible without dedicated retrieval-quality monitoring;
                    generation fluency provides no signal)
  Recoverability: 2 (remediable via re-indexing once identified)
  Novelty: 4
Residual risk: material and likely underestimated, because the failure is specifically
designed (by architecture, not intent) to be invisible in normal quality review.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Sustained retrieval-quality degradation across the customer-facing estate, masked by fluent generation output. |
| **Likelihood** | 2 | Plausible via vendor-side silent embedding updates or organic corpus growth, both foreseeable but not universal. |
| **Detectability** | 4 | Structurally invisible without dedicated retrieval-quality monitoring independent of generation fluency — a genuinely silent failure mode. |
| **Recoverability** | 2 | Remediable via re-indexing once identified. |
| **Novelty** | 4 | Embedding-geometry invalidation and corpus-drift effects are specialist RAG-engineering knowledge, well outside FS domain and even general technical review expertise. |

## 17. Regulatory Basis
> [PRA SS1/23, May 2023, Principle 4/5 ongoing monitoring] extends to all model components influencing output, including the retrieval layer. [EU AI Act, Regulation (EU) 2024/1689, Art. 15(1)] robustness-maintenance obligation applies to the retrieval-augmented system as a whole, not the generative component alone. No regulation names embedding/retrieval drift explicitly. [UNVERIFIED — no further pinpoint exists; mechanism genuinely unaddressed by name] (verified 29 Jul 2026).

## 18. Research Basis
> [Chen, L., Zaharia, M., Zou, J., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009] — direct empirical evidence that a fixed vendor API endpoint drifts substantially over months, the closest documented analogue to silent vendor-side embedding-model change. [Es, S., et al., 2023, "RAGAS: Automated Evaluation of RAG", arXiv:2309.15217] — reference-free retrieval/faithfulness metrics enabling retrieval-quality monitoring independent of generation fluency. [Chen, J., et al., 2023, "Benchmarking Large Language Models in Retrieval-Augmented Generation" (RGB), arXiv:2309.01431] — robustness-testing dimensions applicable to corpus-drift scenarios.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-007 (A.3: RAG ingestion curation — a related but distinct concern, currency vs geometry)
  - IRQ-DAT-011 (A.5: statistical/semantic/source input drift — the model-input-layer counterpart)
  - IRQ-TPR-004 (F.2: silent vendor-side model change detection — the embedding-model-specific instance)
  - IRQ-TPR-006 (F.3: embedding/vector-database dependency and lock-in — the commercial-dependency counterpart)
```

## 20. References
```
[1] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over Time?"
    arXiv:2307.09009.
[2] Es, S., James, J., Espinosa-Anke, L., Schockaert, S., 2023. "RAGAS: Automated Evaluation
    of Retrieval Augmented Generation." arXiv:2309.15217.
[3] Chen, J., et al., 2023. "Benchmarking Large Language Models in Retrieval-Augmented
    Generation." arXiv:2309.01431.
[4] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
[5] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act." Art. 15.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.5 (Data domain, Data Drift)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Version-control discipline is applied to the generative model but
  rarely extended to the embedding model/index, which can change silently without error.
✓ Test 2 (Plausible Harm): Grounded in Chen et al. (2023) empirical evidence of silent vendor
  API drift and RAG evaluation literature (RAGAS, RGB) enabling detection.
✓ Test 3 (Testable): Simulated embedding-version-change and corpus-drift testing are
  executable in non-production. ★2.
✓ Test 4 (Decision-Relevant): Gates whether retrieval-layer changes require re-indexing/
  re-validation before continued reliance.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

