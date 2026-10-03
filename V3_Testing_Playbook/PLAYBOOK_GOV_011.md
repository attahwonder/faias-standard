# TP-GOV-011 — Regulatory Obligation Mapping Re-Determination

## 1. Procedure Identity
**Procedure ID:** TP-GOV-011
**IRQ:** IRQ-GOV-011 — Applicable Regulatory Obligations Not Mapped to Each AI System with an Evidenced Compliance Owner
**Assurance objective:** AO-GOV-011 — Applicable regulatory obligations — EU AI Act classification, outsourcing/CTP register status, Consumer Duty MI requirements, and model risk management scope — shall be explicitly determined and mapped for every AI system in the inventory, with an evidenced named compliance owner accountable for maintaining the mapping and acting on it.
**★ Confidence (carried from canvas, unchanged):** ★3 — credible, established regulatory-mapping adequacy review methodology, strengthened by the EU AI Act's own published classification criteria as an external reference point for the highest-materiality obligation; no benchmark exists for the combined four-obligation mapping exercise as a whole, so professional judgement determines overall mapping adequacy.
**Method classification:** Adapted Industry Practice — regulatory-obligation-mapping adequacy review via independent re-determination and gap comparison.

## 2. Preconditions
**Environment:** Governance records and interviews. No production system access required.
**Access required:** The complete AI inventory (ideally the version tested under TP-GOV-002); the firm's documented regulatory-obligation mapping per system; the outsourcing/CTP register; the model risk management inventory; Consumer Duty MI definitions; system use-case documentation sufficient for independent classification.
**Artefacts required:** AI inventory; per-system obligation mapping with version history; outsourcing/CTP register; MRM inventory; Consumer Duty MI framework; vendor/cloud dependency documentation; named compliance owner records; EU AI Act Annex III classification criteria as the external reference.
**Personnel required:** The named compliance owner(s) for the mapping; the outsourcing register owner; the MRM function; reviewer with competence in the four obligation types.
**Data handling:** Governance records; no customer data. Vendor arrangements may be commercially sensitive.

## 3. Test Design
Independent re-determination followed by gap comparison. For each sampled system the reviewer determines, from the system's *actual* use case and dependencies and without first reading the firm's mapping:

1. Should it be classified under EU AI Act Annex III?
2. Should it appear on the outsourcing/CTP register, based on its vendor/cloud dependency?
3. Should its outcomes feed Consumer Duty MI?
4. Does it fall within SS1/23 MRM scope?

The independently derived determination is then compared to the firm's documented mapping, and any obligation the firm omitted is a finding. Because Annex III publishes explicit classification criteria, obligation 1 is the most externally anchored of the four; the combined four-obligation exercise has no benchmark, which is what the ★3 professional-judgement caveat addresses.

Sample: risk-based from the complete inventory, weighted toward systems plausibly engaging credit, insurance pricing, or vendor/embedded AI arrangements — the three areas where mapping omissions concentrate. Minimum eight systems, including at least three vendor-embedded arrangements (reviewer-set design minimum, disclosed at scoping).

A consistency limb cross-checks the mapping against the registers themselves: a system marked in-scope in the mapping but absent from the corresponding register is an internal contradiction that neither document alone reveals.

## 4. Steps
1. Obtain the AI inventory and note whether it has been completeness-verified. **Record:** version; verification status — an unverified inventory bounds this procedure's coverage.
2. Draw and record the sample with the specified weighting. **Record:** basis; vendor-embedded inclusion.
3. For each sampled system, gather use-case and dependency evidence **without** reading the firm's mapping. **Record:** evidence gathered; confirmation the mapping was not consulted.
4. Independently determine EU AI Act Annex III classification from the actual use case. **Record:** determination and the Annex III category relied upon.
5. Independently determine outsourcing/CTP register applicability from the vendor/cloud dependency against the register's own trigger criteria. **Record:** determination and the trigger relied upon.
6. Independently determine whether outcomes should feed Consumer Duty MI. **Record:** determination and reasoning.
7. Independently determine SS1/23 MRM scope. **Record:** determination and reasoning.
8. **Now** obtain the firm's documented mapping and compare across all four obligations. **Record:** per system per obligation — agreement, firm broader, firm omitted. Every omission is a finding.
9. **Consistency limb.** Cross-check the mapping against the outsourcing/CTP register and the MRM inventory. **Record:** any system marked in-scope in one and absent from the other.
10. Identify the named compliance owner for the mapping as a whole. **Record:** whether a single accountable individual exists or responsibility is diffuse across legal, compliance, model risk and procurement.
11. Interview the compliance owner(s). Ask them to describe the current state of the mapping and cite a recent action taken as a result of it. **Record:** verbatim; whether a concrete action can be cited.
12. Review mapping version history against known material system changes. **Record:** whether the mapping was re-triggered on new use case, new vendor or new customer segment.

## 5. Observations & Measures
| Measure | Threshold | Basis |
|---|---|---|
| Independent re-determination matches firm mapping | 100% of sample across all four obligation types | Categorical per canvas pass indicator |
| Named compliance owner citing a recent action | ≥1 concrete action cited | Categorical per canvas pass indicator |
| Register/mapping consistency | No system in-scope in one record and absent from the corresponding register | Categorical per canvas pass indicator |
| Mapping re-triggered on material change | Evidenced by version history | Categorical per canvas pass indicator |
| Vendor-embedded arrangements on the outsourcing/CTP register where triggers met | 100% | Categorical per canvas pass indicator |
| Adequacy of the combined four-obligation exercise | Reviewer judgement — no benchmark exists for the combined mapping; Annex III criteria anchor obligation 1 only | Explicitly bespoke; the ★3 caveat |

## 6. Interpretation (per CANVASES_GOV.md fields 12–14)
**Pass** where: independent re-determination matches the firm's mapping for 100% of the sample across all four obligation types; the named compliance owner can describe the mapping's current state and cite a recent resulting action; the outsourcing/CTP register and MRM inventory are consistent with the mapping; mapping is re-triggered on material system change evidenced by version history; and no vendor-embedded arrangement meeting register triggers is absent from the register.

**Fail** where: re-determination identifies at least one applicable obligation the firm omitted (most commonly Annex III classification or outsourcing-register status for embedded vendor AI); no named evidenced compliance owner exists and responsibility is diffuse; mapping was performed once at firm level as a generic regulatory-awareness statement with no per-system determination; register and mapping are inconsistent for a vendor-embedded arrangement; or the mapping has not been updated despite a known material change.

**Partial** where three obligations map correctly and one — almost always the outsourcing/CTP status of embedded vendor AI — is systematically omitted.

## 7. Evidence Outputs
- AI inventory extract and firm mapping as obtained — **L2**
- Independent re-determination working paper with the confirmation that the firm's mapping was not consulted first — **L3**
- Four-obligation comparison matrix — **L3**
- Register consistency cross-check — **L3**
- Reviewer's independent mapping-adequacy assessment — **L4**
- Records of real actions taken as a result of the mapping — **L5**

## 8. Common Pitfalls & Limitations
- **Reading the firm's mapping first.** Anchoring again; step 3's confirmation is the safeguard.
- **Sampling from an unverified inventory.** The systems most likely to be unmapped are the ones most likely to be uninventoried. Sequence after TP-GOV-002 and state the dependency.
- **Treating firm-level regulatory awareness as mapping.** The canvas names generic firm-level statements as a fail indicator; the obligation is per-system.
- **Under-weighting vendor-embedded arrangements.** This is where the omissions are. The minimum of three is a floor, not a target.
- **Reviewer competence.** The four obligation types span EU regulation, UK outsourcing rules, conduct and prudential model risk. Where the reviewer lacks depth in one, bring in a specialist and record who determined what.

## 9. Time / Effort Estimate
**4 reviewer-days**: 0.5 day sampling and evidence gathering, 2 days independent re-determination across four obligations for eight systems, 0.5 day comparison and register consistency check, 0.5 day interviews, 0.5 day working papers.

---
---

