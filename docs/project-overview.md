# Tổng quan dự án Torii Nihongo

## 🎯 Mục tiêu dự án
Giải pháp lớp học trực tuyến WebRTC và AI phản hồi thời gian thực bằng FastMCP cho trung tâm Nhật Ngữ. Hệ thống giải quyết sự phân mảnh trong trải nghiệm học tập bằng cách hợp nhất:
- Học video & làm Quiz.
- Lớp học ảo tương tác (Real-time).
- Hệ thống hỗ trợ AI (Sensei, Assessment, Analytics).
- Lộ trình học tập JLPT cá nhân hóa.

## 🏗️ Kiến trúc hệ thống tổng thể (NATS-Centric Architecture)

Dự án được xây dựng dựa trên kiến trúc **Event-Driven (Kiến trúc hướng sự kiện)** với **NATS là xương sống (Backbone)**:

1.  **Giao tiếp Đồng bộ (HTTP/REST via Gateway):** Dùng cho các luồng CRUD (Identity, LMS, Blogs). Gateway đóng vai trò Proxy (cổng chào) cho toàn bộ hệ thống.
2.  **Giao tiếp Microservices (NATS Request/Reply):** Các service trong cụm microservice (Identity <-> Server) giao tiếp trực tiếp qua NATS dùng `ClientProxy` (NATS Transport).
3.  **Hệ thống phân quyền thời gian thực (NATS Auth Callout):** Đây là điểm cốt lõi. NATS Server ủy quyền cho `Gateway` (thông qua `NatsAuthCalloutService`) để cấp JWT NATS động với các quyền (Pub/Sub) cực kỳ chi tiết cho từng User dựa trên Token của họ.
4.  **Xử lý hàng đợi & Tác vụ nền (NATS JetStream):** Sử dụng `RetentionPolicy.Workqueue` để xử lý các tác vụ bất đồng bộ như:
    - `sysJsWorker`: Xử lý sự kiện từ Client (Raise Hand, Join/Leave, Media info).
    - `recorderTranscoderJobs`: Xử lý video transcoding cho Recorder.
5.  **Real-time Media (WebRTC/LiveKit):** Xử lý luồng media, được điều khiển và xác thực bởi các tokens cấp phát qua NATS.

## 🛠️ Công nghệ sử dụng

| Lớp (Layer) | Công nghệ chính |
| :--- | :--- |
| **Backend** | NestJS, Prisma ORM, PostgreSQL, Redis |
| **Giao tiếp** | **NATS Core** (Auth Callout, Pub/Sub), **NATS JetStream** (Workqueues), Protobuf |
| **Gateway** | NestJS Proxy + NATS Auth Provider |
| **AI Agents** | FastMCP, Cortex Service |
| **Web UI** | Next.js (Learner), React/Vite (Admin & Meet) |
| **Mobile App** | Flutter (Riverpod, Drift, GoRouter, NATS client) |
| **Hạ tầng** | Docker Compose, LiveKit Server, NATS Server |

## 🌟 Các tính năng cốt lõi

- **LMS (Learning Management System):** Quản lý khóa học N5-N1, bài học, tiến độ học tập.
- **Lớp học ảo (Meet):** Whiteboard tương tác, chia sẻ tài liệu, chat real-time, ghi lại bài giảng.
- **SRS Flashcards:** Thuật toán lặp lại ngắt quãng để ghi nhớ từ vựng.
- **Hệ thống AI (Cortex):** 
  - *Sensei Agent:* Giải đáp ngữ pháp, dịch thuật.
  - *Assessment Agent:* Chấm điểm và tạo đề thi JLPT.
  - *Analytics Agent:* Đề xuất lộ trình học tập dựa trên điểm yếu.
- **Gamification:** Huy hiệu, điểm thưởng và bảng xếp hạng để tăng động lực.

---
[Quay lại trang chủ](./index.md)
