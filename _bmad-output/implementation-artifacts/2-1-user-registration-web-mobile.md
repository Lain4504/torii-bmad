# Story 2.1: User Registration (Web & Mobile)

Status: backlog

<!-- Note: Planned to be implemented AFTER Story 2.2 (Login) to reuse Auth State logic -->

## Story

As a new user (Learner),
I want to register for a new account using my email, password, and full name,
so that I can start using the platform's learning features.

## Acceptance Criteria

1.  **Web Learner (Next.js)**
    - [ ] Registration page accessible at `/register`
    - [ ] Form includes: Full Name, Email, Password, Confirm Password
    - [ ] Validation:
        - Email format
        - Password strength (min 8 chars)
        - Passwords match
    - [ ] Integration with `POST /api/auth/register`
    - [ ] On success: Auto-login OR redirect to login with success message
    - [ ] Error handling: Show "Email already exists" clearly

2.  **Web Admin (Vite)**
    - [ ] (Optional/Internal) Admin user creation usually handled by existing admins or seed scripts.
    - [ ] If public admin registration is required (rare), implement similar to Learner.
    - [ ] For now: Focus on **Learner Registration**.

3.  **Mobile App (Flutter)**
    - [ ] Registration Screen
    - [ ] Inputs: Full Name, Email, Password, Confirm Password
    - [ ] Validation logic matching web
    - [ ] Integration with backend
    - [ ] Success/Error handling UI (Snackbars)

4.  **Backend Integration**
    - [ ] Use existing `AuthService.register` endpoint
    - [ ] Ensure proper error codes are returned for duplicate emails (409 Conflict)

## Tasks / Subtasks

- [ ] **Task 1: Web Learner - Registration (Next.js)** (AC: #1)
  - [ ] Create `RegisterForm` component (refactor common logic from `LoginForm` if possible)
  - [ ] Create page `app/(auth)/register/page.tsx`
  - [ ] Implement API call to register endpoint
  - [ ] Handle post-registration flow (Reuse `useAuthStore.login` if auto-login)

- [ ] **Task 2: Mobile App - Registration (Flutter)** (AC: #3)
  - [ ] Add `register` method to `AuthRepository`
  - [ ] Create `RegisterScreen` UI
  - [ ] Implement navigation logic (pop to login or go home)

- [ ] **Task 3: Integration Testing**
  - [ ] Verify new user creation in DB
  - [ ] Verify error for duplicate email

## Dependencies
- **Story 2.2 (User Login)**: Should be implemented first to establish `AuthStore`, `dios`, `axios` configuration and error handling patterns.

## Dev Notes
- **API Endpoint:** `POST /api/gateway/auth/register` (Proxy) -> `AuthService.register`
- **Payload:** `{ "email": "...", "password": "...", "fullName": "..." }`
