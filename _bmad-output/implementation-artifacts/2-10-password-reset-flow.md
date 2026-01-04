# Story 2.10: Password Reset Flow

Status: ready-for-dev

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a user,
I want to be able to reset my password via email,
so that I can regain access to my account if I forget my credentials.

## Acceptance Criteria

1. **Request Reset:** A "Forgot Password" link on the login page allows users to enter their email address.
2. **Security Timing:** The system sends a reset email only if the account exists, but the UI response should be generic ("If an account exists, an email has been sent") to prevent user enumeration.
3. **Reset Token:** The email contains a secure, high-entropy, one-time-use token with a short expiration (15 minutes).
4. **Validation:** The reset page validates the token before allowing the user to enter a new password.
5. **Password Policy:** The new password must meet the strong password requirements defined in `ENH-REQ-1` (min 8 chars, complexity).
6. **Session Invalidation:** Upon successful password reset, all current active sessions (Story 2.7) and refresh tokens (Story 2.3) for that user must be invalidated in Redis.
7. **Notification:** A confirmation email is sent to the user after a successful password change notifying them of the activity.

## Tasks / Subtasks

- [ ] **Backend Implementation (NestJS)**
  - [ ] Create `POST /auth/forgot-password` (generates token, emits NATS event).
  - [ ] Create `POST /auth/reset-password` (validates token, updates DB, clears Redis sessions).
  - [ ] Implement `ResetToken` schema/table in redis (includes `expiresAt` and `used` flag).
- [ ] **Notification Service**
  - [ ] Create "Password Reset Request" email template (Vietnamese).
  - [ ] Create "Password Changed Confirmation" email template (Vietnamese).
- [ ] **Frontend (Web & Mobile)**
  - [ ] Create "Forgot Password" request form.
  - [ ] Create "Reset Password" entry form with strength meter.
  - [ ] Create success/link-expired state views.

## Dev Notes

- **Token Disposal:** Tokens must be deleted or marked as used immediately after use to prevent reuse attacks.
- **Rate Limiting:** Apply strict rate limiting on the `/forgot-password` endpoint to prevent mail server abuse.
- **Security:** Ensure the reset link uses HTTPS (`NFR24`).
- **Email Notification:** Log all password reset attempts (success and failure) for the audit trail (`NFR23`). Send email to user to notify users when their password has changed.
- **Notification**: Create notification in database in notification schema.


### Project Structure Notes

- Backend logic in `apps/server/src/modules/auth`.
- Frontend forms in `apps/web-learner/src/app/(auth)/forgot-password` and `apps/web-learner/src/app/(auth)/reset-password`.

### References

- [Source: _bmad-output/planning-artifacts/prd.md#ENH-REQ-1]
- [Source: _bmad-output/planning-artifacts/architecture.md#Authentication & Security]
- [Source: _bmad-output/planning-artifacts/epics-stories-summary.md#Story 2.10]

## Dev Agent Record

### Agent Model Used

Antigravity (Gemini 2.0 Flash)

### Debug Log References

### Completion Notes List

### File List
