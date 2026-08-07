---
title : "Triển khai Frontend lên Amazon S3 và CloudFront"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.7. </b> "
---

#### Triển khai Frontend

Sau khi hoàn thành backend, mình tiến hành triển khai frontend của hệ thống.

Các bước thực hiện gồm:

1. Truy cập **Amazon S3** và tạo một Bucket để lưu trữ website tĩnh.
2. Bật **Block all public access** nhằm hạn chế truy cập trực tiếp vào Bucket.
3. Build ứng dụng React bằng lệnh:

```bash
npm run build
```

4. Upload thư mục `dist` lên S3 Bucket.
5. Truy cập **Amazon CloudFront** và tạo một Distribution mới.
6. Chọn S3 Bucket vừa tạo làm **Origin**.
7. Bật **Origin Access Control (OAC)** để CloudFront là thành phần duy nhất có quyền truy cập S3.
8. Cấu hình CloudFront chuyển tiếp các request `/api/*` và `/ws/*` đến Application Load Balancer.
9. Tích hợp **AWS WAF** để tăng cường bảo mật cho ứng dụng.

Sau khi hoàn tất, người dùng có thể truy cập ứng dụng thông qua CloudFront Domain Name với hiệu năng và khả năng mở rộng tốt hơn.

![cloudfront](/images/5-Workshop/5.7-Frontend/cloudfront.png)