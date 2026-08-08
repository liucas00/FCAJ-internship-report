---
title : "Tạo Amazon ECR và đẩy Docker Images"
date : 2026-07-31
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Tạo Amazon Elastic Container Registry

Đầu tiên, mình tạo các repositories trên Amazon ECR để lưu trữ Docker Images cho từng microservice.

Các repositories được tạo gồm:

+ `cloud-finance/gateway`
+ `cloud-finance/auth`
+ `cloud-finance/finance`
+ `cloud-finance/ai-agent`
+ `cloud-finance/notification-api`
+ `cloud-finance/notification-worker`
+ `cloud-finance/planning`
+ `cloud-finance/recurring`
+ `cloud-finance/ocr`

Sau khi tạo repository, mình thực hiện:

1. Đăng nhập Amazon ECR bằng AWS CLI.
2. Build Docker Image từ source code.
3. Gắn tag tương ứng với repository trên ECR.
4. Push Docker Image lên Amazon ECR.

Sau khi hoàn tất, toàn bộ Docker Images đã sẵn sàng để được sử dụng trong Amazon ECS Fargate.

![ecr](/images/5-Workshop/5.5-ECR/ecr.png)