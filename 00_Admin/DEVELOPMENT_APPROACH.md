# FAIAS — Development Approach

**Companion to `README.md`.** This document records how the standard was developed: the design decisions in the order they were made and the disciplines that governed them.

---

## 1. Design philosophy

Three commitments were fixed before any content was written:

1. **Evidence base before drafting.** The standard's quality rests on its evidence base rather than its drafting. Source registers (regulators, standards bodies, frontier labs, academia, incidents) were compiled and web-verified *before* the review questions were populated, so that canvases draw on pre-verified citations rather than inventing them; a citation whose pinpoint could not be confirmed carries an [UNVERIFIED] tag (README.md §3).
2. **Taxonomy before risks.** Mixing threats, vulnerabilities, controls, consequences and governance failures into one list produces duplication and inconsistent findings. FAIAS built a canonical taxonomy first, with explicit single-homing rules and written boundary rulings for the hard cases (e.g. RAG poisoning: data supply-chain vs inference-time attack; agent memory: data asset vs operational context).
3. **Honesty as a feature.** Where the science is immature, the standard says so — anchored ★ ratings, "none established" labels, and unresolved citations retagged `[UNVERIFIED — reason]` rather than papered over. The intended reader (a board, a regulator, an internal audit committee) is told not only what was found but the basis on which the review was conducted.

## 2. Design evolution — the decisions in sequence

The standard was developed iteratively, each layer superseding or generalising the last:

| Stage | Decision | Rationale |
|---|---|---|
| 1 | Seven-volume research-first methodology ("FAIAS") with a canonical 9-domain taxonomy | Prevent the threat/control/consequence muddle from the outset |
| 2 | **Primary unit changed from "risk" to Independent Review Question (IRQ)** | "Calibration" is a label; "Has the organisation demonstrated the model remains appropriately calibrated across expected operating conditions?" is auditable. A subdomain layer (40 subdomains at the time; 44 since v1.0.3) and a four-test inclusion discipline were added at the same time |
| 3 | **Assurance model layer**: outcome-first review hierarchy; behaviour/failure-mode/consequence separation; mandatory failure chains; technology-neutral assurance objectives with traced controls; Evidence Levels L1–L5; anchored Testing Confidence ★1–★5; five-axis risk weighting with no composite score | Think like an accident investigator, not a checklist auditor: work backwards from harm, keep the control near the bottom of the hierarchy |
| 4 | **Standard-grade upper layers**: 27 assurance claims (28 since v1.1.0) bridging IRQs to a four-box deployment opinion (drawing on ISAE 3000 conclusion forms); ten materiality lenses; AI Safety Case with declared operating envelope; envelope drift promoted to a flagship IRQ; assurance lifecycle; review-confidence statement. Renamed **FAIAS** | The board's question is "should I authorise this deployment?", not "how many findings?". Claims-Argument-Evidence / GSN practice imported from aviation, nuclear and medical devices (UL 4600, ISO/IEC 15026-2) |
| 5 | **Operating machinery**: Tier 0–3 materiality classification (proportionality), six-phase engagement model (reviewer's handbook), Board Dashboard, evidence pack | A methodology becomes usable when it tells a reviewer what depth of review a deployment requires and how to run the engagement |

Two disciplines governed evolution:

- **Selective lifting.** Parallel design drafts (including output from AI systems) were assessed critically, not merged wholesale. Structural improvements (tiering, engagement workflow, dashboard) were lifted; inferior or conflicting material (a competing IRQ catalogue with unanchored maturity labels and a "cite later" stance) was rejected with the disposition recorded.
- **Amendment on principle.** Every lifted idea was checked against the standard's own rules before adoption — e.g. "assurance objectives replace controls" was amended so that traced controls survive beneath each objective (preserving the no-invented-controls rule), and all rating scales were given written behavioural anchors to protect inter-rater reliability.

## 3. The four-test inclusion discipline

Every candidate IRQ had to pass four tests or be removed/merged (dispositions recorded in `REGISTER_STATS.md`):

1. A domain SME is likely to overlook it because it stems from AI behaviour rather than domain expertise.
2. There is a plausible mechanism of harm supported by research, regulation, or documented incidents.
3. It can be answered through evidence and safe testing in a development or test environment.
4. The outcome informs a governance or deployment decision, rather than being an abstract technical curiosity.

This discipline was applied bidirectionally: it removed items (e.g. standalone licensing diligence, data minimisation — both competent-SME territory) and admitted late additions only when a genuine gap was demonstrated (e.g. feedback-data contamination, IRQ-DAT-013).

## 4. Maintenance model

- Every risk item carries publication dates and source versions (per `METHODOLOGY_STANDARDS.md`), so individual canvases can be updated as research, incidents and regulation evolve — without rewriting the framework.
- `TAXONOMY.md` is the single authoritative source for the hierarchy; all other documents defer to it.
- The IRQ↔claim matrix must retain its no-orphan property after any register change; the QA checklist and verification-log format are reusable for future batches.
- Known-aging content (regulatory timelines, in-flight standards such as ISO/IEC 27090 and NIST COSAIS, unpublished MAS AIRG final guidelines) is flagged in the registers for scheduled re-verification.
