---
title: "7 IAM Best Practices giúp bảo vệ AWS Account hiệu quả hơn"
date: 2026-08-07
draft: false
description: "Tìm hiểu 7 nguyên tắc IAM quan trọng giúp bảo vệ AWS Account an toàn hơn, từ việc hạn chế sử dụng Root User, bật MFA, áp dụng Least Privilege đến sử dụng IAM Role và CloudTrail."

categories:
  - AWS
image: "/images/blogs/iam-best-practices.png"
---

Khi bắt đầu sử dụng AWS, nhiều người thường tập trung vào việc tạo EC2, lưu trữ dữ liệu trên S3 hoặc triển khai cơ sở dữ liệu bằng Amazon RDS. Tuy nhiên, trước khi quan tâm hệ thống chạy nhanh đến đâu, chúng ta cần trả lời một câu hỏi quan trọng hơn:

> **Ai được phép truy cập tài nguyên và họ được phép thực hiện những hành động nào?**

Đó chính là vai trò của **AWS Identity and Access Management (IAM)**.

IAM hỗ trợ quản lý danh tính, xác thực người dùng và kiểm soát quyền truy cập đến các tài nguyên trong AWS Account. Khi một người dùng hoặc ứng dụng gửi yêu cầu, AWS sẽ đánh giá danh tính, policy, hành động và tài nguyên liên quan trước khi cho phép hoặc từ chối yêu cầu đó.

Trong bài viết này, chúng ta sẽ cùng điểm qua **7 IAM Best Practices** giúp AWS Account an toàn hơn và dễ quản lý hơn.

---

## 1. Không sử dụng Root User cho công việc hằng ngày

Root User được tạo cùng với AWS Account và có toàn quyền truy cập tài nguyên, thông tin tài khoản cũng như thanh toán. Vì vậy, AWS khuyến nghị **không sử dụng Root User cho các công việc hằng ngày** như:

- Tạo EC2
- Chỉnh sửa Security Group
- Quản lý S3 Bucket
- Cấu hình dịch vụ

Sau khi tạo tài khoản, nên thực hiện:

- Đặt mật khẩu mạnh
- Bật MFA cho Root User
- Không tạo Access Key cho Root User
- Chỉ đăng nhập Root User khi thật sự cần

Đối với công việc quản trị thông thường, nên sử dụng **AWS IAM Identity Center** hoặc IAM Role với phạm vi quyền phù hợp.

---

## 2. Bật Multi-Factor Authentication (MFA)

Mật khẩu dù mạnh vẫn có thể bị lộ do phishing hoặc rò rỉ dữ liệu. MFA bổ sung thêm một lớp xác thực giúp giảm đáng kể nguy cơ tài khoản bị truy cập trái phép.

Nên bật MFA cho:

- Root User
- Administrator
- Người có quyền thay đổi IAM
- IAM User vẫn đang sử dụng

AWS hiện hỗ trợ:

- Passkey
- Security Key
- Ứng dụng tạo mã OTP

Trong đó AWS khuyến nghị ưu tiên Passkey hoặc Security Key khi có thể.

---

## 3. Áp dụng nguyên tắc Least Privilege

Nguyên tắc **Least Privilege** có nghĩa là chỉ cấp đúng quyền cần thiết để hoàn thành công việc.

Ví dụ, nếu ứng dụng chỉ cần đọc ảnh trong một S3 Bucket thì chỉ nên cấp:

```text
s3:ListBucket
s3:GetObject
```

Thay vì:

```text
AdministratorAccess
```

Ví dụ IAM Policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example-image-bucket"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-image-bucket/*"
    }
  ]
}
```

Khi xây dựng IAM Policy, nên hạn chế:

```json
"Action": "*"
```

hoặc

```json
"Resource": "*"
```

và thường xuyên rà soát lại quyền khi hệ thống thay đổi.

---

## 4. Ưu tiên Temporary Credentials

Access Key dài hạn luôn tồn tại cho đến khi bị xóa hoặc vô hiệu hóa. Nếu bị lộ, người khác vẫn có thể sử dụng chúng.

AWS khuyến nghị sử dụng **Temporary Credentials** thông qua IAM Role.

Luồng hoạt động:

```text
Người dùng đăng nhập
        ↓
Nhận quyền thông qua IAM Role
        ↓
AWS cấp Temporary Credentials
        ↓
Truy cập tài nguyên trong phạm vi cho phép
```

Credential chỉ tồn tại trong một khoảng thời gian ngắn nên giúp giảm đáng kể rủi ro bảo mật.

---

## 5. Sử dụng IAM Role cho ứng dụng

Một lỗi rất phổ biến là lưu Access Key trực tiếp trong source code hoặc file `.env`.

```text
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
```

Nếu repository vô tình public hoặc source code bị chia sẻ, credential sẽ bị lộ.

Thay vào đó nên sử dụng IAM Role:

- EC2 → Instance Profile
- ECS → Task Role
- Lambda → Execution Role

Ví dụ:

Một ECS Task chỉ cần upload hóa đơn lên S3 thì Task Role chỉ cần quyền:

```text
s3:PutObject
```

đối với đúng thư mục hóa đơn.

Không cần lưu Access Key trong source code và quyền cũng được quản lý rõ ràng hơn.

---

## 6. Quản lý Access Key cẩn thận

Trong một số trường hợp đặc biệt, hệ thống bên ngoài AWS vẫn cần Access Key.

Khi đó cần lưu ý:

- Không lưu Access Key trong source code
- Không commit `.env` lên GitHub
- Không dùng chung một key cho nhiều ứng dụng
- Chỉ cấp quyền tối thiểu
- Xóa các key không còn sử dụng
- Thay key ngay khi nghi ngờ bị lộ

AWS cũng khuyến cáo không tạo Access Key cho Root User.

---

## 7. Rà soát quyền và theo dõi hoạt động

Việc cấu hình IAM không nên dừng lại sau khi tạo Policy.

### IAM Access Analyzer

IAM Access Analyzer giúp:

- Phát hiện tài nguyên chia sẻ ngoài tài khoản
- Đề xuất thu hẹp quyền
- Hỗ trợ áp dụng Least Privilege

### AWS CloudTrail

CloudTrail ghi nhận toàn bộ hoạt động thông qua:

- AWS Console
- AWS CLI
- SDK
- API

CloudTrail giúp trả lời các câu hỏi:

- Ai thực hiện hành động?
- Thực hiện hành động gì?
- Thời điểm nào?
- Trên tài nguyên nào?

CloudTrail Event History lưu Management Event trong **90 ngày gần nhất** của từng Region. Nếu cần lưu lâu hơn, có thể sử dụng CloudTrail Trail hoặc CloudTrail Lake.

---

## Checklist kiểm tra nhanh AWS Account

Trước khi kết thúc, hãy tự kiểm tra:

- Root User đã bật MFA chưa?
- Root User có Access Key không?
- EC2, ECS, Lambda đã sử dụng IAM Role chưa?
- Có Policy nào cấp AdministratorAccess không cần thiết không?
- Có Access Key nào không còn sử dụng không?
- Đã kiểm tra IAM Access Analyzer chưa?
- CloudTrail đã được bật chưa?

---

## Kết luận

IAM là nền tảng quan trọng nhất của bảo mật trên AWS. Một hệ thống dù được thiết kế tốt vẫn có thể gặp rủi ro nếu Root User được sử dụng thường xuyên, Access Key bị lưu trong source code hoặc quyền truy cập được cấp quá rộng.

Bảy nguyên tắc quan trọng cần ghi nhớ gồm:

1. Hạn chế sử dụng Root User
2. Bật MFA cho các danh tính quan trọng
3. Áp dụng Least Privilege
4. Ưu tiên Temporary Credentials
5. Sử dụng IAM Role cho workload
6. Quản lý chặt chẽ Access Key
7. Kết hợp IAM Access Analyzer và CloudTrail để rà soát hệ thống

Chỉ với những thay đổi đơn giản như bật MFA, loại bỏ Access Key không cần thiết, thu hẹp IAM Policy và sử dụng IAM Role đúng cách, mức độ an toàn của AWS Account đã có thể được cải thiện đáng kể.

---

## Tài liệu tham khảo

- Security best practices in IAM
- Root user best practices for your AWS account
- AWS Multi-factor authentication in IAM
- Manage access keys for IAM users
- What is AWS CloudTrail?