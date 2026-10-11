# FAIAS — Testing Playbook: TPR (Third-Party Risk) Domain

**Volume:** V3 Testing Playbook (Component 5)
**Scope:** Nine executable audit programmes, TP-TPR-001 to TP-TPR-009, one per IRQ in `V2_IRQ_Battery/canvases/CANVASES_TPR.md`.
**Document Custodian:** the maintainer
**Version:** the release version in `README.md`; the signed manifest, `ownership/MANIFEST.sha256`, identifies the release.
**UK spelling throughout.**

---

## Domain Testing Overview (one page)

### What this playbook does

TPR procedures are **structured audit programmes**, not laboratory tests. Their substance is documentation reconciliation, contract-clause walkthroughs, register completeness testing and change-detection design review. Two procedures (TP-TPR-004 and TP-TPR-006) carry a technical limb executed in staging; the rest — TP-TPR-009 included — are desk-based against the firm's own records, its executed contracts, and independently available public information. Each expands the field 11 *Independent Test* of its canvas into a runnable programme with a sampling basis, numbered steps and a defensible evidence trail. Assurance objectives, ★ ratings and pass/fail/partial indicators are carried across **unchanged**.

Written as audit programmes, these procedures follow a common shape: **define the population → stratify and sample → test each sampled item against a stated criterion → reconcile the result against the firm's own register → report exceptions**. Where a criterion comes from a regulation or standard the canvas already cites (DORA Art. 30 for contractual content; GDPR Art. 28 for processor terms; OWASP ML Top 10 for supply-chain and deserialisation risk), it is applied as the criterion. Where no such criterion exists — which is the case for "proportionate AI diligence", embedded-AI discovery, silent-drift detection and AI concentration measurement — the procedure says so plainly and the test becomes an evidenced professional judgement rather than a compliance check.

### Non-negotiable operating rules

1. **Dev/test and desk-based only.** No procedure probes a third party's infrastructure or manipulates production data. TP-TPR-004 and TP-TPR-006 run their technical limbs in the firm's own isolated staging environment; from there TP-TPR-004 calls the provider's generally available endpoint with synthetic prompts, within the provider's published usage terms, which is ordinary use and not production testing (METHODOLOGY_STANDARDS.md §3). TP-TPR-003 involves vendor engagement through the firm's own vendor-management channel, initiated by the firm, never by the reviewer directly.
2. **The register is the population, and the register is also under test.** Every TPR procedure samples from the firm's AI inventory, outsourcing register or contract register. Those registers are themselves evidence, and their completeness is a finding in its own right — most of the real findings in this domain come from what the register omits rather than from what a sampled item fails on. Each procedure therefore includes an **independent completeness challenge** to the population, not merely a sample from it.
3. **Documentary evidence, not assurance-by-conversation.** A statement in a meeting that a control operates is L1. The procedures below specify what document, configuration or register entry constitutes the evidence, and at what level.
4. **Confidentiality.** Contracts, DPAs and provider due-diligence files are commercially sensitive. Extracts are referenced by clause and stored in the controlled evidence store; the report cites clause references, never reproduced commercial terms.
5. **Honest confidence.** Five of the nine procedures are ★2 — the underlying disciplines (vendor risk, contract review, concentration analysis) are mature, but their AI-specific application is emerging practice with no standardised methodology — and one is ★1. That distinction is stated in reporting rather than smoothed over. **The ★1 is the domain's first** (TP-TPR-009), and any conclusion resting on it carries the ★1 form of words required by PLAYBOOK_OVERVIEW.md §8: "This conclusion rests on ★1 methodology — the harm mechanism is theoretically plausible and the testing approach is novel and unvalidated. Result quality depends entirely on assessor expertise. This is expert opinion, not evidence."

### Confidence and method-class distribution

| Procedure | Subdomain | ★ (carried) | Method class (METHODOLOGY_STANDARDS §3) |
|---|---|---|---|
| TP-TPR-001 Provider due diligence | F.1 | ★3 | Adapted Industry Practice (standards-anchored; no agreed FS proportionality benchmark) |
| TP-TPR-002 Contract rights | F.1 | ★3 | Adapted Industry Practice (DORA Art. 30 anchored; AI clause content emerging) |
| TP-TPR-003 Embedded AI discovery | F.1 | ★2 | Emerging Practice (no standardised discovery methodology) |
| TP-TPR-004 Silent provider-side change | F.2 | ★2 | Emerging Practice (bespoke canary design) |
| TP-TPR-005 Open-source provenance | F.3 | ★2 | Mixed; weakest component (backdoor screening) governs |
| TP-TPR-006 Embedding/vector lock-in | F.3 | ★2 | Mixed; IR metrics mature, mismatch/export scenarios bespoke |
| TP-TPR-007 Retention, logging, training use | F.3 | ★3 | Adapted Industry Practice (GDPR Art. 28 anchored) |
| TP-TPR-008 Concentration risk | F.3 | ★2 | Emerging Practice (DORA concept; no standard AI aggregation method) |
| TP-TPR-009 Vendor financial standing and continuity | F.1 | ★1 | None established (a due diligence and contract review item, not an empirical test) |

### Sequencing and shared assets

The **AI inventory** (per IRQ-GOV-002) and the **outsourcing/CTP register** are the shared population for the whole domain. Establish and challenge their completeness once, at the start, and reuse across all nine procedures — this is the single largest efficiency in the domain and also the source of its most consequential findings.

TP-TPR-003 (embedded AI discovery) directly tests inventory completeness and should therefore run **early**, since anything it finds enlarges the population for TP-TPR-001, -002, -007 and -008.

TP-TPR-001, TP-TPR-002 and **TP-TPR-009** share a provider sample and should be executed together on the same sampled files: TP-TPR-009 asks a different question of the same population and the same due-diligence and contract files, and reviewing those files three times is waste. TP-TPR-009 runs third within that group, on the provider sample TP-TPR-001 draws and the files it and TP-TPR-002 have already reviewed. TP-TPR-007 shares its contract limb with TP-SEC-008 (confidential data egress) in the SEC playbook — run them jointly and share evidence rather than reviewing the same DPAs twice. TP-TPR-005 shares subject matter with TP-SEC-009 (artefact supply chain); where both are in scope, TP-SEC-009's pipeline testing and TP-TPR-005's provenance verification should be scheduled together.

### Personnel

Procedures assume a lead reviewer with third-party-risk and outsourcing-regulation competence; legal or procurement support for the contract limbs; a technical reviewer for TP-TPR-004, -005 and -006; and firm-side provision of the AI inventory, outsourcing register, contract files, due-diligence files, vendor-management channel and staging access.

**TP-TPR-009's continuation limb needs one role this paragraph does not supply: the owner of the dependent business activity.** Neither legal, procurement nor the technical reviewer can speak to whether a substitute provider is dimensioned for the volume.

### Total indicative effort

**29.0 reviewer-days** across the nine programmes, excluding report drafting and firm-side effort.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each test procedure of this domain is held in its own file in this folder, and this file holds the domain's introductory text and closing text. The text of each procedure is unchanged by the move. Before v1.3.1 the procedures were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The procedures, in order:

- TP-TPR-001: PLAYBOOK_TPR_001.md
- TP-TPR-002: PLAYBOOK_TPR_002.md
- TP-TPR-003: PLAYBOOK_TPR_003.md
- TP-TPR-004: PLAYBOOK_TPR_004.md
- TP-TPR-005: PLAYBOOK_TPR_005.md
- TP-TPR-006: PLAYBOOK_TPR_006.md
- TP-TPR-007: PLAYBOOK_TPR_007.md
- TP-TPR-008: PLAYBOOK_TPR_008.md
- TP-TPR-009: PLAYBOOK_TPR_009.md

---
---

## Domain effort summary — TPR

| Procedure | ★ | Reviewer-days |
|---|---|---|
| TP-TPR-001 | ★3 | 3.0 |
| TP-TPR-002 | ★3 | 3.0 |
| TP-TPR-003 | ★2 | 4.0 |
| TP-TPR-004 | ★2 | 3.5 |
| TP-TPR-005 | ★2 | 3.0 |
| TP-TPR-006 | ★2 | 3.5 |
| TP-TPR-007 | ★3 | 3.0 |
| TP-TPR-008 | ★2 | 3.0 |
| TP-TPR-009 | **★1** | 3.0 |
| **Total** | | **29.0** |

Excludes report drafting, firm-side effort, and vendor response turnaround for TP-TPR-003 (elapsed time, not reviewer effort). Savings of approximately 1.5 days in total are available by running TP-TPR-001 with TP-TPR-002 (shared provider sample), TP-TPR-005 with TP-SEC-009 (shared artefact inventory), and TP-TPR-007 with TP-SEC-008 (shared contract and data-flow evidence). A further saving of approximately 1.0 day is available across TP-TPR-001, TP-TPR-002 and TP-TPR-009 where all three run on the same materiality-stratified sample and the same due-diligence and contract files; as with TP-TPR-001's own saving, the full figure stands in the column above and the saving is stated here. Establishing and challenging the AI inventory and outsourcing register once at the start of the domain, rather than per procedure, is assumed in these estimates.

---

**Change Log**
- v1.0 (2026-07): Initial publication. Eight audit programmes expanded from CANVASES_TPR.md. ★ ratings, assurance objectives and pass/fail/partial indicators carried unchanged from canvases. No new citations introduced.
- v1.1 (2026-08-25): TP-TPR-009 (AI vendor financial standing and continuity on failure) added, derived 1:1 from the IRQ-TPR-009 canvas; domain totals move to nine programmes and 29.0 reviewer-days; ★ distribution becomes three ★3, five ★2 and one ★1 — the domain's first ★1. No new citations introduced.
- v1.3.2 (2026-10-03): TP-TPR-004's use of the provider's endpoint stated under the non-production rule (METHODOLOGY_STANDARDS.md §3); three procedure subdomains corrected; TP-TPR-002 corrected (00_Admin/CORRECTION_LOG_2026-10-03.md §8). No ★ rating or reviewer-day figure changes.
- v1.3.3 (2026-10-09): TP-TPR-009 — in the confidence line, PRA SS2/21 cited as its November 2024 version (15 November 2024, updating 29 March 2021); the expectations cited are unchanged. No ★ rating or reviewer-day figure changes.
