# TP-TPR-001 — Foundation Model / API Provider Due Diligence Audit

**IRQ:** IRQ-TPR-001 — Disproportionate or Absent Foundation Model / API Provider Due Diligence.
**Assurance objective:** AO-TPR-001 — the firm shall complete and evidence AI-specific due diligence, proportionate to the materiality of the use case, covering safety evaluation coverage, security posture and known model weaknesses, before relying on a foundation model or API provider in production, and shall refresh this diligence at defined intervals.
**Confidence:** ★3 (carried unchanged). Method class: Adapted Industry Practice — a credible, standards-anchored sampling method, but no single agreed FS benchmark exists for scoring "proportionate AI diligence", so the proportionality assessment is professional judgement.

### Preconditions
- The firm's **outsourcing/CTP register** and **AI inventory**, current, with materiality tiering applied.
- The firm's **due diligence policy** setting out required content and refresh cadence, and specifically whether it names AI-specific evaluation criteria.
- Access to completed due diligence files for sampled providers.
- Access to publicly available provider information for the cross-check limb — model cards, published safety reports, published red-team results. The cross-check uses only information the firm could itself have obtained; no provider is contacted by the reviewer.
- Personnel: lead reviewer (third-party risk); firm third-party risk manager; procurement contact.
- Where TP-TPR-003 has already run, its findings enlarge the provider population and must be incorporated before sampling.

### Test design
**Population.** All current AI model/API providers in the outsourcing register and AI inventory, plus any identified by TP-TPR-003. The reviewer independently challenges the population by cross-referencing at least two other sources — expenditure records for AI-category spend, and the platform team's actual configured API endpoints — and records any provider present in those sources but absent from the register.

**Sampling.** Materiality-stratified. **All critical-tier providers** are tested (the canvas pass indicator sets a 100% bar for critical tier, so sampling within it would not support the conclusion). For lower tiers, a judgemental sample of at least 5 per tier (reviewer-set design minimum, disclosed at scoping), or the full population where smaller, selected to span provider type (frontier model API, specialist model vendor, AI-embedded platform) and onboarding vintage — older onboardings frequently predate the firm's AI-specific criteria.

**Testing criterion per sampled file.** Three questions, each answered with a documentary reference:
- **(a) Existence** — does a due diligence file exist at all?
- **(b) AI-specific content** — does it address safety evaluation coverage, security posture and known model weaknesses *specifically*, as distinct from generic commercial, financial and legal vendor risk?
- **(c) Proportionality** — is the depth visibly greater for higher-materiality providers, or is the same boilerplate applied uniformly? Uniformity across tiers is the diagnostic signal for a process that tiers on paper only.

**Cross-check limb.** For a subsample of at least 3 providers (reviewer-set design minimum, disclosed at scoping), provider-claimed evaluation results in the due-diligence file are compared against independently available public information. The question is not whether the claims are true but whether the firm **cross-checked them** or accepted them at face value.

**Refresh limb.** For each sampled provider, establish whether a refresh cadence is defined, what it is, and whether a refresh has actually occurred within it — as opposed to diligence being a single pre-contract event.

### Steps
1. Obtain the outsourcing register, AI inventory and due diligence policy. Record whether the policy names AI-specific evaluation criteria at all — a "no" here frames every subsequent finding.
2. Challenge the population against AI-category expenditure records and the platform team's configured endpoints. Record providers absent from the register.
3. Confirm materiality tiering exists and is applied; record the tiering basis.
4. Select the sample: all critical-tier providers plus the judgemental sample per lower tier.
5. For each sampled provider, test (a), (b) and (c). Record findings against a standard schedule with a documentary reference for each answer. Where content is absent, record what is present instead.
6. Score proportionality by comparing files across tiers side by side. Record whether depth visibly varies.
7. Run the cross-check limb on the subsample: locate independently available information, compare against the file's recorded claims, and record whether the file shows evidence of the firm having cross-checked.
8. Run the refresh limb: record the defined cadence, the last refresh date, and whether it is within cadence, for each sampled provider.
9. Reconcile results back to the register: does the register accurately reflect due diligence status and refresh dates for the sampled providers?
10. Report exceptions individually and the pattern collectively.

### Observations & measures
- **Critical-tier coverage** = critical-tier providers with a due diligence file addressing safety, security and known weaknesses ÷ critical-tier providers. Canvas threshold: **100%**.
- **AI-specific content rate** across the full sample. No numeric threshold in the canvas for lower tiers — **reviewer judgement**; the canvas Fail condition is files consisting solely of commercial/legal checklists with no AI-specific content.
- **Proportionality assessment** (categorical): depth visibly proportionate to tier / uniform boilerplate across tiers / no tiering applied. Canvas Fail condition: tiering absent or not reflected in diligence depth.
- **Cross-check rate** = subsample files showing evidence of independent cross-check ÷ subsample. Canvas Fail condition: provider-reported evaluation claims accepted without any independent cross-check.
- **Refresh compliance** = sampled providers with an in-cadence refresh ÷ sampled providers with a defined cadence; plus the count of providers with no defined cadence at all. Canvas Fail condition: no refresh mechanism exists; diligence is a single pre-contract event regardless of criticality.
- **Population completeness** — providers found outside the register. No threshold; any finding is material and reported.

### Interpretation
- **Pass** — 100% of critical-tier AI providers have a due diligence file addressing safety, security and known weaknesses; diligence depth is visibly proportionate to materiality tier rather than uniform boilerplate; refresh cadence is defined and evidenced as executed, not one-time at onboarding; sampled provider claims are cross-checked against independently available evidence rather than accepted at face value.
- **Fail** — due diligence files consist solely of commercial/legal checklists with no AI-specific safety or security content; **or** materiality tiering is absent or not reflected in diligence depth; **or** no refresh mechanism exists; **or** provider-reported evaluation claims are accepted without any independent cross-check.
- **Partial** — critical-tier coverage is complete and AI-specific, but refresh has lapsed for a stated number of providers, or lower-tier files are boilerplate while critical-tier files are substantive. Quantify.

### Evidence outputs
- E1 Vendor's own model card or safety report, as held unverified in the file — **L1** (explicitly labelled).
- E2 Due diligence policy with AI-specific criteria assessment — **L2**.
- E3 Population challenge record: register versus expenditure and endpoint sources, with omissions — **L3**.
- E4 Sampling basis and materiality stratification record — **L3**.
- E5 Per-provider testing schedule with documentary references for (a), (b), (c) — **L3**.
- E6 Side-by-side proportionality comparison across tiers — **L3**.
- E7 Cross-check limb findings — **L3**.
- E8 Refresh compliance schedule — **L3**.
- E9 Internal audit or second-line review confirming diligence was executed to policy standard across the provider population, where held — **L4**.
- E10 Outsourcing/CTP register extract showing diligence status and refresh dates over the last 12 months — **L5**.

### Common pitfalls & limitations
- **Sampling from an unchallenged register.** If the register is incomplete, a 100% pass across it means little. Step 2 is the substance of the procedure as much as the file testing is.
- **Accepting a completed template as completed diligence.** A file can be fully populated and contain no AI-specific assessment whatsoever. Test content against criterion (b), not completeness of fields.
- **Confusing proportionality with volume.** A longer file is not deeper diligence. Compare what questions were asked, not page count.
- **Cross-checking claims yourself and calling it a firm control.** The measure is whether the *firm* cross-checked. The reviewer's own cross-check establishes whether the claims stand, which is useful context but a different finding.
- **Old onboardings.** Providers onboarded before the firm adopted AI-specific criteria will fail (b) as a class. Report this as a remediation population rather than as eight separate findings.
- **★3 honesty.** There is no agreed benchmark for proportionate AI diligence. The proportionality judgement is the reviewer's, and the criteria used should be stated so it can be challenged.

### Time/effort estimate
**3.0 reviewer-days** — 0.5 register and policy review; 0.5 population challenge; 1.0 file testing across the sample; 0.5 proportionality, cross-check and refresh limbs; 0.5 reconciliation and write-up. Runs efficiently with TP-TPR-002 on a shared provider sample (combined saving of approximately 0.5 day).

---
---

