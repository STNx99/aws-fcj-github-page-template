---
title: "Tạo Upload Lambda Function"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.2.1 </b> "
---

Trong bước này, bạn sẽ tạo **Upload Lambda Function**.

Hàm này chịu trách nhiệm cho các tác vụ sau:
- Sao chép một repository từ GitHub
- Đóng gói mã nguồn thành tệp ZIP
- Tải tệp này lên S3 bucket (`awsdeplybucket12345`)
- Gửi một sự kiện EventBridge (`DeploymentUploaded`) để kích hoạt quy trình triển khai

---

#### Tạo Lambda Function

1. Truy cập [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)

2. Nhấn **Create function**

   ![Create Lambda Function](/images/2.preparation/001-createuploadlambda.png)

3. Trong phần cấu hình, nhập các thông tin sau:

   - **Function name**: `upload-function`  
   - **Runtime**: `Node.js 22.x`  
   - **Permissions**: Chọn `Create a new role with basic Lambda permissions`

   ![Create Lambda Function](/images/2.preparation/002-createuploadlambda.png)

4. Nhấn **Create function**

   ![Create Lambda Function](/images/2.preparation/003-createuploadlambda.png)

---

#### Cấu hình Cơ bản

1. Sau khi tạo hàm, chuyển đến tab **Configuration**

   ![Click Configuration](/images/2.preparation/004-createuploadlambda.png)

2. Trong phần **General configuration**, nhấn **Edit** và cập nhật:

   - **Timeout**: `2 phút`  
   - *(Tuỳ chọn)* **Memory**: `1024 MB` (đề xuất nếu repo Git lớn)

   ![Click Edit](/images/2.preparation/005-createuploadlambda.png)  
   ![Edit Timeout and Memory](/images/2.preparation/006-createuploadlambda.png)

3. Nhấn **Save**

   ![Click Save](/images/2.preparation/007-createuploadlambda.png)

---

#### Thêm Git Layer

1. Cuộn xuống phần **Layers**, nhấn **Add a layer**

   ![Add a layer](/images/2.preparation/001-addgitlayer.png)

2. Chọn:
   - **Specify an ARN**
   - Dán ARN sau:
     ```
     arn:aws:lambda:ap-southeast-1:553035198032:layer:git-lambda2:8
     ```

   ![Paste ARN](/images/2.preparation/002-addgitlayer.png)

3. Nhấn **Add**

   ![Click Add](/images/2.preparation/003-addgitlayer.png)

---

#### Gán Chính sách IAM

1. Vào tab **Permissions** của hàm

2. Nhấn vào tên role để mở IAM console

   ![Click on the role name](/images/2.preparation/008-createuploadlambda.png)

3. Gán các chính sách AWS quản lý sau:
   - `AmazonS3FullAccess`
   - `AmazonDynamoDBFullAccess`
   - `AmazonEventBridgeFullAccess`

   ![Add Attach](/images/2.preparation/009-createuploadlambda.png)  
   ![Choose Attach](/images/2.preparation/010-createuploadlambda.png)

4. Thêm chính sách tuỳ chỉnh để cho phép tải lên S3:

   - Trong trang role, nhấn **Add permissions** → **Create inline policy**

   ![Create inline policy](/images/2.preparation/011-createuploadlambda.png)

   - Tại "Select a service", nhấn **choose a service**

   ![Click choose a service](/images/2.preparation/012-createuploadlambda.png)

   - Chọn **S3**

   ![Select S3](/images/2.preparation/013-createuploadlambda.png)

   - Sao chép đoạn JSON sau:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": "s3:PutObject",
         "Resource": "arn:aws:s3:::awsdeplybucket12345/*"
       }
     ]
   }
   ```
- Trong màn hình tạo chính sách (Create policy), chuyển sang tab **JSON** và **dán đoạn JSON sau**:

  ![Paste the following JSON](/images/2.preparation/014-createuploadlambda.png)

- Nhấn **Next**

  ![Click Next](/images/2.preparation/015-createuploadlambda.png)

- Nhập tên chính sách là `upload` và nhấn **Create Policy**

  ![Create policy](/images/2.preparation/016-createuploadlambda.png)

---

#### Bước tiếp theo
Tiếp tục với [Tạo Deploy Lambda Function](../2.2.2-createlambdadeploy/)