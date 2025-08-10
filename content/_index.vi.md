---
title : "Dewebdeploy: Triển khai và lưu trữ website tĩnh"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Làm việc với Amazon System Manager - Session Manager

#### Tổng quan
Trong bài thực hành này, bạn sẽ xây dựng một quy trình triển khai (deployment pipeline) nâng cao, hoàn toàn serverless và dựa trên kiến trúc sự kiện (event-driven) bằng cách sử dụng AWS Elastic Beanstalk cùng các dịch vụ hỗ trợ như S3, Lambda, API Gateway, EventBridge, Amplify và DynamoDB. Quy trình này sẽ tự động lấy mã nguồn từ GitHub, đóng gói và tải lên thông qua Lambda, kích hoạt triển khai bằng EventBridge, đồng thời theo dõi trạng thái triển khai trong DynamoDB và cung cấp thông tin này qua các endpoint của API Gateway.  
Bạn cũng sẽ cấu hình S3 để lưu trữ và phân phát website tĩnh, tích hợp giao diện frontend để tương tác với hệ thống triển khai, và áp dụng các vai trò IAM an toàn nhằm tuân thủ các nguyên tắc bảo mật tốt nhất. Ngoài ra, bạn sẽ sử dụng AWS Systems Manager – Session Manager để truy cập EC2 một cách an toàn, có thể kiểm soát và ghi nhật ký, mà không cần sử dụng Bastion host hoặc SSH.  
Sau khi hoàn thành bài thực hành, bạn sẽ có được trải nghiệm thực tế trong việc xây dựng một hệ thống triển khai sẵn sàng cho môi trường sản xuất, áp dụng các chiến lược nâng cao của Elastic Beanstalk theo một thiết kế hiện đại và hoàn toàn serverless.

![Kiến trúc](/images/1.intro/architecture.png)

### Nội dung
1. [Giới thiệu](1-Introduce/)
2. [Chuẩn bị](2-Preparation/)
3. [Tích hợp](3-Integration/)
4. [Quản lý nhật ký S3](4-s3log/)
5. [Triển khai lên AWS Amplify](5-deploytoamplify/)
6. [Dọn dẹp tài nguyên](6-cleanup/)