---
title : "Cấu hình AWS Secrets Manager"
date : 2026-07-31
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

#### Cấu hình AWS Secrets Manager

Để tăng cường bảo mật, mình sử dụng AWS Secrets Manager thay cho việc lưu trữ thông tin nhạy cảm trong file `.env`.

Các bước thực hiện:

1. Truy cập **AWS Secrets Manager**.
2. Chọn **Store a new secret**.
3. Chọn **Other type of secret**.
4. Khai báo các cặp Key/Value:

+ `DATABASE_URL`
+ `GEMINI_API_KEY`
+ `JWT_SECRET_KEY`

5. Đặt tên Secret là:

`cloud-finance/production-secrets`

6. Hoàn tất quá trình tạo Secret.

Sau khi hoàn thành, các container có thể lấy thông tin cấu hình trực tiếp từ AWS Secrets Manager trong quá trình khởi động, giúp hạn chế việc lưu trữ thông tin nhạy cảm trong mã nguồn.

![secret](/images/5-Workshop/5.4-Database/secrets-manager.png)