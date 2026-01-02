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
