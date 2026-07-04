# Stages 6–10

## Stage 6 — Elicitation

Don't rely on a single technique. Draw from: interviews, workshops, brainstorming, observation, questionnaires, document/interface/process analysis, competitor analysis, prototyping, scenario walkthroughs.

Actively hunt for what stakeholders *won't* volunteer: hidden requirements, implicit assumptions, business rules stated as asides, exceptions, edge cases, negative scenarios ("what happens when it fails?"). When the user describes a process narratively rather than answering direct questions, use `references/narrative-elicitation.md` — it's a more systematic way to mine a workflow description for hidden requirements than waiting for a Q&A to surface them.

Output: Raw Requirements, Questions, Assumptions, Business Rules (kept as a separate catalogue from functional requirements — see SKILL.md operating discipline).

## Stage 7 — Classification

Sort discovered items into: Business / Stakeholder / User / Functional / Non-Functional / Security / Compliance / Data / Reporting / Operational Requirements, plus Technical Constraints, Business Rules, Assumptions, Dependencies. Anything that doesn't fit cleanly gets flagged rather than force-fit.

## Stage 8 — Analysis

Normalize, decompose oversized requirements, merge duplicates, resolve conflicts (see reasoning-framework.md), check feasibility, map dependencies and impacts.

Output: Refined Requirements + Analysis Findings + Outstanding Issues.

## Stage 9 — Modeling

Only build a model where it adds clarity over prose — not by default. Options: use cases, user stories, BPMN/activity/sequence/state diagrams, ER/domain models, context diagrams, DFDs, decision tables/trees, wireframes.

## Stage 10 — Prioritization

Pick a method that fits: MoSCoW, Kano, WSJF, Value-vs-Effort, or risk-based. Weigh business value, risk reduction, complexity, dependencies, urgency — and record *why* something was prioritized where it landed, not just the ranking.
