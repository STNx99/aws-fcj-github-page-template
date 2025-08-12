---
title: "Xóa API Gateway"
date: "`r Sys.Date()`"
weight: 13
chapter: false
pre: " <b> 6.4 </b> "
---

Trong bước này, bạn sẽ xóa **API Gateway** đã được tạo để cung cấp các hàm Lambda dưới dạng endpoint HTTP.

Bạn có thể đã cấu hình các endpoint sau:

- `POST /deploy` → gọi đến `upload-function`  
- `GET /status` → gọi đến `upload-function`

---

#### Mở Bảng điều khiển API Gateway

1. Truy cập [Amazon API Gateway Console](https://console.aws.amazon.com/apigateway/)

2. Trong menu bên trái, chọn **APIs**

3. Tìm API mà bạn đã tạo (ví dụ: `DeployAPI`)

![](/images/6.clean/001-deleteapigateway.png)

---

#### Xóa API

1. Nhấp vào tên API để mở chi tiết

2. Trong menu bên trái, cuộn xuống và nhấp vào **Stages**

3. Ghi lại API ID và tên stage (tùy chọn, để phục vụ mục đích ghi chú)

![](/images/6.clean/002-deleteapigateway.png)

4. Quay lại trang cấu hình chính của API

![](/images/6.clean/003-deleteapigateway.png)

5. Ở góc trên bên phải, nhấp vào **Delete**

![](/images/6.clean/004-deleteapigateway.png)

6. Xác nhận việc xóa bằng cách nhấp **Delete**

![](/images/6.clean/005-deleteapigateway.png)

---

Sau bước này, các endpoint API sẽ không còn khả dụng công khai và quyền truy cập HTTP vào các hàm Lambda của bạn sẽ bị xóa bỏ.

---

#### (Tùy chọn) Xóa cấu hình CORS

Nếu bạn đã thêm tiêu đề CORS vào API (thủ công hoặc qua bảng điều khiển), những thiết lập đó cũng sẽ bị xóa cùng với API.

Không cần thêm bước nào khác.

---

#### Bước tiếp theo

Tiếp tục đến [6.5 – Xóa IAM Roles và Policies](../6.5-deleteamplify/)