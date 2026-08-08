---
title: "Khởi tạo Tầng dữ liệu & Quản lý cấu hình"
date: 2026-07-31
weight: 4
chapter: true
pre: "<b> 5.4. </b>"
---

### Định hướng triển khai Data Layer

Trong phần này, mình tập trung xây dựng một tầng dữ liệu độc lập để phục vụ xuyên suốt cho Cloud Finance Platform[cite: 4]. Thay vì gắn chặt với tầng ứng dụng, việc tách biệt kiến trúc Data Layer mang lại sự linh hoạt, tối ưu bảo mật và tăng cường độ tin cậy cho toàn bộ hệ thống[cite: 4].

### Triển khai các dịch vụ lưu trữ và bảo mật

Mình kết hợp ba dịch vụ AWS chuyên biệt nhằm xử lý trọn vẹn bài toán lưu trữ dài hạn, bộ nhớ đệm tốc độ cao và quản lý cấu hình an toàn:

*   **Amazon RDS (PostgreSQL):** Mình thiết lập RDS làm cơ sở dữ liệu quan hệ cốt lõi của nền tảng[cite: 4]. Dịch vụ này chịu trách nhiệm lưu trữ bền vững và đảm bảo tính toàn vẹn tuyệt đối cho mọi giao dịch tài chính quan trọng[cite: 4].
*   **Amazon ElastiCache (Redis):** Để tăng tốc độ truy xuất dữ liệu tạm thời, mình triển khai hệ thống bộ nhớ đệm (in-memory cache) này[cite: 4]. Redis giúp giảm tải đáng kể các truy vấn nặng lên cơ sở dữ liệu chính và cải thiện thời gian phản hồi của hệ thống[cite: 4].
*   **AWS Secrets Manager:** Mình sử dụng dịch vụ này làm trung tâm bảo vệ các thông tin nhạy cảm (như mật khẩu DB, API Keys)[cite: 4]. Quá trình này giúp mình loại bỏ triệt để rủi ro lộ lọt thông tin do lưu trữ trực tiếp (hardcode) trong source code[cite: 4].

### Sơ đồ giao tiếp mạng dữ liệu

Hình ảnh dưới đây minh họa cách các thành phần dữ liệu và quản lý bí mật tương tác với nhau bên trong phân vùng mạng kín Private Subnets:

![Kiến trúc Data Layer](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Data-layer/database-diagram.png)

### Đánh giá kết quả

Sau khi hoàn tất bước này, hạ tầng dữ liệu đã được cấu hình hoàn chỉnh và an toàn[cite: 4]. Hệ thống đạt được độ mở rộng cần thiết, đồng thời tối ưu hóa quá trình vận hành, tạo tiền đề lý tưởng để mình tiến hành kết nối liền mạch với các cụm Microservices trong giai đoạn tiếp theo[cite: 4].