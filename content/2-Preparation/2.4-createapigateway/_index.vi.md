---
title: "Tạo API Gateway và Cấu hình Endpoint với CORS"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 2.4 </b> "
---

Trong bước này, bạn sẽ tạo một **API Gateway** để cung cấp các HTTP endpoint gọi tới các Lambda function. Chúng ta sẽ cấu hình hai endpoint:

- **POST /deploy** → gọi Lambda function `upload-function`  
- **GET /status** → truy vấn trạng thái triển khai (cũng xử lý bởi `upload-function`)  

Bạn cũng sẽ cấu hình **CORS** để cho phép các yêu cầu từ `http://localhost:3000`.

---

#### Bước 1: Tạo HTTP API

1. Truy cập [API Gateway Console](https://console.aws.amazon.com/apigateway/home)  
2. Nhấn **Create API**

   ![Tạo API](/images/2.preparation/001-createapigateway.png)

3. Chọn **HTTP API** (không chọn Private)
4. Nhấn **Build**

   ![Tạo HTTP API](/images/2.preparation/002-createapigateway.png)

---

#### Bước 2: Cấu hình API

1. Nhập **API name**: `DeployAPI`  
2. Nhấn **Create API**

   ![Tạo API](/images/2.preparation/003-createapigateway.png)
   ![](/images/2.preparation/004-createapigateway.png)
   ![](/images/2.preparation/005-createapigateway.png)
   ![](/images/2.preparation/006-createapigateway.png)

---

#### Bước 3: Tạo Routes và tích hợp Lambda

##### Tạo route `/deploy`

1. Chọn API HTTP vừa tạo
2. Trong menu bên trái, chọn **Routes**
3. Nhấn **Create**

   ![](/images/2.preparation/007-createapigateway.png)

4. Nhập:
   - **Method**: `POST`
   - **Resource path**: `/deploy`  
5. Nhấn **Create**

   ![](/images/2.preparation/008-createapigateway.png)

##### Gắn Lambda vào route `/deploy`

1. Trong tab **Routes**, chọn route `/deploy`
2. Ở mục **Integration**, nhấn **Attach integration**

   ![](/images/2.preparation/009-createapigateway.png)

3. Nhấn **Create and attach an integration**

   ![](/images/2.preparation/010-createapigateway.png)

4. Chọn **Lambda function**
5. Chọn khu vực (region) và nhập tên function: `upload-function`

   ![](/images/2.preparation/011-createapigateway.png)

6. Nhấn **Create**

   ![](/images/2.preparation/012-createapigateway.png)

---

##### Tạo route `/status`

1. Quay lại **Routes**, nhấn **Create**

   ![](/images/2.preparation/013-createapigateway.png)

2. Chọn Method: `GET`  
3. Nhập Path: `/status`  
4. Nhấn **Create**

   ![](/images/2.preparation/014-createapigateway.png)

##### Gắn Lambda vào route `/status`

1. Chọn route `/status`
2. Nhấn **Attach integration**

   ![](/images/2.preparation/015-createapigateway.png)

3. Chọn `upload-function`  
4. Nhấn **Attach Integration**

   ![](/images/2.preparation/016-createapigateway.png)

---

#### Bước 4: Bật CORS

1. Trong menu bên trái, chọn **CORS**
2. Nhấn **Configure** cho cả `/deploy` và `/status`

   ![](/images/2.preparation/017-createapigateway.png)

3. Cấu hình CORS như sau:
   - **Access-Control-Allow-Origin**: `http://localhost:3000`
   - **Access-Control-Allow-Headers**: `content-type`
   - **Access-Control-Allow-Methods**: `GET,POST`
4. Nhấn **Add**

   ![](/images/2.preparation/018-createapigateway.png)

5. Nhấn **Save**

   ![](/images/2.preparation/019-createapigateway.png)

---

#### Tóm tắt

Hiện tại API Gateway của bạn đã cung cấp hai route:

| Method | Đường dẫn | Lambda Function  | Mô tả                        |
|--------|-----------|------------------|-------------------------------|
| POST   | /deploy   | upload-function  | Tải mã nguồn và phát sự kiện |
| GET    | /status   | upload-function  | Kiểm tra trạng thái triển khai |

Các endpoint này đã được bật CORS để chấp nhận yêu cầu từ `http://localhost:3000`.

---

#### Tiếp theo

Bạn có thể tiếp tục đến [**Chương 3: Kết nối và kiểm tra luồng triển khai**.](../../3-Integration/)