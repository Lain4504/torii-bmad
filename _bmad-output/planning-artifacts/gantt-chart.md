# Gantt Chart - Torii Nihongo Capstone Project

**Project Duration:** 10 weeks (01/01/2026 - 30/04/2026)  
**Last Updated:** 2026-01-02

---

## 📊 Visual Timeline

```
Week:  1    2    3    4    5    6    7    8    9    10
       |----|----|----|----|----|----|----|----|----|----|
Phase: [Foundation][Core Learning][Live+RT][AI][Test][Deploy]
```

---

## 🗓️ Phase Breakdown

### Phase 1: Foundation & Setup (Week 1-2)
```
Week 1: ████████████████████ (Architecture & Infrastructure)
Week 2: ████████████████████ (Core Services Foundation)
```

### Phase 2: Core Learning Features (Week 3-4)
```
Week 3: ████████████████████ (Video Learning & Payment)
Week 4: ████████████████████ (Flashcards & Exams)
```

### Phase 3: Live Classes & Real-time (Week 5-6)
```
Week 5: ████████████████████ (WebRTC Integration)
Week 6: ████████████████████ (Lecturer & Staff Tools)
```

### Phase 4: AI & Polish (Week 7)
```
Week 7: ████████████████████ (AI Sensei & Admin Dashboard)
```

### Phase 5: Testing & Refinement (Week 8-9)
```
Week 8: ████████████████████ (Integration Testing)
Week 9: ████████████████████ (UAT & Bug Fixing)
```

### Phase 6: Deployment & Documentation (Week 10)
```
Week 10: ████████████████████ (Production Deploy & Docs)
```

---

## 📋 Detailed Task Timeline

### Legend:
- 🔴 Critical Path (delay affects deadline)
- 🟡 Important (affects other tasks)
- 🟢 Normal (can be done in parallel)
- ⚪ Optional (nice to have)

---

## Week 1: Architecture & Infrastructure

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Architecture Design Doc | Backend Lead | 🔴 | W1-D1 | W1-D3 | 3d | - | ⬜ TODO |
| Database Schema Design | Backend Lead | 🔴 | W1-D2 | W1-D4 | 3d | Architecture | ⬜ TODO |
| API Contract Definition | Backend Team | 🔴 | W1-D3 | W1-D5 | 3d | Schema | ⬜ TODO |
| Setup CI/CD Pipeline | Backend Lead | 🟡 | W1-D1 | W1-D5 | 5d | - | ⬜ TODO |
| Next.js Project Setup | Frontend | 🟡 | W1-D1 | W1-D2 | 2d | - | ⬜ TODO |
| Flutter Project Setup | Mobile | 🟡 | W1-D1 | W1-D2 | 2d | - | ⬜ TODO |
| Design System Setup | Frontend | 🟢 | W1-D3 | W1-D5 | 3d | Next.js Setup | ⬜ TODO |

---

## Week 2: Core Services Foundation

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Identity Service (Auth) | Backend 1 | 🔴 | W2-D1 | W2-D3 | 3d | DB Schema | ⬜ TODO |
| LMS Service Foundation | Backend 2 | 🔴 | W2-D1 | W2-D4 | 4d | DB Schema | ⬜ TODO |
| MinIO Setup | Backend 1 | 🟡 | W2-D4 | W2-D5 | 2d | - | ⬜ TODO |
| LiveKit Server Setup | Backend 2 | 🟡 | W2-D4 | W2-D5 | 2d | - | ⬜ TODO |
| Auth Pages (Web) | Frontend | 🔴 | W2-D2 | W2-D4 | 3d | Identity API | ⬜ TODO |
| Course Catalog Page | Frontend | 🟡 | W2-D3 | W2-D5 | 3d | LMS API | ⬜ TODO |
| Auth Flow (Mobile) | Mobile | 🔴 | W2-D2 | W2-D4 | 3d | Identity API | ⬜ TODO |

---

## Week 3: Video Learning & Payment

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Video Streaming API | Backend 2 | 🔴 | W3-D1 | W3-D3 | 3d | LMS Service | ⬜ TODO |
| Progress Tracking API | Backend 2 | 🟡 | W3-D3 | W3-D4 | 2d | Video API | ⬜ TODO |
| VNPay Integration (BE) | Backend 1 | 🔴 | W3-D1 | W3-D4 | 4d | Billing Service | ⬜ TODO |
| Video Player (Web) | Frontend | 🔴 | W3-D2 | W3-D4 | 3d | Video API | ⬜ TODO |
| Payment Flow (Web) | Frontend | 🔴 | W3-D3 | W3-D5 | 3d | VNPay API | ⬜ TODO |
| Video Player (Mobile) | Mobile | 🔴 | W3-D2 | W3-D5 | 4d | Video API | ⬜ TODO |

---

## Week 4: Flashcards & Exams

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Flashcards Service | Backend 1 | 🔴 | W4-D1 | W4-D3 | 3d | - | ⬜ TODO |
| SRS Algorithm | Backend 1 | 🔴 | W4-D2 | W4-D4 | 3d | Flashcards API | ⬜ TODO |
| Assessment Service | Backend 2 | 🔴 | W4-D1 | W4-D3 | 3d | - | ⬜ TODO |
| Auto-grading Logic | Backend 2 | 🟡 | W4-D3 | W4-D5 | 3d | Assessment API | ⬜ TODO |
| Flashcard UI (Web) | Frontend | 🟡 | W4-D2 | W4-D4 | 3d | Flashcards API | ⬜ TODO |
| Exam Interface (Web) | Frontend | 🟡 | W4-D2 | W4-D5 | 4d | Assessment API | ⬜ TODO |
| Flashcard UI (Mobile) | Mobile | 🟡 | W4-D2 | W4-D5 | 4d | Flashcards API | ⬜ TODO |

---

## Week 5: WebRTC Integration

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Meet Service (LiveKit) | Backend 2 | 🔴 | W5-D1 | W5-D4 | 4d | LiveKit Setup | ⬜ TODO |
| Room Management API | Backend 2 | 🔴 | W5-D2 | W5-D4 | 3d | Meet Service | ⬜ TODO |
| Recording Service | Backend 1 | 🟡 | W5-D3 | W5-D5 | 3d | Meet Service | ⬜ TODO |
| WebRTC Room (Web) | Frontend | 🔴 | W5-D2 | W5-D5 | 4d | Room API | ⬜ TODO |
| Live Class Schedule UI | Frontend | 🟡 | W5-D1 | W5-D3 | 3d | Meet API | ⬜ TODO |
| WebRTC Room (Mobile) | Mobile | 🔴 | W5-D2 | W5-D5 | 4d | Room API | ⬜ TODO |

---

## Week 6: Lecturer & Staff Tools

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Assignment Service | Backend 1 | 🟡 | W6-D1 | W6-D3 | 3d | - | ⬜ TODO |
| Notification Service | Backend 2 | 🟡 | W6-D1 | W6-D3 | 3d | - | ⬜ TODO |
| Lecturer Dashboard | Frontend | 🟡 | W6-D2 | W6-D4 | 3d | Assignment API | ⬜ TODO |
| Staff Dashboard | Frontend | 🟡 | W6-D2 | W6-D5 | 4d | Multiple APIs | ⬜ TODO |
| Push Notifications (Mobile) | Mobile | 🟡 | W6-D2 | W6-D4 | 3d | Notification API | ⬜ TODO |
| Assignment Submission (Mobile) | Mobile | 🟢 | W6-D3 | W6-D5 | 3d | Assignment API | ⬜ TODO |

---

## Week 7: AI Integration & Admin

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Cortex Service (FastMCP) | Backend 1 | 🟡 | W7-D1 | W7-D4 | 4d | - | ⬜ TODO |
| Sensei Agent (Q&A) | Backend 1 | 🟡 | W7-D2 | W7-D5 | 4d | Cortex Service | ⬜ TODO |
| AI Chat UI (Web) | Frontend | 🟡 | W7-D3 | W7-D5 | 3d | Sensei API | ⬜ TODO |
| Admin Dashboard | Frontend | 🟡 | W7-D1 | W7-D4 | 4d | Multiple APIs | ⬜ TODO |
| AI Chat (Mobile) | Mobile | 🟡 | W7-D3 | W7-D5 | 3d | Sensei API | ⬜ TODO |
| My Folders (Mobile) | Mobile | 🟢 | W7-D1 | W7-D3 | 3d | Storage API | ⬜ TODO |

---

## Week 8: Integration Testing

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| E2E Test Suite Setup | All | 🔴 | W8-D1 | W8-D2 | 2d | All Features | ⬜ TODO |
| Backend API Testing | Backend Team | 🔴 | W8-D1 | W8-D4 | 4d | - | ⬜ TODO |
| Web E2E Testing | Frontend | 🔴 | W8-D2 | W8-D5 | 4d | Backend Tests | ⬜ TODO |
| Mobile E2E Testing | Mobile | 🔴 | W8-D2 | W8-D5 | 4d | Backend Tests | ⬜ TODO |
| Performance Testing | Backend Lead | 🟡 | W8-D3 | W8-D5 | 3d | E2E Tests | ⬜ TODO |
| Security Audit | All | 🟡 | W8-D3 | W8-D5 | 3d | - | ⬜ TODO |

---

## Week 9: UAT & Bug Fixing

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| UAT Test Cases | All | 🔴 | W9-D1 | W9-D2 | 2d | - | ⬜ TODO |
| UAT Execution | All | 🔴 | W9-D2 | W9-D4 | 3d | Test Cases | ⬜ TODO |
| Critical Bug Fixes | All | 🔴 | W9-D3 | W9-D5 | 3d | UAT Results | ⬜ TODO |
| UI/UX Refinement | Frontend/Mobile | 🟡 | W9-D1 | W9-D5 | 5d | - | ⬜ TODO |
| Load Testing (WebRTC) | Backend Team | 🟡 | W9-D2 | W9-D4 | 3d | - | ⬜ TODO |

---

## Week 10: Deployment & Documentation

| Task | Owner | Priority | Start | End | Duration | Dependencies | Status |
|------|-------|----------|-------|-----|----------|--------------|--------|
| Production Deployment | Backend Lead | 🔴 | W10-D1 | W10-D3 | 3d | All Tests Pass | ⬜ TODO |
| Web App Deployment | Frontend | 🔴 | W10-D1 | W10-D2 | 2d | - | ⬜ TODO |
| Mobile App Build | Mobile | 🔴 | W10-D1 | W10-D2 | 2d | - | ⬜ TODO |
| System Design Doc | All | 🔴 | W10-D1 | W10-D4 | 4d | - | ⬜ TODO |
| User Manuals | All | 🔴 | W10-D2 | W10-D4 | 3d | - | ⬜ TODO |
| Demo Preparation | All | 🔴 | W10-D3 | W10-D5 | 3d | Deployment | ⬜ TODO |

---

## 🎯 Critical Path Analysis

**Critical Path Tasks** (Any delay affects final deadline):

```
W1: Architecture → DB Schema → API Contract
  ↓
W2: Identity Service → Auth Pages
  ↓
W3: Video API → Video Player → Payment
  ↓
W4: Flashcards → Exams
  ↓
W5: Meet Service → WebRTC Room
  ↓
W8: E2E Testing
  ↓
W9: UAT → Bug Fixes
  ↓
W10: Deployment → Documentation
```

**Total Critical Path Duration:** ~45 days (9 weeks)  
**Buffer:** 1 week for unexpected issues

---

## 📊 Resource Allocation Chart

```
Member 1 (Backend Lead):
W1-2: [████████] Infrastructure & Identity
W3-4: [████████] Payment & Flashcards
W5-6: [████████] Recording & Assignments
W7:   [████████] Cortex/AI
W8-10:[████████] Testing & Deploy

Member 2 (Backend Dev):
W1-2: [████████] Infrastructure & LMS
W3-4: [████████] Video & Assessment
W5-6: [████████] Meet/WebRTC & Notifications
W7:   [████████] Support & Polish
W8-10:[████████] Testing & Deploy

Member 3 (Frontend):
W1-2: [████████] Setup & Auth UI
W3-4: [████████] Video & Payment UI
W5-6: [████████] WebRTC & Dashboards
W7:   [████████] AI Chat & Admin
W8-10:[████████] Testing & Deploy

Member 4 (Mobile):
W1-2: [████████] Setup & Auth
W3-4: [████████] Video & Flashcards
W5-6: [████████] WebRTC & Notifications
W7:   [████████] AI & Polish
W8-10:[████████] Testing & Deploy
```

---

## ⚠️ Risk Timeline

| Week | Risk | Mitigation | Owner |
|------|------|------------|-------|
| W1-2 | Architecture delays | Start coding in parallel | Backend Lead |
| W3 | VNPay integration issues | Use sandbox early | Backend 1 |
| W5 | WebRTC complexity | Allocate extra time | Backend 2 |
| W7 | AI API rate limits | Implement caching | Backend 1 |
| W8-9 | Major bugs found | Buffer week available | All |

---

## 📈 Progress Tracking

**Update this section weekly:**

| Week | Planned % | Actual % | Status | Notes |
|------|-----------|----------|--------|-------|
| W1 | 10% | - | ⬜ | - |
| W2 | 20% | - | ⬜ | - |
| W3 | 30% | - | ⬜ | - |
| W4 | 40% | - | ⬜ | - |
| W5 | 50% | - | ⬜ | - |
| W6 | 60% | - | ⬜ | - |
| W7 | 70% | - | ⬜ | - |
| W8 | 80% | - | ⬜ | - |
| W9 | 90% | - | ⬜ | - |
| W10 | 100% | - | ⬜ | - |

---

## 🎯 Milestone Checklist

- [ ] **W2 End:** Authentication working (Web + Mobile)
- [ ] **W4 End:** Video learning + Payment functional
- [ ] **W6 End:** Live WebRTC classes working
- [ ] **W7 End:** All core features integrated
- [ ] **W9 End:** System tested & stable
- [ ] **W10 End:** Deployed & documented

---

## 💡 How to Use This Gantt Chart

1. **Weekly Review:** Update status every Friday
2. **Daily Check:** Reference during standup for dependencies
3. **Risk Management:** Monitor critical path tasks closely
4. **Adjust:** Re-plan if tasks take longer than expected
5. **Communicate:** Share updates with team & supervisor

---

**Last Updated:** 2026-01-02  
**Next Review:** End of Week 1
