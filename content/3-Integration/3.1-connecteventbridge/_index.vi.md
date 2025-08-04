---
title: "Kết nối EventBridge Rule với Lambda Deploy"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

### Mục tiêu

Trong bước này, bạn sẽ kết nối rule **`uploaded_success`** của EventBridge với hàm Lambda **`deploy-function`**. Việc tích hợp này đảm bảo rằng sau khi mã nguồn được tải lên thành công, một sự kiện sẽ được kích hoạt để bắt đầu quá trình triển khai tự động.

---

### Các bước thực hiện

#### 1. Truy cập [AWS EventBridge Console](https://console.aws.amazon.com/events/home)

#### 2. Trong thanh điều hướng bên trái, chọn **Event buses**  
- Chọn Event Bus tùy chỉnh có tên là **`upload`**

#### 3. Nhấn vào **Rules**, sau đó chọn rule có tên **`uploaded_success`**

#### 4. Trong phần **Targets**, nhấn **Edit** (hoặc **Add target** nếu chưa có)

- **Target type**: Lambda function  
- **Function**: `deploy-function`  
- Giữ các thiết lập mặc định  
- Nhấn **Update** (hoặc **Add**)

---

### Mẫu sự kiện (Event Pattern)

Rule này sẽ lắng nghe các sự kiện có nội dung như sau:

```json
{
  "source": ["dewebdeploy.upload"],
  "detail-type": ["DeploymentUploaded"]
}
```

Sự kiện này sẽ được gửi từ upload-function sau khi quá trình tải mã nguồn lên S3 hoàn tất.

Kết quả mong đợi
Sau khi tích hợp, khi upload-function gửi sự kiện đến EventBridge, rule sẽ tự động kích hoạt hàm deploy-function để thực hiện triển khai ứng dụng.

Bạn có thể tiếp tục sang bước tiếp theo: 3.2 – Thiết lập quyền truy cập (IAM Role hoàn chỉnh)