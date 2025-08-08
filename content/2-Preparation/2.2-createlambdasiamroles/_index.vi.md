---
title: "Tạo Hàm Lambda và IAM Roles"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

Trong bước này, bạn sẽ tạo hai **hàm Lambda** tạo nền tảng cho quy trình triển khai tự động của bạn:

- `upload-function`: Clones mã nguồn từ GitHub, tải lên S3 và gửi một sự kiện EventBridge.
- `deploy-function`: Xử lý quá trình triển khai thực tế (ví dụ: cập nhật môi trường, thay đổi trạng thái, ghi dữ liệu vào DynamoDB).

Bạn cũng sẽ tạo và cấu hình **IAM roles** để các hàm Lambda này có thể tương tác an toàn với các dịch vụ AWS.

---

### Tổng Quan Kiến Trúc

![Lambda Architecture](/images/arc-lambda-flow.png)

---

### Nội dung

- [2.2.1 Tạo Hàm Lambda Upload](2.2.1-createlambdaupload/)
- [2.2.2 Tạo Hàm Lambda Triển Khai (Deploy)](2.2.2-createlambdadeploy/)