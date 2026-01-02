# Enhanced Requirements & Future Features - Torii Nihongo

**Document Type:** Product Enhancement Backlog  
**Project:** Torii Nihongo Capstone  
**Version:** 1.0  
**Last Updated:** 2026-01-02  
**Status:** Future Consideration / Post-MVP

---

## 📋 Document Purpose

This document contains **enhanced requirements** and **future feature opportunities** that were identified during PRD analysis but are **NOT included in the MVP scope** (10-week graduation project).

These features are categorized by:
- **Priority:** Must Have / Should Have / Nice to Have / Future
- **Effort:** Low / Medium / High
- **Value:** Critical / High / Medium / Low
- **Phase:** When to implement (MVP, Post-MVP, Production)

---

## 🎯 Feature Prioritization Matrix

| Category | Priority | Effort | Value | Recommended Phase |
|----------|----------|--------|-------|-------------------|
| Security & Privacy | 🔴 MUST HAVE | Medium | Critical | MVP (Week 8-9) |
| Error Handling | 🟡 SHOULD HAVE | Low | High | MVP (Week 7-8) |
| Accessibility | 🟡 SHOULD HAVE | Medium | High | Post-MVP |
| Social Learning | 🟢 NICE TO HAVE | High | Medium | Post-MVP |
| Advanced Analytics | 🟢 NICE TO HAVE | Medium | Medium | Post-MVP |
| Engagement Features | 🟢 NICE TO HAVE | Medium | High | Production |
| Content Enhancement | 🟢 NICE TO HAVE | High | Medium | Production |
| Business Features | ⚪ FUTURE | Medium | High | Production |
| Quality of Life | ⚪ FUTURE | Low | Low | Production |

---

## 🔴 CRITICAL: Security & Privacy Requirements

### US.SEC.01 - Strong Password Policy

**As a** User (any role),  
**I want** the system to enforce strong password policies,  
**So that** my account is protected from unauthorized access.

**Acceptance Criteria:**
- [ ] Password minimum 8 characters
- [ ] Must contain: 1 uppercase, 1 lowercase, 1 number, 1 special character
- [ ] Real-time password strength indicator (Weak/Medium/Strong)
- [ ] Cannot reuse last 3 passwords
- [ ] Password reset via email with expiring token (15 minutes validity)
- [ ] Account lockout after 5 failed login attempts (30 min cooldown)

**Technical Notes:**
- Use bcrypt with cost factor 12 for hashing
- Store password history (hashed) for reuse check
- Implement rate limiting on login endpoint

**Estimated Effort:** 3 story points  
**Priority:** 🔴 Critical  
**Recommended Phase:** MVP Week 8

---

### US.SEC.02 - Session Management & Timeout

**As a** User,  
**I want** my session to automatically expire after inactivity,  
**So that** my account remains secure if I forget to log out.

**Acceptance Criteria:**
- [ ] Session timeout after 30 minutes of inactivity
- [ ] Warning popup 2 minutes before timeout with "Extend Session" button
- [ ] Concurrent session limit: 3 devices maximum
- [ ] "Active Sessions" page showing all logged-in devices
- [ ] "Force Logout All" option in settings
- [ ] Auto-save draft work before timeout (assignments, flashcards)

**Technical Notes:**
- JWT access token: 1 hour expiry
- JWT refresh token: 7 days expiry
- Redis for session tracking
- WebSocket heartbeat for activity detection

**Estimated Effort:** 5 story points  
**Priority:** 🔴 Critical  
**Recommended Phase:** MVP Week 8

---

### US.SEC.03 - Data Privacy & GDPR Compliance

**As a** Learner,  
**I want** to download all my personal data and delete my account,  
**So that** I have control over my information.

**Acceptance Criteria:**
- [ ] "Download My Data" button in Settings → Privacy
- [ ] Export includes: Profile, Purchase History, Learning Progress, Test Scores, Flashcards
- [ ] Export format: JSON (machine-readable) and PDF (human-readable)
- [ ] "Delete Account" with 2-step confirmation (password + email verification)
- [ ] 30-day grace period before permanent deletion
- [ ] Data anonymization (replace PII with "Deleted User #12345")
- [ ] Email notification upon successful deletion

**Technical Notes:**
- Async job for data export (can take 5-10 minutes)
- Soft delete (mark as deleted, actual deletion after 30 days)
- Cascade delete related data (progress, submissions, etc.)
- Keep transaction records for legal compliance (7 years)

**Estimated Effort:** 8 story points  
**Priority:** 🟡 Important  
**Recommended Phase:** Post-MVP

---

### US.SEC.04 - Payment Security & Fraud Detection

**As a** Learner,  
**I want** my payment information to be securely handled,  
**So that** I can trust the platform with my financial data.

**Acceptance Criteria:**
- [ ] No credit card data stored on our servers (VNPay handles it)
- [ ] Payment page uses HTTPS with valid SSL certificate (TLS 1.3)
- [ ] Transaction history shows masked card numbers (****1234)
- [ ] Email notification for every transaction (success or failure)
- [ ] Suspicious activity detection:
  - 5+ failed payments in 1 hour → Lock account + notify user
  - Payment from unusual location → 2FA verification required
- [ ] PCI DSS compliance checklist completed

**Technical Notes:**
- Use VNPay's tokenization for recurring payments
- Log all payment attempts (success, failure, reason)
- Implement rate limiting on payment endpoint (3 attempts/min)

**Estimated Effort:** 5 story points  
**Priority:** 🔴 Critical  
**Recommended Phase:** MVP Week 3 (with Payment integration)

---

## 🟡 IMPORTANT: Error Handling & User Experience

### US.ERR.01 - Graceful Error Messages

**As a** User,  
**I want** to see helpful error messages when something goes wrong,  
**So that** I know what to do next.

**Acceptance Criteria:**
- [ ] No technical jargon (e.g., "500 Internal Server Error" → "Something went wrong. Please try again.")
- [ ] Suggest next action (e.g., "Refresh the page" or "Contact support at support@torii.vn")
- [ ] Error codes for support reference (e.g., "Error Code: ERR_AUTH_001")
- [ ] Different messages for different user roles (Learner sees simpler messages than Admin)
- [ ] Friendly illustrations for error pages (404, 500, etc.)
- [ ] "Report Issue" button on error pages

**Technical Notes:**
- Centralized error handling middleware
- Error code mapping table
- Sentry or similar for error tracking

**Estimated Effort:** 3 story points  
**Priority:** 🟡 Important  
**Recommended Phase:** MVP Week 7

---

### US.ERR.02 - Offline Mode (Mobile App)

**As a** Mobile Learner,  
**I want** to continue learning when I lose internet connection,  
**So that** I can study anywhere without interruption.

**Acceptance Criteria:**
- [ ] Downloaded videos playable offline
- [ ] Flashcards work offline (sync when back online)
- [ ] Quiz progress saved locally (submit when online)
- [ ] Clear "Offline" indicator in app header
- [ ] Auto-sync when connection restored
- [ ] Conflict resolution (if data changed on server while offline)
- [ ] Download management (view downloaded content, delete to free space)

**Technical Notes:**
- Use Drift (SQLite) for local storage
- Background sync with WorkManager (Android) / BackgroundTasks (iOS)
- Incremental sync to minimize data usage

**Estimated Effort:** 8 story points  
**Priority:** 🟡 Important  
**Recommended Phase:** MVP Week 4 (with Video feature)

---

### US.ERR.03 - Network Quality Indicator (Live Class)

**As a** Learner in Live Class,  
**I want** to see my network quality status,  
**So that** I know if technical issues are on my end.

**Acceptance Criteria:**
- [ ] Real-time indicator: 🟢 Green (Good), 🟡 Yellow (Fair), 🔴 Red (Poor)
- [ ] Show metrics: Ping (ms), Upload/Download speed (Mbps), Packet loss (%)
- [ ] Automatic video quality adjustment based on network
- [ ] Notification if quality drops below threshold: "Your connection is unstable. Video quality has been reduced."
- [ ] "Report Issue" button to notify Staff with diagnostic data
- [ ] Network test before joining class (optional)

**Technical Notes:**
- LiveKit provides network quality metrics
- WebRTC stats API for detailed metrics
- Adaptive bitrate streaming

**Estimated Effort:** 5 story points  
**Priority:** 🟡 Important  
**Recommended Phase:** MVP Week 5 (with WebRTC)

---

## 🟡 IMPORTANT: Accessibility (A11y)

### US.A11Y.01 - Keyboard Navigation

**As a** User with mobility impairments,  
**I want** to navigate the entire platform using only keyboard,  
**So that** I can use the platform without a mouse.

**Acceptance Criteria:**
- [ ] All interactive elements accessible via Tab key
- [ ] Visible focus indicators (blue outline)
- [ ] Keyboard shortcuts:
  - `Ctrl+S`: Save (assignments, flashcards)
  - `Ctrl+/`: Open search
  - `Esc`: Close modals/popups
  - `Space`: Play/pause video
- [ ] "Skip to main content" link at top of page
- [ ] Logical tab order (top to bottom, left to right)
- [ ] No keyboard traps (can always escape from any component)

**Technical Notes:**
- Use semantic HTML (`<button>`, `<nav>`, etc.)
- Test with keyboard-only navigation
- ARIA attributes where needed

**Estimated Effort:** 5 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

### US.A11Y.02 - Screen Reader Support

**As a** Visually impaired User,  
**I want** the platform to work with screen readers (NVDA, JAWS),  
**So that** I can access all features independently.

**Acceptance Criteria:**
- [ ] All images have descriptive alt text
- [ ] ARIA labels for interactive elements (buttons, links, form fields)
- [ ] Semantic HTML with proper heading hierarchy (H1 → H2 → H3)
- [ ] Form labels properly associated with inputs
- [ ] Live region announcements for dynamic content (e.g., "Quiz submitted successfully")
- [ ] Skip navigation links
- [ ] Tested with NVDA (Windows) and VoiceOver (Mac/iOS)

**Technical Notes:**
- Use `aria-label`, `aria-describedby`, `aria-live`
- Lighthouse accessibility audit score > 90

**Estimated Effort:** 8 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

### US.A11Y.03 - Video Captions & Transcripts

**As a** Deaf/Hard-of-hearing Learner,  
**I want** all video lessons to have captions,  
**So that** I can follow along with the content.

**Acceptance Criteria:**
- [ ] Auto-generated captions for all videos (using AI - Whisper API)
- [ ] Lecturer can edit/improve captions in video management panel
- [ ] Toggle captions on/off
- [ ] Adjustable caption settings:
  - Font size (Small, Medium, Large)
  - Background color (Black, White, Transparent)
  - Position (Bottom, Top)
- [ ] Download caption file (SRT format)
- [ ] Full transcript available below video

**Technical Notes:**
- OpenAI Whisper for auto-captioning
- Store captions in WebVTT format
- Video player supports caption tracks

**Estimated Effort:** 5 story points  
**Priority:** 🟡 Important  
**Recommended Phase:** MVP Week 9 (Quick win for accessibility)

---

## 🟢 NICE TO HAVE: Social Learning Features

### US.SOCIAL.01 - Study Groups

**As a** Learner,  
**I want** to create or join study groups with other learners,  
**So that** we can learn together and motivate each other.

**Acceptance Criteria:**
- [ ] Create study group (max 10 members)
- [ ] Invite by email or shareable link
- [ ] Group chat for discussion
- [ ] Shared flashcard decks within group
- [ ] Schedule group study sessions (sync calendars)
- [ ] Group leaderboard (friendly competition)
- [ ] Group admin can remove members

**Technical Notes:**
- Real-time chat using WebSocket or NATS
- Permissions: Group creator is admin

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

### US.SOCIAL.02 - Peer Review (Assignments)

**As a** Learner,  
**I want** to review other learners' assignments anonymously,  
**So that** I can learn from their work and improve my own.

**Acceptance Criteria:**
- [ ] Opt-in feature (Learner chooses to share assignment)
- [ ] Anonymous peer review (assigned 3 random peers)
- [ ] Rubric provided by Lecturer
- [ ] Peer feedback visible after submission deadline
- [ ] Bonus XP for providing helpful reviews (rated by assignment owner)
- [ ] Report inappropriate reviews

**Technical Notes:**
- Random assignment algorithm (avoid friends reviewing each other)
- Anonymization layer

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

### US.SOCIAL.03 - Discussion Forum

**As a** Learner,  
**I want** to ask questions in a course-specific forum,  
**So that** I can get help from peers and instructors.

**Acceptance Criteria:**
- [ ] Forum per course
- [ ] Post questions with tags (Grammar, Vocabulary, Kanji, etc.)
- [ ] Upvote/downvote answers
- [ ] Lecturer can mark "Best Answer"
- [ ] Email notification for replies (opt-in)
- [ ] Search forum by keyword
- [ ] Sort by: Recent, Popular, Unanswered

**Technical Notes:**
- Similar to Stack Overflow model
- Moderation tools for Staff

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

## 🟢 NICE TO HAVE: Advanced Analytics

### US.ANALYTICS.01 - Learning Insights Dashboard

**As a** Learner,  
**I want** to see detailed insights about my learning patterns,  
**So that** I can optimize my study habits.

**Acceptance Criteria:**
- [ ] Time spent per skill (Listening, Reading, Writing, Speaking, Kanji)
- [ ] Best study time analysis (e.g., "You perform best at 8-10 PM")
- [ ] Streak calendar (days studied consecutively)
- [ ] Comparison with peers (anonymized, percentile rank)
- [ ] Predicted JLPT pass probability (based on current progress)
- [ ] Personalized study recommendations (e.g., "Focus on Grammar this week")
- [ ] Export report as PDF

**Technical Notes:**
- Data warehouse for analytics
- Machine learning model for predictions

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

### US.ANALYTICS.02 - Lecturer Performance Dashboard

**As a** Lecturer,  
**I want** to see analytics about my teaching effectiveness,  
**So that** I can improve my methods.

**Acceptance Criteria:**
- [ ] Student engagement metrics:
  - Average attendance rate
  - Participation rate (questions asked, polls answered)
  - Assignment submission rate
- [ ] Average test scores by class
- [ ] Student satisfaction ratings (anonymous surveys)
- [ ] Comparison with other lecturers (anonymized)
- [ ] Early warning: Identify struggling students (low attendance + low scores)
- [ ] Export reports for performance review

**Technical Notes:**
- Aggregated data from multiple sources
- Privacy-preserving analytics

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

### US.ANALYTICS.03 - Admin Business Intelligence

**As an** Admin,  
**I want** to see business metrics and trends,  
**So that** I can make data-driven decisions.

**Acceptance Criteria:**
- [ ] Revenue trends (daily, weekly, monthly)
- [ ] Course popularity rankings
- [ ] User acquisition sources (organic, referral, ads)
- [ ] Churn rate and retention metrics
- [ ] Lecturer utilization rates (hours taught vs capacity)
- [ ] Predictive analytics:
  - Forecasted revenue (next month)
  - Predicted churn risk (users likely to cancel)
- [ ] Export dashboards as PDF/Excel

**Technical Notes:**
- BI tool integration (Metabase, Superset)
- Data pipeline for ETL

**Estimated Effort:** 21 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

## 🟢 NICE TO HAVE: Engagement & Retention

### US.ENGAGE.01 - Daily Challenges

**As a** Learner,  
**I want** to receive daily mini-challenges,  
**So that** I stay engaged and build a learning habit.

**Acceptance Criteria:**
- [ ] One challenge per day (5-10 minutes to complete)
- [ ] Adaptive difficulty based on learner's level
- [ ] Challenge types: Vocabulary quiz, Grammar exercise, Listening practice
- [ ] Streak bonus for consecutive days (e.g., 7-day streak = 2x XP)
- [ ] Push notification reminder (customizable time)
- [ ] Leaderboard for challenge completion
- [ ] Rewards: XP, badges, or discount vouchers

**Technical Notes:**
- Cron job to generate daily challenges
- Notification service integration

**Estimated Effort:** 8 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** MVP Week 9 (Quick engagement boost)

---

### US.ENGAGE.02 - Learning Streaks & Rewards

**As a** Learner,  
**I want** to be rewarded for consistent learning,  
**So that** I stay motivated to continue.

**Acceptance Criteria:**
- [ ] Streak counter (days studied)
- [ ] Milestone rewards:
  - 7 days: Bronze badge + 100 XP
  - 30 days: Silver badge + 500 XP + 5% discount voucher
  - 100 days: Gold badge + 2000 XP + 10% discount voucher
- [ ] Streak freeze (1 per month if you miss a day)
- [ ] Visual streak calendar (GitHub-style contribution graph)
- [ ] Share streak achievement on social media
- [ ] Leaderboard for longest streaks

**Technical Notes:**
- Daily cron job to update streaks
- Gamification service

**Estimated Effort:** 8 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

### US.ENGAGE.03 - Personalized Smart Reminders

**As a** Learner,  
**I want** the system to remind me to study at optimal times,  
**So that** I don't forget and maintain my progress.

**Acceptance Criteria:**
- [ ] AI learns my study patterns (when I usually study)
- [ ] Smart reminder timing (when I'm most likely to study)
- [ ] Customizable reminder frequency (Daily, Every 2 days, Weekly)
- [ ] Snooze option (15 min, 1 hour, Tomorrow)
- [ ] Different reminders for different activities:
  - SRS flashcards: "Time to review 20 cards!"
  - Live Class: "Your N3 class starts in 15 minutes"
  - Assignments: "Assignment due in 2 days"
- [ ] Quiet hours (no reminders during sleep time)

**Technical Notes:**
- Machine learning for pattern detection
- FCM for push notifications

**Estimated Effort:** 8 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

## 🟢 NICE TO HAVE: Content Enhancement

### US.CONTENT.01 - Interactive Exercises

**As a** Learner,  
**I want** interactive exercises beyond multiple choice,  
**So that** I can practice in more engaging ways.

**Acceptance Criteria:**
- [ ] Drag-and-drop sentence building
- [ ] Fill-in-the-blank with word bank
- [ ] Matching exercises (word to meaning, kanji to reading)
- [ ] Listening comprehension with playback control (slow, normal, fast)
- [ ] Speaking practice:
  - Record audio
  - Playback to self-review
  - AI pronunciation scoring (optional)

**Technical Notes:**
- Custom interactive components
- Web Audio API for recording

**Estimated Effort:** 13 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

### US.CONTENT.02 - AI Conversation Partner

**As a** Learner,  
**I want** to practice conversation with an AI,  
**So that** I can improve my speaking skills anytime.

**Acceptance Criteria:**
- [ ] Text-based conversation (Phase 1)
- [ ] Voice conversation (Phase 2)
- [ ] Scenario-based practice:
  - Restaurant ordering
  - Shopping
  - Job interview
  - Casual conversation
- [ ] Real-time grammar correction
- [ ] Vocabulary suggestions
- [ ] Conversation history saved
- [ ] Difficulty levels (Beginner, Intermediate, Advanced)

**Technical Notes:**
- OpenAI GPT for conversation
- Whisper for speech-to-text
- ElevenLabs for text-to-speech

**Estimated Effort:** 21 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Production

---

### US.CONTENT.03 - Progress-based Content Unlocking

**As a** Learner,  
**I want** content to unlock as I progress,  
**So that** I'm not overwhelmed and stay focused.

**Acceptance Criteria:**
- [ ] Lessons unlock sequentially (Lesson 2 unlocks after Lesson 1)
- [ ] Optional setting: Must pass quiz to unlock next lesson
- [ ] Visual progress path (like a game map)
- [ ] "Skip ahead" option for advanced learners (requires placement test)
- [ ] Locked content shows preview (title, description, duration)
- [ ] Clear indication of prerequisites

**Technical Notes:**
- Prerequisite logic in course structure
- Progress tracking service

**Estimated Effort:** 8 story points  
**Priority:** 🟢 Nice to Have  
**Recommended Phase:** Post-MVP

---

## ⚪ FUTURE: Business & Monetization

### US.BIZ.01 - Subscription Model

**As a** Learner,  
**I want** to subscribe monthly instead of buying individual courses,  
**So that** I have access to all content at a lower cost.

**Acceptance Criteria:**
- [ ] Monthly subscription: $29.99/month (unlimited access to all VOD courses)
- [ ] Annual subscription: $299.99/year (2 months free)
- [ ] Free trial: 7 days (credit card required)
- [ ] Cancel anytime (no refund for current period)
- [ ] Subscription management in Settings
- [ ] Auto-renewal with email reminder 3 days before
- [ ] Pause subscription (1-3 months)

**Technical Notes:**
- VNPay recurring payment
- Subscription lifecycle management

**Estimated Effort:** 13 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** Production

---

### US.BIZ.02 - Referral Program

**As a** Learner,  
**I want** to refer friends and get rewards,  
**So that** I can save money while helping others discover the platform.

**Acceptance Criteria:**
- [ ] Unique referral link per user (e.g., torii.vn/ref/ABC123)
- [ ] Referrer gets 20% discount voucher on next purchase
- [ ] Referee gets 10% off first purchase
- [ ] Track referrals in dashboard (Invited, Signed Up, Purchased)
- [ ] Leaderboard for top referrers
- [ ] Bonus rewards at milestones:
  - 5 referrals: Free 1-month subscription
  - 10 referrals: Free 3-month subscription
  - 20 referrals: Free 1 year subscription

**Technical Notes:**
- Referral tracking service
- Coupon generation

**Estimated Effort:** 8 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** Production

---

### US.BIZ.03 - Corporate/Group Licenses

**As a** Corporate Admin,  
**I want** to purchase licenses for my employees,  
**So that** they can learn Japanese for business purposes.

**Acceptance Criteria:**
- [ ] Bulk license purchase (minimum 10 users)
- [ ] Corporate dashboard to manage users:
  - Add/remove users
  - View usage reports
  - Export progress reports for HR
- [ ] Custom branding option (company logo on login page)
- [ ] Dedicated account manager (for 50+ licenses)
- [ ] Volume discounts:
  - 10-49 users: 10% off
  - 50-99 users: 20% off
  - 100+ users: 30% off
- [ ] Invoice payment option (NET 30)

**Technical Notes:**
- Multi-tenant architecture
- Enterprise billing

**Estimated Effort:** 21 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** Production

---

## ⚪ FUTURE: Quality of Life Improvements

### US.QOL.01 - Dark Mode

**As a** User,  
**I want** a dark mode option,  
**So that** I can study comfortably at night without eye strain.

**Acceptance Criteria:**
- [ ] Toggle in Settings → Appearance
- [ ] System preference detection (auto dark mode based on OS)
- [ ] Consistent across all pages (Web + Mobile)
- [ ] Proper contrast ratios (WCAG AA compliant)
- [ ] Smooth transition animation (0.3s)
- [ ] Persistent preference (saved to user profile)

**Technical Notes:**
- CSS variables for theming
- `prefers-color-scheme` media query

**Estimated Effort:** 3 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** MVP Week 9 (Quick win)

---

### US.QOL.02 - Customizable Dashboard

**As a** User,  
**I want** to customize my dashboard layout,  
**So that** I see the information most relevant to me.

**Acceptance Criteria:**
- [ ] Drag-and-drop widgets
- [ ] Show/hide widgets
- [ ] Resize widgets (1x1, 2x1, 2x2 grid)
- [ ] Save layout preferences to user profile
- [ ] Reset to default layout option
- [ ] Different default layouts for different roles (Learner vs Lecturer)

**Technical Notes:**
- React Grid Layout or similar
- Store layout config in JSON

**Estimated Effort:** 8 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** Production

---

### US.QOL.03 - Multi-language UI

**As a** Non-Vietnamese User,  
**I want** the interface in English,  
**So that** I can navigate the platform easily.

**Acceptance Criteria:**
- [ ] Language switcher in header (🇻🇳 Vietnamese | 🇬🇧 English)
- [ ] Support Vietnamese and English
- [ ] Persistent language preference (saved to user profile)
- [ ] All UI elements translated (buttons, labels, error messages)
- [ ] Course content remains in original language (Japanese)
- [ ] RTL support (optional, for future Arabic/Hebrew)

**Technical Notes:**
- i18next for internationalization
- Translation files (en.json, vi.json)

**Estimated Effort:** 5 story points  
**Priority:** ⚪ Future  
**Recommended Phase:** Production

---

## 📊 Implementation Roadmap

### MVP (Week 1-10) - Graduation Project
**Focus:** Core features + Critical security

✅ **Include:**
- SEC.01, SEC.02, SEC.04 (Security basics)
- ERR.01, ERR.02 (Error handling)
- A11Y.03 (Video captions - easy win)
- QOL.01 (Dark mode - easy win)
- ENGAGE.01 (Daily challenges - engagement boost)

**Total Added Effort:** ~25 story points (fits in Week 8-9 polish phase)

---

### Post-MVP (Month 2-3) - Production Preparation
**Focus:** Accessibility + Social features

✅ **Include:**
- SEC.03 (Data privacy)
- A11Y.01, A11Y.02 (Full accessibility)
- SOCIAL.01 (Study groups)
- CONTENT.03 (Progress unlocking)

**Total Effort:** ~45 story points

---

### Production (Month 4-6) - Growth Features
**Focus:** Engagement + Monetization

✅ **Include:**
- ANALYTICS.01, ANALYTICS.02, ANALYTICS.03
- ENGAGE.02, ENGAGE.03
- BIZ.01, BIZ.02 (Subscription + Referral)
- CONTENT.01, CONTENT.02

**Total Effort:** ~100 story points

---

### Future (Month 7+) - Enterprise & Advanced
**Focus:** Enterprise features + Advanced AI

✅ **Include:**
- BIZ.03 (Corporate licenses)
- SOCIAL.02, SOCIAL.03 (Peer review + Forum)
- QOL.02, QOL.03 (Customization + i18n)

**Total Effort:** ~60 story points

---

## 📝 Notes for Development Team

1. **Prioritization Flexibility:**
   - This backlog is a guide, not a strict requirement
   - Re-prioritize based on user feedback and business needs

2. **Effort Estimation:**
   - Story points are rough estimates (1 SP ≈ 1 day of work)
   - Re-estimate during sprint planning

3. **Dependencies:**
   - Some features depend on infrastructure (e.g., Analytics requires data warehouse)
   - Plan infrastructure work ahead of feature work

4. **User Feedback:**
   - Validate assumptions with real users before building
   - Run A/B tests for engagement features

5. **Technical Debt:**
   - Don't rush features at the cost of code quality
   - Allocate 20% of each sprint to refactoring

---

**Document Status:** Living Document (update as priorities change)  
**Next Review:** End of MVP (Week 10)
