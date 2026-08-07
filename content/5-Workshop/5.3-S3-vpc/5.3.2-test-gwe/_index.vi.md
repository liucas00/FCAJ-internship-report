---
title : "Cấu hình Security Groups"
date : 2026-07-30
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Cấu hình Security Groups

Sau khi hoàn thành VPC, mình tiến hành cấu hình các Security Groups để kiểm soát lưu lượng truy cập giữa các thành phần của hệ thống.

Mình tạo bốn Security Groups như sau:

+ **alb-sg**
    + Cho phép HTTP (80) và HTTPS (443) từ Internet.

+ **ecs-tasks-sg**
    + Cho phép Application Load Balancer truy cập vào các container thông qua cổng 8000.
    + Cho phép các microservices giao tiếp nội bộ với nhau.

+ **rds-sg**
    + Chỉ cho phép kết nối PostgreSQL (5432) từ `ecs-tasks-sg`.
    + Không cho phép truy cập trực tiếp từ Internet.

+ **redis-sg**
    + Chỉ cho phép kết nối Redis (6379) từ `ecs-tasks-sg`.

Sau khi cấu hình xong, toàn bộ tài nguyên trong hệ thống chỉ giao tiếp thông qua các Security Groups được chỉ định, giúp tăng cường tính bảo mật cho môi trường triển khai.

![security-group](/images/5-Workshop/5.3-Networking/security-groups.png)