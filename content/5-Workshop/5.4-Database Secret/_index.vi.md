---
title: "Tầng dữ liệu & Bảo mật cấu hình"
weight: 4
---

### Mục tiêu cốt lõi

Trong phần này, chúng ta sẽ thiết lập một hệ quản trị cơ sở dữ liệu quan hệ (Amazon RDS) nằm an toàn trong mạng nội bộ. Đồng thời, để tránh việc lộ lọt thông tin nhạy cảm (như mật khẩu, chuỗi kết nối), toàn bộ cấu hình truy cập sẽ được mã hóa và quản lý tập trung thông qua AWS Secrets Manager.

---

### 1. Khởi tạo Database với Amazon RDS

Thay vì tự cài đặt và vận hành database trên server EC2, chúng ta sẽ dùng dịch vụ RDS để tiết kiệm thời gian quản trị:

- Truy cập dịch vụ **Amazon RDS** từ giao diện AWS Console.
- Đầu tiên, mình cần tạo một **Subnet group** để quy định nơi database được phép hoạt động. Hãy chọn VPC `cloud-finance-vpc` và chỉ định các **Private Subnets** (để chặn hoàn toàn các luồng truy cập trực tiếp từ Internet).
- Chuyển sang phần **Databases** ở menu trái và chọn **Create database**.
- Lựa chọn engine phù hợp (ví dụ: MySQL hoặc PostgreSQL) và chọn template là Free tier (nếu mình đang dùng tài khoản thực hành để tối ưu chi phí).
- Đặt tên định danh cho DB instance (ví dụ: `cloud-finance-db`), sau đó thiết lập thông tin đăng nhập bao gồm Master username và password.
- Tại mục **Connectivity**, hãy chắc chắn rằng tùy chọn **Public access** đang được đặt là `No`. Gắn Security Group tương ứng cho database để cho phép các dịch vụ backend từ ECS có thể kết nối vào một cách an toàn.

![Khởi tạo RDS](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/rds-postgres.png)

### 2. Tăng tốc ứng dụng với Amazon ElastiCache for Redis

Để giảm tải cho database chính và tăng tốc độ phản hồi API, chúng ta sẽ trang bị thêm một cụm cache bằng Redis:

- Tìm và mở dịch vụ **Amazon ElastiCache** trên AWS Console.
- Tương tự như RDS, bước đầu tiên là tạo **Subnet group**. Bạn chọn lại VPC `cloud-finance-vpc` và gắn các Private Subnets để Redis chạy ngầm bên trong mạng nội bộ.
- Tiếp theo, nhấn **Create Redis cluster** (Tạo cụm Redis).
- Đặt tên cho cụm cache này (ví dụ: `cloud-finance-redis`). 
- Trong phần cấu hình phần cứng (Node type), hãy chọn một loại instance nhỏ (như `cache.t2.micro` hoặc `cache.t3.micro`) để tiết kiệm chi phí cho môi trường lab. 
- Tại phần **Security**, chọn Security Group phù hợp để cấp quyền cho backend trên ECS có thể đọc/ghi dữ liệu vào Redis. 

![Khởi tạo ElastiCache Redis](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/elasticache-redis.png)

### 3. Quản lý thông tin kết nối bằng AWS Secrets Manager

Việc gắn trực tiếp (hardcode) mật khẩu database vào mã nguồn là một rủi ro bảo mật lớn. AWS Secrets Manager sẽ giúp chúng ta giải quyết triệt để bài toán này:

- Điều hướng đến dịch vụ **AWS Secrets Manager** và nhấn nút **Store a new secret**.
- Trong phần loại secret (Secret type), hãy chọn **Credentials for Amazon RDS database**.
- Điền lại chính xác thông tin username và password mà mình đã cấu hình ở bước khởi tạo RDS phía trên.
- Ở phần dưới cùng, hệ thống sẽ liệt kê các database đang có sẵn. Hãy chọn đúng instance `cloud-finance-db` vừa tạo để liên kết.
- Nhấn Next và đặt một cái tên gợi nhớ cho secret này (ví dụ: `cloud-finance/db-credentials`).
- Hoàn tất các bước còn lại và lưu secret. Ở các bài sau, khi triển khai ứng dụng trên ECS, hệ thống sẽ tự động gọi vào Secrets Manager để kéo thông tin đăng nhập về mà không cần phải truyền mật khẩu dạng plain-text.

![Cấu hình Secrets Manager](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/secrets-manager.png)