# Sprint Change Navigation

## Context
**Trigger**: Switch to Magic Link verification & "Soft Gate" (Delayed Verification).
**Analysis Strategy**: Incremental Review.

---

## 1. Feature Restriction Analysis (Approved)

The following restriction model has been adopted for **Unverified Users**:

| Action | Status | Rationale |
| :--- | :--- | :--- |
| **Login / Dashboard Access** | ✅ **Allowed** | Immediate access keeps momentum. User feels "inside". |
| **Browsing Course Catalog** | ✅ **Allowed** | Essential for conversion. Let them see what they can buy. |
| **Viewing "Preview" Videos** | ✅ **Allowed** | "Try before you buy" requires no trust. |
| **Updating Profile** | ✅ **Allowed** | Let them own their identity (Avatar, Name). |
| **Purchasing Courses (Checkout)** | ⛔ **BLOCKED** | **Rationale**: We need a verified email to send receipts, gifting codes, and handle payment disputes securely. |
| **Joining Live Classes** | ⛔ **BLOCKED** | **Rationale**: Security & Safety. Real-time WebRTC access should be gated to trusted users to prevent anonymous disruption. |
| **Posting Reviews/Comments** | ⛔ **BLOCKED** | **Rationale**: Spam prevention. |

**UX Implication**: 
- Unverified users see a persistent **"Verification Banner"**.
- Attempting a restricted action triggers a **"Verify your email to continue"** modal.

---

## 2. Technical Impact (Magic Link Only)

- **Remove**: 6-digit OTP UI, `verify-otp` endpoints.
- **Add**: 
    - `POST /auth/magic-link`: Generates token, sends email.
    - `GET /auth/verify-magic-link?token=xyz`: Validates token, sets `emailVerified=true`.
    - **Guardian**: `VerifiedGuard` interceptor on Backend, checking `emailVerified` claim.
    - **Mobile**: Deep Link handling (`torii://verify`) to open App from Email.

---

## 3. Execution Report

The following artifacts have been updated to reflect these changes:

### ✅ Architecture Document
- Added `VerifiedGuard` specification.
- Defined **Magic Link** security (15 min expiry, 1-time use).
- Updated Authentication flow to include **Soft Gate**.

### ✅ Product Requirements Document (PRD)
- Updated **User Journey 1 (Minh)** to demonstrate the new frictionless flow.
- Added **US.LEARN.12** (Magic Link) and **US.LEARN.13** (Soft Gate).

### ✅ Epics
- Updated **Epic 2** to include Magic Link outcomes.
- Added new FRs to the coverage map.

### ✅ User Stories
- **Story 2.9 (Email Verification)**: COMPLETELY REWRITTEN.
    - Defined specific Magic Link acceptance criteria.
    - Added tasks for `VerificationBanner` and `VerifiedGuard`.
- **Story 2.1 (Registration)**: UPDATED.
    - Success criteria changed from "Redirect to Login" to "Auto-Login + Redirect to Dashboard".

---

## 4. Implementation Handoff

The Analysis phase is **COMPLETE**. The following stories are now **READY FOR DEV**:

1.  **Story 2.1 (Update)**: Modify registration logic to auto-login.
    - *Impact*: Low (Frontend redirection logic).
2.  **Story 2.9 (New Feature)**: Implement Magic Link full stack.
    - *Impact*: High (New Backend Service, New Frontend Page, Mobile Deep Linking).

**Next Step**: Developer can pick up Story 2.9 to begin implementation.
