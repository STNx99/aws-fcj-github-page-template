---
title: "Tạo S3 Bucket"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1.1 </b> "
---

Trong bước này, bạn sẽ tạo một **Amazon S3 bucket** để lưu trữ các gói mã nguồn triển khai và host trang web tĩnh của bạn. Bucket này sẽ được sử dụng bởi các hàm Lambda để tải lên các tệp triển khai, và được frontend sử dụng để hiển thị nội dung đã triển khai.

---

#### Tạo S3 Bucket

1. Truy cập [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)

2. Nhấn **Create bucket**

   ![Create Bucket](/images/2.preparation/001-createbucket.png)

3. Cấu hình bucket:

   - **Bucket name**: `awsdeplybucket12345`  
     *(Đảm bảo tên là duy nhất trên toàn cầu)*
   - **Region**: Chọn khu vực giống với nơi bạn triển khai Lambda (ví dụ: `Asia Pacific (Singapore) ap-southeast-1`)
   - Giữ nguyên các thiết lập mặc định:
     - **Block all public access**: BẬT *(chúng ta sẽ bật quyền truy cập công khai sau để host website)*
     - **Versioning**: TẮT

   ![Bucket Config](/images/2.preparation/002-createbucket.png)
   ![Turn off Block](/images/2.preparation/003-createbucket.png)

4. Kéo xuống và nhấn **Create bucket**

   Sau khi tạo xong, bucket sẽ hiển thị trong danh sách.

   ![Create Bucket](/images/2.preparation/004-createbucket.png)

---

#### Bật Chức Năng Host Website Tĩnh

1. Nhấn vào tên bucket mới được tạo trong S3 Console.

![Chọn bucket mới tạo](/images/2.preparation/005-createbucket.png)

2. Chuyển sang tab **Properties**.

![Tab Properties](/images/2.preparation/006-createbucket.png)

3. Kéo xuống phần **Static website hosting**.

![Static website hosting](/images/2.preparation/007-createbucket.png)

4. Nhấn **Edit**, sau đó chọn:
   - **Hosting type**: `Host a static website`
   - **Index document**: `index.html`
   - *(Tuỳ chọn)* **Error document**: `error.html`

![Cấu hình Static hosting](/images/2.preparation/008-createbucket.png)

5. Nhấn **Save changes**.

![Save changes](/images/2.preparation/009-createbucket.png)

> **Lưu ý**: Bạn cần cấu hình chính sách bucket để cho phép truy cập công khai ở bước triển khai sau.

---

#### Thiết Lập Chính Sách Bucket

Để cho phép truy cập công khai phục vụ trang web tĩnh, bạn cần cấu hình **bucket policy**:

1. Trong S3 Console, chọn bucket của bạn, sau đó đi đến tab **Permissions**.

![](/images/2.preparation/010-createbucket.png)
![](/images/2.preparation/011-createbucket.png)

2. Kéo xuống phần **Bucket policy** và nhấn **Edit**.

![](/images/2.preparation/012-createbucket.png)

3. Dán đoạn policy sau vào ô chỉnh sửa, thay tên bucket nếu cần:

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

4. Nhấn **Save changes** để lưu thay đổi.

![](/images/2.preparation/014-createbucket.png)

Chính sách này cho phép mọi người có thể đọc công khai tất cả các tệp trong bucket của bạn. Hãy chắc chắn rằng điều này phù hợp với mục đích sử dụng của bạn (ví dụ: lưu trữ các tệp trang web công khai).

---

#### Bước tiếp theo

Tiếp tục đến [Tạo bảng DynamoDB](../2.1.2-createdynamodb/)