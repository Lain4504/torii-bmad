# Story 2.2: User Login (Web & Mobile)

Status: done

<!-- Note: This story focuses on FRONTEND integration as Backend Auth is already implemented -->

## Story

As a user (Learner, Lecturer, Staff, Admin),
I want to log in to the application using my email and password,
so that I can access my personalized dashboard and protected features.

## Acceptance Criteria

1.  **Web Learner (Next.js)**
    - [ ] Login page accessible at `/login`
    - [ ] Form validation (email format, required fields) using Zod
    - [ ] Integrates with `POST /api/auth/login`
    - [ ] Stores JWT access token securely (localStorage/cookie)
    - [ ] Redirects to dashboard on success
    - [ ] Displays error messages on failure (invalid credentials)
    - [ ] Protected routes redirect to `/login` if unauthenticated

2.  **Web Admin (Vite + Redux)**
    - [ ] Login page accessible at `/login`
    - [ ] Redux `authSlice` handles login state
    - [ ] Integrates with Gateway API
    - [ ] Stores JWT token
    - [ ] Redirects to admin dashboard on success

3.  **Mobile App (Flutter)**
    - [ ] Login Screen with email/password inputs
    - [ ] Uses `flutter_secure_storage` for token persistence
    - [ ] Riverpod `authProvider` manages global auth state
    - [ ] Error handling with Snackbars
    - [ ] Auto-redirect to Home Screen if token exists on startup

4.  **Security & UX**
    - [ ] "Show Password" toggle on all inputs
    - [ ] Loading state disables submit button (`isLoading`)
    - [ ] Enter key submits the form
    - [ ] Unauthorized (401) responses trigger logout (basic handling)

## Existing Backend API (Reference)

- **Endpoint:** `POST /auth/login` (Gateway) -> `AuthService.login`
- **Payload:** `{ "email": "UserLoginDTO", "password": "..." }`
- **Response:**
  ```json
  {
    "user": { "id": "...", "email": "...", "role": "LEARNER", ... },
    "accessToken": "eyJhbG..."
  }
  ```

## Tasks / Subtasks

- [ ] **Task 1: Web Learner - Auth Setup (Next.js + Redux)** (AC: #1)
  - [ ] Install `@reduxjs/toolkit` and `react-redux`
  - [ ] Configure `StoreProvider` (client component) for Next.js App Router
  - [ ] Create `authSlice` (or share from unused package if available, but keep local for now)
  - [ ] Configure `axios` instance with base URL (env var)
  - [ ] Create `LoginForm` component using `react-hook-form` + `zod`
  - [ ] Create Login Page usage at `app/(auth)/login/page.tsx`
  - [ ] Implement middleware or HOC for protected routes

- [ ] **Task 2: Web Admin - Auth Setup (Vite + Redux)** (AC: #2)
  - [ ] Create `authSlice` in Redux Toolkit (if not existing)
  - [ ] Create `Login` page component using shadcn/ui
  - [ ] Connect login form to `authSlice` async thunk
  - [ ] Configure Axios instance with interceptors
  - [ ] Add `RequireAuth` component for route protection

- [ ] **Task 3: Mobile App - Auth Setup (Flutter)** (AC: #3)
  - [ ] Verify `flutter_secure_storage` and `flutter_riverpod` setup
  - [ ] Create `AuthRepository` with Dio client
  - [ ] Create `AuthNotifier` (Riverpod) for state management
  - [ ] Implement `LoginScreen` UI with Material 3 inputs
  - [ ] Wire up GoRouter redirection based on auth state

- [ ] **Task 4: Integration Verification** (AC: #4)
  - [ ] Verify Web Learner login (Redux state update)
  - [ ] Verify Web Admin login
  - [ ] Verify Mobile login
  - [ ] Test error cases (wrong password, server down)

## Dev Notes

### Architecture
- **Tech Stack Unification:** All web apps (`web-learner`, `web-admin`, `meet`) use **Redux Toolkit** for consistent state management.
- **Mobile:** Uses **Riverpod** (Flutter standard).

### Environment Variables
Ensure `.env` (or comparable) has:
- `NEXT_PUBLIC_API_URL=http://localhost:8080` (Gateway)
- `VITE_API_URL=http://localhost:8080`
- Mobile: Use correct localhost IP for emulator (`10.0.2.2` vs `localhost`)

### Reference Files
- Backend Logic: `apps/server/modules/identity/src/modules/auth/auth.service.ts`
- Gateway: `apps/server/modules/gateway/src/gateway.module.ts`

## Next Steps
- After login is working, we will proceed to **Story 2.1 (Registration)** and **Story 2.3 (Refresh Token)**.
