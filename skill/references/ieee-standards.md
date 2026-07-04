# IEEE / ISO Standards Reference

## What's actually IEEE-standardized

**ISO/IEC/IEEE 29148:2018** — "Systems and software engineering — Life cycle processes — Requirements engineering." This is the current governing standard for requirements engineering practice, and it's what `templates/srs.md` is structured against. It superseded the older, narrower **IEEE 830-1998** (Recommended Practice for Software Requirements Specifications) — 830 is retired but its SRS section outline is still widely taught, so it's worth knowing both.

IEEE 29148 defines, among other things:
- The recommended **SRS outline** (used in `templates/srs.md`): Introduction → Overall Description → Specific Requirements (functional, external interface, performance, design constraints, quality attributes) → Verification → Appendices.
- Requirement quality characteristics a well-formed requirement should meet: **unambiguous, complete, singular (atomic), feasible, verifiable, correct, necessary, implementation-free, and traceable.** These map directly onto the SKILL.md quality checks and are what Stage 12 (Validation) should be checking against.
- A **StRS** (Stakeholder Requirements Specification) sitting between business needs and the SRS — this is effectively what our BRD + stakeholder register jointly cover; there isn't a separate template for it here because BRD does that job, but call it out by name if the user specifically asks for a StRS.

**IEEE 830-1998 (legacy)** SRS section numbering, for reference if someone asks for "the IEEE 830 format" by name:
1. Introduction (Purpose, Scope, Definitions, References, Overview)
2. Overall Description (Product Perspective, Functions, User Characteristics, Constraints, Assumptions/Dependencies)
3. Specific Requirements (Functional, Interface, Performance, Design Constraints, Quality Attributes, Other)

`templates/srs.md` already follows this shape (it predates 830 being retired but 29148 kept the same skeleton), so no separate 830 template is needed — just recognize the name if the user uses it.

## What is NOT an IEEE standard (say so if asked)

- **PRD (Product Requirements Document)** — an industry-standard product-management artifact, not an IEEE standard. No formal spec exists; conventions vary by company. `templates/prd.md` below reflects common practice, not a standard.
- **DoD (Definition of Done)** — an Agile/Scrum team-working-agreement artifact (popularized by Scrum guides, not IEEE or ISO). It's a checklist a team agrees on, not a specification format.
- **EARS** — practitioner-originated (Rolls-Royce, Alistair Mavin et al.), not an IEEE standard, though it's compatible with and often used to write the "Specific Requirements" section of a 29148-structured SRS.

If a user says "make this IEEE-compliant," that claim is only accurate for the SRS/StRS structure and the requirement-quality characteristics above — be precise about that rather than implying PRD/DoD/EARS carry the same standardization.

## Traceability note

29148 requires bidirectional traceability from stakeholder need through to verification — this is exactly what `templates/traceability-matrix.md` and Stage 13 already implement, so no change needed there.
