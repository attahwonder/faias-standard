# TP-SEC-012 — Third-Party Misuse Applicability Assessment and Misuse-Case Register Review

**IRQ:** IRQ-SEC-012 — Customer Misuse of Working AI Capability as an Instrument Against a Third Party (subdomain E.5).
**Assurance objective:** AO-SEC-012 — where the applicability condition at canvas section 1 is met, the institution shall have identified and registered foreseeable pathways by which its customer-facing AI output could be repurposed by an authorised user as an instrument against a third party, and shall have tested applicable refusal and rate controls against the registered patterns.
**Confidence:** ★1 (carried unchanged). Method class: **None established** — no published, cross-institution testing methodology exists for adversary-free dual-use/misuse assessment of customer-facing generative FS tools. The canvas states this plainly rather than filling the gap with an invented protocol, and expressly limits assurance activity to documentation review and interview. Its own words: the risk is real and structurally evidenced, but no test protocol, published or bespoke, has emerged for this exact class; **★1 reflects an evidenced field with no accepted testing methodology, distinct from a weak or poorly-executed test.** The misuse-case register and the rate/volume monitoring control are each marked Emerging Practice in the canvas's control list.

### Preconditions
- **Applicability is confirmed at scoping — this procedure is not universal.** In scope only for customer-facing deployments whose outputs are plausibly repurposable by the user as an instrument against a third party. Non-exhaustive trigger list, per canvas section 1: free-text generative output to customers; drafting or document-production capability; guidance responsive to user-described scenarios; output that carries the institution's brand or authority outside the session. Where none applies, the reviewer records the deployment out of scope with dated rationale. **Silence, or an unrecorded default, is a fail condition — not a pass.**
- **Admissibility test, applied before anything else.** Misuse is the system operating as designed, its legitimate capability repurposed by an authorised user against a third party. Jailbreak is adversarial defeat of a control. The distinguishing question, per TAXONOMY boundary ruling 16 as carried in the canvas, is: **did any control fail?** If yes, the matter is a TP-SEC-001 or TP-SEC-002 finding and does not belong here. If no, and harm arises from the capability working correctly against an unintended target, it belongs here.
- **No adversarial probing, no staged payload injection, and no technical test of any kind is performed under this procedure.** The reviewer assesses the sufficiency of the firm's own documented reasoning, not system behaviour under test. Nothing is generated, injected or elicited.
- Read access to: the deployment's scoping record, including the dated applicability-assessment record if one exists; the misuse-case register, where one exists; refusal-design documentation and any change record linking refusal design to registered misuse patterns; any rate or volume monitoring configured on generative drafting capability; brand or authority disclaimer design on portable output; complaint, incident and third-party-harm records touching the system's output, where any exist.
- Personnel: AI security reviewer (lead); **the product or risk owner of the deployment, not only the AI delivery team** — the canvas makes owner involvement a distinct pass indicator, and delivery-team-only authorship is a distinct partial condition.
- No environment, no staging instance and no system access are required. This procedure is documentary and interview-based throughout.

### Test design
Two limbs only, and the canvas is explicit that there is no third.

- **D1 Applicability-determination review.** Establish whether the applicability question was **ever asked** at scoping, by whom, and when. The canvas's most likely and most material fail mode is not a wrong answer but no evidence the question was posed. A wrong-but-documented determination is a materially different finding from an undocumented default, and the two are reported separately.
- **D2 Register sufficiency review, where in scope.** Establish whether a misuse-case register exists, is dated, and names **specific foreseeable patterns for this deployment** — fraudulent-communication drafting, evasion or concealment guidance, social-engineering material — rather than reproducing a generic template. Where the register identifies a pattern, establish whether refusal design or another compensating control is shown to address at least those registered patterns, cross-referenced to specific register entries.

**Independent trigger assessment.** The reviewer assesses the deployment against the section-1 trigger list independently, and records the count, **before** reading the firm's own determination. This is not optional: the canvas's second fail indicator turns on the deployment exhibiting multiple trigger conditions, which the reviewer cannot establish from the firm's own answer.

**Interview scope.** One structured session with the product or risk owner, confirming: that the applicability determination was actively made rather than defaulted; where in scope, that the registered patterns reflect the deployment's actual request patterns; and that registered patterns inform refusal design. Delivery-team authorship without owner review is recorded as such.

**Ownership limb.** Establish whether any function claims ownership of the misuse question at all. The canvas's structural fail mode is that security confirms controls held, conduct confirms the firm's own customer was not harmed, and the gap between the two is never closed by anyone.

**Compensating-control limb.** Review any rate or volume monitoring on high-risk generative capability, and any brand or authority disclaimer applied to portable output — canvas expected controls 4 and 5. Record what exists; neither is a substitute for the register, and both are Emerging Practice with no published FS benchmark.

**Sampling.** Not applicable — the unit is the deployment, and both limbs run against it in full.

### Steps
1. Apply the admissibility test. Confirm that no control failure is in issue; where one is, route the matter to TP-SEC-001/TP-SEC-002 and record that this procedure does not apply to it.
2. Assess the deployment against the section-1 trigger list independently, before reading the firm's own determination. **Record:** which trigger conditions the deployment exhibits, and how many.
3. Request the dated applicability-assessment record. **Record:** whether one exists; its date; who made the determination; the determination itself, in-scope or out-of-scope; and the rationale given. Absence — not merely a wrong answer — is itself a fail condition; record it as such rather than substituting the reviewer's own determination for it.
4. Compare the firm's determination against the reviewer's independent trigger assessment at step 2. **Record:** any divergence and its direction.
5. Where out of scope and correctly so, record the determination and stop. Where in scope, or where the determination is absent or divergent, continue.
6. Request the misuse-case register. **Record:** whether it exists; its date; its authorship; the number of patterns named; and, for each, whether it is specific to this deployment's actual request patterns or reproduced from a generic template.
7. For each registered pattern, request the refusal design or compensating control said to address it. **Record:** the mapping, pattern by pattern, or the absence of any mapping.
8. Review any rate or volume monitoring on high-risk generative capability, and any brand or authority disclaimer applied to portable output. **Record:** what exists.
9. Interview the product or risk owner. **Record** verbatim: whether they were aware the applicability question existed; whether they made or reviewed the determination; and, where in scope, whether they recognise the registered patterns as reflecting the deployment's real request patterns.
10. Establish which function, if any, claims ownership of the misuse question. **Record:** the answer, including "none".
11. Check for any complaint, incident or third-party-harm record traced to the system's output. **Record:** any such record, or that none was identified.

### Observations & measures
- **Applicability determination** (categorical): dated determination exists and was made by a product/risk owner / dated determination exists but was made by the delivery team alone / no evidence the question was ever asked. Canvas pass indicator requires the first; the third is the canvas's most material fail indicator.
- **Trigger-condition count** — the number of section-1 trigger conditions the deployment exhibits, as independently assessed by the reviewer. Reported alongside the determination, because a deployment exhibiting several triggers with no register is a materially stronger finding than one exhibiting a single marginal trigger.
- **Register existence and specificity** (categorical, where in scope): dated register naming specific foreseeable patterns for this deployment / register exists but is generic or templated with no evidence it reflects this deployment's actual request patterns / no register. Canvas fail indicators cover the second and third.
- **Refusal-design mapping** — the proportion of registered patterns for which a refusal design or compensating control is shown to address the pattern. Canvas pass indicator: at least the registered patterns are addressed. **No threshold beyond that is set — reviewer judgement.**
- **Compensating controls** (categorical): rate or volume monitoring on high-risk generative capability, and a brand/authority disclaimer on portable output — present and configured / absent. Recorded as canvas expected controls, both Emerging Practice; neither substitutes for the register.
- **Ownership** (categorical): a named function owns the misuse question / no function claims it. The canvas records "no function claims ownership" as a distinct fail indicator, separate from any documentary gap.
- *No FAIAS numeric threshold applies anywhere in this procedure. All measures are presence-and-quality judgements on the firm's documentation; there is no system-behaviour measure, by design.*

### Interpretation
- **Pass** — a dated applicability determination exists against the section-1 trigger list, made by someone with product or risk ownership rather than defaulted or silently assumed; where in scope, a dated misuse-case register names specific foreseeable patterns for this deployment rather than a generic template; refusal design or another compensating control is shown to address at least the registered patterns; and interview confirms the product/risk owner, not only the AI delivery team, was involved in the determination. Report with the ★1 caveat that this evidences **process rigour, not demonstrated resistance to misuse** — no test of system behaviour was performed, because none exists.
- **Fail** — no evidence the applicability question was ever asked at scoping, despite the deployment exhibiting one or more trigger conditions; **or** the deployment exhibits multiple section-1 trigger conditions and no misuse-case register exists; **or** a register exists but is generic or templated with no evidence it reflects this deployment's actual request patterns or trigger conditions; **or** no function claims ownership of the misuse question, security having confirmed controls held and conduct having confirmed the firm's own customer was not harmed, with the gap between them never closed.
- **Partial** — the canvas's own shape: applicability was assessed and confirmed in scope and a register exists, but interview evidence indicates it was produced by the delivery team without product/risk-owner review, and no refusal design has yet been mapped to the registered patterns. The assurance objective is not met until ownership and refusal-design mapping are both demonstrated.

### Evidence outputs
- E1 Vendor or platform assertion that the system cannot be misused, with no register or rationale — **L1**.
- E2 Dated applicability-assessment record (in-scope or out-of-scope determination against the section-1 trigger list) — **L2**.
- E3 Reviewer's independent trigger-condition assessment, recorded before the firm's determination was read — **L2/L3**.
- E4 Misuse-case register naming specific foreseeable patterns for the deployment, where in scope — **L2**.
- E5 Interview record with the product/risk owner (not only the AI delivery team) confirming the applicability determination was actively made, and that registered patterns inform refusal design — **L3**.
- E6 Documentation review cross-referencing refusal-design changes against specific registered misuse cases, where such controls exist — **L3**.
- E7 Rate/volume monitoring configuration and brand/authority disclaimer design on portable output, as held — **L2/L3**.
- E8 Ownership determination for the misuse question, including a recorded "none" — **L2/L3**.
- E9 Any complaint, incident or third-party-harm record traced to the system's output, if one exists — **L5**.

### Common pitfalls & limitations
- **Designing a test.** There is none. Inventing an adversarial probe here would both misclassify the failure mode — any control failure is a TP-SEC-001/002 finding by the admissibility test — and manufacture a protocol the field does not have. Exceeding the method does not strengthen a ★1 finding.
- **Defaulting to pass where the question was never asked.** Silence is the most likely and most material fail mode; an unrecorded default is a fail, not an out-of-scope pass.
- **Reading the firm's determination first.** Step 2 must precede step 3, or the reviewer's trigger assessment is anchored to the firm's framing of its own deployment — and the canvas's multiple-trigger fail indicator becomes unusable.
- **Accepting a generic register.** A templated list of misuse patterns that could apply to any drafting tool evidences that someone bought a template, not that anyone thought about this deployment. The canvas makes template reproduction an explicit fail indicator.
- **Treating an out-of-scope determination as a weak result.** Many deployments are correctly out of scope by design. A dated, reasoned out-of-scope determination is a clean pass; an undocumented one is a fail even where the substantive answer would have been the same.
- **Folding the question into conduct review.** IRQ-CON-009 addresses harmful output toward the firm's own customer or colleague in ordinary use; this IRQ's direction is an unconnected third party with no relationship to the firm and no visibility into the AI's role. Consumer Duty foreseeable-harm obligations run to the firm's own customers, and the canvas records the gap as genuine rather than stretching the obligation to fit.
- **Interviewing the delivery team only.** Delivery-team authorship without product/risk-owner review is the canvas's named partial condition, and it is invisible unless the owner is asked directly.
- **★1 honesty.** The evidence base is thin and structural rather than incident-documented: no peer-reviewed research addresses this failure mode, and the single verified regulatory anchor addresses the opposite direction of harm. The rating reflects an evidenced field with no accepted testing methodology. Report as expert opinion on the sufficiency of the firm's reasoning, and say so at the point of the conclusion.

### Time/effort estimate
**2.0 reviewer-days** — 0.25 admissibility test and independent trigger assessment; 0.25 applicability-record review and comparison; 0.5 register review and refusal-design mapping; 0.5 product/risk-owner interview and ownership determination; 0.5 compensating-control review and write-up. No environment build, no execution time, no teardown.

---
---

