---
title: "Tích Hợp"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice info %}}
Trong phần này, bạn sẽ tích hợp tất cả các thành phần đã tạo trước đó — bao gồm Lambda, EventBridge, IAM roles và API Gateway — thành một pipeline triển khai hoàn chỉnh. Điều này đảm bảo rằng các dịch vụ có thể giao tiếp với nhau một cách an toàn và hiệu quả.
{{% /notice %}}

Sau khi hoàn tất, hệ thống của bạn sẽ sẵn sàng nhận các yêu cầu triển khai thông qua API, tự động tải lên và triển khai mã nguồn, đồng thời ghi lại trạng thái của quá trình triển khai.

---

### Nội dung

- [3.1 Kết nối Rule của EventBridge với Lambda triển khai](3.1-connecteventbridge/)
- [3.2 Cấu hình đầy đủ IAM Roles cho Lambda](3.2-completeiamroles/)
- [3.3 Kiểm tra kết nối từ API Gateway đến Lambda](3.3-testapigateway/)