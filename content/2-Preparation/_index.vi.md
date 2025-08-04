---
title: "Chuẩn bị (Preparation)"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice info %}}
Trong phần này, bạn sẽ tạo các tài nguyên cần thiết để phục vụ quy trình triển khai serverless trên AWS. Các bước bao gồm tạo S3 Bucket, DynamoDB Table, Lambda Functions, IAM Roles, EventBridge và API Gateway.
{{% /notice %}}

Sau khi hoàn tất phần chuẩn bị, bạn sẽ có đầy đủ nền tảng để thực hiện kết nối, kiểm thử và triển khai không gián đoạn ở các bước tiếp theo.

---

### Nội dung

- [2.1 Tạo S3 Bucket và DynamoDB Table](2.1-creates3-dynamodb/)
- [2.2 Tạo các Lambda Functions và IAM Roles](2.2-createlambdas-iamroles/)
- [2.3 Tạo EventBridge Event Bus và Rules](2.3-createeventbridge/)
- [2.4 Tạo API Gateway và cấu hình Endpoints, CORS](2.4-createapigateway/)
