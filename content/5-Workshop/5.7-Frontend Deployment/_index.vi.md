---
title: "Triển khai Frontend lên S3 & CloudFront"
weight: 7
chapter : false
pre : " <b> 5.7. </b> "
---

### Mục đích của bài lab

Trong phần này, mình sẽ đưa phần giao diện người dùng (được viết bằng ReactJS) lên AWS. Thay vì chạy trên server thông thường, mình sẽ dùng Amazon S3 để lưu trữ mã nguồn dạng tĩnh (Single Page Application). Sau đó, để trang web tải nhanh hơn ở mọi nơi, Amazon CloudFront sẽ được tận dụng làm mạng phân phối nội dung (CDN). 

Bên cạnh đó, để đảm bảo an toàn, dữ liệu trên S3 sẽ bị khóa lại hoàn toàn (chỉ cho phép CloudFront truy cập qua cơ chế OAC) và ứng dụng cũng sẽ được bảo vệ bởi tường lửa AWS WAF.

---

### 1. Chuẩn bị S3 Bucket để lưu trữ giao diện

Bước đầu tiên là tạo một nơi để chứa các file code giao diện đã được biên dịch:

- Mở AWS Console và tìm đến dịch vụ **Amazon S3**, sau đó click vào nút **Create bucket**.
- Đặt một cái tên duy nhất cho bucket của bạn (ví dụ như `cloud-finance-frontend-<account-id>`). Tại bước này, bạn nhớ giữ nguyên tùy chọn **Block all public access** (Chặn tất cả truy cập công khai). Đây là best practice để tránh rò rỉ dữ liệu ngoài ý muốn.
- Tiếp theo, mở terminal trên máy tính của bạn, chạy lệnh `npm run build` để đóng gói project ReactJS.
- Cuối cùng, upload toàn bộ các file và thư mục nằm trong thư mục `dist` (vừa được tạo ra) thẳng lên bucket S3 này.

![Giao diện S3 Buckets](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.7-frontend-deployment/s3-buckets.png)

### 2. Thiết lập mạng phân phối nội dung với CloudFront

Sau khi code đã nằm gọn trên S3, giờ là lúc cấu hình CloudFront làm đầu mối giao tiếp duy nhất với người dùng:

- Điều hướng đến dịch vụ **Amazon CloudFront** và chọn **Create distribution**.
- Ở mục **Origin domain**, hãy chọn chính xác cái S3 bucket mà bạn vừa tải code frontend lên.
- Sang phần **Origin access**, thay vì để Public, bạn hãy chọn **Origin access control (OAC)**. Hãy tạo mới một thiết lập OAC để cấp quyền cho CloudFront được phép đọc dữ liệu từ S3 bucket (nhờ đó S3 vẫn bảo mật mà web vẫn hoạt động bình thường).
- Tại mục **Behavior configuration**, bạn cần định tuyến (routing) như sau:
  - Các request thông thường (lấy file HTML, CSS, JS, hình ảnh) sẽ được trỏ về S3.
  - Các request bắt đầu bằng `/api/*` hoặc `/ws/*` (dữ liệu backend, websocket) phải được chuyển hướng trực tiếp xuống cho **Application Load Balancer (ALB)** xử lý.
- Để tăng cường an ninh, bạn nên tích hợp thêm **AWS WAF** ngay trên CloudFront distribution này. Nó sẽ đóng vai trò như lớp khiên chặn đứng các truy cập xấu trước khi chúng kịp chạm vào ứng dụng.

![Giao diện cấu hình CloudFront](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.7-frontend-deployment/cloudfront.png)