---
stepsCompleted: [1, 2, 3, 4, 6, 11]
inputDocuments:
  - "bmad/docs/index.md"
  - "bmad/docs/project-overview.md"
  - "bmad/docs/source-tree-analysis.md"
  - "bmad/docs/data-models-server.md"
  - "bmad/docs/api-contracts-server.md"
  - "bmad/docs/integration-architecture.md"
  - "torii-monorepo/docs/architecture-comparison.md"
  - "torii-monorepo/docs/code_review_checklist.md"
  - "torii-monorepo/docs/contributing.md"
workflowType: 'prd'
lastStep: 11
workflowStatus: 'complete'
completedDate: '2026-01-02'
---

# Product Requirements Document - torii-nihongo

**Author:** tienh
**Date:** 2026-01-02 21:50

## Executive Summary

Torii Nihongo (SP26SE005) là một giải pháp EdTech toàn diện được thiết kế để hợp nhất trải nghiệm học tiếng Nhật đang bị phân mảnh. Hệ thống cung cấp một lộ trình học tập JLPT khép kín từ học lý thuyết qua video, ôn tập thông minh bằng Flashcards (SRS), đến thực hành tương tác trong các lớp học ảo WebRTC chất lượng cao. Điểm đột phá của dự án nằm ở hệ thống Multi-Agent AI (Cortex) dựa trên giao thức FastMCP, cung cấp khả năng phản hồi thời gian thực và cá nhân hóa lộ trình học cho từng học viên.

Hệ thống được thiết kế linh hoạt, tối ưu cho cả trải nghiệm tự học (Self-paced) linh hoạt và mô hình học có hướng dẫn (Instructor-led) bài bản. Việc tích hợp thanh toán tức thì qua VNPay cùng cơ chế tặng khóa học (Gifting) giúp hệ thống không chỉ là một nền tảng học tập mà còn là một hệ sinh thái thương mại giáo dục hiện đại.

### What Makes This Special

- **Hybrid Learning Engine:** Kết hợp hài hòa giữa các khóa học Video quay sẵn (Self-paced/VOD) và các lớp học trực tuyến thời gian thực (Live Online Classes) với cơ chế tự động ghi hình để xem lại bài giảng sau khi kết thúc.
- **AI Feedback & Draft Grading:** Phản hồi sửa lỗi viết tay Kanji thời gian thực trên Whiteboard và cơ chế chấm bài nháp để giảng viên duyệt.
- **Resource Control & My Folders:** Phân quyền và đồng bộ tài liệu (PDF/Image) thời gian thực trong lớp học ảo.
- **Smart Operations Command Center:** Giám sát trạng thái lớp học, chẩn đoán mạng và hỗ trợ kỹ thuật tức thì cho cả nghìn lớp học.
- **Adaptive JLPT Analytics:** Quản lý Profile điểm số 5 cột trụ và theo dõi xu hướng phát lực, dự đoán điểm JLPT của học viên.
- **Dynamic Commerce & Gifting:** Thanh toán VNPay tích hợp Deep Link và thiết lập quy trình khuyến mãi linh hoạt kèm cơ chế tặng khóa học tức thì.
- **Flashcard Ecosystem:** Deck Marketplace với cơ chế phiên bản và đồng bộ SRS đa nền tảng để tối ưu hóa việc học từ vựng.

## Project Classification

**Technical Type:** Web Application & Mobile Application (Cross-platform)
**Domain:** EdTech (Education Technology)
**Complexity:** High (Real-time AI, WebRTC, Event-Driven Architecture)
**Project Context:** Brownfield - Nâng cấp và mở rộng dựa trên hạ tầng NATS/Microservices sẵn có.

- **Unified Multi-Platform Learning:** Trải nghiệm đồng nhất giữa Web và Mobile, hỗ trợ tiếp tục học tập (resume) từ điểm dừng cuối cùng.
- **AI Feedback & Draft Grading:** Phản hồi sửa lỗi viết tay Kanji thời gian thực trên Whiteboard và cơ chế chấm bài nháp để giảng viên duyệt.
- **Resource Control & My Folders:** Phân quyền và đồng bộ tài liệu (PDF/Image) thời gian thực trong lớp học ảo.
- **Smart Operations Command Center:** Giám sát trạng thái lớp học, chẩn đoán mạng và hỗ trợ kỹ thuật tức thì cho cả nghìn lớp học.
- **Adaptive JLPT Analytics:** Quản lý Profile điểm số 5 cột trụ và theo dõi xu hướng phát lực, dự đoán điểm JLPT của học viên.
- **Dynamic Commerce & Gifting:** Thanh toán VNPay tích hợp Deep Link và thiết lập quy trình khuyến mãi linh hoạt kèm cơ chế tặng khóa học tức thì.
- **Flashcard Ecosystem:** Deck Marketplace với cơ chế phiên bản và đồng bộ SRS đa nền tảng để tối ưu hóa việc học từ vựng.

## Success Criteria

### Academic Success (Graduation Requirements)

#### 1. Deliverables Completeness
**Thành công khi:**
- ✅ **100% Documentation** theo yêu cầu Capstone:
  - User Requirements ✓
  - Software Requirement Specification (SRS) ✓
  - Architecture Design ✓
  - Detail Design (UML 2.0) ✓
  - System Implementation ✓
  - Testing Document ✓
  - Installation Guide ✓
  - User Manuals (4 roles) ✓

- ✅ **100% Functional Requirements** implemented:
  - Web App (4 roles): Learner, Lecturer, Staff, Admin
  - Mobile App (Learner role)
  - All features listed in Proposal working

- ✅ **100% Non-Functional Requirements** met:
  - RESTful API conventions
  - JWT Authentication & Authorization
  - Cross-platform mobile (Flutter)

#### 2. Technical Excellence
**Thành công khi:**
- ✅ **Architecture Quality:**
  - Microservices properly separated (Identity, LMS, Meet, etc.)
  - NATS event-driven communication working
  - Database schema normalized (3NF)
  - API contracts well-defined (OpenAPI/Swagger)

- ✅ **Code Quality:**
  - Clean code principles applied
  - Design patterns used appropriately
  - Unit test coverage > 60%
  - Integration tests for critical flows

- ✅ **Deployment Success:**
  - System deployed and accessible
  - Installation guide works (can replicate deployment)
  - No critical bugs in demo

#### 3. Presentation & Defense
**Thành công khi:**
- ✅ **Demo Quality:**
  - All core features demonstrated smoothly
  - Live WebRTC class works with 5+ participants
  - AI Sensei responds in < 3 seconds
  - Payment flow (VNPay) completes successfully
  - Mobile app syncs with web seamlessly

- ✅ **Defense Performance:**
  - Can explain architecture decisions
  - Can justify technology choices
  - Can answer questions about scalability, security
  - Team members demonstrate equal contribution

### Business Success (Japanese Learning Center)

#### 1. Problem Resolution
**Thành công khi giải quyết được các vấn đề trong Proposal:**

**❌ Vấn đề cũ:** "Fragmented learning experience"  
**✅ Giải pháp:** Unified platform - 1 hệ thống cho VOD, Quiz, Exam, Live Class  
**📊 Đo lường:** Staff có thể quản lý toàn bộ từ 1 dashboard (không cần 3-4 hệ thống khác nhau)

**❌ Vấn đề cũ:** "Instructor feedback delayed or generic"  
**✅ Giải pháp:** AI real-time feedback + Lecturer tools  
**📊 Đo lường:** 
- AI Sensei phản hồi trong < 3 giây
- Lecturer có thể chấm bài với AI draft grading (tiết kiệm 50% thời gian)

**❌ Vấn đề cũ:** "Online classes lack interactivity"  
**✅ Giải pháp:** WebRTC with Whiteboard, Chat, Screen sharing  
**📊 Đo lường:** 
- WebRTC latency < 200ms
- Whiteboard real-time sync < 100ms
- Lecturer có Engagement Heatmap để theo dõi participation

**❌ Vấn đề cũ:** "Management difficulties across fragmented systems"  
**✅ Giải pháp:** Centralized Staff Dashboard  
**📊 Đo lường:**
- Staff có thể tạo lớp Live trong < 5 phút
- Có thể assign Lecturer và track attendance tự động
- Real-time monitoring cho tất cả lớp đang diễn ra

#### 2. User Satisfaction (Center's Perspective)
**Thành công khi:**

**Learner:**
- ✅ Có thể mua khóa học và bắt đầu học trong < 10 phút
- ✅ Tiến độ học tập được track tự động (không cần tự ghi chép)
- ✅ Có thể join Live class chỉ với 1 click
- ✅ Flashcards đồng bộ giữa Web và Mobile

**Lecturer:**
- ✅ Có thể start Live class trong < 2 phút
- ✅ Thấy được attendance tự động (không cần điểm danh thủ công)
- ✅ AI hỗ trợ chấm bài (giảm workload)
- ✅ Có thể upload tài liệu và share ngay trong class

**Staff:**
- ✅ Có thể tạo khóa học mới trong < 30 phút
- ✅ Có thể schedule lớp Live và assign Lecturer dễ dàng
- ✅ Dashboard hiển thị real-time status của tất cả lớp
- ✅ Có thể export reports cho management

**Admin:**
- ✅ Có overview dashboard với key metrics (users, revenue, engagement)
- ✅ Có thể monitor payments và reconcile với VNPay
- ✅ Có thể approve/deactivate users khi cần

#### 3. Operational Efficiency
**Thành công khi:**
- ✅ **Time Savings:**
  - Tạo lớp Live: Từ 30 phút → 5 phút
  - Chấm bài: Từ 10 phút/bài → 5 phút/bài (với AI)
  - Điểm danh: Từ 5 phút → 0 phút (tự động)

- ✅ **Error Reduction:**
  - Không còn double booking (Distributed Lock)
  - Không còn thanh toán xong nhưng hết chỗ (Atomic Transaction)
  - Không còn mất dữ liệu tiến độ (Auto-save)

- ✅ **Scalability:**
  - Hệ thống có thể handle 50 lớp Live đồng thời
  - Database có thể lưu 10,000 users, 1,000 courses
  - Video storage có thể lưu 1TB content

### Measurable Outcomes (KPIs)

#### Graduation Success (10 weeks)
| Metric | Target | How to Measure |
|--------|--------|----------------|
| **Functional Completeness** | 100% | All features in Proposal working |
| **Documentation Completeness** | 100% | All 8 documents submitted |
| **Demo Success Rate** | 100% | No critical failures during demo |
| **Code Quality** | > 60% | Test coverage report |
| **Defense Score** | > 8.0/10 | Hội đồng evaluation |

#### Business Value (Center's Acceptance)
| Metric | Target | How to Measure |
|--------|--------|----------------|
| **System Uptime** | > 95% | During demo week |
| **WebRTC Quality** | < 200ms latency | LiveKit metrics |
| **AI Response Time** | < 3 seconds | Cortex service logs |
| **Payment Success Rate** | > 99% | VNPay transaction logs |
| **User Onboarding Time** | < 10 minutes | From signup to first lesson |
| **Staff Productivity** | 50% time saved | Compared to manual process |

#### Technical Performance
| Metric | Target | How to Measure |
|--------|--------|----------------|
| **API Response Time** | < 200ms (p95) | APM monitoring |
| **Page Load Time** | < 2s (Web), < 1.5s (Mobile) | Lighthouse score |
| **Database Query Time** | < 100ms (p95) | PostgreSQL logs |
| **Video Streaming** | < 3s initial load | MinIO metrics |
| **Mobile App Size** | < 50MB | APK/IPA file size |

## Product Scope

### MVP - Minimum Viable Product (Week 1-10)
**MUST HAVE for Graduation:**
- ✅ User Management (4 roles) with JWT auth
- ✅ Course Browse & Purchase (VNPay integration)
- ✅ Video Learning with Progress Tracking
- ✅ Live WebRTC Classes (basic features)
- ✅ Flashcards with SRS algorithm
- ✅ Quiz & JLPT Practice Exams
- ✅ Lecturer Dashboard (schedule, attendance, grading)
- ✅ Staff Dashboard (course management, class scheduling)
- ✅ Admin Dashboard (system overview, user management)
- ✅ Mobile App (Learner role - all core features)
- ✅ Basic AI Sensei (Q&A support)
- ✅ Notifications (Push + Email)

### Growth Features (Post-Graduation)
**NICE TO HAVE if time permits:**
- ⏸️ Advanced Gamification (Badges, Leaderboards)
- ⏸️ Deck Marketplace (Community flashcards)
- ⏸️ Multi-Agent AI (Assessment + Analytics Agents)
- ⏸️ Audio Feedback for Lecturers
- ⏸️ Advanced Analytics Dashboard
- ⏸️ Dark Mode
- ⏸️ Video Captions (Auto-generated)

### Vision (Future - Production)
**FOR REAL DEPLOYMENT:**
- 🔮 Social Learning (Study Groups, Peer Review, Forum)
- 🔮 Subscription Model
- 🔮 Referral Program
- 🔮 Corporate Licenses
- 🔮 AI Conversation Partner
- 🔮 Multi-language UI (English)

## Detailed Functional Requirements - Learner Experience (Web & Mobile)

Dành cho học viên trên cả hai nền tảng, tập trung vào sự tiện lợi và lộ trình học tập xuyên suốt.

### 1. Khám phá & Giao dịch (Discovery & Transaction)
- **US.LEARN.01 (Unified Catalog):** AS A Learner, tôi có thể duyệt danh sách khóa học, hệ thống hiển thị rõ ràng loại hình: Video (Học ngay) hoặc Live (Theo lịch).
- **US.LEARN.02 (Live Seat Reservation):** ĐẶC THÙ: Đối với lớp Live, học viên phải chọn một "Lịch khai giảng" cụ thể còn chỗ (Seats Available) trước khi tiến hành thanh toán.
- **US.LEARN.03 (Checkout Flow):** Quy trình chuẩn: Chọn khóa học/Lớp Live -> Kiểm tra giỏ hàng -> Thanh toán VNPay/Nhập Gifting Code -> Tự động kích hoạt quyền truy cập ngay khi giao dịch thành công.

### 2. Trải nghiệm Học tập Hybrid (Learning Journey)
- **US.LEARN.04 (Learning Resources):** Toàn bộ học viên (VOD & Live) đều truy cập tài liệu qua mục **'My Folders'**. Hệ thống tự động phân loại thư mục theo từng khóa học đã mua.
- **US.LEARN.05 (Session Attendance):** Đối với lớp Live, hệ thống tự động ghi nhận 'Hoàn thành' dựa trên dữ liệu điểm danh thời gian thực từ WebRTC.
- **US.LEARN.06 (Progress Aggregation):** Tiến độ tổng thể được tính bằng tổng số đầu mục đã hoàn thành (Video đã xem, Quiz đã đạt, Buổi Live đã tham gia) chia cho tổng khối lượng khóa học.
- **US.LEARN.07 (VOD Access):** Đối với khóa Hybrid, học viên được mở khóa toàn bộ kho Video Studio ngay sau khi mua để chuẩn bị bài (Flipped Classroom) trước khi tham gia lớp Live.

### 3. Đánh giá & Cá nhân hóa (Assessment & Personalization)
- **US.LEARN.08 (Progress Tracking):** AS A Learner, tôi muốn xem thống kê tiến độ học tập, tỷ lệ hoàn thành khóa học ngay trên Dashboard cá nhân.
- **US.LEARN.09 (Exam Center):** AS A Learner, tôi có thể tham gia các bài kiểm tra định kỳ và thi thử JLPT với đồng hồ đếm ngược và chấm điểm tự động.
- **US.LEARN.10 (Profile & Privacy):** AS A Learner, tôi có thể cập nhật thông tin cá nhân, ảnh đại diện, đổi mật khẩu và quản lý thông tin liên hệ.
- **US.LEARN.11 (Financial Records):** AS A Learner, tôi có thể theo dõi lịch sử thanh toán, danh sách đơn hàng và các khóa học đã tặng cho người khác.

## Detailed Functional Requirements - AI (Cortex Service)

Hệ thống AI Multi-Agent (Sensei, Assessment, Analytics) dựa trên giao thức FastMCP và hạ tầng NATS để cung cấp phản hồi siêu nhanh (low-latency).

### 1. Sensei Agent (Trợ lý học tập 24/7)
- **US.AI.01 (Contextual Q&A):** AS A Learner, tôi có thể bôi đen một từ vựng hoặc ngữ pháp trong bài học và hỏi AI Sensei để nhận được giải thích ngay lập tức về ý nghĩa, cách dùng và các ví dụ tương tự.
- **US.AI.02 (Grammar Correction):** AS A Learner, khi tôi viết một câu tiếng Nhật, AI Sensei sẽ phân tích cấu trúc ngữ pháp và gợi ý những cách diễn đạt tự nhiên hơn (Native-like).
- **US.AI.03 (Flashcard Generation):** AS A Learner, tôi có thể yêu cầu AI Sensei tạo thẻ Flashcard tự động từ một đoạn văn bản tôi đang đọc, bao gồm cả âm hán việt, Furigana và câu ví dụ.

### 2. Assessment Agent (Giám khảo JLPT & Trợ lý chấm bài)
- **US.AI.04 (Dynamic Test Creation):** AS A Learner, tôi có thể yêu cầu AI tạo ra một bài kiểm tra ngắn (Mini-test) tập trung đúng vào phần kiến thức tôi vừa học.
- **US.AI.04b (Draft Grading Workflow):** AS A Lecturer, tôi muốn AI chấm nháp các lỗi ngữ pháp/từ vựng và tô đỏ các phần cần lưu ý để tôi có thể duyệt hoặc sửa kết quả nhanh chóng.
- **US.AI.05 (Automated Writing Feedback):** AS A Learner, sau khi tôi hoàn thành bài viết hoặc làm bài tập tự luận, AI Assessment sẽ chấm điểm và chỉ ra chính xác lỗi sai (về ngữ pháp, từ vựng, trợ từ).
- **US.AI.06 (JLPT Score Prediction):** AS A Learner, dựa trên hồ sơ năng lực 5 cột trụ, AI sẽ dự đoán số điểm JLPT có thể đạt được và đưa ra cảnh báo về các vùng kiến thức yếu.
- **US.AI.06b (Smart Exam Generator):** AS An Academic Staff, tôi muốn AI hỗ trợ bốc ngẫu nhiên câu hỏi từ ngân hàng dựa trên yêu cầu ngôn ngữ tự nhiên (Ví dụ: "Tạo đề N3 thiên về trợ từ").

### 3. Analytics Agent (Kỹ sư lộ trình - Adaptive Learning)
- **US.AI.07 (Weakness Identification):** AS A Learner, tôi muốn hệ thống tự động nhận diện các mảng kiến thức yếu qua dữ liệu học tập và đẩy thêm bài tập liên quan vào danh sách ôn tập.
- **US.AI.08 (Recommendation Engine):** AS A Learner, Analytics Agent sẽ đề xuất "3 hành động cần làm ngay hôm nay" dựa trên mục tiêu thi cử và tiến độ thực tế để tăng tỉ lệ đỗ JLPT.

### 4. Meet Integration (Phản hồi thời gian thực trong lớp học)
- **US.AI.09 (Real-time Handwriting Feedback):** AS A Learner, khi tôi viết Kanji trên Whiteboard của lớp học WebRTC, AI sẽ nhận diện nét vẽ và báo lỗi ngay lập tức nếu sai thứ tự nét hoặc bộ thủ.
- **US.AI.10 (Live Transcription & Translation):** AS A Learner, trong lớp học trực tuyến, tôi có thể xem phụ đề (Live Caption) và bản dịch thời gian thực lời giảng của giáo viên.

## Detailed Functional Requirements - Hệ thống Nhân viên (Staff Types)

Hệ thống quản trị được phân rã thành các vai trò chuyên biệt để tối ưu hóa hiệu suất vận hành của trung tâm.

### 1. Academic Staff (Ban Giáo vụ/Nội dung)
- **US.STAFF.ACAD.01 (Smart Bulk Import):** AS A Staff, tôi có thể import hàng ngàn câu hỏi từ Excel/CSV và để AI tự động bóc tách nội dung thô, gợi ý JLPT Level, kỹ năng và đề xuất Furigana cho Kanji.
- **US.STAFF.ACAD.02 (Duplicate Detection):** AS A Staff, tôi muốn hệ thống tự động cảnh báo nếu câu hỏi mới nhập có nội dung trùng lặp trên 90% với câu hỏi đã có sẵn.
- **US.STAFF.ACAD.03b (Question Bank Management):** Quản lý ngân hàng câu hỏi theo cấp độ JLPT, kỹ năng và danh mục chuyên sâu (Ngữ pháp, Từ vựng, Hán tự).
- **US.STAFF.ACAD.04 (Auto-Exam Generator):** AS A Staff, tôi muốn tạo đề thi thử JLPT bằng cách thiết lập cấu trúc để hệ thống tự động bốc ngẫu nhiên câu hỏi chưa từng xuất hiện.
- **US.STAFF.ACAD.05 (Course Lifecycle):** AS A Staff, tôi muốn lập lịch tự động xuất bản (Publish) hoặc lưu trữ (Archive) khóa học theo kế hoạch học thuật.

### 2. Operations Staff (Ban Vận hành/Điều phối)
- **US.STAFF.OPS.01 (Command Center Dashboard):** AS A Staff, tôi muốn theo dõi trạng thái sức khỏe (health metrics) của tất cả các lớp học Live đang diễn ra theo thời gian thực.
- **US.STAFF.OPS.02 (Quick Support Chat):** AS A Staff, tôi muốn tiếp nhận và xử lý các Ticket hỗ trợ kỹ thuật từ học viên trong lớp Live qua kênh chat riêng tư.
- **US.STAFF.OPS.03 (Scheduling & Assignment):** AS A Staff, tôi muốn thiết lập lịch học cho các lớp Online và phân công Giảng viên phù hợp cho từng khung giờ.
- **US.STAFF.OPS.04 (Live Intervention):** Hỗ trợ giảng viên điểm danh, khóa Whiteboard hoặc xử lý các vấn đề kỹ thuật trực tiếp trong phòng học.

### 3. Admissions & Marketing Staff (Ban Tuyển sinh/Sales)
- **US.STAFF.MKT.01 (Dynamic Coupon Rules):** AS A Staff, tôi muốn thiết lập các quy tắc khuyến mãi đa dạng (loại giảm giá, số lượng sử dụng, giới hạn khóa học hoặc đối tượng người dùng).
- **US.STAFF.MKT.02 (CMS Management):** AS A Staff, tôi muốn quản lý Blog, Tags và nội dung truyền thông để thu hút học viên mới.
- **US.STAFF.MKT.03 (Engagement Tracking):** AS A Staff, tôi muốn theo dõi hiệu quả bài viết qua Views/Likes để điều chỉnh chiến lược nội dung.

### 4. Financial Staff (Ban Kế toán)
- **US.STAFF.FIN.01 (Transaction Monitoring):** AS A Financial Staff, tôi muốn theo dõi lịch sử giao dịch VNPay và xác minh trạng thái thanh toán của mọi đơn hàng.
- **US.STAFF.FIN.02 (Revenue Reporting):** AS An Admin/Finance, tôi muốn xem báo cáo doanh thu phân bổ theo từng giảng viên và hiệu quả của từng loại coupon.
- **US.STAFF.FIN.03 (Refund Management):** AS A Financial Staff, tôi muốn xử lý các yêu cầu hoàn tiền và cập nhật trạng thái đơn hàng tương ứng.

### 5. Smart Operations & Task Management (Tất cả Staff)
- **US.STAFF.GEN.01 (Event-Driven To-Do List):** AS A Staff, tôi muốn một danh sách công việc thông minh tự động tổng hợp từ các sự kiện trong hệ thống (ví dụ: bài tập chờ chấm, câu hỏi chờ duyệt, đơn hàng lỗi).
- **US.STAFF.GEN.02 (Task Claiming):** AS A Staff, tôi khi bắt đầu xử lý một nhiệm vụ, trạng thái sẽ chuyển thành 'In Progress' để đồng nghiệp khác biết và không xử lý trùng lặp.
- **US.STAFF.GEN.03 (Priority Alerts):** AS A Staff, tôi muốn nhận thông báo ưu tiên cho các vấn đề kỹ thuật phát sinh trong các lớp Live đang diễn ra để xử lý ngay lập tức.

## Detailed Functional Requirements - Lecturer Operations

Hệ thống cung cấp các công cụ mạnh mẽ để Giảng viên điều phối lớp học và tối ưu hóa hiệu suất giảng dạy.

- **US.LECT.01 (Smart Teaching Schedule):** AS A Lecturer, tôi có thể xem lịch dạy tích hợp, nơi mỗi buổi học Live đã được tự động liên kết với đúng tài nguyên (VOD Studio, Slides, Quiz) từ Master Course.
- **US.LECT.02 (Enhanced Session Control):** AS A Lecturer, tôi có thể chủ động Start/End lớp học, điều khiển quyền hạn của học viên (Mute/Unmute, Lock Whiteboard) và sử dụng tính năng 'Spotlight' để phóng to bài làm của một học viên cho cả lớp xem.
- **US.LECT.03 (Real-time Engagement Heatmap):** AS A Lecturer, tôi muốn thấy trạng thái tương tác của học viên (đang làm quiz, đang vẽ trên whiteboard, hoặc đang vắng mặt khỏi màn hình) để kịp thời gọi tên hỗ trợ.
- **US.LECT.04 (Personal Vault & Material Sync):** AS A Lecturer, tôi có thể quản lý kho tài liệu cá nhân và dễ dàng chia sẻ chúng vào các lớp học khác nhau mà mình phụ trách chỉ với một thao tác kéo thả.
- **US.LECT.05 (Unified Grading & Audio Feedback):** AS A Lecturer, tôi muốn chấm bài tập từ tất cả các lớp trong một giao diện tập trung, hỗ trợ ghi âm nhận xét (Audio Feedback) để tăng tính tương tác và cảm xúc cho học viên.
- **US.LECT.06 (AI Co-Pilot):** AS A Lecturer, tôi muốn AI hỗ trợ lọc các câu hỏi quan trọng trong chat room và tạo bản tóm tắt nội dung (Class Summary) tự động ngay sau khi lớp học kết thúc.
- **US.LECT.07 (Automated Attendance):** Hệ thống tự động ghi nhận thời gian hiện diện của học viên trong lớp Live và cập nhật vào sổ đầu bài mà không cần giảng viên điểm danh thủ công.

## Detailed Functional Requirements - Assignments (Bài tập tự luận)

- **US.ASSIGN.01 (Multi-format Submissions):** AS A Learner, tôi muốn nộp bài tập dưới nhiều định dạng (Text, PDF, Image, Audio) để phù hợp với yêu cầu thực hành đa dạng.
- **US.ASSIGN.02 (AI Pre-grading Assistant):** AS A Lecturer, tôi muốn xem các gợi ý sửa lỗi và đánh giá sơ bộ từ AI đối với bài làm của học viên.
- **US.ASSIGN.03 (Contextual Feedback):** AS A Learner, tôi muốn nhận được nhận xét chi tiết kèm theo điểm số từ giảng viên và có thể gửi thắc mất ngược lại.

## Detailed Functional Requirements - Flashcards & Community

- **US.FLASH.01 (SRS Sync):** AS A Learner, tôi muốn đồng bộ thuật toán lặp lại ngắt quãng giữa Web và Mobile (hỗ trợ cả Offline trên App).
- **US.FLASH.02 (Deck Marketplace):** AS A Learner, tôi muốn chia sẻ bộ thẻ cá nhân (Public/Private), đánh giá và tải về các bộ thẻ từ cộng đồng người học khác.
- **US.FLASH.03 (Version Control):** AS A Learner, tôi muốn nhận thông báo khi bộ thẻ gốc tôi đã tải về có phiên bản cập nhật mới.

## Detailed Functional Requirements - Billing & Gifting

- **US.BILL.01 (Atomic Enrollment):** Quy trình gán quyền học tập (Enrollment) phải là một giao dịch nguyên tử (Atomic Transaction) đi kèm với việc thanh toán thành công để tránh tình trạng thanh toán xong nhưng hết chỗ hoặc không vào được lớp.
- **US.BILL.02 (Gift Experience):** Khi mua quà tặng, hệ thống sinh ngay mã kích hoạt kèm QR Code. Quyền chọn lịch học Live sẽ thuộc về người nhận mã (Reciever) tại thời điểm họ kích hoạt mã.

## Detailed Functional Requirements - Gamification (Module Trò chơi hóa)

- **US.GAME.01 (Streak System):** AS A Learner, tôi muốn thấy chuỗi ngày học liên tiếp để duy trì thói quen và nhận thưởng khi đạt mốc lớn.
- **US.GAME.02 (Dynamic Ranking):** AS A Learner, tôi muốn tích lũy XP từ việc học và thi đấu để thăng hạng (Bronze, Silver, Gold, Torii Master).
- **US.GAME.03 (Badge Collection):** AS A Learner, tôi muốn nhận huy hiệu thành tựu khi hoàn thành các mục tiêu khó.
- **US.GAME.04 (Dual Mode):** AS A Learner, tôi muốn thách đấu giải Quiz nhanh với người khác để tích lũy thêm XP.

## Detailed Functional Requirements - Notification Engine

- **US.NOTIF.01 (Smart Reminders):** AS A Learner, tôi muốn nhận thông báo đẩy trước giờ học 15 phút hoặc khi đến "giờ vàng" ôn tập SRS.
- **US.NOTIF.02 (Assignment Updates):** AS A Learner, tôi muốn nhận thông báo ngay khi bài tập được chấm điểm hoặc có tài liệu mới từ giảng viên.
- **US.NOTIF.03 (Engagement Alerts):** AS A Staff, tôi muốn nhận cảnh báo nếu học viên có dấu hiệu bỏ học hoặc kết quả sụt giảm.

## Detailed Functional Requirements - Dashboard & Analytics

- **US.DASH.01 (Staff/Admin Overview):** Tổng hợp các khóa học được giao, nhiệm vụ cần làm và báo cáo hiệu suất cá nhân/hệ thống trong một trang duy nhất.
- **US.DASH.02 (Retention & Risk):** AI phân tích và cảnh báo những học viên cần được hỗ trợ kịp thời để duy trì tỷ lệ giữ chân.

## Detailed Functional Requirements - Hệ thống Quản trị (Admin Governance)

Dành cho cấp quản lý cao nhất để giám sát toàn bộ vận hành và chính sách hệ thống.

- **US.ADMIN.01 (Strategic Dashboard):** AS An Admin, tôi muốn xem các chỉ số kinh doanh sống còn như LTV, CAC, và tỷ lệ giữ chân học viên qua các biểu đồ trực quan thời gian thực.
- **US.ADMIN.02 (Financial Reconciliation):** AS An Admin, tôi muốn hệ thống tự động đối soát số dư giữa VNPay và cơ sở dữ liệu để cảnh báo ngay lập tức nếu có sai lệch.
- **US.ADMIN.03 (Audit Trail & Governance):** Hệ thống ghi lại toàn bộ nhật ký hành động nhạy cảm của Staff để hậu kiểm và đảm bảo tính minh bạch trong vận hành.
- **US.ADMIN.04 (Platform Kill-Switch):** AS An Admin, tôi có quyền tạm dừng hiển thị bất kỳ khóa học nào hoặc vô hiệu hóa các tính năng hệ thống ngay lập tức khi phát hiện rủi ro nghiêm trọng.
- **US.ADMIN.05 (RBAC & Impersonation):** AS An Admin, tôi quản lý phân quyền chi tiết cho Staff và có quyền truy cập hỗ trợ dưới danh nghĩa người dùng (Impersonation) để xử lý sự cố kỹ thuật.
- **US.ADMIN.06 (Account Governance):** AS An Admin, tôi có quyền phê duyệt hồ sơ giảng viên mới hoặc đình chỉ tài khoản vi phạm chính sách của nền tảng.
- **US.ADMIN.07 (Quality Gatekeeper):** Duyệt lần cuối nội dung master course trước khi cho phép mở bán chính thức trên quy mô lớn.

## Operational Policies & Integration Logic

Dưới đây là các quy tắc nghiệp vụ đã được thống nhất để đảm bảo hệ thống vận hành trơn tru:

1.  **Chính sách Hoàn tiền Hybrid (Refund Policy):** 
    *   Giá khóa học Hybrid được tách làm 2 phần: Học phí VOD (truy cập ngay) và Học phí Live (chi phí giảng dạy). 
    *   Học viên chỉ được hoàn phí Live nếu lớp chưa khai giảng hoặc có sự cố từ phía trung tâm. Phí VOD không được hoàn sau khi đã kích hoạt quyền truy cập.
2.  **Quyền sở hữu Tài liệu (Resource Ownership):**
    *   Tài liệu giáo viên tải lên riêng cho một lớp (Local Resource) thuộc quyền quản lý của lớp đó. 
    *   Academic Staff có quyền duyệt và nâng cấp các tài liệu này lên Master Resource để dùng chung cho toàn hệ thống nếu đạt tiêu chuẩn chất lượng.
3.  **Quản lý Xung đột Lịch dạy (Scheduling Conflict):**
    *   Hệ thống tự động ngăn chặn hoặc cảnh báo khi gán một giảng viên vào 2 lớp có thời gian gối đầu nhau dưới 15 phút.
    *   Cung cấp tính năng 'Emergency Re-assignment' để Ops Staff thay đổi giảng viên trong vòng 3 phút khi có sự cố bất ngờ.
4.  **Cơ chế Giữ chỗ (Seat Reservation):**
    *   Thanh toán/Kích hoạt Gift Code sẽ đi kèm với 'Distributed Lock' trên NATS trong 15 phút để đảm bảo học viên chắc chắn có ghế sau khi trả tiền.

## User Journeys

The following narrative journeys reveal how Torii Nihongo transforms the daily reality of each user type, from struggle to success. Each journey uncovers specific capabilities and requirements needed for the system.

### Journey 1: Minh Nguyen - From JLPT Anxiety to Confident Test-Taker

**The Struggle:**
Minh is a 24-year-old software developer in Ho Chi Minh City who dreams of working for a Japanese tech company. He's been self-studying Japanese for 2 years using YouTube videos and random apps, but his progress feels chaotic. He has the JLPT N3 exam in 4 months, but when he tries practice tests, his scores are all over the place - sometimes he aces grammar, other times he bombs vocabulary. He doesn't know what to focus on, and the clock is ticking.

His daily commute on the metro takes 2 hours each way, but the internet connection is terrible. He wishes he could study during this dead time, but most learning apps require constant connectivity.

**Discovery:**
Late one night after failing another practice test (scoring only 65/180), Minh searches for "JLPT N3 structured course Vietnam" and discovers Torii Nihongo. The homepage promises "AI-powered adaptive learning with live instructor support" - exactly what he needs. He sees a Hybrid course: "JLPT N3 Intensive - 12 weeks" with both pre-recorded videos AND weekly live classes. The price is reasonable, and there's a VNPay option. He decides to give it a shot.

**The Transformation:**
Within 10 minutes of payment, Minh is watching his first video lesson. The system automatically tracks his progress. After completing 3 video modules, he tries the built-in quiz - and the AI Sensei immediately identifies his weakness: he confuses similar particles (に vs で vs を). The system pushes targeted flashcards to his mobile app.

**The Game-Changer - Offline Learning:**
Minh discovers he can download entire lesson modules and flashcard decks to his phone. Now during his metro commute, he watches downloaded videos and practices flashcards completely offline. When he gets home and connects to WiFi, all his progress syncs automatically. Those 4 hours of daily commute time become his most productive study sessions.

**Live Class Breakthrough:**
During his first live WebRTC class, Minh writes a practice sentence on the whiteboard. The AI gives real-time feedback on his Kanji stroke order - something no YouTube video ever did. The lecturer, seeing his AI-flagged particle errors, spends 5 extra minutes explaining the nuances. Minh can ask questions and get immediate answers.

When Minh struggles to understand a grammar point, he uses the screen reader accessibility feature to have the explanation read aloud while he follows along visually. The multi-modal learning helps it finally click.

**Progress Tracking:**
Six weeks in, Minh's JLPT Analytics dashboard shows his 5-pillar scores trending upward:
- **Vocabulary:** 72% → 85% ✓
- **Grammar:** 68% → 81% ✓
- **Reading:** 55% → 70% ⚠️ (needs focus)
- **Listening:** 78% → 84% ✓
- **Kanji:** 65% → 79% ✓

The AI predicts he'll score 125/180 if he maintains his current pace. The system recommends: "Focus 30% more on Reading Comprehension this week." He follows the advice.

**The Resolution:**
On exam day, Minh feels prepared for the first time in his life. Three months later, he receives his results: 138/180 - a solid pass. He immediately logs into Torii Nihongo and enrolls in the N2 course. This time, he gifts an N3 course to his colleague using the platform's gifting feature. The journey continues.

### Journey 2: Cô Hana - From Overwhelmed Teacher to Empowered Educator

**The Struggle:**
Cô Hana is a 32-year-old Japanese language lecturer at a learning center in Hanoi. She teaches 6 live classes per week, each with 15-20 students. Her days are exhausting: manually taking attendance, answering the same grammar questions repeatedly, spending hours grading handwritten assignments, and trying to remember which student needs extra help. She loves teaching, but the administrative burden is crushing her passion.

**Discovery:**
Her center's director announces they're adopting Torii Nihongo for all live classes. Hana is skeptical - another "EdTech solution" that promises everything and delivers nothing. But during the onboarding training, she sees the Lecturer Dashboard and something clicks: "This might actually help."

**The Transformation:**
Her first class using Torii Nihongo is eye-opening. She starts the session with one click - no fumbling with Zoom links or attendance sheets. The system automatically tracks who's present. When students join, she can see their learning history and AI-identified weak points right in her interface.

During the lesson, a student asks about the difference between 〜ている and 〜てある. Instead of explaining for the 50th time, Hana asks AI Sensei to generate a visual explanation with examples. It appears on all students' screens in 3 seconds. She can focus on the nuanced cases.

**The Grading Revolution:**
The real game-changer comes with grading. Students submit their writing assignments through the platform. The AI Assessment Agent pre-grades them, highlighting grammar errors and suggesting scores. What used to take Hana 3 hours now takes 45 minutes - she just reviews the AI's suggestions, adds her personal audio feedback, and approves.

**The Grading Dispute:**
One day, a student challenges her score on an essay, claiming the AI marked a correct answer as wrong. Hana opens the dispute workflow, reviews the AI's reasoning, and realizes the student is actually right - it's an edge case the AI missed. She overrides the score, adds a note explaining the nuance, and the system automatically recalculates the student's grade. The transparency builds trust.

**Proactive Engagement:**
The Engagement Heatmap shows her that 3 students haven't participated in the last 2 classes. She makes a mental note to call on them specifically next session. The system also suggests: "Student Linh's quiz scores dropped 15% this week - consider a check-in."

**Mentorship and Growth:**
When a new lecturer joins the center, Hana shares her lesson templates and whiteboard layouts through the platform's mentorship system. The new teacher can observe her recorded classes and adapt her techniques. Hana feels proud to be helping the next generation of educators.

**The Resolution:**
Three months later, Hana teaches the same 6 classes but leaves work 2 hours earlier each day. She uses that time to create better lesson materials and actually enjoys teaching again. Her student satisfaction scores have increased because she has more energy for personalized attention. When the center asks her to take on a 7th class, she actually says yes - something she would never have done before.

### Journey 3: Anh Tuan - From Managing Chaos to Orchestrating Excellence

**The Struggle:**
Anh Tuan is the Operations Manager at a Japanese learning center with 200+ active students and 15 lecturers. His job is to schedule live classes, assign teachers, handle technical issues during sessions, and somehow keep everything running smoothly. He uses 3 different systems: Excel for scheduling, Google Sheets for attendance, and manual WhatsApp messages to coordinate with lecturers. When a teacher calls in sick 30 minutes before class, it's pure panic.

**Discovery:**
After the center implements Torii Nihongo, Tuan attends a training session for the Operations Staff role. He's shown the "Command Center Dashboard" - a real-time view of all live classes happening right now, their health metrics, and a smart task management system.

**The Transformation:**
Monday morning, Tuan opens his dashboard. Instead of checking 3 different spreadsheets, he sees everything in one place:
- 4 live classes currently in session (all showing green health indicators)
- 7 classes scheduled for today (2 need lecturer assignment)
- 12 pending tasks (3 high-priority: assignments waiting for review, 1 payment reconciliation issue, 8 routine admin tasks)

**Proactive Quality Management:**
Tuan notices something new: a yellow warning icon next to Lecturer Phong's name. He clicks it and sees: "Engagement scores trending down 12% over last 3 classes. Student participation rate: 45% (avg: 72%)." 

Instead of waiting for student complaints, Tuan schedules a private chat with Phong. They discover Phong has been dealing with family stress and hasn't had time to prepare interactive activities. Tuan reassigns some of his classes temporarily and connects him with a mentor lecturer. Crisis prevented before it became a crisis.

**Capacity Planning:**
It's November - JLPT exam season is approaching. Tuan opens the Capacity Planning dashboard and sees a forecast: "Expected enrollment surge: +35% in next 4 weeks. Current lecturer capacity: 85% utilized. Recommendation: Hire 2 additional part-time lecturers or limit new enrollments."

Armed with data, Tuan presents the case to management. They approve hiring 2 new lecturers. When the surge hits, they're ready.

**Emergency Response:**
During a live class, a student reports audio issues. The system automatically creates a support ticket and routes it to Tuan's dashboard. He can see the student's connection diagnostics in real-time: "Latency: 450ms (high), Packet loss: 8% (critical)." He sends a quick chat message with troubleshooting steps, and the issue is resolved in 90 seconds - without disrupting the class.

When a lecturer calls in sick, Tuan uses the "Emergency Re-assignment" feature. The system shows which backup lecturers are free, he selects one, and automated notifications go out to the new lecturer and all students. Crisis averted in 3 minutes.

**Disaster Recovery:**
One day, the WebRTC service experiences an outage mid-class. Tuan's disaster recovery training kicks in: he activates the backup Zoom link stored in the system, sends automated SMS to all students with the new link, and the class resumes in 5 minutes. The system logs the incident for post-mortem analysis.

**The Resolution:**
Six months later, the center has grown from 200 to 350 students, but Tuan's stress level has actually decreased. He manages 50% more classes with the same team size. The director asks him how he's doing it. Tuan smiles: "The system does the coordination. I just make the decisions."

### Journey 4: Chi Mai - From Data Blind to Strategic Visionary

**The Struggle:**
Chi Mai is the Director of a Japanese learning center. She needs to make strategic decisions: Which courses to invest in? Are we retaining students? Is our pricing right? But getting answers requires asking her staff to manually compile reports from multiple systems. By the time she gets the data, it's already outdated.

**Discovery:**
After implementing Torii Nihongo, Mai is given admin access to the Strategic Dashboard. She's skeptical - most "dashboards" are just pretty charts with no actionable insights.

**The Transformation:**
Mai logs in and immediately sees the metrics that matter:
- **Revenue Trend:** ₫45M this month (↑15% vs last month)
- **Student Retention:** 78% (↓3% - WARNING)
- **Course Performance:** N3 Hybrid courses have 2.5x higher completion rates than N3 VOD-only
- **Lecturer Efficiency:** Top 3 lecturers by student satisfaction scores
- **Payment Reconciliation:** VNPay balance matches internal records ✓

**The Retention Insight:**
The retention drop catches her attention. She drills down and discovers that students who don't attend their first live class within 7 days of enrollment are 60% more likely to drop out. This is actionable intelligence.

She immediately asks her Operations team to implement a new policy: automated reminder calls for students who haven't joined their first live session within 5 days.

**Competitive Intelligence:**
Mai opens the new Competitive Analysis dashboard. It shows:
- **Market Positioning:** "Your N3 Hybrid course is priced 15% below market average but has 40% higher completion rates"
- **Competitor Moves:** "3 competitors launched JLPT N2 courses this month"
- **Opportunity:** "N1 advanced courses are underserved in Hanoi market (only 2 providers)"

She decides to fast-track development of an N1 course to capture the underserved market.

**Compliance and Auditing:**
The Ministry of Education requests proof that the center's curriculum meets JLPT standards. Instead of scrambling, Mai generates a compliance report in 5 minutes:
- ✓ All N3 courses cover 100% of JLPT N3 grammar points
- ✓ Question bank validated against official JLPT sample tests
- ✓ Instructor certifications on file
- ✓ Student progress tracking meets educational standards

She emails the PDF report to the Ministry. Audit passed.

**GDPR Compliance:**
Mai notices they have 12 students from Europe. She checks the GDPR compliance dashboard:
- ✓ Data processing consent collected
- ✓ Right to erasure workflow implemented
- ✓ Data export capability available
- ⚠️ Privacy policy needs update for new AI features

She tasks her legal team to update the privacy policy before the next enrollment cycle.

**Financial Reconciliation:**
The Financial Reconciliation feature saves her hours of manual checking. Every VNPay transaction is automatically matched with enrollment records. When there's a discrepancy, she gets an alert immediately instead of discovering it weeks later during monthly accounting.

**The Resolution:**
Three months later, student retention is back up to 82% thanks to the early intervention policy. Mai uses the revenue analytics to identify that Hybrid courses are their most profitable offering. The center is now data-driven, compliant, and strategically positioned for growth.

### Journey 5: Developer Duc - From API Skeptic to Integration Champion

**The Struggle:**
Duc is a developer at an educational consulting firm. His company wants to integrate their student management system with Torii Nihongo's platform. He's dealt with poorly documented APIs before - it usually means weeks of trial and error.

**Discovery:**
Duc visits Torii Nihongo's developer portal and finds comprehensive API documentation with OpenAPI/Swagger specs. There are clear authentication examples using JWT, rate limiting policies, and even sample code in multiple languages.

**The Transformation:**
Within 2 hours, Duc has successfully authenticated and made his first API call.

**Webhook Reliability:**
He implements the enrollment webhook - when his company's system enrolls a student, it triggers an API call that atomically reserves a seat. But Duc is paranoid about reliability. He asks: "What if my webhook endpoint goes down?" The documentation shows a webhook retry mechanism with exponential backoff and an event replay API. Perfect.

**Rate Limits and SLA:**
Duc needs to sync progress data for 10,000 students daily. He checks the API documentation:
- **Rate Limit:** 1000 requests/minute per API key
- **Bulk Operations:** Available for progress sync (up to 500 students per request)
- **SLA:** 99.9% uptime, <200ms p95 response time

He implements bulk sync operations. The progress sync API allows him to pull analytics daily.

**Error Handling:**
Duc writes comprehensive error handling:
- `SEAT_UNAVAILABLE` → Show alternative class times
- `PAYMENT_PENDING` → Poll payment status endpoint
- `RATE_LIMIT_EXCEEDED` → Implement exponential backoff

**The Resolution:**
The integration goes live in 3 weeks. Duc's company becomes a Torii Nihongo partner. When other developers ask about EdTech integrations, he recommends Torii Nihongo's API as the gold standard.

### Journey 6: Thầy Minh - The Content Architect

**The Struggle:**
Thầy Minh is a 45-year-old Academic Staff member who has been teaching Japanese for 20 years. He's responsible for creating the question banks, designing JLPT practice exams, and maintaining the curriculum. His current process is a nightmare: he maintains questions in Excel spreadsheets, manually checks for duplicates, and has no way to track which questions are too easy or too hard until after students take the exam.

Last month, he discovered a critical error in a grammar question AFTER 200 students had already answered it. He had to manually recalculate scores in Excel, send apology emails, and deal with angry students. He's terrified of making another mistake.

**Discovery:**
When the center adopts Torii Nihongo, Minh is shown the Academic Staff dashboard with its Content Management System. He's skeptical - he's tried "question bank software" before and it was clunky and limiting.

**The Transformation - Smart Content Creation:**
Minh starts by importing his existing 5,000-question Excel database. The system's AI analyzes each question and suggests:
- JLPT Level (N5, N4, N3, N2, N1)
- Skill category (Grammar, Vocabulary, Reading, Listening, Kanji)
- Difficulty estimate based on linguistic complexity
- Duplicate detection: "Question #2847 is 92% similar to this one"

What would have taken him weeks of manual categorization happens in 15 minutes. He reviews the AI suggestions, makes corrections where needed, and approves the import.

**Content Versioning:**
Minh needs to update the explanation for a tricky grammar point (〜ばかり vs 〜だけ). Before making the change, the system shows him:
- **Impact Analysis:** "This explanation appears in 12 lessons, 8 quiz questions, and 3 practice exams"
- **Active Students:** "47 students are currently studying modules containing this content"
- **Version Control:** "Create new version or update existing?"

He chooses to create a new version (v2.0) so existing students aren't disrupted mid-course. New enrollments get the updated content automatically.

**Peer Review Workflow:**
Minh creates 50 new N2 grammar questions for next month's exam. Instead of publishing them immediately, he submits them for peer review. Two other Academic Staff members (Cô Lan and Thầy Tuan) receive notifications.

Cô Lan flags 3 questions: "These are too ambiguous - multiple answers could be correct." Thầy Tuan suggests improvements to 5 questions. Minh revises based on their feedback. The collaborative review catches issues before students ever see them.

**The Crisis - Question Invalidation:**
One day, a sharp student points out that Question #4521 has a factual error - the example sentence uses an outdated kanji form that's no longer standard. Minh verifies the student is correct.

He opens the Question Management interface and selects "Invalidate Question." The system shows:
- **Exam Impact:** "This question appears in 3 active practice exams"
- **Student Impact:** "127 students have answered this question in the last 30 days"
- **Recalculation:** "Scores will be recalculated excluding this question"

Minh confirms the invalidation. The system:
1. Removes the question from all future exams
2. Recalculates scores for all affected students (adjusting the total points)
3. Sends automated notifications to affected students explaining the correction
4. Logs the change in the audit trail

What used to be a week-long manual nightmare is resolved in 5 minutes with full transparency.

**Curriculum Migration:**
The JLPT organization releases updated N3 grammar guidelines. Minh needs to migrate 200+ questions to align with the new standards. The system provides a migration wizard:
1. Identifies questions affected by the guideline changes
2. Suggests updates based on the new standards
3. Creates a staging environment to test the changes
4. Allows gradual rollout (10% of students → 50% → 100%)

**The Resolution:**
Six months later, Minh has created 2,000 new high-quality questions, all peer-reviewed and properly categorized. The question bank has zero duplicates, clear difficulty ratings, and full version control. He finally sleeps well at night, knowing the content quality is bulletproof.

### Journey 7: Chị Lan - The Financial Guardian

**The Struggle:**
Chị Lan is the Financial Staff member responsible for payment reconciliation, refund processing, and financial reporting. Every month, she spends 3 days manually matching VNPay transactions with enrollment records in Excel. Discrepancies are common.

Refund requests are even worse. Last month, a VNPay refund succeeded but their database update failed. The student got their money back but still had access to the course. It took 2 weeks to discover the discrepancy.

**Discovery:**
When Torii Nihongo launches, Lan is shown the Financial Dashboard with automated reconciliation and atomic refund workflows.

**The Transformation - Automated Reconciliation:**
Monday morning, Lan opens the Financial Reconciliation dashboard:
- **VNPay Balance:** ₫127,450,000
- **Internal Records:** ₫127,450,000
- **Status:** ✓ MATCHED
- **Last Sync:** 2 minutes ago

For the first time in her career, the numbers match perfectly.

**The Refund Request - Atomic Workflow:**
A student requests a refund for a Hybrid N3 course (₫5,000,000 total: ₫2,000,000 VOD + ₫3,000,000 Live). Lan opens the refund request:

**System Analysis:**
- **Refund Eligibility:** ✓ Within 7-day window, no live attendance
- **Refund Amount:** ₫3,000,000 (Live portion only - VOD is non-refundable after activation)

Lan reviews the calculation and approves. The system executes an **atomic transaction:**

1. Initiate VNPay refund (₫3,000,000)
2. Update enrollment status (Hybrid → VOD-only) & Revoke live class access
3. Send confirmation email

The entire workflow completes in 30 seconds. If VNPay fails, the entire transaction rolls back.

**Revenue Recognition:**
Lan's accountant asks: "How should we recognize revenue for a 12-week course?"
She opens the Revenue Recognition configuration:
- **Policy:** Accrual-based
- **Reporting:** IFRS 15 compliant

The system automatically generates monthly revenue reports showing Deferred Revenue vs. Recognized Revenue.

**Partial Refund Complexity:**
A student attended 4 out of 12 live classes and wants a refund. Lan uses the Partial Refund Calculator:
- **Live Portion:** ₫3,000,000
- **Classes Attended:** 4/12 = 33% (Cost Incurred: ₫1,000,000)
- **Refundable Amount:** ₫2,000,000

Transparency prevents disputes.

**The Resolution:**
Three months later, Lan's monthly reconciliation time has dropped from 3 days to 30 minutes. She catches discrepancies in real-time. The atomic refund workflow has eliminated inconsistency. Her accountant is happy because the financial reports are audit-ready.

### Journey 8: Minh's Dark Timeline - Rising from JLPT Failure

**The Struggle:**
It's been 3 months since Minh took the JLPT N3 exam. He studied hard, but when the results arrive, his heart sinks: **92/180 - FAILED**. He needed 95 to pass. He feels devastated.

**The System Responds:**
The next morning, Minh logs into Torii Nihongo and sees a notification: **"We're Sorry You Didn't Pass - But We're Here to Help You Succeed"**

**Detailed Failure Analysis:**
The AI breaks down his results:
- **Vocabulary:** 28/60 (47%) ⚠️ **CRITICAL WEAKNESS**
- **Grammar:** 38/60 (63%) ⚠️ **BELOW PASSING**

**Personalized Remediation Plan:**
Phase 1: Vocabulary Intensive (50 new words/day)
Phase 2: Reading Speed Training (Target: +25% speed)
Phase 3: Grammar Mastery + Weekly mock exams

**Community Support:**
Minh is invited to a private study group: "N3 Retake Warriors" - 15 other students who also failed. They share struggles and encourage each other.

**The Resolution:**
Four months later, Minh retakes the JLPT N3 exam. This time, he scores **132/180 - PASSED**. He realizes failure wasn't the end, but a data point for success.

### Journey 9: Cô Hana's First Week - From Nervous to Confident

**The Struggle:**
It's Cô Hana's first day as a lecturer. She's fluent in Japanese but terrified of teaching online. She has no idea how to structure a 90-minute online lesson or keep students engaged.

**Discovery - The Onboarding System:**
She finds: **"New Lecturer Onboarding - Your First Week"**

**Day 1: Platform Orientation & Test Classroom:**
Hana spends 30 minutes in the sandbox environment, practicing whiteboard tools and screen sharing.

**Day 2: Lesson Planning with Templates:**
She selects "N3 Grammar Introduction (90 min)" template. It gives her a minute-by-minute breakdown. Suddenly, she has a plan.

**Day 3: Observing Master Lecturers:**
She watches recorded classes from experienced teachers to see how they handle disengaged students and technical issues.

**Day 4: Mentor Assignment:**
She's assigned a mentor, Cô Mai, who reviews her lesson plan and offers tips. Knowing Mai will observe her first class (invisibly) calms her nerves.

**The Resolution:**
Her first class goes smoothly. Student engagement is high. Post-class feedback from her mentor highlights her strengths and offers one specific area for growth. One month later, Hana is confident enough to mentor new lecturers herself.

### Journey Requirements Summary

These narrative journeys reveal critical capabilities needed for Torii Nihongo:

**Learner Experience:**
- **Offline Learning Mode:** Downloadable content for offline study.
- **Failure Recovery:** Detailed analysis and personalized remediation plans for failed exams.
- **Accessibility:** Screen reader support and keyboard navigation.
- **Community:** Retake groups and peer support.

**Lecturer & Academic:**
- **Onboarding:** structured program with templates and mentorship.
- **Content Management:** Version control, impact analysis, and peer review workflows.
- **Dispute Resolution:** Grade override capabilities with audit trails.
- **Question Bank:** Smart import and duplicate detection.

**Operations & Financial:**
- **Financial Integrity:** Atomic refund workflows and real-time reconciliation.
- **Reporting:** GAAP/IFRS compliant financial reports.
- **Disaster Recovery:** Protocols for system outages during live classes.
- **Capacity Planning:** Forecasting tools for enrollment surges.

**Integration:**
- **Reliability:** Webhook retries, event replay, and bulk operations.
- **Transparency:** Clear SLA and rate limit documentation.

## Innovation & Novel Patterns

Torii Nihongo introduces several breakthrough innovations that differentiate it from traditional EdTech platforms and create genuine competitive advantages in the Japanese language learning market.

### Detected Innovation Areas

**1. AI Multi-Agent Architecture (Cortex via FastMCP)**

The system employs a **real-time multi-agent AI architecture** using the FastMCP protocol, enabling multiple specialized AI agents to collaborate during live learning sessions:

- **Sensei Agent**: Provides instant contextual explanations and grammar corrections during live classes
- **Assessment Agent**: Performs draft grading and generates adaptive practice tests based on learner weaknesses
- **Analytics Agent**: Continuously analyzes learning patterns to predict JLPT scores and recommend personalized study paths

**Innovation**: Unlike traditional EdTech platforms that use batch AI processing (analyze → wait → respond), Torii Nihongo's FastMCP-based agents operate in **real-time during live WebRTC sessions**, providing sub-3-second responses while students are actively learning. This transforms AI from a post-class review tool into an active teaching assistant.

**2. Real-time Kanji Handwriting Feedback**

The platform analyzes **Kanji stroke order in real-time** as students write on the collaborative whiteboard during live classes:

- Computer vision analyzes each stroke as it's drawn
- AI validates stroke order against standard writing rules
- Instant visual feedback highlights errors before the student completes the character
- Lecturer sees AI suggestions and can override or reinforce the feedback

**Innovation**: This is a **novel interaction pattern** that combines WebRTC whiteboard technology with real-time computer vision AI. Most language learning apps analyze handwriting after submission; Torii Nihongo provides feedback **during the writing process**, mimicking how a physical teacher would correct students in real-time.

**3. Hybrid Learning Engine with Atomic Seat Reservation**

The platform seamlessly integrates **Video-on-Demand (VOD) content with Live Online Classes** using a flipped classroom model:

- Students watch pre-recorded theory videos at their own pace (VOD)
- Live classes focus on interactive practice, Q&A, and real-time feedback
- Atomic transaction ensures payment + seat reservation happen together (no overbooking)
- Distributed lock on NATS prevents race conditions during high-demand enrollment

**Innovation**: While many platforms offer either VOD or Live classes, few successfully integrate both with **atomic enrollment guarantees**. The use of distributed locking via NATS for seat reservation is a **novel technical approach** that solves the "payment succeeded but class is full" problem that plagues competitors.

**4. Adaptive JLPT Analytics with Failure Recovery**

The system provides **5-pillar JLPT scoring** (Vocabulary, Grammar, Reading, Listening, Kanji) with AI-powered score prediction and personalized remediation:

- Continuous tracking of learner performance across all 5 pillars
- AI predicts JLPT exam score based on practice test trends
- When a learner fails JLPT, the system automatically generates a **personalized remediation plan** targeting specific weaknesses
- Community support groups connect learners who failed the same level for peer encouragement

**Innovation**: Most EdTech platforms abandon learners after exam failure. Torii Nihongo treats failure as a **data point for personalized recovery**, automatically creating study plans and connecting learners with peers. This **data-driven compassion** approach is rare in the industry.

### Market Context & Competitive Landscape

**Why These Innovations Haven't Been Done Before:**

1. **Technical Complexity**: Real-time AI during live WebRTC requires sophisticated event-driven architecture (NATS) and low-latency AI inference. Most EdTech companies lack this technical capability.

2. **Cost Constraints**: Running AI agents in real-time is more expensive than batch processing. Competitors prioritize cost over experience.

3. **Integration Challenges**: Combining VOD + Live + AI + Payment atomicity requires deep systems thinking. Most platforms focus on one modality.

4. **Cultural Barriers**: Japanese language learning has traditionally been instructor-centric. Introducing AI as a "teaching assistant" requires cultural acceptance.

**Competitive Advantages:**

- **Duolingo/Busuu**: VOD-only, no live classes, no real-time AI feedback
- **iTalki/Preply**: Live-only, no structured curriculum, no AI assistance
- **Rosetta Stone**: Outdated pedagogy, no live component, no AI
- **Torii Nihongo**: Combines all three (VOD + Live + AI) with atomic guarantees

### Validation Approach

**How We Prove These Innovations Work:**

**1. AI Multi-Agent Validation**

- **Accuracy Metrics**: Track AI Sensei's answer accuracy vs. lecturer corrections (Target: >90% agreement)
- **Response Time**: Measure AI response latency (Target: <3 seconds p95)
- **Fallback Strategy**: If AI confidence <70%, defer to lecturer instead of showing incorrect answer
- **A/B Testing**: Compare learner outcomes in AI-assisted vs. non-AI-assisted classes

**2. Kanji Handwriting Recognition Validation**

- **Stroke Order Accuracy**: Validate against JLPT official stroke order database (Target: >95% accuracy)
- **Latency Testing**: Measure end-to-end latency (WebRTC → AI → Feedback) (Target: <500ms)
- **User Acceptance**: Survey learners on whether real-time feedback helps vs. distracts (Target: >80% positive)
- **Fallback Strategy**: If latency >1 second, disable real-time feedback and switch to post-submission analysis

**3. Hybrid Model Validation**

- **Completion Rates**: Compare Hybrid course completion vs. VOD-only and Live-only (Hypothesis: Hybrid >30% higher)
- **Engagement Metrics**: Track VOD watch time before live classes (Target: >70% of students watch prep videos)
- **Seat Reservation Testing**: Stress test distributed lock under concurrent enrollment (Target: 0 overbookings in 10,000 transactions)
- **Fallback Strategy**: If distributed lock fails, fall back to pessimistic database locking (slower but guaranteed)

**4. Adaptive Analytics Validation**

- **Prediction Accuracy**: Compare AI-predicted JLPT scores vs. actual exam results (Target: ±10 points accuracy)
- **Remediation Effectiveness**: Track retake pass rates for learners who followed remediation plans (Target: >70% pass on second attempt)
- **Community Impact**: Measure engagement in "Retake Warriors" support groups (Target: >50% active participation)

### Risk Mitigation

**Innovation Risks & Fallback Strategies:**

**Risk 1: AI Gives Wrong Answers During Live Class**
- **Mitigation**: Confidence threshold (only show answers >70% confidence)
- **Fallback**: Lecturer can override AI suggestions with one click
- **Monitoring**: Track AI accuracy metrics daily and retrain models if accuracy drops below 85%

**Risk 2: Real-time Kanji Feedback Has High Latency**
- **Mitigation**: Edge computing for AI inference (deploy models closer to users)
- **Fallback**: Disable real-time mode and switch to post-submission analysis if latency >1s
- **Monitoring**: Alert if p95 latency exceeds 500ms

**Risk 3: Distributed Lock Causes Overbooking**
- **Mitigation**: Comprehensive integration testing with race condition simulations
- **Fallback**: Pessimistic database locking as backup (slower but guaranteed correctness)
- **Monitoring**: Alert on any enrollment where payment succeeded but seat unavailable

**Risk 4: Learners Skip VOD and Only Attend Live Classes**
- **Mitigation**: Require 80% VOD completion before unlocking live class access
- **Fallback**: Lecturer can manually override for exceptional cases
- **Monitoring**: Track VOD completion rates and correlate with live class performance

**Risk 5: AI Score Predictions Are Inaccurate**
- **Mitigation**: Continuous model retraining with actual JLPT results
- **Fallback**: Display prediction as "estimated range" (±15 points) rather than exact score
- **Monitoring**: Track prediction error monthly and retrain if error >15 points

**Risk 6: Remediation Plans Don't Improve Retake Pass Rates**
- **Mitigation**: A/B test remediation plans vs. self-study control group
- **Fallback**: Offer human tutor intervention for learners who fail twice
- **Monitoring**: Track retake pass rates quarterly and adjust remediation algorithms

### Implementation Considerations

**Phased Rollout Strategy:**

**Phase 1 (MVP - Weeks 1-10):**
- Basic AI Sensei (Q&A only, no real-time feedback)
- Hybrid model with manual seat reservation (no distributed lock yet)
- Simple JLPT analytics (no score prediction)

**Phase 2 (Post-Graduation - Months 4-6):**
- Real-time AI feedback during live classes
- Distributed lock for atomic seat reservation
- AI score prediction with ±15 point accuracy

**Phase 3 (Production - Months 7-12):**
- Real-time Kanji handwriting analysis
- Multi-agent AI collaboration (Sensei + Assessment + Analytics)
- Automated remediation plans with community support groups

**Technical Dependencies:**
- **NATS Event-Driven Architecture**: Required for real-time AI and distributed locking
- **FastMCP Protocol**: Required for multi-agent AI coordination
- **WebRTC Infrastructure**: Required for live classes and whiteboard collaboration
- **Computer Vision Models**: Required for Kanji stroke analysis (TensorFlow/PyTorch)
- **Low-Latency AI Inference**: Required for <3s response times (GPU acceleration or edge deployment)

**Success Criteria:**
- AI Sensei accuracy >90% vs. lecturer corrections
- Real-time feedback latency <500ms p95
- Hybrid course completion rates >30% higher than VOD-only
- JLPT score prediction accuracy ±10 points
- Retake pass rates >70% for remediation plan followers
- Zero overbooking incidents in production
