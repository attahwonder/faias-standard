# CANVAS: IRQ-DAT-010

## 1. IRQ ID & Title
**IRQ-DAT-010: Ungoverned Persisted Memory and Conversation Stores**

Register question: "Are persisted memory and conversation stores governed as data assets — scoped per user/tenant with tested separation, retention schedules, obsolescence review and verifiable deletion (including DSAR erasure)?"

## 2. Business Activities Affected
- **Relationship-manager and advisory copilots with persistent memory:** Systems that remember prior interactions with a customer to personalise service depend on that memory being correctly scoped and not bleeding across customers or advisors.
- **Multi-tenant customer service platforms:** Where the same underlying system serves multiple business lines or even multiple client firms, memory-store tenant isolation is a hard confidentiality requirement.
- **Complaint and DSAR handling:** A customer's right-to-erasure request must be capable of removing their data from persisted memory stores, not only from primary case-management systems.

## 3. AI Behaviour(s)
- Writes conversational or interaction context to a persisted memory store to inform future interactions, without inherent scoping discipline beyond whatever the application layer enforces.
- Retrieves from memory to personalise or contextualise future outputs, treating stored memory as trusted input regardless of its age, relevance or continued lawful basis for retention.
- Provides no built-in signal to a human reviewer or DSAR process about which memory records pertain to which data subject.

## 4. Failure Mode
> Persisted memory and conversation stores are not governed as data assets — lacking tested per-user/tenant scoping, defined retention schedules, obsolescence review and verifiable deletion — so customer data can persist beyond its lawful basis, leak across users or tenants, or survive a DSAR erasure request undetected.

## 5. Potential Consequences
- **Customer:** Personal data persists indefinitely without review, or another customer's/advisor's memory context leaks into their interaction; erasure requests are not honoured.
- **Institution:** UK GDPR erasure-obligation breach; cross-tenant data leakage in a multi-client platform is a severe confidentiality and contractual failure.
- **Regulator:** ICO enforcement for unfulfilled DSAR erasure; potential SYSC information-barrier implications if memory bleeds across business lines.

## 6. Failure Chain
```
Conversational/interaction memory is written to a persisted store
without a data-governance framework treating it as a first-class
data asset (owner, retention schedule, scoping rules)
  ↓ (IRQ-DAT-010 — THIS IRQ: memory store ungoverned as a data asset)
Memory persists beyond its lawful retention basis, or scoping
between users/tenants is inadequately tested
  ↓ (IRQ-AGT-008: unvalidated memory also steers future agent
     decisions — the behavioural-influence counterpart)
A DSAR erasure request is received, or a cross-tenant leakage
event occurs
  ↓ (IRQ-GOV-010: no record-keeping mechanism identifies which
     memory records pertain to the affected data subject)
Erasure cannot be verifiably completed, or leaked memory is
discovered by the affected party
  ↓
ICO enforcement / DSAR complaint, or confidentiality breach
→ regulatory and reputational damage

Control Breakpoints:
  • IRQ-DAT-010: memory governed as a data asset (owner, retention, scoping, deletion)
  • IRQ-AGT-008: memory validated before it influences future decisions
  • IRQ-GOV-010: memory records attributable to a specific data subject for DSAR purposes
```

## 7. Why a Domain Expert May Miss It
- Data protection teams are accustomed to governing structured case-management and CRM records; a model's persisted "memory" store is often a newer, less visible data asset that falls outside the standard data-inventory process.
- "It's just conversation history" undersells the sensitivity — memory stores often contain synthesised, inferred or aggregated personal information beyond what was explicitly stated in any single conversation.
- Multi-tenant SaaS-style AI platforms can appear to offer isolation "by design," but tenant separation in a memory/vector store requires the same testing rigour as any other multi-tenant data architecture — an assumption of vendor-provided isolation is not evidence.
- DSAR processes built around primary systems of record may simply not know a memory store exists as a place personal data could be retained.

## 8. Assurance Objective
**AO-DAT-010:** Persisted memory and conversation stores shall be governed as data assets — scoped per user/tenant with tested separation, subject to defined retention schedules and obsolescence review, and capable of verifiable deletion including DSAR erasure.

## 9. Expected Controls (Traced)
- **Memory-store inventory and named ownership** — [UK GDPR Art. 30, records of processing activities] — every persisted memory/conversation store is inventoried with a named owner and documented purpose.
- **Tested per-user/tenant scoping and separation** — [ISO/IEC 27001 access-control and multi-tenancy testing practice] — tenant/user isolation is verified through adversarial testing, not assumed from vendor claims.
- **Defined retention schedule and obsolescence review** — [UK GDPR Art. 5(1)(e), storage limitation] — memory records are retained only as long as necessary and subject to periodic review for continued relevance.
- **Verifiable deletion including DSAR erasure** — [UK GDPR Art. 17, right to erasure] — a technical and procedural mechanism exists to identify and delete a specific data subject's records from memory stores, including any downstream copies or indices.

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "conversation history is stored securely" with no scoping/retention detail — **L1**.
- Memory-store architecture documentation covering scoping, retention and deletion design (or its absence) — **L2**.
- Code/config inspection confirming per-user/tenant scoping logic and deletion mechanisms actually execute — **L3**.
- Staging test results: adversarial cross-tenant/cross-user access attempts against the memory store; a simulated DSAR erasure request traced end-to-end — **L3**.
- Independent audit confirming memory-store governance, including a sample of executed erasure requests verified as complete (including any derived indices/caches) — **L4**.
- Production DSAR fulfilment logs showing memory-store erasure was included and completed within statutory timeframes — **L5**.

## 11. Independent Test
> In a non-production replica of the memory store, populate it with synthetic multi-user, multi-tenant conversational data. (1) Attempt adversarial cross-user and cross-tenant retrieval to test scoping separation. (2) Submit a simulated DSAR erasure request for a synthetic data subject and trace it end-to-end, confirming deletion from the primary memory store and any derived embeddings, caches or backups. (3) Review whether retention/obsolescence review has ever removed stale records absent a specific request. Methodology follows general multi-tenant access-control testing practice (ISO/IEC 27001) and UK GDPR Art. 17 erasure-verification expectations; no published FS-specific benchmark exists for "memory-store erasure completeness." — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (access-control testing methodology is mature, but erasure-completeness verification specifically for AI memory/embedding stores is an emerging, institution-specific test design with no cross-institution benchmark).

## 12. Pass Indicators
- Zero successful cross-user/cross-tenant retrieval in adversarial staging testing.
- Simulated DSAR erasure is traced and confirmed complete across the primary store and all derived indices/embeddings/caches within the firm's target SLA.
- A documented retention schedule exists and obsolescence review has demonstrably removed stale records absent a specific request.
- Memory stores appear in the firm's data inventory with named ownership.

## 13. Fail Indicators
- Adversarial testing successfully retrieves another user's or tenant's memory content.
- Simulated DSAR erasure removes the primary record but leaves the data subject's information recoverable from a derived embedding, cache or backup.
- No retention schedule exists; memory persists indefinitely by default.
- Memory stores are absent from the firm's data inventory and DSAR process scope.

## 14. Reporting Language
**Pass:** "Adversarial cross-tenant/cross-user testing of the memory store found zero successful boundary crossings. A simulated DSAR erasure request was traced end-to-end and confirmed complete across the primary store and derived embeddings/caches within the target SLA (★2 professional assessment given the emerging, institution-specific nature of erasure-completeness testing for AI memory stores)."

**Fail:** "Adversarial testing successfully retrieved another synthetic tenant's memory content, evidencing inadequate scoping. A simulated DSAR erasure request removed the primary conversation record but left the data subject's information recoverable via a derived embedding index, meaning erasure is not currently verifiable end-to-end. This is a direct UK GDPR Art. 17 compliance gap and a confidentiality risk in multi-tenant deployment, requiring urgent remediation."

**Partial:** "Scoping and primary-store erasure are effective, but derived embedding/cache erasure has not been tested or confirmed, affecting [x]% of the memory architecture's storage surface. The assurance objective is not met until end-to-end erasure, including derived stores, is verified."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 3 (unfulfilled erasure obligation or cross-tenant leakage affecting one or more
              data subjects; regulatory notice risk)
  Likelihood: 2 (plausible where derived-index erasure is overlooked, a common technical gap)
  Detectability: 2 (surfaces via periodic DSAR-completeness audit or adversarial testing,
                    within a defined test cycle)
  Recoverability: 2 (remediable via technical fix and completion of outstanding erasures)
  Novelty: 3 (memory stores as a first-class governed data asset, and the derived-index
              erasure gap specifically, are AI-architecture-specific concerns)

If controls are absent or degraded:
  Severity: 4 (systematic unfulfilled erasure obligations across many data subjects, or
              material cross-tenant confidentiality breach in a multi-client platform)
  Likelihood: 3 (memory stores are commonly excluded from legacy DSAR/data-inventory scope
                 by default, a foreseeable governance gap)
  Detectability: 4 (silent — erasure "appears" to succeed at the primary-store level while
                    derived copies persist undetected)
  Recoverability: 3 (requires forensic identification of all derived copies and remediation
                     across potentially many data subjects)
  Novelty: 3
Residual risk: material to critical in multi-tenant or high-DSAR-volume deployments.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Unfulfilled erasure obligations or cross-tenant leakage affecting one or more data subjects; regulatory exposure. |
| **Likelihood** | 2 | Plausible where derived-index erasure is overlooked, a common and foreseeable technical gap. |
| **Detectability** | 3 | Erasure appears to succeed at the primary-store level while derived copies persist, undetected without deliberate testing. |
| **Recoverability** | 2 | Remediable via technical fix and completion of outstanding erasures once identified. |
| **Novelty** | 3 | Treating memory as a governed data asset, and the derived-index erasure gap, are AI-architecture-specific concerns outside standard DSAR-process scope. |

## 17. Regulatory Basis
> [UK GDPR Art. 5(1)(e), storage limitation] requires personal data to be kept no longer than necessary. [UK GDPR Art. 17, right to erasure] requires verifiable deletion on request, extending to all copies including derived/technical stores. [UK GDPR Art. 30, records of processing] requires memory stores to be inventoried as processing activities. (verified 29 Jul 2026)

## 18. Research Basis
> No FS-specific peer-reviewed study of AI memory/conversation-store erasure completeness was located in the source registers; this reflects the genuinely emerging nature of persisted-memory governance as an AI-specific data-asset class, flagged [UNVERIFIED — no FS-specific study located] (verified 29 Jul 2026) rather than filled with an adjacent but non-supporting citation. The adversarial cross-tenant testing methodology draws on established multi-tenant access-control practice (ISO/IEC 27001) rather than AI-specific published research, which is itself part of why this IRQ's test is rated ★2 rather than higher.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-AGT-008 (C.5: operational memory as behavioural influence — the parallel AGT-homed concern per TAXONOMY ruling 2)
  - IRQ-SEC-004 (E.1: attack-origin injection into memory — the adversarial variant)
  - IRQ-GOV-010 (I.4: record-keeping supporting DSAR/decision reconstruction)
  - IRQ-DAT-009 (A.3: retrieval entitlement — the parallel scoping concern for retrieval)
```

## 20. References
```
[1] UK Government, 2018/2021. "UK GDPR / Data Protection Act 2018." Articles 5, 17, 30.
[2] ISO/IEC, 2022. "ISO/IEC 27001:2022 — Information security management systems." (Access
    control and multi-tenancy practice, applied by analogy.)
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: A.4 (Data domain, Memory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Data protection teams govern primary systems of record; memory
  stores are a newer, often-invisible data asset outside standard inventory/DSAR scope.
✓ Test 2 (Plausible Harm): Direct mechanism under UK GDPR Art. 17; multi-tenant leakage is a
  well-understood general information-security risk applied to a new data-asset class.
✓ Test 3 (Testable): Adversarial scoping testing and end-to-end DSAR-erasure tracing are
  executable in non-production. ★2.
✓ Test 4 (Decision-Relevant): Gates whether a persisted-memory system may support multi-tenant
  or customer-data-bearing deployment without governance remediation.

Change Log:
- v1.0 (2026-07): Initial publication.
```

---
---

