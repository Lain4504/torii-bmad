# Story 2.3: JWT Refresh Token Flow

Status: ready-for-dev

<!-- Note: This story requires careful handling of platform-specific auth patterns (Cookie vs Bearer) -->

## Story

As a user (Learner, Lecturer, Staff, Admin),
I want my session to stay active automatically while I am using the application,
so that I am not interrupted by login screens when my short-lived access token expires.

## Acceptance Criteria

### 1. Web Applications (Cookie-Based Flow)
**Context:** Next.js (Learner) and Vite (Admin/Meet) use **HttpOnly Cookies** for both Access and Refresh tokens. JS cannot read these tokens.
- [ ] **Axios Configuration**:
  - [ ] `withCredentials: true` enabled globally (ensures cookies are sent).
  - [ ] Base URL configured for Gateway.
- [ ] **Interceptor Logic**:
  - [ ] Intercepts `401 Unauthorized` responses.
  - [ ] Checks if it's a token expiration error (vs invalid credentials).
  - [ ] **Action**: Calls `POST /auth/refresh` (Browser automatically sends `refresh_token` cookie).
  - [ ] **Success**: Retries the original failed request (Browser automatically sends new `access_token` cookie).
  - [ ] **Failure**: Redirects to `/login` (clears local user state).
  - [ ] **Queueing**: If multiple requests fail simultaneously, queue them and process after one refresh (avoid race conditions).

### 2. Mobile Application (Token-Based Flow)
**Context:** Flutter uses **Bearer Tokens** handled manually. Tokens are stored in secure storage.
- [ ] **Dio Configuration**:
  - [ ] `Authorization` header injected with Access Token from storage.
  - [ ] `x-platform: mobile` header added to login/refresh requests (CRITICAL: tells backend to return tokens in body).
- [ ] **Interceptor Logic**:
  - [ ] Intercepts `401 Unauthorized`.
  - [ ] Locks Request Queue (prevent parallel refreshes).
  - [ ] Reads `refresh_token` from `FlutterSecureStorage`.
  - [ ] **Action**: Calls `POST /auth/refresh` with body `{ refresh_token: "..." }`.
  - [ ] **Success**:
    - [ ] Updates `FlutterSecureStorage` with new Access and Refresh tokens.
    - [ ] Updates Dio instance with new Access Token.
    - [ ] Retries original request.
    - [ ] Unlocks Queue.
  - [ ] **Failure**:
    - [ ] Deletes tokens from storage.
    - [ ] Redirects to Login Screen.

### 3. Shared Requirements
- [ ] **Loop Prevention**: Ensure the interceptor doesn't retry the `/auth/refresh` endpoint itself (infinite loop risk).
- [ ] **Logout Handling**:
  - [ ] Explicit logout calls `POST /auth/logout` to revoke tokens on server.

## Tasks / Subtasks

- [ ] **Task 1: Web Client Interceptor (Shared Logic)** (AC: #1)
  - [ ] Create `setupAxiosInterceptors` utility function in shared lib (or copy to both projects).
  - [ ] Implement `401` detection logic.
  - [ ] Implement "Refresh Queue" pattern (process queue on success/fail).
  - [ ] Integrate into Next.js root layout or provider.
  - [ ] Integrate into Vite `main.tsx` or auth store.
  - [ ] **Verification**: Wait for access token expiry (15m) or manually invalidate cookie, verify smooth refresh.

- [ ] **Task 2: Mobile Client Interceptor (Flutter)** (AC: #2)
  - [ ] Update `AuthRepository` to include `refreshToken` method.
  - [ ] Create `AuthInterceptor` class extending `QueuedInterceptor`.
  - [ ] Implement `onError` override for 401 handling.
  - [ ] Implement `x-platform: mobile` header injection.
  - [ ] **Verification**: Manually expire token or mock 401, verify transparent refresh.

## Dev Notes

### Architecture Criticals
- **Backend Behavior**: The `AuthController` behaves differently based on `x-platform` header.
  - **Web**: Expects/Sets Cookies. Returns `{ success: true, message: ... }`.
  - **Mobile**: Expects/Returns JSON Body. Returns `{ success: true, data: { access_token, ... } }`.
- **Security**:
  - Web Access Token is **HttpOnly**. You cannot read it in JS. Do NOT try to set `Authorization` header in Web App.
  - Mobile MUST use `FlutterSecureStorage`. Never shared preferences.

### Code References
- **Types**: `UserLoginDTO`, `UserRegistrationDTO` in `@workspace/schemas`.
- **Backend Ref**: `apps/server/modules/identity/src/interfaces/http/auth.controller.ts` (Login/Refresh logic).

### Tech Specs
- **Web**: `axios`, `jwt-decode` (optional, for debugging, but cant read HttpOnly cookie).
- **Mobile**: `dio` (use `QueuedInterceptor` for concurrency safety).

## Dev Agent Record

### Agent Model Used
{{agent_model_name_version}}

### File List
