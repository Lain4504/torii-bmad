---
stepsCompleted: [1, 2]
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
lastStep: 2
---

# Product Requirements Document - torii-nihongo

**Author:** tienh
**Date:** 2026-01-02 20:50

## Executive Summary

Torii Nihongo (SP26SE005) là một giải pháp EdTech toàn diện được thiết kế để hợp nhất trải nghiệm học tiếng Nhật đang bị phân mảnh. Hệ thống cung cấp một lộ trình học tập JLPT khép kín từ học lý thuyết qua video, ôn tập thông minh bằng Flashcards (SRS), đến thực hành tương tác trong các lớp học ảo WebRTC chất lượng cao. Điểm đột phá của dự án nằm ở hệ thống Multi-Agent AI (Sensei, Assessment, Analytics) dựa trên giao thức FastMCP, cung cấp khả năng phản hồi thời gian thực và cá nhân hóa lộ trình học cho từng học viên.

### What Makes This Special

- **Hệ sinh thái AI FastMCP:** Sử dụng mô hình Multi-Agent để hỗ trợ học viên 24/7 từ giải đáp ngữ pháp đến đánh giá năng lực thử nghiệm JLPT với độ trễ cực thấp.
- **Lớp học ảo tương tác sâu:** WebRTC không chỉ dừng lại ở Video/Audio mà tích hợp Whiteboard thời gian thực (hỗ trợ AI nhận diện chữ viết Kanji) và quản lý tài liệu tập trung với phân quyền chi tiết.
- **Lộ trình học tập thích ứng:** Tự động hóa việc theo dõi tiến độ và đề xuất bài tập thông qua Analytics Agent, giúp tối ưu hóa việc ôn luyện JLPT.
- **Vận hành thông minh:** Cung cấp công cụ quản trị mạnh mẽ (Bulk Import, Revenue Analytics) giúp trung tâm Nhật ngữ tối ưu hóa quy trình làm việc của Staff và Lecturers.

## Project Classification

**Technical Type:** Web Application & Mobile Application (Cross-platform)
**Domain:** EdTech (Education Technology)
**Complexity:** High (Real-time AI, WebRTC, Event-Driven Architecture)
**Project Context:** Brownfield - Nâng cấp dựa trên hạ tầng NATS/Microservices sẵn có.

### Strategic Key Features (High-Level User Stories)
- **AI Feedback:** Phản hồi sửa lỗi viết tay Kanji thời gian thực trên Whiteboard lớp học.
- **Resource Control:** Phân quyền xem/chỉnh sửa tài liệu học tập linh hoạt trong My Folders.
- **Quality Control (Staff):** Quản lý vòng đời ngân hàng câu hỏi (Draft -> Review -> Published) để đảm bảo chất lượng đề thi.
- **Real-time Operations Dashboard:** Staff giám sát trạng thái lớp học WebRTC trực tiếp để hỗ trợ kỹ thuật ngay lập tức.
- **Exam Analytics:** Quản lý Profile điểm số và theo dõi xu hướng phát lực của học viên theo thời gian.
- **Dynamic Couponing:** Thiết lập quy trình khuyến mãi linh hoạt (giới hạn số lượng, đối tượng mục tiêu).
- **Revenue Analytics:** Báo cáo doanh thu chi tiết theo giảng viên và hiệu quả chiến dịch marketing.

## Detailed Functional Requirements - AI (Cortex Service)

Hệ thống AI Multi-Agent (Sensei, Assessment, Analytics) dựa trên giao thức FastMCP và hạ tầng NATS để cung cấp phản hồi siêu nhanh (low-latency).

### 1. Sensei Agent (Trợ lý học tập 24/7)
- **US.AI.01 (Contextual Q&A):** AS A Learner, tôi có thể bôi đen một từ vựng hoặc ngữ pháp trong bài học và hỏi AI Sensei để nhận được giải thích ngay lập tức về ý nghĩa, cách dùng và các ví dụ tương tự.
- **US.AI.02 (Grammar Correction):** AS A Learner, khi tôi viết một câu tiếng Nhật, AI Sensei sẽ phân tích cấu trúc ngữ pháp và gợi ý những cách diễn đạt tự nhiên hơn (Native-like).
- **US.AI.03 (Flashcard Generation):** AS A Learner, tôi có thể yêu cầu AI Sensei tạo thẻ Flashcard tự động từ một đoạn văn bản tôi đang đọc, bao gồm cả âm hán việt, Furigana và câu ví dụ.

### 2. Assessment Agent (Giám khảo JLPT thông minh)
- **US.AI.04 (Dynamic Test Creation):** AS A Learner, tôi có thể yêu cầu AI tạo ra một bài kiểm tra ngắn (Mini-test) tập trung đúng vào phần kiến thức tôi vừa học.
- **US.AI.05 (Automated Writing Feedback):** AS A Learner, sau khi tôi hoàn thành bài viết hoặc làm bài tập tự luận, AI Assessment sẽ chấm điểm và chỉ ra chính xác lỗi sai (về ngữ pháp, từ vựng, trợ từ).
- **US.AI.06 (JLPT Score Prediction):** AS A Learner, dựa trên lịch sử làm bài, AI sẽ dự đoán số điểm JLPT có thể đạt được và đưa ra cảnh báo về các vùng kiến thức yếu.

### 3. Analytics Agent (Kỹ sư lộ trình - Adaptive Learning)
- **US.AI.07 (Weakness Identification):** AS A Learner, tôi muốn hệ thống tự động nhận diện các mảng kiến thức yếu qua dữ liệu học tập và đẩy thêm bài tập liên quan vào danh sách ôn tập.
- **US.AI.08 (Customized Roadmap):** AS A Learner, Analytics Agent sẽ điều chỉnh khối lượng kiến thức và lộ trình hàng ngày dựa trên mục tiêu thi cử và tiến độ thực tế của tôi.

### 4. Meet Integration (Phản hồi thời gian thực trong lớp học)
- **US.AI.09 (Real-time Handwriting Feedback):** AS A Learner, khi tôi viết Kanji trên Whiteboard của lớp học WebRTC, AI sẽ nhận diện nét vẽ và báo lỗi ngay lập tức nếu sai thứ tự nét hoặc bộ thủ.
- **US.AI.10 (Live Transcription & Translation):** AS A Learner, trong lớp học trực tuyến, tôi có thể xem phụ đề (Live Caption) và bản dịch thời gian thực lời giảng của giáo viên.

## Detailed Functional Requirements - Gamification (Module Trò chơi hóa)

Hệ thống Gamification giúp tăng tỷ lệ giữ chân học viên (retention) và tạo động lực học tập thông qua các cơ chế tâm lý tích cực.

- **US.GAME.01 (Streak System):** AS A Learner, tôi muốn thấy chuỗi ngày học liên tiếp của mình (Streaks) để duy trì thói quen học tập hàng ngày và nhận phần thưởng khi đạt các mốc lớn (7, 30, 100 ngày).
- **US.GAME.02 (Dynamic Ranking):** AS A Learner, tôi muốn tích lũy XP từ việc hoàn thành bài học, giải bài tập và tham gia lớp học WebRTC để thăng hạng (Bronze, Silver, Gold, Torii Master).
- **US.GAME.03 (Badge Collection):** AS A Learner, tôi muốn nhận huy hiệu thành tựu (Achievement Badges) khi hoàn thành các mục tiêu khó hoặc các thử thách đặc biệt từ AI Sensei.
- **US.GAME.04 (Reward Marketplace):** AS A Learner, tôi muốn sử dụng điểm tích lũy (Reward Points) để đổi các Voucher giảm giá khóa học hoặc mở khóa các nội dung AI cao cấp độc quyền.

## Detailed Functional Requirements - Staff Operations (Question Bank)

Hệ thống quản trị ngân hàng câu hỏi tập trung vào hiệu suất làm việc và giảm thiểu các thao tác thủ công cho đội ngũ vận hành (Staff & Admin).

- **US.STAFF.01 (Smart Bulk Import):** AS A Staff, tôi có thể import hàng ngàn câu hỏi từ Excel/CSV và để AI tự động bóc tách nội dung thô, gợi ý JLPT Level, kỹ năng (Skill) và đề xuất Furigana cho Kanji.
- **US.STAFF.02 (Duplicate Detection):** AS A Staff, tôi muốn hệ thống tự động cảnh báo nếu câu hỏi mới nhập có nội dung trùng lặp trên 90% với câu hỏi đã có sẵn để đảm bảo chất lượng dữ liệu.
- **US.STAFF.03 (Quick Review Dashboard):** AS A Reviewer, tôi muốn duyệt hoặc từ chối hàng loạt câu hỏi trong một giao diện danh sách tập trung, hỗ trợ phím tắt để tối ưu hóa thời gian thẩm định nội dung.
- **US.STAFF.04 (Auto-Exam Generator):** AS A Staff, tôi muốn tạo đề thi thử JLPT bằng cách thiết lập cấu trúc (Số câu, Level, Kỹ năng) để hệ thống tự động bốc ngẫu nhiên câu hỏi chưa từng xuất hiện trong các kỳ thi trước đó.

## Detailed Functional Requirements - Billing & Business Operations

Hệ thống quản lý tài chính và kinh doanh đảm bảo tính minh bạch, hỗ trợ tăng trưởng người dùng thông qua các công cụ khuyến mãi và quà tặng.

- **US.BILL.01 (Gift a Course):** AS A User, tôi có thể mua khóa học dưới dạng quà tặng; hệ thống sẽ tự động tạo và gửi mã kích hoạt (Activation Code) qua email/thông báo cho người nhận.
- **US.BILL.02 (Dynamic Coupon Rules):** AS A Staff, tôi muốn thiết lập các quy tắc khuyến mãi đa dạng (loại giảm giá, số lượng sử dụng, giới hạn khóa học hoặc đối tượng người dùng) để tối ưu chiến dịch marketing.
- **US.BILL.03 (Revenue Tracking):** AS An Admin, tôi muốn xem báo cáo doanh thu được phân bổ tự động theo từng giảng viên (hoa hồng) và hiệu quả của từng loại coupon để phục vụ kế toán và payroll.
- **US.BILL.04 (Scheduled Publishing):** AS A Staff, tôi muốn lập lịch tự động xuất bản (Publish) hoặc lưu trữ (Archive) khóa học để chủ động quản lý nội dung mà không cần thao tác thủ công tại thời điểm sự kiện.

## Detailed Functional Requirements - Lecturer Operations

Hệ thống cung cấp các công cụ mạnh mẽ để Giảng viên điều phối lớp học và tối ưu hóa hiệu suất giảng dạy.

- **US.LECT.01 (Advanced Room Control):** AS A Lecturer, tôi muốn toàn quyền điều khiển các tính năng tương tác trong phòng (Bật/Tắt Mic/Cam của học viên, khóa Whiteboard) để đảm bảo chất lượng giảng dạy.
- **US.LECT.02 (Interactive Polling):** AS A Lecturer, tôi muốn tạo và gửi các câu hỏi trắc nghiệm nhanh (Polls) ngay trong lúc giảng bài để đánh giá mức độ tiếp thu của học viên.
- **US.LECT.03 (AI Grading Assistant):** AS A Lecturer, tôi muốn AI hỗ trợ chấm nháp các lỗi ngữ pháp/từ vựng cơ bản trong bài tập để tôi có thể tập trung vào việc đưa ra các nhận xét chuyên môn sâu hơn.
- **US.LECT.04 (Digital Asset Integration):** AS A Lecturer, tôi muốn truy cập trực tiếp kho tài liệu cá nhân (My Folders) ngay trong lớp học để chia sẻ PDF/Hình ảnh lên Whiteboard một cách tức thì.
- **US.LECT.05 (Automated Session Reports):** AS A Lecturer, tôi muốn nhận báo cáo tự động sau mỗi buổi học (danh sách điểm danh, thời lượng tham gia, thống kê tương tác) để quản lý lớp học hiệu quả.
