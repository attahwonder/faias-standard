# ID SCHEME — FAIAS

## Canonical Identifier Format

```
IRQ-<DOM>-<NNN>
```

- `IRQ` — constant prefix (Independent Review Question; FAIAS's unit of analysis)
- `DOM` — three-letter domain code (see domain list below)
- `NNN` — zero-padded sequence number (001–999 per domain)

**Example:** `IRQ-MOD-004` = Independent Review Question, Model domain, question 4 (a real register entry; earlier editions used a fictional ID here, corrected 25 Aug 2026)

---

## Three-Level Taxonomy: Domains → Subdomains → IRQs

FAIAS organises review questions through three hierarchical levels:

1. **Domains** (9 total) — broad risk categories aligned with AI lifecycle and governance
2. **Subdomains** (44 total as at v1.2.0; the original 30–40 design band was retired) — specific capability or threat area within a domain; named by the domain's letter and a number (e.g., `A.1`, `B.3`)
3. **IRQs** (109 as at v1.2.0; the original 75–100 design band was retired — validity, not the band, governs) — individual, testable, auditable review questions within a subdomain

Each IRQ is assigned to exactly one subdomain; each subdomain to exactly one domain. This structure enables:
- **Granular scoping** (assess specific subdomains without full domain review)
- **Taxonomy discipline** (no mixing threats, vulnerabilities, controls, consequences across levels)
- **Roadmapping** (prioritise subdomain build-out by business/regulatory criticality)

---

## Domain & Subdomain Definitions

### Domain Codes (Three-Letter Format)

| Code | Domain | Scope & Examples |
|------|--------|------------------|
| **DAT** | Data | Data sourcing, quality, lineage, contamination, bias injection. Covers training data, inference data, prompt injection via data sources. |
| **MOD** | Model | Model architecture, training integrity, weight manipulation, prompt injection via weights, inference robustness, output quality. |
| **AGT** | Agentic | Agent design, tool use, reward/goal drift, multi-step planning, delegation chains, failure modes in composed systems. |
| **HUM** | Human Oversight | Explainability, human review workflows, escalation, alert fatigue, override controls, SAE (supporting and evaluating) methodologies. |
| **SEC** | Security | Adversarial attacks, extraction/inversion, supply chain (model weights, fine-tuning), API/infrastructure, access control, encryption. |
| **TPR** | Third Party | Vendor assessment, SaaS dependencies, model providers, data brokers, outsourced testing/monitoring. |
| **RES** | Operational Resilience | Availability, failover, drift detection, circuit breakers, graceful degradation, incident response, recovery time. |
| **CON** | Conduct & Fairness | Discrimination (protected attributes), fairness metrics, adverse selection, information asymmetry, transparency to end-users. |
| **GOV** | Governance | Policies, roles/responsibilities, approval workflows, documentation, audit trails, regulatory alignment, board oversight. |

### Subdomain Structure (Examples)

### Canonical Subdomain Reference

**The authoritative subdomain taxonomy is defined in `V2_IRQ_Battery/TAXONOMY.md`.** This section documents naming and allocation rules only.

Subdomains are lettered A–I (one letter per domain) and numbered sequentially within each domain (44 total):

| Domain | Prefix | Subdomains (Total) |
|--------|--------|-------------|
| **Data** | DAT | A.1–A.5 (5) |
| **Model** | MOD | B.1–B.7 (7) |
| **Agentic** | AGT | C.1–C.7 (7) |
| **Human Oversight** | HUM | D.1–D.4 (4) |
| **Security** | SEC | E.1–E.7 (7) |
| **Third Party** | TPR | F.1–F.3 (3) |
| **Operational Resilience** | RES | G.1–G.4 (4) |
| **Conduct & Fairness** | CON | H.1–H.3 (3) |
| **Governance** | GOV | I.1–I.4 (4) |

**For subdomain definitions, scope statements, boundary rulings, and example IRQ mappings, refer to `V2_IRQ_Battery/TAXONOMY.md` (authoritative source).**

---

## Allocation Rules

### Single-Subdomain & Single-Domain Assignment
Every IRQ is assigned to **exactly one subdomain** (and therefore to exactly one domain).

**Discipline:** Do not mix threat (what can go wrong) with vulnerability (why it happens) with control (how to prevent it) with consequence (what happens) across domains or subdomains in a single IRQ. Each sits in its primary subdomain; cross-domain impacts are listed in `Related IRQs`.

### Examples of correct allocation:
- **IRQ-MOD-015** "Where a language model is used as a judge or evaluator to generate the institution's own evaluation evidence, has the judge itself been validated?" → MOD domain, B.5 (Distribution Shift & Evaluation Integrity subdomain)
- **IRQ-HUM-004** "Is the human intervention point positioned where intervention is still effective — before irreversible agent actions?" → HUM domain, D.3 (Escalation & Override Design subdomain)
- **IRQ-SEC-009** "Is the model artefact supply chain — weights, checkpoints, serialisation formats, dependencies — protected against tampering and known deserialisation exploits?" → SEC domain, E.3 (Supply Chain & Tool Security subdomain)
- **IRQ-GOV-005** "Do firm policies address GenAI/agentic specifics — acceptable use, data entry restrictions, output reliance, agent permissions — or only legacy model risk?" → GOV domain, I.2 (Approval, Tiering & Policy subdomain; tiering itself is IRQ-GOV-004)

### Cross-Domain Links
If an IRQ has secondary impact in another domain, this is **not a violation of single-assignment**. Instead, document it in the template field `Related IRQs`.

**Example:**
- **IRQ-MOD-013** (Model, B.6 Model Updates & Configuration) has Related IRQ → **IRQ-HUM-007** (Human Oversight, D.4 Accountability & Contestability; because prompt changes require change control and decision traceability)
- **IRQ-DAT-007** (Data, A.3 Retrieval Data) has Related IRQ → **IRQ-SEC-004** (Security, E.1 Prompt Injection & Jailbreak; because retrieval corruption enables injection attacks)

---

## Sequence Numbering

- Each domain maintains its own sequence: DAT-001 through DAT-999, MOD-001 through MOD-999, etc.
- New IRQs are appended in publication order within their domain
- Numbers are **not** reused; deprecated IRQs retain their ID with status `Deprecated`
- Gaps in numbering (e.g., DAT-001, DAT-003, no DAT-002) are acceptable and signal deprecation

---

## Deprecation & Superseding

When an IRQ is obsolete or superseded by regulation/research:

1. Mark status as `Deprecated` in the IRQ template
2. **Retain the ID** (do not reuse for a new IRQ)
3. Document superseding ID in `Limitations` field:
   ```
   Status: Deprecated (superseded by IRQ-<DOM>-NNN — illustrative format only; no IRQ is currently deprecated)
   ```
4. For major versioning events, publish a **Deprecation Notice** documenting:
   - Old ID
   - Reason (regulatory change, research invalidation, merged with another control)
   - Superseding ID (if any)
   - Sunset date (if a transition period applies)

---

## Cross-Reference Format

When one IRQ references another:

```
Related IRQs:
  - IRQ-HUM-005 (D.3 Escalation & Override Design; escalation authority for fine-tuning drift)
  - IRQ-SEC-010 (E.3 Supply Chain & Tool Security; model weight integrity verification)
  - IRQ-GOV-007 (I.3 Validation & Oversight; independent validation sign-off for model QA)
```

Cross-references are recorded **owner-side**: a link is carried in field 19 of the canvas that owns the dependency, and the register row's Related-IRQs column mirrors that canvas's field 19 exactly. Links are deliberately not asserted to be bidirectional — A referencing B does not require B to reference A. (Rule restated 26 Aug 2026; the earlier bidirectionality statement described a discipline the estate never operated. Register↔canvas agreement is machine-checked at every signing.)

---

## Reserved Ranges (Guidance, not Enforcement)

Organisations may use this scheme as a template. FAIAS reserves:
- **001–100 per domain** for core/foundational IRQs (published in FAIAS)
- **101–999** available for domain extensions, industry-specific variants, or institutional customizations

This is a suggestion only; local instantiations may number differently.

---

## Taxonomy Discipline Rule

### Threats vs. Vulnerabilities vs. Controls vs. Consequences

An IRQ must not simultaneously define:
1. **Threat** (attack/failure mode)
2. **Vulnerability** (weakness that enables threat)
3. **Control** (mitigation)
4. **Consequence** (impact if threat succeeds)
5. **Governance failure** (policy/process gap enabling control failure)

**Instead:**
- Threats → `Failure Modes` field
- Vulnerabilities → `Review Question` phrasing, `Applicable AI Systems`
- Controls → Implicit in test methods and pass/fail indicators
- Consequences → `Why this matters`, `Failure indicators`
- Governance failures → `Regulatory basis`, `Reporting language`

**Example of violation (INCORRECT):**
> "Are model weights secured (control) against extraction attacks (threat) because developers lack version control (governance failure), which could lead to model theft (consequence)?"

**Example of correction (CORRECT — single-subdomain threat+control):**
- **IRQ-MOD-013** (Model domain, B.6 Model Updates & Configuration subdomain): "Are prompt templates, system prompts and decoding parameters version-controlled and regression-tested, given that small changes materially alter behaviour without any code change?" [Threat = untracked prompt drift, vulnerability = lack of versioning, control = configuration management]
- **Related IRQs:** as recorded on the owning canvas's field 19 (for IRQ-MOD-013: see CANVASES_MOD_013.md) — cross-links are recorded owner-side and are not asserted bidirectional

---

## Governance of the Scheme

**Custodian:** the maintainer

**Change process:**
- **New domain or subdomain:** maintainer approval (major version bump)
- **New IRQ:** maintainer approval within subdomain (minor version bump)
- **Renumbering/consolidation:** Not permitted (breaks external references). Use Deprecation instead.

**Conflict resolution:** If two subdomains or domains claim ownership of an IRQ, assign based on primary control mechanism (not threat or consequence). If still ambiguous, escalate to the maintainer.

---

