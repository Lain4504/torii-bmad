# Story 2.9: Email Verification

Status: ready-for-dev

<!-- Note: Processed via validate-create-story - Ultimate context applied to prevent implementation disasters. -->

## Story

As a learner,
I want to verify my email address using a 6-digit OTP,
so that my account is secure and I can receive important course notifications.

## Acceptance Criteria

1. **Trigger on Registration:** Upon successful registration (Story 2.1), a verification email is automatically sent to the user's provided address.
2. **Verification OTP:** The email contains a unique 6-digit OTP, short-lived (expires in 24 hours).
3. **Verification UI:** A dedicated verification page handles the 6-digit input using the project's OTP component standards.
4. **Backend Endpoint:** `POST /auth/verify-email` confirms the OTP against Redis, updates `isEmailVerified` in the database, and returns a success status.
5. **Trigger on Email Change:** When a user updates their email in their profile, the change remains "pending" until the new address is verified via OTP.
6. **Rate Limiting:** Resend verification requests are rate-limited to max 3 requests per hour per user/IP.
7. **Security:** OTPs must be stored securely in Redis with TTL; subsequent failed attempts (max 5) should invalidate the OTP.

## Tasks / Subtasks

- [ ] **Backend Implementation (NestJS)**
  - [ ] **Refactor**: Ensure User model supports `emailVerified` (boolean) and `pendingEmail` (string) for change flows.
  - [ ] Implement OTP generation logic (6-digit numeric) and storage in Redis with 24h expiration.
  - [ ] **Security**: Implement rate limiting for `/auth/resend-verification` (3 req/hr) using `ThrottlerModule` or Redis-based guard.
  - [ ] Create `POST /auth/resend-verification` endpoint.
  - [ ] Create `POST /auth/verify-email` endpoint (validates OTP, updates DB status, clears Redis).
  - [ ] **Event**: Emit NATS event `auth.user.registered` with payload: `{ email: string, otp: string, locale: string }`.
- [ ] **Notification Service**
  - [ ] Create email template for OTP Verification (Vietnamese primary, English fallback).
  - [ ] Handle `auth.user.registered` event to send the email via configured SMTP/Mock service.
- [ ] **Frontend (Web Learner & Mobile)**
  - [ ] **Component**: Implement `input-otp` from `shadcn/ui` on the verification page (`/verify`).
  - [ ] Implement "Resend OTP" button with a 60-second cooldown timer + server-side rate limit handling.
  - [ ] **Error Handling**: Implement specific UI feedback for `OTP_EXPIRED`, `INVALID_OTP`, and `THROTTLED`.
  - [ ] Ensure the OTP flow works seamlessly across Web and Mobile (unified OTP validity).

## Dev Notes

- **OTP Standard:** Use a 6-digit numeric code to maximize compatibility with mobile devices.
- **Service Communication:** The Identity Service emits the event; the Notification Service is the ONLY service that sends emails.
- **Persistence:** OTPs reside in Redis ONLY for speed and auto-expiration. The database only stores the final `isEmailVerified` state.
- **Architecture Compliance:** Follow the `GatewayAuthGuard` patterns established in the server for protected routes.

### Project Structure Notes

- Backend logic: `apps/server/src/modules/auth`.
- Email templates: `apps/server/src/modules/notifications/templates`.
- Frontend views: `apps/web-learner/src/app/(auth)/verify`.
- Shared UI: `packages/ui/src/components/input-otp.tsx`.

### References

- [Source: _bmad-output/planning-artifacts/prd.md#US.LEARN.10]
- [Source: _bmad-output/planning-artifacts/architecture.md#Security & Compliance]
- [Source: _bmad-output/planning-artifacts/epics.md#Epic 2]

## Dev Agent Record

### Agent Model Used

Antigravity (Gemini 2.0 Flash)

### Debug Log References

- Unified OTP logic (Link-based flow removed to avoid confusion with mobile deep-linking complexity).
- Added explicit Rate Limiting tasks.
- Defined NATS event schema for Notification Service integration.

### Completion Notes List

### File List
