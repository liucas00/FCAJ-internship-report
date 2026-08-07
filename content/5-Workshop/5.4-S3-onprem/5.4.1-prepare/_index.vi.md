---
title : "Tạo Amazon RDS PostgreSQL"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

#### Tạo Amazon RDS PostgreSQL

Đầu tiên, mình khởi tạo cơ sở dữ liệu PostgreSQL trên Amazon RDS để lưu trữ dữ liệu của các microservices.

1. Truy cập dịch vụ **Amazon RDS** và chọn **Create database**.
2. Chọn **Standard create**.
3. Thiết lập các thông số:

+ **Engine:** PostgreSQL 15 hoặc phiên bản mới hơn.
+ **Template:** Free Tier hoặc Dev/Test.
+ **DB Instance Identifier:** `cloud-finance-postgres`
+ **Master Username:** `postgres`
+ **Master Password:** thiết lập mật khẩu mạnh.

4. Trong phần **Connectivity**:

+ Chọn VPC `cloud-finance-vpc`.
+ Tắt **Public Access**.
+ Gán Security Group `rds-sg`.

5. Chọn **Create database** để khởi tạo cơ sở dữ liệu.

Sau khi RDS ở trạng thái **Available**, mình tạo các logical databases theo mô hình **Database-per-service**, bao gồm:

+ `auth_db`
+ `finance_db`
+ `ai_db`
+ `notifications_db`
+ `planning_db`
+ `recurring_db`

Việc tách riêng cơ sở dữ liệu cho từng service giúp hệ thống dễ mở rộng và giảm sự phụ thuộc giữa các microservices.

![rds](/images/5-Workshop/5.4-Database/rds.png)