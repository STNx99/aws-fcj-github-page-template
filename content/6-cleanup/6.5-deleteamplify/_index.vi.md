---
title: "Xóa IAM Roles và Chính sách (Policies)"
date: "`r Sys.Date()`"
weight: 14
chapter: false
pre: " <b> 6.5 </b> "
---

Trong bước dọn dẹp cuối cùng này, bạn sẽ xóa các **IAM role** và **chính sách tùy chỉnh (custom policies)** đã được tạo cho các hàm Lambda và tích hợp EventBridge.

Việc này giúp giữ môi trường AWS của bạn gọn gàng và giảm thiểu rủi ro bảo mật không cần thiết.

---

#### Xác định các Role cần xóa

Bạn có thể đã tạo hoặc sử dụng các IAM role sau:

- `upload-function-role` – gắn với `upload-function`  
- `deploy-function-role` – gắn với `deploy-function`

Các role này có thể đã được gắn các chính sách quản lý như:

- `AmazonDynamoDBFullAccess`  
- `AmazonEventBridgeFullAccess`  
- `AmazonS3FullAccess`

Và một **chính sách inline tùy chỉnh**, ví dụ:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::awsdeplybucket1234/*"
    }
  ]
}
```
---

#### Xóa IAM Role

1. Truy cập [IAM Console – Roles](https://console.aws.amazon.com/iamv2/home#/roles)

2. Trong thanh tìm kiếm, nhập `upload-function-role` và chọn nó

![](/images/6.clean/001-deleteamplify.png)

3. Xem lại các chính sách đang được gắn với role

4. Tháo gỡ các chính sách quản lý (managed policies) nếu cần thiết

![](/images/6.clean/002-deleteamplify.png)

5. Nhấp vào **Delete** và xác nhận

![](/images/6.clean/003-deleteamplify.png)

6. Lặp lại các bước trên cho role `deploy-function-role`

![](/images/6.clean/004-deleteamplify.png)  
![](/images/6.clean/005-deleteamplify.png)  
![](/images/6.clean/006-deleteamplify.png)

---

#### Xóa Chính Sách Inline Tùy Chỉnh (nếu có)

Nếu bạn đã tạo chính sách inline tùy chỉnh theo cách thủ công:

1. Tại trang **Roles**, nhấp vào tên của role

![](/images/6.clean/007-deleteamplify.png)

2. Cuộn xuống phần **Permissions policies**

3. Nếu bạn thấy bất kỳ chính sách tùy chỉnh nào, nhấp vào tên của nó

4. Chọn **Remove (Gỡ bỏ)**

![](/images/6.clean/008-deleteamplify.png)  
![](/images/6.clean/009-deleteamplify.png)

> **Lưu ý:** Các chính sách được quản lý sẵn (như `AmazonS3FullAccess`) không cần xóa trừ khi bạn đã tạo phiên bản tùy chỉnh của chúng.

---

#### Hoàn tất Dọn Dẹp

Bạn đã hoàn tất việc xóa tất cả tài nguyên được tạo ra cho quy trình triển khai của mình.