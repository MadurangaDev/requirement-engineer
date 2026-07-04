# EARS Format (Easy Approach to Requirements Syntax)

Use EARS for the requirement *statement* itself — it's what turns "the search should be fast" into something a tester can actually pass or fail. Pair it with `templates/acceptance-criteria.md` (EARS for the requirement, Given/When/Then for the test scenarios built on top of it) — they're not competing formats, they answer different questions.

## Patterns

**Event-response (most common):**
`WHEN [triggering event] THEN [system] SHALL [required response]`

**Conditional:**
`IF [precondition] THEN [system] SHALL [required response]`

**Complex condition:**
`WHEN [event] AND [additional condition] THEN [system] SHALL [response]`

**Optional condition:**
`WHEN [event] OR [alternative event] THEN [system] SHALL [response]`

**State-based:**
`WHILE [system is in specific state] THEN [system] SHALL [behavior]`

**Performance:**
`WHEN [user action] THEN [system] SHALL [respond within X seconds/ms]`

**Security:**
`IF [authentication/authorization condition] THEN [system] SHALL [security response]`

## Rules

- One requirement = one testable statement. If a sentence needs "and" to join two unrelated behaviors, split it (see Requirement Granularity Control in the operating discipline).
- Always name the actor: "the system," not "it."
- Always use SHALL, never should/may/could — see reasoning-framework.md and the weak-language rule in SKILL.md.
- Every event-response requirement should have a matching failure/edge counterpart — see edge case patterns below.

## Edge Case Patterns

Apply these to every requirement, not just the obvious ones:

- **Empty/null:** `WHEN [collection/input] is empty THEN system SHALL [display empty state / reject / default]`
- **Boundary values:** `WHEN [value] equals [minimum/maximum] THEN system SHALL [specific behavior]`
- **Operation failure:** `WHEN [operation] fails THEN system SHALL [display error / retry / log]`
- **Unauthorized access:** `IF user is not authenticated/authorized THEN system SHALL [redirect / deny / log attempt]`
- **Concurrent access:** `WHEN multiple users access [same resource] concurrently THEN system SHALL [conflict resolution behavior]`

## Validation Checklist (quick pass, before calling requirements done)

Run this at the point of writing — don't defer all validation to Stage 12. It's a fast gut-check, not a replacement for the fuller IEEE 29148 characteristics list in `templates/srs.md`.

**Completeness**
- [ ] All user roles identified and addressed
- [ ] Normal flow covered
- [ ] Edge cases documented (see patterns above)
- [ ] Error/failure cases handled
- [ ] Business rules captured separately from functional requirements

**Clarity**
- [ ] Precise language, no ambiguous terms (fast, easy, user-friendly, scalable) left unresolved
- [ ] Jargon avoided or defined in the glossary
- [ ] Expected behavior is specific enough to disagree with if wrong

**Consistency**
- [ ] EARS format used throughout
- [ ] Terminology matches the glossary across every document touched
- [ ] No contradictory requirements left unresolved
- [ ] Similar scenarios handled the same way (don't special-case arbitrarily)

**Testability**
- [ ] Every requirement can be verified
- [ ] Success criteria are observable, not subjective
- [ ] Inputs and expected outputs are specified
- [ ] Performance requirements have numbers, not adjectives

## Bad → Good

| Bad | Good | Why |
|-----|-------|-----|
| "System should be fast" | "WHEN user submits search THEN system SHALL return results within 2 seconds" | Vague → measurable |
| "System shall use Redis for caching" | "WHEN user requests frequently accessed data THEN system SHALL return cached results" | Implementation detail leaked into a requirement — see Architecture Neutrality |
| Only happy-path documented | Every WHEN/THEN paired with an IF for the failure case | Missing error cases |
| "System should be user-friendly" | "WHEN new user completes onboarding THEN system SHALL require no more than 3 clicks to reach the dashboard" | Untestable → testable |
| Two requirements that silently contradict | Conflicts named explicitly and routed to Stage 8 (Analysis) for resolution | Never resolve a conflict by picking a side unilaterally |
