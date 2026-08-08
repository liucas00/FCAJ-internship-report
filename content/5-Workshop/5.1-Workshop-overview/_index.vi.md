---
title : "Giới thiệu"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu Workshop

Chào mừng bạn đến với workshop **Xây dựng và triển khai toàn diện hệ thống quản lý tài chính cá nhân tích hợp AI lên AWS (Cloud-Native Microservices)**.

Workshop hướng dẫn xây dựng và vận hành **Cloud Finance Platform** – một nền tảng quản lý tài chính cá nhân thông minh ứng dụng AI, NLP và OCR. Mình sẽ triển khai toàn bộ hệ thống trên AWS theo kiến trúc Cloud-Native Microservices.

#### Nội dung workshop

Trong workshop này, mình sẽ thực hiện các bước chính sau:

+ Chuẩn bị môi trường phát triển và tài khoản AWS.
+ Xây dựng hạ tầng mạng và bảo mật với Amazon VPC, Subnets và Security Groups.
+ Triển khai tầng dữ liệu sử dụng Amazon RDS PostgreSQL, ElastiCache Redis và AWS Secrets Manager.
+ Đóng gói các microservices thành Docker Images và lưu trữ trên Amazon ECR.
+ Triển khai các dịch vụ Backend trên Amazon ECS Fargate kết hợp Application Load Balancer.
+ Triển khai Frontend lên Amazon S3 và CloudFront.
+ Cấu hình quy trình CI/CD bằng GitHub Actions để tự động hóa việc triển khai.
+ Thực hiện dọn dẹp tài nguyên sau khi hoàn thành workshop nhằm tối ưu chi phí AWS.

#### Tổng quan Kiến trúc

Kiến trúc hệ thống của **Cloud Finance Platform** được thiết kế để đảm bảo tính sẵn sàng cao, bảo mật và khả năng mở rộng bằng cách sử dụng các dịch vụ Cloud-Native trên AWS:

* **Tầng Edge & Frontend:** Người dùng truy cập ứng dụng Web/Mobile thông qua **Amazon CloudFront**, dịch vụ này phân phối Frontend (SPA) được lưu trữ trên **Amazon S3**. **AWS WAF** được gắn vào CloudFront để bảo vệ ứng dụng khỏi các luồng truy cập độc hại.
* **Mạng & Định tuyến:** Hạ tầng mạng được đặt trong **Amazon VPC**. Lưu lượng truy cập từ Internet sẽ đi qua **Application Load Balancer (ALB)** ở Public Subnets để điều phối request đến các dịch vụ Backend ở phía sau.
* **Tầng Ứng dụng (Microservices):** Các microservices (Gateway, Auth, Finance, AI Agent, OCR, Notification...) được triển khai trên **Amazon ECS (AWS Fargate)** nằm trong các Private Subnets. Riêng AI Agent Service sẽ có kết nối với bên ngoài để gọi **External LLM API (Gemini)**.
* **Tầng Dữ liệu:** Đặt tại Private DB Subnets, hệ thống sử dụng **Amazon RDS for PostgreSQL** làm cơ sở dữ liệu quan hệ cho từng service và **Amazon ElastiCache for Redis** để xử lý caching, queue (hàng đợi). Một S3 Bucket riêng biệt khác được dùng để lưu trữ file hóa đơn (receipts) và file trích xuất (exports).
* **Quy trình CI/CD:** Mã nguồn từ **GitHub** sẽ kích hoạt **GitHub Actions** để tự động build và đẩy Docker Image lên **Amazon ECR**, từ đó triển khai phiên bản mới xuống Amazon ECS.
* **Giám sát & Bảo mật:** Hệ thống sử dụng **AWS Secrets Manager** để quản lý biến môi trường nhạy cảm, **Amazon CloudWatch** để theo dõi log/metric, và **Amazon SES** để phục vụ việc gửi email (OTP, thông báo).

![Kiến trúc hệ thống](/FCAJ-internship-report/images/5-Workshop/5.1-Workshop-overview/architect.jpg)