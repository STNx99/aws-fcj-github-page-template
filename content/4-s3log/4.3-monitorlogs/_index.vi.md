---
title: "Giám sát Logs và Sự kiện"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

Trong bước này, bạn sẽ học cách giám sát các log và sự kiện được tạo ra bởi các hàm Lambda và quy tắc EventBridge để đảm bảo quy trình triển khai (deployment pipeline) hoạt động chính xác.

#### Giám sát Log của Lambda trên CloudWatch

1. Truy cập [CloudWatch Console](https://console.aws.amazon.com/cloudwatch/home).
2. Nhấp vào **Logs** trong thanh bên trái.
3. Tìm các nhóm log cho hàm Lambda của bạn (ví dụ: `/aws/lambda/upload-function` và `/aws/lambda/deploy-function`).

![CloudWatch Logs](/images/4.test/001-monitorlogs.png)

4. Nhấp vào nhóm log và xem các luồng log gần đây để kiểm tra chi tiết quá trình thực thi, lỗi và thông điệp hệ thống.

![](/images/4.test/002-monitorlogs.png)

#### Kiểm tra sự kiện từ EventBridge

1. Truy cập [EventBridge Console](https://console.aws.amazon.com/events/home).
2. Nhấp vào **Event buses**, sau đó chọn bus sự kiện tùy chỉnh có tên **upload**.

![](/images/4.test/003-monitorlogs.png)

3. Điều hướng đến tab **Monitoring**.
4. Nhấp vào **View metrics in CloudWatch** để xem các số liệu thống kê về lượt gọi và trạng thái xử lý sự kiện.

![](/images/4.test/004-monitorlogs.png)
![EventBridge Metrics](/images/4.test/006-monitorlogs.png)

---

Bằng cách thường xuyên kiểm tra các log và sự kiện này, bạn có thể nhanh chóng phát hiện và xử lý các vấn đề trong quy trình triển khai.

Tiếp tục bước tiếp theo để tìm hiểu cách triển khai sản phẩm và tích hợp với giao diện người dùng (frontend).

[Tiếp theo: Triển khai sản phẩm và tích hợp giao diện](../5-deploytoamplify/)