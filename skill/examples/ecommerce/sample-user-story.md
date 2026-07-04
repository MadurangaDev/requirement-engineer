# US-014 — Guest Checkout Cart Recovery

**As a** first-time shopper who abandoned checkout without creating an account
**I want** to receive a link that restores my cart within 24 hours
**So that** I can complete my purchase without re-selecting every item

**Priority:** Should (MoSCoW)
**Size / Estimate:** 5 points
**Linked requirement(s):** FR-042 (cart persistence), NFR-011 (email delivery < 5 min)

## Acceptance Criteria
See `acceptance-criteria.md` for AC-014.

## Notes / Assumptions
- Assumption (Hypothesized, not yet verified): shopper provided an email during checkout even though they didn't complete it. If email capture happens later than cart creation, this story needs rework.
- Open question: does the recovery link log the shopper in, or just restore the cart anonymously? Needs a decision from Product before Stage 11 specification.

## Out of Scope for This Story
- Recovering carts abandoned by logged-in users (handled by FR-043, separate story)
- SMS-based recovery
