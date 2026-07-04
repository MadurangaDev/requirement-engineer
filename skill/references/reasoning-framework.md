# Reasoning Framework

Read this once per engagement — it underlies every stage rather than belonging to any single one.

## Evidence Hierarchy

When sources conflict, higher wins:

1. Laws / regulations
2. Signed contracts
3. Approved business decisions
4. Official organizational policy
5. Verified stakeholder confirmation
6. Existing production system behavior
7. Existing documentation
8. Industry standards
9. Expert opinion
10. AI inference (lowest — never overrides verified facts)

## Knowledge States

Tag important conclusions with one of these, and don't let them drift silently between states:

- **Unknown** — not yet discovered
- **Hypothesized** — inferred, not confirmed (state it as a hypothesis, never as a requirement)
- **Observed** — reported by a stakeholder, unverified
- **Verified** — confirmed by evidence or stakeholder validation
- **Rejected** — previously believed, now disproven
- **Superseded** — replaced by newer verified information

A hypothesis like "only managers may approve refunds" must stay labeled as a hypothesis until confirmed — do not write it into a spec as "The system shall allow only managers to approve refunds" without that confirmation step happening first.

## Confidence

Very Low / Low / Medium / High / Very High. Confidence rises only with supporting evidence and falls when contradictions appear. Never present a Low/Very Low conclusion with confident phrasing.

## Requirement Maturity Ladder

Draft → Candidate → Analyzed → Validated → Approved → Baselined

Don't produce implementation-ready specification documents (SRS, FRD) from Draft or Candidate-level requirements — flag that they need analysis/validation first, or do that analysis before specifying.

## Contradiction Handling

When two pieces of information conflict:

1. State both, plainly.
2. Explain the practical impact of the conflict.
3. Ask for a resolution — don't pick a side unilaterally.
4. If unresolved, log it as an open conflict rather than proceeding as if one side won.

## Traceability Chain

Every requirement should trace upward to a reason for existing and downward to a way of verifying it:

Business Goal → Business Requirement → Stakeholder Requirement → Functional/Non-Functional Requirement → Acceptance Criteria → Test Case

A requirement that can't be traced to a goal is worth questioning ("why does this exist?"). A requirement with no acceptance criteria isn't finished.

## Scope Ladder (don't jump levels)

Business Problem → Business Goal → Business Requirement → Stakeholder Requirement → User Requirement → Functional Requirement → Non-Functional Requirement → Technical Design

Keep discussion at the appropriate level — don't let a business-problem conversation jump straight to a database schema.
