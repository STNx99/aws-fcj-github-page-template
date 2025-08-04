---
title: "Thiết lập quyền truy cập (IAM Role hoàn chỉnh)"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 3.2 </b> "
---

### Mục tiêu

Trong bước này, chúng ta sẽ đảm bảo rằng tất cả các hàm Lambda đều có đầy đủ quyền (IAM Role) để truy cập các dịch vụ AWS cần thiết như: **S3**, **DynamoDB**, **EventBridge**, v.v. Điều này rất quan trọng để pipeline hoạt động trơn tru và bảo mật.

---

### 1. Role cho Lambda `upload-function`

#### Gán các Managed Policies:

- `AmazonDynamoDBFullAccess`
- `AmazonDynamoDBFullAccess_v2` *(tùy chọn)*
- `AmazonEventBridgeFullAccess`

#### Thêm Inline Policy cho truy cập S3 có phạm vi:

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

Thao tác:
1. Truy cập IAM Console – Roles
2. Chọn role của upload-function
3. Thêm Managed Policies như trên
4. Thêm Inline Policy vào role

2. Role cho Lambda deploy-function
Gán các Managed Policies:
AmazonDynamoDBFullAccess

AmazonDynamoDBFullAccess_v2 (tùy chọn)

AmazonS3FullAccess

📍 Lưu ý: Hàm này cần quyền để đọc file từ S3 và cập nhật trạng thái vào DynamoDB.

3. Kiểm tra lại vai trò IAM
Đảm bảo:

Đúng role đã được liên kết với đúng hàm Lambda

Không cấp quyền dư thừa (nguyên tắc “Least Privilege”)

Các hàm Lambda có thể ghi logs (mặc định sẽ có quyền CloudWatch thông qua AWSLambdaBasicExecutionRole)

Kết quả mong đợi
Cả hai hàm Lambda đều đã có đủ quyền để:
Ghi/đọc từ S3 và DynamoDB
Gửi sự kiện EventBridge
Ghi logs ra CloudWatch
Bạn có thể tiếp tục sang bước 3.3 - Kiểm tra kết nối API Gateway với Lambda để xác minh hệ thống hoạt động như mong đợi.