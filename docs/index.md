# Torii Nihongo Project Documentation

Chào mừng bạn đến với tài liệu kỹ thuật toàn diện của dự án **Torii Nihongo**. Tài liệu này được tự động tạo ra bằng cách phân tích chuyên sâu (Deep Scan) mã nguồn hiện tại của dự án.

## 📌 Tổng quan dự án

Dự án **Torii Nihongo** là một nền tảng học tiếng Nhật hiện đại, kết hợp giữa học trực tuyến qua video, ôn tập thông minh (SRS), lớp học ảo thời gian thực (WebRTC) và hỗ trợ bởi AI (Multi-Agent System).

- **Mô hình kiến trúc:** Multi-part Monorepo (TurboRepo)
- **Công nghệ chính:** NestJS, Flutter, Next.js, React, NATS, PostgreSQL.

## 🧭 Điều hướng tài liệu

### 🏗️ Kiến trúc & Hệ thống
- [**Tổng quan dự án**](./project-overview.md) - Tầm nhìn, chức năng chính và sơ đồ hệ thống.
- [**Phân tích cấu trúc thư mục**](./source-tree-analysis.md) - Giải thích chi tiết các folder và trách nhiệm của từng phần.
- [**Kiến trúc tích hợp**](./integration-architecture.md) - Cách các thành phần giao tiếp qua NATS và HTTP.

### 💻 Thành phần dự án (Parts)

#### 1. Backend Ecosystem (`torii-monorepo/apps/server`)
- [**Tài liệu Backend**](./architecture-server.md)
- [**Danh mục API (API Contracts)**](./api-contracts-server.md)
- [**Mô hình dữ liệu (Data Models)**](./data-models-server.md)

#### 2. Mobile App (`torii-mobile`)
- [**Tài liệu Mobile**](./architecture-mobile.md)
- [**Dữ liệu Local (Offline DB)**](./data-models-mobile.md)

#### 3. Web Clients
- [**Web Learner (Next.js)**](./architecture-web-learner.md)
- [**Web Admin (React)**](./architecture-web-admin.md)
- [**Meet Web Client (Specialized WebRTC)**](./architecture-meet-web.md)

### 🚀 Hướng dẫn phát triển
- [**Hướng dẫn cài đặt & Chạy dự án**](./development-guide.md)
- [**Hướng dẫn Deployment**](./deployment-guide.md)

---
*Tài liệu được khởi tạo bởi BMAD Analyst Agent vào ngày 2026-01-02.*
