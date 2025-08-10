---
title: "Tích hợp hệ thống"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice info %}}
Trong phần này, bạn sẽ tích hợp tất cả các thành phần đã tạo trước đó — bao gồm Lambda, EventBridge, IAM Roles và API Gateway — vào một quy trình triển khai hoạt động hoàn chỉnh. Việc này giúp các dịch vụ giao tiếp với nhau một cách an toàn và hiệu quả.
{{% /notice %}}

Sau khi hoàn thành, hệ thống của bạn sẽ sẵn sàng tiếp nhận các yêu cầu triển khai thông qua API, tự động tải mã nguồn lên, thực hiện triển khai và ghi lại trạng thái triển khai.

---

### Nội dung

- [3.1 Kết nối EventBridge Rule với Lambda triển khai](3.1-connecteventbridge/)
- [3.2 Cấu hình đầy đủ IAM Roles cho Lambda](3.2-completeiamroles/)
- [3.3 Kiểm tra kết nối giữa API Gateway và Lambda](3.3-testapigateway/)