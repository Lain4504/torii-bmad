# Danh mục API (API Contracts - Server)

Hệ thống backend sử dụng kiến trúc API Gateway (`port 8080`) để điều phối yêu cầu đến các microservices. Phần lớn các API sử dụng **Protobuf** để truyền tải dữ liệu hiệu quả giữa Backend và Mobile.

## 🎥 1. Room / Meet API (Port 8091 via Gateway)

| Endpoint | Method | Guard | Mô tả |
| :--- | :--- | :--- | :--- |
| `/auth/room/create` | `POST` | ApiKey | Tạo một phòng học WebRTC mới. |
| `/auth/room/getJoinToken` | `POST` | ApiKey | Lấy token để tham gia phòng (LiveKit token). |
| `/auth/room/isRoomActive` | `POST` | ApiKey | Kiểm tra phòng học có đang diễn ra không. |
| `/auth/room/getActiveRoomInfo` | `POST` | ApiKey | Lấy thông tin chi tiết phòng đang active. |
| `/api/endRoom` | `POST` | JwtAuth | Kết thúc phòng học (Dành cho Admin/Lecturer). |

## 👥 2. Identity API (Port 8081 via Gateway)

| Endpoint | Method | Mô tả |
| :--- | :--- | :--- |
| `/auth/login` | `POST` | Đăng nhập hệ thống, hỗ trợ Dual-mode (Web/Mobile). |
| `/auth/refresh` | `POST` | Lấy Access Token mới bằng Refresh Token. |
| `/auth/register` | `POST` | Đăng ký tài khoản người dùng mới. |
| `/users/profile` | `GET` | Lấy thông tin cá nhân của người dùng hiện tại. |

## 4. NATS System Events (`sysJsWorker.{roomId}.{userId}`)

Đây là các sự kiện gửi từ Client lên Server qua NATS JetStream.

| Event Name | Enum Value | Mô tả |
| :--- | :--- | :--- |
| `REQ_INITIAL_DATA` | 1 | Yêu cầu dữ liệu khởi tạo phòng học. |
| `REQ_MEDIA_SERVER_DATA` | 3 | Yêu cầu thông tin kết nối media (LiveKit). |
| `REQ_RENEW_WAJLC_TOKEN` | 4 | Yêu cầu gia hạn Token. |
| `REQ_RAISE_HAND` | 6 | Giơ tay phát biểu. |
| `PING` | 5 | Heartbeat từ client. |

## 5. NATS Infrastructure Subjects

| Subject | Role | Mô tả |
| :--- | :--- | :--- |
| `$SYS.REQ.USER.AUTH` | Auth Callout | NATS Server gửi yêu cầu xác thực người dùng. |
| `$SYS.ACCOUNT.PNM.>` | Conn Events | Theo dõi CONNECT/DISCONNECT của người dùng. |
| `recorderTranscoderJobs` | JetStream | Hàng đợi các tác vụ xử lý video/transcoding. |

## 6. LMS API (Port 8082 via Gateway)

| Endpoint | Method | Mô tả |
| :--- | :--- | :--- |
| `/courses` | `GET` | Danh sách các khóa học (hỗ trợ filter theo JLPT level). |
| `/courses/:id` | `GET` | Chi tiết khóa học bao gồm danh sách bài học. |
| `/learning/progress` | `GET` | Lấy tiến độ học tập cá nhân. |

---
**Ghi chú kỹ thuật:**
- Các request/response payload được định nghĩa trong `packages/protocol/proto/`.
- Hầu hết các API liên quan đến Live/Real-time đều yêu cầu `ApiKeyGuard` hoặc `JwtAuthGuard`.

---
[Quay lại trang chủ](./index.md)
