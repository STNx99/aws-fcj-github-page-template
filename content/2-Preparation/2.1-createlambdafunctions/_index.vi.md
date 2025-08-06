---
title: "Tạo S3 Bucket và Bảng DynamoDB"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

Trong bước này, bạn sẽ chuẩn bị các dịch vụ lưu trữ và cơ sở dữ liệu hỗ trợ quy trình triển khai serverless.

Cụ thể, bạn sẽ:
- Tạo một **S3 bucket** (`awsdeplybucket1234`) để lưu trữ các gói triển khai  
- Tạo một **bảng DynamoDB** với khóa phân vùng là `id` để theo dõi trạng thái triển khai

Các tài nguyên này là nền tảng cho các hàm Lambda và pipeline dựa trên sự kiện sẽ được cấu hình ở các bước tiếp theo.

---

### Tổng Quan Kiến Trúc

Khi hoàn thành bước này, kiến trúc ban đầu sẽ như sau:

![Kiến trúc Serverless](/images/arc-lambda-dynamodb.png)

---

### Nội dung

- [2.1.1 Tạo S3 bucket](2.1.1-creates3bucket/)
- [2.1.2 Tạo bảng DynamoDB](2.1.2-createdynamodb/)