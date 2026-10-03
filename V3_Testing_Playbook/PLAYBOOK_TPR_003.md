# TP-TPR-003 — Embedded AI Discovery Audit

**IRQ:** IRQ-TPR-003 — Undiscovered AI Embedded Inside Procured Software.
**Assurance objective:** AO-TPR-003 — the firm shall maintain an active discovery mechanism capable of identifying AI capabilities embedded within procured software, and shall bring every identified capability under the same risk assessment and governance framework applied to directly procured AI systems.
**Confidence:** ★2 (carried unchanged). Method class: Emerging Practice — research supports the shadow/embedded-AI phenomenon generally, but no standardised, benchmarked discovery methodology exists for FS; this is largely bespoke, professional-judgement-driven investigation and must be reported as such.

### Preconditions
- The firm's **software asset inventory** or application register, covering categories **not** originally flagged as AI: CRM, HR, surveillance/monitoring, case management, and any other line-of-business platform.
- The firm's **AI inventory**, for reconciliation.
- The **vendor management policy** and procurement questionnaire currently in use, plus the version in use at the time each sampled product was onboarded.
- Access to the firm's own vendor-management channel to re-issue AI-capability questionnaires. **The reviewer does not contact vendors directly**; questionnaires are issued by the firm's vendor manager, and the reviewer reviews the responses.
- Access to sampled products' current feature documentation, release notes and — where available — an administrative console or test tenant for technical inspection.
- Personnel: lead reviewer; firm vendor manager; application owners for sampled products; IT asset management contact.
- **Run early in the domain**, since findings enlarge the population for TP-TPR-001, -002, -007 and -008.

### Test design
**Population.** All procured software in categories not flagged as AI. In most firms this is a large population, so sampling is judgemental rather than statistical, and the sampling rationale is recorded.

**Sampling.** A cross-section of at least 12 products (reviewer-set design minimum, disclosed at scoping) spanning: the four categories the canvas names; both recently onboarded and long-standing products (long-standing products are where AI arrives silently via update); and both high-materiality platforms and lower-profile tools. Deliberately include at least two products the firm is confident contain no AI (reviewer-set design minimum, disclosed at scoping) — those are where the finding usually is.

**Three-limb testing per sampled product:**

- **D1 Documentary inspection** — current feature documentation and release notes over the last 24 months (reviewer-set design minimum, disclosed at scoping), read for AI-driven capability: scoring, ranking, recommendation, sentiment analysis, summarisation, anomaly detection, generative drafting, predictive prioritisation. Vendors frequently describe these without using the word "AI", so the reviewer searches by *capability*, not by keyword.
- **D2 Technical inspection** — where an administrative console or test tenant is available, inspect current feature settings for AI capabilities enabled by default or newly available. This limb is what distinguishes the procedure from a paper exercise. It is performed against test tenants or read-only administrative views; no production data is manipulated.
- **D3 Vendor re-questionnaire** — the firm re-issues an AI-capability questionnaire, through its own channel, to the sampled vendors. Responses are compared against D1 and D2 findings. A vendor response contradicting the reviewer's documentary findings is itself informative about the reliability of self-declaration as a control.

**Reconciliation.** Every capability found in D1–D3 is reconciled against the AI inventory: is there a corresponding entry, and a risk assessment?

**Control-design limb.** Independently of discovery, test whether the vendor management policy requires AI-capability disclosure **at intake and at each material feature update**, and whether recent procurement files evidence that requirement being applied. The update trigger is the control that matters most: AI capability arriving via routine software update after initial procurement is precisely the gap the IRQ names.

### Steps
1. Obtain the software asset inventory and the AI inventory. Record the size of the non-AI-flagged population.
2. Obtain the vendor management policy and procurement questionnaire, current and historical versions. Record whether an AI-capability field exists and when it was introduced.
3. Select the sample per the stratification above; record the sampling rationale.
4. **D1:** For each sampled product, review current feature documentation and 24 months of release notes. Record every capability meeting the AI-capability definition, with the documentary reference and the date it appeared.
5. **D2:** Where a console or test tenant is available, inspect feature settings. Record enabled AI capabilities, their default state, and whether they process firm or customer data. Where no such access is available, record the limitation.
6. **D3:** Have the firm's vendor manager re-issue AI-capability questionnaires to the sampled vendors. Record responses and compare against D1 and D2. Flag contradictions.
7. Reconcile every identified capability against the AI inventory. Record: inventory entry present with risk assessment / entry present without risk assessment / no entry.
8. Assess materiality of each undisclosed capability found: what does it do, does it influence a customer-affecting decision, and does it process personal data?
9. **Control-design limb:** test recent procurement files for evidence that AI-capability disclosure was required at intake; and test whether any mechanism exists to catch capability added via routine update — a change-notification requirement, a periodic re-questionnaire, or a release-note monitoring process.
10. Report findings by product, and report the enlarged AI population to the other TPR procedures.

### Observations & measures
- **Undisclosed capability count and materiality** — capabilities found in D1–D3 with no corresponding AI inventory entry, graded by materiality. Canvas threshold: **no material undisclosed embedded AI capability** in the sample.
- **Inventory reconciliation rate** = identified capabilities with an inventory entry and risk assessment ÷ identified capabilities.
- **Self-declaration reliability** = vendor questionnaire responses consistent with D1/D2 findings ÷ responses received. No canvas threshold — **reviewer judgement**; contradictions are reported as evidence about the control rather than about the vendor.
- **Policy requirement** (binary): AI-capability disclosure required at intake **and** at each material feature update, evidenced in recent procurement files / not. Canvas Fail condition: questionnaires have no AI-capability field and disclosure relies entirely on unprompted vendor honesty.
- **Update-trigger mechanism** (binary): a mechanism exists to catch AI capability added via routine software update / none exists. Canvas Fail condition: none.
- **Active-discovery evidence** = AI inventory entries added in the last 12 months as a result of active discovery activity rather than vendor self-declaration. Canvas pass indicator requires such entries to exist.

### Interpretation
- **Pass** — sample technical inspection finds no material undisclosed embedded AI capability; the vendor management policy requires AI-capability disclosure at intake and at each material feature update, evidenced in recent procurement files; the AI inventory shows entries added specifically as a result of active discovery activity rather than solely vendor self-declaration. Report with the ★2 caveat that no standardised discovery methodology exists and that a clean sample does not evidence a clean population.
- **Fail** — sample inspection finds embedded AI features (for example AI-driven scoring or sentiment analysis) operating in production software with no corresponding inventory entry or risk assessment; **or** vendor management questionnaires have no AI-capability field and disclosure relies entirely on unprompted vendor honesty; **or** no mechanism exists to catch AI capability added via routine software update after initial procurement.
- **Partial** — the policy requires disclosure at intake and recent files evidence it, but no update-trigger mechanism exists; or discovery found only immaterial capabilities but the inventory shows no entries from active discovery. State the gap.

### Evidence outputs
- E1 Vendor assertion of "no AI functionality" in the original procurement questionnaire — **L1** (explicitly labelled).
- E2 Vendor management policy requiring AI-capability disclosure at intake and at each material update — **L2**.
- E3 Sampling rationale and stratification record — **L3**.
- E4 D1 documentary inspection findings per product with references and capability dates — **L3**.
- E5 D2 technical inspection findings, or the access limitation where inspection was not possible — **L3**.
- E6 D3 vendor re-questionnaire responses with consistency comparison — **L3**.
- E7 Inventory reconciliation schedule with materiality grading — **L3**.
- E8 Control-design limb findings on intake and update triggers — **L3**.
- E9 Second-line or internal audit report confirming AI inventory completeness testing was performed and gaps remediated, where held — **L4**.
- E10 AI inventory register showing embedded-AI entries added over the last 12 months as a result of active discovery — **L5**.

### Common pitfalls & limitations
- **Keyword searching for "AI".** Vendors describe AI capability as "smart prioritisation", "intelligent routing", "automated insights". Search by capability, not by label.
- **Sampling only products the firm suspects.** Deliberately include the confident ones.
- **Skipping D2 for convenience.** Documentary review alone reproduces the vendor's own account. The technical inspection is what makes this more than a questionnaire exercise, and where it is not possible the limitation must be reported explicitly.
- **Contacting vendors directly.** The reviewer works through the firm's vendor-management channel; direct contact creates contractual and relationship problems and is out of scope.
- **Treating a vendor's "no" as closure.** D3's value lies in the contradictions, not the confirmations.
- **Ignoring the update vector.** Initial procurement diligence catches nothing added later. The update-trigger finding is often more consequential than any individual capability discovered.
- **★2 honesty.** A clean sample of 12 in a population of hundreds evidences the sample, not the population. Say so plainly, and report the discovery-mechanism findings as the more generalisable result.

### Time/effort estimate
**4.0 reviewer-days** — 0.5 population and policy review; 0.5 sampling; 1.25 D1 documentary inspection across the sample; 0.75 D2 technical inspection; 0.5 D3 questionnaire coordination and response review; 0.25 reconciliation and materiality grading; 0.25 control-design limb and write-up. Vendor response turnaround adds elapsed time without reviewer effort; initiate D3 on day one.

---
---

