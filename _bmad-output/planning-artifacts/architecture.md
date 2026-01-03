---
stepsCompleted: [1, 2, 3, 4]
inputDocuments:
  - "_bmad-output/planning-artifacts/prd.md"
  - "_bmad-output/planning-artifacts/ux-design-specification.md"
  - "_bmad-output/planning-artifacts/enhanced-requirements.md"
  - "bmad/docs/project-overview.md"
  - "bmad/docs/integration-architecture.md"
  - "bmad/docs/data-models-server.md"
  - "bmad/docs/api-contracts-server.md"
workflowType: 'architecture'
project_name: 'torii-nihongo'
user_name: 'Tienh'
date: '2026-01-03'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

**Project:** torii-nihongo  
**Type:** Brownfield Capstone (10-week graduation project)  
**Domain:** EdTech - Japanese Language Learning (JLPT Certification)  
**Date:** 2026-01-03

### Requirements Overview

**Functional Requirements:**

The system serves **4 distinct user roles** with comprehensive feature sets:

1. **Learner Experience** (Web + Mobile):
   - Course discovery, enrollment, and VNPay payment integration
   - Hybrid learning: VOD courses + scheduled live WebRTC classes
   - SRS flashcards with cross-platform sync (web ↔ mobile)
   - JLPT practice exams with auto-grading
   - AI Sensei for 24/7 Q&A, grammar correction, flashcard generation
   - Progress tracking with 5-pillar JLPT analytics
   - Offline learning capability (4-hour metro commute use case)

2. **Lecturer Operations** (Web):
   - Live class management (start/end, attendance auto-tracking)
   - Real-time engagement heatmap showing student participation
   - AI-assisted grading (draft grading + lecturer review workflow)
   - Whiteboard control, screen sharing, resource management
   - Audio feedback recording for assignments
   - Mentorship system for new lecturers

3. **Staff Operations** (Web - 3 specialized roles):
   - **Academic Staff**: Question bank management, exam generation, content versioning
   - **Operations Staff**: Command center dashboard for 50+ concurrent classes, emergency re-assignment
   - **Admissions/Marketing**: Coupon management, CMS, engagement tracking
   - **Financial Staff**: VNPay reconciliation, refund workflows, revenue reporting

4. **Admin Governance** (Web):
   - Strategic KPI dashboard (LTV, CAC, retention, revenue trends)
   - Financial reconciliation (VNPay ↔ internal DB)
   - Audit trails for compliance (GDPR, educational standards)
   - RBAC management and user impersonation for support

**Non-Functional Requirements:**

**Performance Targets:**
- API response time: <200ms (p95)
- WebRTC latency: <200ms
- Whiteboard sync: <100ms
- AI feedback: <3 seconds
- Page load: <2s (web), <1.5s (mobile)
- Database queries: <100ms (p95)
- Video streaming: <3s initial load

**Scalability Requirements:**
- 50+ concurrent live classes
- 10,000 users, 1,000 courses
- 1TB video storage capacity
- 1000 requests/minute per API key

**Reliability & Availability:**
- 99.9% uptime SLA
- Atomic transactions for payments/enrollments (no race conditions)
- Graceful degradation (auto video quality reduction on poor network)
- Disaster recovery (backup Zoom link for WebRTC outages)
- Auto-save (every 30 seconds for assignments/progress)

**Security & Compliance:**
- JWT authentication with 1-hour access tokens, 7-day refresh tokens
- RBAC with granular permissions
- NATS Auth Callout for dynamic pub/sub authorization
- GDPR compliance (data export, right to erasure, 30-day grace period)
- PCI DSS compliance (VNPay tokenization, no card storage)
- Audit trails for all sensitive operations

**Offline Capability (Mobile):**
- Download entire lesson modules for offline viewing
- Offline flashcard practice with SRS algorithm
- Background sync when WiFi reconnects
- Conflict resolution for offline changes

### Scale & Complexity

**Project Complexity Level:** **HIGH**

**Complexity Indicators:**
- ✅ Real-time features (WebRTC, whiteboard, chat, AI feedback)
- ✅ Multi-tenancy (4 user roles with distinct workflows)
- ✅ Regulatory compliance (GDPR, PCI DSS, educational standards)
- ✅ High integration complexity (VNPay, LiveKit, FastMCP, NATS, MinIO)
- ✅ Complex user interactions (live collaboration, AI augmentation)
- ✅ Significant data complexity (courses, users, progress, analytics, media)

**Primary Technical Domain:** Full-Stack EdTech Platform
- **Frontend:** Web (Next.js + React/Vite) + Mobile (Flutter)
- **Backend:** NestJS microservices with NATS event-driven coordination
- **Real-time:** WebRTC (LiveKit) + NATS JetStream
- **AI:** Multi-agent system (FastMCP protocol)
- **Data:** PostgreSQL + Redis + MinIO/S3

**Estimated Architectural Components:** 15-20 major components

**Backend Microservices:**
1. API Gateway (NATS Auth Provider + HTTP Proxy)
2. Identity Service (Auth, Users, RBAC)
3. LMS Service (Courses, Lessons, Progress)
4. Meet Service (WebRTC rooms, whiteboard, attendance)
5. Cortex Service (AI Multi-Agent: Sensei, Assessment, Analytics)
6. Flashcard Service (SRS algorithm, deck marketplace)
7. Assessment Service (Question bank, exams, grading)
8. Gamification Service (XP, badges, streaks, leaderboards)
9. Community Service (Blogs, comments, forums)
10. Storage Service (MinIO integration, file management)
11. Notification Service (Push, email, SMS)
12. Payment Service (VNPay integration, refunds)

**Frontend Applications:**
13. Web Learner (Next.js - course discovery, enrollment, live classes)
14. Web Admin/Staff (React/Vite - dashboards, management)
15. Web Meet (React/Vite - live class interface)
16. Mobile App (Flutter - offline-first learner experience)

**Infrastructure Components:**
17. NATS Server (Event backbone + Auth Callout)
18. LiveKit Server (WebRTC media)
19. PostgreSQL (Primary database)
20. Redis (Caching, session management)
21. MinIO/S3 (Video storage)

### Technical Constraints & Dependencies

**Existing Infrastructure (Brownfield):**
- NATS-centric event-driven architecture already in place
- Microservices pattern established (Identity, LMS, Meet, etc.)
- Protobuf for efficient serialization (backend ↔ mobile)
- PostgreSQL + Prisma ORM for data persistence
- Docker Compose for local development

**Third-Party Dependencies:**
- **VNPay**: Payment gateway (Vietnam market)
- **LiveKit**: WebRTC infrastructure for live classes
- **FastMCP**: Multi-agent AI protocol (Cortex integration)
- **Firebase**: Authentication (sync with internal DB)
- **MinIO/S3**: Object storage for videos and files

**Technology Constraints:**
- **Timeline**: 10-week capstone project (graduation requirement)
- **Team Skill Level**: Intermediate developers
- **Platform Requirements**: Cross-platform (Web + Mobile mandatory)
- **Language**: Vietnamese UI for target market (Vietnamese learners)

**Performance Constraints:**
- WebRTC must support 15-20 participants per class with <200ms latency
- Mobile app must work offline for 4+ hours (metro commute)
- AI feedback must respond in <3 seconds (real-time teaching assistant)
- System must handle 50+ concurrent live classes without degradation

### Cross-Cutting Concerns Identified

**1. Authentication & Authorization:**
- JWT-based auth for HTTP APIs
- NATS Auth Callout for dynamic pub/sub permissions
- RBAC with role-specific UI and API access
- Session management (30-min timeout, concurrent session limits)
- Impersonation for admin support

**2. Real-Time Communication:**
- NATS JetStream for event-driven workflows (workqueues, pub/sub)
- WebRTC for live video/audio (LiveKit integration)
- WebSocket for real-time UI updates (chat, whiteboard, presence)
- Optimistic UI updates with server reconciliation

**3. AI Integration & Orchestration:**
- FastMCP protocol for multi-agent coordination
- Three specialized agents: Sensei (Q&A), Assessment (grading), Analytics (recommendations)
- Real-time inference (<3s response time requirement)
- AI transparency (show confidence levels, allow overrides, explain reasoning)
- Lecturer-in-the-loop for final grading decisions

**4. Data Synchronization:**
- Cross-platform sync (web ↔ mobile) for progress, flashcards, quiz scores
- Offline-first mobile architecture (Drift SQLite + background sync)
- Conflict resolution (last-write-wins for progress, server-authoritative for payments)
- Incremental sync to minimize mobile data usage

**5. Payment Processing:**
- VNPay integration with webhook callbacks
- Atomic enrollment (distributed lock via NATS for 15-min window)
- Refund workflows (atomic: VNPay refund + DB update + email)
- Financial reconciliation (VNPay balance ↔ internal DB)
- Gifting system (generate codes, receiver chooses schedule)

**6. Video & Media Management:**
- MinIO/S3 for video storage (1TB capacity)
- Transcoding pipeline (NATS JetStream workqueue)
- Adaptive bitrate streaming
- Live class recording with auto-transcoding
- Video progress tracking (resume from last position)

**7. Monitoring & Observability:**
- Real-time health metrics for 50+ concurrent classes
- Connection quality indicators (green/yellow/red)
- Operations command center dashboard
- Proactive alerts (class degrading, lecturer no-show)
- Audit trails for compliance and debugging

**8. Error Handling & Resilience:**
- Graceful degradation (reduce video quality on poor network)
- Disaster recovery (backup Zoom link for WebRTC failures)
- Clear error messages with recovery paths
- Auto-save to prevent data loss
- Retry mechanisms with exponential backoff

**9. Accessibility & Internationalization:**
- Keyboard navigation for all interactive elements
- Screen reader support (ARIA labels, semantic HTML)
- Video captions (auto-generated via Whisper API)
- Vietnamese UI (primary), English (future)
- Dark mode support

**10. Testing & Quality Assurance:**
- Unit test coverage >60% (graduation requirement)
- Integration tests for critical flows (payment, enrollment, live class join)
- E2E tests for user journeys
- Load testing for 50+ concurrent classes
- AI grading accuracy validation

## Starter Template Evaluation

### Primary Technology Domains

Based on project requirements analysis, this is a **multi-platform full-stack EdTech application** requiring:

1. **Backend Microservices** (Existing - Brownfield)
2. **Web Frontend Applications** (New - Greenfield)
3. **Mobile Application** (New - Greenfield)

### Existing Backend Stack (Brownfield - Already Established)

**Technology Decisions Already Made:**

**Language & Runtime:**
- TypeScript with NestJS framework
- Node.js runtime
- Microservices architecture pattern

**Event-Driven Backbone:**
- NATS Core for pub/sub and request/reply
- NATS JetStream for workqueues and event streaming
- NATS Auth Callout for dynamic authorization
- Protobuf for efficient serialization

**Data Layer:**
- PostgreSQL as primary database
- Prisma ORM for type-safe database access
- Redis for caching and session management
- MinIO/S3 for object storage (videos, files)

**Real-Time & AI:**
- LiveKit for WebRTC infrastructure
- FastMCP protocol for multi-agent AI orchestration

**Development Environment:**
- Docker Compose for local development
- Established microservice structure (Identity, LMS, Meet, Cortex, etc.)

**Rationale:** These decisions are already implemented and working. The architecture must build upon this foundation rather than replace it.

---

### Frontend Web Applications (Greenfield - New Development)

#### Selected Starter: Next.js 15 + shadcn/ui (Learner App)

**Initialization Command:**

```bash
# Create Next.js 15 project with recommended options
npx create-next-app@latest torii-web-learner --typescript --tailwind --eslint --app --src-dir --turbopack --import-alias "@/*"

# Navigate to project
cd torii-web-learner

# Initialize shadcn/ui
npx shadcn@latest init

# Configuration options during init:
# - TypeScript: Yes
# - Style: Default (or New York based on preference)
# - Base color: Slate
# - Global CSS: src/app/globals.css
# - CSS variables: Yes
# - Tailwind config: tailwind.config.ts
# - Components alias: @/components
# - Utils alias: @/lib/utils

# Add initial components
npx shadcn@latest add button card input dialog table tabs
```

**Architectural Decisions Provided by Next.js 15 + shadcn/ui:**

**Language & Runtime:**
- TypeScript with strict mode enabled
- React 19 (latest stable)
- Next.js 15 with App Router (server components by default)
- Node.js runtime for server-side rendering

**Styling Solution:**
- Tailwind CSS 4 for utility-first styling
- shadcn/ui components (copy-paste, not npm dependency)
- Built on Radix UI primitives for accessibility
- CSS variables for theming (supports dark mode)
- PostCSS for CSS processing

**Build Tooling:**
- Turbopack (stable in Next.js 15) for fast development builds
- Webpack for production builds with automatic optimization
- Image optimization built-in (next/image)
- Font optimization (next/font)
- Automatic code splitting and lazy loading

**Routing & Navigation:**
- App Router with file-system based routing
- Server Components by default (opt-in to Client Components)
- Nested layouts and loading states
- Parallel routes and intercepting routes support

**Development Experience:**
- Hot Module Replacement (HMR) with Turbopack
- TypeScript IntelliSense and autocomplete
- ESLint with Next.js recommended rules
- Built-in debugging support
- Fast Refresh for instant feedback

**Code Organization:**
- `src/app/` - App Router pages and layouts
- `src/components/` - Reusable React components
- `src/lib/` - Utility functions and helpers
- `public/` - Static assets
- Clear separation of server and client components

**Rationale for Selection:**
- **Performance**: Turbopack provides 700x faster builds than Webpack for development
- **SEO-Friendly**: Server-side rendering for course catalog and discovery
- **Type Safety**: Full TypeScript integration with Next.js and shadcn/ui
- **Design System**: shadcn/ui provides production-ready components with full customization
- **Accessibility**: Radix UI primitives ensure WCAG 2.1 compliance
- **Developer Experience**: Fast refresh, excellent TypeScript support, modern tooling
- **Scalability**: App Router supports complex routing patterns needed for multi-role UI

---

#### Selected Starter: Vite 6 + React + TypeScript + shadcn/ui (Admin/Staff/Meet Apps)

**Initialization Command:**

```bash
# Create Vite React TypeScript project
npm create vite@latest torii-web-admin -- --template react-ts

# Navigate to project
cd torii-web-admin

# Install Tailwind CSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Initialize shadcn/ui
npx shadcn@latest init

# Configuration options during init:
# - TypeScript: Yes
# - Style: Default
# - Base color: Slate
# - Global CSS: src/index.css
# - CSS variables: Yes
# - Tailwind config: tailwind.config.ts
# - Components alias: @/components
# - Utils alias: @/lib/utils

# Add initial components for dashboards
npx shadcn@latest add button card input dialog table dropdown-menu tabs badge
```

**Architectural Decisions Provided by Vite + React + shadcn/ui:**

**Language & Runtime:**
- TypeScript with strict mode
- React 19 (latest stable)
- Vite 6 for lightning-fast development
- SWC for ultra-fast TypeScript compilation

**Styling Solution:**
- Tailwind CSS 4 for utility-first styling
- shadcn/ui components (full ownership and customization)
- Radix UI primitives for complex interactions (dropdowns, modals, tooltips)
- CSS variables for theming

**Build Tooling:**
- Vite 6 with esbuild for development (instant HMR)
- Rollup for production builds with tree-shaking
- Automatic code splitting
- Asset optimization (images, fonts)

**Routing (To Be Added):**
- React Router v6 for client-side routing
- Nested routes for dashboard layouts
- Protected routes for role-based access

**State Management (To Be Added):**
- React Context for global state (user, theme)
- TanStack Query (React Query) for server state management
- Zustand or Jotai for complex client state (if needed)

**Development Experience:**
- Instant HMR (<50ms updates)
- TypeScript IntelliSense
- ESLint + Prettier for code quality
- Vite DevTools for debugging

**Code Organization:**
- `src/pages/` - Page components
- `src/components/` - Reusable UI components
- `src/lib/` - Utilities and helpers
- `src/hooks/` - Custom React hooks
- `src/api/` - API client and data fetching
- `src/types/` - TypeScript type definitions

**Rationale for Selection:**
- **Performance**: Vite provides instant dev server startup and <50ms HMR
- **Simplicity**: No server-side rendering needed for admin dashboards (authenticated users only)
- **Flexibility**: Full control over routing and state management
- **Build Speed**: 10-100x faster builds than Create React App
- **Modern Tooling**: SWC, esbuild, and Rollup for optimal performance
- **Developer Experience**: Instant feedback loop for rapid dashboard development
- **Bundle Size**: Smaller production bundles compared to Next.js for SPA use cases

---

### Mobile Application (Greenfield - New Development)

#### Selected Starter: Flutter with Material 3

**Initialization Command:**

```bash
# Create Flutter project (Material 3 is default in Flutter 3.16+)
flutter create --org com.torii --project-name torii_mobile torii_mobile

# Navigate to project
cd torii_mobile

# Add essential dependencies
flutter pub add riverpod flutter_riverpod riverpod_annotation
flutter pub add go_router
flutter pub add drift drift_flutter
flutter pub add dev:build_runner dev:riverpod_generator dev:drift_dev

# Generate code for Riverpod and Drift
flutter pub run build_runner build --delete-conflicting-outputs
```

**Architectural Decisions Provided by Flutter + Material 3:**

**Language & Runtime:**
- Dart language (type-safe, null-safe)
- Flutter SDK 3.16+ (Material 3 enabled by default)
- Ahead-of-time (AOT) compilation for production
- Just-in-time (JIT) compilation for development (hot reload)

**UI Framework:**
- Material 3 design system (modern, accessible)
- Adaptive widgets for iOS/Android platform conventions
- Built-in theming system with ColorScheme
- Dark mode support out of the box

**State Management:**
- Riverpod for dependency injection and state management
- Riverpod code generation for type-safe providers
- AsyncValue for handling loading/error states
- StateNotifier for complex state logic

**Routing:**
- GoRouter for declarative routing
- Deep linking support
- Type-safe route parameters
- Nested navigation for complex flows

**Local Database (Offline-First):**
- Drift (SQLite) for local data persistence
- Type-safe SQL queries
- Reactive streams for real-time updates
- Migration support for schema changes

**Development Experience:**
- Hot reload (<1s code changes)
- Hot restart for state reset
- DevTools for debugging and profiling
- Widget Inspector for UI debugging

**Code Organization:**
- `lib/features/` - Feature-based organization
- `lib/core/` - Shared utilities and services
- `lib/models/` - Data models and entities
- `lib/providers/` - Riverpod providers
- `lib/widgets/` - Reusable widgets
- `lib/database/` - Drift database and DAOs

**Rationale for Selection:**
- **Offline-First**: Drift provides robust SQLite integration for 4-hour metro commute use case
- **Performance**: AOT compilation delivers native performance (60fps animations)
- **Cross-Platform**: Single codebase for iOS and Android with platform-specific adaptations
- **Material 3**: Modern design system aligned with UX spec requirements
- **Type Safety**: Dart's null safety and Riverpod code generation prevent runtime errors
- **Developer Experience**: Hot reload enables instant UI iteration
- **Ecosystem**: Mature package ecosystem for all required features (networking, storage, etc.)

---

### Cross-Platform Consistency Strategy

**Design Token Synchronization:**

To ensure visual consistency across Next.js, Vite/React, and Flutter:

1. **Define Shared Design Tokens** (colors, typography, spacing, shadows)
2. **Tailwind Config** (Web) → `tailwind.config.ts` with custom theme
3. **Flutter ThemeData** (Mobile) → Match color values from Tailwind config
4. **Documentation** → Maintain design token reference in Storybook (web) and Widget Catalog (Flutter)

**Component Naming Conventions:**

Use consistent naming across platforms:
- `CourseCard` (web) ↔ `CourseCard` (Flutter)
- `ProgressDashboard` (web) ↔ `ProgressDashboard` (Flutter)
- `FlashcardDeck` (web) ↔ `FlashcardDeck` (Flutter)

**API Integration:**

- **Web**: Axios or Fetch API with TypeScript types
- **Mobile**: Dio with Protobuf deserialization
- **Shared**: OpenAPI/Swagger spec for contract-first development

---

### Implementation Priority

**Phase 1: Backend Foundation** (Already Complete - Brownfield)
- ✅ NATS infrastructure
- ✅ Microservices (Identity, LMS, Meet, Cortex)
- ✅ Database schema (Prisma)
- ✅ API Gateway

**Phase 2: Web Learner App** (Week 1-4)
- Initialize Next.js 15 + shadcn/ui
- Course catalog and discovery
- Enrollment and payment (VNPay)
- Live class join (WebRTC)

**Phase 3: Web Admin/Staff Apps** (Week 3-6)
- Initialize Vite + React + shadcn/ui
- Role-specific dashboards
- Command center for operations
- Analytics and reporting

**Phase 4: Mobile App** (Week 5-8)
- Initialize Flutter + Material 3
- Offline-first architecture with Drift
- Core learner features (courses, flashcards, progress)
- Background sync

**Phase 5: Integration & Polish** (Week 7-10)
- Cross-platform testing
- Design system consistency validation
- Performance optimization
- Documentation

**Note:** Project initialization using these commands should be the first implementation story for each application.

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**
- Authentication & authorization patterns (JWT with refresh tokens)
- State management strategy (Redux for admin/meet, Zustand for learner)
- API communication patterns (Axios + TanStack Query)
- Cross-platform data synchronization (Protobuf for mobile, REST for web)
- Real-time communication architecture (NATS + WebRTC)

**Important Decisions (Shape Architecture):**
- Frontend routing strategies (App Router for Next.js, React Router for Vite)
- Error handling and logging standards
- Testing strategy and coverage targets
- CI/CD pipeline approach
- Monitoring and observability

**Deferred Decisions (Post-MVP):**
- Advanced caching strategies beyond Redis
- Microservices orchestration patterns
- Advanced analytics and BI integration
- Multi-region deployment strategy

---

### Data Architecture

**Database: PostgreSQL with Prisma ORM** (Existing - Brownfield)
- **Version**: PostgreSQL 15+, Prisma 5+
- **Rationale**: Already implemented, type-safe queries, excellent TypeScript integration
- **Migration Strategy**: Prisma Migrate for schema changes
- **Normalization**: 3NF for relational data
- **Affects**: All backend microservices

**Caching: Redis** (Existing - Brownfield)
- **Version**: Redis 7+
- **Use Cases**: Session management, API response caching, rate limiting
- **TTL Strategy**: 
  - Sessions: 30 minutes
  - API responses: 5-60 minutes (based on data volatility)
  - Rate limit counters: 1 minute sliding window
- **Affects**: Identity service, API Gateway

**Object Storage: MinIO/S3** (Existing - Brownfield)
- **Use Cases**: Video lessons, course materials, user uploads, live class recordings
- **Bucket Strategy**:
  - `videos-vod`: Pre-recorded course videos
  - `videos-live`: Live class recordings
  - `materials`: PDF, images, documents
  - `user-uploads`: Student assignments, profile pictures
- **CDN**: Consider CloudFront or similar for video delivery
- **Affects**: LMS service, Meet service, Storage service

**Mobile Local Database: Drift (SQLite)** (New - Greenfield)
- **Version**: Drift 2.14+
- **Use Cases**: Offline-first data persistence for mobile app
- **Sync Strategy**: Background sync when WiFi available, conflict resolution (last-write-wins for progress)
- **Schema**: Mirror subset of backend schema for offline access
- **Affects**: Flutter mobile app

**Data Validation Strategy:**
- **Backend**: Zod for DTO validation in NestJS
- **Frontend Web**: Zod + React Hook Form for form validation
- **Mobile**: Freezed + Riverpod for immutable state validation
- **Rationale**: Type-safe validation across all layers

---

### Authentication & Security

**Authentication Method: JWT with Refresh Tokens** (Existing + Enhanced)
- **Access Token**: 1 hour expiry, stored in memory (web) or secure storage (mobile)
- **Refresh Token**: 7 days expiry, httpOnly cookie (web) or Flutter Secure Storage (mobile)
- **Token Rotation**: Refresh token rotates on each use for security
- **Logout**: Blacklist refresh tokens in Redis
- **Affects**: All applications

**Authorization: RBAC with NATS Auth Callout** (Existing - Brownfield)
- **Roles**: Learner, Lecturer, Staff (Academic/Operations/Admissions/Financial), Admin
- **NATS Permissions**: Dynamic pub/sub permissions per user/room via Auth Callout
- **HTTP Permissions**: Role-based guards in NestJS
- **Frontend**: Role-based route protection and UI rendering
- **Affects**: All services, especially Meet service for real-time permissions

**API Security:**
- **CORS**: Centralized at API Gateway, whitelist specific origins
- **Rate Limiting**: Redis-based, 1000 requests/minute per API key
- **Input Validation**: Zod schemas for all DTOs
- **SQL Injection Prevention**: Prisma parameterized queries
- **XSS Prevention**: Content Security Policy headers, sanitize user inputs
- **CSRF Protection**: SameSite cookies, CSRF tokens for state-changing operations

**Data Encryption:**
- **In Transit**: TLS 1.3 for all HTTP/WebSocket connections
- **At Rest**: PostgreSQL encryption, encrypted S3 buckets
- **Sensitive Data**: bcrypt for passwords (cost factor 12), AES-256 for PII if needed
- **Affects**: All services

---

### API & Communication Patterns

**API Design: RESTful with Protobuf for Mobile** (Existing - Brownfield)
- **Web**: REST APIs with JSON responses
- **Mobile**: Protobuf for efficient serialization (bandwidth optimization)
- **Versioning**: URL versioning (`/api/v1/...`)
- **Pagination**: Cursor-based for large datasets, offset for small
- **Filtering**: Query parameters with Zod validation

**API Documentation: OpenAPI/Swagger** (Existing)
- **Generation**: NestJS Swagger decorators auto-generate spec
- **TypeScript Codegen**: Use `openapi-typescript-codegen` for web clients
- **Interactive Docs**: Swagger UI at `/api/docs`
- **Affects**: All microservices, frontend development

**HTTP Client (Web):**
- **Library**: Axios
- **Interceptors**: 
  - Request: Add JWT access token to Authorization header
  - Response: Auto-refresh token on 401, retry original request
- **Error Handling**: Centralized error interceptor, map backend errors to user-friendly messages
- **Base URLs**: Environment-specific (dev/staging/prod)
- **Affects**: Next.js learner app, Vite admin/meet apps

**Real-Time Communication:**
- **NATS JetStream**: Event-driven workflows (workqueues, pub/sub)
  - Subjects: `sysJsWorker.{roomId}.{userId}`, `chat.{roomId}`, `whiteboard.{roomId}`
  - Consumers: Per-user consumers for chat/whiteboard, worker pool for system events
- **WebRTC (LiveKit)**: Live video/audio for classes
  - Adaptive bitrate: Auto-adjust quality based on network
  - Recording: Auto-record to MinIO, transcode via NATS workqueue
- **WebSocket Fallback**: For clients that can't use NATS directly
- **Affects**: Meet service, mobile app, web meet app

**Error Handling Standards:**
- **HTTP Status Codes**: Proper use (200, 201, 400, 401, 403, 404, 500)
- **Error Response Format**:
  ```json
  {
    "statusCode": 400,
    "message": "User-friendly error message",
    "error": "BadRequest",
    "errorCode": "ERR_AUTH_001",
    "timestamp": "2026-01-03T15:30:00Z"
  }
  ```
- **Logging**: Structured logs with correlation IDs for request tracing
- **Affects**: All services

---

### Frontend Architecture

**State Management:**
- **Web Admin/Staff Apps (Vite/React)**: Redux Toolkit
  - Complex RBAC state management
  - Multi-role permission handling
  - Redux DevTools for debugging
- **Web Meet App (Vite/React)**: Redux Toolkit
  - Complex WebRTC state (participants, tracks, quality)
  - Real-time collaboration state
  - Debugging complex state transitions
- **Web Learner App (Next.js)**: Zustand
  - Lightweight state management
  - Simple learner-focused flows
  - Better performance for SSR
- **All Web Apps**: TanStack Query for server state
  - Automatic caching and refetching
  - Optimistic updates
  - Loading/error states
- **Mobile App (Flutter)**: Riverpod
  - Type-safe dependency injection
  - Code generation for providers
  - AsyncValue for loading/error states

**Routing:**
- **Next.js Learner App**: App Router (file-system based)
  - Server Components by default
  - Nested layouts for consistent UI
  - Protected routes via middleware
- **Vite Admin/Meet Apps**: React Router v6
  - Client-side routing
  - Nested routes for dashboard layouts
  - Protected routes via route guards
- **Mobile App**: GoRouter
  - Declarative routing
  - Deep linking support
  - Type-safe navigation

**Component Architecture:**
- **Design System**: shadcn/ui (web), Material 3 (mobile)
- **Component Structure**:
  - Atomic design pattern (atoms, molecules, organisms, templates, pages)
  - Feature-based organization for complex features
  - Shared components library for common UI elements
- **Styling**: Tailwind CSS (web), ThemeData (mobile)
- **Accessibility**: WCAG 2.1 AA compliance, ARIA labels, keyboard navigation

**Performance Optimization:**
- **Code Splitting**: Automatic (Next.js, Vite), manual for large features
- **Lazy Loading**: Route-based, component-based for heavy components
- **Image Optimization**: next/image (Next.js), CachedNetworkImage (Flutter)
- **Bundle Size**: Target <500KB initial load (web), <50MB APK (mobile)
- **Caching**: Service Worker for web, Drift cache for mobile

---

### Infrastructure & Deployment

**Hosting Strategy:**
- **Backend Microservices**: Docker containers, orchestrated via Docker Compose (dev) or Kubernetes (prod)
- **Web Apps**: 
  - Next.js: Vercel or self-hosted Node.js server
  - Vite/React: Static hosting (Netlify, Vercel, or S3 + CloudFront)
- **Mobile App**: App Store (iOS), Google Play (Android)
- **Database**: Managed PostgreSQL (AWS RDS, DigitalOcean, or self-hosted)
- **Redis**: Managed Redis (AWS ElastiCache or self-hosted)
- **NATS**: Self-hosted NATS cluster
- **LiveKit**: Self-hosted or LiveKit Cloud

**CI/CD Pipeline:**
- **Version Control**: Git with feature branch workflow
- **CI**: GitHub Actions or GitLab CI
  - Lint, test, build on every PR
  - Auto-deploy to staging on merge to `develop`
  - Manual approval for production deploy
- **CD**: Automated deployment to staging, manual to production
- **Docker Registry**: Docker Hub or private registry
- **Secrets Management**: Environment variables, encrypted secrets in CI/CD

**Environment Configuration:**
- **Environments**: Development, Staging, Production
- **Config Management**: `.env` files (local), environment variables (deployed)
- **Secrets**: Never commit to Git, use CI/CD secrets or secret management service
- **Feature Flags**: Simple boolean flags in config for gradual rollout

**Monitoring & Logging:**
- **Application Monitoring**: Sentry for error tracking
- **Performance Monitoring**: Lighthouse CI for web, Firebase Performance for mobile
- **Logging**: Structured JSON logs, centralized via ELK stack or similar
- **Metrics**: Prometheus + Grafana for backend metrics
- **Uptime Monitoring**: UptimeRobot or Pingdom
- **Affects**: All services

**Scaling Strategy:**
- **Horizontal Scaling**: Stateless microservices, load balancer in front
- **Database**: Read replicas for read-heavy operations
- **Caching**: Redis cluster for high availability
- **CDN**: CloudFront or similar for static assets and videos
- **WebRTC**: LiveKit auto-scales based on participant count
- **Target**: Support 50+ concurrent live classes, 10K users

---

### Decision Impact Analysis

**Implementation Sequence:**

1. **Phase 1: Foundation** (Week 1)
   - Initialize frontend projects (Next.js, Vite, Flutter)
   - Set up CI/CD pipelines
   - Configure environment variables
   - Set up monitoring and logging

2. **Phase 2: Authentication** (Week 1-2)
   - Implement JWT refresh token flow
   - Set up CORS at API Gateway
   - Implement protected routes
   - Test auth across all platforms

3. **Phase 3: Core Features** (Week 2-6)
   - Implement state management (Redux, Zustand, Riverpod)
   - Set up API clients (Axios, TanStack Query)
   - Implement core UI components (shadcn/ui, Material 3)
   - Build feature modules

4. **Phase 4: Real-Time Features** (Week 5-7)
   - Integrate NATS for real-time events
   - Implement WebRTC live classes
   - Build whiteboard collaboration
   - Test real-time sync

5. **Phase 5: Polish & Deploy** (Week 8-10)
   - Performance optimization
   - Accessibility audit
   - Security audit
   - Production deployment

**Cross-Component Dependencies:**

- **Authentication** affects all components (must be implemented first)
- **State Management** depends on API client setup
- **Real-Time Features** depend on NATS infrastructure (already exists)
- **Mobile Offline** depends on Drift schema (mirrors backend)
- **Monitoring** should be set up early to catch issues during development
