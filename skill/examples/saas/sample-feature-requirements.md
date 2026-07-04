# Feature Requirements: Team Workspace Seat Management (B2B SaaS)

*Domain note: SaaS examples exist to show NFR depth (multi-tenancy, SLA, billing) and prioritization tradeoffs, which tend to be under-specified compared to functional flows.*

## Overview
Account admins need to add/remove team members and have billing reflect seat count automatically, for a subscription-based B2B product.

## Stakeholder Narrative
"Admins invite people by email, they accept and get a seat. If someone's removed, their seat frees up. Billing should just follow how many seats are active."

## Narrative Elicitation Findings
- **Actor in passing:** "someone's removed" — by whom? Only admins, or can members leave themselves? (surfaces a permissions requirement not stated as one)
- **Decision point:** "billing should just follow" — follow how precisely? Immediate proration, or only at next billing cycle? (surfaces a business rule requiring explicit confirmation — this is a revenue-affecting decision, don't assume)
- **Data jump:** "invite people by email" — what if the email is already tied to another workspace, or the invite expires unaccepted? (surfaces failure-path requirements)
- **Handoff:** removing a seat — does that revoke access immediately, or at end of billing period? Affects both UX and billing logic; needs a decision, not an assumption.

## User Roles
- **Workspace Admin:** invites/removes members, sees billing
- **Member:** accepts invites, can view own seat status
- **Billing system (internal):** consumes seat-count events

## Requirements

### Requirement 1: Invite Team Member
**User Story:** As a workspace admin, I want to invite someone by email, so that they can join and use a seat.

**Acceptance Criteria (EARS):**
1. WHEN admin sends an invite to a valid, unused email THEN system SHALL create a pending invite and send an email with an acceptance link
2. IF the invited email already belongs to an active member of this workspace THEN system SHALL reject the invite with a specific "already a member" message
3. WHEN a pending invite is not accepted within 7 days THEN system SHALL expire it and notify the admin
4. WHEN an invite is accepted THEN system SHALL allocate a seat and, IF the current plan has no available seats, prompt the admin to upgrade before completing the join — never silently add a seat that causes overage without a confirmed billing decision

### Requirement 2: Remove Team Member / Seat Reclamation
**User Story:** As a workspace admin, I want to remove a member, so that their seat and access are freed for someone else.

**Acceptance Criteria (EARS):**
1. WHEN admin removes a member THEN system SHALL revoke their access within 60 seconds (NFR — see below) and free the seat
2. IF the removed member is the sole owner of shared resources (e.g. a workspace they created) THEN system SHALL require reassignment of ownership before removal completes, not leave orphaned resources
3. WHEN a seat is freed mid-billing-cycle THEN system SHALL apply the confirmed proration rule — **open question, see below**

## Non-Functional Requirements
- **Multi-tenancy:** Seat and billing data SHALL be strictly isolated per workspace; no cross-tenant query path should exist even for admin tooling
- **Performance/SLA:** Access revocation on removal SHALL propagate to all active sessions within 60 seconds
- **Availability:** Seat management actions SHALL remain available during billing-provider outages (queue and reconcile billing events asynchronously rather than blocking the invite/remove flow on the billing API)
- **Auditability:** Every seat add/remove event SHALL be logged with actor, timestamp, and resulting seat count for billing dispute resolution

## Prioritization Note (Stage 10)
Immediate access revocation (NFR) is Must — security-sensitive. Proration logic is Should — affects revenue but isn't a launch blocker if the interim behavior (bill at next cycle regardless) is acceptable to the business; confirm before deciding.

## Out of Scope
- Self-serve seat-count changes via API (admin UI only for v1)

## Open Questions
- Immediate proration on removal, or reconcile at next billing cycle only? Revenue-affecting — needs a business decision, not an engineering default.
- Can members remove themselves, or is that admin-only?
