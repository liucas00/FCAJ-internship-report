---
title : "Tạo Amazon VPC"
date : 2026-07-30
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

#### Tạo Amazon VPC

Đầu tiên, mình tạo một Virtual Private Cloud (VPC) để làm môi trường mạng riêng cho toàn bộ hệ thống.

1. Đăng nhập **AWS Management Console** và mở dịch vụ **Amazon VPC**.
2. Chọn **Create VPC** và chọn cấu hình **VPC and more**.
3. Cấu hình các thông số:

+ **Name tag:** `cloud-finance-vpc`
+ **IPv4 CIDR block:** `10.0.0.0/16`
+ **Availability Zones:** 2
+ **Public Subnets:** 2
+ **Private Subnets:** 4 (2 cho Application và 2 cho Database)
+ **NAT Gateway:** 1 (Single AZ)
+ Không cấu hình **VPC Endpoints** ở bước này.

4. Chọn **Create VPC** và chờ AWS hoàn tất việc khởi tạo hạ tầng mạng.

Sau khi hoàn thành, mình đã có một VPC với đầy đủ Subnets và Route Tables để phục vụ việc triển khai các dịch vụ ở các bước tiếp theo.

![vpc](/images/5-Workshop/5.3-Networking/create-vpc.png)