# CANVAS: IRQ-DAT-009

## 1. IRQ ID & Title
**IRQ-DAT-009: Retrieval Surfacing Documents Beyond the User's Entitlements**

Register question: "Does retrieval respect the firm's entitlement model, or can the system surface documents to users or agents lacking the underlying access rights?"

## 2. Business Activities Affected
- **Cross-team knowledge assistants:** A single shared knowledge store spanning multiple business lines (retail, wealth, commercial) risks surfacing content a given user's role does not entitle them to see.
- **Customer-facing assistants grounded on internal documents:** Customer-facing retrieval must never surface internal-only content (e.g. fraud-detection rules, internal risk scores) even if semantically relevant to the customer's question.
- **Agent-mediated workflows with delegated retrieval:** Where an agent retrieves on behalf of a human or another agent, entitlement must follow the ultimate requester, not the agent's own broader access.

## 3. AI Behaviour(s)
- Retrieves documents based on semantic relevance to a query, with entitlement enforcement — if it exists — implemented as a separate layer the retrieval mechanism itself has no inherent awareness of.
- Generates responses synthesising retrieved content without independently verifying the requesting user was entitled to see every source it drew upon.
- In agentic settings, may retrieve using the agent's own (often broader) credentials rather than the credentials of the human or process on whose behalf it is acting.

## 4. Failure Mode
> Retrieval does not enforce the firm's document-level entitlement model at retrieval time, so a user, customer or agent can be surfaced content — directly or synthesised into a generated response — that they lack the underlying access rights to see.

## 5. Potential Consequences
- **Customer:** Exposure to another customer's data, or to internal-only content (e.g. fraud scoring criteria) that undermines control effectiveness if disclosed.
- **Institution:** Confidentiality breach; if internal risk/fraud logic is disclosed, control circumvention becomes easier for bad actors; regulatory notification obligations may be triggered.
- **Regulator:** UK GDPR Art. 32 security-of-processing breach; potential market-abuse implications if retrieval crosses information-barrier boundaries (e.g. wealth/corporate advisory).

## 6. Failure Chain
```
Documents from multiple entitlement domains (business lines, customer
records, internal-only content) are indexed into a shared or
inadequately segmented knowledge store
  ↓ (IRQ-DAT-009 — THIS IRQ: retrieval-time entitlement enforcement absent or incomplete)
Retriever scores and returns documents purely on semantic relevance,
unaware of the requester's actual entitlements
  ↓ (IRQ-AGT-004: in agentic settings, the agent's own broader credentials
     are used rather than the delegator's)
Retrieved content — directly or synthesised — reaches a user or
customer lacking the underlying access right
  ↓
Confidentiality breach, information-barrier crossing, or customer
data exposure → regulatory notification, reputational damage, and
(where internal control logic is disclosed) weakened control effectiveness

Control Breakpoints:
  • IRQ-DAT-009: document-level ACL enforcement at retrieval time
  • IRQ-AGT-004: agent retrieval acts under the delegator's entitlement, not its own
  • IRQ-SEC-008: data-flow mapping confirms no uncontrolled egress via retrieval
```

## 7. Why a Domain Expert May Miss It
- Information-security SMEs think of access control at the system/application level (who can log in) not at the retrieval-scoring level (which specific document a query happens to surface).
- A knowledge store "behind the firewall" is assumed safe by virtue of network perimeter, even though the actual risk is document-level entitlement within an authenticated user base spanning multiple business lines.
- Semantic retrieval is a black box to most SMEs; the idea that a cleverly phrased query could surface a document the retriever "shouldn't" return is not intuitive without security testing specifically targeting this.
- Agentic delegation (an agent retrieving on a human's behalf) introduces a credential-substitution risk that traditional access-review processes, built around individual human logins, do not naturally cover.

## 8. Assurance Objective
**AO-DAT-009:** Retrieval shall enforce the firm's document-level entitlement model at query time, such that no user, customer or agent can be surfaced content — directly or synthesised into a generated response — beyond their underlying access rights.

## 9. Expected Controls (Traced)
- **Document-level access control lists enforced at retrieval time** — [OWASP Top 10 for LLM Applications 2025, vector/embedding weaknesses and access-control guidance] — retrieval queries are filtered by the requester's entitlements before scoring/ranking, not after.
- **Entitlement-aware indexing (not just post-hoc filtering)** — [ISO/IEC 27001 access-control practice, as applied to vector/embedding stores] — the index itself is partitioned or tagged by entitlement domain to prevent scoring leakage even at the ranking stage.
- **Delegated-retrieval entitlement propagation for agents** — [linked IRQ-AGT-004; OWASP Agentic Security Initiative, Feb 2025] — agents retrieving on behalf of a human or process use the delegator's entitlement, not their own broader access.
- **Pre-production and periodic entitlement-boundary testing** — [OWASP Top 10 for LLM Applications 2025, LLM08:2025 Vector and Embedding Weaknesses, permission and access control guidance] — adversarial testing specifically targets whether crafted queries can surface out-of-entitlement content.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the knowledge base is behind our firewall" with no document-level ACL detail — **L1**.
- Architecture documentation describing entitlement enforcement at retrieval time (or its absence) — **L2**.
- Code/config inspection confirming entitlement filtering is applied pre-retrieval/pre-ranking, not merely post-hoc display filtering — **L3**.
- Staging test results: adversarial queries crafted by a user with limited entitlement, attempting to surface out-of-scope content; success rate measured — **L3**.
- Independent security assessment of the retrieval entitlement model, including agentic delegation paths — **L4**.
- Production access logs showing entitlement-denial events over a defined period, with investigation of any anomalies — **L5**.

## 11. Independent Test
> In a non-production replica of the knowledge store, populate it with documents spanning at least two entitlement domains (e.g. retail-only and wealth-only content, or customer-A-only and customer-B-only records). Using accounts with defined, limited entitlements, issue a representative and adversarially-crafted query set (including paraphrase and indirect-reference attempts) designed to surface out-of-entitlement content. Separately, test an agentic delegation path to confirm the agent's retrieval respects the delegating user's entitlement rather than its own service credentials. Measure any successful entitlement-boundary crossing. Methodology draws on OWASP Top 10 for LLM Applications 2025 control guidance (LLM08:2025 Vector and Embedding Weaknesses; under review, URO-6, REGISTER_STATS.md) and OWASP Agentic Security Initiative (Feb 2025) delegation-risk guidance. No real customer data used. — **★3 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (OWASP guidance is published and increasingly standardised; agentic-delegation testing specifically is newer (2025) and less battle-tested across institutions, keeping this at ★3 rather than ★4).

## 12. Pass Indicators
- Zero successful entitlement-boundary crossings across the adversarial query set in staging testing, for both direct human queries and agentic delegation paths.
- Entitlement filtering is confirmed applied pre-retrieval/pre-ranking, not as a display-layer afterthought.
- Production access logs show entitlement-denial events are logged and periodically reviewed.
- Entitlement-boundary testing is repeated on knowledge-store schema changes and agentic tool/permission changes.

## 13. Fail Indicators
- Any adversarial query in staging testing successfully surfaces out-of-entitlement content.
- Entitlement enforcement exists only as a post-generation display filter, with the underlying retrieval/ranking having already processed the out-of-scope document.
- Agentic delegation paths use the agent's own broader credentials rather than the delegating user's entitlement.
- No entitlement-boundary testing has been performed since the last significant schema or permission change.

## 14. Reporting Language
**Pass:** "Adversarial entitlement-boundary testing across [n] queries, including agentic delegation paths, found zero successful crossings of the firm's document-level entitlement model. Filtering is confirmed applied at the pre-retrieval stage, not as a display-layer afterthought (★3 methodology)."

**Fail:** "Adversarial testing successfully surfaced out-of-entitlement content in [x] of [n] test queries, and the agentic delegation path was found to retrieve using the agent's own broader service credentials rather than the delegating user's entitlement. This is a demonstrated confidentiality-breach vector requiring remediation before continued reliance on the shared knowledge store."

**Partial:** "Entitlement enforcement is effective for direct human queries but has not been extended to the agentic delegation path, which accounts for [x]% of retrieval volume. The assurance objective is not met until delegation-path enforcement is verified."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (confidentiality breach affecting one or more customers/business lines;
              regulatory notification risk)
  Likelihood: 2 (plausible where entitlement enforcement is display-layer only, a common
                 architectural shortcut)
  Detectability: 2 (adversarial testing and access-log review surface this within a test
                    cycle; not real-time by default)
  Recoverability: 2 (remediable via retrieval-layer entitlement fix; affected disclosures
                     require individual assessment)
  Novelty: 3 (document-level entitlement-at-retrieval-time, and agentic credential
              substitution specifically, are AI-architecture-specific risks)

If controls are absent or degraded:
  Severity: 4 (systematic cross-business-line or cross-customer data exposure; potential
              information-barrier/market-abuse implications)
  Likelihood: 3 (display-layer-only filtering is a foreseeable default absent explicit
                 pre-retrieval enforcement design)
  Detectability: 4 (silent — retrieval "succeeds" and the leak is invisible without
                    deliberate adversarial testing)
  Recoverability: 3 (breach notification, forensic review of all affected interactions,
                     potential regulatory engagement)
  Novelty: 3
Residual risk: material to critical depending on the sensitivity of cross-domain content
in the shared knowledge store.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Confidentiality breach affecting one or more customers/business lines; regulatory notification risk. |
| **Likelihood** | 2 | Plausible where entitlement enforcement is a display-layer-only shortcut, a common architectural pattern. |
| **Detectability** | 3 | Requires deliberate adversarial testing; a successful leak is otherwise invisible (retrieval "succeeds" normally). |
| **Recoverability** | 2 | Remediable via retrieval-layer fix; affected-disclosure assessment adds complexity but is bounded. |
| **Novelty** | 3 | Document-level entitlement-at-retrieval and agentic credential substitution are AI-architecture-specific risks outside traditional access-review scope. |

## 17. Regulatory Basis
> [UK GDPR Art. 32(1)(b), security of processing] requires appropriate technical measures to prevent unauthorised access to personal data; retrieval-time entitlement failure is a direct security-of-processing gap. [FCA information-barrier expectations, SYSC 10 (conflicts of interest) and general SYSC 3/6 systems-and-controls requirements] apply where cross-business-line retrieval could cross established information barriers. No regulation names RAG entitlement enforcement explicitly. [UNVERIFIED — no further pinpoint exists; mechanism genuinely unaddressed by name] (verified 29 Jul 2026).

## 18. Research Basis
> [OWASP, 2025, "Top 10 for LLM Applications 2025", vector and embedding weaknesses entry] — names inadequate access control on retrieval/embedding stores as a recognised LLM application risk. [OWASP Agentic Security Initiative, "Agentic AI: Threats and Mitigations", v1.0, Feb 2025 — the edition consulted; the list stands at v1.1, December 2025 (T16–T17 added, T1–T15 carried) as at 12 September 2026, and no entry is cited here by number, so the citation is unaffected] — first structured threat model covering agentic delegation and credential-substitution risk, directly applicable to the agent-retrieval failure mode described here.
>
> **Research basis last reviewed:** 12 September 2026 · **review cadence:** Standard (12 months)
>
> **URO-6: OWASP Top 10 for LLM Applications 2025 — whether §11's ★3 and the method class hold once the OWASP limb is read as control guidance (LLM08:2025) rather than a test method, which the 2025 list does not name (LLM01:2025 asks for penetration testing of access controls without giving a method) — resolve by 2027-04-03.** The ★3 above stands untouched while this observation is open (§6A.2).

## 19. Related IRQs
```
  - IRQ-SEC-008 (E.2: confidential data egress via prompts/context/logs — the general leakage control)
  - IRQ-AGT-004 (C.2: composite-action/permission-chaining risk — the agentic-delegation variant)
  - IRQ-SEC-011 (E.4: non-human identity and credential scoping — the technical credential-substitution root cause)
  - IRQ-DAT-010 (A.4: memory scoping — the parallel entitlement concern for persisted memory)
```

## 20. References
```
[1] OWASP Foundation, 2025. "OWASP Top 10 for LLM Applications 2025." Vector and Embedding
    Weaknesses entry. Published November 2024 for 2025.
[2] OWASP GenAI Security Project, 2025. "Agentic AI: Threats and Mitigations." v1.0, February 2025.
[3] UK Government, 2018/2021. "UK GDPR." Article 32.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.3 (Data domain, Retrieval Data)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): InfoSec SMEs think in perimeter/login terms, not document-level
  entitlement at the retrieval-scoring layer; agentic credential substitution is a further
  step removed.
✓ Test 2 (Plausible Harm): Grounded in OWASP Top 10 for LLM Applications 2025 (vector/
  embedding weaknesses) and OWASP Agentic Security Initiative (Feb 2025).
✓ Test 3 (Testable): Adversarial entitlement-boundary testing, incl. agentic delegation, is
  executable in non-production. ★3.
✓ Test 4 (Decision-Relevant): Gates whether a shared multi-domain knowledge store may support
  cross-business-line or customer-facing retrieval.

Change Log:
- v1.0 (2026-07): Initial publication.
- v1.2.0 (2026-09-12): Research Basis — the OWASP Agentic Security Initiative "Agentic AI: Threats and Mitigations" citation gains a dated currency note: v1.0, Feb 2025 is the edition consulted, the list stands at v1.1, December 2025 (T16–T17 added, T1–T15 carried) as at 12 September 2026, and no entry is cited here by number, so the citation is unaffected. No change to controls, test, ★ or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; field 18 — URO-6 opened, resolve by 2027-04-03; the ★3 and the risk profile unchanged.
```

---
---

