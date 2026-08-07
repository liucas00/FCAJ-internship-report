---
title : "Khởi tạo tầng dữ liệu và quản lý cấu hình"
date : 2026-07-31
weight : 4
chapter : true
pre : " <b> 5.4. </b> "
---

Trong phần này, mình triển khai tầng dữ liệu phục vụ cho toàn bộ hệ thống Cloud Finance Platform.

Các thành phần được cấu hình bao gồm Amazon RDS PostgreSQL để lưu trữ dữ liệu, Amazon ElastiCache for Redis để tăng tốc xử lý dữ liệu tạm thời và AWS Secrets Manager để quản lý các thông tin nhạy cảm như mật khẩu cơ sở dữ liệu và API Key.

Việc tách riêng tầng dữ liệu giúp hệ thống đảm bảo tính bảo mật, khả năng mở rộng và thuận tiện trong quá trình vận hành.