---
title: "Cấu hình AWS Secrets Manager"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b> 5.4.3. </b>"
---

### Quản lý Cấu hình Bảo mật
Nhằm nâng cao mức độ bảo mật cho toàn hệ thống, AWS Secrets Manager được triển khai để thay thế cho phương pháp lưu trữ cấu hình truyền thống thông qua file `.env`. Kiến trúc này cho phép các ứng dụng (container) tự tự động truy xuất các thông tin nhạy cảm một cách an toàn trong quá trình khởi động, từ đó loại bỏ hoàn toàn rủi ro lộ lọt thông tin cấu hình bên trong mã nguồn dự án.

#### Hướng dẫn cấu hình
Thực hiện các bước sau để thiết lập kho lưu trữ bảo mật:

1. Truy cập vào bảng điều khiển dịch vụ **AWS Secrets Manager**.
2. Nhấn chọn nút **Store a new secret** để tạo mới một cấu hình bảo mật.
3. Tại mục phân loại, chọn **Other type of secret**.
4. Tiến hành khai báo các cặp Key/Value (Khóa/Giá trị) cho các thông tin nhạy cảm sau:
   * `DATABASE_URL`
   * `GEMINI_API_KEY`
   * `JWT_SECRET_KEY`
5. Đặt tên định danh cho Secret là: `cloud-finance/production-secrets`
6. Kiểm tra lại thông số và hoàn tất quá trình tạo Secret.

![Cấu hình Secrets Manager](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/secrets-manager.png)