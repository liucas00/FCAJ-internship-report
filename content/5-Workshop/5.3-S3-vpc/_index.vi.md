---
title : "Xây dựng hạ tầng mạng và bảo mật"
date : 2026-07-30
weight : 3
chapter : true
pre : " <b> 5.3. </b> "
---

Trong phần này, mình sẽ xây dựng hạ tầng mạng làm nền tảng cho toàn bộ hệ thống Cloud Finance Platform trên AWS.

Mục tiêu là tạo một Amazon VPC riêng biệt, phân tách Public Subnets và Private Subnets, đồng thời cấu hình Security Groups để kiểm soát lưu lượng truy cập giữa các thành phần của hệ thống.

Sau khi hoàn thành, hạ tầng mạng sẽ đáp ứng các yêu cầu về bảo mật, khả năng mở rộng và sẵn sàng cho việc triển khai các microservices trên Amazon ECS Fargate.