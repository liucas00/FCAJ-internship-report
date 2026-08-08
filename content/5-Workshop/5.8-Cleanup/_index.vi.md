---
title : "Dọn dẹp tài nguyên"
date : 2026-07-31
weight : 8
chapter : true
pre : " <b> 5.8. </b> "
---

#### Dọn dẹp tài nguyên

Sau khi hoàn thành workshop, mình tiến hành xóa các tài nguyên AWS đã tạo để tránh phát sinh chi phí không cần thiết.

Thứ tự dọn dẹp được thực hiện như sau:

1. Giảm số lượng Task của các ECS Services về `0`.
2. Xóa Application Load Balancer và các Target Groups.
3. Xóa Amazon RDS PostgreSQL và Amazon ElastiCache for Redis.
4. Xóa NAT Gateway và giải phóng Elastic IP.
5. Xóa CloudFront Distribution và S3 Bucket đã sử dụng để lưu trữ frontend.

Sau khi hoàn thành các bước trên, toàn bộ tài nguyên của workshop sẽ được gỡ bỏ và tài khoản AWS sẽ không tiếp tục phát sinh chi phí từ môi trường thử nghiệm.