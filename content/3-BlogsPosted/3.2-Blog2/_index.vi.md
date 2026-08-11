---
title: "Điều mình thích nhất là Auto Scaling không chỉ dành cho những hệ thống cực lớn"
date: 2026-08-07
draft: false
description: "Auto Scaling không chỉ dành cho những hệ thống có hàng triệu người dùng. Tìm hiểu cách Amazon ECS Service Auto Scaling giúp ứng dụng tự mở rộng theo nhu cầu, tối ưu chi phí và nâng cao hiệu năng."
categories:
  - AWS
image: "/images/blogs/ecs-auto-scaling.png"
---

Khi mới bắt đầu tìm hiểu về AWS, mình luôn nghĩ **Auto Scaling** là tính năng chỉ dành cho những hệ thống cực lớn với hàng triệu lượt truy cập mỗi ngày.

Nhưng sau khi có cơ hội triển khai ứng dụng trên Amazon ECS Fargate, mình nhận ra điều đó không hoàn toàn đúng.

Ngay cả với những ứng dụng nhỏ hoặc dự án học tập, việc cấu hình Auto Scaling cũng giúp hiểu rõ hơn cách một hệ thống cloud vận hành trong thực tế. Thay vì phải dự đoán trước sẽ cần bao nhiêu máy chủ, mình chỉ cần xác định một số giới hạn và để AWS tự động điều chỉnh tài nguyên dựa trên lưu lượng sử dụng.

Đây cũng là một trong những điểm mình thấy khác biệt rõ ràng giữa việc triển khai ứng dụng trên Cloud và mô hình máy chủ truyền thống.

---

## Auto Scaling là gì?

Auto Scaling là cơ chế tự động tăng hoặc giảm số lượng tài nguyên khi nhu cầu sử dụng thay đổi.

Đối với Amazon ECS, Auto Scaling thường sẽ tăng hoặc giảm số lượng **Task** đang chạy trong Service dựa trên các chỉ số như:

- CPU Utilization
- Memory Utilization
- Request Count
- Hoặc các CloudWatch Metric tùy chỉnh

Ví dụ:

- Khi lượng người dùng tăng, ECS sẽ tự tạo thêm Task để xử lý.
- Khi lưu lượng giảm, các Task không còn cần thiết sẽ được dừng để tiết kiệm chi phí.

Nhờ đó, ứng dụng luôn duy trì hiệu năng ổn định mà không cần người quản trị can thiệp thủ công.

---

## Cách Auto Scaling hoạt động

Một cấu hình Auto Scaling cơ bản thường gồm các thành phần:

- Amazon ECS Service
- Application Auto Scaling
- Amazon CloudWatch
- Application Load Balancer (ALB)

Quy trình hoạt động có thể mô tả như sau:

```text
Người dùng gửi request
        ↓
Application Load Balancer
        ↓
Amazon ECS Service
        ↓
CloudWatch theo dõi CPU hoặc Memory
        ↓
Nếu vượt ngưỡng đã cấu hình
        ↓
Application Auto Scaling
        ↓
Tăng hoặc giảm số lượng ECS Task
```

Toàn bộ quá trình này diễn ra tự động mà không cần triển khai lại ứng dụng.

---

## Lợi ích của Auto Scaling

### Tối ưu chi phí

Khi lượng truy cập thấp, Auto Scaling sẽ giảm số lượng Task đang chạy.

Điều này giúp doanh nghiệp chỉ phải trả chi phí cho đúng lượng tài nguyên đang sử dụng thay vì duy trì nhiều máy chủ hoạt động liên tục.

---

### Đảm bảo hiệu năng

Khi có nhiều người dùng truy cập cùng lúc, hệ thống sẽ tự động mở rộng để xử lý thêm lưu lượng.

Người dùng sẽ ít gặp tình trạng chậm hoặc quá tải hơn so với việc sử dụng số lượng máy chủ cố định.

---

### Giảm thao tác vận hành

Thay vì phải liên tục theo dõi và tăng số lượng Task bằng tay, Auto Scaling sẽ tự động thực hiện khi các điều kiện đã cấu hình được đáp ứng.

Điều này giúp giảm đáng kể khối lượng công việc của đội ngũ vận hành.

---

## Một vài lưu ý khi cấu hình Auto Scaling

Trong quá trình tìm hiểu, mình thấy có một số điểm khá quan trọng:

- Không nên đặt ngưỡng CPU quá thấp, nếu không Service sẽ liên tục Scale Out dù lưu lượng chưa thực sự cao.
- Nên cấu hình thời gian **Cooldown** hợp lý để tránh việc vừa tăng tài nguyên xong lại giảm ngay sau đó.
- Nếu ứng dụng sử dụng nhiều RAM hơn CPU, nên theo dõi **Memory Utilization** thay vì chỉ dựa vào CPU Utilization.
- Auto Scaling giúp tăng số lượng ECS Task, nhưng nếu không có **Application Load Balancer**, việc phân phối request giữa các Task sẽ không hiệu quả.

---

## Auto Scaling không chỉ dành cho hệ thống lớn

Điều khiến mình thích nhất là Auto Scaling không yêu cầu ứng dụng phải có hàng triệu người dùng mới phát huy tác dụng.

Ngay cả khi xây dựng một dự án học tập hoặc một hệ thống có quy mô nhỏ, việc cấu hình Auto Scaling vẫn mang lại nhiều giá trị:

- Hiểu rõ cách Cloud tự động quản lý tài nguyên.
- Làm quen với CloudWatch Metrics và Scaling Policy.
- Tối ưu chi phí khi hệ thống hoạt động không liên tục.
- Chuẩn bị sẵn khả năng mở rộng khi lượng người dùng tăng trong tương lai.

Đây cũng là một trong những lý do khiến mình cảm thấy việc triển khai ứng dụng trên AWS thú vị hơn so với mô hình triển khai truyền thống.

---

## Kết luận

Sau khi tìm hiểu tính năng này, mình nhận ra Auto Scaling không phải là một tính năng "xa xỉ" chỉ dành cho các hệ thống cực lớn.

Điều quan trọng nhất là ứng dụng luôn sử dụng đúng lượng tài nguyên tại đúng thời điểm. Khi ít người dùng, hệ thống có thể tự thu hẹp để tiết kiệm chi phí. Khi lượng truy cập tăng, AWS sẽ tự động mở rộng tài nguyên nhằm duy trì hiệu năng và khả năng phục vụ.

Chính khả năng vận hành linh hoạt này là một trong những ưu điểm nổi bật khiến mình đánh giá cao nền tảng AWS trong quá trình học tập và triển khai ứng dụng trên Cloud.

---

## Kiến trúc tham khảo

Hình dưới đây minh họa kiến trúc triển khai ứng dụng trên AWS sử dụng **Amazon ECS Fargate**, **Application Load Balancer**, **Amazon S3**, **Amazon SQS** và **Amazon DynamoDB** để xử lý lưu lượng truy cập, lưu trữ dữ liệu và xử lý bất đồng bộ.

*Nguồn: AWS Architecture Diagram.*

---

## Tài liệu tham khảo

- Amazon ECS Service Auto Scaling – AWS Documentation
- Amazon CloudWatch Metrics for Amazon ECS
- Application Auto Scaling User Guide
- Amazon ECS Best Practices Guide

{{<figure src="https://vvinh118.github.io/fcaj-workshop/3-blogsposted/3.3-blog3/blog3.png" title="Ảnh minh chứng bài đăng trên AWS Study Group VN">}}