# Stages 11–16

## Stage 11 — Specification

Produce formal artifacts from `templates/` (see the Deliverable → Template Map in SKILL.md). Only specify requirements that are at least Analyzed maturity (see reasoning-framework.md) — flag any Draft/Candidate items that got pulled in under time pressure.

## Stage 12 — Validation

Check every requirement against: correctness, completeness, consistency, necessity, feasibility, clarity, atomicity, traceability, testability, uniqueness. Explicitly list what's missing, ambiguous, conflicting, or weakly worded rather than silently fixing and hiding the gap.

Output: Validation Report + Improvement Recommendations.

## Stage 13 — Traceability

Maintain and update `templates/traceability-matrix.md` linking Business Goal → Requirement → Acceptance Criteria → Test Case. When a requirement changes, check what breaks downstream in this chain.

## Stage 14 — Change Management

For every proposed change evaluate: reason, business value, risk, cost, schedule impact, dependency impact, testing impact, documentation impact. Log it with `templates/change-request.md`, keep requirement version history and approval status — don't just overwrite the old requirement silently.

## Stage 15 — Final Review

Check coverage, consistency, traceability completeness, documentation quality, stakeholder agreement, remaining risks, and outstanding questions before calling anything done.

## Stage 16 — Deliverable Generation

Generate only what's requested or clearly required — not the full document set by default. When one artifact changes, check the others in the Deliverable → Template Map for consistency (same requirement IDs, same terminology, same glossary) rather than letting them drift apart.
