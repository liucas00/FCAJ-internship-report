---
title : "Cấu hình Application Load Balancer"
date : 2026-07-31
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

#### Cấu hình Application Load Balancer

Tiếp theo, mình tạo một Application Load Balancer (ALB) để tiếp nhận lưu lượng truy cập từ Internet và phân phối đến các backend services.

Quá trình cấu hình gồm:

+ Tạo Application Load Balancer với tên `cloud-finance-alb`.
+ Chọn chế độ **Internet-facing**.
+ Gắn vào VPC `cloud-finance-vpc`.
+ Sử dụng hai Public Subnets.
+ Gán Security Group `alb-sg`.
+ Tạo Target Group cho Gateway Service sử dụng cổng `8000`.
+ Cấu hình Health Check với endpoint `/health`.

Sau khi hoàn thành, ALB sẽ đóng vai trò là điểm truy cập chính cho toàn bộ hệ thống.

![alb](/images/5-Workshop/5.6-ECS/alb.png)