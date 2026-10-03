# TP-SEC-008 — Confidential Data Egress via Prompts, Context, Telemetry or Logs

**IRQ:** IRQ-SEC-008 (subdomain E.2).
**Assurance objective:** AO-SEC-008 — confidential firm or customer data shall not egress to environments outside the firm's control via prompts, context windows, telemetry or logs without an established lawful basis and contractual/technical control, demonstrated by complete data-flow mapping across all AI-adjacent egress paths.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — the parent discipline (data-flow mapping) is mature, but there is no AI-specific, cross-institution standardised test procedure for telemetry and logging egress paths; rated below TP-SEC-006's ★3 accordingly. Anchored to DSIT AI Cyber Security Code of Practice (2025) data-flow mapping principle and OWASP LLM02:2025.

### Preconditions
- Staging environment whose **telemetry, observability and logging configuration matches production**. This is the crux: staging is frequently configured with different log verbosity or a different APM tenant, and a test against it answers nothing. Where configurations differ, the difference must be documented and the result caveated.
- The firm's current **AI data-flow map**, plus access to configuration for: model API client, embedding store, observability/APM tooling, log aggregation, any sub-agent or tool-chain context propagation.
- Access to executed provider contracts and DPAs (or to the legal/procurement summary of their retention, logging, training-use and sub-processor terms) — this procedure's contract limb overlaps with TP-TPR-007 and the two should share evidence rather than duplicate the review.
- DLP/filtering configuration where such a control is claimed.
- Personnel: AI security reviewer (lead); firm platform engineer; observability/SRE contact (usually a different team from the AI platform team — this separation is precisely why paths get missed); legal/procurement contact for contract terms.
- Isolation attestation. Note the specific tension in this procedure: tracing egress to a third-party provider requires the staging instance to genuinely call that provider. Confirm in writing that the staging tenancy is contractually covered and that only synthetic marker content will be sent.

### Test design
**Marker methodology.** Distinct, unmistakably synthetic, high-entropy marker strings are generated — one per intended path — formatted to *resemble* confidential categories (a simulated account-number-shaped token, a simulated deal-term string) without being or deriving from anything real. Each marker is unique so that its appearance in any downstream store identifies the exact path it travelled. Markers are registered in a manifest before use and searched for afterwards.

**Paths traced:**
- **G1 Model provider** — does marker content appear in provider-side logs or training-eligible storage per the contractual terms and per any provider-side data-access console the firm holds?
- **G2 Observability / APM** — does marker content appear in traces, spans, error payloads or performance logs?
- **G3 Log aggregation** — does marker content appear in application logs, and at what verbosity level; does default configuration capture full prompt/response content?
- **G4 Downstream propagation** — does marker content propagate into tool calls, sub-agent contexts, caches, or the embedding store?

**Sampling.** Every path in the firm's data-flow map plus every path the reviewer independently identifies, each exercised with at least 3 distinct markers across at least 3 usage patterns (simple chat, retrieval-grounded query, agentic/tool-chained task where applicable) — a reviewer-set design minimum, disclosed at scoping.

**Contract limb.** Provider terms are read against what the technical test observes. The two must be reconciled: a technical finding of no egress is not a Pass if the contract permits retention the firm has not risk-accepted, and a contractual prohibition is not a Pass if markers are found in an uncovered destination.

### Steps
1. Record environment metadata and, critically, a **diff of staging versus production telemetry/logging configuration**. Any material difference is recorded and caveated.
2. Obtain the firm's AI data-flow map. Then independently enumerate egress paths from configuration — model client, APM agent, log shippers, cache layers, embedding store, tool endpoints. Record every path the map omitted; this finding stands regardless of the marker results.
3. Review provider contracts/DPAs for retention, logging, training-use and sub-processor terms. Record what is contractually permitted, prohibited, or silent. Share evidence with TP-TPR-007.
4. Inspect DLP/filtering configuration: what categories does it cover, is it applied pre-transmission, and can it be bypassed? Record.
5. Inspect default logging configuration: does it capture full prompt and response content by default? Record the verbosity setting and what it captures.
6. Generate and register markers. Confirm with the firm in writing that only these synthetic markers will be transmitted.
7. Submit markers through each usage pattern.
8. Search every identified destination for each marker: provider-side console/logs where available, APM store, log aggregation platform, caches, embedding store, tool logs. Record marker-by-destination results in a matrix.
9. For any marker found in a destination not covered by the data-flow map or by contract, record it as a discrete finding with the path traced.
10. Reconcile technical findings with contractual position; record any case where the technical result is clean but the contract permits use the firm has not risk-accepted, or vice versa.
11. Purge markers from all destinations where the firm is able to, record where purge was not possible (itself a finding), and obtain sign-off.

### Observations & measures
- **Marker-by-destination matrix** — for each marker, every destination in which it was found. Canvas threshold: **marker content not found in any telemetry/logging destination outside the firm's contractual control boundary.**
- **Map completeness** — paths independently identified ÷ paths in the firm's map. Threshold: the map must cover all AI-adjacent paths including telemetry, and must have been independently verified rather than self-declared by the platform team.
- **Contract position per provider** — confirmed exclusion of training/retention use / explicit consented use with risk acceptance / silent or ambiguous. Canvas Fail: silent or ambiguous with no compensating technical control.
- **DLP coverage** — does filtering demonstrably block or flag the confidential categories actually in use? Binary per category. No numeric threshold — reviewer judgement on category coverage adequacy.
- **Default log capture** (binary): full prompt/response content captured by default / not captured, or captured under documented contractual and technical control.
- **Policy enforcement** (binary): acceptable-use policy technically enforced / policy exists but staff can paste confidential content with no system-level prevention.

### Interpretation
- **Pass** — no marker found outside the contractual control boundary; provider terms confirmed (not merely asserted) to exclude training/retention use, or such use explicitly consented to and risk-accepted; DLP demonstrably blocks or flags confidential-category content pre-transmission; the data-flow map is current, covers all AI-adjacent paths including telemetry, and was independently verified. Report with the ★2 caveat that no standardised AI-specific egress test procedure exists and that coverage is bounded by the paths identified.
- **Fail** — a marker appears in an observability/logging destination not covered by the map or the contract review; **or** provider contract is silent or ambiguous on training/retention with no compensating technical control; **or** DLP does not exist or does not cover the confidential categories actually in use; **or** an acceptable-use policy exists but is not technically enforced.
- **Partial** — technical tracing clean on the identified paths but the data-flow map was found materially incomplete (paths added by the reviewer), or staging telemetry configuration differs from production such that G2/G3 results do not transfer. State precisely what remains unassessed.

### Evidence outputs
- E1 Environment attestation including staging-versus-production telemetry configuration diff — **L3**.
- E2 Firm's data-flow map as provided — **L2**.
- E3 Independently enumerated egress-path inventory with omissions flagged — **L3**.
- E4 Contract/DPA review note on retention, logging, training-use and sub-processors (shared with TP-TPR-007) — **L4** where a full legal review is performed and evidenced; **L2** where only the firm's own contract summary is read.
- E5 DLP and logging-configuration inspection note — **L3**.
- E6 Marker manifest and transmission authorisation — **L3**.
- E7 Marker-by-destination matrix — **L3**.
- E8 Discrete findings for markers in uncovered destinations, with path traced — **L3**.
- E9 Technical-versus-contractual reconciliation note — **L3**.
- E10 Marker purge record including any destination where purge was not possible — **L3**.
- E11 Independent data-flow/security assessment covering AI-adjacent egress paths, where held — **L4**.

### Common pitfalls & limitations
- **Staging telemetry ≠ production telemetry.** The most common invalidator. Diff it in step 1 and caveat honestly.
- **Trusting the firm's data-flow map.** Observability pipelines are owned by a different team and are routinely absent from AI data-flow maps. Independent enumeration is the substance of this test.
- **Markers that are not searchable.** Low-entropy markers collide with real content and cannot be found reliably. Use high-entropy unique strings and register them.
- **Markers that cannot be purged.** Some destinations have immutable retention. Discover this before transmitting, not after; and where purge is impossible, ensure markers are unmistakably synthetic so the residue is harmless.
- **Confusing the contract limb with the technical limb.** Both must pass. A clean technical trace under a permissive contract is not assurance.
- **Sending anything real.** Under no circumstances is real confidential content used as a marker.
- **★2 honesty.** The result covers the paths found on the test date under the staging configuration observed. It is not a guarantee of no egress.

### Time/effort estimate
**4.0 reviewer-days** — 0.5 configuration diff and environment verification; 1.0 independent path enumeration; 0.5 contract review (reduced where TP-TPR-007 runs jointly); 0.5 DLP and logging inspection; 0.5 marker generation and transmission; 0.5 destination searching; 0.5 reconciliation and write-up.

---
---

