---
title: "Dọn Dẹp Tài Nguyên"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 6 </b> "
---

Trong bước cuối cùng này, bạn sẽ học cách dọn dẹp tất cả các tài nguyên AWS đã được tạo trong quá trình thực hành. Điều này giúp bạn tránh phát sinh chi phí không mong muốn và giữ cho môi trường AWS của bạn gọn gàng.

#### Tổng Quan Dọn Dẹp

Quy trình dọn dẹp bao gồm:

- Xóa tất cả các hàm Lambda đã tạo cho việc tải lên và triển khai.
- Gỡ bỏ S3 bucket và bảng DynamoDB dùng để lưu trữ tập tin triển khai và theo dõi trạng thái.
- Xóa EventBridge event bus và các quy tắc liên quan.
- Xóa API Gateway và tất cả tài nguyên liên quan.
- Xóa ứng dụng AWS Amplify nếu bạn đã sử dụng nó để triển khai giao diện frontend.

Hãy chắc chắn làm theo từng bước một cách cẩn thận để không để sót lại tài nguyên không sử dụng.

Sau khi hoàn tất các bước triển khai và tích hợp, việc dọn dẹp tài nguyên AWS là điều cần thiết để tránh chi phí dư thừa và giữ cho môi trường làm việc sạch sẽ.

---

#### Mục Lục  
[6.1 Xóa các hàm Lambda](6.1-deletelambdafunctions/)  
[6.2 Xóa S3 Bucket và Bảng DynamoDB](6.2-deletes3dynamodb/)  
[6.3 Xóa EventBridge và Quy tắc liên quan](6.3-deleteeventbridge/)  
[6.4 Xóa API Gateway và tài nguyên liên quan](6.4-deleteapigateway/)  
[6.5 Xóa Ứng dụng AWS Amplify (nếu có)](6.5-deleteamplify/)