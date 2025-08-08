---
title: "Tạo Lambda Functions và IAM Roles"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

Trong bước này, bạn sẽ tạo hai **hàm Lambda** là nền tảng cho quy trình triển khai tự động của bạn:

- `upload-function`: Sao chép mã nguồn từ GitHub và tải lên S3, sau đó kích hoạt một sự kiện EventBridge.
- `deploy-function`: Xử lý quá trình triển khai thực tế (ví dụ: cập nhật môi trường, thay đổi trạng thái, ghi dữ liệu vào DynamoDB).

Bạn cũng sẽ tạo và cấu hình **IAM roles** để các hàm Lambda này có thể tương tác một cách an toàn với các dịch vụ AWS.

---

### Nội dung

- [2.2.1 Tạo Upload Lambda Function](2.2.1-createlambdaupload/)
- [2.2.2 Tạo Deploy Lambda Function](2.2.2-createlambdadeploy/)