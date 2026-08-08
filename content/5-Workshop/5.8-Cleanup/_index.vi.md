---
title: "Dọn dẹp tài nguyên"
weight: 8
chapter : false
pre : " <b> 5.8. </b> "
---

### Mục đích

Sau khi hoàn thành bài thực hành, việc xóa bỏ toàn bộ các tài nguyên đã tạo là một bước cực kỳ quan trọng để đảm bảo tài khoản AWS của mình không bị trừ tiền ngoài ý muốn. Nguyên tắc dọn dẹp thường sẽ đi ngược lại với trình tự lúc mình khởi tạo hệ thống.

---

### 1. Dọn dẹp Frontend (CloudFront & S3)

- **CloudFront:** Truy cập vào giao diện quản lý CloudFront và chọn Distribution mình đã tạo. Đầu tiên, hãy nhấn **Disable** (quá trình vô hiệu hóa sẽ mất vài phút). Sau khi trạng thái đã chuyển sang disabled, mình mới có thể nhấn **Delete** để xóa hoàn toàn.
- **S3 Bucket:** Tiếp tục qua dịch vụ S3. Mình cần lưu ý là AWS không cho phép xóa bucket nếu bên trong vẫn còn chứa file. Do đó, hãy chọn bucket `cloud-finance-frontend-<account-id>`, click **Empty** để dọn sạch toàn bộ mã nguồn frontend, sau đó mới nhấn **Delete** để xóa bucket.

### 2. Gỡ bỏ tầng Compute (ECS & ALB)

- **Amazon ECS:** 
  - Đi đến cluster `cloud-finance-cluster`.
  - Chọn Service đang chạy, cập nhật số lượng task (Desired tasks) về mức `0`.
  - Chờ một lát để các task dừng hẳn, tiến hành xóa Service, và cuối cùng là xóa luôn Cluster.
- **Load Balancer (ALB):** 
  - Mở EC2 Dashboard, tìm mục Load Balancers, tick chọn `cloud-finance-alb` và bấm **Delete**.
  - Cuộn xuống phần Target Groups, chọn nhóm `tg-gateway` và thực hiện xóa.

### 3. Xóa Docker Image (ECR)

- Quay trở lại dịch vụ **Elastic Container Registry (ECR)**.
- Chọn repository chứa image của backend. Tương tự như S3, mình cần tick chọn để xóa hết các image nằm bên trong trước, sau đó mới có quyền xóa toàn bộ repository.

### 4. Dọn dẹp tầng Database & Secrets

- **Amazon RDS:** Vào giao diện quản lý RDS > Databases. Tick chọn instance đã tạo, nhấn **Delete**. Đừng quên bỏ tick tùy chọn "Create final snapshot" (trừ khi mình muốn tốn phí lưu trữ bản backup) và xác nhận xóa.
- **Secrets Manager:** Tìm đến secret lưu thông tin cấu hình database, chọn **Delete secret**. (AWS thường yêu cầu một khoảng thời gian chờ để xóa vĩnh viễn, mình có thể thiết lập mức tối thiểu là 7 ngày).

### 5. Xóa hạ tầng mạng (VPC)

Bước cuối cùng này sẽ dọn sạch tận gốc các cấu hình mạng:
- Truy cập vào **VPC Dashboard** > **Your VPCs**.
- Chọn `cloud-finance-vpc`, nhấn **Actions** > **Delete VPC**. Thao tác này rất tiện vì nó sẽ tự động phát hiện và dọn sạch các thành phần đi kèm bên trong như Subnets, Internet Gateway, Route Tables và Security Groups.

