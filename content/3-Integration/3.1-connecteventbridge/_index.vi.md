---
title: "Kết nối Rule EventBridge để Triển khai Lambda"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

Trong bước này, bạn sẽ kết nối rule EventBridge có tên `uploaded_success` với hàm Lambda `deploy-function`.

Việc tích hợp này đảm bảo rằng khi một gói triển khai được tải lên S3 bởi `upload-function`, một sự kiện sẽ được phát ra và tự động kích hoạt hàm `deploy-function`.

---

#### Điều hướng đến Bảng điều khiển EventBridge

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/home)

2. Trong thanh bên, nhấn vào **Event buses**

  ![](/images/3.integration/001-connecteventbridge.png)

3. Chọn event bus tùy chỉnh có tên **`upload`**

  ![](/images/3.integration/002-connecteventbridge.png)

---

#### Cấu hình Target của Rule

1. Nhấn tab **Rules** dưới event bus đã chọn

2. Tìm và nhấn vào rule có tên **`uploaded_success`**

![](/images/3.integration/003-connecteventbridge.png)

3. Kéo xuống phần **Targets**

![](/images/3.integration/004-connecteventbridge.png)

4. Nếu chưa có target, nhấn **Add another target**. Nếu đã có, nhấn **Edit**

   - **Target type**: `AWS service`  
   - **Service**: `Lambda function`  
   - **Function**: `deploy-function`  
   - Giữ nguyên các tùy chọn khác mặc định

![](/images/3.integration/005-connecteventbridge.png)  
![](/images/3.integration/006-connecteventbridge.png)  
![](/images/3.integration/007-connecteventbridge.png)

5. Nhấn **Skip to review and update**.

![](/images/3.integration/008-connecteventbridge.png)

6. Dán mẫu sự kiện (event pattern) sau:

```json
{
  "source": ["dewebdeploy.upload"],
  "detail-type": ["DeploymentUploaded"]
}
```
7. Nhấn **Update rule**.

![](/images/3.integration/009-connecteventbridge.png)

---

#### Kết quả mong đợi  
Sau khi thiết lập:  
  - `upload-function` phát ra sự kiện `DeploymentUploaded` đến event bus `upload`  
  - EventBridge nhận diện sự kiện này qua rule `uploaded_success`  
  - `deploy-function` được tự động kích hoạt

---

#### Bước tiếp theo  
Tiếp tục đến [Cấu hình IAM Role hoàn chỉnh](../3.2-completeiamrole/)