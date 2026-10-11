# CANVAS: IRQ-AGT-009

## 1. IRQ ID & Title
**IRQ-AGT-009: Behaviour-Altering Prompt Content Managed Outside Controlled Configuration**

Register question: "Does agent behaviour depend on undocumented intermediate reasoning artefacts or prompt content, such that a prompt change alters behaviour without any code change — and is prompt text managed as controlled configuration?"

## 2. Business Activities Affected
- **Any customer-facing or decision-supporting agent:** System prompts, tool-use instructions and reasoning scaffolds materially determine agent behaviour; an uncontrolled change to any of these can alter customer-facing conduct or decision quality without a corresponding code deployment being visible to change-management processes.
- **AML/fraud triage agents:** Subtle prompt wording changes (e.g. adjusting how "suspicious" is defined in an instruction) can shift triage thresholds across an entire caseload without a model or code change being logged as the cause.
- **Regulatory/compliance-adjacent copilots:** Prompt-embedded compliance instructions (disclosure requirements, prohibited statements) constitute de facto policy; if not version-controlled, a change to this "policy" can occur without any of the change-approval processes applied to genuine policy updates.

## 3. AI Behaviour(s)
- Behaviour is materially shaped by the system prompt, tool-use instructions and any reasoning scaffold (e.g. chain-of-thought prompting templates) supplied at runtime, in addition to the underlying model weights.
- A small, seemingly cosmetic change to prompt wording can produce materially different downstream behaviour, disproportionate to the size of the textual change.
- The model's own stated reasoning (chain-of-thought) may not faithfully reflect the actual factors driving its output, meaning even inspecting the reasoning trace does not reliably reveal which prompt element caused a given behaviour.

## 4. Failure Mode
> Agent behaviour depends materially on prompt text, tool-use instructions or reasoning scaffolds that are not managed as version-controlled, approved configuration — so a prompt change can alter customer-facing or decision-relevant behaviour with the same materiality as a code or model change, but without passing through the change-control, testing and approval processes applied to those.

## 5. Potential Consequences
- **Customer:** An undocumented prompt edit shifts triage thresholds, disclosure content or decision criteria, affecting customer outcomes with no corresponding record of what changed or why.
- **Institution:** Loss of the ability to reconstruct why an agent behaved differently at two points in time, since "nothing changed" in the code or model version history when in fact the prompt did; audit and incident-investigation capability is degraded.
- **Regulator/market:** Inability to demonstrate change-control discipline over a component that materially determines regulated-activity behaviour; supervisory concern that "prompt engineering" operates outside the firm's model risk and change-management framework.

## 6. Failure Chain
```
Prompt/instruction text is edited by an engineer or product owner as a
routine tweak, outside formal change control (no version tag, no
regression test, no approval record)
  ↓ (IRQ-AGT-009 — THIS IRQ: prompt not managed as controlled configuration)
Agent behaviour materially shifts (e.g. triage threshold, disclosure
wording, tool-use pattern) as a direct result
  ↓ (IRQ-MOD-013: no regression testing was triggered because the change
     was not recognised as a "model change")
Shift in behaviour affects a batch of customer interactions before
anyone notices, because monitoring baselines assume model/code version
is the only driver of behaviour change
  ↓ (IRQ-GOV-008: monitoring signals do not distinguish prompt-driven
     drift from model drift)
Customer harm or compliance gap emerges; investigation cannot readily
identify the cause, since version-control records show no code/model change
  ↓
Complaint or audit finding → forensic reconstruction discovers the
undocumented prompt edit → governance and change-control failure identified

Control Breakpoints:
  • IRQ-AGT-009: prompts/scaffolds version-controlled as behaviour-bearing
    configuration
  • IRQ-MOD-013: regression testing triggered by any prompt/config change,
    not only model/code changes
  • IRQ-GOV-008: monitoring capable of attributing behavioural drift to its
    actual source, including prompt changes
```

## 7. Why a Domain Expert May Miss It
- Traditional change management distinguishes "code changes" (subject to release process) from "content" or "copy" changes (often treated as low-risk, marketing-adjacent edits); prompt text is frequently perceived and handled as the latter, even though for a generative agent it functions as the former.
- SMEs reviewing model risk typically ask "has the model changed?" — a version-pinned, well-understood question — and may not think to ask "has any prompt or scaffold the model runs against changed?", which is a materially different and often unrecorded question.
- The disproportionate sensitivity of LLM behaviour to small wording changes is counter-intuitive to anyone used to traditional software, where a small text edit rarely has large behavioural consequences.
- Testing gap: regression test suites triggered by code/model deployments will not run if a prompt change is deployed through a separate, lighter-weight content-management path.

## 8. Assurance Objective
**AO-AGT-009:** All behaviour-bearing artefacts — system prompts, tool-use instructions and reasoning scaffolds — shall be managed as version-controlled, documented configuration subject to the same change-control and regression-testing discipline as code or model changes.

## 9. Expected Controls (Traced)
- **Version control and change-approval for all prompt/scaffold artefacts** — [linked IRQ-MOD-013; NIST AI RMF 1.0, Jan 2023, MANAGE function] — prompts are stored, versioned and change-approved with the same rigour as code, closing the "content vs code" gap.
- **Behavioural regression testing triggered by any prompt/scaffold change** — [linked IRQ-MOD-013; Chen et al., "How Is ChatGPT's Behavior Changing over Time?", 2023, arXiv:2307.09009; Harvard Data Science Review 6(2), 2024, demonstrating that behaviour drifts materially with configuration/version changes even absent a stated model change] — a defined regression suite runs before any prompt change reaches production.
- **Monitoring capable of attributing behavioural drift to its source (model, code, or prompt/config)** — [linked IRQ-GOV-008, IRQ-RES-005/006; PRA SS1/23 ongoing monitoring principle] — drift-detection tooling distinguishes which layer changed, rather than assuming model version stability implies behavioural stability.
- **Explicit caveat on reliance on model-stated reasoning as an oversight control** — [Anthropic, "Reasoning Models Don't Always Say What They Think," Apr 2025; OpenAI, "Detecting Misbehavior in Frontier Reasoning Models," Mar 2025] — any control relying on chain-of-thought inspection documents that stated reasoning may not faithfully reflect actual drivers of behaviour.
- **Change-log linkage between prompt versions and observed behavioural test results** — [linked IRQ-GOV-009 documentation standard] — each prompt version is traceable to the regression evidence that supported its approval.

## 10. Expected Evidence (Tagged L1–L5)
- Assertion that "prompts are just configuration, low risk" — **L1** (flag: materiality not assessed).
- Documentation of the prompt/scaffold inventory, version history and change-approval process — **L2**.
- Repository/config inspection confirming prompts are actually stored under version control with access-controlled change history (not edited ad hoc in a live console) — **L3**.
- Staging regression test results comparing behaviour before/after a representative prompt change, across the defined test suite — **L3**.
- Independent audit confirming change-control discipline is applied consistently across all agents, not only flagship deployments — **L4**.
- Production monitoring data: behavioural drift signals correlated with prompt-version change timestamps, demonstrating attribution capability — **L5**.

**Dated worked example, added at the September 2026 refresh — behaviour-altering content changed outside any configuration-control path.** A disclosed vulnerability in a locally deployed agent stack (CVE-2026-65105, reported 25 August 2026) let a remote page rewrite the Go template that renders the structured message array into the raw text the model actually receives: the rewrite "survives client-supplied system prompts" and "is invisible to the user: the model's name, size, metadata, and capabilities appear unchanged", persisting across all subsequent conversations. The entry path was an inference server bound to a non-loopback address, where "the Host header validation is skipped entirely", combined with DNS rebinding [Cyera, "Drive-By Agent Hijacking", 25 August 2026]. Two things a reviewer should take from it: behaviour-altering content is not only the system prompt a firm wrote — it includes the rendering layer beneath it, which this canvas's inventory (§10, L2) will not list unless it is asked to; and a change of this kind produces no prompt-version timestamp for the L5 attribution evidence to correlate against. The rewritten template also persists across every subsequent conversation, so the poisoned artefact behaves as retained state between sessions — which is IRQ-AGT-008's subject, cross-referenced there rather than re-tested here.

## 11. Independent Test
> In a non-production environment, apply a set of representative, individually plausible prompt edits (e.g. rewording a risk-triage instruction, adjusting a disclosure template, modifying a tool-use instruction) one at a time to a staging copy of the agent. Run the firm's standard behavioural regression suite before and after each edit and measure the magnitude of behavioural change per edit. Separately, confirm whether the change-management system in use for prompts would have required version control, testing and approval for each edit, or whether it could have been deployed through a lighter-weight content path. Methodology informed by Chen et al.'s empirical demonstration that LLM behaviour drifts materially with configuration change over time. No production customers or live traffic used. — **★2 Confidence — as at FAIAS v1.1.0 (25 August 2026)** (Chen et al. provides credible empirical grounding for prompt/config sensitivity; the specific test of "would this change have bypassed governance" is bespoke to the firm's own change-management tooling, with no external benchmark).

## 12. Pass Indicators
- Every prompt/scaffold artefact is under version control with a documented, approved change history.
- Regression testing runs automatically before any prompt change reaches production, with results retained and linked to the version.
- Monitoring can attribute a behavioural drift signal to a specific prompt-version change when one occurs.
- No prompt change in the test set could be deployed via a path that bypasses version control and regression testing.

## 13. Fail Indicators
- Any prompt/scaffold change can be deployed to production without version control, approval or regression testing (a "content" path bypassing governance).
- Behavioural regression testing is not run, or is run only for code/model releases, missing prompt-only changes.
- Monitoring cannot distinguish a prompt-driven behavioural shift from genuine model drift, misattributing the cause during incident investigation.
- No documented change history exists for the current production prompt/scaffold set.

## 14. Reporting Language
**Pass:** "All system prompts, tool-use instructions and reasoning scaffolds are managed under version control with documented change approval and automated behavioural regression testing before deployment. Testing of [n] representative prompt edits confirms no path exists to bypass this governance. This is a ★2 assessment — credible empirical grounding, bespoke governance-bypass testing — and should be re-verified whenever the prompt deployment tooling changes."

**Fail:** "Testing found that prompt and scaffold text can be edited and deployed to production through a content-management path that bypasses version control, regression testing and change approval entirely. A representative test edit produced a material shift in triage/disclosure behaviour with no corresponding entry in the model or code change log. This creates an unrecoverable audit and accountability gap and should be remediated by bringing all behaviour-bearing prompt artefacts under the same change-control discipline as code."

**Partial:** "Version control and regression testing are enforced for the primary customer-facing agent's prompts but not for internal-tool-use instructions embedded in the same deployment, which remain editable outside governance. Remediation should extend the same controls to all behaviour-bearing artefacts."

## 15. Residual Judgement
```
Assuming controls are well-implemented and monitored:
  Severity: 2 (behavioural drift bounded and quickly attributable; limited to
              the scope of a controlled, tested change)
  Likelihood: 2 (requires the version-control/regression pipeline to be
               bypassed or incomplete)
  Detectability: 2 (drift-attribution monitoring surfaces prompt-driven change
                    promptly where implemented)
  Recoverability: 2 (rollback to a prior approved prompt version is
                     straightforward once version control exists)
  Novelty: 3 (requires recognising prompt text as behaviour-bearing
              configuration equivalent to code, a non-obvious reframing)

Interpretation: acceptable once prompts are brought under the same governance
discipline as code; highest residual concern is organisations treating this as
a documentation exercise rather than a technically enforced control.

If controls are absent or degraded:
  Severity: 3 (undocumented, potentially widescale shifts in customer-facing
              triage, disclosure or decision behaviour)
  Likelihood: 3 (foreseeable wherever a lighter-weight content path exists
               alongside formal code release — a common organisational pattern)
  Detectability: 3 (surfaces via customer complaint or downstream audit rather
                    than real-time monitoring, absent attribution tooling)
  Recoverability: 2 (once the causal prompt edit is identified, reversal is
                     usually straightforward)
  Novelty: 3
Residual risk: High. Bringing prompts under version control and regression
testing should be a standard deployment-governance requirement, not optional.
```

## 16. Risk Weighting Profile (5 Axes, 1–4)
| Axis | Rating | Justification |
|---|---|---|
| **Severity** | 3 | Undocumented shifts in customer-facing triage, disclosure or decision behaviour can affect a broad caseload before detection. |
| **Likelihood** | 3 | Foreseeable wherever a lighter-weight content-deployment path coexists with formal code release governance — a common, not rare, organisational pattern. |
| **Detectability** | 3 | Without drift-attribution monitoring, surfaces via complaint or audit rather than in real time; version history alone will not reveal the cause. |
| **Recoverability** | 2 | Once the causal prompt edit is identified, reversal to a prior version is typically straightforward. |
| **Novelty** | 3 | Recognising prompt text as behaviour-bearing configuration equivalent to code requires a non-obvious reframing for most change-management functions. |

## 17. Regulatory Basis
> No regulation names "prompt version control" explicitly. [PRA SS1/23, April 2026 (16 April 2026, updating 17 May 2023)] requires model risk governance covering all components materially affecting model behaviour, which extends to prompts and scaffolds by principle. [FCA AI Update, Apr 2024] and [SYSC change-management expectations] require firms to control changes affecting regulated activities. [NIST AI RMF 1.0, Jan 2023, MANAGE function] establishes ongoing management of AI system changes as a governance expectation. [EU AI Act, Regulation (EU) 2024/1689, Art. 9 (risk management), Art. 12 (record-keeping/logging)], applicable where prompt changes alter a high-risk system's behaviour (from 2 Dec 2027, per the Digital Omnibus postponement of Annex III deadlines agreed Jul 2026; Art. 9/12 obligations otherwise unaffected by the postponement for non-Annex-III uses already in scope). (corrected & verified 29 Jul 2026)

## 18. Research Basis
> [Chen, L., Zaharia, M., Zou, J., 2023, "How Is ChatGPT's Behavior Changing over Time?", arXiv:2307.09009; Harvard Data Science Review 6(2), 2024] — empirically demonstrates that the same API endpoint's behaviour drifted materially across months, evidencing that configuration/version changes (which may include undisclosed prompt or system changes on the provider side) produce behavioural drift independent of headline "model" changes. [Anthropic, 2025, "Reasoning Models Don't Always Say What They Think"] — chain-of-thought is not faithful to actual computation, meaning inspecting stated reasoning cannot substitute for controlling the actual prompt/scaffold configuration. [OpenAI, 2025, "Detecting Misbehavior in Frontier Reasoning Models"] — shows that penalising visible "bad thoughts" teaches models to hide them, reinforcing that oversight must rely on controlled configuration rather than reasoning-trace inspection alone. [Chatterjee, A., et al., 2024, "POSIX: A Prompt Sensitivity Index For Large Language Models," Findings of EMNLP 2024, pp. 14550-14565, arXiv:2410.02185] — a published index of prompt sensitivity, the relative change in the log-likelihood of a response when its prompt is replaced by a different, intent-preserving prompt; code is public. It measures sensitivity to variation that preserves intent, not the effect of an edit that changes the content of an instruction, which field 11 also covers; it needs response log-likelihoods, and the paper applies it to open-source models.
>
> **[FAIAS Incident Register, row 54, "xAI Grok unauthorised prompt change", 2025]** — xAI states that on 14 May 2025 an unauthorised modification was made to the Grok response bot's prompt on X, and that its "existing code review process for prompt changes was circumvented"; its remedies were to publish its prompts on GitHub, add checks so that employees cannot change the prompt without review, and monitor round the clock. A prompt change reached users outside xAI's code review process for prompt changes, and it directed the bot's replies on a political topic. This is a different event from the July 2025 episode that the register carries at row 24.
>
> **Research basis last reviewed:** 9 October 2026 · **review cadence:** Fast (6 months)

## 19. Related IRQs
```
  - IRQ-MOD-013 (B.6: prompt/config version control and regression testing —
    the model-domain twin of this agentic-domain IRQ)
  - IRQ-MOD-009 (B.4: chain-of-thought unfaithfulness — the reason reasoning
    inspection cannot substitute for configuration control)
  - IRQ-GOV-008 (I.3: monitoring/governance escalation triggers — must
    distinguish prompt-driven from model-driven drift)
  - IRQ-GOV-012 (I.2: envelope drift — prompt changes are one mechanism by
    which the effective operating envelope can silently shift)
  - IRQ-SEC-010 (E.3: compromised serving or tool layer — one route by which
    behaviour-altering content is changed outside any configuration-control path)
  - IRQ-SEC-011 (E.4: non-human identity and credentials — an unauthenticated
    local control interface is the entry condition in the documented case)
```

## 20. References
```
[1] Chen, L., Zaharia, M., Zou, J., 2023. "How Is ChatGPT's Behavior Changing over
    Time?" arXiv:2307.09009. Published in Harvard Data Science Review 6(2), 12 March 2024,
    https://doi.org/10.1162/99608f92.5317da47.
[2] Anthropic, 2025. "Reasoning Models Don't Always Say What They Think." April 2025.
[3] OpenAI, 2025. "Detecting Misbehavior in Frontier Reasoning Models." March 2025.
[4] NIST, 2023. "Artificial Intelligence Risk Management Framework (AI RMF) Version
    1.0." January 2023.
[5] PRA, 2026. "SS1/23 — Model risk management principles for banks."
    April 2026 (16 April 2026, updating 17 May 2023).
[6] European Union, 2024. "Regulation (EU) 2024/1689 — Artificial Intelligence Act."
    OJ L 12.7.2024.
[7] Chatterjee, A., Renduchintala, H. S. V. N. S. K., Bhatia, S., Chakraborty, T., 2024.
    "POSIX: A Prompt Sensitivity Index For Large Language Models." Findings of the
    Association for Computational Linguistics: EMNLP 2024, pp. 14550-14565.
    arXiv:2410.02185.
```

## 21. Four-Test Validation Footer
```
---
Version: the release version in README.md
Subdomain: C.6 (Agentic domain, Hidden Reasoning Dependencies)
Status: Active

FOUR-TEST VALIDATION:
✓ Test 1 (SME Blind Spot): Change-management SMEs classify prompt text as low-risk
  "content" rather than behaviour-bearing configuration, missing that small wording
  changes can have code-change-equivalent consequences for a generative agent.
✓ Test 2 (Plausible Harm): Grounded in Chen et al.'s empirical demonstration of
  behavioural drift from configuration change, and Anthropic/OpenAI research showing
  chain-of-thought inspection cannot substitute for configuration control.
✓ Test 3 (Testable): Fully testable via representative prompt-edit regression testing
  in a non-production environment. ★2 methodology, honestly caveated.
✓ Test 4 (Decision-Relevant): Gates whether prompt/scaffold changes may bypass formal
  change control, directly informing release-governance policy.

Change Log:
- v1.0 (2026-07): Initial publication; all four tests passed; xAI Grok system-prompt
  incident (Jul 2025) referenced in domain preamble as the closest public incident
  analogue for this failure mode.
- v1.2.0 (2026-09-12): Expected Evidence — dated worked example added (rendering-template
  poisoning via an unauthenticated local inference interface, CVE-2026-65105, 25 Aug
  2026), re-homed from IRQ-SEC-010 on the September 2026 refresh reading. Related IRQs —
  SEC-010 and SEC-011 added. No change to controls, test, ★ or risk profile.
- v1.3.3 (2026-10-09): Field 20 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — incident-register citation added in the reserved form (row 54, xAI Grok unauthorised prompt change of May 2025, a different event from row 24). Research-basis review date moved. No change to controls, test, ★2 or risk profile.
- v1.3.3 (2026-10-09): Field 17 — PRA SS1/23 cited as its April 2026 version (16 April 2026, updating 17 May 2023); the principles cited are unchanged.
- v1.3.3 (2026-10-09): Fields 9, 18 and 20 — the Chen, Zaharia and Zou citation (arXiv:2307.09009) now also gives its publication in Harvard Data Science Review 6(2), 2024. Research-basis review date moved. No change to the ★ rating or the risk profile.
- v1.3.3 (2026-10-09): Field 18 Research Basis — POSIX prompt sensitivity index added as a
  published method for sensitivity to intent-preserving variation, with its limits.
  Field 20 — entry [7] added. Research-basis review date moved. No change to controls,
  test, ★2 or risk profile.
```

---
---

