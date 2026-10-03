# FAIAS — Review Canvases: Agentic Domain (C.1–C.7)

**Domain:** AGT — Agentic
**IRQs covered:** IRQ-AGT-001 … IRQ-AGT-014 (14 of 14)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md (21 fields per canvas), per ASSURANCE_MODEL.md
**Spelling:** UK throughout

## Domain Preamble

Agentic systems — models that plan, invoke tools, delegate to sub-agents, retain operational memory across turns, and act with reduced or no per-step human confirmation — are where FAIAS is deliberately built as the standard's strongest domain. The reason is structural, not rhetorical: every other domain (Data, Model, Human Oversight, Security, Third Party, Resilience, Conduct, Governance) governs a *component*; the Agentic domain governs what happens when those components are wired into a system that **acts** on a financial institution's behalf — moving funds, committing to customers, writing to memory that will steer the next decision, and delegating to other agents whose reasoning it cannot fully inspect. The consequence is that agentic failure modes compound: a single unmitigated gap in tool-permission scoping (C.2), recursive delegation (C.3) or irreversible-action gating (C.7) can turn a moderate-severity model error into an unrecoverable one. Traditional financial-services risk functions — credit risk, AML operations, compliance monitoring — are built around discrete human or rule-based decisions with a clear point of accountability; none of that machinery was designed to ask whether a multi-step plan silently drifted from its original goal, whether a chain of individually-authorised tool calls produced an unauthorised composite action, or whether an agent's own prior mistake, written to memory, is quietly steering today's output. This is precisely the blind-spot profile the Novelty axis of ASSURANCE_MODEL.md exists to capture, and it recurs across all fourteen IRQs below.

The evidence base for this domain is genuinely emergent. Where the Data and Model domains can draw on a decade of statistical-learning and MRM literature, agentic AI safety research is roughly 2023–2026 vintage: Anthropic's Agentic Misalignment and Project Vend, OpenAI's Practices for Governing Agentic AI Systems and Operator/Deep Research system cards, Microsoft's Taxonomy of Failure Modes in Agentic AI Systems, the OWASP Agentic Security Initiative's Agentic AI: Threats and Mitigations (the first structured agent threat model, February 2025), and NIST AI 600-1's GenAI risk categories collectively form the control catalogue this domain draws on — but almost none of it has matured into a benchmarked, widely-adopted testing standard. Readers should therefore expect Independent Tests in this domain to sit at **★2 confidence**: credible published research and emerging practitioner methodology, but bespoke test design and heavy reliance on assessor judgement rather than a canonical benchmark. That honesty is itself the point of FAIAS's evidence model — inflating agentic test confidence to ★3+ would misrepresent the state of the art and undermine the standard's credibility with both boards and regulators. Two IRQs (AGT-008, memory poisoning; AGT-013, computer-use GUI safety) are rated ★1 because the harm mechanism, while plausible and partly demonstrated, has no standard evaluation at all.

Every canvas below anchors on a failure mode (not merely a behaviour), traces every expected control to a named regulation, standard or peer-reviewed/frontier-lab source, tags every evidence item L1–L5, and reports risk as a five-axis profile rather than a composite score, per ASSURANCE_MODEL.md sections 5–7. Public financial-services-relevant incidents (Knight Capital's automation-speed loss, the Replit agent's production-database deletion during a code freeze, the xAI Grok code-path update that unexpectedly incorporated deprecated instructions into a production bot, and Anthropic's disclosure of an agentic cyber-espionage campaign it attributes, with high confidence, to a state-sponsored actor) recur through the failure chains as the closest available real-world analogues, since documented FS-sector agentic incidents remain sparse — itself evidence for why this domain requires assurance now, ahead of a large incident base.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-AGT-001: CANVASES_AGT_001.md
- IRQ-AGT-002: CANVASES_AGT_002.md
- IRQ-AGT-003: CANVASES_AGT_003.md
- IRQ-AGT-004: CANVASES_AGT_004.md
- IRQ-AGT-005: CANVASES_AGT_005.md
- IRQ-AGT-006: CANVASES_AGT_006.md
- IRQ-AGT-007: CANVASES_AGT_007.md
- IRQ-AGT-008: CANVASES_AGT_008.md
- IRQ-AGT-009: CANVASES_AGT_009.md
- IRQ-AGT-010: CANVASES_AGT_010.md
- IRQ-AGT-011: CANVASES_AGT_011.md
- IRQ-AGT-012: CANVASES_AGT_012.md
- IRQ-AGT-013: CANVASES_AGT_013.md
- IRQ-AGT-014: CANVASES_AGT_014.md

