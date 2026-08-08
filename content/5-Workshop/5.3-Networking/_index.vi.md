---
title: "Thiết lập hạ tầng mạng (VPC)"
date: 2026-07-30
weight: 3
chapter: true
pre: "<b> 5.3. </b>"
---

### 1. Tổng quan & Mục tiêu

Để đảm bảo an toàn cho ứng dụng và cơ sở dữ liệu, chúng ta cần một môi trường mạng nội bộ (VPC) được thiết kế khép kín và phân tầng rõ ràng. 

Mục tiêu cốt lõi là tách biệt luồng truy cập thành hai vùng:
- **Public Subnet**: Khu vực tiếp xúc trực tiếp với Internet, đóng vai trò làm nơi đặt Load Balancer để nhận traffic từ ngoài vào.
- **Private Subnet**: Khu vực bảo mật cao, cách ly hoàn toàn với Internet. Vùng này chỉ cho phép truy cập nội bộ và được dùng để triển khai các container ứng dụng cùng hệ quản trị cơ sở dữ liệu.

### 2. Triển khai Amazon VPC

Tiến hành khởi tạo mạng riêng ảo với các thông số được tối ưu cho Cloud Finance Platform.

**Các bước thực hiện:**
1. Đăng nhập vào AWS Management Console, tìm kiếm và truy cập dịch vụ **VPC**.
2. Tại màn hình **VPC Dashboard**, nhấn nút **Create VPC**.
3. Chọn tùy chọn **VPC and more** để hệ thống tự động khởi tạo các tài nguyên liên đới.
4. Điền thông tin cấu hình mạng như sau:
   - **Name tag auto-generation**: Đặt tên là `cloud-finance-vpc`.
   - **IPv4 CIDR block**: Sử dụng dải mạng `10.0.0.0/16`.
   - **Tenancy**: Giữ nguyên `Default`.
   - **Number of Availability Zones (AZs)**: Chọn `2` vùng (ví dụ: `ap-southeast-1a` và `ap-southeast-1b`) để đảm bảo tính dự phòng cao.
   - **Number of public subnets**: `2`.
   - **Number of private subnets**: `4` (sẽ chia đều: 2 subnet cho cụm ứng dụng ECS và 2 subnet cho Database).
   - **NAT gateways**: Lựa chọn `1 NAT gateway` (đặt ở chế độ Single AZ nhằm tiết kiệm chi phí cho bài lab).
   - **VPC endpoints**: Không chọn (None).
5. Cuối cùng, nhấn **Create VPC** và chờ AWS hoàn tất việc thiết lập hạ tầng.

![Kết quả tạo VPC](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/vpc-created.png)

### 3. Thiết lập hệ thống tường lửa (Security Groups)

Để kiểm soát chặt chẽ luồng dữ liệu giữa các thành phần, cần định nghĩa 4 nhóm Security Groups áp dụng quy tắc đặc quyền tối thiểu (least privilege).

- **`alb-sg` (Dành cho Load Balancer):** 
  - Thiết lập cho phép luồng truy cập (Inbound traffic) từ Internet (nguồn `0.0.0.0/0`) thông qua cổng `80` (HTTP) và `443` (HTTPS).
- **`ecs-sg` (Dành cho các dịch vụ Microservices):** 
  - Giới hạn Inbound traffic chỉ mở cổng `8000`, và chỉ chấp nhận luồng dữ liệu đi vào từ `alb-sg`. Cho phép các dịch vụ nằm trong nhóm này giao tiếp nội bộ với nhau.
- **`rds-sg` (Dành cho hệ quản trị PostgreSQL):** 
  - Giới hạn kết nối Inbound qua cổng `5432` và chỉ nhận request xuất phát từ `ecs-sg`. Tuyệt đối không được mở public ra Internet.
- **`redis-sg` (Dành cho bộ nhớ đệm ElastiCache Redis):** 
  - Tương tự như database, chỉ mở cổng Inbound `6379` cho nguồn truy cập từ `ecs-sg`, đặc biệt để phục vụ hoạt động của Notification Worker.

![Cấu hình Security Groups](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/security-groups.png)