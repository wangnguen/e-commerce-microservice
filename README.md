# Dự án e-commerce

Dự án này là một hệ thống thương mại điện tử được xây dựng dựa trên **kiến trúc microservice**.

## Các service cốt lõi

- Identity Service - Quản lý định danh
- Catalog Service - Quản lý sản phẩm
- Order Service - Quản lý đơn hàng
- Inventory Service - Quản lý tồn kho
- Payment Service - Thanh toán

Tất cả được điều phối qua **API Gateway** và sử dụng **Docker** để dễ dàng triển khai.

---

## Getting Started

Hướng dẫn từ cài đặt, chạy thử, khám phá hệ thống đến gọi API.

---

## 1. Yêu cầu cài đặt

Hãy đảm bảo máy tính đã có sẵn:

**Docker Desktop**

- [Tải tại đây](https://www.docker.com/products/docker-desktop/)
- Sau khi cài đặt, hãy khởi động Docker Desktop và đợi đến khi nó chạy ổn định.

**Git**

- [Tải tại đây](https://git-scm.com/downloads)

**IntelliJ IDEA & JDK 21** (Tùy chọn - nếu muốn nghiên cứu mã nguồn)

- [Tải IntelliJ IDEA Community](https://www.jetbrains.com/idea/download/)
- [Tải OpenJDK 21](https://jdk.java.net/21/)

---

## 2. Tải mã nguồn

Mở terminal và chạy:

```bash
git clone https://github.com/wangnguen/e-commerce-microservice.git
```

---

## 3. Build chương trình với docker

Chạy lệnh để build và khởi chạy toàn bộ hệ thống:

```bash
docker-compose up --build -d
```

**Tùy chọn:**

- `--build`: buộc Docker build lại các image (lần đầu sẽ hơi lâu)
- `-d`: chạy ở chế độ background (detached mode)

Lần chạy đầu tiên Docker sẽ tải Java, Maven, RabbitMQ và biên dịch mã nguồn. Các lần sau sẽ nhanh hơn nhiều.

---

## 4. Kiểm tra và Khám phá hệ thống

Sau khi khởi động thành công, bạn có thể truy cập vào các công cụ sau:

### 4.1. Eureka Dashboard

[http://localhost:8761](http://localhost:8761)

Tại đây bạn sẽ thấy tất cả các microservice đã đăng ký và đang chạy.

### 4.2. RabbitMQ Dashboard

[http://localhost:15672](http://localhost:15672)

Đăng nhập bằng:

- Username: guest
- Password: guest

### 4.3. Swagger UI

[http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)

Đây là nơi bạn có thể xem toàn bộ API và thực hành gọi thử.

---

## 5. Thực hành gọi API

### 5.1. Đăng nhập để lấy Token

Để gọi được các API bảo vệ, bạn cần lấy access token.

**Endpoint:**

```
POST http://localhost:8080/identity-service/auth/login
```

**Body (JSON):**

```json
{
	"username": "testuser",
	"password": "password123"
}
```

Kết quả trả về sẽ có `accessToken`. Hãy sao chép token này.

Nếu chưa có tài khoản, bạn có thể dùng endpoint `/register` để tạo.

### 5.2. Gọi API được bảo vệ

- Ví dụ: GET /catalog-service/api/products

  - Trên Swagger UI hoặc Postman:

  - Nhấn Authorize hoặc mở tab Authorization

  - Type: Bearer Token

  - Token: Dán token vừa nhận được

🎉 Bây giờ bạn đã có thể gọi API và nhận kết quả thành công.

---

## 6. Dừng hệ thống (Shutdown)

- Khi muốn dừng toàn bộ chương trình:
  ```bash
  docker-compose down
  ```
- Lệnh này sẽ dừng và xóa tất cả container, giải phóng môi trường.
