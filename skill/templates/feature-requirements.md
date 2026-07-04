# Feature Requirements: {Feature Name}

*Fast-path template — use this instead of the full BRD→SRS→FRD chain when the ask is "capture requirements for this one feature," not a full engagement. See SKILL.md routing.*

## Overview
{What this feature is and why it matters, in 2-3 sentences}

## User Roles
- {Role}: {description}

## Requirements

### Requirement 1: {Name}
**User Story:** As a {role}, I want {capability}, so that {benefit}

**Acceptance Criteria (EARS — see `references/ears-format.md`):**
1. WHEN {event} THEN system SHALL {response}
2. IF {condition} THEN system SHALL {response}
3. WHEN {event} AND {condition} THEN system SHALL {response}

**Edge Cases:**
- {Edge case and how it's handled — see edge case patterns in ears-format.md}

### Requirement 2: {Name}
{Continue pattern...}

## Key Constraints
{Inline domain-specific numbers/limits that make requirements concrete and easy to reference — e.g. "Max File Size: 10MB," "Minimum Search Length: 2 characters," "Supported Types: PDF, PNG, JPG." Not every feature needs this section, but if requirements above reference a specific limit, state it here once rather than repeating the number in prose each time.}

## Validation Checklist
Run `references/ears-format.md`'s Completeness / Clarity / Consistency / Testability checklist before calling this done.

## Non-Functional Requirements
- **Performance:** {measurable target, not "fast"}
- **Security:** {}
- **Accessibility:** {}

## Out of Scope
- {Explicitly excluded from this feature}

## Open Questions
- {Anything unresolved — don't paper over it}

## Next Steps
1. Review with stakeholders for accuracy
2. Get explicit approval before design work starts
3. Use as the foundation for acceptance testing (`definition-of-done.md`)
