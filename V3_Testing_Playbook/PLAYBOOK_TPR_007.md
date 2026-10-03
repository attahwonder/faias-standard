# TP-TPR-007 — Provider Retention, Logging and Training-Use Verification

**IRQ:** IRQ-TPR-007 — Unestablished Provider Data Retention, Logging and Sub-Processor Training Use.
**Assurance objective:** AO-TPR-007 — the firm shall contractually and technically establish, for every AI provider processing firm or customer data, whether that provider or any sub-processor retains, logs or trains on submitted prompts, files and outputs, and shall confirm this is consistent with the firm's confidentiality and data protection obligations before reliance.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — GDPR Article 28 provides a well-established compliance checklist for processor terms, but AI-specific training-use verification and AI-specific sub-processor disclosure remain less mature, pulling overall confidence down from ★4.

### Preconditions
- The **AI provider population** established at the start of the domain, enlarged by TP-TPR-003's findings, filtered to providers processing firm or customer data.
- Access to **executed DPAs** for sampled providers.
- Access to **API configuration** for the deployed integration of each sampled provider — specifically, which product tier and which endpoint type is actually in use.
- The firm's **sub-processor review records** and any flow-down obligation documentation.
- DPIA records covering AI-specific processing.
- Data-flow mapping evidence, shared with **TP-SEC-008** in the SEC playbook. Run the two jointly.
- Personnel: lead reviewer; data protection officer or privacy counsel; platform engineer for configuration inspection; procurement contact.

### Test design
**Population and sampling.** All providers processing firm or customer data; test all critical-tier providers and a judgemental sample of at least 5 lower-tier (reviewer-set design minimum, disclosed at scoping), spanning both formally procured providers and any identified through TP-TPR-003 or through shadow-use investigation.

**Three testing limbs per sampled provider:**

- **R1 DPA content.** Does the executed DPA **explicitly** address retention, logging and training-use? Silence on training-use is the characteristic finding: the firm relies on a marketing statement while the contract says nothing. Test each of the three elements separately — a DPA can address retention and be silent on training use.
- **R2 Tier conformance.** Does the **product tier actually deployed** match the tier covered by that DPA? This is the limb that most often produces a finding, and it cannot be tested from documents alone: it requires inspection of the API configuration — enterprise API keys with training opt-out versus consumer endpoints, enterprise tenancy versus default tenancy. Contractual protections attaching to an enterprise tier do not attach to a consumer endpoint the business is actually using.
- **R3 Sub-processor disclosure and flow-down.** Are sub-processors disclosed, and are they covered by flow-down obligations equivalent to the head DPA? AI providers frequently use infrastructure and model sub-processors whose own terms differ materially.

**Shadow-use limb.** Independently of the sampled providers, establish whether staff or business units are using **consumer-tier AI products** for confidential data outside the enterprise contractual perimeter. Evidence routes: expenditure records for consumer AI subscriptions, network or SaaS-discovery telemetry where the firm holds it, and the acceptable-use policy's technical enforcement status (shared with TP-SEC-008). This is named as a Fail indicator in the canvas and is rarely surfaced by document review alone.

**DPIA limb.** For each materially-used provider, establish whether a DPIA exists covering AI-specific processing — not a generic vendor DPIA that predates the AI use case.

**Reconciliation limb.** Compare the contractual position established in R1–R3 against the data-flow mapping and monitoring evidence: does observed data flow stay within contracted terms? Where TP-SEC-008 has run, its marker-tracing results provide the technical half of this reconciliation directly.

### Steps
1. Establish the provider population processing firm or customer data; incorporate TP-TPR-003 findings. Record the population basis.
2. Select the sample; record the rationale.
3. **R1:** For each sampled provider, read the executed DPA. Record, with clause references, the explicit position on each of: retention period, logging of prompts/files/outputs, and training use. Record "silent" where silent — do not infer from marketing material.
4. **R2:** With the platform engineer, inspect the actual deployed API configuration for each sampled provider: product tier, endpoint type, key type, tenancy, and any training opt-out setting. Compare against the tier the DPA covers. Record any mismatch.
5. **R3:** Obtain the sub-processor list for each sampled provider. Record whether it is disclosed, current, and whether flow-down obligations are documented and equivalent. Assess whether any sub-processor introduces AI-specific processing risk not covered by the head DPA.
6. **Shadow-use limb:** review expenditure records for consumer AI subscriptions and any SaaS-discovery telemetry. Establish whether the acceptable-use policy is technically enforced. Record any evidence of confidential data in consumer-tier products.
7. **DPIA limb:** for each materially-used provider, obtain the DPIA and assess whether it covers AI-specific processing.
8. **Reconciliation limb:** compare the contractual position against data-flow mapping and monitoring evidence over the last 12 months, incorporating TP-SEC-008's results where available.
9. Report per provider and per limb, with the shadow-use and reconciliation findings reported at portfolio level.

### Observations & measures
- **DPA explicitness** = sampled providers whose DPA explicitly addresses retention, logging **and** training-use ÷ sampled providers. Canvas threshold: **all** sampled providers. Canvas Fail condition: DPAs silent on training-use or retention specifics with the firm relying on marketing claims.
- **Tier conformance** = providers where the deployed tier matches the DPA-covered tier ÷ sampled providers. Canvas threshold: **all**; no shadow use of weaker consumer tiers for firm or customer data.
- **Sub-processor disclosure and flow-down** = providers with disclosed sub-processors covered by documented flow-down obligations ÷ sampled providers. Canvas Fail condition: sub-processor list undisclosed or not reviewed for AI-specific processing risk.
- **Shadow-use finding** (categorical): no evidence of consumer-tier use for confidential data / evidence found, quantified by business unit and data category. Canvas Fail condition: staff or business units found using consumer-tier AI products for confidential data.
- **DPIA coverage** = materially-used providers with an AI-specific DPIA ÷ materially-used providers. Canvas Fail condition: no DPIA covering AI-specific processing for a materially-used provider.
- **Reconciliation outcome** (binary): data-flow mapping confirms no uncontrolled egress beyond contracted terms / uncontrolled egress identified.

### Interpretation
- **Pass** — all sampled AI providers have DPAs explicitly confirming retention, logging and training-use terms; the product tier in actual use matches the tier covered by contractual protections with no shadow use of weaker consumer tiers for firm or customer data; sub-processors are disclosed with confirmed flow-down obligations; data-flow mapping confirms no uncontrolled egress beyond contracted terms.
- **Fail** — DPAs are silent on training-use or retention specifics and the firm relies on marketing claims rather than contractual terms; **or** staff or business units are found using consumer-tier AI products for confidential data, bypassing enterprise contractual protections; **or** the sub-processor list is undisclosed or not reviewed for AI-specific processing risk; **or** no DPIA exists covering AI-specific processing for a materially-used provider.
- **Partial** — DPAs are explicit and tiers conform for the critical-tier population, but sub-processor flow-down is documented for only some providers, or the DPIA population is complete for new procurements but not for pre-existing ones. Quantify.

### Evidence outputs
- E1 Provider marketing page stating "we don't train on your data" with no contractual backing — **L1** (explicitly labelled).
- E2 Executed DPA with explicit clauses on retention, logging and training-use status — **L2**.
- E3 Population and sampling rationale — **L3**.
- E4 R1 per-provider DPA content schedule with clause references and explicit "silent" markings — **L3**.
- E5 R2 API configuration inspection record: tier, endpoint, key type, tenancy, opt-out settings, with DPA-tier comparison — **L3**.
- E6 R3 sub-processor disclosure and flow-down assessment per provider — **L3**.
- E7 Shadow-use investigation record: expenditure review, SaaS-discovery telemetry, acceptable-use enforcement status — **L3**.
- E8 DPIA coverage schedule — **L2/L3**.
- E9 Data protection or legal audit confirming sub-processor flow-down obligations are met for the critical AI provider population, where held — **L4**.
- E10 Data-flow mapping and monitoring evidence confirming no uncontrolled egress over the last 12 months, cross-checked against contracted terms (shared with TP-SEC-008) — **L5**.

### Common pitfalls & limitations
- **Reading the marketing page instead of the DPA.** The canvas makes this the archetypal L1 finding. Record what the contract says, and record "silent" as silent.
- **Skipping the tier-conformance inspection.** It is the limb that finds the real exposure, and it cannot be done from documents. Get the platform engineer to show you the actual configuration.
- **Treating a sub-processor list as flow-down evidence.** Disclosure and flow-down are different questions; test both.
- **Shadow use investigated only by asking.** Business units do not self-report consumer-tier use. Expenditure records and SaaS-discovery telemetry are the routes that work.
- **Generic DPIAs.** A DPIA written for the vendor relationship before the AI use case existed does not cover AI-specific processing.
- **Duplicating TP-SEC-008.** Run them jointly; TP-SEC-008 supplies the technical egress evidence, this procedure supplies the contractual position, and the reconciliation limb needs both.
- **★3 honesty.** Art. 28 gives a real checklist for processor terms; AI-specific training-use verification and sub-processor AI risk assessment are less mature and the judgement in R3 in particular is professional rather than standardised.

### Time/effort estimate
**3.0 reviewer-days** — 0.25 population and sampling; 1.0 R1 DPA review across the sample; 0.5 R2 configuration inspection; 0.5 R3 sub-processor assessment; 0.5 shadow-use investigation; 0.25 DPIA and reconciliation limbs. Reduced by approximately 0.5 day where run jointly with TP-SEC-008.

---
---

