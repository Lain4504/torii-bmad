# 10-Week Sprint Plan - Torii Nihongo Capstone Project

**Project Duration:** 01/01/2026 - 30/04/2026 (10 weeks)  
**Team Size:** 3-4 members  
**Target:** MVP Delivery with Core Features  
**Last Updated:** 2026-01-02

---

## 🎯 Project Scope - MVP Definition

### ✅ IN SCOPE (Must Have)
- Course Browse, Search & Purchase (VOD + Live)
- Video-based Learning with Progress Tracking
- Live WebRTC Classes (Basic features)
- Personal Flashcards with SRS Algorithm
- Quiz & JLPT Practice Exams
- User Management (Learner, Lecturer, Staff, Admin)
- Payment Integration (VNPay)
- Basic AI Sensei (1 Agent - Q&A support)
- Mobile App (Learner role)
- Notifications & Reminders

### ⏸️ DEFERRED (Phase 2)
- Advanced Gamification (Badges, XP, Leaderboard)
- Deck Marketplace (Community sharing)
- Multi-Agent AI (Assessment & Analytics Agents)
- Audio Feedback for Lecturers
- Advanced Analytics Dashboard
- AI Handwriting Recognition

---

## 📅 Sprint Breakdown

### **WEEK 1-2: Foundation & Setup** 🏗️

#### Week 1: Architecture & Infrastructure
**Backend Team (2 people):**
- [x] Finalize Architecture Design Document
- [x] Setup Microservices structure (NestJS + Spring Boot)
- [ ] Database schema design & review
- [x] Setup PostgreSQL with Prisma
- [x] Configure NATS messaging
- [ ] Setup CI/CD pipeline (GitHub Actions)
- [ ] API Contract definition (OpenAPI/Swagger)

**Frontend Team (1 person):**
- [x] Setup Next.js project structure
- [x] Design system & component library
- [x] Setup Tailwind CSS + shadcn/ui
- [x] Authentication flow (JWT)
- [x] Layout templates (Dashboard, Course, Live Class)

**Mobile Team (1 person):**
- [x] Setup Flutter project
- [x] Configure libraries
- [x] Setup state management (Riverpod/Bloc)
- [x] Design mobile UI/UX mockups
- [x] Setup navigation structure

**Deliverables:**
- ✅ Architecture Design Document
- ✅ Database Schema (ERD)
- ✅ API Contract Specification
- ✅ Development environment ready

---

#### Week 2: Core Services Foundation
**Backend Team:**
- [ ] Identity Service (Auth, User Management)
  - JWT authentication
  - Role-based access control (RBAC)
  - User CRUD operations
- [ ] LMS Service foundation
  - Course model & API
  - Lesson/Module structure
  - Enrollment logic
- [ ] Setup MinIO for file storage
- [x] Setup LiveKit server (WebRTC)

**Frontend Team:**
- [x] Authentication pages (Login, Register)
- [ ] User profile management
- [ ] Course catalog page (Browse & Search)
- [ ] Course detail page

**Mobile Team:**
- [x] Authentication flow
- [x] Splash screen & onboarding
- [ ] Home screen layout
- [ ] Course list screen

**Deliverables:**
- ✅ Working authentication system
- ✅ Basic course browsing (Web + Mobile)

---

### **WEEK 3-4: Core Learning Features** 📚

#### Week 3: Course Learning & Video Player
**Backend Team:**
- [ ] LMS Service - Video streaming
  - Video upload & transcoding
  - Progress tracking API
  - Quiz/Exam API
- [ ] Billing Service foundation
  - VNPay integration
  - Order management
  - Payment webhook handling

**Frontend Team:**
- [ ] Video player with progress tracking
- [ ] Quiz interface
- [ ] Course progress dashboard
- [ ] Payment checkout flow
- [ ] VNPay integration (Web)

**Mobile Team:**
- [ ] Video player (video_player package)
- [ ] Offline video download
- [ ] Progress sync
- [ ] Course detail screen
- [ ] Quiz screen

**Deliverables:**
- ✅ Video learning functional (Web + Mobile)
- ✅ Payment flow working

---

#### Week 4: Flashcards & Exams
**Backend Team:**
- [ ] Flashcards Service
  - CRUD operations
  - SRS algorithm implementation
  - Sync API (Web ↔ Mobile)
- [ ] Assessment Service
  - Exam generation
  - Auto-grading (MCQ)
  - Score tracking

**Frontend Team:**
- [ ] Flashcard creation & review UI
- [ ] SRS study session
- [ ] Exam interface (timer, navigation)
- [ ] Test history & reports

**Mobile Team:**
- [ ] Flashcard UI (swipe cards)
- [ ] Offline SRS (Drift/SQLite)
- [ ] Background sync
- [ ] Exam interface (mobile-optimized)

**Deliverables:**
- ✅ Flashcard system with SRS
- ✅ JLPT practice exams

---

### **WEEK 5-6: Live Classes & Real-time Features** 🎥

#### Week 5: WebRTC Integration
**Backend Team:**
- [x] Meet Service (LiveKit integration)
  - Room creation & management
  - Participant management
  - Recording functionality
- [x] NATS signaling for WebRTC
- [ ] Attendance tracking

**Frontend Team:**
- [ ] Live class scheduling UI (Staff)
- [ ] Live class registration (Learner)
- [ ] WebRTC room interface
  - Video grid layout
  - Chat panel
  - Screen sharing
  - Basic whiteboard

**Mobile Team:**
- [ ] Live class list & schedule
- [ ] WebRTC mobile interface
  - LiveKit Flutter SDK
  - Mobile-optimized layout
  - Chat integration

**Deliverables:**
- ✅ Live WebRTC classes functional
- ✅ Recording & playback

---

#### Week 6: Lecturer & Staff Features
**Backend Team:**
- [ ] Assignment Service
  - Assignment CRUD
  - Submission handling
  - Grading API
- [ ] Notification Service
  - Push notifications (FCM)
  - Email notifications
  - In-app notifications

**Frontend Team:**
- [ ] Lecturer Dashboard
  - Class schedule
  - Student list & attendance
  - Assignment management
- [ ] Staff Dashboard
  - Course management
  - Class scheduling
  - Question bank management

**Mobile Team:**
- [ ] Assignment submission (mobile)
- [ ] Push notification setup
- [ ] Notification center
- [ ] Profile & settings

**Deliverables:**
- ✅ Lecturer tools functional
- ✅ Staff management tools
- ✅ Notification system working

---

### **WEEK 7: AI Integration & Polish** 🤖

#### Week 7: AI Sensei (Basic)
**Backend Team:**
- [ ] Cortex Service (FastMCP)
  - Sensei Agent (Q&A)
  - Grammar checking
  - Translation support
- [ ] AI API integration (OpenAI/Gemini)
- [ ] Context management

**Frontend Team:**
- [ ] AI chat interface
- [ ] Context-aware help (highlight text → ask AI)
- [ ] Admin Dashboard
  - System statistics
  - User management
  - Payment monitoring

**Mobile Team:**
- [ ] AI chat (mobile)
- [ ] My Folders (shared resources)
- [ ] Payment history
- [ ] Settings & preferences

**Deliverables:**
- ✅ Basic AI Sensei working
- ✅ Admin dashboard complete
- ✅ All core features integrated

---

### **WEEK 8-9: Testing & Refinement** 🧪

#### Week 8: Integration Testing
**Whole Team:**
- [ ] End-to-end testing
  - User registration → Course purchase → Learning → Live class
  - Payment flow (VNPay sandbox)
  - WebRTC stability testing
- [ ] Cross-browser testing (Web)
- [ ] Cross-device testing (Mobile)
- [ ] Performance optimization
  - API response time
  - Video streaming quality
  - Database query optimization
- [ ] Security audit
  - JWT validation
  - SQL injection prevention
  - XSS protection

**Deliverables:**
- ✅ Test report
- ✅ Bug tracking & fixes

---

#### Week 9: User Acceptance Testing & Bug Fixing
**Whole Team:**
- [ ] UAT with real users (if possible)
- [ ] Bug fixing sprint
- [ ] UI/UX refinement
- [ ] Mobile app optimization
- [ ] Load testing (WebRTC rooms)
- [ ] Documentation updates

**Deliverables:**
- ✅ Stable, tested system
- ✅ Known issues documented

---

### **WEEK 10: Deployment & Documentation** 🚀

#### Week 10: Final Sprint
**Backend Team:**
- [ ] Production deployment
  - Docker containers
  - Kubernetes/Cloud deployment
  - Database migration
  - Environment configuration
- [ ] Monitoring setup (Prometheus/Grafana)
- [ ] Backup & recovery procedures

**Frontend Team:**
- [ ] Web app deployment (Vercel/Netlify)
- [ ] Final UI polish
- [ ] User manual (Web)
- [ ] Installation guide

**Mobile Team:**
- [ ] Mobile app build (APK/IPA)
- [ ] App store preparation (if needed)
- [ ] User manual (Mobile)

**Documentation Team (All):**
- [ ] System Analysis & Design Document
- [ ] Test Plan & Test Cases
- [ ] Installation Manual
- [ ] User Manual (Admin, Staff, Lecturer, Learner)
- [ ] API Documentation
- [ ] Demo preparation
- [ ] Presentation slides

**Deliverables:**
- ✅ Deployed system (Production)
- ✅ Complete documentation set
- ✅ Demo-ready application

---

## 📊 Resource Allocation

### Recommended Team Structure (4 people)

| Member       | Primary Role       | Secondary Role | Workload                 |
|--------------|--------------------|----------------|--------------------------|
| **Member 1** | Backend Lead       | DevOps | 40% Backend, 10% DevOps  |
| **Member 2** | Backend Developer  | Testing | 40% Backend, 10% Testing |
| **Member 3** | Frontend Developer | Documentation | 40% Web, 10% Docs        |
| **Member 4** | Mobile Developer   | UI/UX | 40% Mobile, 10% Design   |
| **Member 5** | Testing            |UI/UX + Docs | 40% Testing, 5% UX, 5% Docs  |
### Alternative (3 people - Tight but doable)

| Member | Responsibilities |
|--------|-----------------|
| **Member 1** | Backend (Identity, LMS, Billing) + DevOps |
| **Member 2** | Backend (Meet, Flashcards, Cortex) + Web Frontend |
| **Member 3** | Mobile App + Documentation |

---

## ⚠️ Risk Mitigation

### Critical Risks & Mitigation Strategies

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| WebRTC complexity | HIGH | MEDIUM | Use LiveKit SDK, start early (Week 5) |
| VNPay integration issues | HIGH | LOW | Use sandbox early, test thoroughly |
| AI API rate limits | MEDIUM | MEDIUM | Implement caching, use fallback responses |
| Team member unavailable | HIGH | MEDIUM | Cross-training, documentation |
| Scope creep | HIGH | HIGH | Strict MVP scope, defer non-critical features |

---

## 🎯 Success Metrics

### Week-by-Week Milestones

- **Week 2:** Authentication working ✅
- **Week 4:** Video learning + Payment working ✅
- **Week 6:** Live classes functional ✅
- **Week 7:** All core features integrated ✅
- **Week 9:** System tested & stable ✅
- **Week 10:** Deployed & documented ✅

### Final Acceptance Criteria

- [ ] All functional requirements (MVP scope) implemented
- [ ] Web app supports 4 user roles
- [ ] Mobile app supports Learner role
- [ ] Live WebRTC classes work with 10+ participants
- [ ] Payment flow (VNPay) functional
- [ ] System deployed to production
- [ ] All documentation complete
- [ ] Demo presentation ready

---

## 📝 Notes

- **Daily Standups:** 15 minutes, track progress & blockers
- **Weekly Reviews:** Friday afternoon, demo progress
- **Code Reviews:** Mandatory for all PRs
- **Documentation:** Update continuously, not just Week 10
- **Testing:** Write tests alongside features, not after

---

**Good luck! 🚀 Bạn có thể làm được!**
