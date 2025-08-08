---
title: "Tạo Bảng DynamoDB"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.1.2 </b> "
---

Trong bước này, bạn sẽ tạo một **bảng DynamoDB** để lưu trữ thông tin trạng thái triển khai. Bảng này sau đó sẽ được các hàm Lambda truy cập và cập nhật như một phần của quy trình theo dõi triển khai.

---

#### Tạo Bảng DynamoDB

1. Truy cập [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodb/)

2. Nhấn **Create table**

   ![Click Create Table](/images/2.preparation/001-createdynamodb.png)

3. Cấu hình bảng:

   - **Tên bảng (Table name)**: `DeploymentUploaded`  
   - **Partition key**: `id` (Kiểu: `String`)  
   - Giữ nguyên các tùy chọn mặc định khác:
     - **Sort key**: *Không có*
     - **Chế độ công suất (Capacity mode)**: `On-demand`
     - **Lớp bảng (Table class)**: `Standard`

   ![Configure table settings](/images/2.preparation/002-createdynamodb.png)

4. Nhấn **Create table**

   Sau khi tạo, bảng của bạn sẽ xuất hiện trong danh sách.

   ![Table created](/images/2.preparation/003-createdynamodb.png)

---

#### Ghi chú

- Trường `id` sẽ là định danh duy nhất cho mỗi bản ghi triển khai.
- Bạn có thể mở rộng bảng sau này với các thuộc tính như `status`, `timestamp`, hoặc `log_url`.

---

#### Bước tiếp theo

Tiếp tục đến [Tạo Hàm Lambda và IAM Roles](../2.2-createlambdasiamroles/)