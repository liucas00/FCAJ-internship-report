---
title: "Xây dựng hạ tầng mạng và bảo mật"
date: 2026-07-30
weight: 3
chapter: true
pre: "<b> 5.3. </b>"
---

### Mục tiêu kiến trúc mạng

Để đảm bảo an toàn cho ứng dụng và cơ sở dữ liệu, tôi chuẩn bị một môi trường mạng nội bộ (VPC) được thiết kế khép kín và phân tầng rõ ràng. 

Chiến lược ở đây là tách biệt luồng truy cập thành hai vùng:

*   **Public Subnet**: Khu vực tiếp xúc trực tiếp với Internet. Tôi sẽ đặt Load Balancer tại đây để nhận traffic từ ngoài vào.
*   **Private Subnet**: Khu vực bảo mật cao, cách ly hoàn toàn với Internet. Vùng này chỉ cho phép truy cập nội bộ và được dùng để triển khai các container ứng dụng cùng hệ cơ sở dữ liệu.

### Triển khai Amazon VPC

Tôi tiến hành khởi tạo mạng riêng ảo với các thông số được tối ưu cho Cloud Finance Platform. Các bước thực hiện như sau:

1. Đăng nhập vào AWS Management Console và truy cập dịch vụ **VPC**.
2. Tại màn hình **VPC Dashboard**, nhấn nút **Create VPC**.
3. Chọn tùy chọn **VPC and more** để hệ thống tự động khởi tạo các tài nguyên liên đới.
4. Thiết lập các thông số cấu hình mạng:
    *   **Name tag auto-generation**: `cloud-finance-vpc`
    *   **IPv4 CIDR block**: `10.0.0.0/16`
    *   **Tenancy**: `Default`
    *   **Number of Availability Zones (AZs)**: `2` (chọn các vùng như `ap-southeast-1a` và `ap-southeast-1b` để đảm bảo tính dự phòng).
    *   **Number of public subnets**: `2`
    *   **Number of private subnets**: `4` (chia đều 2 subnet cho cụm ECS và 2 subnet cho Database).
    *   **NAT gateways**: Chọn `1 NAT gateway` (đặt ở chế độ Single AZ để tối ưu chi phí).
    *   **VPC endpoints**: Không chọn (None).
5. Nhấn **Create VPC** và chờ AWS hoàn tất việc thiết lập hạ tầng.

![Kết quả tạo VPC](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/vpc-created.png)

### Thiết lập Security Groups

Tiếp theo, tôi định nghĩa 4 nhóm Security Groups. Bằng việc áp dụng quy tắc đặc quyền tối thiểu (least privilege), tôi đảm bảo các tài nguyên chỉ có thể giao tiếp với đúng các thành phần được phép.

*   **`alb-sg` (Dành cho Load Balancer):** Cho phép luồng truy cập (Inbound traffic) từ mọi nơi (`0.0.0.0/0`) thông qua cổng `80` (HTTP) và `443` (HTTPS).
*   **`ecs-sg` (Dành cho Microservices):** Giới hạn Inbound traffic ở cổng `8000`, chỉ nhận luồng dữ liệu đi vào từ `alb-sg`. Các dịch vụ trong nhóm này được phép giao tiếp nội bộ với nhau.
*   **`rds-sg` (Dành cho PostgreSQL):** Cho phép kết nối Inbound qua cổng `5432` và chỉ nhận request từ `ecs-sg`. Tuyệt đối không mở ra Internet.
*   **`redis-sg` (Dành cho ElastiCache Redis):** Mở cổng Inbound `6379` chỉ cho nguồn truy cập từ `ecs-sg` để phục vụ hoạt động của Notification Worker.

![Cấu hình Security Groups](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/security-groups.png)