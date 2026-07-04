# Narrative Elicitation — Finding Hidden Requirements in a Described Process

A questionnaire is one elicitation technique (Stage 6). A stakeholder describing how a process actually works is another, often richer, source — hidden requirements usually surface as things *implied* by the workflow, not as answers to direct questions. Use this when the user says "here's how it works" instead of answering a Q&A.

## How to scan a narrative

As the process is described, tag every instance of these five signal types. Each tag type maps to a category of hidden requirement to surface and confirm — not to silently assume.

### 1. Actors mentioned in passing
"Then it goes to the warehouse team" introduces a role that was never formally scoped. → Surface: Who exactly? What's their access/permissions? Is this a manual handoff or does the system need to notify/route to them? Add to stakeholder discovery if not already captured.

### 2. Decision points
"If the order is over $500, someone approves it" is a business rule and an approval workflow stated as an aside. → Surface: Who approves? What if they're unavailable? Is there a threshold edge case (exactly $500)? This becomes both a Business Rule entry and a functional requirement with an EARS conditional (`IF order total exceeds $500 THEN system SHALL route for approval`).

### 3. Handoffs between people or systems
"Customer pays, then we ship" skips the transition. → Surface: What happens if payment succeeds but the shipping system is unreachable? Partial payment? Is there a status the order sits in during the gap? A described handoff with no failure behavior is an incomplete requirement, not a resolved one.

### 4. Data mentioned once, never revisited
"We log the reason for the return" implies retention, reporting, and possibly privacy requirements that were never stated as such. → Surface: How long is it kept? Who can see it? Does it feed a report anyone relies on? Add to Data Requirements (Stage 6 output) even though the stakeholder never called it a "requirement."

### 5. Narrative jumps ("then somehow...")
Any point where the description speeds past a step ("...and then it just gets approved and processed") is usually where the real complexity lives, not where it's absent. → Surface: ask specifically about that gap rather than accepting the smooth version. Stakeholders often gloss over the messiest part because it's the part they've stopped noticing.

## What to do with what you find

- Don't convert a tagged item straight into a baselined requirement. It's Hypothesized or Observed (see reasoning-framework.md knowledge states) until confirmed.
- Batch findings back to the stakeholder rather than interrogating line-by-line: "You mentioned the warehouse team gets involved for large orders — a few things I want to pin down: who exactly, what happens if they're slow, and what the customer sees while that's happening." One grouped follow-up beats five separate ones.
- Feed confirmed findings into the normal Stage 7 classification (Business Rule vs Functional Requirement vs NFR vs Assumption) — narrative elicitation is a discovery method, not a separate output format.

## Worked example

**Narrative given:** "New customers sign up, verify their email, and then can start ordering. Repeat customers just log in. Occasionally support has to manually reset someone's account if they're locked out."

**Tags found:**
- Actor in passing → "support" — do they have a defined role/tool for this, or do they do it ad hoc in the database? (surfaces an operational requirement + possibly an audit-logging requirement)
- Decision point → implicit: verified vs. unverified email — what can an unverified user do, if anything, before verifying? (surfaces an access-control requirement never stated as one)
- Handoff → "verify their email... then can start ordering" — what if verification email never arrives, or the link expires? (surfaces failure-path requirements)
- Data jump → "locked out" — after how many failed attempts? Is that configurable? Is it logged? (surfaces a security NFR and a business rule)

None of this was asked for directly. All of it came from paying attention to what the four sentences implied rather than just what they stated.
