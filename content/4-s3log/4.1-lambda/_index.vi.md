---
title: "Tải Mã Nguồn Lên Lambda Upload và Lambda Deploy"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

Trong bước này, bạn sẽ kiểm tra chức năng **Lambda Upload** và **Lambda Deploy**, có nhiệm vụ:

- Clone mã nguồn từ một kho GitHub  
- Tải file zip lên S3 bucket  
- Gửi sự kiện tùy chỉnh đến EventBridge để bắt đầu quá trình triển khai

Các hàm Lambda này **phải được tạo sẵn và cấu hình đúng**, bao gồm:

- Tích hợp GitHub (qua Lambda Layer hoặc thư viện tích hợp sẵn)
- Quyền truy cập S3, DynamoDB và EventBridge
- Thời gian timeout: 2 phút
- Môi trường runtime (Node.js hoặc Python) hỗ trợ `git` (qua Lambda layer hoặc đóng gói)

---

#### Cập Nhật Mã Nguồn Lambda Upload (nếu chưa có)

Hàm Lambda `upload` nên thực hiện các bước sau:

1. Clone repository GitHub (ví dụ: [TanPhat23/awscode](https://github.com/TanPhat23/awscode))

![](/images/4.test/001-uploadlambda.png)
![](/images/4.test/002-uploadlambda.png)

2. Nén mã nguồn tải lên trên `awscode/lambdacode`

![](/images/4.test/003-uploadlambda.png)
![](/images/4.test/004-uploadlambda.png)

3. Tải file zip lên S3

![](/images/4.test/005-uploadlambda.png)
![](/images/4.test/006-uploadlambda.png)
![](/images/4.test/007-uploadlambda.png)
![](/images/4.test/008-uploadlambda.png)
![](/images/4.test/009-uploadlambda.png)

4. Gửi sự kiện tùy chỉnh đến EventBridge

![](/images/4.test/010-uploadlambda.png)
![](/images/4.test/011-uploadlambda.png)

Nếu kết quả kiểm tra như hình dưới thì là chính xác.

![](/images/4.test/012-uploadlambda.png)

Nếu hàm Lambda của bạn chưa có logic clone GitHub, hãy cập nhật bằng repo mẫu:  
https://github.com/TanPhat23/awscode

---

#### Tải file .zip (Gói Deploy) lên Lambda

Trước khi kiểm tra, bạn cần:

1. Build và zip mã nguồn Lambda `upload` (nếu bạn đã thực hiện thay đổi)
2. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)
3. Chọn hàm `upload`, sau đó nhấn **Upload from** → **.zip file**
4. Tải lên file zip đã cập nhật (bạn có thể tạo bằng `zip -r function.zip .` từ thư mục dự án của bạn)

---
#### Thêm biến môi trường (nếu chưa có)
1. Trong cấu hình Lambda function, kéo xuống **Environment variables**.
2. Thêm các biến môi trường sau:
    - `BUCKET_NAME`: Tên S3 bucket của bạn (ví dụ: `awsdeplybucket12345`) hoặc tên s3 bucket của bạn
    - `DEPLOYMENT_TABLE_NAME`: Tên bảng DynamoDB của bạn (ví dụ: `DeploymentUploaded`) hoặc tên bảng tùy chỉnh của bạn
![env](/images/4.test/021-env.png)

#### Gọi thực thi hàm Lambda Upload (Kiểm tra thủ công)

Bạn có thể kiểm tra hàm Lambda bằng hai cách: trực tiếp từ AWS Lambda Console hoặc sau này qua API Gateway.

**Các bước kiểm tra thủ công:**

1. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)
2. Chọn hàm có tên `upload-function`

![](/images/4.test/005-uploadlambda.png)

3. Mở tab **Test**

![](/images/4.test/010-uploadlambda.png)

4. Tạo một test event mới với nội dung sau:

```json
{
  "httpMethod": "POST",
  "path": "/deploy",
  "body": "{\"repoUrl\": \"https://github.com/TanPhat23/staticwebsite\"}"
}
```

![](/images/4.test/013-uploadlambda.png)

**Lưu ý:** Dữ liệu kiểm tra này mô phỏng một request được gửi qua API Gateway.  
Đảm bảo mã Lambda của bạn xử lý `event.body` đúng cách  
(ví dụ: `JSON.parse(event.body)` nếu sử dụng Node.js).

5. Nhấn **Test** để gọi thực thi hàm Lambda.

![](/images/4.test/014-uploadlambda.png)

Nếu kết quả kiểm tra như bên dưới thì là chính xác.

![](/images/4.test/015-uploadlambda.png)

---

#### Kết quả mong đợi nếu thành công

- Mã nguồn được **clone từ GitHub**
- Mã được **nén thành zip**
- File zip được **tải lên S3 bucket** (ví dụ: `awsdeplybucket12345`)
- Một **sự kiện tùy chỉnh** được gửi đến EventBridge với `source: dewebdeploy.upload`

---

#### Xác minh việc Upload trong S3

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Mở bucket `awsdeplybucket12345`

![](/images/4.test/016-uploadlambda.png)

3. Kiểm tra xem file zip (chứa mã nguồn) đã được tải lên chưa

![](/images/4.test/017-uploadlambda.png)

---

#### Xác minh EventBridge Event

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/)
2. Mở **Event Buses**, và chọn event bus có tên `upload`

![](/images/4.test/018-uploadlambda.png)

3. Chuyển đến tab **Monitoring**, sau đó nhấn **View metrics in CloudWatch**

![](/images/4.test/019-uploadlambda.png)

4. Kiểm tra biểu đồ invocation hoặc logs để xác minh rằng event đã được gửi

![](/images/4.test/020-uploadlambda.png)

---

Sau khi hoàn thành bước này, hàm Lambda `deploy` sẽ được tự động kích hoạt  
nếu EventBridge rule đã được cấu hình chính xác.

Tiếp tục bước tiếp theo để kiểm tra trạng thái deployment:

[Tiếp theo: Kiểm tra Trạng thái Deployment qua API](../4.2-checkstatus/)

#### Tải mã nguồn Lambda Deploy (nếu chưa có)
1. Nén mã nguồn tải lên trên `awscode/lambdacode/deploy` (thực hiện các bước tương tự như hàm upload)

2. Tải file zip lên S3 (thực hiện các bước tương tự như hàm upload)

#### Thêm biến môi trường cho lambda deploy (nếu chưa có)
1. Trong cấu hình Lambda function, kéo xuống **Environment variables**.
2. Thêm các biến môi trường sau:
    - `BUCKET_NAME`: Tên S3 bucket của bạn (ví dụ: `awsdeplybucket12345`) hoặc tên s3 bucket của bạn
    - `DEPLOYMENT_TABLE_NAME`: Tên bảng DynamoDB của bạn (ví dụ: `DeploymentUploaded`) hoặc tên bảng tùy chỉnh của bạn
![env](/images/4.test/021-env.png)

#### Gọi thực thi hàm Lambda Deploy (Kiểm tra thủ công)
Gửi lại custom event đến hàm Lambda `upload` để kiểm tra quá trình deployment.
1. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)
2. Chọn hàm có tên `upload-function`
3. Mở tab **Test**
4. Tạo một test event mới với nội dung sau (nếu chưa tạo):

```json
{
  "httpMethod": "POST",
  "path": "/deploy",
  "body": "{\"repoUrl\": \"https://github.com/TanPhat23/staticwebsite\"}"
}
```
![](/images/4.test/013-uploadlambda.png)
5. Nhấn **Test** để gọi thực thi hàm Lambda.
![](/images/4.test/014-uploadlambda.png)
#### Kiểm tra S3 bucket
1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Mở bucket `awsdeplybucket12345`
3. Sẽ có một thư mục mới tên `dist` chứa các file đã deploy
![](/images/4.test/022-deploylambda.png)

---
Sau khi hoàn thành bước này, hàm Lambda `deploy` sẽ được tự động kích hoạt  
nếu EventBridge rule đã được cấu hình chính xác.

Tiếp tục bước tiếp theo để kiểm tra trạng thái triển khai:

[Tiếp theo: Kiểm tra trạng thái triển khai qua API](../4.2-checkstatus/)
