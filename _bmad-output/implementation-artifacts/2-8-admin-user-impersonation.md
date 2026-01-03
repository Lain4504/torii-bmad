# Story 2.8: Admin User Impersonation

Status: draft

## Story

As an Admin or authorized Support Staff, I want to impersonate a user, so that I can see exactly what they see on their dashboard and help them troubleshoot technical issues or support requests.

## Acceptance Criteria

1. **Authorization & Security**
   - Only users with `user.impersonate` permission (typically Admins and Support Staff) can initiate impersonation.
   - For security, certain sensitive actions are DISALLOWED while impersonating:
     - Changing the user's password.
     - Changing the user's email or sensitive security settings.
     - Performing financial transactions (optional, depending on center policy).
   - Impersonation session must be clearly distinguishable from a normal session.

2. **Backend Implementation**
   - Endpoint: `POST /admin/users/:userId/impersonate`.
   - Generates a specialized JWT access token and refresh token:
     - Payload includes `sub: {targetUserId}`.
     - Payload includes `impersonatorId: {adminUserId}`.
     - Payload includes `isImpersonating: true`.
   - The session service must track the impersonated session in Redis with a clear flag.
   - Every action taken while impersonating must include the `impersonatorId` in the audit logs.

3. **Frontend Implementation (Admin App)**
   - "Impersonate" action in the User Management table and User Detail page.
   - Successful initiation redirects the admin to the Learner Web App (or remains in admin if troubleshooting admin features) with the impersonated context.
   - A persistent, high-visibility banner must be displayed: "URGENT: You are currently impersonating [User Name]. Actions are being logged."
   - "Stop Impersonation" button in the banner that restores the original Admin session.

4. **Audit & Monitoring**
   - Audit log entry created when impersonation starts: `[ADMIN_ID] started impersonating [USER_ID]`.
   - Audit log entry created when impersonation ends: `[ADMIN_ID] stopped impersonating [USER_ID]`.
   - High-level dashboards show currently active impersonation sessions for security monitoring.

## Tasks / Subtasks

### Backend Tasks

- [ ] **Task 1: RBAC Permission for Impersonation** (AC: #1)
  - [ ] Add `user.impersonate` permission to `rbac-config.yaml`.
  - [ ] Assign `user.impersonate` to `admin` and `staff-support` roles.

- [ ] **Task 2: Impersonation Endpoint** (AC: #2)
  - [ ] Create `impersonateUser(targetUserId)` method in `AuthService`.
  - [ ] Validate that the target user is a `learner` or `lecturer` (prevent impersonating other admins/staff).
  - [ ] Generate JWT with `impersonatorId` and `isImpersonating` claims.
  - [ ] Add audit log entry for the start event.

- [ ] **Task 3: Exit Impersonation Logic** (AC: #3)
  - [ ] Create endpoint `POST /auth/impersonate/exit`.
  - [ ] Invalidate the impersonated token (add to blacklist).
  - [ ] Log the exit event.
  - [ ] Note: The frontend will need to restore the original admin token.

- [ ] **Task 4: Audit Log Enhancement** (AC: #4)
  - [ ] Update `AuditLogService` or middleware to capture `impersonatorId` from JWT if present.
  - [ ] Ensure all subsequent actions in other services (LMS, Meet, etc.) correctly log the impersonator context if the session is an impersonation.

### Frontend Tasks (Web Admin)

- [ ] **Task 5: User Management UI Update** (AC: #3)
  - [ ] Add "Impersonate" button to User table/details.
  - [ ] Implement confirmation dialog: "You are about to enter user's environment. All actions will be logged. Continue?"
  - [ ] Call impersonation API and handle the session switch.

- [ ] **Task 6: Restore Admin Session Logic** (AC: #3)
  - [ ] Store the original Admin tokens in `sessionStorage` or a secure temp location before switching.
  - [ ] Implement "Stop Impersonation" logic to swap tokens back and clear the impersonation flag.

### Frontend Tasks (Web Learner / Shared UI)

- [ ] **Task 7: Impersonation Banner Component** (AC: #3)
  - [ ] Create a globally visible banner (e.g., at the top of the viewport).
  - [ ] Display name of impersonated user and an "Exit" button.
  - [ ] Ensure it doesn't conflict with main navigation.

### Testing Tasks

- [ ] **Task 8: Security and Audit Tests**
  - [ ] Test that non-admins cannot call the impersonate endpoint.
  - [ ] Verify that audit logs contain both `actorId` (the user) and `impersonatorId` (the admin).
  - [ ] Test "Sensitive Action Block" while impersonating (e.g., try changing password).
  - [ ] Verify that exiting impersonation correctly restores access to admin-only features.

## Dev Notes

### Architecture Patterns

**JWT Claims for Impersonation:**
```json
{
  "sub": "user_123",
  "impersonatorId": "admin_456",
  "isImpersonating": true,
  "iat": 1700000000,
  "exp": 1700003600
}
```

**Token Handling:**
- The frontend should treat the impersonation token like a normal access token for API calls.
- The `AuditHistory` should show: "Minh Nguyen (Impersonated by Admin Tuan) updated profile".

### Security Considerations

1. **Hierarchy Check**: Admins should only be able to impersonate users with lower or non-administrative roles (Learners, Lecturers). Admins should NOT be able to impersonate other Admins.
2. **Session Persistence**: Impersonation tokens should have a shorter TTL than normal tokens (e.g., 1 hour, no auto-refresh or restricted refreshing).
3. **Data Privacy**: Admins should still see masked data if implemented (e.g., partial email/phone) unless explicitly required for support.

### Implementation Specifics

| Feature | Technology |
|---------|------------|
| Auth | NestJS JWT, RBAC Guard |
| Frontend | Next.js/Vite, Zustand/Redux for session state |
| Logging | Prisma AuditLog table |
