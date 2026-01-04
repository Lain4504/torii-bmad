# Story 2.9: Email Verification (Magic Link)

Status: ready-for-dev

<!-- Note: Updated Processed via validate-create-story - Magic Link & Soft Gate Update -->

## Story

As a learner,
I want to verify my email address by clicking a "Magic Link" sent to my inbox,
so that I can prove ownership of my account without typing codes, while still accessing the platform immediately.

## Acceptance Criteria

1.  **Immediate Access (Soft Gate):** Upon registration, the user is **logged in immediately** and redirected to the Dashboard. They are NOT blocked by a verification screen.
2.  **Magic Link Email:** A verification email is sent immediately. It contains a clickable link: `https://torii-platform.com/verify?token=XYZ` (Web) or `torii://verify?token=XYZ` (Mobile Deep Link).
3.  **Token Security:**
    *   One-time use only.
    *   Expires in 15 minutes.
    *   Cryptographically signed (JWT or random string stored in Redis).
4.  **Verification Banner:** Unverified users see a persistent "Verification Needed" banner on all pages.
5.  **Restricted Actions (Hard Gate):** Unverified users **CANNOT**:
    *   Purchase courses.
    *   Join Live Classes.
    *   Post comments/reviews.
6.  **Allowed Actions:** Unverified users **CAN**:
    *   Browse catalog.
    *   Watch intro videos.
    *   Update profile.
7.  **Verification Endpoint:** `GET /auth/verify-link?token=...` verifies the token, updates `emailVerified=true`, and redirects to a "Success" page.

## Tasks / Subtasks

- [ ] **Backend Implementation (NestJS)**
    - [ ] **Data Model**: Ensure `emailVerified` (boolean) exists in User model.
    - [ ] **Token Logic**: Create `MagicLinkService` to generate signed tokens (15m expiry) and store in Redis.
    - [ ] **Endpoint**: Create `POST /auth/send-magic-link` (triggered by Reg or "Resend" button).
    - [ ] **Endpoint**: Create `GET /auth/verify-magic-link` that accepts `token`, verifies it, updates DB, and redirects.
    - [ ] **Guard**: Implement `VerifiedGuard` to block `Purchase` and `LiveClass` routes for unverified users.

- [ ] **Notification Service**
    - [ ] Update Email Template: Replace OTP code design with a "Verify Email" button (Magic Link).

- [ ] **Frontend (Web Learner & Mobile)**
    - [ ] **Banner**: Create `VerificationBanner` component (Global Layout).
    - [ ] **Interceptors**: Update API clients to handle `403 Unverified` errors by showing a "Verify to continue" modal.
    - [ ] **Success Page**: Create `/verify/success` page to land on after clicking the link.
    - [ ] **Mobile**: Configure Deep Linking (Universal Links / App Links) to handle `torii://verify`.

## Dev Notes

- **One-Click vs Deep Link**: Ensure the email template uses a URL that the backend can redirect intelligently, OR use a Universal Link that opens the App directly on mobile.
- **Security**: The token should be invalidated immediately after use ("burn after reading").
- **UX**: "Soft Gate" means we must capture the user's attention *persuasively* (via the Banner) rather than *coercively* (via a Block Screen).

### References

- [Source: _bmad-output/planning-artifacts/prd.md#US.LEARN.12] (Magic Link)
- [Source: _bmad-output/planning-artifacts/prd.md#US.LEARN.13] (Soft Gate)
- [Source: _bmad-output/planning-artifacts/architecture.md#VerifiedGuard]
- [Source: _bmad-output/planning-artifacts/epics.md#Epic 2]
