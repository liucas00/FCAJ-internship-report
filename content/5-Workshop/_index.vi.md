---
title: "Workshop"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai Nền tảng Tài chính lên Đám mây: Tự động hóa CI/CD và Lưu trữ An toàn trên AWS

#### Tổng quan

**Amazon Web Services (AWS)** cung cấp bộ công cụ mạnh mẽ và khả năng mở rộng linh hoạt, là hạ tầng lý tưởng để đưa dự án **Cloud Finance Platform** từ môi trường phát triển (development) lên môi trường thực tế (production). 

Trong bài lab/workshop này, chúng ta sẽ thực hành cách tích hợp kiến trúc Backend-as-a-Service (đang sử dụng) với hạ tầng AWS. Mục tiêu cốt lõi là thiết lập luồng triển khai tự động hóa không chạm (CI/CD) cho giao diện Web Dashboard (ReactJS), đồng thời xây dựng một hệ thống lưu trữ độc lập, bảo mật cao cấp trên AWS để quản lý các tệp nhạy cảm (như hóa đơn, chứng từ giao dịch của người dùng).

Chúng ta sẽ tập trung thiết lập và cấu hình chuyên sâu hai dịch vụ cốt lõi:

+ **AWS Amplify (CI/CD & Hosting):** Thiết lập pipeline tự động nhận diện thay đổi mã nguồn từ kho lưu trữ (GitHub/GitLab) để build và deploy Web Dashboard. Quá trình này bao gồm việc cấu hình các biến môi trường an toàn (Environment Variables) để kết nối với cơ sở dữ liệu Supabase, thiết lập rules định tuyến lại (Redirect/Rewrite rules) cho ứng dụng Single Page Application (SPA), và liên kết tên miền tùy chỉnh (Custom Domain) với chứng chỉ SSL/TLS miễn phí.
+ **Amazon S3 (Lưu trữ Dữ liệu Tĩnh & Chứng từ):** Xây dựng hệ thống lưu trữ Object Storage thay thế hoặc bổ trợ cho hệ thống hiện tại. Chúng ta sẽ tạo các Private Buckets được thiết kế riêng để lưu trữ ảnh chụp hóa đơn giao dịch. Phần này đi sâu vào việc cấu hình CORS (Cross-Origin Resource Sharing) cho phép Client (Web/Mobile) upload trực tiếp thông qua Pre-signed URLs, và thiết lập IAM Policies/Bucket Policies nghiêm ngặt để chặn mọi truy cập ẩn danh (public access), đảm bảo an toàn tuyệt đối cho dữ liệu tài chính của người dùng.

#### Nội dung chi tiết Workshop

1. [Tổng quan Kiến trúc Triển khai AWS cho Nền tảng Tài chính](5.1-Architecture-overview/)
   - Bản đồ kiến trúc tích hợp: Client (Flutter/React) - AWS Amplify - S3 - Supabase.
2. [Chuẩn bị Môi trường và Bảo mật Phân quyền](5.2-Prerequisites/)
   - Khởi tạo IAM User/Role với quyền hạn tối thiểu (Least Privilege).
   - Chuẩn bị GitHub Repository và bộ biến môi trường (Supabase URL, API Keys).
3. [Lab 1: Triển khai Web Dashboard với AWS Amplify](5.3-Deploy-Amplify/)
   - Kết nối nhánh `main` với Amplify Console.
   - Cấu hình Build settings (`amplify.yml`) cho dự án ReactJS/TypeScript.
   - Xử lý lỗi 404 cho SPA bằng Rewrite Rules.
4. [Lab 2: Thiết lập Amazon S3 cho Hệ thống Chứng từ Giao dịch](5.4-S3-Storage/)
   - Tạo Private Bucket với mã hóa mặc định (Server-Side Encryption).
   - Thiết lập Block Public Access.
5. [Lab 3: Cấu hình CORS và Tích hợp API Upload](5.5-CORS-Integration/)
   - Cấu hình tệp JSON CORS để cấp quyền cho domain của Amplify.
   - Triển khai luồng upload/download bằng cơ chế Pre-signed URL kết nối với Client.
6. [Kiểm thử Tích hợp và Dọn dẹp Tài nguyên](5.6-Testing-Cleanup/)
   - Kiểm thử luồng End-to-End: Thêm giao dịch mới đính kèm ảnh hóa đơn.
   - Hướng dẫn xóa tài nguyên (Teardown) để tránh phát sinh chi phí.