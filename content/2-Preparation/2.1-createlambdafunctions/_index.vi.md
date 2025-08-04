---
title: "Chuẩn bị Lambda và DynamoDB"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

Trong bước này, chúng ta sẽ chuẩn bị các thành phần **serverless** cần thiết cho quy trình tự động triển khai, bao gồm:

- Một **S3 bucket** để lưu trữ mã nguồn từ GitHub  
- Một **bảng DynamoDB** để theo dõi trạng thái triển khai  
- Hai **hàm Lambda**: một dùng để tải mã nguồn lên S3 và một để triển khai  
- Các **IAM Role và quyền truy cập cần thiết**  
- Một **Git Layer** để Lambda có thể clone mã từ GitHub

Sau khi hoàn tất bước này, bạn sẽ có một quy trình làm việc serverless tự động hóa việc tải mã, kích hoạt sự kiện và triển khai ứng dụng.

---

### Tổng quan kiến trúc

Kiến trúc sau khi hoàn tất sẽ trông như sau:

![Serverless Architecture](/images/arc-lambda-dynamodb.png)

---

### Nội dung

- [Tạo S3 bucket và bảng DynamoDB](2.1.1-creates3dynamodb/)
- [Tạo hàm Lambda Upload](2.1.2-createlambdaupload/)
- [Thiết lập IAM Role cho Lambda Upload](2.1.3-rolelambdaupload/)
- [Thêm Git Layer cho Lambda Upload](2.1.4-gitlayerupload/)
- [Tạo hàm Lambda Deploy](2.1.5-createlambdadeploy/)
- [Thiết lập IAM Role cho Lambda Deploy](2.1.6-rolelambdadeploy/)