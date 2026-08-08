---
title: "Tạo Amazon RDS PostgreSQL"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b> 5.4.1. </b>"
---

### Khởi tạo Cơ sở dữ liệu chính
Bước đầu tiên trong việc thiết lập tầng dữ liệu là khởi tạo một instance PostgreSQL trên Amazon RDS để lưu trữ dữ liệu của các microservices.

#### Hướng dẫn cấu hình
Thực hiện theo các bước sau trên AWS Management Console:

1. Truy cập dịch vụ **Amazon RDS** và chọn **Create database**.
2. Tại mục tùy chọn khởi tạo, chọn **Standard create**.
3. Thiết lập các thông số cơ bản cho hệ quản trị cơ sở dữ liệu:
   * **Engine options:** Chọn PostgreSQL phiên bản 15 hoặc mới hơn.
   * **Templates:** Sử dụng Free Tier hoặc Dev/Test.
   * **DB instance identifier:** Nhập `cloud-finance-postgres`.
   * **Master username:** Nhập `postgres`.
   * **Master password:** Thiết lập mật khẩu đủ mạnh và an toàn.
4. Trong phần **Connectivity** (Kết nối mạng), thiết lập như sau:
   * **Virtual private cloud (VPC):** Chọn `cloud-finance-vpc`.
   * **Public access:** Tắt quyền truy cập công khai.
   * **VPC security groups:** Gán Security Group `rds-sg`.
5. Nhấn **Create database** để bắt đầu quá trình khởi tạo cơ sở dữ liệu.

#### Áp dụng mô hình Database-per-service
Sau khi instance RDS chuyển sang trạng thái **Available**, tiến hành truy cập vào cơ sở dữ liệu và khởi tạo các logical databases riêng biệt dựa trên mô hình **Database-per-service**:

* `auth_db`
* `finance_db`
* `ai_db`
* `notifications_db`
* `planning_db`
* `recurring_db`

*Lưu ý kiến trúc:* Việc tách biệt cơ sở dữ liệu cho từng service là tiêu chuẩn quan trọng giúp hệ thống dễ mở rộng và giảm sự phụ thuộc giữa các microservices.

![Cấu hình RDS](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/rds.png)