# FAIAS — Testing Playbook: SEC (Security) Domain

**Volume:** V3 Testing Playbook (Component 5)
**Scope:** Fourteen executable test procedures, TP-SEC-001 to TP-SEC-014, one per IRQ in `V2_IRQ_Battery/canvases/CANVASES_SEC.md` and (for IRQ-SEC-003) `V2_IRQ_Battery/EXEMPLAR_CANVASES.md`.
**Document Custodian:** the maintainer
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.
**UK spelling throughout.**

---

## Domain Testing Overview (one page)

### What this playbook does

Each Review Canvas in the SEC domain contains a field 11 *Independent Test* — a paragraph describing what should be tested and to what published methodology. This playbook expands each of those paragraphs into an **executable procedure**: preconditions, test design, numbered steps, what to record, how to measure, and how the result maps to the canvas's pass/fail/partial indicators. Nothing in this playbook changes the canvas. Assurance objectives, ★ confidence ratings, pass and fail indicators are carried across **unchanged**; where this playbook adds anything, it adds procedural detail, not new risk assertions and not new citations.

### Non-negotiable operating rules

1. **Dev/test only.** Every procedure runs in an isolated non-production environment. No procedure in this playbook may be executed against a production endpoint, a live customer channel, real transactional rails, real credentials, or real customer data. This restates METHODOLOGY_STANDARDS.md §3 (Non-Production Rule) and is a condition of the engagement, not a preference. The domain now also contains a **documentation-and-interview-only procedure** — TP-SEC-012 executes no technical test of any kind — for which this rule applies vacuously; no environment is built for it, and none should be expected.
2. **No working exploits in FAIAS artefacts.** SEC procedures below describe **test classes and observation points**, not payloads. No FAIAS document — playbook, working paper, evidence pack or report — contains a working jailbreak string, a functioning injection payload, a live credential, a plaintext secret, or a reusable attack script. Where a corpus is required, the procedure specifies how the reviewer *sources or constructs* it from published technique taxonomies in a controlled repository, and how it is destroyed afterwards. Corpora are held in the engagement's controlled evidence store, referenced by identifier in the report, and never reproduced in the report body.
3. **Benign-payload principle.** Test content is constructed so that a successful "attack" produces a harmless, unambiguously observable marker — an inert instruction the system either follows or does not (e.g. emit a specified nonsense token, call a mocked no-op tool, retrieve a synthetic document). Success is measured by whether the boundary was crossed, never by causing real harm. All marker content is synthetic and clearly labelled as test data.
4. **Reversibility.** Every environment change made by a procedure (seeded corpus entries, test tool servers, test artefacts, test credentials) is inventoried at the start and removed at the end, with a teardown record signed off.
5. **Honest confidence.** The ★ rating on each procedure is the canvas rating, carried unchanged. Where a procedure has sub-tests of differing maturity (TP-SEC-009 is the clearest case), the weaker component governs the overall rating and this is stated in reporting, per ASSURANCE_MODEL.md §6 and METHODOLOGY_STANDARDS.md §3c. **The domain now contains a ★1 procedure** (TP-SEC-012), the first in SEC. Any conclusion resting on it carries the ★1 form of words required by PLAYBOOK_OVERVIEW.md §8: "This conclusion rests on ★1 methodology — the harm mechanism is theoretically plausible and the testing approach is novel and unvalidated. Result quality depends entirely on assessor expertise. This is expert opinion, not evidence."

### Confidence and method-class distribution

| Procedure | Subdomain | ★ (carried) | Method class (METHODOLOGY_STANDARDS §3) |
|---|---|---|---|
| TP-SEC-001 Direct prompt injection | E.1 | ★4 | Established Benchmark (OWASP LLM01:2025; MITRE ATLAS AML.T0051) |
| TP-SEC-002 Multi-turn / encoded / cross-lingual | E.1 | ★3 | Adapted Industry Practice |
| TP-SEC-003 Indirect injection via retrieval | E.1 | ★4 | Established Benchmark (OWASP LLM01:2025) |
| TP-SEC-004 Untrusted content → agent action | E.1 | ★2 | Emerging Practice |
| TP-SEC-005 Inference-time RAG poisoning | E.1 | ★3 | Adapted Industry Practice (PoisonedRAG) |
| TP-SEC-006 System prompt / config extraction | E.2 | ★3 | Adapted Industry Practice (OWASP LLM07:2025) |
| TP-SEC-007 Training-data extraction / MIA | E.2 | ★3 | Adapted Industry Practice |
| TP-SEC-008 Confidential data egress | E.2 | ★2 | Emerging Practice (mature parent discipline, novel application) |
| TP-SEC-009 Artefact supply chain | E.3 | ★2 | Mixed; weakest component (backdoor probing) governs |
| TP-SEC-010 MCP / tool-server compromise | E.3 | ★2 | Emerging Practice |
| TP-SEC-011 Non-human identity & credentials | E.4 | ★2 | Adapted Industry Practice (mature IAM testing, novel subject) |
| TP-SEC-012 Third-party misuse register | **E.5** | ★1 | None established |
| TP-SEC-013 AI-as-control adversarial evolution | **E.6** | ★2 | Adapted Industry Practice (NIST AI 100-2e2025; MITRE ATLAS) |
| TP-SEC-014 Improper output handling | **E.7** | ★2 | Adapted Industry Practice (OWASP Top 10 for LLM Applications 2025, LLM05:2025) |

### Sequencing

TP-SEC-001 establishes the single-turn baseline that TP-SEC-002 and TP-SEC-006 both compare against; run it first. TP-SEC-003 and TP-SEC-005 share a staging knowledge store and should be scheduled consecutively to amortise environment build. TP-SEC-004 and TP-SEC-010 share the agentic test harness. TP-SEC-011 should precede TP-SEC-004, because a finding that the agent runs on a shared or over-scoped credential materially changes the blast-radius interpretation of any TP-SEC-004 result.

Placement of TP-SEC-012, TP-SEC-013 and TP-SEC-014, assigned from the canvas observations: TP-SEC-012 runs after TP-SEC-001 and TP-SEC-002, since its admissibility test turns on whether any control failed and reads better once control integrity has been characterised. TP-SEC-014 is deliberately **not** scheduled together with TP-AGT-005 or TP-SEC-004 — its canvas names them as the reverse-direction and inbound counterparts and is explicit that passing one is not evidence for the other, and scheduling them together risks the exact conflation the IRQ exists to break. TP-SEC-013 shares no environment with any existing SEC procedure and is placed wherever environment readiness allows.

### Personnel

Procedures assume an AI security reviewer (lead), a platform/infrastructure engineer with staging access provided by the firm, and — for TP-SEC-007 — a reviewer with applied privacy/ML background. The firm provides an environment owner accountable for the isolation of the test environment and for teardown sign-off.

Three further roles are required by the additions. **TP-SEC-012** needs the **product or risk owner of the deployment**, not only the AI delivery team — a canvas pass indicator rather than a convenience. **TP-SEC-013** needs a **fraud, AML, surveillance or screening domain SME** for the plausibility limb. **TP-SEC-014** needs **application-security competence in the lead reviewer and the owners of each consuming system**, because boundary enumeration depends on people who do not sit in the AI team.

### Total indicative effort

**57.0 reviewer-days** across the fourteen procedures, excluding report drafting and firm-side effort. See per-procedure estimates.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-SEC-001: PLAYBOOK_SEC_001.md
- TP-SEC-002: PLAYBOOK_SEC_002.md
- TP-SEC-003: PLAYBOOK_SEC_003.md
- TP-SEC-004: PLAYBOOK_SEC_004.md
- TP-SEC-005: PLAYBOOK_SEC_005.md
- TP-SEC-006: PLAYBOOK_SEC_006.md
- TP-SEC-007: PLAYBOOK_SEC_007.md
- TP-SEC-008: PLAYBOOK_SEC_008.md
- TP-SEC-009: PLAYBOOK_SEC_009.md
- TP-SEC-010: PLAYBOOK_SEC_010.md
- TP-SEC-011: PLAYBOOK_SEC_011.md
- TP-SEC-012: PLAYBOOK_SEC_012.md
- TP-SEC-013: PLAYBOOK_SEC_013.md
- TP-SEC-014: PLAYBOOK_SEC_014.md

---
---

## Domain effort summary — SEC

| Procedure | ★ | Reviewer-days |
|---|---|---|
| TP-SEC-001 | ★4 | 4.0 |
| TP-SEC-002 | ★3 | 5.0 |
| TP-SEC-003 | ★4 | 5.0 |
| TP-SEC-004 | ★2 | 6.0 |
| TP-SEC-005 | ★3 | 4.0 |
| TP-SEC-006 | ★3 | 3.0 |
| TP-SEC-007 | ★3 | 5.0 |
| TP-SEC-008 | ★2 | 4.0 |
| TP-SEC-009 | ★2 | 3.5 |
| TP-SEC-010 | ★2 | 4.0 |
| TP-SEC-011 | ★2 | 3.0 |
| TP-SEC-012 | **★1** | 2.0 |
| TP-SEC-013 | ★2 | 4.5 |
| TP-SEC-014 | ★2 | 4.0 |
| **Total** | | **57.0** |

Excludes report drafting, firm-side effort, environment build by the firm, and compute wall-time for TP-SEC-007. Savings of roughly 1.0 day in total are available by scheduling TP-SEC-003 with TP-SEC-005 (shared knowledge store) and TP-SEC-004 with TP-SEC-010 (shared agentic harness). None of TP-SEC-012, TP-SEC-013 or TP-SEC-014 shares an environment with an existing SEC procedure, so the scheduling saving above is unaffected by them.

---

**Change Log**
- v1.0 (2026-07): Initial publication. Eleven procedures expanded from CANVASES_SEC.md and EXEMPLAR_CANVASES.md (IRQ-SEC-003). ★ ratings, assurance objectives and pass/fail/partial indicators carried unchanged from canvases. No new citations introduced.
- v1.1 (2026-08-25): TP-SEC-012 (third-party misuse applicability and register review), TP-SEC-013 (AI-as-control efficacy against adversarially evolved inputs) and TP-SEC-014 (improper output handling) added, derived 1:1 from the IRQ-SEC-012, IRQ-SEC-013 and IRQ-SEC-014 canvases; subdomains E.5, E.6 and E.7 added; domain totals move to fourteen procedures and 57.0 reviewer-days; ★ distribution becomes two ★4, four ★3, seven ★2 and one ★1 — the domain's first ★1. No new citations introduced.
- v1.2.1 (2026-09-19): TP-SEC-004 and TP-SEC-013 — errata carried from CANVASES_SEC.md. TP-SEC-004's Pass interpretation no longer cites GTG-1002 as documented use of this attack class: it cites the documented exploitation of the class (incident register row 37) and, for the scale at which adversaries operate agentic tooling, GTG-1002, whose attribution to a state actor is the provider's own assessment. The FTC v. Rite Aid precedent in TP-SEC-013 is re-dated: the complaint and a proposed stipulated order were filed on 19 December 2023 and the stipulated order was signed on 23 February 2024 and filed on 26 February 2024. Its characterisation is corrected with the canvas: the complaint alleges that the technology's accuracy was never tested and that both vendors disclaimed it, so no reported accuracy existed for an error rate to diverge from, and the allegations were neither admitted nor denied. The precedent's stated limitation — a facial-recognition matching failure, not a fraud or AML adversarial-evasion incident — is unchanged, as are both procedures, their ★2 ratings and the reviewer-day estimates. No new citations introduced beyond those the canvas carries.
