# Mô hình dữ liệu Backend (Data Models)

Dưới đây là các thực thể dữ liệu chính được quản lý bởi Prisma trong PostgreSQL.

## 📚 1. E-Learning (LMS)
- **`Course`**: Thông tin khóa học (title, jlptLevel, price, ratings, status).
- **`Module`**: Các chương trong một khóa học.
- **`Lesson`**: Bài học chi tiết (videoUrl, articleContent, order).
- **`Wishlist`**: Lưu trữ các khóa học yêu thích của người dùng.

## 👥 2. Người dùng & Phân quyền (Identity)
- **`User`**: Thông tin người dùng (email, fullName, role, status).
- **`RefreshToken`**: Quản lý phiên đăng nhập và cơ chế quay vòng token bảo mật.
- **`RolePermission` / `UserPermission`**: Hệ thống phân quyền chi tiết (RBAC).
- **`AuditLog`**: Ghi lại mọi hành động nhạy cảm trên hệ thống (ai thực hiện, hành động gì, dữ liệu cũ/mới).

## 🎥 3. Lớp học ảo (Meet)
- **`RoomInfo`**: Trạng thái phòng học (roomId, isRunning, isRecording, joinedParticipants).
- **`RoomFile`**: Các tài liệu được chia sẻ hoặc sử dụng trong phòng học.
- **`RoomAnalytics`**: Dữ liệu thống kê về việc sử dụng và tham gia phòng học.
- **`RoomArtifact`**: Các sản phẩm sinh ra sau buổi học (bản ghi, whiteboard data).

## 🧠 4. Nội dung & Công cụ học tập
- **`BlogPost` / `BlogComment`**: Hệ thống tin tức và cộng đồng.
- **`FlashcardDeck` / `Flashcard`**: Hệ thống ôn tập thẻ từ vựng với các tham số SRS (intervalDays, easeFactor, reviewCount).
- **`QuestionBank`**: Ngân hàng câu hỏi dùng cho Quiz và bài thi thử JLPT.
- **`Notification`**: Quản lý thông báo người dùng.
- **`FileAsset`**: Quản lý tập trung mọi file upload (S3/MinIO) kèm metadata.

---
[Quay lại trang chủ](./index.md)
