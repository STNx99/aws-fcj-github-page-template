---
title: "Tải Mã Nguồn Lên Qua Lambda Upload"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

Trong bước này, bạn sẽ kiểm tra chức năng **Lambda Upload**, có nhiệm vụ:

- Clone mã nguồn từ một kho GitHub  
- Tạo file zip và tải lên S3 bucket  
- Gửi sự kiện tùy chỉnh đến EventBridge để bắt đầu quá trình triển khai

Hàm Lambda này **phải được tạo sẵn và cấu hình đúng**, bao gồm:

- Tích hợp GitHub (qua Lambda Layer hoặc thư viện tích hợp sẵn)
- Quyền truy cập S3, DynamoDB và EventBridge
- Thời gian timeout: 2 phút
- Môi trường runtime (Node.js hoặc Python) hỗ trợ `git` (qua Layer hoặc đóng gói)

---

#### Cập Nhật Mã Nguồn Lambda Upload (nếu chưa có)

Hàm Lambda `upload` nên thực hiện các bước sau:

1. Clone repository GitHub (ví dụ: [TanPhat23/awscode](https://github.com/TanPhat23/awscode))

![](/images/4.test/001-uploadlambda.png)  
![](/images/4.test/002-uploadlambda.png)

2. Nén mã nguồn tại `awscode/lambdacode`

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

Nếu kết quả như hình dưới là đúng.

![](/images/4.test/012-uploadlambda.png)

Nếu hàm Lambda của bạn chưa có logic clone GitHub, hãy cập nhật từ repo mẫu:  
https://github.com/TanPhat23/awscode

---

#### Tải File .zip (Gói Deploy) lên Lambda

Trước khi test, bạn cần:

1. Build và zip mã nguồn Lambda `upload` (nếu bạn đã chỉnh sửa)  
2. Truy cập [Lambda Console](https://console.aws.amazon.com/lambda/)  
3. Chọn hàm `upload`, nhấn **Upload from** → **.zip file**  
4. Tải lên file zip mới (có thể tạo bằng `zip -r function.zip .` từ thư mục dự án)

---

#### Gọi Thử Hàm Lambda Upload (Kiểm tra Thủ Công)

Bạn có thể kiểm tra hàm Lambda bằng 2 cách: trực tiếp từ Lambda Console hoặc thông qua API Gateway sau này.

**Các bước test thủ công:**

1. Vào [Lambda Console](https://console.aws.amazon.com/lambda/)  
2. Chọn hàm tên `upload-function`  

![](/images/4.test/005-uploadlambda.png)

3. Mở tab **Test**

![](/images/4.test/010-uploadlambda.png)

4. Tạo event test với nội dung sau:

```json
{
  "httpMethod": "POST",
  "path": "/deploy",
  "body": "{\"repoUrl\": \"https://github.com/TanPhat23/staticwebsite\"}"
}
```

![](/images/4.test/013-uploadlambda.png)

**Lưu ý:** Dữ liệu kiểm tra này mô phỏng một yêu cầu được gửi qua API Gateway.  
Hãy đảm bảo hàm Lambda của bạn xử lý `event.body` đúng cách  
(ví dụ: sử dụng `JSON.parse(event.body)` nếu dùng Node.js).

5. Nhấn **Test** để kích hoạt hàm Lambda.

![](/images/4.test/014-uploadlambda.png)

Nếu kết quả kiểm tra giống như bên dưới, thì mọi thứ đã hoạt động chính xác.

![](/images/4.test/015-uploadlambda.png)

---

#### Kết quả mong đợi nếu thành công

- Mã nguồn được **clone từ GitHub**
- Mã được **nén thành file zip**
- File zip được **tải lên S3 bucket** (ví dụ: `awsdeplybucket12345`)
- Một **sự kiện tùy chỉnh** được gửi đến EventBridge với `source: dewebdeploy.upload`

---

#### Xác minh việc tải lên trong S3

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Mở bucket có tên `awsdeplybucket12345`

![](/images/4.test/016-uploadlambda.png)

3. Kiểm tra xem file zip (chứa mã nguồn) đã được tải lên chưa

![](/images/4.test/017-uploadlambda.png)

---

#### Xác minh sự kiện trong EventBridge

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/)
2. Vào mục **Event Buses**, chọn bus tên `upload`

![](/images/4.test/018-uploadlambda.png)

3. Chuyển đến tab **Monitoring**, sau đó nhấn **View metrics in CloudWatch**

![](/images/4.test/019-uploadlambda.png)

4. Kiểm tra biểu đồ hoặc log để xác nhận sự kiện đã được gửi

![](/images/4.test/020-uploadlambda.png)

---

Sau khi hoàn tất bước này, hàm Lambda `deploy` sẽ được tự động kích hoạt  
nếu EventBridge rule đã được cấu hình đúng.

Tiếp tục bước tiếp theo để kiểm tra trạng thái triển khai:

[Tiếp theo: Kiểm tra trạng thái triển khai qua API](../4.2-checkstatus/)