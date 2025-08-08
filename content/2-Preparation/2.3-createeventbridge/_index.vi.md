---
title: "Tạo Event Bus và Rule trên EventBridge"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

Trong bước này, bạn sẽ thiết lập **Event Bus** và **Rule** trong **Amazon EventBridge** để kết nối giữa `upload-function` và `deploy-function`.

Sau khi hoàn tất, luồng sự kiện tự động sẽ như sau:

> `upload-function` → (gửi sự kiện) → `EventBridge` → (rule khớp) → `deploy-function`

---

#### Tạo Event Bus

1. Truy cập [Amazon EventBridge Console](https://console.aws.amazon.com/events/home)

2. Ở menu bên trái, chọn **Event buses**

   ![Click Event Bus](/images/2.preparation/001-createbus.png)

3. Nhấn **Create event bus**

   ![Create Event Bus](/images/2.preparation/002-createbus.png)

4. Nhập các thông tin sau:
   - **Name**: `upload`
   - Các cài đặt khác giữ mặc định

   ![Enter the following name](/images/2.preparation/003-createbus.png)

5. Nhấn **Create event bus**

   ![Click Create event bus](/images/2.preparation/004-createbus.png)

---

#### Tạo Event Rule: `uploaded_success`

1. Truy cập [EventBridge Rules Console](https://console.aws.amazon.com/events/home#/rules)

2. Đảm bảo bạn đã chọn đúng **event bus** tên là `upload`

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

#### Thêm Mẫu Sự Kiện (Event Pattern)

1. Trong phần **Events**:
   - **Event source**: `Other`

2. Ở mục **Event pattern**, chọn:  
   - **Custom pattern (JSON editor)**

3. Dán mẫu JSON sau:

```json
{
  "source": ["dewebdeploy.upload"],
  "detail-type": ["DeploymentUploaded"]
}
```

![Thêm Mẫu Sự Kiện](/images/2.preparation/008-createbus.png)

4. Nhấn **Next**

![Nhấn Next](/images/2.preparation/009-createbus.png)

---

#### Cấu Hình Mục Tiêu (Target) Cho Rule

Trong phần **Target**:

- **Target type**: AWS service  
- **Service**: Lambda function  
- **Function**: `deploy-function`

![Chọn Lambda Function làm mục tiêu](/images/2.preparation/010-createbus.png)

6. Nhấn **Next**

![Nhấn Next](/images/2.preparation/011-createbus.png)

7. Xem lại cấu hình rule và nhấn **Next**

![Xem lại cấu hình](/images/2.preparation/012-createbus.png)

8. Nhấn **Create rule** để hoàn tất

![Tạo Rule](/images/2.preparation/013-createbus.png)

---

Bây giờ, khi `upload-function` phát sự kiện `DeploymentUploaded`, EventBridge sẽ tự động kích hoạt `deploy-function`.

---

#### Bước Tiếp Theo

Tiếp tục đến [Tạo API Gateway và Cấu Hình CORS](../2.4-createapigateway/)