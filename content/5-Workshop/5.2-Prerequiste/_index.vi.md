---
title : "Các bước chuẩn bị"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Chuẩn bị môi trường

Trước khi bắt đầu triển khai hệ thống, mình cần chuẩn bị đầy đủ môi trường làm việc để quá trình thực hiện workshop diễn ra thuận lợi.

#### Các yêu cầu cần chuẩn bị

Mình chuẩn bị các thành phần sau:

+ Một tài khoản AWS đã được kích hoạt đầy đủ quyền IAM hoặc Administrator để tạo và quản lý tài nguyên trên AWS.
+ Cài đặt Docker và Docker Compose để build và kiểm thử Docker Image trên máy cá nhân.
+ Cài đặt AWS CLI và cấu hình thông tin xác thực bằng lệnh `aws configure`.
+ Cài đặt Visual Studio Code để quản lý và chỉnh sửa mã nguồn.
+ Chuẩn bị sẵn source code của dự án gồm:
  + Frontend sử dụng ReactJS và Vite.
  + Backend gồm 9 microservices phát triển bằng FastAPI:
    + Gateway
    + Auth
    + Finance
    + AI Agent
    + Notification API
    + Notification Worker
    + Planning
    + Recurring
    + OCR

Sau khi hoàn tất các bước chuẩn bị, mình có thể bắt đầu xây dựng hạ tầng và triển khai toàn bộ hệ thống lên AWS.