# torii-nihongo - Epic Stories Summary

## Epic 1: Foundation & Project Initialization (6 stories)

### Story 1.1: Initialize Next.js Learner App
As a developer, I want to initialize the Next.js 15 learner app with shadcn/ui, so that we have a production-ready foundation.

**AC:** Next.js 15 created, shadcn/ui configured, Tailwind CSS working, TypeScript strict mode enabled.

### Story 1.2: Initialize Vite Admin/Staff/Meet Apps
As a developer, I want to initialize Vite React apps for admin/staff/meet, so that we have SPAs for power users.

**AC:** 3 Vite apps created, shadcn/ui configured, React Router v6 setup, Redux Toolkit integrated.

### Story 1.3: Initialize Flutter Mobile App
As a developer, I want to initialize the Flutter mobile app with Material 3, so that learners have offline-capable mobile experience.

**AC:** Flutter project created, Material 3 enabled, Riverpod setup, Drift configured, GoRouter integrated.

### Story 1.4: Set Up CI/CD Pipelines
As a developer, I want CI/CD pipelines for all apps, so that we can deploy automatically.

**AC:** GitHub Actions configured, lint/test/build on PR, auto-deploy to staging, manual prod approval.

### Story 1.5: Configure Monitoring & Logging
As a developer, I want monitoring and logging infrastructure, so that we can track errors and performance.

**AC:** Sentry for errors, Prometheus+Grafana for metrics, structured JSON logging, correlation IDs.

### Story 1.6: Set Up Environment Configuration
As a developer, I want environment configs for dev/staging/prod, so that we can manage secrets securely.

**AC:** .env files for local, environment variables for deployed, secrets in CI/CD, feature flags support.

---

## Epic 2: Authentication & User Management (8 stories)

### Story 2.1: User Registration (Web & Mobile)
As a learner, I want to register with email/password, so that I can create an account.

**AC:** Registration form, email validation, password strength check, bcrypt hashing, JWT tokens issued.

### Story 2.2: User Login (Web & Mobile)
As a user, I want to login with email/password, so that I can access my account.

**AC:** Login form, credentials validation, JWT access (1hr) + refresh (7day) tokens, httpOnly cookies (web), secure storage (mobile).

### Story 2.3: JWT Refresh Token Flow
As a user, I want automatic token refresh, so that I stay logged in without interruption.

**AC:** Axios interceptor detects 401, refreshes token, retries original request, logout on refresh failure.

### Story 2.4: Profile Management
As a user, I want to update my profile, so that my information is current.

**AC:** Update name/email/avatar, password change, email verification for email changes, avatar upload to MinIO.

### Story 2.5: RBAC Implementation
As an admin, I want role-based access control, so that users only see what they're authorized for.

**AC:** 4 roles (Learner, Lecturer, Staff, Admin), role-based route guards, role-specific UI rendering, permission checks on API.

### Story 2.6: NATS Auth Callout Integration
As a system, I want dynamic NATS permissions, so that users can only pub/sub to authorized subjects.

**AC:** Auth Callout endpoint, JWT validation, dynamic permissions per user/room, pub/sub authorization working.

### Story 2.7: Session Management
As a system, I want session management, so that we prevent unauthorized access.

**AC:** 30-min timeout, concurrent session limits, session blacklist in Redis, logout invalidates tokens.

### Story 2.8: Admin User Impersonation
As an admin, I want to impersonate users, so that I can provide support.

**AC:** Impersonate button (admin only), switch to user context, audit trail logged, exit impersonation.

---

## Epic 3: Course Discovery & Enrollment (7 stories)

### Story 3.1: Course Catalog (Web & Mobile)
As a learner, I want to browse courses, so that I can find what I want to learn.

**AC:** Course list with filters (VOD/Live, JLPT level), search, pagination, course cards with details.

### Story 3.2: Course Detail Page
As a learner, I want to view course details, so that I can decide if I want to enroll.

**AC:** Course description, curriculum, instructor info, price, reviews, enrollment button.

### Story 3.3: Live Class Seat Reservation
As a learner, I want to reserve a seat for live classes, so that I can secure my spot.

**AC:** Schedule selection, seat availability check, atomic reservation (15-min lock via NATS), reservation confirmation.

### Story 3.4: VNPay Payment Integration
As a learner, I want to pay via VNPay, so that I can enroll in courses.

**AC:** VNPay checkout, deep linking, webhook callback, atomic enrollment (payment + DB + email), transaction logging.

### Story 3.5: Gifting Code System
As a learner, I want to gift courses, so that I can share learning with others.

**AC:** Generate gift code, code redemption, recipient chooses schedule, gifting history tracking.

### Story 3.6: Enrollment Confirmation
As a learner, I want enrollment confirmation, so that I know I'm enrolled.

**AC:** Email confirmation, course access granted, My Courses list updated, calendar invite for live classes.

### Story 3.7: Financial Records
As a learner, I want to view my payment history, so that I can track my spending.

**AC:** Transaction list, invoice download, gifted courses list, refund status.

---

## Epic 4: Video Learning & Progress Tracking (6 stories)

### Story 4.1: Video Player (Web & Mobile)
As a learner, I want to watch course videos, so that I can learn at my own pace.

**AC:** Video playback from MinIO, playback controls, quality selection, resume from last position, <3s initial load.

### Story 4.2: My Folders Organization
As a learner, I want my course materials organized, so that I can find resources easily.

**AC:** Auto-organized folders by course, PDFs/images accessible, download for offline (mobile).

### Story 4.3: Progress Tracking
As a learner, I want my progress tracked, so that I know how much I've completed.

**AC:** Videos watched tracked, quiz completion tracked, live session attendance tracked, progress % calculated.

### Story 4.4: Progress Dashboard
As a learner, I want to see my progress dashboard, so that I can monitor my learning.

**AC:** Completion statistics, time spent, upcoming live classes, recommended next steps.

### Story 4.5: Cross-Platform Sync (Web ↔ Mobile)
As a learner, I want my progress synced, so that I can switch between devices.

**AC:** Bidirectional sync, conflict resolution (last-write-wins), sync indicator, background sync on WiFi.

### Story 4.6: Auto-Save Progress
As a learner, I want auto-save, so that I don't lose my progress.

**AC:** Auto-save every 30 seconds, save on navigation, save on app background, recovery on crash.

---

## Epic 5: Flashcards & SRS Learning (5 stories)

### Story 5.1: Flashcard Deck Display
As a learner, I want to view flashcard decks, so that I can practice vocabulary.

**AC:** Deck list, card count, SRS stats, deck selection, study button.

### Story 5.2: SRS Flashcard Practice
As a learner, I want SRS-based practice, so that I memorize efficiently.

**AC:** SRS algorithm (SM-2), card flip animation, difficulty rating (Again/Hard/Good/Easy), next review date calculated.

### Story 5.3: Offline Flashcard Practice (Mobile)
As a learner, I want offline flashcard practice, so that I can study without internet.

**AC:** Drift SQLite stores cards, offline practice works, sync when WiFi reconnects, 4+ hours offline capability.

### Story 5.4: Flashcard Progress Sync
As a learner, I want flashcard progress synced, so that my reviews are consistent across devices.

**AC:** Review history synced, SRS intervals synced, conflict resolution, sync indicator.

### Story 5.5: Custom Flashcard Creation
As a learner, I want to create custom flashcards, so that I can personalize my learning.

**AC:** Add card form, front/back text, furigana support, image upload, save to personal deck.

---

## Epic 6: JLPT Practice & Assessment (4 stories)

### Story 6.1: Exam Center
As a learner, I want to access practice exams, so that I can prepare for JLPT.

**AC:** Exam list (N5-N1), exam details, start exam button, timer display.

### Story 6.2: Take Practice Exam
As a learner, I want to take timed exams, so that I can simulate real JLPT conditions.

**AC:** Countdown timer, question navigation, answer selection, submit exam, auto-submit on timeout.

### Story 6.3: Auto-Grading & Results
As a learner, I want instant results, so that I know my score immediately.

**AC:** Auto-grading for multiple choice, score calculation, correct/incorrect answers shown, explanations provided.

### Story 6.4: 5-Pillar JLPT Profile
As a learner, I want my 5-pillar profile, so that I can see my strengths/weaknesses.

**AC:** Vocabulary/Grammar/Reading/Listening/Kanji scores, trend charts, weak areas highlighted, recommendations.

---

## Epic 7: Live WebRTC Classes (10 stories)

### Story 7.1: Join Live Class (Learner)
As a learner, I want to join live classes, so that I can attend real-time lessons.

**AC:** Join button, LiveKit connection, video/audio enabled, participant list visible, <200ms latency.

### Story 7.2: Start/End Live Class (Lecturer)
As a lecturer, I want to start/end classes, so that I can manage sessions.

**AC:** Start class button, LiveKit room created, end class button, auto-attendance tracking, recording starts.

### Story 7.3: Collaborative Whiteboard
As a user, I want a shared whiteboard, so that we can draw/write together.

**AC:** Drawing tools, real-time sync (<100ms), multi-user cursors, clear board, save snapshot.

### Story 7.4: Chat During Class
As a user, I want to chat, so that I can ask questions.

**AC:** Chat panel, send message via NATS, real-time delivery, emoji support, chat history.

### Story 7.5: Screen Sharing (Lecturer)
As a lecturer, I want to share my screen, so that I can show materials.

**AC:** Share screen button, screen selection, stop sharing, learners see shared screen.

### Story 7.6: Automatic Attendance Tracking
As a lecturer, I want auto-attendance, so that I don't manually track it.

**AC:** Attendance based on WebRTC presence, join/leave timestamps, attendance report, export to CSV.

### Story 7.7: Adaptive Bitrate
As a user, I want adaptive quality, so that class works on poor networks.

**AC:** Auto-adjust video quality, network quality indicator (green/yellow/red), graceful degradation.

### Story 7.8: Class Recording
As a system, I want to record classes, so that learners can review later.

**AC:** Auto-record on class start, save to MinIO, transcode via NATS workqueue, recording available in My Folders.

### Story 7.9: AI Kanji Handwriting Feedback
As a learner, I want AI to check my Kanji, so that I learn correct stroke order.

**AC:** Draw Kanji on whiteboard, AI recognizes strokes, real-time feedback on errors, <100ms latency.

### Story 7.10: Backup Zoom Link (Disaster Recovery)
As a user, I want a backup link, so that class continues if WebRTC fails.

**AC:** Zoom link generated, displayed on WebRTC failure, automatic fallback, notification sent.

---

## Epic 8: AI Sensei (Learning Assistant) (4 stories)

### Story 8.1: Contextual Q&A
As a learner, I want to ask AI about vocabulary/grammar, so that I get instant help.

**AC:** Highlight text, ask AI button, AI response <3s, context-aware answers, examples provided.

### Story 8.2: Grammar Correction
As a learner, I want AI to correct my Japanese, so that I write naturally.

**AC:** Input Japanese text, AI analyzes grammar, suggests corrections, native-like alternatives, explanations.

### Story 8.3: Auto-Generate Flashcards
As a learner, I want AI to create flashcards, so that I save time.

**AC:** Select text passage, generate flashcards button, AI extracts vocabulary, furigana added, save to deck.

### Story 8.4: FastMCP Integration
As a system, I want FastMCP protocol, so that AI responses are fast.

**AC:** FastMCP client setup, Sensei agent connected, <3s response time, error handling, retry logic.

---

## Epic 9: AI Assessment & Grading (6 stories)

### Story 9.1: Dynamic Mini-Test Creation
As a learner, I want AI-generated tests, so that I can practice recent topics.

**AC:** Request mini-test, AI selects questions based on recent learning, test generated, take test, auto-graded.

### Story 9.2: Draft Grading Workflow (Lecturer)
As a lecturer, I want AI draft grading, so that I save time.

**AC:** AI grades assignments, highlights errors, draft score, lecturer reviews, approve/modify score, final grade saved.

### Story 9.3: Automated Writing Feedback
As a learner, I want AI feedback on writing, so that I improve.

**AC:** Submit writing, AI analyzes grammar/vocabulary, errors highlighted, suggestions provided, score given.

### Story 9.4: JLPT Score Prediction
As a learner, I want JLPT score prediction, so that I know if I'm ready.

**AC:** Based on 5-pillar profile, AI predicts JLPT score, confidence level shown, weak areas identified.

### Story 9.5: Smart Exam Generator (Academic Staff)
As academic staff, I want AI to generate exams, so that I create tests faster.

**AC:** Natural language query ("Create N3 exam focused on particles"), AI selects from question bank, exam generated, preview, publish.

### Story 9.6: Weakness Identification & Adaptive Practice
As a learner, I want AI to identify weaknesses, so that I focus on what I need.

**AC:** AI analyzes performance, identifies weak topics, recommends practice, adaptive difficulty, daily recommendations.

---

## Epic 10: Lecturer & Staff Dashboards (12 stories)

### Story 10.1: Lecturer Dashboard
As a lecturer, I want my dashboard, so that I can manage my classes.

**AC:** Upcoming classes, attendance stats, grading queue, student performance overview.

### Story 10.2: Engagement Heatmap
As a lecturer, I want engagement metrics, so that I know who's participating.

**AC:** Real-time heatmap, participation scores, question frequency, attention indicators.

### Story 10.3: Resource Management
As a lecturer, I want to upload/share resources, so that students have materials.

**AC:** Upload PDF/images, share in real-time during class, students receive instantly, resource library.

### Story 10.4: Audio Feedback Recording
As a lecturer, I want to record audio feedback, so that I provide personalized comments.

**AC:** Record audio button, attach to assignment, student receives notification, playback in app.

### Story 10.5: Mentorship System
As a lecturer, I want mentorship features, so that I can guide new lecturers.

**AC:** Mentor assignment, observation scheduling, feedback forms, mentorship progress tracking.

### Story 10.6: Academic Staff - Question Bank Management
As academic staff, I want to manage questions, so that we have quality exams.

**AC:** CRUD operations, question versioning, difficulty tagging, JLPT level categorization, approval workflow.

### Story 10.7: Academic Staff - Exam Generation
As academic staff, I want to create exams, so that we can assess students.

**AC:** Select questions, configure exam (time, passing score), preview, publish, versioning.

### Story 10.8: Operations Staff - Command Center Dashboard
As operations staff, I want to monitor all classes, so that I can provide support.

**AC:** 50+ concurrent classes displayed, health metrics (connection quality, participant count), alerts for issues.

### Story 10.9: Operations Staff - Emergency Re-assignment
As operations staff, I want to reassign lecturers, so that classes continue if lecturer is absent.

**AC:** Detect lecturer no-show, available lecturers list, reassign button, notifications sent, class continues.

### Story 10.10: Admissions/Marketing - Coupon Management
As admissions staff, I want to manage coupons, so that we can run promotions.

**AC:** Create coupon, set discount %, expiry date, usage limits, track redemptions, deactivate.

### Story 10.11: Admissions/Marketing - CMS
As admissions staff, I want to manage content, so that marketing pages are updated.

**AC:** Edit homepage, blog posts, landing pages, preview, publish, SEO metadata.

### Story 10.12: Financial Staff - VNPay Reconciliation
As financial staff, I want to reconcile payments, so that finances are accurate.

**AC:** VNPay balance vs internal DB, discrepancy report, refund workflows, revenue dashboards.

---

## Epic 11: Admin Governance & Analytics (5 stories)

### Story 11.1: Strategic KPI Dashboard
As an admin, I want KPI dashboard, so that I can track business health.

**AC:** LTV, CAC, retention, revenue trends, user growth, course popularity, charts/graphs.

### Story 11.2: Financial Reconciliation Tools
As an admin, I want reconciliation tools, so that finances are transparent.

**AC:** VNPay ↔ DB comparison, transaction logs, refund tracking, revenue reports, export to Excel.

### Story 11.3: Audit Trails
As an admin, I want audit trails, so that we comply with regulations.

**AC:** All sensitive operations logged, user/timestamp/action, GDPR compliance, data export, right to erasure.

### Story 11.4: RBAC Management
As an admin, I want to manage roles, so that permissions are correct.

**AC:** Assign roles, modify permissions, role templates, permission matrix, audit log.

### Story 11.5: System Health Monitoring
As an admin, I want system health metrics, so that I can ensure uptime.

**AC:** 99.9% uptime tracking, error rates, API response times, database performance, alerts on issues.

---

## Epic 12: Gamification & Notifications (7 stories)

### Story 12.1: XP System
As a learner, I want to earn XP, so that I feel rewarded for learning.

**AC:** XP for actions (video watched, quiz passed, class attended), XP display, level progression.

### Story 12.2: Streak Tracking
As a learner, I want streak tracking, so that I stay motivated to study daily.

**AC:** Daily login streak, study streak, streak calendar, streak recovery (1-day grace), notifications.

### Story 12.3: Badge System
As a learner, I want to earn badges, so that I can celebrate achievements.

**AC:** Badge criteria defined, badges awarded automatically, badge collection display, share badges.

### Story 12.4: Leaderboards (Optional)
As a learner, I want leaderboards, so that I can compete with peers.

**AC:** Weekly/monthly leaderboards, privacy-respecting (opt-in), XP-based ranking, top 10 display.

### Story 12.5: Push Notifications (Mobile)
As a learner, I want push notifications, so that I don't miss important updates.

**AC:** Class reminders, assignment due, new content, streak reminder, notification preferences.

### Story 12.6: Email Notifications
As a user, I want email notifications, so that I stay informed.

**AC:** Class reminders, payment confirmations, enrollment confirmations, weekly summary, unsubscribe option.

### Story 12.7: Accessibility Features
As a user, I want accessible features, so that everyone can use the platform.

**AC:** Keyboard navigation, screen reader support (ARIA), video captions, high-contrast mode, skip-to-content links.

---

## Summary

**Total Epics:** 12  
**Total Stories:** 80  
**Coverage:** 65/65 FRs (100%), 38 NFRs, 43 Additional Requirements

**Implementation Priority:**
1. Epic 1 (Foundation) - Week 1
2. Epic 2 (Auth) - Week 1-2
3. Epic 3 (Enrollment) - Week 2-3
4. Epic 4 (Video Learning) - Week 3-4
5. Epic 5 (Flashcards) - Week 4-5
6. Epic 6 (JLPT) - Week 5-6
7. Epic 7 (Live Classes) - Week 5-7
8. Epic 8-9 (AI) - Week 6-8
9. Epic 10 (Dashboards) - Week 7-9
10. Epic 11 (Admin) - Week 8-9
11. Epic 12 (Gamification) - Week 9-10
