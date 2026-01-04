# Story 12.6: Email Notifications

Status: ready-for-dev

## Story

As a User,
I want to receive essential updates via email,
so that I have a persistent record of important transactions and alerts outside the app.

## Acceptance Criteria

1. **Transactional Emails**:
   - Welcome/Verify Email (Already done in 2-9, verify/audit).
   - Payment Receipt / Invoice.
   - Password Reset.
   - "You have been enrolled in Course X".
2. **Design**:
   - Branded HTML templates (responsive).
   - "View in Browser" link.
   - Unsubscribe link (for marketing types, not transactional).

## Tasks / Subtasks

- [ ] Select/Config Provider
  - [ ] Resend or AWS SES.
- [ ] Build Template Engine
  - [ ] React Email or Handlebars.
- [ ] Implement Notification Service Email worker.

## Dev Notes

### Technical Requirements
- Robust error handling/retries for delivery failures.

### References
- Epic 12, FR64.
