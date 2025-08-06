---
title: "Tạo S3 Bucket"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1.1 </b> "
---

Trong bước này, bạn sẽ tạo một **Amazon S3 bucket** để lưu trữ các gói triển khai và lưu trữ website tĩnh của bạn. Bucket này sau đó sẽ được các hàm Lambda sử dụng để tải lên các file triển khai, và frontend sẽ dùng để phục vụ nội dung đã triển khai.

---

#### Tạo S3 bucket

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)

2. Nhấn **Create bucket**

   ![Create Bucket](/images/2.preparation/001-createbucket.png)

3. Cấu hình bucket:

   - **Tên bucket**: `awsdeplybucket12345`  
     *(Đảm bảo tên này là duy nhất trên toàn cầu)*
   - **Khu vực (Region)**: Chọn cùng khu vực với nơi các hàm Lambda của bạn chạy (ví dụ: `Asia Pacific (Singapore) ap-southeast-1`)
   - Giữ các tùy chọn còn lại mặc định:
     - **Block all public access**: BẬT *(sẽ cấu hình truy cập công khai để hosting website ở bước sau)*
     - **Versioning**: TẮT

   ![Bucket Config](/images/2.preparation/002-createbucket.png)
   ![Turn off Block](/images/2.preparation/003-createbucket.png)

4. Kéo xuống dưới cùng và nhấn **Create bucket**

   Sau khi tạo, bucket sẽ xuất hiện trong danh sách bucket.

   ![Create Bucket](/images/2.preparation/004-createbucket.png)

---

#### Bật tính năng Hosting Website Tĩnh

1. Nhấn vào tên bucket vừa tạo trong S3 Console.

![Click on the newly created bucket name in the S3 Console](/images/2.preparation/005-createbucket.png)

2. Chuyển sang tab **Properties**.

![Navigate to the Properties tab](/images/2.preparation/006-createbucket.png)

3. Kéo xuống phần **Static website hosting**.

![Scroll down to the Static website hosting](/images/2.preparation/007-createbucket.png)

4. Nhấn **Edit**, chọn:
   - **Hosting type**: `Host a static website`
   - **Index document**: `index.html`
   - *(Tùy chọn)* **Error document**: `error.html`

![Setup Static website hosting](/images/2.preparation/008-createbucket.png)

5. Nhấn **Save changes**.

![Click Save changes](/images/2.preparation/009-createbucket.png)

> **Lưu ý**: Bạn sẽ cần cấu hình bucket policy để cho phép truy cập công khai đọc file ở bước triển khai sau.

---

#### Cấu hình Bucket Policy

Để cho phép truy cập công khai phục vụ website tĩnh, bạn cần cấu hình **bucket policy** như sau:

1. Trong S3 Console, chọn bucket của bạn, sau đó vào tab **Permissions**.

![](/images/2.preparation/010-createbucket.png)  
![](/images/2.preparation/011-createbucket.png)

2. Kéo xuống mục **Bucket policy**, nhấn **Edit**.

![](/images/2.preparation/012-createbucket.png)

3. Dán đoạn policy sau vào trình chỉnh sửa, thay thế tên bucket nếu cần:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::awsdeplybucket12345/*"
       }
     ]
   }
   ```

![](/images/2.preparation/013-createbucket.png)

4. Nhấn Save changes.

![](/images/2.preparation/014-createbucket.png)

Chính sách này cho phép truy cập công khai để đọc tất cả các đối tượng trong bucket. Hãy chắc chắn điều này phù hợp với mục đích của bạn (ví dụ: hosting file website công khai).

---

#### Bước tiếp theo
Tiếp tục sang [Tạo bảng DynamoDB](../2.1.2-createdynamodb/)