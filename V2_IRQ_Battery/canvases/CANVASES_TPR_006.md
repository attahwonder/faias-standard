# CANVAS: IRQ-TPR-006

## 1. IRQ ID & Title
**IRQ-TPR-006: Hidden Embedding/Vector Database Lock-In and Index Invalidation Risk**

Register question: "Do embedding models and vector databases create hidden dependencies — index invalidation on embedding-model change, or lock-in without export paths?"

## 2. Business Activities Affected
- **RAG-grounded customer service and advisory:** Retrieval quality for any grounded generation workflow depends entirely on embedding-index integrity; a silent embedding model change invalidates the index geometry without an obvious symptom.
- **Knowledge management and search:** Internal knowledge retrieval tools built on the same vector infrastructure inherit the same fragility.
- **Business continuity/exit planning:** Vector database vendor lock-in without an export path undermines the firm's ability to substitute providers within impact tolerance (links RES-004, TPR-008).

## 3. AI Behaviour(s)
- System embeds documents into a vector space using a specific embedding model, then retrieves by nearest-neighbour similarity at query time using the same embedding model.
- If the embedding model changes (provider update, version bump) but the stored index is not regenerated, retrieval silently degrades — queries embedded under the new model are compared against vectors from the old geometry.
- Vector database vendor may use proprietary index formats with no standard export mechanism.

## 4. Failure Mode
> A change to the embedding model used for query-time encoding is not matched by re-indexing the stored document vectors (or vice versa), so retrieval silently returns semantically irrelevant results while appearing to function normally — and/or the firm cannot migrate away from its vector database vendor because no viable export path exists, creating unmanaged dependency risk.

## 5. Potential Consequences
- **Customer:** RAG-grounded responses degrade in relevance/accuracy without any visible error — the system still "answers," just increasingly wrongly, directly linking to hallucination risk (IRQ-MOD-004).
- **Institution:** Vector database vendor lock-in prevents timely substitution if the vendor fails, raises prices materially, or exits the market, with disproportionate remediation cost (full re-embedding of the corpus).
- **Regulator/market:** If retrieval degradation affects a regulated advisory or disclosure process, this compounds into a Consumer Duty or model risk finding whose root cause (infrastructure, not model) is easy to misdiagnose.

## 6. Failure Chain
```
Embedding model or vector database version changes (provider update,
internal migration, or cost-driven model swap)
  ↓ (IRQ-DAT-012: retrieval/embedding drift not monitored at the data layer)
Stored index is not regenerated to match the new embedding geometry
  ↓ (IRQ-TPR-006 — THIS IRQ: hidden dependency between embedding model
     version and index validity is not documented or tested)
Retrieval returns semantically mismatched documents; system still
returns a fluent, confident-sounding answer
  ↓ (IRQ-MOD-004: hallucination/confabulation risk realised via
     degraded grounding, not model weakness)
Customer receives inaccurate grounded response; root cause
misdiagnosed as a model problem, delaying correct remediation

Control Breakpoints:
  • IRQ-DAT-012: retrieval-layer drift monitoring with re-indexing triggers
  • IRQ-TPR-006: documented dependency mapping with rebuild/exit plan
  • IRQ-RES-004: rehearsed rollback/rebuild of the index within recovery objectives
```

## 7. Why a Domain Expert May Miss it
- Retrieval degradation produces no error message — the system continues to function and "answer," so traditional monitoring (uptime, error rate) shows green while output quality silently deteriorates.
- The dependency between embedding-model version and index validity is a narrow, AI-infrastructure-specific concept; a domain SME reviewing "the model" (the LLM) would not think to check "the embedding model" as a separate, coupled component.
- Vector database procurement is often treated as a standard database/infrastructure decision, missing the AI-specific lock-in risk (proprietary index formats, no standard export/rebuild tooling).
- Re-embedding an entire corpus is expensive and slow, so teams are incentivised to avoid discovering the problem rather than proactively test for it.

## 8. Assurance Objective
**AO-TPR-006:** The firm shall document and test the dependency between embedding-model version and vector index validity, ensure index re-generation is triggered on embedding-model change, and maintain a viable rebuild and export/exit path for its vector database dependency.

## 9. Expected Controls (Traced)
- **Embedding/retrieval drift monitoring and re-indexing triggers** — [linked IRQ-DAT-012] — detect embedding-model version mismatch between query-time and index-time encoding; trigger automated or gated re-indexing.
- **Documented dependency mapping** — [linked IRQ-TPR-008, IRQ-RES-007] — embedding-model-to-index dependency recorded in the firm's technical dependency register as part of AI-in-IBS mapping.
- **Rehearsed index rebuild within recovery objectives** — [linked IRQ-RES-004] — rebuild procedure tested against defined RTO for the affected service.
- **Vector database exit/portability assessment** — [linked IRQ-TPR-002] — contractual and technical export path confirmed as part of provider due diligence and contract negotiation.
- **Retrieval quality regression testing on index change** — Emerging Practice — no published FS-specific standard; firms are adapting general information-retrieval evaluation methods (precision@k, recall) to this specific trigger event.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "retrieval is working fine" based on absence of error logs — **L1**.
- Dependency map documenting embedding model version, index format, and vendor export capability — **L2**.
- Staging test: deliberately mismatch embedding-model version between index and query time; measure retrieval relevance degradation — **L3**.
- Independent review confirming re-indexing triggers actually fire on embedding-model change events in the current architecture — **L4**.
- Production retrieval quality monitoring data (relevance/precision metrics) over the last 90 days, including any re-indexing events and their impact — **L5**.

## 11. Independent Test
> In staging, intentionally update the embedding model used for query encoding while leaving the stored index un-regenerated; run a fixed query set and measure retrieval relevance (precision@k) against the pre-change baseline. Separately, attempt a full data export from the vector database using only documented vendor mechanisms, and record success/time/completeness. Non-production environment; no customer data used if synthetic corpus available, otherwise anonymised. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (information-retrieval evaluation metrics are well established generally — ★4 for that component — but the specific "embedding-version mismatch" test scenario and vector-database export testing are bespoke, FS-specific applications with no agreed benchmark — blended rating reflects the weaker, novel component).

## 12. Pass Indicators
- Staging test confirms re-indexing triggers fire correctly on embedding-model version change; no undetected mismatch state is reachable in the tested architecture.
- Retrieval quality monitoring is in place in production with defined relevance thresholds.
- Full data export from the vector database succeeds via documented vendor mechanisms within a reasonable timeframe.
- Dependency map is current and reviewed at least annually or on material architecture change.

## 13. Fail Indicators
- Staging test demonstrates a mismatch state (query embedded under new model, index unchanged) that produces degraded but undetected retrieval — no monitoring or alert fires.
- No retrieval quality monitoring exists in production; the only signal of a problem is customer complaint.
- Data export from the vector database is not possible via any documented mechanism, or requires vendor professional services with no defined SLA.
- No dependency map exists linking embedding model version to index validity.

## 14. Reporting Language
**Pass:** "Staging testing confirms re-indexing triggers correctly detect and respond to embedding-model version changes; production retrieval quality monitoring is active with defined thresholds. Vector database export was demonstrated successfully via documented vendor mechanisms. Conclusions rest on a blended methodology — ★4 for information-retrieval evaluation, ★2 for the FS-specific mismatch and export test design — and should be read accordingly."

**Fail:** "Staging testing reproduced an undetected retrieval-degradation state following a simulated embedding-model mismatch, with no monitoring or alert triggered. No viable data export path exists from the current vector database vendor. This combination represents both an active quality risk (silent hallucination-adjacent degradation) and a business continuity risk (unmanaged lock-in)."

**Partial:** "Re-indexing triggers are implemented for the primary production RAG pipeline but not for a secondary internal knowledge-search tool sharing the same vector infrastructure. Export capability has been demonstrated at small scale but not tested at full production corpus volume."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (retrieval degradation is typically gradual and workflow-bounded)
  Likelihood: 2 (embedding model changes are infrequent but do occur, especially via provider-side updates)
  Detectability: 2 (relevance monitoring, if active, detects the shift promptly)
  Recoverability: 2 (re-indexing is achievable within hours-to-days depending on corpus size)
  Novelty: 3 (requires understanding of the embedding-index coupling, an AI-infrastructure-specific concept)

If controls are absent or degraded:
  Severity: 3 (systematic, undetected retrieval degradation affects all users of the RAG system; compounds into hallucination-driven customer harm)
  Likelihood: 3 (probable given embedding models are updated by providers on their own cadence)
  Detectability: 4 (silent by design; no error state, only quality decay)
  Recoverability: 3 (full corpus re-embedding is slow and costly if not automated; vendor lock-in extends recovery timelines further)
  Novelty: 4 (fully outside traditional data/infrastructure review scope)

Residual risk interpretation: Detectability is the dominant concern — this failure mode produces no natural error signal, making proactive retrieval quality monitoring the single highest-value control.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|------|--------|---------------|
| **Severity** | 2 | Bounded to retrieval-dependent workflows; severity rises where those workflows are customer-facing and material |
| **Likelihood** | 2 | Embedding model changes are periodic rather than constant, but firm rarely controls their timing |
| **Detectability** | 4 | No natural error signal; requires dedicated relevance monitoring to detect at all |
| **Recoverability** | 2 | Re-indexing is technically straightforward if automated and rehearsed |
| **Novelty** | 4 | The embedding-index coupling is a narrow, AI-infrastructure-specific dependency unfamiliar outside specialist teams |

## 17. Regulatory Basis
> No FS regulation directly addresses embedding/vector database dependency risk; this IRQ is grounded in general ICT dependency mapping and business continuity obligations ([Regulation (EU) 2022/2554, DORA, Art. 11] business continuity policy; [PRA SS2/21, November 2024 (15 November 2024, updating 29 March 2021)] outsourcing and third-party risk, including exit planning) applied to this specific AI-infrastructure dependency [UNVERIFIED — SS2/21 does not name embedding/vector-database dependencies specifically; applicability is FAIAS's interpretive extension] (verified 29 Jul 2026).

## 18. Research Basis
> No peer-reviewed research specifically documents "embedding-index mismatch" as a named failure class in FS contexts [UNVERIFIED — no such named study was located after search, and no FS-specific study was located; non-FS peer-reviewed work measures the retrieval loss when queries from a newer embedding model search an index built with an older one (Vejendla, H., 2025, "Drift-Adapter: A Practical Approach to Near Zero-Downtime Embedding Model Upgrades in Vector Databases", EMNLP 2025, pp. 15938-15949)] (verified 29 Jul 2026; Vejendla read 7 Oct 2026). This IRQ is grounded in established information-retrieval evaluation methodology (precision/recall metrics) and general software dependency/lock-in risk analysis, applied to the specific technical coupling between embedding models and vector index geometry.
>
> For the metrics used in the staging test, [Muennighoff, N., Tazi, N., Magne, L., Reimers, N., 2023, "MTEB: Massive Text Embedding Benchmark", Proceedings of the 17th Conference of the European Chapter of the Association for Computational Linguistics (EACL 2023), pp. 2014–2037, https://doi.org/10.18653/v1/2023.eacl-main.148] provides public retrieval datasets and metrics: the model under test embeds all queries and all corpus documents, and the benchmark reports nDCG, MRR, MAP, precision and recall at several cut-offs, with nDCG@10 as its main metric. It compares embedding models, each used for both queries and corpus. It does not test a stale index queried by a new model. Its code is public at github.com/embeddings-benchmark/mteb. [Vejendla, H., 2025, "Drift-Adapter: A Practical Approach to Near Zero-Downtime Embedding Model Upgrades in Vector Databases", Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing (EMNLP 2025, Main), pp. 15938–15949, https://doi.org/10.18653/v1/2025.emnlp-main.805] is a mitigation paper by a single author: it trains a mapping from new-model queries into the old embedding space. In its evaluation, the baseline with no adaptation, which searches the old index with new-model queries, reaches 0.589 to 0.723 of the Recall@10 of a full re-embedding on three public text datasets in an upgrade from MiniLM to MPNet. It is not a financial-services study or a monitoring protocol, and the paper names no code repository. No ★ change follows from this addition.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
Related IRQs:
  - IRQ-DAT-012 (A.5 Data Drift: retrieval/embedding/document drift monitoring)
  - IRQ-MOD-004 (B.2 Hallucination: degraded grounding as a hallucination driver)
  - IRQ-RES-004 (G.2 Containment & Recovery: rollback/rebuild of index within recovery objectives)
  - IRQ-TPR-008 (F.3 Concentration: vector database provider as a concentration point)
```

## 20. References
```
[1] European Union, 2022. "Regulation (EU) 2022/2554 (DORA)", Art. 11.
    Applied: 17 January 2025
    URL: https://eur-lex.europa.eu/eli/reg/2022/2554/oj

[2] Prudential Regulation Authority, 2024. "SS2/21 — Outsourcing and third party risk management."
    Published: November 2024 (15 November 2024, updating 29 March 2021)
    URL: https://www.bankofengland.co.uk/prudential-regulation/publication/2021/march/outsourcing-and-third-party-risk-management-ss

[3] Muennighoff, N., Tazi, N., Magne, L., Reimers, N., 2023. "MTEB: Massive Text Embedding Benchmark." Proceedings of the 17th Conference of the European Chapter of the Association for Computational Linguistics (EACL 2023), pp. 2014–2037. Code: github.com/embeddings-benchmark/mteb.
    Published: May 2023
    URL: https://doi.org/10.18653/v1/2023.eacl-main.148

[4] Vejendla, H., 2025. "Drift-Adapter: A Practical Approach to Near Zero-Downtime Embedding Model Upgrades in Vector Databases." Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing (EMNLP 2025, Main), pp. 15938–15949. The paper names no code repository.
    Published: November 2025
    URL: https://doi.org/10.18653/v1/2025.emnlp-main.805
```

## 21. Four-Test Validation Footer
```
---
**Version:** the release version in `README.md`
**Subdomain:** F.3 (Third Party domain, Dependencies, Concentration & Data Handling)
**Status:** Active

**FOUR-TEST VALIDATION:**
✓ Test 1 (SME Blind Spot): Retrieval degradation produces no error signal; domain SMEs check "the model," not the coupled embedding/index layer.
✓ Test 2 (Plausible Harm): Grounded in information-retrieval evaluation methodology and general dependency/lock-in risk.
✓ Test 3 (Testable): Answerable via staging mismatch test and export-path demonstration.
✓ Test 4 (Decision-Relevant): Outcome gates whether retrieval quality monitoring investment is prioritised.

**Change Log:**
- v1.0 (2026-07): Initial publication.
- v1.3.3 (2026-10-09): Field 20 — the reference entry for PRA SS2/21 gives its current version, November 2024 (15 November 2024, updating 29 March 2021). No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS2/21 cited as its November 2024 version (15 November 2024, updating 29 March 2021); the expectations cited are unchanged.
- v1.3.3 (2026-10-09): Field 18 Research Basis — MTEB (EACL 2023) and Drift-Adapter (EMNLP 2025) cited with their limits stated; the Drift-Adapter figures give the retrieval loss of its no-adaptation baseline on public text, not on financial-services data. Field 20 References — entries [3] and [4] added. Research-basis review date moved. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — the tag now cites non-FS peer-reviewed work on retrieval across embedding-model versions (Vejendla, EMNLP 2025) and states that no FS-specific study was located; the first sentence of the field is unchanged. No change to the ★ rating or the risk profile.
```

---
---

