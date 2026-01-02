---
stepsCompleted: [1, 2, 3, 4, 5, 6]
inputDocuments:
  - "_bmad-output/planning-artifacts/prd.md"
  - "bmad/docs/index.md"
  - "bmad/docs/project-overview.md"
  - "bmad/docs/source-tree-analysis.md"
  - "bmad/docs/data-models-server.md"
  - "bmad/docs/api-contracts-server.md"
  - "bmad/docs/integration-architecture.md"
  - "bmad/docs/project-scan-report.json"
workflowType: 'ux-design'
lastStep: 6
---

# UX Design Specification - torii-nihongo

**Author:** Tienh
**Date:** 2026-01-02

---

## Executive Summary

### Project Vision

Torii Nihongo is a **unified Japanese language learning platform** that eliminates the fragmented experience currently plaguing Vietnamese learners preparing for JLPT certification. The platform uniquely combines self-paced video learning, live interactive classes with real-time AI feedback, and intelligent spaced-repetition flashcards into a single cohesive ecosystem.

**What Makes This Special:**
- **Real-time AI Teaching Assistant**: Multi-agent AI system (Sensei, Assessment, Analytics) provides sub-3-second feedback during live classes, including real-time Kanji handwriting correction on collaborative whiteboards
- **Hybrid Learning Model**: Seamlessly blends VOD courses (learn anytime) with scheduled live WebRTC classes (learn together), allowing flipped classroom pedagogy
- **Failure Recovery as a Feature**: When students fail JLPT exams, the system provides detailed weakness analysis and personalized remediation plans, turning failure into a growth opportunity
- **Cross-Platform Continuity**: Learn on web, continue on mobile during commute, resume on web at home - with full offline capability for metro/bus learning

**Business Context**: This is a capstone project for a real Japanese learning center currently managing 200+ students across fragmented systems (separate platforms for VOD, quizzes, live classes). Success means replacing 3-4 disconnected tools with one unified experience.

### Target Users

**Primary User Archetypes:**

1. **Minh - The Commuter Learner** (Mobile-First)
   - 24-year-old software developer, 2-hour daily metro commute
   - Self-motivated but needs structure and progress tracking
   - **Key Need**: Offline learning capability, progress sync, AI-powered weakness identification
   - **Success Metric**: Can study 4 hours/day during commute without internet

2. **Cô Hana - The Overwhelmed Lecturer** (Web-Centric)
   - 32-year-old instructor teaching 6 classes/week (15-20 students each)
   - Loves teaching but drowns in administrative work (attendance, grading)
   - **Key Need**: AI-assisted grading, automated attendance, engagement insights
   - **Success Metric**: Reduces grading time by 50%, leaves work 2 hours earlier

3. **Anh Tuan - The Operations Manager** (Command Center)
   - Manages 50+ concurrent live classes, handles technical emergencies
   - Currently uses Excel + Google Sheets + WhatsApp (chaos)
   - **Key Need**: Real-time monitoring dashboard, emergency re-assignment tools
   - **Success Metric**: Resolves technical issues in <3 minutes, prevents scheduling conflicts

4. **Chi Mai - The Strategic Director** (Analytics & Compliance)
   - Needs data-driven insights for business decisions
   - Must comply with Ministry of Education and GDPR requirements
   - **Key Need**: Strategic KPIs, financial reconciliation, audit trails
   - **Success Metric**: Makes decisions based on real-time data, not outdated Excel reports

**User Skill Level**: Intermediate (per config) - users are tech-comfortable but not developers. Vietnamese students familiar with smartphones and web apps.

**Language Context**: Primary UI in Vietnamese (per config: `communication_language: English` for documentation, but product UI should be Vietnamese for target market).

### Key Design Challenges

**1. Multi-Role Complexity Without Cognitive Overload**
- **Challenge**: Four distinct user types (Learner, Lecturer, Staff, Admin) with vastly different mental models and workflows
- **UX Approach**: Role-based navigation with progressive disclosure - show only what's relevant to each role, hide complexity until needed
- **Example**: Learners never see "Command Center" features; Staff never see "My Learning Progress"

**2. Real-Time Collaboration at Scale (50+ Concurrent Classes)**
- **Challenge**: Live classes with 15-20 students using whiteboard, chat, screen sharing simultaneously while maintaining <100ms sync latency
- **UX Approach**: Optimistic UI updates with conflict resolution, graceful degradation when network is poor, clear visual feedback for connection quality
- **Critical**: Design for failure scenarios (lecturer drops, student loses connection mid-class)

**3. Cross-Platform Consistency with Platform-Specific Strengths**
- **Challenge**: Web (Next.js) and Mobile (Flutter) must feel like "one product" while leveraging each platform's strengths
- **UX Approach**: 
  - **Mobile-First for Learners**: Offline-first architecture, downloadable lessons, background sync
  - **Web-First for Lecturers/Staff**: Rich dashboards, multi-window workflows, keyboard shortcuts
  - **Shared Design Language**: Same colors, typography, interaction patterns across platforms

**4. AI Transparency & Trust Building**
- **Challenge**: AI grading, handwriting feedback, and JLPT predictions must be trustworthy; mistakes can damage student confidence
- **UX Approach**: 
  - Always show AI confidence levels ("85% confident this is correct")
  - Allow lecturer override with audit trail
  - Explain AI reasoning ("Marked incorrect because particle should be に not で")
  - Graceful error handling ("AI suggestion - please review")

### Design Opportunities

**1. Gamification as Intrinsic Motivation (Not Extrinsic Rewards)**
- **Opportunity**: Create a progression system that taps into mastery and autonomy, not just points
- **UX Strategy**: 
  - Streak system shows consistency, not competition
  - XP tied to actual learning outcomes (quiz scores, lesson completion), not just "logging in"
  - Badges for meaningful achievements ("Completed 50 consecutive days", "Mastered N3 Grammar")
  - Leaderboards optional and private by default (respect cultural context - Vietnamese learners may prefer private progress)

**2. Proactive Learning Coach (Analytics Agent as Companion)**
- **Opportunity**: Position AI as a personal tutor who knows your weaknesses and adapts your path
- **UX Strategy**:
  - Daily personalized recommendations: "Today's focus: Reading Comprehension (your weak spot)"
  - JLPT score predictions with confidence intervals: "Predicted score: 125-135/180 (70% confidence)"
  - Gentle nudges, not nagging: "You're 3 days away from losing your streak - 10 minutes today?"
  - Celebrate small wins: "Your Grammar score improved 15% this month! 🎉"

**3. Failure Recovery as Competitive Differentiator**
- **Opportunity**: Most EdTech platforms abandon students who fail exams. Torii Nihongo doubles down on support.
- **UX Strategy**:
  - Empathetic messaging: "We're sorry you didn't pass - but we're here to help you succeed"
  - Detailed failure analysis: Visual breakdown of 5-pillar scores with specific weaknesses highlighted
  - Personalized remediation plan: "Phase 1: Vocabulary Intensive (50 words/day for 4 weeks)"
  - Community support: "Join 'N3 Retake Warriors' study group (15 students like you)"
  - **Emotional Design**: Turn failure into a data point for growth, not shame

**4. Lecturer Empowerment Through AI Augmentation**
- **Opportunity**: Position AI as a "teaching assistant" that amplifies lecturer expertise, not replaces it
- **UX Strategy**:
  - AI draft grading shows suggestions, lecturer has final say
  - Engagement heatmap highlights disengaged students so lecturer can intervene
  - AI-generated class summaries save post-class admin time
  - Mentorship system: New lecturers learn from recorded classes of master teachers
  - **Key Message**: "AI handles the tedious work so you can focus on teaching"

---

## Core User Experience

### Defining Experience

Torii Nihongo delivers **role-optimized experiences** tailored to four distinct user types, each with their own core interaction loop:

**Learner Experience: "Learn → Practice → Progress → Repeat"**
The learner's core loop is a continuous cycle of consuming content (video lessons, live classes), practicing through active recall (flashcards, quizzes), seeing measurable progress (5-pillar JLPT analytics), and repeating with AI-recommended focus areas. The experience is designed to work seamlessly across devices and connectivity states - learn on mobile during commute, continue on web at home.

**Lecturer Experience: "Prepare → Teach → Assess → Improve"**
Lecturers focus on conducting engaging live classes with minimal administrative burden. The system auto-handles attendance, AI pre-grades assignments, and engagement heatmaps show which students need attention. The core value is "teach more, admin less."

**Operations Experience: "Monitor → Detect → Respond → Resolve"**
Operations staff manage 50+ concurrent live classes through a real-time command center. The system proactively detects issues (scheduling conflicts, technical problems) and provides instant resolution tools (emergency re-assignment, support chat).

**Admin Experience: "Analyze → Decide → Execute → Validate"**
Admins make strategic decisions based on real-time KPIs, compliance dashboards, and financial reconciliation. The core value is "data-driven decisions, not gut feelings."

### Platform Strategy

**Multi-Platform Architecture with Role-Specific Optimization:**

**Mobile (Flutter) - Learner-Centric:**
- **Primary Use Case**: Offline learning during commute (2-4 hours/day without internet)
- **Core Capabilities**: 
  - Download entire lesson modules for offline viewing
  - Offline flashcard practice with SRS algorithm
  - Background sync when WiFi reconnects
  - Push notifications for class reminders and assignment feedback
- **Interaction Model**: Touch-first (swipe flashcards, tap to play, pinch to zoom)
- **Success Metric**: 4 hours of productive learning without internet connection

**Web (Next.js) - Learner Discovery & Live Classes:**
- **Primary Use Case**: Course discovery, enrollment, live class participation
- **Core Capabilities**:
  - Rich course catalog with filtering (JLPT level, instructor, schedule)
  - WebRTC live classes (desktop preferred for larger screen)
  - VNPay payment integration with gifting system
  - Progress dashboards with 5-pillar analytics
- **Interaction Model**: Mouse/keyboard with responsive touch support
- **Success Metric**: Complete enrollment in <10 minutes, join live class in 1 click

**Web (React/Vite) - Lecturer/Staff/Admin Dashboards:**
- **Primary Use Case**: Power user workflows (grading, scheduling, analytics)
- **Core Capabilities**:
  - Multi-window workflows (grade assignments while monitoring live class)
  - Keyboard shortcuts for efficiency (Ctrl+G to grade, Ctrl+S to save)
  - Real-time data tables with filtering and export
  - Command center for operations monitoring
- **Interaction Model**: Desktop-first with extensive keyboard navigation
- **Success Metric**: Complete grading 50% faster, resolve issues in <3 minutes

**Platform Synchronization:**
- **Progress Sync**: Flashcard reviews, video progress, quiz scores sync bidirectionally (mobile ↔ web)
- **Conflict Resolution**: Last-write-wins for progress data, server-authoritative for enrollment/payments
- **Offline Queue**: Mobile queues actions (mark lesson complete, submit quiz) and syncs when online

### Effortless Interactions

**1. Automatic Attendance Tracking**
- **What**: System auto-detects who joined WebRTC room and updates attendance in real-time
- **Why Effortless**: Lecturers never manually take roll call (saves 5 minutes per class)
- **Technical**: WebRTC participant events trigger attendance updates via NATS

**2. One-Click Class Join**
- **What**: Single "Join Class" button instantly enters live session with pre-configured A/V
- **Why Effortless**: No fumbling with links, waiting rooms, or audio setup
- **Technical**: LiveKit token pre-generated, A/V permissions requested on first join and cached

**3. Offline-to-Online Sync**
- **What**: All offline activity (videos, flashcards, quizzes) auto-syncs when WiFi reconnects
- **Why Effortless**: 4 hours of metro study seamlessly continues at home on web
- **Technical**: Drift (SQLite) local DB queues changes, background sync service uploads when online

**4. AI Pre-Grading with Lecturer Override**
- **What**: AI grades all assignments, highlights errors, lecturer reviews and approves in 45 minutes (vs. 3 hours manual)
- **Why Effortless**: Lecturer focuses on edge cases and personal feedback, not repetitive error marking
- **Technical**: Assessment Agent analyzes submissions, generates draft grades with confidence scores

**5. Atomic Seat Reservation**
- **What**: Payment and seat reservation happen in single atomic transaction (distributed lock via NATS)
- **Why Effortless**: Zero "sorry, class is full" after payment (prevents race conditions)
- **Technical**: 15-minute distributed lock during checkout, atomic enrollment on payment success

### Critical Success Moments

**First-Time Learner Success (10-Minute Onboarding):**
- **Moment**: Within 10 minutes of VNPay payment, learner is watching first video lesson
- **Why Critical**: Slow onboarding creates buyer's remorse; instant access builds trust
- **UX Requirement**: Skip email verification, instant enrollment on payment webhook, pre-load first lesson

**Live Class "Aha!" Moment (Real-Time AI Feedback):**
- **Moment**: Student writes Kanji on whiteboard, AI gives instant stroke order feedback (<100ms)
- **Why Critical**: This is the differentiator - no YouTube video or static course can do this
- **UX Requirement**: WebRTC whiteboard with computer vision AI, visual feedback overlay, <100ms latency

**Lecturer Relief Moment (AI Grading Revolution):**
- **Moment**: Seeing AI pre-grade 60 assignments in 3 seconds vs. usual 3-hour manual grading
- **Why Critical**: This is when lecturers realize "I can't teach without this anymore"
- **UX Requirement**: >85% AI accuracy, easy override workflow, audit trail for grade changes

**Operations "Crisis Averted" Moment (Emergency Re-Assignment):**
- **Moment**: Lecturer calls in sick 30 minutes before class, backup assigned in 3 minutes via system
- **Why Critical**: Prevents student disappointment and center reputation damage
- **UX Requirement**: <5-click emergency workflow, automated notifications to backup lecturer and students

**Failure Recovery "Hope Restored" Moment (JLPT Retake Support):**
- **Moment**: Student fails JLPT, logs in next day, sees empathetic message + personalized remediation plan + community invite
- **Why Critical**: Most EdTech abandons failed students; Torii Nihongo doubles down on support
- **UX Requirement**: Empathetic messaging, detailed weakness analysis, actionable 12-week plan, peer support group

### Experience Principles

**1. "Invisible Technology, Visible Progress"**
- **Principle**: Technology should fade into the background; learning progress should be front and center
- **Application**: Auto-save, auto-sync, auto-attendance - users never think about "the system"
- **Example**: Learners see "You've completed 65% of N3 Grammar" not "Sync successful"
- **Anti-Pattern**: Showing technical details ("WebSocket connected") instead of learning outcomes

**2. "AI as Amplifier, Not Replacement"**
- **Principle**: AI enhances human expertise (lecturers, learners) but never replaces judgment
- **Application**: AI suggests, humans decide; always show confidence levels and allow overrides
- **Example**: "AI suggests 7/10 (85% confident) - Review and approve"
- **Anti-Pattern**: AI makes final decisions without human review or explanation

**3. "Fail Fast, Recover Faster"**
- **Principle**: Anticipate failures (network drops, payment issues, lecturer no-shows) and have instant recovery paths
- **Application**: Graceful degradation, clear error messages, proactive support
- **Example**: "Connection unstable - switching to low-bandwidth mode (audio-only)"
- **Anti-Pattern**: Generic error messages ("Something went wrong") with no recovery path

**4. "Role-Specific, Not Role-Restricted"**
- **Principle**: Each user type sees their optimal workflow, but can access other views when needed
- **Application**: Progressive disclosure based on role, not hard permission walls
- **Example**: Learner dashboard shows learning progress; can view "Become a Lecturer" if interested
- **Anti-Pattern**: Hard-coded role restrictions that prevent legitimate cross-role exploration

**5. "Offline-First for Learners, Real-Time for Collaboration"**
- **Principle**: Learners should never be blocked by connectivity; live collaboration demands real-time sync
- **Application**: Mobile app works offline for solo learning; live classes require stable connection with fallback
- **Example**: Download lessons for offline study, but live whiteboard requires internet with audio-only fallback
- **Anti-Pattern**: Requiring internet for all features, or allowing offline mode for real-time collaboration

---

## Desired Emotional Response

### Primary Emotional Goals

**For Learners: "Empowered Progress"**
Learners should feel in control of their learning journey with visible, measurable improvement. The system provides constant feedback and validation that their effort is translating into real skill gains. Secondary emotion: "Supported, Not Alone" - AI Sensei and community features make learners feel they have a personal tutor and peer support network, not isolated self-study.

**For Lecturers: "Liberated to Teach"**
Lecturers should feel free from administrative burden to focus on what they love - teaching and connecting with students. The system handles tedious tasks (attendance, grading, scheduling) so lecturers can invest energy in personalized instruction. Secondary emotion: "Augmented Expertise" - AI amplifies their teaching power without replacing their judgment.

**For Operations Staff: "In Command"**
Operations staff should feel they have real-time visibility and instant resolution tools, creating a sense of control even when managing 50+ concurrent classes. Secondary emotion: "Proactive, Not Reactive" - the system detects issues before they become crises, allowing staff to prevent problems rather than constantly putting out fires.

**For Admins: "Strategic Clarity"**
Admins should feel confident making data-driven decisions with real-time insights, not outdated gut feelings. Secondary emotion: "Compliant and Secure" - peace of mind from audit trails, GDPR compliance, and financial reconciliation.

### Emotional Journey Mapping

**Learner Emotional Arc:**
1. **Discovery** (Anxiety  Hope): "Can I really pass JLPT in 4 months?"  "This looks structured and comprehensive"
2. **Onboarding** (Uncertainty  Confidence): "Will this work for me?"  "I'm watching my first lesson in 10 minutes!"
3. **Daily Use** (Routine  Engagement): Offline metro study feels productive, not wasted time
4. **Progress Tracking** (Doubt  Validation): "Am I improving?"  "My Grammar score went from 68% to 81%!"
5. **Live Class** (Nervous  Excited): "Will I embarrass myself?"  "The AI just corrected my Kanji in real-time!"
6. **Failure Recovery** (Devastation  Renewed Hope): "I failed the exam"  "I have a personalized plan and a community to help me succeed"

**Lecturer Emotional Arc:**
1. **Adoption** (Skepticism  Openness): "Another EdTech tool to learn?"  "This might actually help me"
2. **First Class** (Nervous  Relieved): "Will this work smoothly?"  "Attendance is automatic - I can focus on teaching!"
3. **Grading** (Dread  Amazement): "3 hours of grading ahead"  "AI pre-graded everything in 3 seconds"
4. **Ongoing** (Energized  Fulfilled): "I have time to actually teach"  "I'm mentoring new lecturers now"

**Operations Emotional Arc:**
1. **Monitoring** (Overwhelmed  In Control): "50 classes to track manually"  "Dashboard shows everything at a glance"
2. **Crisis** (Panic  Calm): "Lecturer called in sick!"  "Backup assigned in 3 minutes via system"
3. **Daily** (Reactive  Proactive): "Constantly putting out fires"  "Preventing fires before they start"

### Micro-Emotions

**Confidence vs. Confusion:**
- **Design For**: Confidence through clear progress indicators, AI explanations with reasoning, and predictable navigation patterns
- **Avoid**: Confusion from unclear AI decisions, hidden features, or inconsistent UI
- **Implementation**: "AI suggests 7/10 (85% confident) - Review and approve" builds trust through transparency

**Trust vs. Skepticism:**
- **Design For**: Trust through transparency (AI confidence levels), audit trails, and lecturer override capabilities
- **Avoid**: Skepticism from unexplained AI decisions or black-box grading without human review
- **Implementation**: Show AI reasoning: "Marked incorrect because particle should be ? not ?"

**Accomplishment vs. Frustration:**
- **Design For**: Accomplishment through visible progress, streak celebrations, and milestone badges
- **Avoid**: Frustration from unclear goals, invisible progress, or punishing failures
- **Implementation**: "Your Grammar score improved 15% this month! " celebrates incremental progress

**Belonging vs. Isolation:**
- **Design For**: Belonging through community features (study groups), peer support, and shared progress
- **Avoid**: Isolation from purely solo learning without social elements
- **Implementation**: "Join 15 students like you in the N3 Retake Warriors study group"

**Calm vs. Anxiety:**
- **Design For**: Calm through graceful error handling, clear recovery paths, and proactive support
- **Avoid**: Anxiety from cryptic errors, data loss fears, or unclear system status
- **Implementation**: "Connection unstable - switching to low-bandwidth mode (audio-only)"

### Design Implications

**Empowered Progress  Progress Visualization:**
- **UX Approach**: 5-pillar JLPT analytics dashboard with trend lines showing improvement over time, not just static scores
- **Visual Design**: Color-coded progress bars (red < 60%, yellow 60-80%, green > 80%) with clear thresholds
- **Micro-interaction**: Animated progress bar fill when completing lessons, satisfying visual feedback

**Supported, Not Alone  AI Personality:**
- **UX Approach**: AI Sensei has a warm, encouraging tone that feels like a patient tutor, not a robotic system
- **Voice & Tone**: "Great job on that grammar quiz! Let's tackle particles next - I'll help you understand the nuances."
- **Visual Design**: AI avatar with friendly expressions that change based on context (encouraging, thoughtful, celebratory)

**Liberated to Teach  Time-Saving Indicators:**
- **UX Approach**: Explicitly show time saved: "AI pre-graded 60 assignments in 3 seconds (saved you 2h 57m)"
- **Visual Design**: Before/after comparison of grading time with clear metrics
- **Celebration**: Monthly summary: "You've saved 12 hours this month with AI grading - that's 1.5 extra days!"

**In Command  Real-Time Status Indicators:**
- **UX Approach**: Traffic light system (green/yellow/red) for class health with clear thresholds
- **Visual Design**: Live participant count, connection quality meters, engagement heatmaps
- **Proactive Alerts**: Warnings before issues become critical: "Class 3B connection quality degrading - 2 students at risk"

**Strategic Clarity  Data Storytelling:**
- **UX Approach**: Dashboards tell stories and provide actionable insights, not just display numbers
- **Visual Design**: "Retention dropped 3% this month - Analysis: Students not attending first live class within 7 days are 60% more likely to drop out"
- **Actionable Recommendations**: "Recommendation: Implement automated 5-day reminder calls for new enrollments"

### Emotional Design Principles

**1. "Celebrate Progress, Not Perfection"**
- **Principle**: Acknowledge every step forward, even small wins; treat failure as data for growth, not shame
- **Application**: Streak celebrations, progress notifications, empathetic failure recovery messaging
- **Example**: "You studied 5 days in a row! Keep it up! " vs. "You broke your streak" (negative framing)
- **Anti-Pattern**: Punishing failures, only celebrating perfect scores, or making users feel inadequate

**2. "Transparency Builds Trust"**
- **Principle**: Always explain AI reasoning, show confidence levels, and allow human override with audit trails
- **Application**: AI suggestions with explanations, grade dispute workflows, lecturer final say
- **Example**: "AI marked this incorrect (85% confident) because the particle should be ? not ? in this context" vs. just showing a red X
- **Anti-Pattern**: Black-box AI decisions without explanation, no override mechanism, or hiding system logic

**3. "Anticipate Anxiety, Provide Calm"**
- **Principle**: Proactively address user fears (data loss, payment issues, connection drops) with clear communication
- **Application**: Auto-save indicators, graceful degradation messages, clear error recovery paths
- **Example**: "Your progress is saved automatically every 30 seconds" vs. relying on manual save without indication
- **Anti-Pattern**: Generic errors ("Something went wrong") without explanation or recovery path

**4. "Delight in the Details"**
- **Principle**: Micro-interactions and animations create moments of joy without being distracting or childish
- **Application**: Smooth transitions, satisfying button feedback, playful success animations
- **Example**: Flashcard flip animation with physics, progress bar fill with easing, confetti on milestone achievements
- **Anti-Pattern**: Over-animation that slows down power users, or animations that feel juvenile for adult learners

**5. "Empathy in Failure, Encouragement in Success"**
- **Principle**: When users fail (exam, quiz, streak), respond with empathy and actionable support; when they succeed, celebrate meaningfully
- **Application**: Failure recovery messaging, personalized remediation plans, community support invites
- **Example**: "We're sorry you didn't pass this time - but we're here to help you succeed. Here's your personalized plan..." vs. "You failed"
- **Anti-Pattern**: Abandoning failed users, making them feel ashamed, or generic "try again" messages without support

---

## UX Pattern Analysis & Inspiration

### Inspiring Products Analysis

Based on the EdTech domain, language learning context, and target market (Vietnamese users), we analyzed four inspiring products to extract transferable UX patterns:

**1. Duolingo - Gamified Language Learning**

**What They Do Well:**
- **Streak System**: Simple, visual streak counter creates daily habit formation without feeling punitive
- **Bite-Sized Lessons**: 5-10 minute lessons perfect for commute learning (matches "Minh" persona)
- **Progress Visualization**: Clear skill trees show what's completed, what's next, and what's locked
- **Gentle Nudges**: Push notifications feel encouraging, not nagging
- **Immediate Feedback**: Instant right/wrong feedback with explanations keeps learners engaged

**Core Problem Solved**: Making language learning feel like a game, not homework

**Onboarding Excellence**: 5-minute lesson before signup - users experience value before commitment

**Most Innovative Interaction**: Hearts system (limited lives) creates tension without being punishing

**Transferable Patterns**: Streak system, bite-sized content, immediate feedback, progress visualization

---

**2. Notion - Flexible Workspace for Power Users**

**What They Do Well:**
- **Progressive Disclosure**: Simple at first glance, powerful when you dig deeper
- **Keyboard Shortcuts**: Power users can navigate entirely via keyboard (Ctrl+K command palette)
- **Templates**: Pre-built templates reduce blank-page syndrome
- **Real-Time Collaboration**: Multiple users editing simultaneously with cursor presence indicators
- **Offline-First**: Works offline, syncs when online (critical for mobile learners)

**Core Problem Solved**: Flexible workspace that adapts to any workflow without overwhelming new users

**Navigation**: Sidebar + breadcrumbs + quick switcher - multiple ways to navigate

**Most Innovative Interaction**: Slash commands (/) for inline formatting - discoverable and efficient

**Transferable Patterns**: Progressive disclosure, keyboard shortcuts, offline-first architecture, real-time collaboration

---

**3. Zoom/Microsoft Teams - Live Collaboration at Scale**

**What They Do Well:**
- **One-Click Join**: Meeting links work instantly, no account required for attendees
- **Connection Quality Indicators**: Visual feedback (green/yellow/red) for audio/video quality
- **Graceful Degradation**: Automatically reduces video quality when bandwidth is poor
- **Waiting Room**: Host controls when participants join (security + preparation time)
- **Screen Sharing**: Seamless transition between camera and screen share

**Core Problem Solved**: Making remote meetings feel almost as natural as in-person

**Onboarding**: Test audio/video before joining - prevents embarrassing technical issues

**Most Innovative Interaction**: Gallery view with active speaker detection

**Transferable Patterns**: One-click join, connection quality indicators, graceful degradation, waiting room

---

**4. Coursera - Structured Online Learning**

**What They Do Well:**
- **Progress Tracking**: Clear percentage completion for each course module
- **Deadline Reminders**: Flexible deadlines with gentle reminders (not rigid)
- **Peer Review**: Students grade each other's work (scales grading burden)
- **Discussion Forums**: Async community support for questions
- **Certificates**: Tangible proof of completion motivates learners

**Core Problem Solved**: Making online education feel structured and credible

**Navigation**: Course syllabus sidebar always visible - learners know where they are

**Most Innovative Interaction**: Video playback speed control (1.25x, 1.5x, 2x) - respects learner's time

**Transferable Patterns**: Progress tracking, flexible deadlines, discussion forums, certificates

### Transferable UX Patterns

**Navigation Patterns:**

1. **Sidebar + Breadcrumbs (Notion-style)**
   - **Pattern**: Persistent sidebar for main navigation, breadcrumbs for context
   - **Applies To**: Lecturer/Staff dashboards (complex multi-level navigation)
   - **Why**: Power users need quick access to deep features without getting lost

2. **Tab Bar + Floating Action Button (Mobile)**
   - **Pattern**: Bottom tab bar for main sections, FAB for primary action
   - **Applies To**: Mobile learner app (Course, Flashcards, Progress, Profile + "Join Live Class" FAB)
   - **Why**: Thumb-friendly navigation on mobile, primary action always accessible

**Interaction Patterns:**

1. **Progressive Disclosure (Notion-style)**
   - **Pattern**: Show simple view by default, reveal advanced features on demand
   - **Applies To**: All dashboards (Learner, Lecturer, Staff, Admin)
   - **Why**: Prevents cognitive overload for new users while empowering power users
   - **Example**: Learner dashboard shows "My Courses" by default, "Advanced Analytics" behind a toggle

2. **Optimistic UI Updates (Notion-style)**
   - **Pattern**: Update UI immediately, sync to server in background
   - **Applies To**: Flashcard reviews, lesson completion, quiz submissions
   - **Why**: Feels instant even on slow connections, reduces perceived latency
   - **Example**: Mark lesson complete  UI updates instantly  sync happens in background

3. **Real-Time Presence Indicators (Zoom-style)**
   - **Pattern**: Show who's online, who's typing, who's drawing on whiteboard
   - **Applies To**: Live classes (WebRTC collaboration)
   - **Why**: Creates sense of "being together" in virtual classroom
   - **Example**: Show lecturer's cursor on whiteboard, typing indicators in chat

**Visual Patterns:**

1. **Color-Coded Progress (Duolingo-style)**
   - **Pattern**: Red (< 60%), Yellow (60-80%), Green (> 80%) for skill levels
   - **Applies To**: 5-pillar JLPT analytics dashboard
   - **Why**: Instant visual feedback on strengths/weaknesses
   - **Example**: Grammar 81% (green), Reading 55% (red) - immediately shows focus area

2. **Streak Visualization (Duolingo-style)**
   - **Pattern**: Flame icon + number + calendar heatmap
   - **Applies To**: Learner daily study habit tracking
   - **Why**: Creates intrinsic motivation through visible consistency
   - **Example**: " 15 day streak - Don't break it!"

3. **Connection Quality Indicators (Zoom-style)**
   - **Pattern**: Traffic light colors (green/yellow/red) for network status
   - **Applies To**: Live class participant list, operations command center
   - **Why**: Proactive visibility into technical issues before they become critical
   - **Example**: Student name with red dot = poor connection, lecturer can intervene

### Anti-Patterns to Avoid

**1. Overwhelming Onboarding (Common EdTech Mistake)**
- **Anti-Pattern**: 20-minute tutorial before first use, forcing users to watch all features
- **Why Avoid**: Users want to experience value immediately, not sit through lectures
- **Your Approach**: 10-minute onboarding - payment  first video lesson (immediate value)
- **Example**: Don't force learners to complete "platform tour" before accessing content

**2. Punitive Gamification (Duolingo's Mistake)**
- **Anti-Pattern**: "You lost your 50-day streak!" with no recovery option (feels punishing)
- **Why Avoid**: Vietnamese learners may prefer private progress over public shaming
- **Your Approach**: Streak freeze option, empathetic messaging, private leaderboards by default
- **Example**: "Life happens - use a streak freeze to protect your progress"

**3. Black-Box AI Decisions (Common AI Mistake)**
- **Anti-Pattern**: AI grades assignment with no explanation, no override option
- **Why Avoid**: Breaks trust, especially when AI makes mistakes (which it will)
- **Your Approach**: Always show AI confidence + reasoning + lecturer override
- **Example**: "AI suggests 7/10 (85% confident) - Marked incorrect because particle should be ? not ?"

**4. Generic Error Messages (Common Web Mistake)**
- **Anti-Pattern**: "Something went wrong. Please try again." with no context or recovery path
- **Why Avoid**: Creates anxiety and frustration, especially during critical moments (payment, live class join)
- **Your Approach**: Specific errors with clear recovery steps
- **Example**: "Payment failed: Card declined. Try a different card or contact your bank."

**5. Desktop-Only Live Classes (Zoom's Limitation)**
- **Anti-Pattern**: Mobile app is second-class citizen for live collaboration
- **Why Avoid**: Vietnamese learners may only have smartphones, not laptops
- **Your Approach**: Mobile-optimized live class experience (touch-friendly whiteboard, simplified UI)
- **Example**: Whiteboard works with finger drawing on mobile, not just mouse on desktop

### Design Inspiration Strategy

**What to Adopt Directly:**

1. **Duolingo's Streak System**
   - **Why**: Proven to create daily habit formation for language learners
   - **How**: Flame icon + number + calendar heatmap on learner dashboard
   - **Adaptation**: Add "streak freeze" option (Vietnamese cultural preference for saving face)

2. **Notion's Offline-First Architecture**
   - **Why**: Critical for "Minh" persona (2-hour metro commute without internet)
   - **How**: Local SQLite DB (Drift) + background sync when online
   - **Adaptation**: Show sync status clearly ("Last synced 2 minutes ago")

3. **Zoom's Connection Quality Indicators**
   - **Why**: Essential for managing 50+ concurrent live classes
   - **How**: Green/yellow/red dots next to participant names
   - **Adaptation**: Add proactive alerts for operations staff ("Class 3B connection degrading")

**What to Adapt for Your Context:**

1. **Duolingo's Playful Tone  Professional Encouragement**
   - **Why**: Users are adult learners preparing for serious JLPT exam, not kids
   - **How**: Keep encouragement, remove childish elements (no cartoon mascots)
   - **Example**: "Great progress this week!" instead of "Duo is proud of you!"

2. **Coursera's Peer Review  AI Pre-Grading + Lecturer Review**
   - **Why**: You have AI capability that Coursera lacks
   - **How**: AI grades first (instant feedback), lecturer reviews (quality assurance)
   - **Example**: "AI pre-graded 60 assignments in 3 seconds - review and approve"

3. **Zoom's Waiting Room  Lecturer Preparation Mode**
   - **Why**: Lecturers need time to load materials before students flood in
   - **How**: "Start Class" button for lecturer, students see "Class starting soon..."
   - **Example**: Lecturer joins 5 minutes early, loads slides, then admits students

**What to Avoid Completely:**

1. **Duolingo's Hearts System (Limited Lives)**
   - **Why**: Creates anxiety for JLPT learners who need to practice extensively
   - **Your Approach**: Unlimited quiz attempts, focus on mastery not rationing
   - **Example**: "Try again - you'll get it!" instead of "Out of hearts, come back tomorrow"

2. **Zoom's Lack of Educational Features**
   - **Why**: Generic video conferencing doesn't support pedagogy
   - **Your Approach**: Add whiteboard, AI feedback, engagement heatmap, attendance tracking
   - **Example**: Real-time Kanji stroke order correction (Zoom can't do this)

3. **Coursera's Rigid Deadlines**
   - **Why**: Vietnamese learners juggle work/study, need flexibility
   - **Your Approach**: Flexible deadlines with gentle reminders, not penalties
   - **Example**: "Suggested completion: Jan 15" instead of "Hard deadline: Jan 15 (late penalty)"

---

## Design System Foundation

### Design System Choice

**Web Platforms (Next.js + React/Vite): shadcn/ui**
**Mobile Platform (Flutter): Flutter Material 3**
**Shared: Design Token System for Cross-Platform Consistency**

This hybrid approach leverages the best design system for each platform while maintaining visual consistency through shared design tokens.

### Rationale for Selection

**Why shadcn/ui for Web:**

1. **Copy-Paste, Not NPM Dependency**
   - Components are copied into your codebase, giving you full ownership
   - No version lock-in or breaking changes from external packages
   - Perfect for capstone project where you need to demonstrate "your code"

2. **Built on Radix UI Primitives**
   - Accessibility built-in (WCAG 2.1 compliant)
   - Unstyled primitives you can customize completely
   - Handles complex interactions (dropdowns, modals, tooltips) out of the box

3. **Tailwind CSS Integration**
   - Utility-first styling matches modern web development
   - Easy to customize colors, spacing, typography
   - Small bundle size (only includes CSS you actually use)

4. **TypeScript Native**
   - Type-safe components match your NestJS backend
   - Autocomplete and IntelliSense in VS Code
   - Catches errors at compile time

5. **Rapid Prototyping**
   - 40+ pre-built components (Button, Card, Dialog, Table, etc.)
   - Can build entire dashboard in days, not weeks
   - Responsive by default

**Why Flutter Material 3 for Mobile:**

1. **Native Flutter Integration**
   - Built into Flutter SDK, no external dependencies
   - Optimized performance for mobile
   - Follows platform conventions (iOS/Android)

2. **Theming System**
   - ColorScheme and ThemeData allow full customization
   - Can match web design tokens for consistency
   - Dark mode support built-in

3. **Rich Component Library**
   - 100+ widgets for common UI patterns
   - Handles touch interactions natively
   - Offline-first architecture support

**Why This Combination:**
- **Timeline**: 10-week capstone requires fast development
- **Team Skill**: Intermediate developers can learn quickly
- **Cross-Platform**: Shared design tokens ensure consistency
- **Flexibility**: Can customize to create unique brand identity
- **Production-Ready**: Both systems are battle-tested at scale

### Implementation Approach

**Phase 1: Design Tokens (Week 1)**
Define shared design tokens that work across web and mobile:

\\\	ypescript
// Design Tokens (shared across web and mobile)
const tokens = {
  colors: {
    primary: { 
      50: '#f0f9ff',   // Lightest
      100: '#e0f2fe',
      200: '#bae6fd',
      300: '#7dd3fc',
      400: '#38bdf8',
      500: '#3b82f6',  // Base
      600: '#2563eb',
      700: '#1d4ed8',
      800: '#1e40af',
      900: '#1e3a8a'   // Darkest
    },
    secondary: {
      500: '#a78bfa',  // Lavender
      900: '#6d28d9'   // Deep purple
    },
    accent: {
      500: '#f97316'   // Vibrant orange (streaks, achievements)
    },
    success: { 500: '#10b981' },
    warning: { 500: '#f59e0b' },
    error: { 500: '#ef4444' },
    neutral: { 
      50: '#f9fafb',
      100: '#f3f4f6',
      200: '#e5e7eb',
      300: '#d1d5db',
      400: '#9ca3af',
      500: '#6b7280',
      600: '#4b5563',
      700: '#374151',
      800: '#1f2937',
      900: '#111827'
    }
  },
  typography: {
    fontFamily: {
      sans: 'Inter, system-ui, sans-serif',
      mono: 'JetBrains Mono, monospace'
    },
    fontSize: {
      xs: '0.75rem',   // 12px
      sm: '0.875rem',  // 14px
      base: '1rem',    // 16px
      lg: '1.125rem',  // 18px
      xl: '1.25rem',   // 20px
      '2xl': '1.5rem', // 24px
      '3xl': '1.875rem' // 30px
    },
    fontWeight: {
      normal: 400,
      medium: 500,
      semibold: 600,
      bold: 700
    }
  },
  spacing: {
    xs: '0.25rem',  // 4px
    sm: '0.5rem',   // 8px
    md: '1rem',     // 16px
    lg: '1.5rem',   // 24px
    xl: '2rem',     // 32px
    '2xl': '3rem'   // 48px
  },
  borderRadius: {
    sm: '0.25rem',  // 4px
    md: '0.5rem',   // 8px
    lg: '1rem',     // 16px
    full: '9999px'  // Fully rounded
  },
  shadows: {
    sm: '0 1px 2px 0 rgb(0 0 0 / 0.05)',
    md: '0 4px 6px -1px rgb(0 0 0 / 0.1)',
    lg: '0 10px 15px -3px rgb(0 0 0 / 0.1)'
  }
}
\\\

**Phase 2: Web Setup (Week 1-2)**
1. Install shadcn/ui in Next.js (web-learner) and React/Vite (web-admin, meet) projects
2. Configure Tailwind with design tokens
3. Copy core components: Button, Card, Input, Dialog, Table, Dropdown, Tabs
4. Create custom components for domain-specific needs:
   - CourseCard (thumbnail, JLPT badge, progress bar, CTA)
   - FlashcardDeck (flip animation, swipe gestures, SRS indicator)
   - LiveClassRoom (video grid, whiteboard, chat, participant list)
   - ProgressDashboard (5-pillar radar chart, streak calendar, activity timeline)

**Phase 3: Mobile Setup (Week 2-3)**
1. Configure Flutter Material 3 theme with matching design tokens
2. Create custom widgets mirroring web components
3. Ensure offline-first architecture with Drift integration
4. Implement touch-optimized interactions (swipe, long-press, pinch-to-zoom)

**Phase 4: Cross-Platform Consistency (Week 3-4)**
1. Visual regression testing (compare web vs mobile screenshots)
2. Ensure color, typography, spacing match across platforms
3. Document component usage patterns in Storybook (web) and Widget Catalog (Flutter)

### Customization Strategy

**Brand Identity:**
Modern EdTech aesthetic that feels professional, trustworthy, and motivating for adult learners preparing for JLPT certification.

**Color Palette:**
- **Primary (Blue)**: Trust, professionalism, learning
  - Base: \#3b82f6\ (sky blue)
  - Dark: \#1e40af\ (deep blue)
  - Usage: Primary CTAs, navigation, links
  
- **Secondary (Purple)**: Creativity, wisdom, mastery
  - Base: \#a78bfa\ (lavender)
  - Dark: \#6d28d9\ (deep purple)
  - Usage: Advanced features, AI indicators, premium content
  
- **Accent (Orange)**: Energy, motivation, achievement
  - Base: \#f97316\ (vibrant orange)
  - Usage: Streaks, achievements, urgent CTAs, gamification elements
  
- **Semantic Colors**:
  - Success (Green \#10b981\): Progress, completion, correct answers
  - Warning (Yellow \#f59e0b\): Attention, caution, pending actions
  - Error (Red \#ef4444\): Mistakes, alerts, critical issues
  - Neutral (Gray scale): Text, backgrounds, borders

**Typography:**
- **Headings**: Inter Bold (modern, clean, professional)
- **Body**: Inter Regular (highly readable, web-optimized)
- **Code/Monospace**: JetBrains Mono (for Japanese characters, code examples)
- **Font Sizes**: Modular scale (12px, 14px, 16px, 18px, 20px, 24px, 30px)

**Visual Style:**
- **Cards**: Subtle shadows (\shadow-md\), rounded corners (8px)
- **Buttons**: 
  - Primary: Solid fills with hover states
  - Secondary: Outlined with hover fills
  - Ghost: Transparent with hover backgrounds
- **Inputs**: 
  - Clear focus states (ring-2 ring-primary-500)
  - Inline validation (success/error states)
  - Placeholder text in neutral-400
- **Animations**: 
  - Subtle, purposeful (150-300ms duration)
  - Progress bars with easing
  - Page transitions with fade
  - Micro-interactions on hover/click
- **Illustrations**: Minimalist, flat design (not cartoonish)

**Custom Components:**

1. **CourseCard**
   - Thumbnail image (16:9 aspect ratio)
   - JLPT level badge (N5-N1 with color coding)
   - Progress bar (if enrolled, shows % completion)
   - Price + enrollment CTA
   - Hover state: Lift effect (shadow-lg)

2. **FlashcardDeck**
   - Flip animation (CSS transform 3D)
   - Swipe gestures (mobile: left = wrong, right = correct)
   - SRS indicator (due today, overdue, mastered)
   - Furigana support for Kanji
   - Audio playback button

3. **LiveClassRoom**
   - Video grid (Zoom-style, responsive 2x2, 3x3, 4x4)
   - Whiteboard canvas (real-time sync via NATS)
   - Chat sidebar (collapsible, persistent scroll)
   - Participant list with connection quality indicators (green/yellow/red dots)
   - Toolbar: Mute, Camera, Screen Share, Raise Hand

4. **ProgressDashboard**
   - 5-pillar radar chart (JLPT analytics: Vocabulary, Grammar, Reading, Listening, Kanji)
   - Streak calendar heatmap (GitHub-style)
   - Recent activity timeline
   - AI recommendations card

**Accessibility:**
- **WCAG 2.1 AA Compliance** (minimum standard)
- **Keyboard Navigation**: All interactive elements accessible via Tab, Enter, Escape
- **Screen Reader Support**: ARIA labels, roles, and live regions
- **Color Contrast**: Minimum 4.5:1 for normal text, 3:1 for large text
- **Focus Indicators**: Visible and clear (2px ring in primary color)
- **Motion**: Respect \prefers-reduced-motion\ for animations
- **Text Scaling**: Support up to 200% zoom without breaking layout

**Responsive Breakpoints:**
- Mobile: 0-640px (sm)
- Tablet: 641-1024px (md)
- Desktop: 1025-1280px (lg)
- Wide: 1281px+ (xl)

---

##  UX Design Specification Complete!

This comprehensive UX design specification provides a solid foundation for implementing **Torii Nihongo**. The specification covers:

 **Project Vision** - Unified Japanese learning platform eliminating fragmentation
 **Target Users** - 4 distinct user archetypes with specific needs
 **Core Experiences** - Role-optimized interaction loops for each user type
 **Platform Strategy** - Multi-platform architecture (Web + Mobile) with offline-first mobile
 **Emotional Design** - Desired feelings and emotional journey mapping
 **UX Patterns** - Transferable patterns from Duolingo, Notion, Zoom, Coursera
 **Design System** - shadcn/ui (web) + Flutter Material 3 (mobile) with shared tokens

**Next Steps:**
1. **Design Phase**: Create high-fidelity mockups based on this specification
2. **Component Library**: Build reusable components following design system
3. **Prototyping**: Create interactive prototypes for user testing
4. **Implementation**: Develop features following UX patterns and principles
5. **Testing**: Validate emotional responses and usability with real users

The UX specification is now ready to guide your development team! 
