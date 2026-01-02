# Kiến trúc tích hợp (Integration Architecture)

Dự án **Torii Nihongo** sử dụng NATS làm trung tâm điều phối cho cả xác thực và giao tiếp nghiệp vụ.

## 1. Luồng xác thực NATS (Auth Callout Flow)

Đây là cơ chế bảo mật quan trọng nhất, cho phép cấp quyền Pub/Sub chi tiết đến từng Subject cho mỗi User.

```text
Client (Web/Mobile)          NATS Server              Gateway (Auth Provider)
      |                          |                           |
      |-- 1. CONNECT (JWT) ----->|                           |
      |                          |-- 2. Auth Request ------->|
      |                          |   ($SYS.REQ.USER.AUTH)    |
      |                          |                           |-- 3. Verify JWT
      |                          |                           |-- 4. Map Permissions
      |                          |                           |-- 5. Sign NATS JWT
      |                          |<-- 6. Auth Response ------|
      |<-- 7. Connected ---------|                           |
```

### Chi tiết quyền hạn (Permissions Mapping):
- **Publish:**
  - `sysJsWorker.{roomId}.{userId}`: Chỉ được gửi sự kiện hệ thống của chính mình.
  - `$JS.API.STREAM.INFO.{roomId}`: Lấy thông tin stream của phòng.
- **Subscribe:**
  - `_INBOX.>` (Dành cho request-reply).
  - Tự động tạo JetStream Consumers riêng cho mỗi người dùng để nhận Chat, Whiteboard, System Events.

## 2. Luồng xử lý sự kiện hệ thống (System Events Flow)

Các hành động real-time không đi qua HTTP mà đi qua NATS JetStream để đảm bảo tính sẵn sàng và thứ tự.

- **Subject:** `sysJsWorker.{roomId}.{userId}`
- **Worker Pool:** Backend duy trì 50 workers để xử lý hàng đợi này.
- **Các sự kiện xử lý:**
  - `REQ_INITIAL_DATA`: Lấy dữ liệu khởi tạo phòng.
  - `REQ_MEDIA_SERVER_DATA`: Lấy thông tin kết nối LiveKit (xử lý broadcast).
  - `REQ_RENEW_WAJLC_TOKEN`: Gia hạn token khi sắp hết hạn.
  - `REQ_RAISE_HAND` / `REQ_LOWER_HAND`: Giơ tay phát biểu.

## 3. Giao tiếp Microservices

Sử dụng NATS Request/Reply pattern thay cho HTTP nội bộ.

- **Hệ thống:** Sử dụng `NatsClientModule` cung cấp `NATS_SERVICE` token.
- **Queue Group:** `torii_queue` được sử dụng để cân bằng tải giữa các instance của cùng một service.

## 4. Theo dõi kết nối (Connection Tracking)

Hệ thống lắng nghe sự kiện hệ thống của NATS (`$SYS.ACCOUNT.<NAME>.>`) để biết trạng thái online/offline thực tế của người dùng, từ đó cập nhật `joinedParticipants` và trigger các logic khi người dùng mất kết nối đột ngột.

---
[Quay lại trang chủ](./index.md)
