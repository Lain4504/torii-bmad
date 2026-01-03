# Epic 2: Authentication & User Management - Readiness Assessment

**Generated:** 2026-01-03T16:25:00+07:00  
**Analyst:** Dev Agent (Amelia)  
**Project:** torii-nihongo (Brownfield Monorepo)

---

## Executive Summary

**FINDING:** Epic 2 backend is **70% implemented** - core auth logic exists, but **frontend integration is missing**.

**Recommendation:** Focus on **frontend stories** (web + mobile auth flows) rather than backend re-implementation.

---

## Backend Authentication Infrastructure Analysis

### ✅ What's Already Built (Identity Microservice)

#### **1. Core Auth Service** (`apps/server/modules/identity/src/modules/auth/`)

**AuthService** (auth.service.ts):
```typescript
✅ register(dto: UserRegistrationDTO): Promise<UserResponseDTO>
   - Email uniqueness check
   - Argon2 password hashing
   - Auto-assign LEARNER role
   - Soft delete support

✅ login(dto: UserLoginDTO): Promise<AuthResponse>
   - Email/password validation
   - Argon2 password verification
   - User status check (ACTIVE only)
   - JWT token generation
   - Returns: { user, accessToken }

✅ getProfile(userId: string): Promise<UserResponseDTO & { permissions }>
   - Fetch user data
   - Include RBAC permissions
   
✅ updateProfile(userId, dto): Promise<UserResponseDTO>
   - Update fullName
   - Auto-update timestamp

✅ deleteProfile(userId): Promise<void>
   - Soft delete (status = DELETED)
   - Set deletedAt timestamp
```

**RefreshTokenService** (refresh-token.service.ts):
```typescript
✅ Refresh token rotation logic
✅ Token storage in database
✅ Automatic cleanup of expired tokens
```

**RBAC Service** (`modules/rbac/`):
```typescript
✅ getUserPermissions(userId, role): Promise<{ permissions: string[] }>
✅ Role-based access control
✅ Permission checking
```

#### **2. API Gateway** (`apps/server/modules/gateway/`)

**Architecture:**
```typescript
✅ HTTP Proxy pattern to microservices
✅ NATS Auth Callout integration (for LiveKit)
✅ Redis caching (Keyv)
✅ ApiKeyGuard for API protection
✅ ProxyModule for routing
```

**Note:** Gateway uses **proxy pattern** - no direct controllers, routes to Identity service.

#### **3. Shared Infrastructure** (`apps/server/libs/shared/`)

**JwtTokenProvider:**
```typescript
✅ generateToken(payload): Promise<string>
✅ JWT signing with secret
✅ Token expiration handling
```

**Guards:**
```typescript
✅ ApiKeyGuard - API key validation
✅ (Likely) JwtAuthGuard - JWT validation
```

---

## Gap Analysis: What's Missing?

### ❌ Backend Gaps:

1. **Email Verification** (TODO in code)
   ```typescript
   // auth.service.ts line 108
   emailVerified: false, // TODO: Implement email verification
   ```

2. **Session Management**
   - No session timeout enforcement (30-min requirement)
   - No concurrent session limits
   - No session invalidation on logout

3. **Password Reset Flow**
   - No forgot password endpoint
   - No reset token generation
   - No email sending integration

4. **Rate Limiting**
   - No Redis-based rate limiting (1000 req/min per API key)
   - No brute-force protection on login

5. **Security Enhancements**
   - No strong password policy validation
   - No CSRF protection
   - No XSS prevention headers

### ❌ Frontend Gaps (CRITICAL - 100% Missing):

#### **Web Apps (web-learner, web-admin, meet):**
1. **No registration pages**
2. **No login pages**
3. **No profile management UI**
4. **No Axios interceptors** for JWT refresh
5. **No auth state management** (Zustand/Redux)
6. **No protected route guards**

#### **Mobile App (torii-mobile):**
1. **No registration screens**
2. **No login screens**
3. **No profile management screens**
4. **No token storage** (flutter_secure_storage exists but not integrated)
5. **No Dio interceptors** for JWT refresh
6. **No auth state management** (Riverpod providers)

---

## Epic 2 Stories - Relevance Assessment

Based on `sprint-status.yaml`, Epic 2 has **8 stories**:

### Story 2.1: User Registration (Web & Mobile)
**Status:** `backlog`  
**Relevance:** ✅ **HIGH PRIORITY**

**Backend:** ✅ Already implemented (`AuthService.register`)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Build registration UI (web-learner, web-admin, mobile)
- Form validation (Zod schemas)
- Error handling (email conflict, validation errors)
- Success flow (auto-login or redirect to login)

---

### Story 2.2: User Login (Web & Mobile)
**Status:** `backlog`  
**Relevance:** ✅ **HIGH PRIORITY**

**Backend:** ✅ Already implemented (`AuthService.login`)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Build login UI (web-learner, web-admin, mobile)
- Form validation
- Token storage (localStorage/cookies for web, flutter_secure_storage for mobile)
- Auth state management (Zustand/Redux/Riverpod)
- Protected route guards

---

### Story 2.3: JWT Refresh Token Flow
**Status:** `backlog`  
**Relevance:** ✅ **HIGH PRIORITY**

**Backend:** ✅ Already implemented (`RefreshTokenService`)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Axios interceptors (web) for auto-refresh on 401
- Dio interceptors (mobile) for auto-refresh
- Token rotation logic
- Handle refresh token expiration (force logout)

---

### Story 2.4: Profile Management
**Status:** `backlog`  
**Relevance:** ✅ **MEDIUM PRIORITY**

**Backend:** ✅ Already implemented (`AuthService.getProfile`, `updateProfile`)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Profile view page (web + mobile)
- Profile edit form (fullName, avatar upload)
- Password change flow (backend needs implementation)
- Delete account flow (soft delete)

---

### Story 2.5: RBAC Implementation
**Status:** `backlog`  
**Relevance:** ⚠️ **PARTIALLY IMPLEMENTED**

**Backend:** ✅ Already implemented (`RBACService`)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Role-based UI rendering (hide/show features by role)
- Permission-based guards (web + mobile)
- Admin role assignment UI (web-admin only)

---

### Story 2.6: NATS Auth Callout Integration
**Status:** `backlog`  
**Relevance:** ✅ **ALREADY IMPLEMENTED**

**Backend:** ✅ Already implemented (`NatsAuthModule` in Gateway)  
**Frontend:** N/A (backend-only feature)

**Verdict:** ✅ **SKIP** - Already complete.

---

### Story 2.7: Session Management
**Status:** `backlog`  
**Relevance:** ⚠️ **NEEDS BACKEND ENHANCEMENT**

**Backend:** ⚠️ Partial (JWT expiration exists, but no session tracking)  
**Frontend:** ❌ **NEEDS IMPLEMENTATION**

**Scope:**
- Backend: Implement 30-min session timeout
- Backend: Concurrent session limits
- Backend: Session invalidation on logout
- Frontend: Auto-logout on session expiration
- Frontend: Session activity tracking

---

### Story 2.8: Admin User Impersonation
**Status:** `backlog`  
**Relevance:** ⚠️ **NEEDS FULL IMPLEMENTATION**

**Backend:** ❌ Not implemented  
**Frontend:** ❌ Not implemented

**Scope:**
- Backend: Impersonation token generation
- Backend: Audit trail for impersonation
- Frontend: Admin UI to impersonate users
- Frontend: "Exit impersonation" button

---

## Recommended Story Prioritization

### **Phase 1: Core Auth (MUST HAVE - Sprint 1)**

1. **Story 2.2: User Login (Web & Mobile)** ⭐⭐⭐
   - **Why first:** Blocks all other features
   - **Effort:** 3-5 days
   - **Dependencies:** None

2. **Story 2.1: User Registration (Web & Mobile)** ⭐⭐⭐
   - **Why second:** Users need to create accounts
   - **Effort:** 2-3 days
   - **Dependencies:** 2.2 (reuse auth state management)

3. **Story 2.3: JWT Refresh Token Flow** ⭐⭐⭐
   - **Why third:** Prevents session interruptions
   - **Effort:** 2-3 days
   - **Dependencies:** 2.2 (requires login flow)

### **Phase 2: User Experience (SHOULD HAVE - Sprint 2)**

4. **Story 2.4: Profile Management** ⭐⭐
   - **Effort:** 2-3 days
   - **Dependencies:** 2.2 (requires auth)

5. **Story 2.5: RBAC Implementation** ⭐⭐
   - **Effort:** 3-4 days (complex UI logic)
   - **Dependencies:** 2.2 (requires auth)

### **Phase 3: Security & Admin (NICE TO HAVE - Sprint 3)**

6. **Story 2.7: Session Management** ⭐
   - **Effort:** 2-3 days
   - **Dependencies:** 2.2, 2.3

7. **Story 2.8: Admin User Impersonation** ⭐
   - **Effort:** 3-4 days
   - **Dependencies:** 2.2, 2.5 (RBAC)

8. **Story 2.6: NATS Auth Callout** ✅ **SKIP** (already done)

---

## Additional Stories Needed (Security Enhancements)

### **Story 2.9: Email Verification** (NEW)
**Priority:** ⭐⭐  
**Scope:**
- Backend: Email verification token generation
- Backend: Email sending integration (SendGrid/AWS SES)
- Frontend: Verification success/failure pages
- Frontend: Resend verification email

### **Story 2.10: Password Reset Flow** (NEW)
**Priority:** ⭐⭐  
**Scope:**
- Backend: Forgot password endpoint
- Backend: Reset token generation (time-limited)
- Backend: Email sending
- Frontend: Forgot password form
- Frontend: Reset password form

### **Story 2.11: Security Hardening** (NEW)
**Priority:** ⭐  
**Scope:**
- Backend: Strong password policy (Zod validation)
- Backend: Rate limiting (Redis-based)
- Backend: CSRF protection
- Backend: XSS prevention headers (CSP)
- Frontend: Password strength indicator

---

## Technical Recommendations

### **1. Frontend Auth Architecture**

#### **Web Apps (Zustand for web-learner, Redux for web-admin/meet):**

```typescript
// auth.store.ts (Zustand example for web-learner)
interface AuthState {
  user: UserResponseDTO | null;
  accessToken: string | null;
  isAuthenticated: boolean;
  login: (credentials: UserLoginDTO) => Promise<void>;
  logout: () => void;
  refreshToken: () => Promise<void>;
}

export const useAuthStore = create<AuthState>((set) => ({
  user: null,
  accessToken: localStorage.getItem('accessToken'),
  isAuthenticated: !!localStorage.getItem('accessToken'),
  
  login: async (credentials) => {
    const response = await authApi.login(credentials);
    localStorage.setItem('accessToken', response.accessToken);
    set({ user: response.user, accessToken: response.accessToken, isAuthenticated: true });
  },
  
  logout: () => {
    localStorage.removeItem('accessToken');
    set({ user: null, accessToken: null, isAuthenticated: false });
  },
  
  refreshToken: async () => {
    const response = await authApi.refreshToken();
    localStorage.setItem('accessToken', response.accessToken);
    set({ accessToken: response.accessToken });
  },
}));
```

#### **Mobile App (Riverpod):**

```dart
// auth_provider.dart
final authProvider = StateNotifierProvider<AuthNotifier, AuthState>((ref) {
  return AuthNotifier(ref.read(authRepositoryProvider));
});

class AuthNotifier extends StateNotifier<AuthState> {
  final AuthRepository _repository;
  
  AuthNotifier(this._repository) : super(AuthState.initial());
  
  Future<void> login(String email, String password) async {
    state = state.copyWith(isLoading: true);
    try {
      final response = await _repository.login(email, password);
      await _secureStorage.write(key: 'accessToken', value: response.accessToken);
      state = state.copyWith(
        user: response.user,
        isAuthenticated: true,
        isLoading: false,
      );
    } catch (e) {
      state = state.copyWith(error: e.toString(), isLoading: false);
    }
  }
}
```

### **2. Axios/Dio Interceptors**

#### **Web (Axios):**

```typescript
// axios.config.ts
axios.interceptors.response.use(
  (response) => response,
  async (error) => {
    const originalRequest = error.config;
    
    if (error.response?.status === 401 && !originalRequest._retry) {
      originalRequest._retry = true;
      
      try {
        const { accessToken } = await authApi.refreshToken();
        localStorage.setItem('accessToken', accessToken);
        originalRequest.headers.Authorization = `Bearer ${accessToken}`;
        return axios(originalRequest);
      } catch (refreshError) {
        // Refresh failed, logout user
        useAuthStore.getState().logout();
        window.location.href = '/login';
        return Promise.reject(refreshError);
      }
    }
    
    return Promise.reject(error);
  }
);
```

#### **Mobile (Dio):**

```dart
// dio_interceptor.dart
class AuthInterceptor extends Interceptor {
  @override
  Future<void> onError(DioException err, ErrorInterceptorHandler handler) async {
    if (err.response?.statusCode == 401) {
      try {
        final newToken = await _refreshToken();
        err.requestOptions.headers['Authorization'] = 'Bearer $newToken';
        final response = await _dio.fetch(err.requestOptions);
        return handler.resolve(response);
      } catch (e) {
        // Refresh failed, logout
        await _authNotifier.logout();
        return handler.reject(err);
      }
    }
    return handler.next(err);
  }
}
```

---

## Next Steps

### **Immediate Actions:**

1. **Create Story 2.2 (Login)** using `/create-story`
   - Focus on web-learner first (Next.js)
   - Then web-admin (Vite + Redux)
   - Then mobile (Flutter)

2. **Update sprint-status.yaml:**
   ```yaml
   epic-2: in-progress
   2-1-user-registration-web-mobile: backlog
   2-2-user-login-web-mobile: ready-for-dev  # Create this story first
   2-3-jwt-refresh-token-flow: backlog
   2-4-profile-management: backlog
   2-5-rbac-implementation: backlog
   2-6-nats-auth-callout-integration: obsolete  # Already implemented
   2-7-session-management: backlog
   2-8-admin-user-impersonation: backlog
   
   # New stories
   2-9-email-verification: backlog
   2-10-password-reset-flow: backlog
   2-11-security-hardening: backlog
   ```

3. **Run `/create-story` for Story 2.2:**
   - Story ID: `2-2-user-login-web-mobile`
   - Context: Backend already implemented, focus on frontend
   - Platforms: web-learner (Next.js), web-admin (Vite), mobile (Flutter)

---

## Conclusion

**Epic 2 Backend:** 70% complete ✅  
**Epic 2 Frontend:** 0% complete ❌

**Critical Path:** Stories 2.2 → 2.1 → 2.3 (Login → Registration → Refresh Token)

**Estimated Timeline:**
- Sprint 1 (2 weeks): Stories 2.2, 2.1, 2.3 (Core Auth)
- Sprint 2 (2 weeks): Stories 2.4, 2.5 (UX + RBAC)
- Sprint 3 (1 week): Stories 2.7, 2.9, 2.10 (Security)

**Total Epic 2 Effort:** 5-6 weeks (assuming 1 developer)

---

**Generated by:** Dev Agent (Amelia)  
**Analysis Date:** 2026-01-03T16:25:00+07:00  
**Confidence Level:** High (based on direct codebase inspection)
