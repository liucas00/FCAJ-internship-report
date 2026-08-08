---
title: "Tạo Amazon ElastiCache for Redis"[cite: 13]
date: 2026-07-31[cite: 13]
weight: 2[cite: 13]
chapter: false[cite: 13]
pre: "<b> 5.4.2. </b>"[cite: 13]
---

### Triển khai Bộ nhớ đệm (In-Memory Data Store)
Tiếp theo, hệ thống yêu cầu triển khai Amazon ElastiCache for Redis để cung cấp giải pháp lưu trữ dữ liệu tạm thời tốc độ cao[cite: 13]. Redis đóng vai trò cốt lõi trong việc quản lý bộ nhớ đệm (caching) và hỗ trợ xử lý các tác vụ bất đồng bộ, qua đó cải thiện đáng kể hiệu năng tổng thể của ứng dụng[cite: 13].

#### Hướng dẫn cấu hình
Thực hiện các bước sau để khởi tạo Redis Cluster:

1. Truy cập vào bảng điều khiển dịch vụ **Amazon ElastiCache**[cite: 13].
2. Tại menu điều hướng, chọn **Redis Caches** và bắt đầu quá trình tạo một Redis Cluster mới[cite: 13].
3. Thiết lập các thông số cơ bản cho Cluster[cite: 13]:
   * **Cluster Name (Tên cụm):** Nhập `cloud-finance-redis`[cite: 13].
   * **Node Type (Loại Node):** Chọn `cache.t4g.micro`[cite: 13].
   * **Replicas (Bản sao):** Đặt là `0`[cite: 13].
4. Cấu hình tích hợp hạ tầng mạng[cite: 13]:
   * **VPC:** Chọn `cloud-finance-vpc`[cite: 13].
   * **Security Group:** Gán Security Group có tên `redis-sg`[cite: 13].
5. Kiểm tra lại thông tin và xác nhận hoàn tất quá trình tạo Redis Cluster[cite: 13].

![Cấu hình Redis](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/redis.png)