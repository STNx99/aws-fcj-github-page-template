---
title: "Tạo Hàm Lambda Triển Khai (Deploy)"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2.2 </b> "
---

Trong bước này, bạn sẽ tạo **Hàm Lambda Triển Khai (Deploy Lambda Function)**.

Hàm này sẽ được kích hoạt bởi **EventBridge** sau khi quá trình upload hoàn tất. Nó sẽ mô phỏng hoặc thực hiện logic triển khai như đọc dữ liệu từ S3, cập nhật trạng thái trong DynamoDB hoặc kích hoạt các workflow tự động khác.

---

#### Tạo Hàm Lambda

1. Truy cập [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)
2. Nhấn **Create function**

   ![Tạo Lambda](/images/2.preparation/001-createlambdadeploy.png)

3. Trong biểu mẫu cấu hình, nhập:
   - **Function name**: `deploy-function`  
   - **Runtime**: `Node.js 22.x`  
   - **Permissions**: Chọn `Create a new role with basic Lambda permissions`

   ![Cấu hình Lambda](/images/2.preparation/002-createlambdadeploy.png)
   ![Click Permissions](/images/2.preparation/003-createlambdadeploy.png)

4. Nhấn **Create function**

   ![Click Create function](/images/2.preparation/004-createlambdadeploy.png)

---

#### Cấu Hình Cơ Bản

1. Sau khi hàm được tạo, chuyển sang tab **Configuration**

   ![Chuyển sang Configuration](/images/2.preparation/005-createlambdadeploy.png)

2. Trong phần **General configuration**, nhấn **Edit** và cập nhật:
   - **Timeout**: `2 phút`  
   - **Memory**: `1024 MB`

   ![Chỉnh timeout và memory](/images/2.preparation/006-createlambdadeploy.png)
   ![Cập nhật thông tin](/images/2.preparation/007-createlambdadeploy.png)

3. Nhấn **Save**

   ![Lưu lại](/images/2.preparation/008-createlambdadeploy.png)

---

#### Gán Quyền IAM

Để cho phép `deploy-function` truy cập DynamoDB và S3, bạn cần gán các quyền sau:

1. Vào tab **Permissions** của hàm
2. Nhấn vào tên role để mở IAM Console

   ![Vào phần Permissions](/images/2.preparation/009-createlambdadeploy.png)

3. Nhấn **Add permissions** và chọn **Attach policy**

   ![Gán quyền](/images/2.preparation/010-createlambdadeploy.png)

4. Gán các policy AWS quản lý sau:
   - `AmazonDynamoDBFullAccess`
   - `AmazonS3FullAccess`
   - *(Tùy chọn)* `AmazonDynamoDBFullAccess_v2`

5. Nhấn **Add permissions**

   ![Gán quyền thành công](/images/2.preparation/011-createlambdadeploy.png)

> **Ghi chú**: Bạn không cần tạo inline policy riêng cho S3 trừ khi muốn giới hạn quyền truy cập theo đường dẫn cụ thể trong bucket.

---

#### Bước Tiếp Theo

Tiếp tục đến [Tạo Rule EventBridge](../../2.3-createeventbridge/)