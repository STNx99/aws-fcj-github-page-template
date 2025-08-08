---
title: "Upload Source Code via Lambda Upload"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

Trong bước này, bạn sẽ kiểm tra **Lambda Upload function**, có nhiệm vụ:

- Clone source code từ GitHub repository  
- Upload file zip lên S3 bucket  
- Gửi một sự kiện tùy chỉnh tới EventBridge để bắt đầu quy trình triển khai

Lambda function này **phải được tạo sẵn và cấu hình đầy đủ**, bao gồm:

- Tích hợp GitHub (qua Lambda Layer hoặc thư viện bên trong package)
- Quyền truy cập S3, DynamoDB, và EventBridge
- Timeout: 2 phút
- Môi trường chạy Node.js hoặc Python có hỗ trợ `git` (qua Lambda layer hoặc bundling)

---

#### Cập nhật mã nguồn cho Lambda Upload (nếu chưa có)

Lambda `upload` cần thực hiện các bước sau:

1. Clone GitHub repository (ví dụ: [TanPhat23/awscode](https://github.com/TanPhat23/awscode))
2. Nén (zip) mã nguồn
3. Upload file zip lên S3
4. Gửi custom event đến EventBridge

Nếu Lambda của bạn chưa có đoạn mã clone GitHub, hãy cập nhật nó từ repo mẫu:  
https://github.com/TanPhat23/awscode

---

#### Upload file .zip (Deploy package) lên Lambda

Trước khi test, bạn cần:

1. Build và zip mã nguồn Lambda `upload` nếu bạn đã thay đổi logic
2. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)
3. Chọn hàm `upload`, nhấn nút **Upload from** → **.zip file**
4. Tải lên file zip mới (có thể tạo bằng lệnh `zip -r function.zip .` trong thư mục project)

---

#### Invoke Upload Lambda Function (Test thủ công)

Bạn có thể test Lambda theo hai cách: trực tiếp trên AWS Lambda Console hoặc thông qua API Gateway (cấu hình ở bước sau).

**Bước thực hiện:**

1. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)
2. Chọn function tên `upload`
3. Vào tab **Test**
4. Tạo event test mới với nội dung sau:

```json
{
  "httpMethod": "POST",
  "path": "/deploy",
  "body": "{\"repoUrl\": \"https://github.com/TanPhat23/staticwebsite\"}"
}
```

Lưu ý: Dữ liệu test sử dụng format giống như khi gọi qua API Gateway. Lambda cần xử lý `event.body` đúng cách trong code  
(ví dụ: `JSON.parse(event.body)` nếu dùng Node.js).

Nhấn nút **Test** để kích hoạt Lambda

---

#### Kết quả mong đợi nếu thành công:

- Source code được **clone từ GitHub**
- Mã nguồn được **nén thành file zip**
- File zip được **upload lên S3 bucket** (ví dụ: `awsdeplybucket12345`)
- Một **custom event** được gửi tới EventBridge với `source: dewebdeploy.upload`

---

#### Kiểm tra kết quả trên S3

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Mở bucket `awsdeplybucket12345`
3. Kiểm tra xem file zip (chứa source code) đã được upload chưa

---

#### Kiểm tra EventBridge Event

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/)
2. Vào mục **Event Buses**, chọn event bus tên `upload`
3. Chọn tab **Monitoring**, sau đó nhấn **View metrics in CloudWatch**
4. Kiểm tra biểu đồ invocation hoặc log để xác nhận sự kiện đã được gửi

---

Sau khi hoàn tất bước này, Lambda `deploy` sẽ được kích hoạt tự động nếu bạn đã cấu hình rule đúng trên EventBridge.

Tiếp tục bước tiếp theo để kiểm tra trạng thái deployment:

[Next: Check Deployment Status via API](../4.2-checkstatus/)