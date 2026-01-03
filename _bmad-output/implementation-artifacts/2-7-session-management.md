# Story 2.7: Session Management

Status: ready-for-dev

## Story

As a system, I want session management, so that we prevent unauthorized access and maintain security.

## Acceptance Criteria

1. **Active Sessions Tracking**
   - Track all active sessions per user account (no limit)
   - "Active Sessions" page showing all logged-in devices with details:
     - Device type (Web/Mobile)
     - Browser/App version
     - IP address (masked for privacy: 192.168.*.*)
     - Last activity timestamp
     - Location (city level)
   - "Force Logout All" option in user settings
   - "Terminate Session" button for individual sessions

2. **Token Blacklist in Redis**
   - Invalidated **refresh tokens AND access tokens** stored in Redis blacklist
   - Blacklist checked on **every authenticated API request** (via middleware)
   - Blacklisted tokens return 401 Unauthorized
   - TTL on blacklist entries:
     - Refresh token blacklist: 7 days (match refresh token expiry)
     - Access token blacklist: 1 hour (match access token expiry)

3. **Logout Invalidates Both Tokens**
   - Logout endpoint adds **both refresh token AND access token** to blacklist
   - Access token blacklisted immediately (prevents use of saved tokens)
   - Refresh token blacklisted (prevents token refresh)
   - Session deleted from Redis
   - Redirect to login page after successful logout

4. **Activity Tracking**
   - Track user activity via API requests (any authenticated endpoint)
   - Update "last activity" timestamp in Redis on each activity
   - Display last activity time in Active Sessions page

## Tasks / Subtasks

### Backend Tasks

- [ ] **Task 1: Redis Session Store Implementation** (AC: #1, #2, #3)
  - [ ] Create `SessionService` in Identity module
  - [ ] Implement Redis schema for session tracking:
    ```typescript
    // Key: session:{userId}:{sessionId}
    {
      userId: string,
      sessionId: string,
      deviceType: 'web' | 'mobile',
      browser: string,
      ipAddress: string,
      location: string,
      lastActivity: Date,
      createdAt: Date,
      refreshToken: string (hashed)
    }
    ```
  - [ ] Implement `createSession()` method
  - [ ] Implement `updateActivity()` method
  - [ ] Implement `getActiveSessions(userId)` method
  - [ ] Implement `terminateSession(sessionId)` method
  - [ ] Implement `terminateAllSessions(userId)` method
  - [ ] Set TTL on session keys (7 days to match refresh token expiry)

- [ ] **Task 2: Token Blacklist Implementation** (AC: #2, #3)
  - [ ] Create `TokenBlacklistService`
  - [ ] Implement Redis schema for blacklist:
    ```typescript
    // Key: blacklist:refresh:{refreshToken}
    {
      userId: string,
      tokenType: 'refresh',
      reason: 'logout' | 'force_logout_all' | 'security',
      blacklistedAt: Date
    }
    
    // Key: blacklist:access:{accessToken}
    {
      userId: string,
      tokenType: 'access',
      reason: 'logout' | 'force_logout_all' | 'security',
      blacklistedAt: Date
    }
    ```
  - [ ] Implement `addRefreshTokenToBlacklist(refreshToken, userId, reason)` method
  - [ ] Implement `addAccessTokenToBlacklist(accessToken, userId, reason)` method
  - [ ] Implement `isRefreshTokenBlacklisted(refreshToken)` method
  - [ ] Implement `isAccessTokenBlacklisted(accessToken)` method
  - [ ] Set TTL on blacklist keys:
    - Refresh token: 7 days
    - Access token: 1 hour
  - [ ] Update JWT refresh endpoint to check refresh token blacklist
  - [ ] Create `TokenBlacklistMiddleware` to check access token blacklist on every authenticated request

- [ ] **Task 3: Logout Endpoint Enhancement** (AC: #3)
  - [ ] Update `POST /auth/logout` endpoint:
    - Extract **access token** from Authorization header
    - Extract **refresh token** from httpOnly cookie (web) or request body (mobile)
    - Add **both tokens** to blacklist with reason: 'logout'
    - Delete session from Redis
    - Clear httpOnly cookie (web)
    - Return 200 OK with success message
  - [ ] Add error handling for missing/invalid tokens
  - [ ] Log logout events for audit trail

- [ ] **Task 4: Activity Tracking Middleware** (AC: #4)
  - [ ] Create `ActivityTrackingMiddleware` for all authenticated routes
  - [ ] Extract userId and sessionId from JWT access token
  - [ ] Update session's lastActivity timestamp in Redis (async, non-blocking)
  - [ ] Debounce updates (max 1 update per 60 seconds per session)
  - [ ] Handle Redis connection failures gracefully (log error, don't block request)

- [ ] **Task 5: Active Sessions API Endpoints** (AC: #1)
  - [ ] `GET /auth/sessions` - Get all active sessions for current user
    - Return array of sessions with masked IP addresses
    - Sort by lastActivity (most recent first)
  - [ ] `DELETE /auth/sessions/:sessionId` - Terminate specific session
    - Verify session belongs to current user
    - Extract refresh token and access token from session
    - Add both tokens to blacklist
    - Delete session from Redis
    - Return 200 OK
  - [ ] `DELETE /auth/sessions/all` - Force logout all sessions
    - Get all sessions for current user
    - For each session:
      - Extract refresh token and access token
      - Add both tokens to blacklist with reason: 'force_logout_all'
    - Delete all sessions from Redis
    - Return 200 OK with count of terminated sessions

### Frontend Tasks (Web - Next.js Learner, Vite Admin/Meet)

- [ ] **Task 6: Active Sessions Management Page** (AC: #1)
  - [ ] Create `ActiveSessionsPage` component (Settings → Security → Active Sessions)
  - [ ] Fetch sessions from `GET /auth/sessions`
  - [ ] Display session cards with:
    - Device icon (desktop/mobile)
    - Browser/App name and version
    - Masked IP address (e.g., "192.168.*.*")
    - Location (city, country)
    - Last activity (relative time: "5 minutes ago")
    - "Current Session" badge for active session
    - "Terminate" button for other sessions
  - [ ] Implement "Force Logout All" button:
    - Confirmation dialog: "This will log you out from all devices. Continue?"
    - Call `DELETE /auth/sessions/all`
    - Redirect to login page after success
  - [ ] Handle session termination:
    - Call `DELETE /auth/sessions/:sessionId`
    - Remove session from UI
    - Show success toast: "Session terminated"

- [ ] **Task 7: Logout Flow Enhancement** (AC: #3)
  - [ ] Update logout function to call `POST /auth/logout`
  - [ ] Clear local storage/session storage
  - [ ] Clear Zustand/Redux state
  - [ ] Clear TanStack Query cache
  - [ ] Redirect to login page
  - [ ] Show success toast: "Logged out successfully"
  - [ ] Handle logout errors gracefully (still redirect to login)

### Frontend Tasks (Mobile - Flutter)

- [ ] **Task 8: Mobile Activity Tracking** (AC: #4)
  - [ ] Implement `ActivityTracker` service using Riverpod
  - [ ] Track app lifecycle events:
    - App resumed (foreground)
    - User interaction (tap, scroll)
  - [ ] Send activity update to backend on each authenticated API call
  - [ ] Pause tracking when app is in background

- [ ] **Task 9: Mobile Active Sessions Screen** (AC: #1)
  - [ ] Create `ActiveSessionsScreen` in Settings
  - [ ] Fetch and display sessions (same as web)
  - [ ] Implement "Force Logout All" with confirmation dialog
  - [ ] Handle session termination

### Testing Tasks

- [ ] **Task 10: Backend Unit Tests**
  - [ ] Test `SessionService` methods
  - [ ] Test `TokenBlacklistService` methods (both access and refresh tokens)
  - [ ] Test `TokenBlacklistMiddleware` (access token check on every request)
  - [ ] Test activity tracking middleware

- [ ] **Task 11: Backend Integration Tests**
  - [ ] Test login creates session in Redis
  - [ ] Test logout adds **both tokens** to blacklist
  - [ ] Test refresh token fails when blacklisted
  - [ ] Test **access token fails when blacklisted** (401 on API requests)
  - [ ] Test activity updates session timestamp
  - [ ] Test force logout all blacklists all tokens

- [ ] **Task 12: Frontend E2E Tests**
  - [ ] Test active sessions page displays correctly
  - [ ] Test "Force Logout All" terminates all sessions
  - [ ] Test logout clears auth state and redirects
  - [ ] Test session termination from active sessions page
  - [ ] Test blacklisted access token returns 401 on API call

## Dev Notes

### Architecture Patterns

**Session Storage Strategy:**
- Use Redis for session tracking (fast, TTL support, distributed)
- Session key pattern: `session:{userId}:{sessionId}`
- Blacklist key patterns:
  - `blacklist:refresh:{refreshToken}`
  - `blacklist:access:{accessToken}`
- TTL on session keys: 7 days (match refresh token expiry)
- TTL on blacklist keys:
  - Refresh token: 7 days
  - Access token: 1 hour

**Activity Tracking:**
- Middleware-based approach for backend (non-blocking)
- Update lastActivity timestamp on each authenticated API request
- Debounced updates (max 1 update per 60 seconds per session)

**Token Blacklist (Dual-Token Strategy):**
- Check **access token blacklist** on every authenticated API request (middleware)
- Check **refresh token blacklist** on token refresh attempts
- Add both tokens to blacklist on logout or force logout all
- Use hashed tokens as keys for privacy
- Different TTLs for different token types

**Session Termination:**
- Individual session termination: blacklist both tokens, delete session
- Force logout all: iterate all sessions, blacklist all tokens, delete all sessions
- NATS event for session termination (notify other services)

### Security Considerations

1. **Token Security:**
   - Store refresh tokens hashed in Redis (SHA-256)
   - Store access tokens hashed in blacklist (SHA-256)
   - Never log tokens (access or refresh)
   - Use httpOnly cookies for web (XSS protection)
   - Use Flutter Secure Storage for mobile

2. **Access Token Blacklist (Critical Security Feature):**
   - **Problem:** Access tokens are valid for 1 hour. If user logs out, attacker with saved access token can still use it.
   - **Solution:** Blacklist access token immediately on logout
   - **Implementation:** Middleware checks blacklist on **every authenticated request**
   - **Performance:** Redis lookup is fast (~1ms), acceptable overhead for security
   - **Trade-off:** Slight performance impact vs. immediate logout security

3. **IP Address Privacy:**
   - Mask IP addresses in UI (show only first 2 octets)
   - Store full IP in backend for security audit
   - Comply with GDPR (IP is PII)

4. **Session Hijacking Prevention:**
   - Bind session to device fingerprint (optional enhancement)
   - Detect suspicious activity (IP change, location change)
   - Force re-authentication on suspicious activity

5. **Audit Trail:**
   - Log all session events (create, terminate, logout)
   - Include userId, sessionId, IP, timestamp, reason
   - Store logs for compliance (30 days minimum)

### Performance Considerations

1. **Redis Performance:**
   - Use Redis pipelining for batch operations
   - Set appropriate TTLs to auto-cleanup expired data
   - Monitor Redis memory usage (estimate: 1KB per session)

2. **Activity Tracking:**
   - Debounce updates (max 1 update per 60s per session)
   - Make activity updates async (don't block API requests)
   - Handle Redis failures gracefully (log error, continue)

### Testing Standards

**Unit Test Coverage:**
- SessionService: 100% (critical security component)
- TokenBlacklistService: 100%
- ActivityTrackingMiddleware: 90%

**Integration Tests:**
- Test all session lifecycle events
- Test concurrent session limits
- Test token blacklist enforcement
- Test activity tracking

**E2E Tests:**
- Test complete user flows (login → activity → logout)
- Test multi-device scenarios
- Test session management UI

### Project Structure Notes

**Backend (NestJS):**
```
apps/server/modules/identity/
├── src/
│   ├── modules/
│   │   ├── session/
│   │   │   ├── session.service.ts          # Session CRUD operations
│   │   │   ├── session.module.ts
│   │   │   ├── session.controller.ts       # Active sessions API
│   │   │   ├── token-blacklist.service.ts  # Blacklist management
│   │   │   └── activity-tracking.middleware.ts
│   │   ├── auth/
│   │   │   ├── auth.controller.ts          # Update login/logout
│   │   │   └── jwt-refresh.guard.ts        # Add blacklist check
```

**Frontend Web (Next.js/Vite):**
```
src/
├── components/
│   ├── session/
│   │   └── ActiveSessionCard.tsx
├── pages/ (or app/)
│   ├── settings/
│   │   └── active-sessions.tsx
├── hooks/
│   └── useActivityTracking.ts
├── services/
│   └── session.service.ts                  # API calls
```

**Frontend Mobile (Flutter):**
```
lib/
├── features/
│   ├── auth/
│   │   ├── providers/
│   │   │   ├── session_provider.dart
│   │   │   └── activity_tracker_provider.dart
│   │   └── screens/
│   │       └── active_sessions_screen.dart
```

### References

- [Source: _bmad-output/planning-artifacts/architecture.md#Authentication & Security]
- [Source: _bmad-output/planning-artifacts/enhanced-requirements.md#US.SEC.02]
- [Source: _bmad-output/planning-artifacts/epics-stories-summary.md#Story 2.7]
- [Source: _bmad-output/planning-artifacts/epics.md#Epic 2]

### Dependencies

**NPM Packages (Backend):**
- `ioredis` - Redis client (already in use)
- `crypto` - For hashing refresh tokens (Node.js built-in)

**NPM Packages (Frontend Web):**
- `date-fns` - For relative time formatting

**Flutter Packages (Mobile):**
- `flutter_secure_storage` - For secure token storage (already in use)
- `connectivity_plus` - For network status detection

### Environment Variables

```env
# Session Management
SESSION_TTL_DAYS=7
TOKEN_BLACKLIST_TTL_DAYS=7
ACCESS_TOKEN_BLACKLIST_TTL_HOURS=1
ACTIVITY_DEBOUNCE_SECONDS=60
```

## Dev Agent Record

### Agent Model Used

_To be filled by dev agent_

### Debug Log References

_To be filled by dev agent_

### Completion Notes List

_To be filled by dev agent_

### File List

_To be filled by dev agent_
