---
title: "Kiểm thử & Thực thi"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

{{% notice info %}}
Trong giai đoạn này, chúng ta sẽ kiểm thử quy trình triển khai bằng cách tải lên mã nguồn, kích hoạt quy trình triển khai, và theo dõi các log và sự kiện. Việc này nhằm đảm bảo rằng tất cả các thành phần — Lambda, API Gateway, EventBridge và DynamoDB — được tích hợp và hoạt động đúng cách.
{{% /notice %}}

Bằng cách hoàn thành các bước này, bạn sẽ xác thực luồng hoạt động toàn diện của pipeline triển khai và đảm bảo rằng nó sẵn sàng cho môi trường sản xuất.

---

#### Nội dung liên quan

- [4.1 Tải mã nguồn qua Lambda Upload](4.1-uploadlambda/)
- [4.2 Kiểm tra trạng thái triển khai qua API](4.2-checkstatus/)  
- [4.3 Giám sát logs và sự kiện](4.3-monitorlogs/)