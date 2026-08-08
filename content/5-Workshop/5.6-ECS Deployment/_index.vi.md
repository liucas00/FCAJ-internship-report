---
title: "Vận hành trên ECS Fargate & ALB"
weight: 6
---

### Mục tiêu chính

Bài thực hành này hướng dẫn mình cách khởi tạo một cụm ECS Cluster dạng serverless. Tiếp theo, chúng ta sẽ thiết lập Application Load Balancer nhằm mục đích phân bổ lưu lượng mạng, cũng như tạo các Task Definitions để chạy các microservices. Một điểm quan trọng là hệ thống sẽ được cấu hình để tự động kéo các thông tin bảo mật từ AWS Secrets Manager thay vì gán trực tiếp.

---

### 1. Khởi tạo cụm Amazon ECS (ECS Cluster)

Để bắt đầu, mình cần tạo một không gian quản lý chung cho các container của mình:

- Từ giao diện chính của AWS Console, tìm và truy cập vào dịch vụ **Amazon ECS**.
- Ở menu bên trái, nhấn vào **Clusters**, sau đó click vào nút **Create cluster**.
- Trong form khởi tạo, hãy điền tên cho cụm là `cloud-finance-cluster`.
- Chú ý ở mục **Infrastructure**: Hãy đảm bảo mình đánh dấu chọn **AWS Fargate** để sử dụng kiến trúc serverless, giúp mình không cần bận tâm đến việc quản lý máy chủ vật lý.
- Cuối cùng, nhấn **Create** để hệ thống bắt đầu quá trình tạo mới.

![Tạo ECS Cluster](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/ecs-cluster.png)

### 2. Thiết lập Application Load Balancer (ALB)

Việc trang bị một Load Balancer là cần thiết để cân bằng tải và điều hướng luồng truy cập vào các dịch vụ bên trong:

- Mở dịch vụ **EC2**, cuộn xuống phần **Load Balancing** ở thanh điều hướng bên trái và chọn **Load Balancers**. Tiếp tục nhấn **Create Load Balancer**.
- Chọn loại **Application Load Balancer** trong danh sách các tùy chọn.
- Mình cần cung cấp các thông số cấu hình cơ bản sau:
  - **Tên (Name):** Đặt là `cloud-finance-alb`.
  - **Mô hình (Scheme):** Chọn `Internet-facing` để nhận được các request từ môi trường public internet.
  - **VPC & Subnets:** Lựa chọn VPC có tên `cloud-finance-vpc`, đồng thời chỉ định 2 Public Subnets tương ứng.
  - **Security groups:** Gắn security group `alb-sg` để kiểm soát các luồng truy cập an toàn.
- Kế tiếp, mình tiến hành tạo Target Groups (ví dụ đặt tên là `tg-gateway` lắng nghe trên cổng `8000`, đường dẫn health check là `/health`). Lưu lại thiết lập này để hoàn thành việc tạo ALB.

![Tạo ALB](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/alb.png)

### 3. Cấu hình Task Definitions và chạy ECS Services

Bước cuối cùng là khai báo hình thái của container và tiến hành chạy dịch vụ trên cluster vừa tạo:

- Quay trở lại giao diện ECS Console, tìm đến mục **Task definitions** và chọn **Create new task definition**.
- Định danh cho task family, giả sử là `cloud-finance-gateway-task`. Lựa chọn môi trường chạy (launch type) là **AWS Fargate** và chế độ mạng (network mode) được thiết lập ở dạng `awsvpc`.
- Về phần **Container Definitions**, mình cần cấu hình các thông số sau: 
  - Chỉ định đường dẫn image đã lưu trữ trước đó trên ECR.
  - Cấu hình mở cổng mạng (port mapping) là `8000`.
  - Đặc biệt ở khối `secrets`, hãy tham chiếu cấu hình để hệ thống tự động kéo các giá trị bảo mật từ AWS Secrets Manager và tiêm vào biến môi trường của container ngay lúc khởi động.
- Khi Task Definition đã sẵn sàng, mình quay lại màn hình quản lý cụm `cloud-finance-cluster`. Bấm vào **Create Service** để khởi chạy dịch vụ thực tế. Gắn dịch vụ này với ALB vừa tạo ở bước 2, đồng thời đừng quên kích hoạt tính năng **Service Connect** để tối ưu hóa khả năng giao tiếp nội bộ giữa các microservices.

![Cấu hình ECS Services](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/ecs-services.png)