# FAIAS — Review Canvases: Human Oversight Domain (D.1–D.4)

**Domain:** HUM — Human Oversight
**IRQs covered:** IRQ-HUM-001 … IRQ-HUM-009 (9 of 9)
**Compiled:** 2026-07
**Structure:** IRQ_TEMPLATE.md (21 fields per canvas), per ASSURANCE_MODEL.md
**Spelling:** UK throughout

## Domain Preamble

Human Oversight is where every other domain's residual risk is meant to be caught. A hallucinating model (Model domain), a drifting agent plan (Agentic domain), an injected instruction (Security domain) — all of these failure chains route, in FAIAS's design, through a human checkpoint before they reach a customer or a regulator. This domain asks the uncomfortable question: does that checkpoint actually work? The honest answer, grounded in four decades of human-factors and automation research, is frequently no. Automation bias — the well-documented tendency of human operators to accept automated recommendations without adequate independent verification, even when contradictory evidence is available — was characterised by Parasuraman & Riley (1997) and empirically demonstrated in Skitka, Mosier & Burdick's decision-aid studies (1999, 2000); it is not an AI-era novelty but it is sharply amplified by generative and agentic systems whose outputs are fluent, confident and individually plausible. Unlike the Agentic domain, HUM's evidence base has real teeth: disagreement-rate analysis, override-rate monitoring, dwell-time and approval-throughput analysis, and AI-free competency assessment are established human-factors and ergonomics (HF/E) methods with decades of aviation, healthcare and process-control precedent (e.g. Goddard, Roudsari & Wyatt's 2012 systematic review of automation bias in clinical decision support) — several of the tests in this domain therefore sit at **★3 confidence**, higher than the Agentic or Security domains typically achieve. Where a control is AI-specific in a way the underlying HF/E literature does not directly anticipate — e.g. contestability of a genuinely generative recommendation, or accountability tracing through a multi-agent delegation chain — confidence is honestly marked down to ★2.

This domain also carries the sharpest regulatory anchoring in the register: EU AI Act Article 14 (human oversight) is the closest thing FAIAS has to a directly on-point legal requirement for an entire subdomain, and UK-regulated firms carry parallel obligations under the FCA Consumer Duty (PRIN 2A, fair value and good outcomes), the Senior Managers & Certification Regime (SM&CR, individual accountability for AI-influenced decisions) and FCA SYSC/PS21/3 operational resilience expectations for critical human-performed tasks. The recurring failure pattern across all nine IRQs is "approval theatre": a human sits in the loop, a record shows sign-off occurred, and yet no genuine independent judgement was exercised — because reviewers were not trained to challenge, dwell time made genuine review physically impossible, overriding carried a career penalty, or the escalation point was positioned after the point where intervention could still change the outcome. Every canvas below anchors on that failure mode, not on the presence or absence of a human-in-the-loop label.

All Independent Tests in this domain are explicitly non-production: they use staging decision samples, historical case replays, reviewer studies and simulated escalation scenarios, never live customer underwriting, claims or AML decisions.

---
---

## Files of this domain (note added 3 October 2026)

From FAIAS v1.3.1 each Review Canvas of this domain is held in its own file in this folder, and this file holds the domain's introductory text. The text of each canvas is unchanged by the move. Before v1.3.1 the canvases were held in this file; 00_Admin/MIGRATION_2026-10-03.md maps each line of the earlier file to its new file and line.

The canvases, in order:

- IRQ-HUM-001: CANVASES_HUM_001.md
- IRQ-HUM-002: CANVASES_HUM_002.md
- IRQ-HUM-003: CANVASES_HUM_003.md
- IRQ-HUM-004: CANVASES_HUM_004.md
- IRQ-HUM-005: CANVASES_HUM_005.md
- IRQ-HUM-006: CANVASES_HUM_006.md
- IRQ-HUM-007: CANVASES_HUM_007.md
- IRQ-HUM-008: CANVASES_HUM_008.md
- IRQ-HUM-009: CANVASES_HUM_009.md

