---
title: "Khởi tạo tầng dữ liệu và quản lý cấu hình"
date: 2026-07-31
weight: 4
chapter: true
pre: " <b> 5.4. </b> "
---

### Tổng quan
Trong phần này, mình triển khai tầng dữ liệu độc lập, đóng vai trò quan trọng phục vụ cho toàn bộ hệ thống Cloud Finance Platform[cite: 9]. Việc xây dựng một Data Layer chuyên biệt là bước đi thiết yếu để đảm bảo hiệu năng và độ tin cậy của nền tảng.

### Các thành phần cốt lõi
Hệ thống sẽ được cấu hình với sự kết hợp của 3 dịch vụ AWS chuyên biệt nhằm tối ưu hóa việc lưu trữ, xử lý tốc độ cao và bảo mật:

*   **Amazon RDS PostgreSQL:** Được thiết lập để lưu trữ dữ liệu cốt lõi của ứng dụng[cite: 9]. RDS cung cấp một cơ sở dữ liệu quan hệ mạnh mẽ, đảm bảo tính toàn vẹn cho các giao dịch tài chính quan trọng.
*   **Amazon ElastiCache for Redis:** Đóng vai trò làm bộ nhớ đệm (cache), giúp tăng tốc độ xử lý dữ liệu tạm thời[cite: 9]. ElastiCache giảm tải đáng kể cho Database chính và tăng tốc độ phản hồi của các API.
*   **AWS Secrets Manager:** Công cụ quản lý vòng đời và bảo vệ các thông tin nhạy cảm như mật khẩu cơ sở dữ liệu và API Key[cite: 9]. Dịch vụ này giúp loại bỏ hoàn toàn rủi ro lộ lọt thông tin khi không cần phải lưu trữ mật khẩu trực tiếp (hardcode) trong source code.

### Sơ đồ kiến trúc tầng dữ liệu
Mô hình dưới đây mô tả cách các dịch vụ dữ liệu và cấu hình giao tiếp với nhau trong môi trường Private Subnets:

![Kiến trúc Data Layer](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Data-layer/database-diagram.png)

### Lợi ích hệ thống
Việc tách riêng tầng dữ liệu mang lại giá trị to lớn, giúp hệ thống đảm bảo tính bảo mật, khả năng mở rộng và thuận tiện trong quá trình vận hành[cite: 9]. Nền tảng dữ liệu lúc này đã hoàn toàn sẵn sàng để kết nối với các Microservices ở các bước tiếp theo.