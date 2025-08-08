---
title: "Kiểm Tra Trạng Thái Triển Khai Qua API"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

Trong bước này, bạn sẽ kiểm tra trạng thái của một yêu cầu triển khai bằng cách gọi endpoint **/status** thông qua API Gateway. Endpoint này sẽ truy vấn trạng thái triển khai được lưu trong bảng DynamoDB dựa trên `id`.

Hàm Lambda Upload sẽ tạo một item mới trong bảng DynamoDB với một `id` duy nhất và các thông tin liên quan (trạng thái, thời gian, v.v.).

---
#### Lấy URL API Gateway
Để kiểm tra trạng thái triển khai, bạn cần có URL của API Gateway. URL này thường có dạng: `https://your-api-id.execute-api.region.amazonaws.com/`

Khi đã có `id` của deployment, bạn sẽ gọi endpoint của API Gateway để kiểm tra trạng thái.


1. Lấy **endpoint mặc định** của bạn

![](/images/4.test/002-checkstatus.png)
![](/images/4.test/003-checkstatus.png)

#### Lấy Deployment ID

Trước khi kiểm tra trạng thái, bạn cần biết `id` của deployment. Bạn có thể tìm thấy nó bằng một trong các cách sau:

- Trong log của hàm Lambda Upload trên [CloudWatch](https://console.aws.amazon.com/cloudwatch/)
- Là một phần của response body khi gọi API upload
- Trong bảng DynamoDB `DeploymentStatus`

Khi gọi endpoint `/deploy` trong POSTMAN với:

POST `https://your-api-id.execute-api.ap-southeast-1.amazonaws.com/deploy`

```json
{
    "repoUrl": "https://github.com/TanPhat23/staticwebsite"
}
```
 
Nếu thành công, bạn sẽ nhận được phản hồi tương tự ví dụ dưới đây:

![](/images/4.test/001-checkstatus.png)


Ở bước tiếp theo, hãy thay `your-deployment-id` bằng giá trị thực tế của trường `id` trả về, ví dụ:

your-deployment-id = 35403e3b-3e97-4d67-9fc7-08de9e75ce30

#### Gọi Endpoint /status

1. Lấy id từ phản hồi của endpoint `/deploy` ở trên hoặc từ bảng DynamoDB.

2. Kiểm tra **trạng thái triển khai** với **POSTMAN**

GET "https://your-api-id.execute-api.ap-southeast-1.amazonaws.com/status?id=your-deployment-id"

Ví dụ: "https://j5eeru81c3.execute-api.ap-southeast-1.amazonaws.com/status?id=35403e3b-3e97-4d67-9fc7-08de9e75ce30"

![](/images/4.test/005-checkstatus.png)

---

#### Ví Dụ Phản Hồi

Một phản hồi thành công có thể như sau:

```json
{
  "status": "deployed"
}
```

Trường `status` có thể nhận một trong các giá trị sau:

- `uploaded`: Đã upload mã nguồn thành công
- `deployed`: Đã triển khai thành công

Bạn có thể làm mới (refresh) request để lấy trạng thái mới nhất sau khi hàm Lambda Deploy hoàn thành.

---

Tiếp tục bước tiếp theo để tìm hiểu cách giám sát log và sự kiện.

[Tiếp theo: Giám sát Log và Sự kiện](../4.3-monitorlogs/)