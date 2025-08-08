---
title: "Tạo EventBridge Event Bus và Rule"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

Trong bước này, bạn sẽ thiết lập **EventBridge Event Bus** và một **Rule (quy tắc)** để kết nối giữa `upload-function` và `deploy-function`.

Sau khi hoàn thành, luồng hoạt động theo sự kiện sẽ như sau:

> `upload-function` → (gửi event) → `EventBridge` → (khớp rule) → `deploy-function`

---

#### Tạo Event Bus

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/home)

2. Trong menu bên trái, nhấn **Event buses**

   ![Click Event Bus](/images/2.preparation/001-createbus.png)

3. Nhấn **Create event bus**

   ![Create Event Bus](/images/2.preparation/002-createbus.png)

4. Nhập thông tin sau:
   - **Name**: `upload`
   - Giữ nguyên các thiết lập mặc định khác

   ![Enter the following name](/images/2.preparation/003-createbus.png)

5. Nhấn **Create event bus**

   ![Click Create event bus](/images/2.preparation/004-createbus.png)

---

#### Tạo Rule: `uploaded_success`

1. Truy cập [EventBridge Rules Console](https://console.aws.amazon.com/events/home#/rules)

2. Đảm bảo bạn đã chọn **upload** event bus

3. Nhấn **Create rule**

   ![Click Create rule](/images/2.preparation/005-createbus.png)

4. Nhập thông tin rule:
   - **Name**: `uploaded_success`
   - **Event bus**: `upload`
   - **Rule type**: `Rule with an event pattern`

   ![Enter rule](/images/2.preparation/006-createbus.png)

5. Nhấn **Next**

   ![Click Next](/images/2.preparation/007-createbus.png)

---

#### Thêm Event Pattern

1. Ở mục **Events**:
   - **Event source**: `Other`

2. Tại **Event pattern**, chọn:  
   - **Custom pattern (JSON editor)**

3. Dán đoạn pattern sau vào:

```json
{
  "source": ["dewebdeploy.upload"],
  "detail-type": ["DeploymentUploaded"]
}
```

  ![Thêm Event Pattern](/images/2.preparation/008-createbus.png)

4. Nhấn **Next**

  ![Nhấn Next](/images/2.preparation/009-createbus.png)

5. Thiết lập Target là Lambda Deploy

Tại phần **Target**:

  - **Target type**: AWS service

  - **Service**: Lambda function

  - **Function**: deploy-function

  ![Thiết lập Target là Lambda Deploy](/images/2.preparation/010-createbus.png)

6. Nhấn **Next**

  ![Nhấn Next](/images/2.preparation/011-createbus.png)

7. Xem lại cấu hình rule và nhấn **Next**

  ![Xem lại cấu hình](/images/2.preparation/012-createbus.png)

8. Nhấn **Create rule**

  ![Nhấn Create rule](/images/2.preparation/013-createbus.png)

Bây giờ, khi `upload-function` phát ra một sự kiện `DeploymentUploaded`, EventBridge sẽ tự động kích hoạt `deploy-function`.

---

#### Bước tiếp theo

Tiếp tục với [Tạo API Gateway và Cấu hình CORS](../2.4-createapigateway/)


