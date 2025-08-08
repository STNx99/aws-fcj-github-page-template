---
title: "Xóa S3 Bucket và Bảng DynamoDB"
date: "`r Sys.Date()`"
weight: 11
chapter: false
pre: " <b> 6.2 </b> "
---

Trong bước này, bạn sẽ xóa **S3 bucket** và **bảng DynamoDB** được sử dụng trong hệ thống triển khai của bạn.

Tài nguyên cần xóa:

- S3 bucket: `awsdeplybucket12345`  
- Bảng DynamoDB: (bảng mà bạn đã tạo với khóa phân vùng `id`)

---

#### Xóa S3 Bucket

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)

2. Trong danh sách **Buckets**, tìm kiếm `awsdeplybucket12345`

3. Nhấp vào tên bucket để mở

![](/images/6.clean/001-deletes3dynamodb.png)

4. Trước khi có thể xóa bucket, bạn cần làm trống nó:
   - Nhấp vào **Empty**
   - Xác nhận việc xóa bằng cách nhập tên bucket
   - Nhấp **Empty bucket**

![](/images/6.clean/002-deletes3dynamodb.png)  
![](/images/6.clean/003-deletes3dynamodb.png)

5. Sau khi bucket đã được làm trống, quay lại trang tổng quan bucket

6. Nhấp **Delete**

![](/images/6.clean/004-deletes3dynamodb.png)

7. Xác nhận việc xóa bằng cách nhập lại tên bucket, sau đó nhấp **Delete bucket**

![](/images/6.clean/005-deletes3dynamodb.png)

---

#### Xóa bảng DynamoDB

1. Truy cập [DynamoDB Console](https://console.aws.amazon.com/dynamodb/)

2. Trong menu bên trái, nhấp **Tables (Bảng)**

![](/images/6.clean/006-deletes3dynamodb.png)

3. Tìm bảng bạn đã tạo (có thể có tên như `DeploymentUploaded`)

![](/images/6.clean/007-deletes3dynamodb.png)

4. Nhấp vào tên bảng để mở chi tiết

5. Ở góc trên bên phải, nhấp **Actions** → **Delete table (Xóa bảng)**

![](/images/6.clean/008-deletes3dynamodb.png)

6. Xác nhận việc xóa bằng cách nhập tên bảng

7. Nhấp **Delete (Xóa)**

![](/images/6.clean/009-deletes3dynamodb.png)

---

Khi cả S3 bucket và bảng DynamoDB đã được xóa, các tài nguyên lưu trữ chính của bạn sẽ được gỡ bỏ hoàn toàn khỏi tài khoản AWS.

---

#### Bước tiếp theo

Tiếp tục đến [6.3 – Xóa tài nguyên EventBridge](../6.3-deleteeventbridge/)