---
title : "Tạo Amazon ElastiCache for Redis"
date : 2026-07-31
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

#### Tạo Amazon ElastiCache for Redis

Tiếp theo, mình triển khai Amazon ElastiCache for Redis để lưu trữ dữ liệu tạm thời và hỗ trợ các tác vụ cần truy cập nhanh.

Các bước thực hiện:

1. Truy cập **Amazon ElastiCache**.
2. Chọn **Redis Caches** và tạo một Redis Cluster mới.
3. Thiết lập:

+ **Cluster Name:** `cloud-finance-redis`
+ **Node Type:** `cache.t4g.micro`
+ **Replicas:** `0`

4. Chọn VPC `cloud-finance-vpc` và Security Group `redis-sg`.
5. Hoàn tất quá trình tạo Redis Cluster.

Redis được sử dụng để lưu cache và hỗ trợ các tác vụ bất đồng bộ, giúp cải thiện hiệu năng của hệ thống.

![redis](/images/5-Workshop/5.4-Database/redis.png)