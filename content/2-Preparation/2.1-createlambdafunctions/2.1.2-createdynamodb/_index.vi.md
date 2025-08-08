---
title: "Tạo bảng DynamoDB"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.1.2 </b> "
---

Trong bước này, bạn sẽ tạo một **bảng DynamoDB** để lưu trữ thông tin trạng thái triển khai. Bảng này sẽ được các hàm Lambda truy cập và cập nhật như một phần trong quy trình theo dõi triển khai.

---

#### Tạo bảng DynamoDB

1. Truy cập [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodb/)

2. Nhấn **Create table**

   ![Nhấn Create Table](/images/2.preparation/001-createdynamodb.png)

3. Cấu hình bảng:

   - **Table name**: `DeploymentUploaded`  
   - **Partition key**: `id` (Kiểu: `String`)  
   - Giữ nguyên các thiết lập mặc định còn lại:
     - **Sort key**: *Không có*
     - **Capacity mode**: `On-demand`
     - **Table class**: `Standard`

   ![Cấu hình bảng](/images/2.preparation/002-createdynamodb.png)

4. Nhấn **Create table**

   Sau khi tạo, bảng sẽ xuất hiện trong danh sách.

   ![Bảng đã được tạo](/images/2.preparation/003-createdynamodb.png)

---

#### Ghi chú

- Thuộc tính `id` sẽ đóng vai trò là định danh duy nhất cho mỗi bản ghi triển khai.
- Sau này, bạn có thể mở rộng bảng với các thuộc tính bổ sung như `status`, `timestamp`, hoặc `log_url`.

---

#### Bước tiếp theo

Tiếp tục đến [Tạo Lambda Functions và IAM Roles](../2.2-createlambdasiamroles/)