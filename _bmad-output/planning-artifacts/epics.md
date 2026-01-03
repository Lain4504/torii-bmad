---
stepsCompleted: [1, 2, 3, 4]
inputDocuments:
  - "_bmad-output/planning-artifacts/prd.md"
  - "_bmad-output/planning-artifacts/architecture.md"
  - "_bmad-output/planning-artifacts/ux-design-specification.md"
  - "_bmad-output/planning-artifacts/enhanced-requirements.md"
---

# torii-nihongo - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for torii-nihongo, decomposing the requirements from the PRD, UX Design, Architecture, and Enhanced Requirements into implementable stories.

## Requirements Inventory

### Functional Requirements

Based on the PRD, the system serves **4 user roles** with the following functional capabilities:

**Learner Experience (Web & Mobile):**
- FR1: Course discovery and browsing (VOD and Live classes)
- FR2: Live class seat reservation with availability checking
- FR3: VNPay payment integration and gifting code redemption
- FR4: Access to learning resources via "My Folders" (auto-organized by course)
- FR5: Automatic attendance tracking for live classes via WebRTC
- FR6: Progress tracking (videos watched, quizzes passed, live sessions attended)
- FR7: VOD access for hybrid courses (flipped classroom model)
- FR8: Progress dashboard with completion statistics
- FR9: JLPT practice exams with auto-grading
- FR10: Profile management (personal info, avatar, password)
- FR11: Financial records (payment history, gifted courses)
- FR12: SRS flashcards with cross-platform sync (web ↔ mobile)
- FR13: Offline learning capability (mobile - 4 hours without internet)

**AI Cortex Service (Multi-Agent):**
- FR14: AI Sensei - Contextual Q&A for vocabulary and grammar
- FR15: AI Sensei - Grammar correction with native-like suggestions
- FR16: AI Sensei - Auto-generate flashcards from text passages
- FR17: AI Assessment - Dynamic mini-test creation based on recent learning
- FR18: AI Assessment - Draft grading workflow for lecturers
- FR19: AI Assessment - Automated writing feedback (grammar, vocabulary errors)
- FR20: AI Assessment - JLPT score prediction based on 5-pillar profile
- FR21: AI Assessment - Smart exam generator from question bank (natural language queries)
- FR22: AI Analytics - Weakness identification and adaptive practice
- FR23: AI Analytics - Daily recommendation engine ("3 actions for today")
- FR24: AI Meet Integration - Real-time Kanji handwriting feedback on whiteboard
- FR25: AI Meet Integration - Live transcription and translation during classes

**Lecturer Operations (Web):**
- FR26: Live class management (start/end sessions)
- FR27: Automatic attendance tracking via WebRTC presence
- FR28: Real-time engagement heatmap (student participation metrics)
- FR29: AI-assisted grading (draft grading + lecturer review workflow)
- FR30: Whiteboard control with screen sharing
- FR31: Resource management (upload/share PDFs, images in real-time)
- FR32: Audio feedback recording for assignments
- FR33: Mentorship system for new lecturers

**Staff Operations (Web - 3 specialized roles):**

*Academic Staff:*
- FR34: Question bank management (CRUD operations)
- FR35: Exam generation with versioning
- FR36: Content versioning and approval workflows

*Operations Staff:*
- FR37: Command center dashboard (50+ concurrent classes monitoring)
- FR38: Real-time class health metrics (connection quality, participant count)
- FR39: Emergency lecturer re-assignment
- FR40: Network diagnostics and technical support

*Admissions/Marketing Staff:*
- FR41: Coupon management (create, distribute, track usage)
- FR42: CMS for marketing content
- FR43: Engagement tracking and analytics

*Financial Staff:*
- FR44: VNPay reconciliation (VNPay balance ↔ internal DB)
- FR45: Refund workflows (atomic: VNPay + DB + email)
- FR46: Revenue reporting and financial dashboards

**Admin Governance (Web):**
- FR47: Strategic KPI dashboard (LTV, CAC, retention, revenue trends)
- FR48: Financial reconciliation tools
- FR49: Audit trails for compliance (GDPR, educational standards)
- FR50: RBAC management (role assignment, permissions)
- FR51: User impersonation for support purposes

**Live Class Features (WebRTC):**
- FR52: WebRTC video/audio for live classes (15-20 participants per class)
- FR53: Collaborative whiteboard with real-time sync (<100ms latency)
- FR54: Chat functionality during live classes
- FR55: Screen sharing for lecturers
- FR56: Automatic class recording with transcoding
- FR57: Adaptive bitrate based on network quality
- FR58: Backup Zoom link for WebRTC failures (disaster recovery)

**Gamification:**
- FR59: XP system for learner actions
- FR60: Streak tracking (daily login, study consistency)
- FR61: Badge system for achievements
- FR62: Leaderboards (optional, privacy-respecting)

**Notifications:**
- FR63: Push notifications (mobile)
- FR64: Email notifications (class reminders, payment confirmations)
- FR65: SMS notifications (optional, for critical alerts)

### Non-Functional Requirements

**Performance:**
- NFR1: API response time <200ms (p95)
- NFR2: WebRTC latency <200ms
- NFR3: Whiteboard sync <100ms
- NFR4: AI feedback <3 seconds
- NFR5: Page load <2s (web), <1.5s (mobile)
- NFR6: Database queries <100ms (p95)
- NFR7: Video streaming <3s initial load

**Scalability:**
- NFR8: Support 50+ concurrent live classes
- NFR9: Support 10,000 users
- NFR10: Support 1,000 courses
- NFR11: 1TB video storage capacity
- NFR12: 1000 requests/minute per API key

**Reliability & Availability:**
- NFR13: 99.9% uptime SLA
- NFR14: Atomic transactions for payments/enrollments (no race conditions)
- NFR15: Graceful degradation (auto video quality reduction on poor network)
- NFR16: Disaster recovery (backup Zoom link for WebRTC outages)
- NFR17: Auto-save every 30 seconds (assignments, progress)

**Security & Compliance:**
- NFR18: JWT authentication (1-hour access tokens, 7-day refresh tokens)
- NFR19: RBAC with granular permissions
- NFR20: NATS Auth Callout for dynamic pub/sub authorization
- NFR21: GDPR compliance (data export, right to erasure, 30-day grace period)
- NFR22: PCI DSS compliance (VNPay tokenization, no card storage)
- NFR23: Audit trails for all sensitive operations
- NFR24: TLS 1.3 for all HTTP/WebSocket connections
- NFR25: bcrypt for passwords (cost factor 12)

**Accessibility:**
- NFR26: Keyboard navigation for all interactive elements
- NFR27: Screen reader support (ARIA labels, semantic HTML)
- NFR28: Video captions (auto-generated via Whisper API)
- NFR29: WCAG 2.1 AA compliance

**Cross-Platform:**
- NFR30: Consistent UX across web and mobile
- NFR31: Bidirectional sync (web ↔ mobile) for progress, flashcards, quiz scores
- NFR32: Offline-first mobile architecture (4+ hours without internet)
- NFR33: Background sync when WiFi reconnects

**Testing:**
- NFR34: Unit test coverage >60% (graduation requirement)
- NFR35: Integration tests for critical flows (payment, enrollment, live class join)
- NFR36: E2E tests for user journeys
- NFR37: Load testing for 50+ concurrent classes
- NFR38: AI grading accuracy validation

### Additional Requirements

**From Architecture Document:**

*Starter Templates & Initialization:*
- ARCH-REQ-1: Initialize Next.js 15 + shadcn/ui for Web Learner App
- ARCH-REQ-2: Initialize Vite 6 + React + shadcn/ui for Web Admin/Staff/Meet Apps
- ARCH-REQ-3: Initialize Flutter + Material 3 + Riverpod + Drift for Mobile App
- ARCH-REQ-4: Set up CI/CD pipelines (GitHub Actions or GitLab CI)
- ARCH-REQ-5: Configure environment variables for dev/staging/prod

*State Management:*
- ARCH-REQ-6: Implement Redux Toolkit for Web Admin/Staff Apps (complex RBAC)
- ARCH-REQ-7: Implement Redux Toolkit for Web Meet App (complex WebRTC state)
- ARCH-REQ-8: Implement Zustand for Web Learner App (lightweight)
- ARCH-REQ-9: Implement TanStack Query for all web apps (server state)
- ARCH-REQ-10: Implement Riverpod for Mobile App (dependency injection)

*API Integration:*
- ARCH-REQ-11: Set up Axios with interceptors (JWT refresh token flow)
- ARCH-REQ-12: Implement OpenAPI/Swagger TypeScript codegen for web clients
- ARCH-REQ-13: Configure CORS at API Gateway (centralized)
- ARCH-REQ-14: Implement error handling standards (structured error responses)

*Real-Time Communication:*
- ARCH-REQ-15: Integrate NATS JetStream for event-driven workflows
- ARCH-REQ-16: Implement WebRTC via LiveKit for live classes
- ARCH-REQ-17: Implement WebSocket fallback for NATS-incompatible clients
- ARCH-REQ-18: Set up NATS subjects (chat, whiteboard, system events)

*Data Synchronization:*
- ARCH-REQ-19: Implement Drift schema mirroring backend (mobile offline)
- ARCH-REQ-20: Implement background sync when WiFi reconnects
- ARCH-REQ-21: Implement conflict resolution (last-write-wins for progress)
- ARCH-REQ-22: Implement Protobuf serialization for mobile ↔ backend

*Monitoring & Observability:*
- ARCH-REQ-23: Set up Sentry for error tracking
- ARCH-REQ-24: Set up Prometheus + Grafana for backend metrics
- ARCH-REQ-25: Implement structured JSON logging with correlation IDs
- ARCH-REQ-26: Set up Lighthouse CI for web performance monitoring
- ARCH-REQ-27: Set up Firebase Performance for mobile monitoring

**From UX Design Specification:**

*Design System:*
- UX-REQ-1: Implement shadcn/ui design system for web applications
- UX-REQ-2: Implement Material 3 design system for mobile application
- UX-REQ-3: Synchronize design tokens across web and mobile (colors, typography, spacing)
- UX-REQ-4: Implement dark mode support (web and mobile)

*Responsive Design:*
- UX-REQ-5: Implement responsive layouts for web (desktop-first for power users)
- UX-REQ-6: Implement touch-optimized UI for mobile
- UX-REQ-7: Implement adaptive components for iOS/Android platform conventions

*User Experience Principles:*
- UX-REQ-8: "Invisible Technology, Visible Progress" - Hide complexity, show achievements
- UX-REQ-9: "AI as Amplifier, Not Replacement" - Lecturer-in-the-loop for grading
- UX-REQ-10: "Fail Fast, Recover Faster" - Clear error messages with recovery paths
- UX-REQ-11: "Role-Specific, Not Role-Restricted" - Contextual UI based on user role
- UX-REQ-12: "Offline-First for Learners, Real-Time for Collaboration" - Mobile offline, live class real-time

*Emotional Design Goals:*
- UX-REQ-13: Learners feel "Empowered Progress" (not overwhelmed)
- UX-REQ-14: Lecturers feel "Liberated to Teach" (not burdened by admin)
- UX-REQ-15: Operations staff feel "In Command" (not reactive)
- UX-REQ-16: Admins feel "Strategic Clarity" (not lost in data)

**From Enhanced Requirements:**

*Security Enhancements:*
- ENH-REQ-1: Implement strong password policies (min 8 chars, complexity requirements)
- ENH-REQ-2: Implement session management (30-min timeout, concurrent session limits)
- ENH-REQ-3: Implement rate limiting (Redis-based, 1000 req/min per API key)
- ENH-REQ-4: Implement input validation (Zod schemas for all DTOs)
- ENH-REQ-5: Implement XSS prevention (Content Security Policy headers)
- ENH-REQ-6: Implement CSRF protection (SameSite cookies, CSRF tokens)

*Accessibility Enhancements:*
- ENH-REQ-7: Implement keyboard shortcuts for power users
- ENH-REQ-8: Implement focus management for modals and dialogs
- ENH-REQ-9: Implement skip-to-content links
- ENH-REQ-10: Implement high-contrast mode option

*Future Enhancements (Post-MVP):*
- ENH-REQ-11: Social learning features (study groups, peer review, forums)
- ENH-REQ-12: Subscription model (monthly/yearly plans)
- ENH-REQ-13: Referral program with rewards
- ENH-REQ-14: Corporate licenses for bulk purchases
- ENH-REQ-15: AI conversation partner for speaking practice
- ENH-REQ-16: Multi-language UI (English support)

### FR Coverage Map

**Learner Experience:**
- FR1 → Epic 3: Course Discovery & Enrollment
- FR2 → Epic 3: Course Discovery & Enrollment
- FR3 → Epic 3: Course Discovery & Enrollment
- FR4 → Epic 4: Video Learning & Progress Tracking
- FR5 → Epic 7: Live WebRTC Classes
- FR6 → Epic 4: Video Learning & Progress Tracking
- FR7 → Epic 4: Video Learning & Progress Tracking
- FR8 → Epic 4: Video Learning & Progress Tracking
- FR9 → Epic 6: JLPT Practice & Assessment
- FR10 → Epic 2: Authentication & User Management
- FR11 → Epic 3: Course Discovery & Enrollment
- FR12 → Epic 5: Flashcards & SRS Learning
- FR13 → Epic 5: Flashcards & SRS Learning

**AI Cortex Service:**
- FR14 → Epic 8: AI Sensei (Learning Assistant)
- FR15 → Epic 8: AI Sensei (Learning Assistant)
- FR16 → Epic 8: AI Sensei (Learning Assistant)
- FR17 → Epic 9: AI Assessment & Grading
- FR18 → Epic 9: AI Assessment & Grading
- FR19 → Epic 9: AI Assessment & Grading
- FR20 → Epic 9: AI Assessment & Grading
- FR21 → Epic 9: AI Assessment & Grading
- FR22 → Epic 9: AI Assessment & Grading (Analytics)
- FR23 → Epic 9: AI Assessment & Grading (Analytics)
- FR24 → Epic 7: Live WebRTC Classes (AI Integration)
- FR25 → Epic 7: Live WebRTC Classes (AI Integration)

**Lecturer Operations:**
- FR26 → Epic 7: Live WebRTC Classes
- FR27 → Epic 7: Live WebRTC Classes
- FR28 → Epic 10: Lecturer & Staff Dashboards
- FR29 → Epic 9: AI Assessment & Grading
- FR30 → Epic 7: Live WebRTC Classes
- FR31 → Epic 7: Live WebRTC Classes
- FR32 → Epic 10: Lecturer & Staff Dashboards
- FR33 → Epic 10: Lecturer & Staff Dashboards

**Staff Operations:**
- FR34 → Epic 10: Lecturer & Staff Dashboards (Academic)
- FR35 → Epic 10: Lecturer & Staff Dashboards (Academic)
- FR36 → Epic 10: Lecturer & Staff Dashboards (Academic)
- FR37 → Epic 10: Lecturer & Staff Dashboards (Operations)
- FR38 → Epic 10: Lecturer & Staff Dashboards (Operations)
- FR39 → Epic 10: Lecturer & Staff Dashboards (Operations)
- FR40 → Epic 10: Lecturer & Staff Dashboards (Operations)
- FR41 → Epic 10: Lecturer & Staff Dashboards (Admissions/Marketing)
- FR42 → Epic 10: Lecturer & Staff Dashboards (Admissions/Marketing)
- FR43 → Epic 10: Lecturer & Staff Dashboards (Admissions/Marketing)
- FR44 → Epic 10: Lecturer & Staff Dashboards (Financial)
- FR45 → Epic 10: Lecturer & Staff Dashboards (Financial)
- FR46 → Epic 10: Lecturer & Staff Dashboards (Financial)

**Admin Governance:**
- FR47 → Epic 11: Admin Governance & Analytics
- FR48 → Epic 11: Admin Governance & Analytics
- FR49 → Epic 11: Admin Governance & Analytics
- FR50 → Epic 11: Admin Governance & Analytics
- FR51 → Epic 2: Authentication & User Management (Admin impersonation)

**Live Class Features:**
- FR52 → Epic 7: Live WebRTC Classes
- FR53 → Epic 7: Live WebRTC Classes
- FR54 → Epic 7: Live WebRTC Classes
- FR55 → Epic 7: Live WebRTC Classes
- FR56 → Epic 7: Live WebRTC Classes
- FR57 → Epic 7: Live WebRTC Classes
- FR58 → Epic 7: Live WebRTC Classes

**Gamification:**
- FR59 → Epic 12: Gamification & Notifications
- FR60 → Epic 12: Gamification & Notifications
- FR61 → Epic 12: Gamification & Notifications
- FR62 → Epic 12: Gamification & Notifications

**Notifications:**
- FR63 → Epic 12: Gamification & Notifications
- FR64 → Epic 12: Gamification & Notifications
- FR65 → Epic 12: Gamification & Notifications

**Coverage Summary:** 65/65 FRs mapped (100%)

## Epic List

### Epic 1: Foundation & Project Initialization
Enable the development team to set up all frontend applications with proper tooling, CI/CD, and monitoring infrastructure.

**User Outcome:** Development team can build, test, and deploy all applications with confidence.

**FRs covered:** None directly (enables all future epics)  
**NFRs covered:** NFR34-NFR38 (testing), NFR13 (uptime)  
**Additional Requirements:** ARCH-REQ-1 to ARCH-REQ-5, ARCH-REQ-23 to ARCH-REQ-27

---

### Epic 2: Authentication & User Management
Enable all users (Learners, Lecturers, Staff, Admin) to securely register, login, and manage their profiles across web and mobile platforms.

**User Outcome:** Users can create accounts, login securely, and manage their personal information.

**FRs covered:** FR10, FR51  
**NFRs covered:** NFR18-NFR20, NFR24-NFR25  
**Additional Requirements:** ARCH-REQ-6 to ARCH-REQ-14, ENH-REQ-1 to ENH-REQ-6

---

### Epic 3: Course Discovery & Enrollment
Enable learners to browse courses (VOD and Live), reserve seats for live classes, and complete purchases via VNPay or gifting codes.

**User Outcome:** Learners can discover courses, check live class availability, and enroll instantly.

**FRs covered:** FR1, FR2, FR3, FR11  
**NFRs covered:** NFR14, NFR22  
**Additional Requirements:** ARCH-REQ-11 to ARCH-REQ-14

---

### Epic 4: Video Learning & Progress Tracking
Enable learners to watch VOD lessons, track their progress, and resume from where they left off across web and mobile.

**User Outcome:** Learners can study at their own pace with seamless progress tracking.

**FRs covered:** FR4, FR6, FR7, FR8  
**NFRs covered:** NFR7, NFR17, NFR30-NFR33  
**Additional Requirements:** ARCH-REQ-19 to ARCH-REQ-22, UX-REQ-8

---

### Epic 5: Flashcards & SRS Learning
Enable learners to practice vocabulary using SRS flashcards with cross-platform synchronization and offline capability.

**User Outcome:** Learners can efficiently memorize vocabulary using spaced repetition.

**FRs covered:** FR12, FR13  
**NFRs covered:** NFR32, NFR33  
**Additional Requirements:** ARCH-REQ-19 to ARCH-REQ-22, UX-REQ-12

---

### Epic 6: JLPT Practice & Assessment
Enable learners to take JLPT practice exams with auto-grading and view their 5-pillar skill profile.

**User Outcome:** Learners can assess their JLPT readiness and identify weak areas.

**FRs covered:** FR9  
**NFRs covered:** NFR1, NFR6  
**Additional Requirements:** UX-REQ-8, UX-REQ-13

---

### Epic 7: Live WebRTC Classes
Enable learners and lecturers to participate in real-time live classes with video, audio, chat, and whiteboard collaboration.

**User Outcome:** Users can attend/teach live classes with high-quality real-time interaction.

**FRs covered:** FR5, FR24, FR25, FR26, FR27, FR30, FR31, FR52-FR58  
**NFRs covered:** NFR2, NFR3, NFR8, NFR15, NFR16  
**Additional Requirements:** ARCH-REQ-15 to ARCH-REQ-18, UX-REQ-12

---

### Epic 8: AI Sensei (Learning Assistant)
Enable learners to get instant help from AI for vocabulary, grammar, and flashcard generation.

**User Outcome:** Learners have 24/7 AI support for their learning questions.

**FRs covered:** FR14, FR15, FR16  
**NFRs covered:** NFR4  
**Additional Requirements:** UX-REQ-9, UX-REQ-13

---

### Epic 9: AI Assessment & Grading
Enable lecturers to use AI-assisted grading and enable learners to receive automated feedback on writing and JLPT score predictions.

**User Outcome:** Faster grading for lecturers, instant feedback for learners.

**FRs covered:** FR17, FR18, FR19, FR20, FR21, FR22, FR23, FR29  
**NFRs covered:** NFR4  
**Additional Requirements:** UX-REQ-9, UX-REQ-14

---

### Epic 10: Lecturer & Staff Dashboards
Enable lecturers and staff (Academic, Operations, Admissions, Financial) to manage their specialized workflows efficiently.

**User Outcome:** Lecturers and staff can perform their roles with powerful, role-specific tools.

**FRs covered:** FR28, FR32, FR33, FR34-FR46  
**NFRs covered:** NFR19  
**Additional Requirements:** ARCH-REQ-6, ARCH-REQ-7, UX-REQ-11, UX-REQ-14 to UX-REQ-16

---

### Epic 11: Admin Governance & Analytics
Enable admins to monitor system health, manage users, view strategic KPIs, and ensure compliance.

**User Outcome:** Admins have complete visibility and control over the platform.

**FRs covered:** FR47, FR48, FR49, FR50  
**NFRs covered:** NFR13, NFR21, NFR23  
**Additional Requirements:** UX-REQ-16, ENH-REQ-1 to ENH-REQ-6

---

### Epic 12: Gamification & Notifications
Enable learners to stay motivated through XP, streaks, badges, and receive timely notifications across all platforms.

**User Outcome:** Learners stay engaged and informed through gamification and notifications.

**FRs covered:** FR59-FR65  
**NFRs covered:** NFR26-NFR29  
**Additional Requirements:** UX-REQ-13, ENH-REQ-7 to ENH-REQ-10
