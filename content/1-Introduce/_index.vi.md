---
title: "Dewebdeploy: Triển khai và lưu trữ trang web tĩnh"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

Hướng dẫn này sẽ đưa bạn từng bước xây dựng một **pipeline triển khai nâng cao** sử dụng **AWS Elastic Beanstalk**, kết hợp với các dịch vụ hỗ trợ như **S3**, **Lambda**, **API Gateway**, **EventBridge**, **Amplify** và **DynamoDB**. Mục tiêu là mô phỏng một quy trình triển khai hoàn toàn serverless và dựa trên sự kiện, nơi các gói triển khai được tải lên và tự động triển khai, đồng thời trạng thái triển khai được theo dõi và truy xuất thông qua API.

Khác với quy trình triển khai Elastic Beanstalk cơ bản chỉ dựa vào việc tải tệp ZIP qua console hoặc CLI, hướng dẫn này cung cấp các khả năng nâng cao:

- Tự động lấy mã nguồn từ GitHub
- Tải lên và đóng gói thông qua Lambda
- Triển khai dựa trên sự kiện thông qua EventBridge
- Theo dõi trạng thái triển khai với DynamoDB
- Tích hợp frontend thông qua API Gateway (HTTP API)

Để hỗ trợ quản lý hạ tầng an toàn, chúng ta cũng sử dụng **Session Manager** — một tính năng của AWS Systems Manager — để truy cập instance một cách bảo mật và có kiểm soát **mà không cần dùng đến Bastion hosts hay SSH**. Điều này giúp đảm bảo các phương pháp bảo mật tốt nhất, đặc biệt trong các môi trường vẫn còn sử dụng EC2 hoặc yêu cầu can thiệp thủ công.

#### Các Tính Năng Chính của Kiến Trúc Này
  ![Architecture](/images/1.intro/architecture.png)
- **Luồng triển khai hoàn toàn tự động** dựa trên kiến trúc sự kiện (event-driven)
- **Các hàm Lambda tách biệt theo chức năng**, xử lý logic tải lên và triển khai
- **Các endpoint API Gateway** để gọi triển khai và kiểm tra trạng thái
- **Hosting website tĩnh trên S3** để phục vụ giao diện frontend
- **Theo dõi metadata triển khai bằng DynamoDB**
- **Quyền IAM được phân quyền chặt chẽ và an toàn**
- **Tích hợp frontend** để người dùng tương tác với hệ thống triển khai

Kết thúc hướng dẫn này, bạn sẽ có một hệ thống triển khai hoạt động hoàn chỉnh, phản ánh các mẫu triển khai nâng cao trong **Elastic Beanstalk**, được chuyển thể thành một thiết kế hiện đại, serverless, phù hợp cho cả môi trường sản xuất và thử nghiệm.

---