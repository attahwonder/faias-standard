# TP-TPR-005 — Open-Source Model Provenance Verification

**IRQ:** IRQ-TPR-005 — Unverified Open-Source Model Provenance.
**Assurance objective:** AO-TPR-005 — the firm shall verify publisher authenticity, weight integrity, licence compatibility and freedom from known backdoors or unsafe fine-tunes for every open-source model before deployment, and shall use safe serialisation and loading practices.
**Confidence:** ★2 (carried unchanged). Method class: Mixed. OWASP ML Top 10 provides a structured checklist for supply-chain and deserialisation risk (that component alone would rate ★3); backdoor and unsafe-fine-tune behavioural screening remains bespoke research-grade testing (★1–2). **The weaker component governs the blended rating**, per the canvas — state this in reporting rather than averaging.

### Preconditions
- **Applicability check.** This procedure applies only where the firm deploys open-source or externally-sourced model weights. Where all models are accessed via provider APIs, record that finding and close.
- The firm's **artefact registry** or model inventory listing deployed open-source models, with claimed source and version.
- The firm's **open-source model intake policy** specifying required provenance, integrity, licence and serialisation checks.
- Access to intake files for sampled models, and to the deployed artefacts themselves in staging.
- Isolated staging environment for the behavioural probe limb.
- Legal support for licence-compatibility assessment against intended commercial use.
- Personnel: lead reviewer; technical reviewer for hash and format verification; legal contact for licence terms.
- Where TP-SEC-009 is also in scope, schedule together: TP-SEC-009 tests whether the intake **pipeline** enforces controls; this procedure tests whether **deployed artefacts** actually satisfy them. They are complementary and share the artefact inventory.

### Test design
**Population and sampling.** All deployed open-source models where the population is small (typically it is); otherwise a judgemental sample of at least 5 (reviewer-set design minimum, disclosed at scoping) spanning model families, sourcing routes and deployment vintage.

**Four verification limbs per sampled model:**

- **V1 Publisher authenticity** — is the claimed publisher the actual publisher? Verify the artefact's registry namespace, any publisher signature or attestation, and whether the source location matches the claimed publisher's official channel. Typosquatted and mirror-hosted artefacts are the failure this limb catches.
- **V2 Weight integrity** — compare the deployed weight file hash against a known-good reference where one is available. Where no reference hash is published by the publisher, record that limitation — it is a finding about the ecosystem as much as about the firm, and it bounds what verification is possible.
- **V3 Serialisation format safety** — establish the serialisation format of each deployed artefact and whether any unsafe (pickle-based) format is in production. Where an unsafe format is present, establish whether a mitigating scan step is applied before loading.
- **V4 Licence compatibility** — obtain the licence terms for each deployed model, and assess compatibility with the firm's actual intended commercial use, with legal input. Many permissively-badged model licences carry use restrictions (field-of-use, acceptable-use, downstream-distribution) that are incompatible with commercial FS deployment.

**V5 Backdoor probe (Emerging Practice, labelled).** Where feasible, a bounded behavioural probe for known trigger-pattern backdoor classes is run against a non-production instance. This limb has no benchmark, no coverage guarantee, and a negative result carries very little weight. It is run for completeness and reported with an explicit statement that absence of evidence is not evidence of absence, and that its immaturity is what caps the procedure's overall rating at ★2.

**Registry reconciliation.** Independently of the sampled verification, the artefact registry is tested for whether it records integrity verification status for **all** open-source models in production over the review period, or only for some.

### Steps
1. Perform the applicability check; record the outcome.
2. Obtain the artefact registry, intake policy and intake files for sampled models. Record whether the policy specifies provenance, integrity, licence and serialisation checks.
3. Select the sample; record the rationale.
4. **V1:** For each sampled model, verify publisher authenticity against the claimed source: registry namespace, publisher attestation, official channel match. Record the verification route and result.
5. **V2:** Obtain the deployed weight file hash and compare against a published reference where available. Record match, mismatch, or reference-unavailable.
6. **V3:** Determine the serialisation format of each deployed artefact. Where unsafe formats are found, establish whether a scanning step is applied before loading, and verify it in configuration rather than accepting the assertion.
7. **V4:** Obtain licence terms; assess against intended commercial use with legal input; record any restriction incompatible with that use.
8. **V5:** Where feasible, run the bounded behavioural probe in isolated staging. Record the probe design, its coverage bounds, and the result — labelled Emerging Practice.
9. Reconcile the registry: does it record integrity verification status for all production open-source models, or a subset? Record the coverage proportion.
10. Compare each sampled model's intake file against the policy's required checks; log gaps.
11. Report per model and per limb.

### Observations & measures
- **V1 publisher authenticity** = sampled models with verified publisher authenticity ÷ sampled. Canvas threshold: **all** sampled models show verified publisher authenticity.
- **V2 integrity match** = models with a matching known-good hash ÷ models where a reference hash was available; plus the count where no reference was available. Canvas threshold: matching integrity hashes across sampled models. Canvas Fail condition: deployed models lack any integrity verification and provenance rests solely on the download source's reputation.
- **V3 serialisation safety** — count of unsafe-format artefacts in production, and of those, how many have a verified mitigating scan step. Canvas threshold: **no unsafe (pickle-based) formats in production without a mitigating scan step.** Canvas Fail condition: unsafe formats loaded without scanning.
- **V4 licence compatibility** = models with documented terms confirmed compatible with commercial FS use ÷ models deployed. Canvas threshold: **every** deployed model. Canvas Fail condition: terms undocumented or incompatible.
- **V5 probe result** — anomalous behaviour found / not found, with coverage bounds stated. **No established threshold; reviewer judgement, and a negative result carries very little weight.** Canvas Fail condition: no screening for backdoor/trigger behaviour has ever been performed on deployed open-source models.
- **Registry coverage** = production open-source models with recorded integrity verification status ÷ production open-source models.

### Interpretation
- **Pass** — all sampled models show verified publisher authenticity and matching integrity hashes (or, where no reference hash exists, an alternative documented verification route); no unsafe serialisation formats in production without a mitigating scan step; licence terms documented and confirmed compatible with commercial FS use for every deployed model; backdoor/trigger screening finds no anomalous behaviour on the tested probe set, reported with the absence-of-evidence caveat.
- **Fail** — deployed models lack any integrity verification and provenance rests solely on the download source's reputation; **or** unsafe serialisation formats are loaded without scanning; **or** licence terms are undocumented or incompatible with intended commercial use; **or** no screening for backdoor or trigger behaviour has ever been performed on deployed open-source models.
- **Partial** — publisher authenticity, integrity and format checks pass, but licence review is complete for the primary model only, or V5 was not performable and no compensating behavioural monitoring exists. State the gap.

### Evidence outputs
- E1 Model hub listing showing a "verified" badge, accepted without further check — **L1** (explicitly labelled).
- E2 Open-source model intake policy specifying required checks — **L2**.
- E3 Applicability determination and sampling rationale — **L3**.
- E4 V1 publisher authenticity verification record per model, with route used — **L3**.
- E5 V2 hash comparison record, including reference-unavailable cases — **L3**.
- E6 V3 serialisation format inventory and scan-step configuration verification — **L3**.
- E7 V4 licence terms schedule with legal compatibility assessment — **L3**.
- E8 V5 probe design, coverage bounds and result, labelled Emerging Practice — **L3**.
- E9 Registry coverage reconciliation — **L3**.
- E10 Intake file versus policy gap log — **L3**.
- E11 Security assessment or red-team report on the deployed model including backdoor-trigger screening results, where held — **L4**.
- E12 Artefact registry log showing integrity verification status for all open-source models in production over the last 12 months — **L5**.

### Common pitfalls & limitations
- **Accepting a registry "verified" badge as verification.** The canvas names this as L1 explicitly. The badge attests to the hub's own process, not the firm's.
- **No published reference hash.** Common, and it genuinely bounds what V2 can establish. Record the limitation rather than reporting a pass on an unverifiable check.
- **Licence assessed against intended use as described rather than as deployed.** The actual deployment may exceed the described use — ask what the model is used for, not what it was procured for.
- **Format check on the intake artefact rather than the deployed one.** They diverge, particularly where conversion steps exist in the pipeline. Check what is actually loaded.
- **Over-reading V5.** A bounded probe covers a vanishing fraction of possible trigger space. Say so.
- **Averaging the rating.** The canvas is explicit that the weaker component governs. Reproduce that reasoning.
- **Duplicating TP-SEC-009.** That procedure tests the pipeline's enforcement; this tests the deployed artefacts' provenance. Run both, share the inventory, do not conflate the findings.

### Time/effort estimate
**3.0 reviewer-days** — 0.25 applicability and sampling; 0.5 V1 publisher verification; 0.5 V2 hash comparison; 0.5 V3 format inventory and scan verification; 0.5 V4 licence review with legal; 0.25 V5 where performable; 0.5 registry reconciliation and write-up. Reduced by roughly 0.5 day where run jointly with TP-SEC-009.

---
---

