# Story 2.5: RBAC Implementation

Status: draft

## Story

As an admin, I want a comprehensive role-based access control (RBAC) system, so that I can ensure only authorized users can access specific features and data across the platform.

## Acceptance Criteria

1. **Role & Permission Definitions**
   - Implement roles: `admin`, `staff`, `staff-lms`, `staff-support`, `staff-sales`, `lecturer`, `learner`.
   - Implement granular permissions grouped by categories (Course, Class, Assessment, Content, User, Payment, Analytics, System).
   - Support role inheritance (e.g., `staff-lms` inherits from `staff`).

2. **Backend Enforcement (Guards & Decorators)**
   - Create `@Roles(...roles: UserRole[])` decorator to restrict access by role.
   - Create `@Permissions(...permissions: string[])` decorator to restrict access by specific permission codes.
   - Implement `RBACGuard` in the shared library to enforce these decorators.
   - Add the guard to all sensitive controllers in the `Identity` service.

3. **Database Seeding & Persistence**
   - Ensure the database is seeded with initial roles and permissions from `rbac-config.yaml`.
   - Support audit logging for all permission changes (who changed what role's permissions).

4. **Frontend Integration (Learner & Admin/Staff)**
   - Create a `CanAccess` wrapper component to conditionally render UI elements based on permissions.
   - Create a `usePermission(permissionCode: string)` hook for logic-level checks.
   - Implement route guards in Next.js (Learner) and Vite (Admin) to prevent unauthorized page access.
   - Redirect unauthorized users to a "403 Forbidden" page.

5. **NATS Pre-requisites**
   - Ensure the RBAC service is ready to be used by the NATS Auth Callout (Story 2.6) for dynamic pub/sub permissioning.

## Tasks / Subtasks

### Backend Tasks

- [ ] **Task 1: Update UserRole Enum** (AC: #1)
  - [ ] Add `STAFF_LMS`, `STAFF_SUPPORT`, `STAFF_SALES` to `UserRole` enum in `packages/schemas`.
  - [ ] Update Zod schemas to include these new roles.

- [ ] **Task 2: Define RBAC Decorators** (AC: #2)
  - [ ] Create `roles.decorator.ts` in `@server/shared`.
  - [ ] Create `permissions.decorator.ts` in `@server/shared`.

- [ ] **Task 3: Implement RBACGuard** (AC: #2)
  - [ ] Create `rbac.guard.ts` in `@server/shared/guards`.
  - [ ] Logic:
    - Extract required roles/permissions from Reflector.
    - If none specified, allow access (or default to auth-only).
    - Get current user's role and permissions from `RBACService`.
    - Handle Admin wildcard (`*`).
    - Support role-based OR permission-based checks.

- [ ] **Task 4: Integrate Guards into Controllers** (AC: #2)
  - [ ] Apply `@UseGuards(RBACGuard)` and decorators to `UsersController`.
  - [ ] Apply to `RBACController`.
  - [ ] Apply to `AuditLogController`.

- [ ] **Task 5: Verify & Run RBAC Seeder** (AC: #3)
  - [ ] Test `RBACSeederService` with current `rbac-config.yaml`.
  - [ ] Create a script to trigger manual re-seed if config changes.

### Frontend Tasks (Web Learner - Next.js)

- [ ] **Task 6: RBAC Context/Hooks** (AC: #4)
  - [ ] Create `useUserPermissions()` hook to extract permissions from Redux auth state.
  - [ ] Create `CanAccess` component for conditional rendering.

- [ ] **Task 7: Route Protection Middleware** (AC: #4)
  - [ ] Update Next.js middleware or create a Higher-Order Component (HOC) to protect routes.
  - [ ] Map routes to required permissions (e.g., `/settings/security` might require `user.manage`).

### Frontend Tasks (Web Admin - Vite)

- [ ] **Task 8: Admin RBAC Security** (AC: #4)
  - [ ] Implement similar `CanAccess` and `usePermission` logic in the Vite app.
  - [ ] Protect nested dashboard routes based on Staff variant (e.g., LMS Staff only sees Course mgmt).

### Testing Tasks

- [ ] **Task 9: Integration Tests**
  - [ ] Test that a Learner cannot access Admin routes (403).
  - [ ] Test that a Lecturer has access to assigned permissions but not others.
  - [ ] Test that Admin wildcard works across all endpoints.
  - [ ] Test that revoking a permission in the DB takes immediate effect (after session refresh or token expiry).

## Dev Notes

### Architecture Patterns

**Permission Checking Logic:**
1. Check if user is `admin` → **Grant All**.
2. Check if user has required **Role** (if `@Roles` specified).
3. Check if user has required **Permission** (if `@Permissions` specified).
4. If either check passes (OR logic) or both required (AND logic - to be determined), grant access.
5. Default: Deny.

**Performance:**
- Cache user permissions in Redis (TTL matched to Access Token) to avoid repeated DB lookups on every request.
- *Optional:* Include permissions in JWT payload (only if payload size stays small).

**Frontend Role-Specific UI:**
```tsx
<CanAccess permission="course.create">
  <Button>Create Course</Button>
</CanAccess>
```

### Security Considerations

1. **Fail-Safe Defaults:** If a guard is present but no specific metadata is found, the system should default to the strictest setting (Authenticated Admin only or Deny).
2. **Token Integrity:** Ensure roles/permissions cannot be tampered with on the client side (Backend is the source of truth).
3. **Granularity vs Complexity:** Keep the permission list manageable but detailed enough to support the 3 Staff variants.

### Implementation Specifics

| Feature | Technology |
|---------|------------|
| Backend | NestJS Guards, Reflector |
| Database | Prisma (RolePermission, UserPermission tables) |
| Configuration | YAML (rbac-config.yaml) |
| Frontend | Next.js/React, Redux Toolkit |
| Caching | Redis (for permission lookup) |
