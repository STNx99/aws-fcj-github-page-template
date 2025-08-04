---
title: "Tạo S3 bucket và bảng DynamoDB"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1.1 </b> "
---

Trong bước này, bạn sẽ tạo một **S3 bucket** để lưu trữ mã nguồn triển khai, và một **bảng DynamoDB** để theo dõi trạng thái của các lần triển khai.

---

#### Tạo S3 Bucket: `awsdeplybucket1234`

1. Truy cập [S3 Management Console](https://s3.console.aws.amazon.com/s3/home)
2. Nhấn **Create bucket**

   ![Create Bucket](/images/2.serverless/001-createbucket.png)

3. Trong trang **Create bucket**:
   - **Bucket name**: `awsdeplybucket1234`
   - **Region**: Chọn cùng khu vực với Lambda của bạn (ví dụ: `Asia Pacific (Singapore) ap-southeast-1`)
   - Các phần còn lại giữ nguyên mặc định
   - Nhấn **Create bucket**

   ![Bucket Settings](/images/2.serverless/002-bucketsettings.png)

---

#### Tạo DynamoDB Table: `deployment-status`

1. Truy cập [DynamoDB Console](https://console.aws.amazon.com/dynamodb/home)
2. Nhấn **Create table**

   ![Create Table](/images/2.serverless/003-createdynamodb.png)

3. Cấu hình bảng:
   - **Table name**: `deployment-status`
   - **Partition key**: `id` (Type: String)
   - Các phần còn lại giữ mặc định
   - Nhấn **Create table**

   ![Table Settings](/images/2.serverless/004-dynamodbsettings.png)

---

Sau khi hoàn thành, bạn đã có:
- Một bucket S3 để chứa mã nguồn từ GitHub
- Một bảng DynamoDB để lưu trữ trạng thái của các lần deploy (thành công, lỗi, thời gian v.v.)

Tiếp theo, bạn sẽ tạo Lambda để tải mã nguồn từ GitHub và kích hoạt chuỗi triển khai.