# CANVAS: IRQ-DAT-007

## 1. IRQ ID & Title
**IRQ-DAT-007: Uncurated RAG Ingestion Allowing Stale Content to Override Current Policy**

Register question: "Can documents enter the RAG knowledge store without curation, deduplication, currency checks and an assigned content owner, such that stale content can override current policy?"

## 2. Business Activities Affected
- **Policy and product-terms assistants:** Advisors and customer-facing assistants retrieve from a knowledge store that must reflect current, not superseded, policy and terms.
- **Claims handling copilots:** Retrieval of claims-handling procedures or coverage rules must reflect the current version; a superseded procedure surfacing as current directly drives wrong claims outcomes.
- **Compliance/regulatory guidance assistants:** Internal assistants answering "what does policy require" must not retrieve withdrawn or draft guidance as if current.

## 3. AI Behaviour(s)
- Retrieves whichever documents its indexing and ranking mechanism scores as relevant, with no innate concept of document currency, ownership or supersession.
- Treats all indexed content as equally authoritative unless the application layer encodes otherwise.
- Generates responses citing or synthesising retrieved content without independently verifying it is the current, owned, deduplicated version.

## 4. Failure Mode
> Documents enter the RAG knowledge store without curation, deduplication, currency checks or an assigned content owner, so stale or superseded content can be retrieved and presented as current, overriding the policy or terms actually in force.

## 5. Potential Consequences
- **Customer:** Receives advice, a quote or a claims decision based on withdrawn policy or superseded product terms; direct financial or contractual harm.
- **Institution:** Advice given on stale terms is not defensible; potential mis-selling or claims-handling breach; remediation cost across all affected interactions.
- **Regulator:** FCA Consumer Duty and PRIN breach if customer-facing outputs are systematically ungrounded in current policy.

## 6. Failure Chain
```
Document uploaded/ingested into the RAG knowledge store without
a mandatory currency check, deduplication or assigned owner
  ↓ (IRQ-DAT-007 — THIS IRQ: no curation gate at ingestion)
Superseded document persists in the index alongside (or instead of)
the current version
  ↓ (IRQ-DAT-008: no precedence/conflict-resolution mechanism disambiguates)
Retriever scores the stale document as relevant for a user query
  ↓ (IRQ-SEC-003: application treats retrieved content as trusted
     without currency verification)
Model generates a response grounded in stale policy, presented
with the same confidence as current guidance
  ↓
Customer receives wrong advice/decision → complaint → FOS/regulatory
finding that the decision was not supported by current evidence

Control Breakpoints:
  • IRQ-DAT-007: curation gate at ingestion (currency check, dedup, owner assignment)
  • IRQ-DAT-008: precedence/conflict resolution for competing documents
  • IRQ-SEC-003: retrieved content treated as data requiring currency verification, not blind trust
```

## 7. Why a Domain Expert May Miss It
- Document management SMEs think in terms of the authoritative document repository (e.g. the policy intranet), not realising the RAG index is a separate, potentially unsynchronised copy that can silently diverge.
- "We uploaded the current policy" is a point-in-time action; without an ongoing currency-check mechanism, the index does not know when that policy is superseded.
- Deduplication failures (the same policy uploaded twice, once current and once from an old backup) are an IT hygiene issue rarely considered a customer-harm risk.
- The assumption that "the model would know" if content were stale is false — retrieval and generation have no inherent temporal awareness of supersession.

## 8. Assurance Objective
**AO-DAT-007:** All content entering the RAG knowledge store shall pass curation controls — currency verification, deduplication and an assigned content owner — before being retrievable, such that stale or superseded content cannot be presented as current.

## 9. Expected Controls (Traced)
- **Mandatory currency check and content-owner assignment at ingestion** — [NIST AI RMF 1.0, MAP function; general document-lifecycle governance practice] — no document enters the retrievable index without a named owner and a review/expiry date.
- **Automated deduplication and version-supersession detection** — [Barnett et al., 2024, "Seven Failure Points When Engineering a RAG System", arXiv:2401.05856] — duplicate or superseded document versions are detected and the superseded copy removed or flagged.
- **Scheduled re-verification of indexed content currency** — [linked IRQ-DAT-012 retrieval drift] — indexed documents are periodically re-checked against the authoritative source repository, not assumed static.
- **Faithfulness/grounding evaluation of retrieval outputs** — [Es et al., 2023, "RAGAS: Automated Evaluation of RAG", arXiv:2309.15217; Magesh et al., 2024, "Hallucination-Free? Assessing the Reliability of Leading AI Legal Research Tools"] — periodic testing confirms retrieved and generated content reflects the current authoritative source.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "our knowledge base is kept up to date" with no process detail — **L1**.
- Ingestion pipeline documentation showing (or not showing) a currency-check and ownership-assignment step — **L2**.
- Code/config inspection confirming the currency check and deduplication logic actually execute before a document becomes retrievable — **L3**.
- Staging test results: a deliberately stale document injected alongside its current replacement; retrieval outcome measured — **L3**.
- Independent audit of the knowledge-store governance process, including a sample document-currency reconciliation against the authoritative source repository — **L4**.
- Production monitoring: count and resolution of stale-content flags raised over a defined period — **L5**.

## 11. Independent Test
> In a non-production replica of the RAG knowledge store, seed a superseded policy/product-terms document alongside its current replacement (both present, as would occur from an incomplete update). Run representative customer-facing queries and measure: (1) whether the retriever surfaces the stale document, the current document, or both without disambiguation; (2) whether the generated response reflects stale or current terms; (3) whether any currency/ownership metadata would have flagged the stale document had the ingestion control been active. Methodology follows the RAG failure-point taxonomy of Barnett et al. (2024) and RAGAS-style faithfulness evaluation (Es et al., 2023). No production data or systems used. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (RAG failure-point taxonomies and faithfulness-evaluation tooling are published and used by multiple independent groups; no single canonical "currency-check adequacy" benchmark exists for FS knowledge stores, keeping this short of ★4).

## 12. Pass Indicators
- No document in the knowledge store lacks a currency check, owner and review date.
- Staging test: stale documents are either excluded from the index or clearly flagged/deprioritised versus their current replacement in retrieval and generation.
- Deduplication catches duplicate/superseded uploads before they become independently retrievable.
- Periodic reconciliation against the authoritative source repository finds no undetected divergence.

## 13. Fail Indicators
- Documents are retrievable with no owner, review date or currency metadata.
- Staging test shows a stale document retrieved and presented as current, with the generated response reflecting superseded terms.
- No deduplication mechanism exists; the same policy exists in multiple, potentially divergent versions in the index.
- No scheduled reconciliation against the source repository; drift between the two is discovered only via complaint or incident.

## 14. Reporting Language
**Pass:** "All content in the [system] knowledge store passes a currency check, deduplication and owner-assignment gate before becoming retrievable. Staging testing confirmed that a seeded stale document was correctly excluded/deprioritised in favour of its current replacement across the query set tested (★3 methodology)."

**Fail:** "Staging testing demonstrated that a superseded policy document, present alongside its current replacement in the knowledge store, was retrieved and presented as current in [x]% of test queries, with the generated response reflecting withdrawn terms. No currency check or content ownership gate exists at ingestion. This is a direct, demonstrated path to customers receiving advice or decisions based on stale policy and requires remediation before continued reliance."

**Partial:** "Currency checking is applied to the primary policy document set but not to product-terms documents ingested via [secondary path], which constitute [x]% of the knowledge store. The assurance objective is not met until coverage is equivalent across all content types."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (customers receive advice/decisions on stale terms; Consumer Duty and
              contractual exposure across affected interactions)
  Likelihood: 2 (plausible where a document update process misses the deduplication/removal
                 step, which is a common operational lapse)
  Detectability: 2 (detected via periodic reconciliation audit or customer complaint,
                    typically within days-weeks)
  Recoverability: 2 (correctable via index remediation and affected-interaction review)
  Novelty: 3 (document-lifecycle SMEs understand version control but not that the RAG index
              is a separate, potentially divergent copy of the authoritative repository)

If controls are absent or degraded:
  Severity: 3 (systematic stale-content exposure across all interactions touching the
              affected document, potentially large volume)
  Likelihood: 3 (uncurated ingestion is a foreseeable default absent explicit process design)
  Detectability: 3 (silent until a complaint or targeted audit surfaces the divergence)
  Recoverability: 2 (correctable once identified via index remediation)
  Novelty: 3
Residual risk: material and cumulative; scales with knowledge-store size and update frequency.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Customers receive advice or decisions grounded in withdrawn policy/terms; Consumer Duty and contractual exposure. |
| **Likelihood** | 2 | Plausible given uncurated ingestion is a common operational default absent explicit design. |
| **Detectability** | 2 | Surfaces via periodic reconciliation or complaint, typically within days to weeks. |
| **Recoverability** | 2 | Correctable via index remediation and review of affected interactions. |
| **Novelty** | 3 | Document-lifecycle SMEs rarely realise the RAG index is a separate, silently divergent copy of the authoritative source. |

## 17. Regulatory Basis
> [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] requires customer communications and decisions to be supported by accurate, current information; stale-policy retrieval is a direct foreseeable-harm risk under this outcome. [PRA SS1/23, Principle 3 (development/use) and Principle 4 (ongoing validation)] data-governance expectations extend to grounding-data currency for models influencing customer outcomes. No regulation names RAG currency-checking explicitly. [UNVERIFIED — no further pinpoint exists; the mechanism is genuinely unaddressed by name in the cited sources] (verified 29 Jul 2026).

## 18. Research Basis
> [Barnett, S., et al., 2024, "Seven Failure Points When Engineering a RAG System", arXiv:2401.05856] — empirical failure-point taxonomy including stale/conflicting-document retrieval, directly informing the control set above. [Es, S., et al., 2023, "RAGAS: Automated Evaluation of RAG", arXiv:2309.15217] — reference-free faithfulness/relevance metrics usable for currency-grounding evaluation. [Magesh, V., et al., 2024, "Hallucination-Free? Assessing the Reliability of Leading AI Legal Research Tools", arXiv:2405.20362] — evidence that commercial RAG tools still hallucinate at material rates (between 17% and 33% of the time) even where vendors claim otherwise. [Friel, R., Belyi, M., Sanyal, A., 2024 (latest version January 2025), "RAGBench: Explainable Benchmark for Retrieval-Augmented Generation Systems", arXiv:2407.11005] — a 100,000-example benchmark spanning five industry domains including finance (FinQA, TAT-QA), whose TRACe framework makes retrieval quality separately measurable from generation quality: context Relevance isolates whether the retriever surfaced the right material at all, giving the ingestion-curation question a quantitative downstream check — poorly curated or stale corpora manifest as measurably degraded Relevance and Adherence rather than as an undetectable narrative problem. This lets the test score the retrieval layer with an explainable, published metric set instead of ad-hoc spot checks; the finance component (FinQA/TAT-QA-style tabular-plus-text reasoning) lets the tester exercise the corpus on document shapes resembling FS content. RAGBench is an academic benchmark, not FS-certified; no ★ change follows from this addition.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-008 (A.3: conflicting-document precedence and retrieval determinism)
  - IRQ-DAT-012 (A.5: retrieval/embedding/document drift — ongoing currency decay)
  - IRQ-SEC-003 (E.1: retrieved content trust boundary — application-layer verification)
  - IRQ-MOD-005 (B.2: behavioural distinction of conflicting/missing evidence)
```

## 20. References
```
[1] Barnett, S., et al., 2024. "Seven Failure Points When Engineering a RAG System." arXiv:2401.05856.
[2] Es, S., James, J., Espinosa-Anke, L., Schockaert, S., 2023. "RAGAS: Automated Evaluation
    of Retrieval Augmented Generation." arXiv:2309.15217.
[3] Magesh, V., et al., 2024. "Hallucination-Free? Assessing the Reliability of Leading AI
    Legal Research Tools." arXiv:2405.20362.
[4] FCA, 2022. "PS22/9: A New Consumer Duty" and "FG22/5." PRIN 2A in force 31 July 2023.
[5] PRA, 2023. "SS1/23 — Model risk management principles for banks." May 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.3 (Data domain, Retrieval Data)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Document-lifecycle SMEs manage the authoritative repository but
  rarely realise the RAG index is a separate, silently divergent copy.
✓ Test 2 (Plausible Harm): Grounded in Barnett et al. (2024) RAG failure-point taxonomy and
  Magesh et al. (2024) real-world commercial-tool failure rates.
✓ Test 3 (Testable): Seeded stale-document injection testing is executable in non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates whether a knowledge store may support customer-facing
  advice without a curation gate.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

