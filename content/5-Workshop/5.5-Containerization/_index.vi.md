---
title : "Đóng gói và Đẩy Docker Image lên ECR"
date : 2026-07-31
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### Thiết lập không gian lưu trữ với Amazon ECR

Để chuẩn bị cho việc chạy ứng dụng trên ECS Fargate, tôi cần một không gian an toàn để quản lý các bản build của hệ thống. Dựa theo kiến trúc chia nhỏ, tôi tiến hành tạo 9 repositories riêng biệt trên Amazon Elastic Container Registry (ECR) tương ứng với từng dịch vụ backend.

Danh sách các kho lưu trữ tôi đã khởi tạo bao gồm:
* `cloud-finance/gateway`
* `cloud-finance/auth`
* `cloud-finance/finance`
* `cloud-finance/ai-agent`
* `cloud-finance/notification-api`
* `cloud-finance/notification-worker`
* `cloud-finance/planning`
* `cloud-finance/recurring`
* `cloud-finance/ocr`

![Amazon ECR Repositories](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.5-ECR/ecr.png)

### Quy trình Build và Push Image

Khi các ECR repositories đã sẵn sàng, tôi bắt tay vào việc đóng gói source code thành Docker Image theo một quy trình chuẩn:

1. **Xác thực kết nối:** Tôi sử dụng lệnh từ AWS CLI để đăng nhập an toàn vào registry của tài khoản AWS.
2. **Đóng gói (Build):** Tiến hành build Docker Image cho từng microservice ngay trên môi trường local.
3. **Định danh (Tag):** Gắn thẻ (tag) cho các image vừa tạo để chúng khớp chính xác với đường dẫn của repository tương ứng trên ECR.
4. **Tải lên (Push):** Thực thi lệnh push để đẩy toàn bộ các images này lên Amazon ECR.

Kết thúc bước này, tất cả các mảnh ghép của hệ thống đã được container hóa thành công và nằm chờ sẵn sàng để tôi đem đi triển khai trên hạ tầng Amazon ECS Fargate.