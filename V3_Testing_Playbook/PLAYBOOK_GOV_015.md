# TP-GOV-015 — External Capability Claim Reconciliation Against the Validated Envelope

## 1. Procedure Identity
**Procedure ID:** TP-GOV-015
**IRQ:** IRQ-GOV-015 — External Capability Claims Exceeding the Validated Envelope
**Assurance objective:** AO-GOV-015 — The firm's external representations of AI capability shall be substantiated by, and periodically reconciled against, the system's validated capability envelope and documented limitation statements, before publication and on a defined cycle thereafter.
**★ Confidence (carried from canvas, unchanged):** ★2 — the enforcement pattern this control addresses is well evidenced, but **no established audit methodology exists beyond documentation review and sample tracing**, and no benchmark exists for how closely a claim must sit to the validated envelope.
**Method classification:** Emerging Practice — a reconciliation and documentation review, not an empirical test, conducted entirely against documentation and sample tracing. The canvas records that **no published methodology for this specific reconciliation control was identified**, and that the control follows from the enforcement pattern recorded in its regulatory basis rather than from a prescriptive published standard. Three of its five expected controls — the reconciliation process itself, the periodic cycle, and the correction or retraction route — are each marked Emerging Practice.

## 2. Preconditions
**Environment:** Documentation and sample tracing only. **No production system access is required**, and none is taken. This procedure examines the firm's external representations about the system, not the system's own outputs. External materials are reviewed as published; no claim is altered and no external party is contacted.
**Access required:** The documented capability envelope and limitation statement per system in scope, current as maintained, with its last-updated date and change history — this is the IRQ-GOV-009 artefact and this procedure depends on it existing; external-facing capability claims across **all** channels — marketing material and product disclosures, RFP and due-diligence responses, investor communications — with publication dates; the reconciliation process documentation, if one exists, including its scope, cadence and ownership; correction or retraction records.
**Artefacts required:** The validated capability envelope and limitation statement, with the date it was last updated and every material change in the review period; a drawable population of external claims per channel, with publication dates; the underlying validation evidence each claim would need to be traced to (TP-MOD-001's capability and limitation testing supplies this where it is in scope); the reconciliation process documentation; ownership records for both the claim and the reconciliation.
**Personnel required:** Reviewer (lead); the validation or model-risk owner who maintains the envelope; the marketing or product-disclosure owner; the sales or bid function that authors RFP and due-diligence responses; the investor-relations owner where investor communications are in scope; legal or compliance liaison for the correction and retraction route; the owner of the reconciliation process, **if one exists** — establishing whether that ownership is distinct from ownership of the claim itself is one of the findings.
**Data handling:** RFP and due-diligence responses are commercially sensitive and are frequently subject to counterparty confidentiality. Extracts are referenced by document and section in the controlled evidence store; the report cites the claim and its reference, not the surrounding commercial terms.

## 3. Test Design
**Sample tracing of external claims back to the validation record, and nothing more.** For each sampled claim, the question is whether it is substantiated by, and does not exceed, the documented capability envelope and limitation statement. **A claim with no traceable basis, or one exceeding what validation established, is a finding.**

**Dependency handling.** Where the documented capability envelope does not exist for a system in scope, that is recorded as a dependency failure against IRQ-GOV-009 and is not worked around. A reconciliation cannot be performed against an artefact that does not exist, and constructing a substitute envelope would replace the control being tested.

**Independent determination, then comparison** — the domain's second discipline applies directly. The reviewer establishes what the validated envelope actually supports **before** reading the firm's justification of the claim, because reading the justification first anchors the reviewer to the firm's own reading of its evidence.

**Channel coverage is a pass condition, not a sampling convenience.** The canvas requires claims reviewed to span marketing, RFP/due-diligence responses **and** investor communications, not only one channel. The canvas's own partial condition is precisely the pattern of marketing tracing correctly while a sampled RFP response and an investor communication both exceed what validation established — the channels least likely to have been reviewed by anyone technical, and the ones carrying a written, retained record.

**Drift limb, distinct from the substantiation limb.** A claim can be true at launch and drift silently as the system is retrained, reconfigured or has its scope narrowed. The claim itself carries no expiry or version marker to prompt review. For each sampled claim, establish the publication date and compare it against the envelope's change history: was the claim accurate against the envelope **as it stood at publication**, and is it accurate against the envelope **as it stands now**? Those are two different findings, with two different remediations, and both are reported.

**Process limbs.** Establish whether a reconciliation process exists; whether it runs both pre-publication **and** on a periodic cycle; whether its ownership is distinct from ownership of the claim itself; and — applying "existence is not operation" — whether at least one historical instance evidences it catching and correcting drift. Establish separately whether a correction or retraction route exists and has been used where needed.

**Sampling.** Risk-based, weighted to claims about Tier 2–3 systems and to the most specific claims — a specific capability assertion is traceable and a vague one is not, and the specific ones are where the exposure sits. The sample basis, size, weighting and channel coverage are recorded before fieldwork begins.

## 4. Steps
1. Obtain the documented capability envelope and limitation statement for each system in scope, with its last-updated date and change history. **Record:** the envelope as it stands, and every material change to it in the review period. Where an envelope does not exist, record the dependency failure against IRQ-GOV-009 rather than constructing a substitute.
2. Draw and record the claim sample across all three channel types, with publication dates. **Record:** the sampling basis, size, weighting and channel coverage, before fieldwork begins.
3. For each sampled claim, establish independently what the validated envelope supports on that point, **before** reading any justification the firm offers for the claim. **Record:** the reviewer's independent determination.
4. Trace each sampled claim to the underlying validation evidence. **Record:** the evidence relied on, or that the claim has no traceable basis.
5. Compare each claim against the envelope **as it stood at the claim's publication date**. **Record:** substantiated / exceeded, with the specific excess identified / untraceable.
6. Compare each claim against the envelope **as it stands now**. **Record:** the same three outcomes, and flag every claim that was accurate at publication and has since drifted.
7. Request the reconciliation process documentation. **Record:** whether one exists, its scope, its cadence, and which channels it covers.
8. Establish whether reconciliation runs pre-publication only, or pre-publication and periodically. **Record:** the cycle and evidence of it operating.
9. Establish ownership of the reconciliation process and compare it against ownership of the claim itself. **Record:** whether the two are distinct or the same function.
10. Search for at least one historical instance where reconciliation caught and corrected an overreaching claim, before or after publication. **Record:** the instance, or the absence of any.
11. Establish whether a correction or retraction route exists and whether it has been used. **Record:** the route definition and any correction or retraction records.
12. For every claim found to exceed the envelope, establish whether the firm was already aware. **Record:** the awareness position, which distinguishes a process gap from a disclosure problem.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Sampled claims traced to validation evidence | **All** sampled claims trace to validation evidence and do not exceed the documented envelope (canvas pass indicator). A claim with no traceable basis, or one exceeding what validation established, is a finding | Canvas |
| Claim accuracy at publication versus now | Both assessed and reported separately. A claim accurate at publication that has since drifted is a distinct finding, with a distinct remediation, from one that was never substantiated | Canvas failure chain: the envelope changes and the claim is not updated |
| Channel coverage of the sample | Spans marketing, RFP/due-diligence responses **and** investor communications, not only one channel (canvas pass indicator) | Canvas |
| Reconciliation process | Exists, is **independently owned**, and runs both pre-publication and on a periodic cycle (canvas pass indicator). Reconciliation occurring only at launch and never repeated as the envelope changes is a canvas fail indicator | Canvas |
| Historical drift catch | At least one instance evidences the reconciliation process catching and correcting drift (canvas pass indicator) — "existence is not operation" applied; where none exists, the absence is recorded rather than treated as a pass | Canvas; GOV domain posture |
| Correction or retraction route | Exists and has been used where needed (canvas pass indicator); its absence is a canvas fail indicator | Canvas |
| Ownership distinctness | Reconciliation ownership is distinct from ownership of the claim itself (canvas pass indicator); ownership that is not distinct is a canvas fail indicator | Canvas |
| Proximity of a claim to the envelope | **Reviewer judgement — no established threshold.** The canvas states that no benchmark exists for how closely a claim must sit to the validated envelope; the materiality basis is recorded per claim so it can be challenged | Canvas — explicitly bespoke |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where sampled external claims trace to validation evidence and do not exceed the documented envelope; a reconciliation process exists, is independently owned, and runs both pre-publication and on a periodic cycle; at least one historical instance evidences the process catching and correcting drift; a correction or retraction route exists and has been used where needed; and the claims reviewed span marketing, RFP/due-diligence responses and investor communications rather than only one channel.

**Fail** where: one or more sampled claims cannot be traced to validation evidence, or exceed the documented envelope; **or** no reconciliation process exists and claims are drafted and published with no link to the validation record; **or** reconciliation, where it exists, occurs only at launch and is never repeated as the envelope changes; **or** no correction or retraction route exists for claims later found to exceed the envelope; **or** ownership of reconciliation is not distinct from ownership of the claim itself.

**Partial** where — the canvas's own shape — marketing materials trace correctly to the validated envelope, but a sampled RFP response and an investor communication both contain claims exceeding what validation established, with no reconciliation process covering those channels. The assurance objective is not met; remediation should extend the process to all external-facing channels and correct the identified claims. Name the claims and the channels; a count alone cannot be acted on.

## 7. Evidence Outputs
- Statement that the system is validated and documented — **L1** (asserts an internal record exists; does not evidence that external claims are reconciled against it)
- Documented capability envelope and limitation statement, with its change history over the review period — **L2**
- Reconciliation process documentation defining scope, cadence and ownership — **L2**
- Sample selection record with basis, size, weighting, channel coverage and publication dates, recorded before fieldwork — **L2**
- Reviewer's independent determination of what the envelope supports, recorded before any firm justification was read — **L3**
- Sample trace of external materials back to the validated envelope, claim by claim, with the at-publication and as-now comparisons reported separately and the materiality basis recorded per marginal claim — **L3**
- Ownership comparison between the reconciliation process and the claim itself — **L3**
- Correction or retraction records where drift was found and corrected — **L3/L4**
- Evidence from an actual historical instance where reconciliation caught and corrected an overreaching claim before or after publication — **L5**

## 8. Common Pitfalls & Limitations
- **Accepting a documented envelope as the assurance.** "The system is validated" and "what we say about the system is validated" read as the same question and are structurally different controls — the first tests the internal record (IRQ-GOV-009), the second tests whether anyone reconciles the outward-facing statement against it. The canvas's blind-spot finding is exactly this conflation.
- **Sampling marketing only.** Marketing is the channel most likely to have been through a compliance review. RFP and due-diligence responses carry a written, retained record and are frequently drafted under time pressure by a bid team with no line to the validation function. Investor communications carry disclosure-accuracy consequences distinct from and additional to customer-facing exposure. Claims are owned by different teams per channel.
- **Reading the firm's justification first.** Step 3 precedes step 4 for the same reason the domain's second discipline exists: reading the firm's record first anchors the reviewer to it.
- **Assessing the claim only against today's envelope.** A claim can have been accurate at publication and drifted since — a different finding, and a different remediation, from a claim that was never substantiated. The claim carries no expiry or version marker to prompt review. Steps 5 and 6 are both required.
- **Launch-only reconciliation treated as the control.** A process that runs pre-publication and never again cannot catch the drift that is this IRQ's characteristic failure.
- **Self-policed claims.** Reconciliation owned by the team that wrote the claim is not the control; the canvas makes ownership distinctness a pass indicator.
- **Accepting a general commercial-compliance review as coverage.** Capability claims are conventionally reviewed for general misleading-statement risk, not for AI-specific substantiation against a technical validation record. An AI-specific gap passes that review unchallenged.
- **Treating a designed reconciliation process as a control.** The historical-catch evidence is the substance. A process that has never caught anything, in a period during which the envelope changed, has not been shown to operate.
- **Judging marginal claims without recording the reasoning.** No benchmark exists for how closely a claim must sit to the envelope. Where the reviewer calls a claim marginal, the recorded reasoning is the finding's only defence against challenge.
- **Regulatory-basis limitation carried forward.** The canvas cites enforcement actions against unsubstantiated AI capability claims — **the SEC's two settled Investment Advisers Act orders of 18 March 2024 (AI-washing), recorded in the incident register at row 15, and the FTC's final consent order against DoNotPay, Inc., on capability claims the complaint charged as unsubstantiated (allegations neither admitted nor denied), recorded at row 46** — and records that **no UK/EU regulatory instrument specifically requiring reconciliation between AI-capability claims and a validated capability envelope was identified**. The enforcement pattern is cited as cross-jurisdictionally instructive precedent, not as a UK/EU binding instrument. Report against the assurance objective, not as a breach.
- **★2 caveat.** A documentation and sample-tracing review with no published protocol. Report as professional assessment **of the sample reviewed**, not as a claim-by-claim audit of every external statement the firm has made.

## 9. Time / Effort Estimate
**3 reviewer-days**: 0.5 day envelope extraction and change-history review; 0.5 day sampling across three channel types with publication dates; 1 day independent determination and claim-by-claim tracing, including both the at-publication and as-now comparisons; 0.5 day reconciliation process, ownership, historical-catch and correction-route limbs; 0.5 day analysis and working papers. Where investor communications require legal or company-secretarial retrieval, allow additional elapsed time outside reviewer-days.

---
---

