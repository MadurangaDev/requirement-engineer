# Requirement Engineer

> A Claude skill that turns Claude into an active Requirements Engineer / Business Analyst — not a note-taker. It discovers the real need behind a stakeholder request, hunts for hidden requirements, writes testable specs, and keeps every generated document (BRD, SRS, user stories, traceability matrix, etc.) consistent with each other.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-v1.0.0-blue.svg)](CHANGELOG.md)

---

## Why this exists

Most "write me an SRS" prompts just transcribe whatever you say. This skill is built to push back: it separates facts from assumptions, flags vague language before it becomes an ambiguous requirement, surfaces business rules hidden inside casual descriptions of how a process works, and refuses to silently paper over conflicting requirements.

---

## Download & Install

### Option 1 — Direct download (recommended)

Download the `.skill` file directly — no cloning required:

**[⬇️ Download requirement-engineer.skill](https://github.com/MadurangaDev/requirement-engineer/releases/download/beta/requirement-engineer.skill)**

Then install it in Claude Chat:

```text
Customizations → Skills → + → Create Skill → Upload a Skill
```

Select the downloaded `requirement-engineer.skill` file and complete the installation.

If you want to install in Claude Code:

```bash
claude skill install requirement-engineer.skill
```

### Option 2 — Clone the repository

```bash
git clone https://github.com/MadurangaDev/requirement-engineer.git
cd requirement-engineer
claude skill install skill/
```

---

## Core capabilities

- **16-stage workflow** — from project context discovery through deliverable generation, with a routing rule that skips the full march for a single quick deliverable.
- **EARS format** — `WHEN [event] THEN [system] SHALL [response]` and its variants, so requirements are testable by construction, not just in theory.
- **Narrative elicitation** — feed it a description of how a process works ("customer pays, then we ship") instead of answering a questionnaire, and it'll extract the business rules, failure paths, and implied actors hiding in the description.
- **Confidence-driven interview** — say *"interview me until you're confident about what I actually want"* and it will persist across many turns, tracking confidence per dimension (problem, scope, flows, hidden requirements, NFRs, architecture, priorities, risks) and specifically hunting for the gap between what you say you want and what you actually want.
- **IEEE-honest documentation** — the SRS structure is grounded in ISO/IEC/IEEE 29148:2018 (successor to IEEE 830), and the skill is explicit about which artifacts (PRD, DoD, EARS) are industry convention rather than formal standards, instead of implying false certification.
- **Traceability by default** — every requirement is expected to trace back to a business goal and forward to acceptance criteria and a test case.

---

## Example usage

```
"Interview me until you're confident about what I actually want for this project."
"I'm building a subscription seat-management feature — here's how it currently works: ..."
"Write me an SRS for this in IEEE format."
"Give me a fast requirements doc for just this one feature."
"Validate these requirements against the completeness/clarity/consistency/testability checklist."
```

---

## What's inside

```
requirements-engineer/
├── SKILL.md                          orchestrator: role, 16-stage workflow, routing, deliverable map
├── references/
│   ├── reasoning-framework.md        evidence hierarchy, knowledge states, requirement maturity ladder
│   ├── ears-format.md                EARS requirement grammar, edge case patterns, validation checklist
│   ├── ieee-standards.md             what's actually IEEE-standardized (29148/830) vs. convention (PRD, DoD)
│   ├── narrative-elicitation.md      extracting hidden requirements from a described workflow
│   ├── confidence-interview.md       persistent, confidence-driven interview mode for new projects
│   ├── stage-01-context-discovery.md
│   ├── stages-02-05.md               stakeholders → scope definition
│   ├── stages-06-10.md               elicitation → prioritization
│   └── stages-11-16.md               specification → deliverable generation
├── templates/
│   ├── vision.md · brd.md · srs.md · frd.md
│   ├── prd.md · definition-of-done.md
│   ├── user-story.md · use-case.md · acceptance-criteria.md
│   ├── stakeholder-register.md · traceability-matrix.md · risk-register.md
│   ├── glossary.md · change-request.md
│   └── feature-requirements.md       single-file fast path for one feature
└── examples/
    ├── ecommerce/                    assumption labeling on a single story
    ├── healthcare/                   regulatory/compliance discovery (HIPAA-style)
    ├── saas/                         multi-tenancy, SLA, billing-edge-case NFRs
    └── mobile-app/                   offline state, push permissions, app-store constraints
```

---



## Acknowledgments

The EARS format section, edge-case patterns, and validation checklist were adapted from an MIT-licensed [requirements-engineering skill](https://github.com/jasonkneen/kiro/blob/main/skills/requirements-engineering/) by the **[Kiro Team](https://github.com/jasonkneen/kiro)**, then integrated into this skill's broader 16-stage workflow and cross-referenced against IEEE 29148.

---

## License

MIT — see [LICENSE](LICENSE) for details.
