# Confidence-Driven Interview

Triggered by requests like *"interview me until you're confident about what I want,"* *"grill me on this before we start,"* or any explicit request to be interviewed rather than to just answer a question and move on. This is a distinct mode from a normal clarifying question — the difference is persistence toward a stated confidence level, and a specific hunt for the gap between what someone says they want and what they actually want.

## The core mechanic

Don't ask a question, get an answer, and move to specification. Instead:

1. After every answer, internally re-assess confidence (0–100%) across the dimensions below.
2. Ask the single question that targets the **lowest-confidence dimension** — not the next item on a checklist.
3. State your current confidence and *what's driving it down* periodically, out loud, so the process is transparent rather than a hidden gate: *"Around 70% right now — the two things holding it back are how you want conflicting edits resolved, and whether this needs to work offline."*
4. Keep going until you either hit the stated threshold (default: treat "98%" as "I could write the spec right now and defend every section if challenged") or you and the user agree remaining uncertainty is acceptable to proceed with as flagged assumptions.
5. Don't pad the interview once genuinely confident — stopping at real 95% beats manufacturing questions to hit an arbitrary number. The threshold is a discipline against stopping too early, not a quota.

## Confidence dimensions to track

Rate each separately rather than one blended number — a project can be 95% clear on the problem and 40% clear on failure behavior, and blending hides that.

- **Problem/goal** — do you understand *why* this exists, not just what was asked for?
- **Scope boundaries** — what's explicitly out, not just what's in?
- **User roles & flows** — every actor, including ones mentioned only in passing?
- **Hidden requirements** — business rules, edge cases, exceptions not yet stated (cross-reference `references/narrative-elicitation.md` if the user is describing a process)
- **Non-functional constraints** — performance, security, compliance, scale expectations
- **Architecture-relevant decisions** — data ownership, integration points, things expensive to change later if guessed wrong
- **Priorities & tradeoffs** — what gets sacrificed under pressure, and who decides
- **Risks** — what could invalidate the whole approach

## Hunting the "actually want" vs. "think I should want" gap

This is the part a generic clarifying-question loop misses. Watch for:

- **Buzzword or best-practice answers given reflexively.** If someone says "yeah, it should be scalable to millions of users" for a tool three people will use internally, don't just record it — ask what happens if it's built for 50 users and that assumption is wrong. Often the honest answer is "that's fine, we're nowhere near that," and the real requirement was much smaller.
- **Hedged language** ("I guess we'd probably want...", "it'd be nice if...") — these often signal a should-want, not a want. Follow up with something concrete: "if that feature didn't exist at all, would it actually block you, or just feel incomplete?"
- **Copied patterns from other products** ("like how Stripe does it") — ask what specifically about that pattern matters to them, rather than assuming the whole pattern transfers. Often it's one property (e.g. "the checkout doesn't reload the page") not the entire architecture.
- **Answers that contradict earlier, more specific answers.** A general aspirational statement ("security is critical") sitting next to a specific detail that undercuts it ("but let's just store passwords in plaintext for now, we'll fix it later") is a real signal worth naming directly rather than averaging out.

When you catch one of these, don't silently accept either version — surface it: *"Earlier you said X in general terms, but the specific example you gave suggests Y. Which one is actually true for this project?"*

## Interaction shape

- One question at a time, or a small tightly-grouped set — this is a conversation, not a form. See `ask_user_input_v0`-style single-question discipline, but note this mode is explicitly allowed to run for many turns, unlike the normal "ask at most one clarifying question then proceed" default.
- Don't front-load a giant list of every dimension above — that recreates the questionnaire this technique is meant to avoid. Let each answer determine the next question.
- If the user's answers reveal the project is much smaller/simpler than the opening description implied, say so — collapsing scope honestly is as valuable as expanding it.

## Output at the end

Once confidence is stated as sufficient, summarize what's now known, organized by the dimensions above, explicitly labeling anything that's still an assumption (per the Knowledge States in `references/reasoning-framework.md`) rather than confirmed. This summary becomes the input to Stage 1 (Context Discovery) or directly to whichever deliverable was the actual goal — the interview isn't the deliverable, it's what makes the deliverable trustworthy.
