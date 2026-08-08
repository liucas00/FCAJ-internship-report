---
title: "Tạo Amazon ElastiCache for Redis"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b> 5.4.2. </b>"
---

### Triển khai Bộ nhớ đệm (In-Memory Data Store)
Tiếp theo, hệ thống yêu cầu triển khai Amazon ElastiCache for Redis để cung cấp giải pháp lưu trữ dữ liệu tạm thời tốc độ cao. Redis đóng vai trò cốt lõi trong việc quản lý bộ nhớ đệm (caching) và hỗ trợ xử lý các tác vụ bất đồng bộ, qua đó cải thiện đáng kể hiệu năng tổng thể của ứng dụng.

#### Hướng dẫn cấu hình
Thực hiện các bước sau để khởi tạo Redis Cluster:

1. Truy cập vào bảng điều khiển dịch vụ **Amazon ElastiCache**.
2. Tại menu điều hướng, chọn **Redis Caches** và bắt đầu quá trình tạo một Redis Cluster mới.
3. Thiết lập các thông số cơ bản cho Cluster:
   * **Cluster Name (Tên cụm):** Nhập `cloud-finance-redis`.
   * **Node Type (Loại Node):** Chọn `cache.t4g.micro`.
   * **Replicas (Bản sao):** Đặt là `0`.
4. Cấu hình tích hợp hạ tầng mạng:
   * **VPC:** Chọn `cloud-finance-vpc`.
   * **Security Group:** Gán Security Group có tên `redis-sg`.
5. Kiểm tra lại thông tin và xác nhận hoàn tất quá trình tạo Redis Cluster.

![Cấu hình Redis](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/redis.png)