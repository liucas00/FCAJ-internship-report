---
title : "Tạo Amazon ECS Cluster"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Tạo Amazon ECS Cluster

Đầu tiên, mình tạo một ECS Cluster để quản lý các container của hệ thống.

Các bước thực hiện:

1. Truy cập **Amazon ECS**.
2. Chọn **Clusters**.
3. Chọn **Create Cluster**.
4. Đặt tên:

`cloud-finance-cluster`

5. Chọn **AWS Fargate** làm hạ tầng triển khai.
6. Hoàn tất quá trình tạo Cluster.

Sau khi hoàn thành, ECS Cluster sẽ là nơi quản lý và vận hành toàn bộ backend microservices.

![cluster](/images/5-Workshop/5.6-ECS/cluster.png)