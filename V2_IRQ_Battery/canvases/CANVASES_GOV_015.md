# CANVAS: IRQ-GOV-015

## 1. IRQ ID & Title
**IRQ-GOV-015: External Capability Claims Exceeding the Validated Envelope**

Register question: "Are the firm's external representations about AI capability — marketing, product disclosures, RFP and due-diligence responses, investor communications — substantiated by, and periodically reconciled against, the system's validated capability envelope and documented limitation statements?"

## 2. Business Activities Affected
- **Marketing and product disclosure:** any public or customer-facing description of what an AI system can do is a candidate for this control, regardless of channel.
- **Sales, RFP and due-diligence responses:** capability claims made to prospective clients or counterparties in a procurement or diligence process carry the same substantiation risk as marketing material, with the added exposure of a written, retained record.
- **Investor communications:** capability claims made to investors or analysts are subject to the same drift risk, with disclosure-accuracy consequences distinct from, and additional to, customer-facing exposure.

## 3. AI Behaviour(s)
- N/A at the model-behaviour level — this IRQ concerns the firm's external representations about the system, not the system's own outputs.
- The system's actual validated capability envelope and documented limitations change as the system is retrained, reconfigured or has its scope altered, independent of whether external claims are updated to match.

## 4. Failure Mode
> The firm's external representations about AI capability — in marketing, product disclosures, RFP responses or investor communications — exceed what the system's validated capability envelope and documented limitations actually support, with no reconciliation process to detect or correct the drift once the claim is published.

## 5. Potential Consequences
- **Customer/counterparty:** relies on a stated capability that has not been validated to that extent, encountering unexpected failure in a context the firm represented as covered.
- **Institution:** enforcement exposure for unsubstantiated capability claims, reputational damage, and RFP or due-diligence responses proving inaccurate under later scrutiny.
- **Regulator/market:** enforcement action against capability marketing generally increases supervisory attention to AI disclosures across the sector, raising scrutiny of any firm unable to substantiate its own claims.

## 6. Failure Chain
```
AI system validated to a defined capability envelope and limitation statement at
go-live
  ↓ (IRQ-GOV-009: documentation records the envelope, but does not itself
  reconcile it against external claims)
Marketing, sales, RFP and investor-relations teams draft external
representations of system capability, typically independently of the
validation record
  ↓ (IRQ-GOV-015 — THIS IRQ: no reconciliation process links external claims
  back to the validated envelope)
System is retrained, reconfigured or its scope narrowed; the validated
envelope changes, but the external claim is not updated to match
  ↓
External claim now exceeds what validation supports, undetected
  ↓
Customer, counterparty or investor relies on the claim → capability gap
surfaces in use, complaint, or due-diligence audit → supervisory or
enforcement scrutiny of unsubstantiated capability claims → reputational and
enforcement exposure

Control Breakpoints:
  • IRQ-GOV-009: documented capability envelope and limitation statement
    exists to reconcile against
  • IRQ-GOV-015: reconciliation process links external claims to the
    validated envelope, before publication and periodically thereafter
  • IRQ-GOV-011: regulatory obligation mapping identifies which external
    claims carry disclosure-accuracy obligations
```

## 7. Why a Domain Expert May Miss It
- Capability claims are typically owned by commercial, marketing or investor-relations teams with no structural link to the technical validation record, so a governance reviewer checking "is the envelope documented" (GOV-009) will not by itself surface whether external claims still match it.
- A claim can be true at launch and drift silently as the system is retrained or its scope changes; the claim itself carries no expiry or version marker to prompt review.
- "The system is validated" and "what we say about the system is validated" read as the same assurance question but are structurally different controls — the first tests the internal record, the second tests whether anyone reconciles the outward-facing statement against it.
- Capability-marketing claims are conventionally reviewed for general misleading-statement risk rather than for AI-specific substantiation against a technical validation record, so an AI-specific gap can pass a standard commercial-compliance review unchallenged.

## 8. Assurance Objective
**AO-GOV-015:** The firm's external representations of AI capability shall be substantiated by, and periodically reconciled against, the system's validated capability envelope and documented limitation statements, before publication and on a defined cycle thereafter.

## 9. Expected Controls (Traced)
- **Documented capability envelope and limitation statement per system, maintained current** — [linked IRQ-GOV-009].
- **Reconciliation process linking external capability claims (marketing, product disclosure, RFP/due-diligence response, investor communication) to the validated envelope before publication** — [Emerging Practice] — no published methodology for this specific reconciliation control was identified; the control follows from the enforcement pattern evidenced in the Regulatory Basis below, rather than from a prescriptive published standard.
- **Periodic, not only pre-publication, reconciliation cycle, to catch drift where the underlying envelope changes after a claim is published** — [Emerging Practice].
- **Named ownership for the reconciliation process, distinct from marketing/investor-relations ownership of the claim itself** — [linked IRQ-GOV-001 ownership principle, extended].
- **Correction or retraction process where reconciliation finds a claim exceeds the validated envelope** — [Emerging Practice].

## 10. Expected Evidence (Tagged L1–L5)
- Statement that "the system is validated and documented" — **L1** (asserts an internal record exists; does not evidence that external claims are reconciled against it).
- Documented capability envelope and limitation statement — **L2**.
- Reconciliation process documentation defining scope, cadence and ownership — **L2**.
- Sample trace of external materials (marketing, an RFP or due-diligence response, an investor communication) back to the validated envelope, confirming each sampled claim is substantiated — **L3**.
- Correction or retraction records where drift was found and corrected — **L3/L4**.
- Evidence from an actual historical instance where reconciliation caught and corrected an overreaching claim before or after publication — **L5**.
- **Worked example — the substantiating source can change after the claim is made, 8–10 September 2026 (OpenAI, "On the Navier–Stokes Millennium Prize Problem"; the disclosure analysis is held at IRQ-GOV-009 Field 10 and is not restated here).** A published research page was amended two days after publication; the amendment is disclosed in a dated footnote naming the amended section, but the removal of a hedge sentence from that section is not, and is establishable only by comparing an archived capture against the live page. For this canvas the consequence is narrow and specific: where an external capability or data-use claim in a firm's own marketing, product disclosure, RFP response or investor communication is substantiated by reference to a third-party page, the reconciliation record must fix the substantiating text at a date, because a periodic re-reconciliation performed against the *current* page can silently pass a claim whose basis has moved. Expected evidence: the reconciliation record names the substantiating source, the version or capture date relied on, and a hash or archived copy — **L3**.

## 11. Independent Test
> Reviewer selects a sample of external-facing capability claims (marketing material, a recent RFP or due-diligence response, an investor communication) and traces each to the underlying validation evidence, checking whether the claim is substantiated by, and does not exceed, the documented capability envelope and limitation statement. A claim with no traceable basis, or one exceeding what validation established, is a finding. No published testing methodology exists for this as a discipline — stated plainly, not implied; this is a reconciliation/documentation review, not an empirical test, conducted entirely against documentation and sample tracing, with no production system access required. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026) · P2 (§6A.4)** (the enforcement pattern this control addresses is well evidenced — see Regulatory Basis — but no established audit methodology exists beyond documentation review and sample tracing, and no benchmark exists for how closely a claim must sit to the validated envelope).

## 12. Pass Indicators
- Sampled external claims trace to validation evidence and do not exceed the documented envelope.
- A reconciliation process exists, is independently owned, and runs both pre-publication and on a periodic cycle.
- At least one historical instance evidences the reconciliation process catching and correcting drift.
- A correction or retraction route exists and has been used where needed.
- Claims reviewed span marketing, RFP/due-diligence responses and investor communications, not only one channel.

## 13. Fail Indicators
- One or more sampled claims cannot be traced to validation evidence, or exceed the documented envelope.
- No reconciliation process exists; claims are drafted and published with no link to the validation record.
- Reconciliation, where it exists, occurs only at launch and is never repeated as the envelope changes.
- No correction or retraction route exists for claims later found to exceed the envelope.
- Ownership of reconciliation is not distinct from ownership of the claim itself.

## 14. Reporting Language
**Pass:** "Sample tracing confirms external capability claims across marketing, RFP/due-diligence and investor communications are substantiated by, and do not exceed, the documented validated capability envelope. A reconciliation process, independently owned, operates both pre-publication and periodically. Conclusions rest on ★2 methodology — a documentation and sample-tracing review with no published protocol — and should be read as professional assessment of the sample reviewed, not a claim-by-claim audit of every external statement."
**Fail:** "Sample tracing found [n] external capability claims with no traceable basis in the validation record, or exceeding the documented envelope. No reconciliation process links external representations to validation evidence; drift, once introduced, is not detected or corrected. This is a material gap carrying direct enforcement exposure for unsubstantiated capability claims and should be reported as a finding requiring remediation."
**Partial:** "Marketing materials trace correctly to the validated envelope, but a sampled RFP response and an investor communication both contained claims exceeding what validation established, with no reconciliation process covering those channels. The assurance objective is not yet met; remediation should extend the reconciliation process to all external-facing channels and correct the identified claims within [n] days."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (drift is typically corrected before or shortly after
              publication; exposure is reputational and administrative
              rather than direct customer harm in most instances)
  Likelihood: 2 (plausible given claims are typically owned separately from
              validation records, but reduces materially once a
              reconciliation process is deliberately built)
  Detectability: 2 (a scheduled reconciliation cycle catches drift on a
              defined cadence, rather than leaving it to accidental
              discovery)
  Recoverability: 1 (correcting or retracting an external statement is a
              low-cost, fast remedy compared to a technical control failure)
  Novelty: 3 (moderately likely to be missed: commercial and
              investor-relations teams do not naturally treat their own
              claims as an assurance object)

Interpretation: acceptable residual risk once reconciliation is built and run
on a defined cycle; the principal concern is that, absent this IRQ, a firm may
reasonably believe a documented capability envelope (IRQ-GOV-009) itself
constitutes assurance that external claims are accurate, when nothing
requires the two to be reconciled.

If controls are absent or degraded:
  Severity: 3 (enforcement action for unsubstantiated capability claims
              carries direct regulatory and reputational consequence,
              distinct from and additional to any underlying system defect)
  Likelihood: 3 (foreseeable wherever claims are commercially owned with no
              structural link to validation, which is common)
  Detectability: 4 (silent by construction — nothing in routine operation
              signals that a claim has drifted from the validated envelope;
              discovery typically requires external enforcement action, a
              due-diligence audit, or a customer/counterparty dispute)
  Recoverability: 2 (the claim itself can be corrected quickly, but
              enforcement action or reputational damage already triggered by
              an unsubstantiated claim is not retrospectively undone)
  Novelty: 3
Residual risk: Moderate-to-high while unreconciled; low-cost to remediate
once a reconciliation process is built, arguing for routine testing of this
IRQ rather than a one-off check.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 2 | Drift is typically corrected before or shortly after publication; exposure is reputational/administrative rather than direct customer harm in most instances. |
| **Likelihood** | 3 | Probable given capability claims are conventionally owned by commercial/marketing/investor-relations teams with no structural link to the technical validation record. |
| **Detectability** | 4 | Silent by construction — nothing in routine operation signals a claim has drifted from the validated envelope; discovery typically requires external enforcement, audit or dispute. |
| **Recoverability** | 2 | The claim itself is cheaply corrected, but enforcement action or reputational damage already triggered is not retrospectively undone. |
| **Novelty** | 3 | Moderately likely to be missed — commercial teams do not naturally treat their own external statements as an assurance object subject to technical reconciliation. |

## 17. Regulatory Basis
> SEC enforcement actions against unsubstantiated AI capability claims (AI-washing), as recorded in the incident register, evidence that regulators are prepared to act directly on the gap between external AI-capability representations and what a firm has actually validated. **[FAIAS Incident Register, row 15, "SEC AI-washing orders — Delphia and Global Predictions", 2024]**, citing [Securities and Exchange Commission, *In the Matter of Delphia (USA) Inc.*, Investment Advisers Act of 1940 Release No. 6573, Administrative Proceeding File No. 3-21894, 18 March 2024] and [Securities and Exchange Commission, *In the Matter of Global Predictions, Inc.*, Investment Advisers Act of 1940 Release No. 6574, Administrative Proceeding File No. 3-21895, 18 March 2024] — the two settled orders behind that pattern, each entered on the firm's offer of settlement and to which the firm consented without admitting or denying the findings, and each finding a capability representation the firm's own systems did not support: the first that from at least August 2019 to August 2023 the adviser "represented that it used artificial intelligence and machine learning to analyze its retail clients' spending and social media data to inform its investment advice when, in fact, no such data was being used in its investment process", and the second that the adviser claimed on its website that its technology incorporated "'[e]xpert AI-driven forecasts,' when in fact it did not" and, on a separate claim, "could not produce documents to substantiate this claim". **[FAIAS Incident Register, row 46, "FTC final order against DoNotPay, Inc.", 2025]**, citing [Federal Trade Commission, *In the Matter of DoNotPay, Inc.*, File No. 232-3042, Docket No. C-4812, Complaint Count I and Decision and Order; press release of 11 February 2025] — a second United States regulator acting on the same gap, under consumer-protection rather than securities law and on a different product class, and reaching the point this question turns on. Count I is pleaded as "False or Unsubstantiated Performance Claims": that the respondent represented that "the Service's artificial intelligence and other technology operates like a human lawyer, including by applying the relevant laws to subscribers' particular legal and factual situations", and that those representations "are false or misleading or were not substantiated at the time the representations were made". According to the complaint as the Commission summarises it, the firm "did not test whether its 'AI lawyer' operated to the level of a human lawyer when generating legal documents and giving advice", and "did not hire or retain attorneys to test the quality and accuracy of its service's law-related features" — the alleged absence of validation is itself the charged defect, not merely evidence of one. The final order "requires DoNotPay to pay $193,000 in monetary relief and notify consumers who subscribed to the service between 2021 and 2023", and "prohibits DoNotPay from advertising that its service performs like a real lawyer unless it has sufficient evidence to back it up"; the Commission "voted 5-0 on January 16, 2025, to approve the final order"; the order was entered by consent, DoNotPay neither admitting nor denying the complaint's allegations, and no violation was adjudicated. Recorded precisely: the counts are consumer-protection deception counts and no finding of unauthorised practice of law was made, although the complaint records at ¶¶25 and 27 that the State Bar of California opened an unauthorised-practice investigation on or about 16 November 2021 and sent a cease-and-desist notice on 15 June 2023. No UK/EU regulatory instrument specifically requiring reconciliation between AI-capability claims and a validated capability envelope was identified in the verified source set; this control area rests on the enforcement pattern above as a cross-jurisdictionally instructive precedent rather than a UK/EU binding instrument, and this gap is stated openly rather than a UK/EU anchor being invented.

## 18. Research Basis
> No peer-reviewed literature specifically evaluating reconciliation between AI capability claims and validated capability envelopes was identified in the source registers; this control area is enforcement-pattern-led (see Regulatory Basis) rather than research-led, consistent with the Governance domain's wider evidentiary profile.
>
> **Research basis last reviewed:** 1 August 2026 · **review cadence:** Standard (12 months)

## 19. Related IRQs
```
  - IRQ-GOV-009 (I.4: documentation adequacy — supplies the validated
    capability envelope and limitation statement this IRQ reconciles claims
    against)
  - IRQ-GOV-011 (I.4: regulatory obligation mapping — identifies which
    external claims carry disclosure-accuracy obligations)
  - IRQ-MOD-001 (B.1: capability/limitation testing — supplies the underlying
    validation evidence this IRQ traces claims back to)
```

## 20. References
```
[1] SEC enforcement actions against unsubstantiated AI capability claims
    (AI-washing), as recorded in the incident register at row 15.
[2] Securities and Exchange Commission, 2024. "In the Matter of Delphia
    (USA) Inc." Investment Advisers Act of 1940 Release No. 6573;
    Administrative Proceeding File No. 3-21894.
    Published: 18 March 2024
    URL: https://www.sec.gov/files/litigation/admin/2024/ia-6573.pdf
[3] Securities and Exchange Commission, 2024. "In the Matter of Global
    Predictions, Inc." Investment Advisers Act of 1940 Release No. 6574;
    Administrative Proceeding File No. 3-21895.
    Published: 18 March 2024
    URL: https://www.sec.gov/files/litigation/admin/2024/ia-6574.pdf
[4] Federal Trade Commission, 2025. "In the Matter of DoNotPay, Inc."
    Complaint; Docket No. C-4812; File No. 232-3042.
    Issued: 14 January 2025
    URL: https://www.ftc.gov/system/files/ftc_gov/pdf/2323042_donotpay_complaint.pdf
[5] Federal Trade Commission, 2025. "In the Matter of DoNotPay, Inc."
    Decision and Order; Docket No. C-4812; File No. 232-3042.
    Issued: 14 January 2025
    URL: https://www.ftc.gov/system/files/ftc_gov/pdf/2323042_donotpay_decision_and_order_0.pdf
[6] Federal Trade Commission, 2025. "FTC Finalizes Order with DoNotPay
    That Prohibits Deceptive 'AI Lawyer' Claims, Imposes Monetary Relief,
    and Requires Notice to Past Subscribers." Press release.
    Published: 11 February 2025
    URL: https://www.ftc.gov/news-events/news/press-releases/2025/02/ftc-finalizes-order-donotpay-prohibits-deceptive-ai-lawyer-claims-imposes-monetary-relief-requires
[7] OpenAI, 2026. "On the Navier–Stokes Millennium Prize Problem." Web page.
    Published: 8 September 2026 (updated 10 September 2026)
    URL: https://openai.com/index/navier-stokes-solution/
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: I.4 (Governance domain, Documentation, Records & Regulatory)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): capability claims are commercially owned with no
  structural link to the technical validation record, so a documentation
  review of "does the envelope exist" (GOV-009) does not by itself surface
  whether external claims still match it.
✓ Test 2 (Plausible Harm): grounded in the established SEC enforcement
  pattern against unsubstantiated AI capability claims, as recorded in the
  incident register.
✓ Test 3 (Testable): testable via sample tracing of external claims to
  validation evidence. ★2 methodology, honestly caveated — no published
  protocol exists.
✓ Test 4 (Decision-Relevant): outcome bears on enforcement exposure
  independent of whether the underlying AI system itself passes every other
  IRQ.

Change Log:
- v1.0 (2026-07-31): Initial publication; all four tests passed.
- v1.2.0 (2026-09-12): Field 10 — the OpenAI Navier–Stokes page amendment of 10 Sep 2026 added as a worked example of a substantiating third-party source changing after a claim is made, carried here as the derivative outbound-claims consequence only (the disclosure analysis sits at IRQ-GOV-009 Field 10), with the expectation that a reconciliation record fixes the substantiating text at a version or capture date. ★2 unchanged.
- v1.2.1 (2026-09-19): Field 17 — incident-register citations added in the reserved form. Row 15 is named for the first time, with the two settled Investment Advisers Act orders of 18 March 2024 behind the enforcement pattern this control area rests on; row 46 is added as a second United States regulator acting on AI capability claims alleged to be unsubstantiated and untested, under consumer-protection rather than securities law, with the counts recorded as consumer-protection deception counts, the order recorded as entered by consent with the allegations neither admitted nor denied, and no unauthorised-practice finding. Field 20 — reference entries added for the two orders and for the Federal Trade Commission's complaint, decision and order, and press release, and entry [1] given its pinpoint. No change to controls, test, ★2 or risk profile.
- v1.3.2 (2026-10-03): Corrections listed in 00_Admin/CORRECTION_LOG_2026-10-03.md §8; no change to the ★ rating or the risk profile.
```

---
---

