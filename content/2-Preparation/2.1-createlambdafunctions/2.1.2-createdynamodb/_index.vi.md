---
title: "Tạo Lambda Function Upload"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.1.2 </b> "
---

Trong bước này, bạn sẽ tạo một **Lambda function** có nhiệm vụ lấy mã nguồn từ repository GitHub, tải lên **S3 bucket**, sau đó kích hoạt một sự kiện **EventBridge** để tiếp tục quá trình triển khai.

---

#### Bước 1: Tạo Lambda Function Upload

1. Truy cập [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)
2. Nhấn **Create function**

   ![Tạo Lambda](/images/2.serverless/010-createlambda.png)

3. Ở trang **Create function**:
   - **Function name**: `upload-function`
   - **Runtime**: Chọn runtime phù hợp, ví dụ `Python 3.9` hoặc `Node.js 18.x`
   - **Execution role**: Chọn **Create a new role with basic Lambda permissions**

   Nhấn **Create function**

   ![Cấu hình Lambda](/images/2.serverless/011-createlambda-config.png)

---

#### Bước 2: Thêm Git Layer vào Lambda

1. Trên trang Lambda function vừa tạo, kéo xuống phần **Layers**, chọn **Add a layer**
2. Chọn **Specify an ARN**
3. Dán ARN sau:  
   `arn:aws:lambda:ap-southeast-1:553035198032:layer:git-lambda2:8`

Nhấn **Add**

![Thêm Layer](/images/2.serverless/012-addlayer.png)

---

#### Bước 3: Cập nhật IAM Role cho Lambda

Lambda function cần quyền để:
- Upload file lên S3
- Ghi dữ liệu vào DynamoDB
- Gửi sự kiện đến EventBridge

1. Vào **IAM Console > Roles**
2. Tìm và mở role tự động tạo khi bạn tạo Lambda (ví dụ `lambda-role-upload-function`)
3. Gắn các **Managed Policies** sau:
   - `AmazonS3FullAccess`
   - `AmazonEventBridgeFullAccess`
   - `AmazonDynamoDBFullAccess`
   - *(Tuỳ chọn)* `AmazonDynamoDBFullAccess_v2`

4. Thêm **Inline Policy** sau để giới hạn quyền truy cập S3:

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
---
#### Bước 4: Upload code Lambda
Bạn có thể tải code Lambda lên dưới dạng file .zip hoặc viết trực tiếp trong trình soạn thảo.

```python
import boto3
import subprocess
import json

def lambda_handler(event, context):
    repo_url = "https://github.com/your-user/your-repo.git"
    output_zip = "/tmp/deploy.zip"

    # Clone repo GitHub về thư mục /tmp
    subprocess.run(["git", "clone", repo_url, "/tmp/code"], check=True)

    # Nén code (yêu cầu có zip trong layer)
    subprocess.run(["zip", "-r", output_zip, "/tmp/code"], check=True)

    # Upload lên S3
    s3 = boto3.client('s3')
    with open(output_zip, "rb") as f:
        s3.upload_fileobj(f, "awsdeplybucket1234", "deploy.zip")

    # Gửi sự kiện đến EventBridge
    eventbridge = boto3.client('events')
    eventbridge.put_events(
        Entries=[
            {
                'Source': 'dewebdeploy.upload',
                'DetailType': 'DeploymentUploaded',
                'Detail': json.dumps({"status": "uploaded"}),
                'EventBusName': 'upload'
            }
        ]
    )

    return {
        "statusCode": 200,
        "body": json.dumps("Upload và gửi sự kiện thành công.")
    }
```
---
Bước tiếp theo: Thiết lập IAM Role cho Lambda Upload