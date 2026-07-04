# Feature Requirements: Offline Order Tracking (Mobile App)

*Domain note: mobile examples exist to show platform-specific constraints — offline state, push notification permissions, and app-store review requirements — that don't come up in web-first thinking.*

## Overview
Customers should be able to check the status of a recent order in the app even without a network connection, and get notified when status changes.

## Stakeholder Narrative
"Users check their order status a lot, especially on the subway with no signal. We want the app to show the last known status even offline, and push a notification when it updates."

## Narrative Elicitation Findings
- **Data jump:** "show the last known status even offline" — how stale can that be before it's misleading? (surfaces a data-freshness requirement — needs a "last updated" timestamp shown, not just a raw cached value presented as current)
- **Decision point (implicit):** "push a notification when it updates" — requires the user to have granted push permission; what's shown to users who denied it? (surfaces a permission-fallback requirement)
- **Handoff:** device regains signal after being offline — does the app silently reconcile, or does the user need to manually refresh? (surfaces a sync-behavior requirement)

## User Roles
- **Customer:** views order status, may be offline
- **Push notification service (internal):** delivers status-change alerts

## Requirements

### Requirement 1: Offline Status Display
**User Story:** As a customer with no signal, I want to see my order's last known status, so that I'm not left with a blank screen.

**Acceptance Criteria (EARS):**
1. WHEN the app has no network connectivity THEN system SHALL display the most recently cached order status along with a "last updated [timestamp]" label
2. IF no cached status exists for an order (e.g. first-ever load with no connectivity) THEN system SHALL display an explicit "unable to load — no connection" state rather than a blank or misleading default
3. WHEN connectivity is restored THEN system SHALL automatically refresh the displayed status within 5 seconds without requiring manual user action

### Requirement 2: Push Notification on Status Change
**User Story:** As a customer, I want to be notified when my order status changes, so that I don't have to keep checking manually.

**Acceptance Criteria (EARS):**
1. WHEN an order status changes AND the user has granted push permission THEN system SHALL send a push notification within 60 seconds of the change
2. IF the user has denied push permission THEN system SHALL NOT prompt repeatedly on every order update — surface an in-app, non-blocking banner suggesting they enable it instead, at most once per app session
3. WHEN the user taps the notification THEN system SHALL open directly to that order's status screen, using cached data if currently offline

## Non-Functional Requirements
- **Offline resilience:** Last-known state for at least the 5 most recent orders SHALL be cached locally
- **Platform compliance:** Push permission requests SHALL follow platform guidelines (iOS: contextual pre-prompt before the system dialog; Android 13+: runtime notification permission) — required for app-store review, not optional polish
- **Battery/data:** Background sync on connectivity restore SHALL NOT trigger a full app refresh — only the affected order's data

## Out of Scope
- Real-time live tracking map (this feature is status-state only, not location tracking)

## Open Questions
- How many recent orders should be cached offline — is 5 sufficient, or should it be configurable?
- Should denied-push users get a periodic in-app reminder, or is once-per-session enough to avoid feeling naggy? (UX decision, not purely technical)
