# TP-SEC-009 — Model Artefact Supply-Chain Integrity and Deserialisation Safety

**IRQ:** IRQ-SEC-009 (subdomain E.3).
**Assurance objective:** AO-SEC-009 — model artefacts (weights, checkpoints, serialisation formats and their dependencies) shall be integrity-verified — via signing, scanning, safe-format enforcement and trusted-source sourcing — before being loaded into any training, evaluation or production environment.
**Confidence:** ★2 (carried unchanged). Method class: Mixed. The format, signing and registry-enforcement sub-tests draw on mature software-supply-chain security practice (OWASP LLM03:2025; NIST SP 800-53 SR control family analogues) and would rate higher alone; the backdoor-probing sub-test has no established methodology or benchmark for AI model artefacts. **The weaker component governs the overall rating**, per the canvas and ASSURANCE_MODEL.md §6 — this must be stated in reporting rather than averaged away.

### Preconditions
- Isolated staging instance of the artefact intake pipeline, including the registry client, scanning step, signature verification step and loader.
- Ability to place benign test artefacts into the intake path, and to attempt a direct file-system load bypassing the pipeline (the bypass route is the usual finding).
- Inventory of all currently deployed model artefacts with claimed provenance.
- Read access to intake pipeline code/configuration and to the approved trusted-registry list.
- **Benign test artefacts only**, constructed by the reviewer: a well-formed artefact in an unsafe serialisation format whose "payload" is an inert, non-executing marker; an artefact with a deliberately invalid signature; an artefact sourced from an unapproved registry location within the isolation boundary. No malicious payloads are created, stored or transmitted at any point.
- Personnel: AI security reviewer (lead); firm ML platform engineer.
- Isolation attestation confirming the staging loader cannot reach production infrastructure.

### Test design
Four sub-tests:

- **S1 Unsafe-format rejection.** Attempt to load a benign artefact packaged in an unsafe serialisation format; confirm the pipeline rejects it or handles it without code execution. The marker is inert by construction — success is measured by whether the pipeline rejected, not by whether anything ran.
- **S2 Signature enforcement.** Attempt to load an artefact with a tampered or absent signature; confirm rejection.
- **S3 Registry enforcement.** Attempt to source an artefact from outside the approved trusted-registry list; confirm the intake process blocks it.
- **S4 Bypass-path testing.** Attempt to load a test artefact by a route that circumvents the pipeline — direct file-system placement, a data-scientist workspace mount, a notebook loader. This is not in the canvas's numbered test list but is directly implied by the canvas Fail indicator naming "an unscanned side-loading route"; it is the sub-test most likely to produce a finding.
- **S5 Backdoor probing (Emerging Practice, labelled as such).** Where feasible and where an externally-sourced checkpoint is in use, a bounded adversarial input search for anomalous trigger-conditioned behaviour. This sub-test has no benchmark, no coverage guarantee and no meaningful negative result; it is run for completeness and reported with an explicit statement that absence of evidence is not evidence of absence.

**Provenance limb.** Independently of the load tests, the inventory of currently deployed artefacts is reconciled against the trusted-registry list and against provenance records.

### Steps
1. Record environment metadata and pipeline version; isolation attestation.
2. Inspect intake pipeline code/configuration: at which stage are signing and scanning enforced; is that stage bypassable; what formats are permitted; how is the registry allow-list evaluated. Record file/line references.
3. Construct the benign test artefacts. Peer-check that no artefact contains executable content of any kind.
4. Execute S1; record the pipeline's behaviour, the rejection message or the load outcome, and whether any code execution occurred.
5. Execute S2; record.
6. Execute S3; record.
7. Execute S4 across every side-load route identified in step 2 and every route the platform engineer describes as available to data scientists in practice. Record each route and its outcome. Where a route succeeds, record what controls (if any) would have detected the load afterwards.
8. Reconcile the deployed-artefact inventory: for each artefact, is its source on the approved registry list, and does a provenance record exist? Record coverage as a proportion.
9. Where an externally-sourced checkpoint is in use and S5 is feasible, run the bounded probe. Record the probe design, its coverage bounds, and the result — with the Emerging Practice label attached.
10. Remove test artefacts; sign-off.

### Observations & measures
- **S1/S2/S3 rejection outcomes** (binary each). Canvas threshold: unsafe-format, unsigned and untrusted-registry artefacts are **all** demonstrably rejected.
- **Code-execution occurrence during S1** (binary). Threshold: none.
- **S4 bypass routes** — count of routes by which a test artefact was loaded without passing signing/scanning. Threshold: **0** for a Pass; any available side-load route is a Fail condition per the canvas.
- **Provenance coverage** = deployed artefacts with confirmed trusted-registry source and provenance record ÷ deployed artefacts. Canvas threshold: **all** currently deployed artefacts confirmed sourced from the approved list with valid provenance.
- **S5 result** — anomalous trigger-conditioned behaviour found / not found, with probe coverage bounds stated. **No established threshold; reviewer judgement, and a negative result carries very little weight.**
- **Compensating control** where S5 is not performable: does behavioural monitoring exist for externally-sourced checkpoints? Binary.

### Interpretation
- **Pass** — S1, S2 and S3 all reject; no code execution; zero viable bypass routes in S4; 100% provenance coverage on deployed artefacts; and either S5 found nothing (reported with the absence-of-evidence caveat) or a compensating behavioural-monitoring control exists.
- **Fail** — any unsafe-format, unsigned or untrusted-source artefact loads successfully; **or** signing/scanning exists only on the primary deployment path with an unscanned side-loading route available; **or** no inventory of deployed-artefact provenance exists; **or** no backdoor-probing capability exists **and** no compensating control is in place for externally-sourced checkpoints.
- **Partial** — S1–S3 pass and provenance coverage is complete, but S5 was not performable and compensating monitoring is only partially implemented; or bypass routes exist but are constrained to an environment not promoted to production (state the constraint and its enforcement).

### Evidence outputs
- E1 Environment and pipeline-version attestation — **L3**.
- E2 Intake pipeline code/configuration inspection note with enforcement-stage analysis — **L3**.
- E3 Test-artefact manifest and peer-check record confirming no executable content — **L3**.
- E4 S1–S3 execution results with pipeline responses — **L3**.
- E5 S4 bypass-route enumeration and outcomes — **L3**.
- E6 Deployed-artefact provenance reconciliation table — **L3**.
- E7 S5 probe design, coverage bounds and result, labelled Emerging Practice — **L3**.
- E8 Intake pipeline design documentation reviewed — **L2**.
- E9 Independent security assessment of the ML artefact supply chain, where held — **L4**.
- E10 Operational evidence of intake-scanning rejections or confirmed incident from a comparable deployment — **L5**.
- E11 Teardown certificate — **L3**.

### Common pitfalls & limitations
- **Creating a real malicious artefact to "prove" the risk.** Prohibited. The inert marker establishes whether the pipeline rejected; nothing further is needed and creating live malware in a client environment is indefensible.
- **Testing only the sanctioned path.** S4 is where findings live. Ask the platform engineer how data scientists actually load models day-to-day, not how the documentation says they do.
- **Averaging the confidence rating.** The temptation is to report ★3 because three of five sub-tests are solid. The canvas rates ★2 because the weakest component governs; reproduce that reasoning in the report.
- **Over-reading a negative S5.** A bounded probe covers a vanishing fraction of possible trigger space. A clean S5 is close to uninformative and must be reported as such.
- **Stale inventory.** Provenance reconciliation against an inventory the firm has not maintained produces false completeness. Spot-check inventory entries against the running environment.
- **Format allow-lists that are advisory.** A configuration that "prefers" safe formats but falls back is not enforcement; read the code path.

### Time/effort estimate
**3.5 reviewer-days** — 0.5 pipeline inspection; 0.5 test-artefact construction and peer check; 0.75 S1–S3 execution; 0.5 S4 bypass exploration; 0.5 provenance reconciliation; 0.25 S5 where performable; 0.5 write-up.

---
---

