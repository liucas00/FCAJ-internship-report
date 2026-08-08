---
title: "Xây dựng hạ tầng mạng và bảo mật"
date: 2026-07-30
weight: 3
chapter: true
pre: " <b> 5.3. </b> "
---

### Tổng quan
Hạ tầng mạng là nền tảng cốt lõi cho sự ổn định của **Cloud Finance Platform**. Trong phần này, chúng ta sẽ thiết kế một môi trường AWS an toàn, biệt lập, tạo tiền đề vững chắc cho việc triển khai các kiến trúc microservices hiện đại.

### Mục tiêu triển khai
Việc xây dựng hệ thống mạng tập trung vào việc hiện thực hóa các yêu cầu khắt khe về bảo mật và khả năng mở rộng:

*   **Thiết lập VPC:** Tạo một Amazon VPC riêng biệt, đóng vai trò là "vỏ bọc" an toàn cho toàn bộ hệ thống.
*   **Phân tầng Subnet:** Phân tách rõ ràng giữa **Public Subnets** (dành cho các dịch vụ tiếp xúc Internet) và **Private Subnets** (dành cho các dịch vụ nội bộ quan trọng).
*   **Kiểm soát luồng dữ liệu:** Thiết lập các **Security Groups** nghiêm ngặt nhằm quản lý lưu lượng truy cập giữa các thành phần, hạn chế tối đa các nguy cơ bảo mật.

### Sơ đồ kiến trúc
Dưới đây là mô hình mạng tổng quan mà chúng ta sẽ hiện thực hóa:

![Kiến trúc mạng](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.3-S3-vpc/diagram2.png)

### Kết quả đạt được
Sau khi hoàn thiện hạ tầng này, hệ thống sẽ đáp ứng tốt các tiêu chí:
1.  **Tính bảo mật:** Phân lớp rõ ràng, bảo vệ dữ liệu nhạy cảm.
2.  **Tính linh hoạt:** Khả năng mở rộng cao, sẵn sàng phục vụ lượng truy cập lớn.
3.  **Sẵn sàng cho Microservices:** Hạ tầng được tối ưu hóa để triển khai trên **Amazon ECS Fargate** một cách mượt mà nhất.