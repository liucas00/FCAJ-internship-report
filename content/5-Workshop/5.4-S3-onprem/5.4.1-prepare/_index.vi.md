---
title: "Tạo Amazon RDS PostgreSQL"[cite: 11]
date: 2026-07-31[cite: 11]
weight: 1[cite: 11]
chapter: false[cite: 11]
pre: "<b> 5.4.1. </b>"[cite: 11]
---

### Khởi tạo Cơ sở dữ liệu chính
Bước đầu tiên trong việc thiết lập tầng dữ liệu là khởi tạo một instance PostgreSQL trên Amazon RDS để lưu trữ dữ liệu của các microservices[cite: 11].

#### Hướng dẫn cấu hình
Thực hiện theo các bước sau trên AWS Management Console:

1. Truy cập dịch vụ **Amazon RDS** và chọn **Create database**[cite: 11].
2. Tại mục tùy chọn khởi tạo, chọn **Standard create**[cite: 11].
3. Thiết lập các thông số cơ bản cho hệ quản trị cơ sở dữ liệu[cite: 11]:
   * **Engine options:** Chọn PostgreSQL phiên bản 15 hoặc mới hơn[cite: 11].
   * **Templates:** Sử dụng Free Tier hoặc Dev/Test[cite: 11].
   * **DB instance identifier:** Nhập `cloud-finance-postgres`[cite: 11].
   * **Master username:** Nhập `postgres`[cite: 11].
   * **Master password:** Thiết lập mật khẩu đủ mạnh và an toàn[cite: 11].
4. Trong phần **Connectivity** (Kết nối mạng), thiết lập như sau[cite: 11]:
   * **Virtual private cloud (VPC):** Chọn `cloud-finance-vpc`[cite: 11].
   * **Public access:** Tắt quyền truy cập công khai[cite: 11].
   * **VPC security groups:** Gán Security Group `rds-sg`[cite: 11].
5. Nhấn **Create database** để bắt đầu quá trình khởi tạo cơ sở dữ liệu[cite: 11].

#### Áp dụng mô hình Database-per-service
Sau khi instance RDS chuyển sang trạng thái **Available**, tiến hành truy cập vào cơ sở dữ liệu và khởi tạo các logical databases riêng biệt dựa trên mô hình **Database-per-service**[cite: 11]:

* `auth_db`[cite: 11]
* `finance_db`[cite: 11]
* `ai_db`[cite: 11]
* `notifications_db`[cite: 11]
* `planning_db`[cite: 11]
* `recurring_db`[cite: 11]

*Lưu ý kiến trúc:* Việc tách biệt cơ sở dữ liệu cho từng service là tiêu chuẩn quan trọng giúp hệ thống dễ mở rộng và giảm sự phụ thuộc giữa các microservices[cite: 11].

![Cấu hình RDS](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/rds.png)