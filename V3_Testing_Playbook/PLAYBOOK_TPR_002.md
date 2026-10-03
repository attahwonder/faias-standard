# TP-TPR-002 — AI Provider Contract Rights Walkthrough

**IRQ:** IRQ-TPR-002 — Contracts Failing to Secure Transparency, Audit, Notification and Exit Rights.
**Assurance objective:** AO-TPR-002 — contracts with AI model/API providers shall secure advance notification of material model changes and deprecations, meaningful audit rights, and defined output usage and exit/portability rights, proportionate to the materiality of the dependent business activity.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — a regulation-anchored checklist exists for DORA-in-scope contracts (Art. 30 minimum contractual content), but AI-specific clause content is still emerging practice and adequacy requires professional judgement.

### Preconditions
- The **contract register** for AI providers, and access to **executed contracts** (not templates, not standard terms of service the firm never negotiated).
- The firm's **contract negotiation checklist** requiring AI-specific clauses, where one exists.
- Materiality tiering, shared with TP-TPR-001.
- The firm's business continuity and impact tolerance requirements for the dependent business activities — required to judge whether exit timeframes are adequate rather than merely present.
- Legal or procurement support for clause interpretation; the reviewer identifies presence and drafting adequacy, and legal opinion is sought on enforceability where drafting is ambiguous.
- Personnel: lead reviewer; legal/procurement contact; business continuity contact for the exit-timeframe limb.

### Test design
**Population and sampling.** As TP-TPR-001, sharing the provider sample: all critical-tier contracts, plus a judgemental sample of at least 5 per lower tier (reviewer-set design minimum, disclosed at scoping). Sampling shares the provider list so that diligence and contract findings can be read together per provider.

**Four clause families tested per contract**, each against a stated criterion:

- **(a) Advance notice of model change/deprecation** — present? With a **defined notice period**? Is "material change" defined, or left to the provider's discretion (in which case the clause is close to unenforceable in practice)?
- **(b) Audit rights** — present? **Contractually enforceable**, or expressed as cooperation "available on request"? Does the clause specify scope, frequency and whether third-party audit reports substitute for direct audit?
- **(c) Output usage rights** — explicitly addressed, or silent? Silence is a Fail indicator in the canvas, not a neutral position.
- **(d) Exit/portability** — present? With a **defined timeframe**? Is that timeframe consistent with the firm's own business continuity and impact tolerance requirements for the dependent activity?

**DORA comparison limb.** For contracts in DORA scope, presence of the Art. 30 minimum contractual content is tested as a compliance check. For contracts outside DORA scope, the same content is used as a reference standard and the gap reported as a risk finding rather than a compliance breach — the distinction is stated.

**Enforceability-in-practice limb.** For audit rights specifically, establish whether the right has **ever been exercised** or tested for practical enforceability. A clause never invoked, on a provider that would in practice refuse, is a paper right; the canvas lists a never-exercised audit-rights clause as a Fail Indicator (§13).

**Substitution-assumption limb.** Establish whether the firm's substitution planning assumes indefinite provider availability. Where no exit timeframe exists, this assumption is usually implicit and unexamined.

### Steps
1. Obtain the contract register and confirm it reconciles to the provider population established in TP-TPR-001. Record discrepancies.
2. Obtain the negotiation checklist; record whether it requires AI-specific clauses and when it was adopted (contracts predating adoption form a distinct population).
3. Select the sample, shared with TP-TPR-001.
4. For each sampled contract, walk the four clause families. For each, record: clause reference, presence, drafting quality against the stated criterion, and any material qualification or carve-out. Record what governs where the contract is silent — typically the provider's standard terms, which should then themselves be read.
5. Where drafting is ambiguous on enforceability, obtain a legal view and record it as legal opinion rather than reviewer finding.
6. Run the DORA comparison limb, distinguishing in-scope compliance testing from out-of-scope reference comparison.
7. Run the enforceability-in-practice limb: has the audit right ever been exercised? Ask procurement and the relationship owner; seek documentary evidence of any exercise.
8. Run the exit-timeframe adequacy limb: compare each contract's exit timeframe against the business continuity requirement for the dependent activity. Record any contract where the exit timeframe exceeds the impact tolerance.
9. Run the substitution-assumption limb.
10. Log gaps against the firm's own checklist and report exceptions per contract and per clause family.

### Observations & measures
- **Critical-tier model-change notification** = critical-tier contracts with an explicit model-change notification clause **with a defined notice period** ÷ critical-tier contracts. Canvas threshold: **all**.
- **Audit-rights enforceability** (categorical per contract): contractually enforceable with defined scope / referenced as available on request only / absent. Canvas Fail condition: a clause on paper never exercised or tested for practical enforceability.
- **Output usage rights** (binary per contract): explicitly addressed / silent or ambiguous. Canvas Fail condition: silent or ambiguous.
- **Exit timeframe adequacy** (categorical per contract): defined and consistent with impact tolerance / defined but exceeds impact tolerance / no defined timeframe. Canvas threshold: specified and consistent with business continuity/impact tolerance requirements.
- **DORA Art. 30 gap count** for in-scope contracts. Compliance criterion, applied as stated in the regulation the canvas cites.
- **Checklist gap rate** = sampled contracts with at least one gap against the firm's own checklist ÷ sampled contracts.
- **Generic-terms reliance** = contracts relying on standard vendor terms of service with no negotiated AI-specific content. Canvas Fail condition where present.

### Interpretation
- **Pass** — all critical-tier contracts contain explicit model-change notification clauses with defined notice periods; audit rights are contractually enforceable rather than merely referenced as available on request; exit/portability provisions specify a timeframe consistent with business continuity and impact tolerance requirements; output usage rights are explicitly addressed.
- **Fail** — contracts rely on generic vendor terms of service with no AI-specific notification, audit or exit clauses; **or** an audit-rights clause exists on paper but has never been exercised or tested for practical enforceability; **or** no defined exit timeframe exists and substitution planning assumes indefinite provider availability; **or** output ownership/usage rights are silent or ambiguous.
- **Partial** — critical-tier contracts are compliant on notification and exit but audit rights are untested, or output usage rights are addressed for the primary provider and silent for others. Quantify by clause family.

### Evidence outputs
- E1 Vendor standard terms of service as relied upon — **L1** (explicitly labelled where the firm treats them as the contract).
- E2 Contract negotiation checklist requiring AI-specific clauses — **L2**.
- E3 Contract register reconciliation to the provider population — **L3**.
- E4 Per-contract clause walkthrough schedule with clause references and drafting assessment — **L3**.
- E5 Legal opinion record on ambiguous enforceability — **L3**.
- E6 DORA Art. 30 comparison table, distinguishing in-scope and out-of-scope treatment — **L3**.
- E7 Audit-right exercise enquiry record and any documentary evidence — **L3**.
- E8 Exit-timeframe versus impact-tolerance comparison per dependent activity — **L3**.
- E9 Gap log against the firm's own checklist — **L3**.
- E10 Legal/procurement audit confirming contractual gap remediation across the critical-provider population, where held — **L4**.
- E11 Contract register showing notification/audit/exit clause status refreshed at renewal — **L5**.

### Common pitfalls & limitations
- **Reviewing templates rather than executed contracts.** The negotiated position is frequently weaker than the template, particularly with large model providers who negotiate little.
- **Treating clause presence as clause adequacy.** A notification clause with no defined notice period, or with "material" left to provider discretion, is present and near-worthless. Test drafting against the criterion.
- **Ignoring what governs on silence.** Where the contract is silent, the provider's standard terms usually govern — read them and record the resulting position, rather than recording "silent".
- **Exit timeframe without impact tolerance.** A 90-day exit provision is adequate or catastrophic depending on the dependent service's tolerance. The comparison is the finding, not the number.
- **Reviewer opining on enforceability.** Presence and drafting quality are reviewer findings; enforceability is a legal opinion and should be recorded as such.
- **Confusing DORA scope.** Applying Art. 30 as a compliance criterion to an out-of-scope contract misstates the finding. Use it as a reference standard and say so.
- **★3 honesty.** The regulatory anchor is real for in-scope contracts; the AI-specific clause content is emerging practice and adequacy is judgement.

### Time/effort estimate
**3.0 reviewer-days** — 0.25 register reconciliation and checklist review; 1.5 clause walkthroughs across the sample (the dominant cost, scaling with contract count and length); 0.25 legal liaison; 0.5 DORA comparison, audit-exercise and exit-adequacy limbs; 0.5 gap logging and write-up. Shares provider sampling with TP-TPR-001.

---
---

