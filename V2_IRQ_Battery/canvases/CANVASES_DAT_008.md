# CANVAS: IRQ-DAT-008

## 1. IRQ ID & Title
**IRQ-DAT-008: Non-Deterministic Retrieval Across Conflicting Documents**

Register question: "Where the knowledge store contains conflicting documents (superseded policies, divergent product terms), is retrieval behaviour deterministic and precedence-controlled rather than arbitrary?"

## 2. Business Activities Affected
- **Multi-jurisdiction or multi-brand product assistants:** Where the same product exists under divergent regional or brand-specific terms, retrieval must consistently surface the applicable version, not an arbitrary one.
- **Claims handling with historical and current policy wordings:** A claim governed by a historical policy wording alongside the current wording requires deterministic selection of the applicable document, not arbitrary retrieval.
- **Internal compliance assistants:** Draft, consulted-on and final versions of the same guidance may coexist; arbitrary retrieval risks surfacing an unapproved draft as authoritative.

## 3. AI Behaviour(s)
- Retrieves the top-k most semantically similar documents to a query, ranked by an embedding-similarity or hybrid scoring mechanism that has no inherent concept of document precedence or authority.
- When multiple conflicting documents score similarly, retrieval order/selection can vary between runs, sessions or minor query rephrasing (non-determinism from ties, index updates, or model/embedding version changes).
- Synthesises or selects from whichever document(s) the retriever returns, without independently resolving the conflict.

## 4. Failure Mode
> Where the knowledge store contains conflicting documents, retrieval behaviour is non-deterministic and lacks a precedence rule, so which version of the truth the system surfaces to a given user depends on retrieval arbitrariness rather than a controlled, auditable resolution of the conflict.

## 5. Potential Consequences
- **Customer:** Two customers asking materially the same question receive different, potentially contradictory answers, both presented with equal confidence.
- **Institution:** Inconsistent treatment across customers is itself a fair-treatment issue, independent of which specific answer was wrong; audit cannot explain why a given answer was given without reconstructing the exact retrieval state at that moment.
- **Regulator:** Consumer Duty consistency-of-outcome concerns; inability to reconstruct why a specific answer was given undermines accountability (IRQ-GOV-010 record-keeping).

## 6. Failure Chain
```
Conflicting documents (superseded/current, draft/final, regional
variants) coexist in the knowledge store
  ↓ (IRQ-DAT-007: curation did not resolve or flag the conflict at ingestion)
No precedence rule or conflict-resolution logic exists in the
retrieval/ranking layer
  ↓ (IRQ-DAT-008 — THIS IRQ: retrieval selection is arbitrary/non-deterministic)
Different users (or the same user on different occasions) receive
different answers to materially the same question
  ↓ (IRQ-GOV-010: no record captures which document version was
     actually used for a given decision)
Inconsistent treatment discovered via complaint pattern or audit;
cannot be explained or defended without full retrieval-state
reconstruction
  ↓
Fair-treatment finding; loss of confidence in the system's answers

Control Breakpoints:
  • IRQ-DAT-007: curation resolves/flags conflicts at ingestion
  • IRQ-DAT-008: explicit precedence rule and deterministic tie-breaking in retrieval
  • IRQ-GOV-010: retrieval state (which document version) logged per interaction
```

## 7. Why a Domain Expert May Miss It
- Traditional document management assumes a single authoritative current version exists at any time; the possibility of multiple valid-looking versions simultaneously retrievable, with no precedence logic, is architecturally specific to RAG.
- "The system retrieved the most relevant document" sounds like a quality statement; it says nothing about whether "most relevant" tracks "authoritative" when several documents are near-tied in similarity score.
- Non-determinism from embedding-model updates, index rebuilds or infrastructure-level tie-breaking is invisible without deliberately re-running the same query multiple times or across sessions.
- Compliance SMEs reviewing a single transcript see one plausible answer and have no natural trigger to ask "would this have been different for another customer asking the same thing?"

## 8. Assurance Objective
**AO-DAT-008:** Where the knowledge store contains conflicting documents, retrieval behaviour shall be deterministic and governed by an explicit, auditable precedence rule, such that materially identical queries receive consistent, defensible answers.

## 9. Expected Controls (Traced)
- **Explicit precedence metadata and conflict-resolution logic** — [Barnett et al., 2024, "Seven Failure Points When Engineering a RAG System"] — documents carry precedence metadata (current/superseded, jurisdiction, approval status) consulted by the retrieval layer, not left to similarity score alone.
- **Deterministic tie-breaking in the retrieval/ranking pipeline** — [Chen et al., 2023, "Benchmarking Large Language Models in Retrieval-Augmented Generation" (RGB), arXiv:2309.01431, negative-rejection and counterfactual-robustness testing] — retrieval configuration is version-pinned and reproducible for a given index state, and conflicts are resolved by rule rather than arbitrary rank.
- **Consistency testing across repeated and rephrased queries** — [Wu, K., et al., 2024, "ClashEval", arXiv:2404.10198, tug-of-war between an LLM's internal prior and external evidence] — periodic testing confirms the same underlying question yields consistent answers regardless of phrasing or session.
- **Retrieval-state logging per interaction** — [linked IRQ-GOV-010] — the specific document version(s) retrieved and used are logged, enabling reconstruction of why a given answer was produced.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the system retrieves the most relevant document" with no precedence-rule detail — **L1**.
- Retrieval architecture documentation describing (or not describing) precedence metadata and conflict-resolution logic — **L2**.
- Code/config inspection confirming precedence rules are actually consulted, not just documented — **L3**.
- Staging test results: repeated and rephrased queries against a knowledge store seeded with known conflicting documents; consistency rate measured — **L3**.
- Independent audit of retrieval-state logs for a sample of production-representative interactions, confirming reconstructability — **L4**.
- Production monitoring: complaint or audit findings of inconsistent answers to materially similar queries, with root-cause analysis — **L5**.

## 11. Independent Test
> In a non-production replica of the knowledge store, seed deliberately conflicting document pairs (superseded/current, draft/final, regional variant A/B) with near-tied similarity scores against a representative query set. Run each query multiple times, with minor rephrasing, and across simulated separate sessions. Measure: (1) consistency rate of which document is retrieved/used; (2) whether a precedence rule, where one exists, is actually applied to resolve the tie deterministically; (3) whether retrieval-state logs would allow reconstruction of which document informed a given answer. Methodology draws on RGB negative-rejection/counterfactual-robustness testing (Chen et al., 2023) and ClashEval-style prior-vs-evidence analysis (Wu et al., 2024). No production data used. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (RAG robustness benchmarking methods are published and used by multiple research groups; no single canonical "precedence-determinism" benchmark exists for FS document conflict resolution, keeping this short of ★4).

## 12. Pass Indicators
- Repeated/rephrased queries against known conflicting-document pairs return consistent, precedence-rule-compliant answers in staging testing.
- Precedence metadata exists and is demonstrably consulted by the retrieval pipeline, not merely present in documentation.
- Retrieval-state logs allow full reconstruction of which document version informed a sampled set of production-representative interactions.
- No unresolved conflicting-document pairs exist in the live knowledge store without an assigned precedence rule.

## 13. Fail Indicators
- Staging testing shows the same or rephrased query returns different, conflicting answers across repeated runs.
- No precedence metadata or conflict-resolution logic exists; retrieval relies solely on similarity score.
- Retrieval-state logs do not capture which document version was used, preventing reconstruction of a given answer.
- Known conflicting documents (draft/final, superseded/current) coexist in the live index with no resolution mechanism.

## 14. Reporting Language
**Pass:** "Staging testing of deliberately conflicting document pairs found retrieval behaviour deterministic and precedence-rule-compliant across [x] repeated and rephrased query variants. Retrieval-state logging allows reconstruction of which document informed each sampled interaction (★3 methodology)."

**Fail:** "Staging testing found that repeated and rephrased instances of the same underlying query returned inconsistent, conflicting answers in [x]% of cases, with no precedence rule governing which document version was used. Retrieval-state logs do not capture which document informed a given answer, meaning inconsistent treatment cannot be explained or defended after the fact. This represents a fair-treatment and accountability gap requiring remediation."

**Partial:** "Precedence rules are applied and effective for the primary policy document set but not for regional product-terms variants, which showed [x]% inconsistency in staging testing. Extend precedence logic and logging before the assurance objective is met."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (inconsistent but individually plausible answers; correctable via targeted
              customer follow-up once identified)
  Likelihood: 2 (plausible wherever multiple valid-looking document versions coexist, which
                 is common in multi-jurisdiction/multi-brand estates)
  Detectability: 3 (requires deliberate repeated/rephrased query testing to surface;
                    invisible in single-transcript review)
  Recoverability: 2 (correctable via precedence-rule implementation and logging retrofit)
  Novelty: 3 (the concept of a "most relevant" retrieval producing arbitrary rather than
              authoritative selection is specific to RAG architecture)

If controls are absent or degraded:
  Severity: 3 (systematic inconsistent treatment across the customer base, undermining
              fair-treatment obligations even before considering which answer is "wrong")
  Likelihood: 3 (foreseeable wherever conflicting documents are not actively curated)
  Detectability: 4 (invisible without deliberate consistency testing; standard QA review of
                    single transcripts would not surface it)
  Recoverability: 2 (correctable once identified, but historical inconsistency may be
                     unreconstructable without retrieval-state logs)
  Novelty: 3
Residual risk: moderate-to-material, compounding with IRQ-DAT-007; primarily a fair-treatment
and accountability risk rather than a single catastrophic-harm risk.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Systematic inconsistent treatment across the customer base is a fair-treatment issue independent of individual answer correctness. |
| **Likelihood** | 2 | Plausible wherever multiple valid-looking document versions coexist, common in multi-jurisdiction/multi-brand estates. |
| **Detectability** | 3 | Requires deliberate repeated/rephrased consistency testing; invisible in standard single-transcript QA review. |
| **Recoverability** | 2 | Correctable via precedence-rule implementation and logging retrofit once identified. |
| **Novelty** | 3 | "Most relevant" producing arbitrary rather than authoritative selection is an architecture-specific RAG behaviour. |

## 17. Regulatory Basis
> [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] fair-treatment and consistency-of-outcome expectations are engaged where materially similar customers receive materially different treatment without a defensible reason. [PRA SS1/23, Principle 2 (governance) and documentation expectations under Principle 4] require decisions to be reconstructable. No regulation names RAG retrieval determinism explicitly. [UNVERIFIED — no further pinpoint exists; mechanism genuinely unaddressed by name] (verified 29 Jul 2026).

## 18. Research Basis
> [Barnett, S., et al., 2024, "Seven Failure Points When Engineering a RAG System", arXiv:2401.05856] — names conflicting-document retrieval as a documented empirical failure point. [Chen, J., et al., 2023, "Benchmarking Large Language Models in Retrieval-Augmented Generation" (RGB), arXiv:2309.01431] — tests negative-rejection and counterfactual robustness, directly applicable to conflict-resolution testing. [Wu, K., et al., 2024, "ClashEval" on faithfulness under conflicting evidence, arXiv:2404.10198] — quantifies the tug-of-war between retrieved evidence and model prior, relevant to predicting which conflicting document "wins." [Friel, R., Belyi, M., Sanyal, A., 2024 (latest version January 2025), "RAGBench: Explainable Benchmark for Retrieval-Augmented Generation Systems", arXiv:2407.11005] — its TRACe framework separates context Relevance from context Utilization, allowing a reviewer to observe not just what was retrieved when conflicting documents exist but which retrieved passages the generator actually used in the answer, converting the precedence question from output inspection ("did the answer cite the current policy?") into a measurable utilisation profile across superseded and current documents. This lets the test build conflicting-document test sets and measure Utilization split across the conflict pair, evidencing whether precedence control operates in the generator as well as the retriever — previously only retrieval-rank evidence was practically obtainable. RAGBench is an academic benchmark, not FS-certified; no ★ change follows from this addition.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-DAT-007 (A.3: curation at ingestion — upstream conflict-prevention control)
  - IRQ-MOD-005 (B.2: behavioural distinction of conflicting evidence — the generation-layer counterpart)
  - IRQ-GOV-010 (I.4: record-keeping/reconstruction of AI-influenced decisions)
  - IRQ-CON-005 (H.2: fair-access/consistency-of-outcome — the conduct-facing consequence)
```

## 20. References
```
[1] Barnett, S., et al., 2024. "Seven Failure Points When Engineering a RAG System." arXiv:2401.05856.
[2] Chen, J., et al., 2023. "Benchmarking Large Language Models in Retrieval-Augmented
    Generation." arXiv:2309.01431.
[3] Wu, K., et al., 2024. "ClashEval: Quantifying the tug-of-war between an LLM's internal prior and external evidence" arXiv:2404.10198.
[4] FCA, 2022. "PS22/9: A New Consumer Duty" and "FG22/5." PRIN 2A in force 31 July 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.3 (Data domain, Retrieval Data)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Traditional document management assumes a single current version;
  simultaneous retrievability of near-tied conflicting documents is RAG-specific.
✓ Test 2 (Plausible Harm): Documented as an empirical failure point (Barnett et al., 2024)
  with directly applicable robustness-testing methods (Chen et al., 2023; Wu et al., 2024).
✓ Test 3 (Testable): Repeated/rephrased query consistency testing is executable in
  non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates whether a knowledge store with known conflicting content
  may support customer-facing use without precedence logic.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

