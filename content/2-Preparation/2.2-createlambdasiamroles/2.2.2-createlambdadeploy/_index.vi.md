---
title: "Tạo Deploy Lambda Function"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2.2 </b> "
---

Trong bước này, bạn sẽ tạo **Deploy Lambda Function**.

Hàm này sẽ được kích hoạt bởi **EventBridge** sau khi quá trình upload hoàn tất. Nó sẽ mô phỏng hoặc thực hiện logic triển khai như đọc dữ liệu từ S3, cập nhật trạng thái trong DynamoDB, hoặc khởi chạy các quy trình tự động khác.

---

#### Tạo Lambda Function

1. Truy cập [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)
2. Nhấn **Create function**

   ![Create Lambda](/images/2.preparation/001-createlambdadeploy.png)

3. Trong biểu mẫu cấu hình, nhập:
   - **Function name**: `deploy-function`  
   - **Runtime**: `Node.js 22.x`  
   - **Permissions**: Chọn `Create a new role with basic Lambda permissions`

   ![Create Deploy Function](/images/2.preparation/002-createlambdadeploy.png)
   ![Click Permissions](/images/2.preparation/003-createlambdadeploy.png)

4. Nhấn **Create function**

   ![Click Create function](/images/2.preparation/004-createlambdadeploy.png)

---

#### Cấu hình thiết lập cơ bản

1. Sau khi hàm được tạo, chuyển đến tab **Configuration**

   ![Go to the Configuration](/images/2.preparation/005-createlambdadeploy.png)

2. Trong phần **General configuration**, nhấn **Edit** và cập nhật:
   - **Timeout**: `2 minutes`  
   - **Memory**: `1024 MB`

   ![Go to the Configuration](/images/2.preparation/006-createlambdadeploy.png)
   ![Edit Timeout and Memory](/images/2.preparation/007-createlambdadeploy.png)

3. Nhấn **Save**

   ![Click Add](/images/2.preparation/008-createlambdadeploy.png)

---

#### Gán quyền IAM

Để `deploy-function` có thể truy cập vào DynamoDB và S3, bạn cần gán các quyền sau:

1. Chuyển đến tab **Permissions** của hàm
2. Nhấn vào tên role để mở IAM Console

   ![Go to the Permissions](/images/2.preparation/009-createlambdadeploy.png)

3. Nhấn **Add permissions** và chọn **Attach policy**

   ![Add permissions](/images/2.preparation/010-createlambdadeploy.png)

4. Gán các chính sách được quản lý sẵn sau:
   - `AmazonDynamoDBFullAccess`
   - `AmazonS3FullAccess`
   - *(Tùy chọn)* `AmazonDynamoDBFullAccess_v2`

5. Nhấn **Add permissions**

   ![Attach Deploy Policies](/images/2.preparation/011-createlambdadeploy.png)

> Lưu ý: Bạn không cần tạo inline policy riêng cho S3 trừ khi muốn giới hạn quyền truy cập vào các đường dẫn cụ thể trong bucket.

---

#### Bước tiếp theo

Tiếp tục với [Tạo EventBridge Rule](../../2.3-createeventbridge/)