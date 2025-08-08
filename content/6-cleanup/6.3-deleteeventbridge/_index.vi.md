---
title: "Xóa Tài Nguyên EventBridge"
date: "`r Sys.Date()`"
weight: 12
chapter: false
pre: " <b> 6.3 </b> "
---

Trong bước này, bạn sẽ xóa các tài nguyên **EventBridge** đã được sử dụng để kết nối giữa `upload-function` và `deploy-function`.

Tài nguyên cần xóa:

- Quy tắc sự kiện: `uploaded_success`  
- Event bus: `upload`

---

#### Xóa Quy Tắc Sự Kiện (Event Rule)

1. Truy cập [Amazon EventBridge Console – Rules](https://console.aws.amazon.com/events/home#/rules)

2. Ở góc trên bên trái, chọn **upload** trong danh sách event bus

![](/images/6.clean/001-deleteeventbridge.png)

3. Tìm quy tắc có tên `uploaded_success`

4. Tích chọn vào checkbox bên cạnh tên quy tắc

5. Nhấp vào **Delete (Xóa)**

![](/images/6.clean/002-deleteeventbridge.png)

6. Xác nhận xóa bằng cách nhấp **Delete**

![](/images/6.clean/003-deleteeventbridge.png)

---

#### Xóa Event Bus

1. Truy cập [Amazon EventBridge Console – Event Buses](https://console.aws.amazon.com/events/home#/event-buses)

2. Tìm event bus tùy chỉnh có tên là `upload`

![](/images/6.clean/004-deleteeventbridge.png)

3. Tích chọn vào checkbox bên cạnh

4. Nhấp **Delete**

![](/images/6.clean/005-deleteeventbridge.png)

5. Xác nhận việc xóa bằng cách nhấp **Delete**

![](/images/6.clean/006-deleteeventbridge.png)

> **Lưu ý:** Bạn phải xóa tất cả các quy tắc liên kết với event bus trước khi có thể xóa event bus đó.

---

Sau khi quy tắc sự kiện và event bus tùy chỉnh đã bị xóa, tích hợp EventBridge sẽ được loại bỏ hoàn toàn.

---

#### Bước tiếp theo

Tiếp tục đến [6.4 – Xóa API Gateway](../6.4-deleteapigateway/)