---
title: "Xóa các hàm Lambda"
date: "`r Sys.Date()`"
weight: 10
chapter: false
pre: " <b> 6.1 </b> "
---

Trong bước này, bạn sẽ xóa các **hàm Lambda** đã được tạo ra cho hệ thống triển khai, cụ thể là:

- `upload-function`  
- `deploy-function`

Việc này thường được thực hiện trong quá trình dọn dẹp hoặc khi triển khai lại với các thay đổi đáng kể.

---

#### Mở Bảng điều khiển Lambda

1. Truy cập vào [AWS Lambda Console](https://console.aws.amazon.com/lambda/)
2. Trong menu bên trái, nhấp vào **Functions (Hàm)**

![](/images/6.clean/001-deletelambdafunctions.png)

---

#### Xóa hàm `upload-function`

1. Trong thanh tìm kiếm, nhập `upload-function`
2. Nhấp vào tên hàm để mở chi tiết
3. Ở góc trên bên phải, nhấp vào nút **Actions (Hành động)**
4. Chọn **Delete (Xóa)**

![](/images/6.clean/002-deletelambdafunctions.png)

5. Trong cửa sổ xác nhận, nhập lại tên hàm và nhấp **Delete (Xóa)**

![](/images/6.clean/003-deletelambdafunctions.png)

---

#### Xóa hàm `deploy-function`

1. Quay lại danh sách **Functions**
2. Nhấp vào tên hàm `deploy-function` để mở chi tiết
3. Ở góc trên bên phải, nhấp vào **Actions**
4. Chọn **Delete**

![](/images/6.clean/004-deletelambdafunctions.png)

5. Trong cửa sổ xác nhận, nhập lại tên hàm và nhấp **Delete**

![](/images/6.clean/005-deletelambdafunctions.png)

---

Sau khi bị xóa, các hàm Lambda sẽ không còn tồn tại trong tài khoản AWS của bạn, và bất kỳ trigger (như EventBridge rule) nào liên kết với chúng cũng sẽ không hoạt động cho đến khi được cấu hình lại.

---

#### Bước tiếp theo

Tiếp tục đến [6.2 – Xóa tài nguyên EventBridge](../6.2-deletes3dynamodb/)