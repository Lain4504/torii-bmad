# Phân tích cấu trúc thư mục (Source Tree Analysis)

Dự án được tổ chức dưới dạng Monorepo kết hợp với một repository di động riêng biệt. Dưới đây là phân tích các folder quan trọng nhất.

## 📁 Cấu trúc tổng thể
```text
/
├── bmad/                      # Cấu hình BMAD AI Agents & Workflows
├── torii-mobile/              # Flutter Mobile Application
└── torii-monorepo/            # Hệ sinh thái Backend & Web Clients
    ├── apps/
    │   ├── server/            # NestJS Microservices
    │   ├── web-admin/         # React Admin Dashboard
    │   ├── web-learner/       # Next.js Learning Platform
    │   └── meet/              # React WebRTC Meet Client
    ├── packages/
    │   ├── protocol/          # Định nghĩa Protobuf chung
    │   ├── schemas/           # Zod Schemas/DTOs dùng chung
    │   └── ui/                # Thư viện UI chung (shadcn/ui)
    └── infrastructure/        # Cấu hình Docker, NATS, LiveKit
```

## 🖥️ 1. Backend Service Details (`torii-monorepo/apps/server`)
Hệ thống chia thành các module nghiệp vụ độc lập (Bounded Contexts):

- **`src/modules/identity/`**: Quản lý Authentication (JWT, Refresh Token), RBAC.
- **`src/modules/lms/`**: Quản lý nội dung học tập.
- **`src/modules/meet/`**:
  - `interfaces/nats/`: Xử lý Auth Callout, System Events (`sysJsWorker`), JetStream Consumers cho Chat/Whiteboard.
  - `interfaces/http/`: API truyền thống cho Room Metadata/Polls.
- **`src/modules/cortex/`**: Nơi tích hợp các AI Agents.
- **`libs/shared/nats/`**: Chứa `NatsAuthService` và `NatsClientModule` dùng chung để giao tiếp microservice.

## 📱 2. Mobile App Details (`torii-mobile`)
Áp dụng kiến trúc **Feature-based + Riverpod**:

- **`lib/features/`**: Chia theo nghiệp vụ (Auth, Course, Flashcards, Meet).
- **`lib/data/`**: 
  - `repositories/`: Giao tiếp với Backend qua Dio.
  - `database/`: Định nghĩa Drift (SQLite) cho Offline mode.
- **`lib/core/`**: Cấu hình chung, Theme, App Config.

## 🌐 3. Web Clients Details
- **`apps/web-learner`**: Sử dụng Next.js để tối ưu SEO cho trang giới thiệu khóa học và hiệu năng cho trang học tập.
- **`apps/web-admin`**: Vite/React tối ưu cho dashboard quản trị với các bảng dữ liệu phức tạp.
- **`apps/meet`**: Một client chuyên biệt chỉ dành cho lớp học ảo, tập trung vào hiệu năng WebRTC.

---
[Quay lại trang chủ](./index.md)
