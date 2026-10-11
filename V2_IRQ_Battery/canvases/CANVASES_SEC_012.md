# CANVAS: IRQ-SEC-012

## 1. IRQ ID & Title
**IRQ-SEC-012: Customer Misuse of Working AI Capability as an Instrument Against a Third Party**

Register question: "For deployments meeting the applicability condition below, has the institution assessed and bounded the risk of its own AI being used by a customer as an instrument against third parties (drafting fraudulent communications, evasion or concealment guidance, social-engineering material) — with misuse cases identified and registered, and refusal and rate controls tested against them?"

**Applicability condition (assessor confirms at scoping — this IRQ is not universal):** In scope only for customer-facing deployments whose outputs are plausibly repurposable by the user as an instrument against a third party. **Non-exhaustive trigger list:** free-text generative output to customers; drafting or document-production capability; guidance responsive to user-described scenarios; output that carries the institution's brand or authority outside the session. Where none of these apply, the assessor records the deployment out of scope for this IRQ, with dated rationale — silence or an unrecorded default is a fail condition at section 13, not a pass.

## 2. Business Activities Affected
- **Customer correspondence and document-drafting assistants:** A tool that drafts letters, disputes, or formal communications on a customer's behalf produces fluent, plausible text that the customer can redirect at an unrelated third party (a fraudulent demand letter, a fabricated reference, a coerced-sounding communication).
- **Guidance and scenario-response tools:** Assistants that respond to a customer's described situation ("how do I structure this to avoid X") can, without any control failing, supply generically accurate guidance that is also usable for evasion or concealment against a counterparty, regulator, or another individual.
- **Brand- or authority-carrying output:** Any output a customer can present outside the session as originating from, or endorsed by, the institution (a generated letter on notional letterhead, an assistant-drafted "explanation" a customer forwards as if institutionally authoritative) carries instrumental value to a third-party recipient independent of the AI provenance being disclosed.

## 3. AI Behaviour(s)
- Generates fluent, task-competent free text in response to a legitimate-seeming customer request, with no distinction in the generation process between a request whose downstream use is benign and one whose downstream use targets an unconnected third party.
- Produces drafting or document-style output that is portable — copyable, forwardable, presentable — outside the session in which it was generated, and outside the firm's own channel of use.
- Responds to scenario-described requests on their own terms (what would help achieve the described goal), without a control layer distinguishing "help the requester" from "help the requester act against someone else."

## 4. Failure Mode
> The AI system's legitimate, working capability — no control has failed, no guardrail has been defeated — is deliberately repurposed by an authorised customer as an instrument against an unintended third party, producing content (a fraudulent communication, evasion or concealment guidance, social-engineering material) that causes harm outside the firm's own customer relationship and outside the firm's normal visibility.

**Misuse-vs-jailbreak boundary (TAXONOMY boundary ruling 16, applied here as the admissibility test for this IRQ):** *Misuse* is the system operating as designed, its legitimate capability repurposed by an authorised user against a third party — homed here, E.5. *Jailbreak* is adversarial defeat of a control — homed at IRQ-SEC-001/002, E.1. The distinguishing question: **did any control fail?** Yes → this is a IRQ-SEC-001/002 finding, not this IRQ. No, and harm arises from the capability working correctly against an unintended target → this IRQ.

## 5. Potential Consequences
- **Third party (not the firm's own customer):** Receives or is targeted by a fraudulent communication, a social-engineering script, or concealment/evasion material that is fluent and plausible precisely because the drafting capability worked as intended; this person has no relationship with the firm and no visibility into the AI's role.
- **Institution:** Reputational and potential legal exposure once the AI's role in producing the instrument surfaces — "the bank's own chatbot helped write the fraud letter" is a materially different, and less defensible, story than a customer's unaided misconduct; brand/authority-carrying output used this way compounds the exposure.
- **Market/regulator:** The CFPB has already evidenced active regulatory attention to chatbot-mediated harm channels in consumer finance (see field 17); an institution unable to show it considered this direction of harm — even having tested for adversarial jailbreak and its own customers' outcomes — presents an incomplete assurance picture at supervisory review.

## 6. Failure Chain
```
Customer (an authorised user, no adversarial intent toward the firm) makes
a legitimate-seeming request within the tool's intended purpose
  ↓ (IRQ-SEC-001 / IRQ-SEC-002: controls hold — this is NOT a jailbreak;
     the capability is working exactly as designed)
System generates fluent, competent, portable output (drafted text, guidance,
a document) in response
  ↓ (IRQ-SEC-012 — THIS IRQ: no misuse-case register or applicability
     assessment exists to have flagged this request pattern)
Customer repurposes the output against an unconnected third party (fraudulent
communication, evasion/concealment guidance, social-engineering material)
  ↓ (no control in this domain is positioned to catch this — SEC-001/002
     test control integrity, not downstream redirection of compliant output)
Harm crystallises to the third party, who has no relationship with the firm
  ↓
Discovered, if at all, via the victim's own complaint, an unrelated
investigation, or press/regulatory attention — not the firm's own monitoring
  ↓
Reputational and regulatory exposure once the AI's role surfaces

Control Breakpoints:
  • IRQ-SEC-012: applicability assessment at scoping; misuse-case register;
    refusal/rate controls tested against registered patterns, where applicable
  • IRQ-GOV-003: conditions of use and brand/authority disclaimer design on
    portable output
  • IRQ-CON-009: the adjacent, distinct control for harmful output toward the
    firm's OWN customer/colleague in ordinary use (not this IRQ's direction)
```

## 7. Why a Domain Expert May Miss It
- Security reviewers test whether controls held — and for this failure mode, they did. Nothing about a standard security review's pass/fail framing surfaces an event where every control worked and harm still occurred to someone outside the session.
- Conduct/complaints SMEs assess harm to the firm's own customer under Consumer Duty; harm the customer causes to an unconnected third party using the firm's tool sits outside that framework's subject, not merely outside its evidence.
- The event genuinely falls between two established review disciplines — security (control integrity) and conduct (own-customer outcome) — with no traditional owner, which is why TAXONOMY boundary ruling 16 was needed to locate it at all rather than fold it into either.
- The closest available regulatory attention (CFPB, field 17) addresses the opposite direction — harm to the firm's own customer from a deficient chatbot — so even a diligent reviewer working from that source alone would not be led to this direction of risk.

## 8. Assurance Objective
**AO-SEC-012:** Where the applicability condition at section 1 is met, the institution shall have identified and registered foreseeable pathways by which its customer-facing AI output could be repurposed by an authorised user as an instrument against a third party, and shall have tested applicable refusal and rate controls against the registered patterns.

## 9. Expected Controls (Traced)
- **Applicability assessment at scoping** — [applicability-conditional by design, confirmed at adoption, 31 Jul 2026] — the assessor actively records an in-scope/out-of-scope determination against the trigger list at section 1, dated; this is the baseline control this IRQ tests for, and its absence (not merely a wrong answer) is itself a fail condition.
- **Misuse-case register** — **Emerging Practice** — no published, cross-institution methodology exists for cataloguing dual-use misuse patterns for customer-facing generative FS tools; the register (foreseeable patterns: fraudulent-communication drafting, evasion/concealment guidance, social-engineering material) is the firm's own documented reasoning, reviewed rather than benchmarked.
- **Refusal design for registered misuse-pattern classes** — [linked IRQ-SEC-001; OWASP Top 10 for LLM Applications 2025, LLM01] — where the register identifies a pattern, refusal/guardrail design extends to it using the same instruction-privilege architecture tested for direct-injection resistance, applied here to a compliant (non-adversarial) request rather than an attack.
- **Rate/volume monitoring on high-risk generative capability** — **Emerging Practice** — no published FS benchmark exists; monitoring for anomalous volume or pattern in drafting-type requests as a coarse signal of potential misuse-at-scale.
- **Brand/authority disclaimer and traceability on portable output** — [linked IRQ-GOV-003; CFPB, "Chatbots in Consumer Finance", 6 June 2023] — output capable of being presented outside the session carries a disclaimer reducing its instrumental value to a third-party recipient who might otherwise treat it as institutionally authoritative.

## 10. Expected Evidence (Tagged L1–L5)
- Vendor/platform assertion that "the system cannot be misused" with no register or rationale — **L1**.
- Dated applicability-assessment record (in-scope or out-of-scope determination against the section 1 trigger list) — **L2**.
- Misuse-case register document naming specific foreseeable patterns for the deployment, where in scope — **L2**.
- Interview record with the product/risk owner (not only the AI delivery team) confirming the applicability determination and, where in scope, that registered patterns inform refusal design — **L3**.
- Documentation review cross-referencing refusal-design changes against specific registered misuse cases, where such controls exist — **L3**.
- Any complaint, incident or third-party-harm record traced to the system's output (if one exists) — **L5**.

## 11. Independent Test
> **None established.** No published, cross-institution testing methodology exists for adversary-free dual-use/misuse assessment of customer-facing generative FS tools — this is stated plainly rather than filled with an invented protocol (this standard's discipline: flag risk and the recognised testing methodology, or its absence, never fabricate one). Assurance activity for this IRQ is limited to: (1) documentation review confirming a dated applicability-assessment record exists against the section 1 trigger list, and, where in scope, that a misuse-case register exists and names specific foreseeable patterns; (2) interview with the product/risk owner to confirm the applicability determination was actively made — not defaulted — and, where applicable, that registered patterns inform refusal design. No adversarial probing, staged payload injection, or other technical test is performed under this IRQ; the reviewer assesses the sufficiency of the firm's own documented reasoning, not system behaviour under test. — **★1 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (the risk is real and structurally evidenced — see fields 17–18 — but no test protocol, published or bespoke, has emerged for this exact class; ★1 reflects an evidenced field with no accepted testing methodology, distinct from a weak or poorly-executed test).

## 12. Pass Indicators
- A dated applicability determination exists against the section 1 trigger list, made by someone with product/risk ownership, not defaulted or silently assumed.
- Where in scope: a misuse-case register exists, is dated, and names specific foreseeable patterns for this deployment (not a generic template).
- Where in scope: refusal design or another compensating control is shown to address at least the registered patterns.
- Interview confirms the product/risk owner, not only the AI delivery team, was involved in the applicability determination.

## 13. Fail Indicators
- No evidence the applicability question was ever asked at scoping — the most likely and most material fail mode, distinct from a wrong-but-documented answer.
- The deployment exhibits multiple section 1 trigger conditions (e.g. customer-facing free-text drafting output) yet no misuse-case register exists.
- A register exists but is generic or templated, with no evidence it reflects this deployment's actual request patterns or trigger conditions.
- No function claims ownership of the misuse question — security confirms controls held and conduct confirms the firm's own customer was not harmed, and the gap between the two is never closed.

## 14. Reporting Language
**Pass:** "Applicability was assessed at scoping against the E.5 trigger list and confirmed [in scope / out of scope], with dated documentation and product/risk-owner sign-off. [Where in scope:] A misuse-case register identifies [n] foreseeable patterns, and interview confirms these inform refusal design. No independent test methodology exists for this class (★1); this finding rests on documentation review and interview only, and should be read as evidence of process rigour, not of demonstrated resistance to misuse."

**Fail:** "No evidence exists that applicability was assessed at scoping, despite the deployment exhibiting [n] of the section 1 trigger conditions (e.g. free-text customer-facing drafting output). No misuse-case register exists. This is a structural gap: the deployment's exposure to repurposing by an authorised user against a third party has not been considered by either the security function (which tests control integrity, not repurposing of working capability) or the conduct function (which tests harm to the firm's own customer, not to an unconnected third party)."

**Partial:** "Applicability was assessed and confirmed in scope, and a misuse-case register exists, but interview evidence indicates it was produced by the delivery team without product/risk-owner review, and no refusal design has yet been mapped to the registered patterns. The assurance objective is not met until ownership and refusal-design mapping are demonstrated."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (harm falls principally on an unconnected third party, not the firm's own
              customer or the firm directly; moderated upward only if brand/authority
              provenance surfaces and compounds reputational exposure)
  Likelihood: 2 (plausible wherever the applicability condition genuinely bites; deliberately
              not universal — many deployments are correctly out of scope by design)
  Detectability: 3 (surfaces via the victim's own complaint or an unrelated investigation,
              not the firm's own monitoring, since the third party has no relationship
              with the firm and no control fails to generate an internal signal)
  Recoverability: 2 (once identified, reversible via register-building and refusal-design
              remediation; moderate reputational cost)
  Novelty: 4 (sits in the conceptual gap between security — tests control integrity — and
              conduct — tests the firm's own customer's outcome; a dedicated boundary
              ruling (TAXONOMY ruling 16) was required to locate this risk at all)

Interpretation: acceptable residual risk where the applicability assessment is genuinely
performed and, where in scope, a register and refusal design exist. Highest concern:
Novelty combined with the thin, structural evidence base (one non-financial-services
incident, none located in a customer-facing financial-services tool)
— reflected in the ★1 rating — meaning this control area depends more on the assessor's
own reasoning than on a benchmarked test.

If controls are absent or degraded:
  Severity: 3 (brand/authority-carrying output used as an effective instrument against a
              third party; discovered only when it becomes a reputational or regulatory
              incident, with no internal warning beforehand)
  Likelihood: 3 (fluent generative drafting/guidance capability is common in customer-facing
              deployment and requires no adversarial skill from the customer to repurpose)
  Detectability: 4 (silent by construction — no control fails, so no security signal fires;
              discovery is external, typically via the victim or a third-party channel)
  Recoverability: 3 (register-building and refusal design after the fact, plus reputational
              repair once the AI's role is public)
  Novelty: 4
Residual risk: Critical where the applicability condition is met and unaddressed; genuinely
not applicable, and therefore not a finding, where the deployment carries none of the
section 1 trigger conditions.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Harm falls principally on an unconnected third party rather than the firm's own customer or the firm directly; moderated upward only where brand/authority provenance surfaces. |
| **Likelihood** | 2 | Plausible wherever the applicability condition genuinely bites; deliberately not universal, per the assessor-confirmed scoping condition at section 1. |
| **Detectability** | 3 | Surfaces via the victim's own complaint or an unrelated investigation, not the firm's own monitoring — no control fails, so no internal signal is generated. |
| **Recoverability** | 2 | Reversible via register-building and refusal-design remediation once identified; moderate reputational cost. |
| **Novelty** | 4 | Sits in the conceptual gap between security (control integrity) and conduct (own-customer outcome); required a dedicated taxonomy boundary ruling to be locatable at all. |

## 17. Regulatory Basis
> No UK regulation directly addresses the harm this IRQ tests. [FCA, PRIN 2A Consumer Duty, in force 31 July 2023] foreseeable-harm obligations run to the firm's own customers, not to unconnected third parties harmed by a customer's downstream misuse of the firm's tool — this is recorded as a genuine regulatory gap, not stretched to fit. [CFPB, "Chatbots in Consumer Finance", 6 June 2023, consumerfinance.gov] was verified against the primary source at consumerfinance.gov on 1 August 2026: it documents that deficient chatbots preventing access to live human support "can lead to law violations, diminished service, and other harms," and that inaccurate information or failure to recognise dispute/complaint signals engages federal consumer-financial-law obligations. Its own finding addresses harm to the firm's **own** customer — the opposite direction to the third-party misuse this IRQ tests — so it is cited as evidence of active regulatory attention to chatbot-mediated harm channels generally, not as direct authority for the specific direction tested here.

## 18. Research Basis
> One peer-reviewed study bears on this IRQ in part: [Hou et al., 2026, "FinSafetyBench: Evaluating LLM Safety in Real-World Financial Scenarios," Findings of the Association for Computational Linguistics: ACL 2026, pp. 14181–14208] is a bilingual (English–Chinese) red-teaming benchmark, with a released dataset, that tests whether a model refuses requests that violate financial compliance, across 14 subcategories of financial crime and ethical violation and under three attack settings. It tests model refusal and not misuse against third parties as such; its attack settings test whether a refusal can be defeated, which is the jailbreak side of the boundary at section 4, so it bears on this IRQ only through refusal design. It does not test a deployed customer-facing tool, a misuse-case register, rate or volume controls, or the repurposing of a legitimate output, and it is partial evidence on the refusal limb only (read 7 October 2026). Beyond that limb, no peer-reviewed research was located that specifically addresses AI-enabled dual-use misuse of customer-facing financial-services generative tools against third parties; this is recorded as a genuine evidentiary gap rather than filled with an adjacent-but-inapplicable citation. The CFPB report at section 17 is the only verified regulatory anchor for this IRQ and is limited as described there. **[FAIAS Incident Register, row 85, "North Korean remote-worker fraud using Claude", 2025]**, citing [Anthropic, 2025, "Detecting and countering misuse of AI: August 2025," 27 August 2025] — the provider reports that operatives used its model to build false identities, pass technical assessments and do the work, in order to secure and keep remote jobs at US technology companies, so a provider's working capability was used by its users against third parties. The victims were employers and the case is not financial-services; the report does not say whether any control failed, which the boundary test at section 4 requires, so it evidences the mechanism and is not classified as misuse or jailbreak here. This thin evidence base — structural plausibility with one documented non-financial-services instance, and no incident or research corpus located for a customer-facing financial-services tool — is the basis for the ★1 rating (as distinct from ★2, "research exists, method bespoke") and is recorded plainly rather than inflated.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-SEC-001 (E.1: direct jailbreak — the control-failure boundary this IRQ is
    distinguished from per TAXONOMY ruling 16; did a control fail?)
  - IRQ-SEC-002 (E.1: multi-turn jailbreaks — same boundary distinction)
  - IRQ-CON-009 (H.2: unprompted harmful output toward the firm's OWN customer/colleague in
    ordinary use — the adjacent, distinct control; this IRQ's direction is a third party,
    not the firm's own customer)
  - IRQ-GOV-003 (I.2: conditions of use and technical enforcement — brand/authority
    disclaimer design on portable output)
```

## 20. References
```
[1] Consumer Financial Protection Bureau, 2023. "Chatbots in Consumer Finance."
    consumerfinance.gov/data-research/research-reports/chatbots-in-consumer-finance/.
    Published 6 June 2023. Verified 1 August 2026.
[2] FCA, 2022. "PS22/9: A New Consumer Duty"; PRIN 2A in force 31 July 2023.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: E.5 (Security domain, Misuse & Dual-Use) — NEW subdomain, applicability-conditional
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Misuse of a working system falls between security (tests whether
  controls held — they did) and conduct (tests harm to the firm's own customer — this
  targets someone else); neither function owns it without the dedicated taxonomy ruling.
✓ Test 2 (Plausible Harm): Evidence base is thin and structural: one non-financial-services
  incident is recorded (incident register, row 85) and none was located in a customer-facing
  financial-services tool — CFPB (6 Jun 2023) evidences active regulatory attention to
  chatbot-mediated consumer-finance harm generally, though not this exact direction;
  FinSafetyBench (Findings of ACL 2026) evidences that adversarial prompts can bypass a
  model's financial-compliance refusals, which is partial evidence on the refusal limb
  only; rated ★1 accordingly, not asserted as heavily evidenced.
✓ Test 3 (Testable): Partially — answerable via documentation review of the misuse-case
  register and interview, not adversarial testing; no published protocol exists, stated
  plainly rather than invented.
✓ Test 4 (Decision-Relevant): Yes, but conditionally — gates deployment only where the
  applicability condition at section 1 is met; the assessor confirms applicability at
  scoping, and an unrecorded default is itself a fail condition.

Change Log:
- v1.0 (2026-08-01): Initial publication as part of the v1.0.3 batch. New subdomain E.5,
  applicability-conditional by design (confirmed at adoption, 31 Jul 2026) and
  TAXONOMY boundary ruling 16 (misuse vs jailbreak: did a control fail?). Four tests passed,
  with the Test 2 thin-evidence-base caveat recorded explicitly rather than smoothed over.
- v1.3.3 (2026-10-09): Fields 15, 18 and 21 — FinSafetyBench (Findings of
  ACL 2026) added as partial evidence on the refusal limb only, with its limits; the
  statement that no peer-reviewed research addresses the IRQ qualified accordingly; the CFPB
  report described as the only verified regulatory anchor; incident register row 85 cited
  as a non-financial-services instance of the mechanism, with the financial-services gap
  kept. Research-basis review date moved. ★1 unchanged.
```

---
---

