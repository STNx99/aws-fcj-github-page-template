---
title: "Chuẩn Bị"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice info %}}
Trong phần này, bạn sẽ khởi tạo tất cả các tài nguyên cần thiết trên AWS để hỗ trợ quy trình triển khai serverless. Bao gồm: một S3 Bucket để lưu trữ các tệp tĩnh, một bảng DynamoDB để theo dõi trạng thái triển khai, các hàm Lambda để tự động hóa, IAM roles để quản lý quyền truy cập, một EventBridge event bus để kích hoạt triển khai, và một API Gateway để cung cấp giao diện HTTP công khai.
{{% /notice %}}

Kết thúc phần này, bạn sẽ có một hạ tầng nền tảng đầy đủ, sẵn sàng cho việc tích hợp, kiểm thử và triển khai ở các bước tiếp theo.

---

#### Nội dung

- [2.1 Tạo S3 Bucket và Bảng DynamoDB](2.1-createlambdafunctions/)
- [2.2 Tạo Hàm Lambda và IAM Roles](2.2-createlambdasiamroles/)
- [2.3 Tạo EventBridge Event Bus và Quy tắc (Rules)](2.3-createeventbridge/)
- [2.4 Tạo API Gateway và Cấu Hình Endpoints & CORS](2.4-createapigateway/)