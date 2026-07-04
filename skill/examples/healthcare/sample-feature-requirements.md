# Feature Requirements: Patient Appointment Reminders

*Domain note: healthcare examples exist to show regulatory/compliance discovery (Stage 1) and PHI-aware data requirements, which are easy to under-specify if not actively asked about.*

## Overview
Automated reminders sent to patients ahead of scheduled appointments, to reduce no-show rates at the clinic.

## Stakeholder Narrative (as given, unprompted Q&A)
"Right now the front desk calls people the day before. We want to automate that — text or email them a reminder. If they don't show up twice, we flag their file."

## Narrative Elicitation Findings (see `references/narrative-elicitation.md`)
- **Actor in passing:** "front desk" currently does this manually — do they still need visibility/override once automated? (surfaces an operational requirement: staff-facing dashboard or opt-out per patient)
- **Decision point:** "flag their file" — flagged how, visible to whom, does it trigger any workflow (e.g. requires deposit for future bookings)? (surfaces a business rule needing confirmation, not yet a requirement)
- **Handoff / data jump:** "text or email them" — what if the clinic doesn't have a valid phone/email on file, or the patient has opted out of one channel? (surfaces a failure-path requirement)
- **Regulatory flag (Stage 1 — not volunteered, must be actively asked):** patient contact data and appointment details are PHI under HIPAA. Reminder content, delivery logs, and any third-party SMS/email provider need a Business Associate Agreement and encryption-in-transit — this must be confirmed with the stakeholder, not assumed absent.

## User Roles
- **Patient:** receives reminders, may reply to confirm/cancel
- **Front desk staff:** monitors no-show flags, manages overrides
- **Clinic admin:** configures reminder timing and channel rules

## Requirements

### Requirement 1: Send Appointment Reminder
**User Story:** As a patient, I want a reminder before my appointment, so that I don't forget and miss it.

**Acceptance Criteria (EARS):**
1. WHEN an appointment is scheduled more than 24 hours in advance THEN system SHALL send a reminder 24 hours before the appointment time
2. IF the patient has no valid phone number or email on file THEN system SHALL flag the appointment for manual front-desk follow-up instead of failing silently
3. WHEN a reminder is sent THEN system SHALL log delivery status (sent/failed/opted-out) for audit purposes

**Edge Cases:**
- Appointment scheduled less than 24 hours out → send an immediate reminder rather than skipping it
- Patient has opted out of SMS but not email → system SHALL fall back to the remaining enabled channel, not silently drop the reminder

### Requirement 2: No-Show Flagging
**User Story:** As front desk staff, I want repeat no-shows flagged, so that we can follow up before booking future appointments.

**Acceptance Criteria (EARS):**
1. WHEN a patient has two or more no-shows within a rolling 12-month period THEN system SHALL flag their record as "at-risk"
2. IF a patient's record is flagged "at-risk" THEN system SHALL display the flag to front desk staff at next booking, without blocking the booking outright (business decision — confirm with stakeholder whether blocking is actually wanted; do not assume)

## Non-Functional Requirements
- **Compliance:** All PHI in reminder content and logs SHALL be encrypted in transit and at rest; third-party delivery providers require a signed BAA (HIPAA) — **confirm current vendor's BAA status before build**
- **Security:** Access to no-show flags and delivery logs restricted to authenticated clinic staff roles
- **Performance:** Reminder dispatch job SHALL complete for a full day's schedule within 15 minutes of the scheduled run

## Out of Scope
- Two-way SMS conversation / chatbot-style rescheduling (only confirm/cancel reply parsing, not open text handling)

## Open Questions
- Does "flagging their file" mean blocking future self-service booking, or just a visible staff-side note? (confirmed as a business decision, not yet resolved)
- What's the current BAA status with the SMS/email provider under consideration?
