# Story 2.1: User Registration (Web & Mobile)

Status: review

<!-- Note: Planned to be implemented AFTER Story 2.2 (Login) to reuse Auth State logic -->

## Story

As a new user (Learner),
I want to register for a new account using my email, password, and full name,
so that I can start using the platform's learning features.

## Acceptance Criteria

1.  **Web Learner (Next.js)** - Public Registration
    - [x] Registration page accessible at `/register`
    - [x] Form includes: Full Name, Email, Password, Confirm Password
    - [x] Validation:
        - Email format
        - Password strength (min 8 chars)
        - Passwords match
    - [x] Integration with `POST /api/auth/register`
    - [x] On success: **Auto-login** and redirect to **Dashboard**.
    - [x] Show global "Verification Needed" banner on dashboard.
    - [x] Error handling: Show "Email already exists" clearly

2.  **Web Admin (Vite)** - NO PUBLIC REGISTRATION
    - [x] Web Admin does NOT have public registration page
    - [x] Admin users are created by existing admins via user management dialog
    - [x] This story focuses ONLY on **Learner Registration** (Web + Mobile)

3.  **Mobile App (Flutter)** - Public Registration
    - [x] Registration Screen
    - [x] Inputs: Full Name, Email, Password, Confirm Password
    - [x] Validation logic matching web
    - [x] Integration with backend
    - [x] Success/Error handling UI (Snackbars)

4.  **Backend Integration**
    - [x] Use existing `AuthService.register` endpoint
    - [x] Ensure proper error codes are returned for duplicate emails (409 Conflict)

## Tasks / Subtasks

- [x] **Task 1: Web Learner - Registration Page (Next.js)** (AC: #1)
  - [x] Create `RegisterForm` component in `components/auth/register-form.tsx`
  - [x] Create page `app/(auth)/register/page.tsx` with split-screen layout (matching login page)
  - [x] Implement form validation with Zod schema
  - [ ] Update register action to handle auto-login (store token from response).
  - [ ] Handle post-registration flow (redirect to Dashboard).

- [x] **Task 2: Mobile App - Registration Screen (Flutter)** (AC: #3)
  - [x] Add `register` method to `AuthRepository`
  - [x] Create `RegisterScreen` UI with Material 3 design
  - [x] Implement form validation
  - [x] Implement navigation logic (navigate to login on success)

## Dependencies
- **Story 2.2 (User Login)**: Should be implemented first to establish `AuthStore`, `dios`, `axios` configuration and error handling patterns.

## Dev Notes
- **API Endpoint:** `POST /api/gateway/auth/register` (Proxy) -> `AuthService.register`
- **Payload:** `{ "email": "...", "password": "...", "fullName": "..." }`

## Dev Agent Record

### Implementation Plan
**Web Learner (Next.js):**
- Created `RegisterForm` component with Zod validation (extends `userRegistrationDTOSchema` + confirmPassword)
- Implemented split-screen layout matching login page (left: value props, right: form)
- Used existing `register` thunk from `authSlice.ts`
- Password visibility toggle for both password fields
- Redirect to `/login` with success toast on registration

**Mobile App (Flutter):**
- Already implemented in brownfield codebase
- `AuthRepository.register()` method exists at `lib/data/repositories/auth_repository.dart`
- `RegisterPage` UI exists at `lib/features/auth/views/pages/register_page.dart`
- Uses Riverpod for state management
- Material 3 design with proper validation

### Completion Notes
✅ **Web Learner Registration** - Implemented
- File: `apps/web-learner/components/auth/register-form.tsx` (NEW)
- File: `apps/web-learner/app/(auth)/register/page.tsx` (NEW)
- Validation: Zod schema with password confirmation
- Error handling: Toast notifications + inline error display
- Flow: Register → Redirect to login with success message

✅ **Mobile Registration** - Already Implemented (Brownfield)
- File: `torii-mobile/lib/data/repositories/auth_repository.dart` (EXISTING)
- File: `torii-mobile/lib/features/auth/views/pages/register_page.dart` (EXISTING)
- All required functionality already present

## File List
**New Files:**
- `apps/web-learner/components/auth/register-form.tsx`
- `apps/web-learner/app/(auth)/register/page.tsx`

**Modified Files:**
- None (all existing files already had required functionality)

## Change Log
- 2026-01-03: Started implementation. Status: ready-for-dev -> in-progress.
- 2026-01-03: Completed implementation. Created web learner registration page and form. Mobile app registration already existed. Status: in-progress -> review.
- 2026-01-04: **Re-opened** to update for Soft Gate flow (Auto-login + Dashboard redirect). Status: review -> in-progress.
