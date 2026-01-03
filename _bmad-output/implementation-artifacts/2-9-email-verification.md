# Story 2.9: Email Verification

Status: ready-for-dev

<!-- Note: Validation is optional. Run validate-create-story for quality check before dev-story. -->

## Story

As a learner,
I want to verify my email address after registration or change,
so that my account is secure and I can receive important course notifications.

## Acceptance Criteria

1. **Trigger on Registration:** Upon successful registration (Story 2.1), a verification email is automatically sent to the user's provided address.
2. **Verification Token:** The email contains a unique, high-entropy, short-lived (e.g., 24 hours) verification token/link.
3. **Verification Endpoint:** A GET endpoint `/auth/verify-email?token=...` confirms the token, updates the user's `isEmailVerified` status in the database, and redirects to a success page.
4. **Trigger on Email Change:** When a user updates their email in their profile, the change remains "pending" until verified via the new address.
5. **Notification Service Integration:** Leverage the `Notification Service` (per Architecture) via NATS to trigger the actual email sending.
6. **Rate Limiting:** Resend verification requests are rate-limited to prevent spam (max 3 per hour).
7. **Security:** Verification tokens must be hashed in the database (matching token logic for passwords).

## Tasks / Subtasks

- [ ] **Backend Implementation (NestJS)**
  - [ ] Update User model in Prisma to include `isEmailVerified` (Boolean) and `verificationToken` (String, nullable).
  - [ ] Implement `VerificationToken` generation logic (using `crypto` or similar).
  - [ ] Create `POST /auth/resend-verification` endpoint.
  - [ ] Create `GET /auth/verify-email` endpoint logic.
  - [ ] Emit NATS event `auth.user.registered` for Notification Service.
- [ ] **Notification Service**
  - [ ] Create email template for Verification (Vietnamese primary, English fallback).
  - [ ] Integrate with an SMTP provider or Mock service for Dev/Staging.
- [ ] **Frontend (Web Learner & Mobile)**
  - [ ] Show "Verify your email" banner for unverified accounts.
  - [ ] Create dedicated "Verification Success/Failure" pages.
  - [ ] Implement "Resend Email" button with countdown/throttling.

## Dev Notes

- **Language:** The email content MUST be in Vietnamese by default (per PRD Market preference).
- **Service Communication:** The Identity Service should NOT send emails directly. It should emit an event to NATS, and the Notification Service should handle the delivery.
- **Persistence:** Ensure `prisma.user.update` handles the verification status atomically.
- **Testing:** Unit test the token expiration logic and the token validation service.

### Project Structure Notes

- Backend logic in `apps/server/src/modules/auth`.
- Email templates in `apps/server/src/modules/notifications/templates`.
- Frontend views in `apps/web-learner/src/app/(auth)/verify`.

### References

- [Source: _bmad-output/planning-artifacts/prd.md#US.LEARN.10]
- [Source: _bmad-output/planning-artifacts/architecture.md#Backend Microservices]
- [Source: _bmad-output/planning-artifacts/epics.md#Epic 2]

## Dev Agent Record

### Agent Model Used

Antigravity (Gemini 2.0 Flash)

### Debug Log References

### Completion Notes List

### File List
