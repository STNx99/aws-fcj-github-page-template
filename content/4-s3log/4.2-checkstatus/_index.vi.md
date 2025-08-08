---
title: "Kiểm Tra Trạng Thái Triển Khai Qua API"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

Ở bước này, bạn sẽ kiểm tra trạng thái của một yêu cầu triển khai bằng cách gọi endpoint **/status** thông qua API Gateway. Endpoint này sẽ truy vấn trạng thái của bản triển khai được lưu trong bảng DynamoDB dựa trên giá trị `id`.

Hàm Lambda Upload sẽ tạo một mục (item) mới trong bảng DynamoDB với `id` duy nhất cùng các thông tin liên quan (trạng thái, thời gian, v.v.).

---

#### Lấy Deployment ID

Trước khi kiểm tra trạng thái, bạn cần biết `id` của bản triển khai. Bạn có thể tìm thấy `id` thông qua một trong các cách sau:

- Trong log của hàm Lambda Upload trên [CloudWatch](https://console.aws.amazon.com/cloudwatch/)
- Là một phần trong nội dung phản hồi khi API upload được gọi
- Trực tiếp trong bảng DynamoDB có tên `DeploymentStatus`

Ví dụ khi bạn gửi yêu cầu đến endpoint `/deploy` trong POSTMAN với nội dung:

POST https://j5eeru81c3.execute-api.ap-southeast-1.amazonaws.com/deploy

```json
{
    "repoUrl": "https://github.com/TanPhat23/staticwebsite"
}
```

Nếu thành công, bạn sẽ nhận được phản hồi như ví dụ dưới đây:

![](/images/4.test/001-checkstatus.png)


Trong bước tiếp theo, hãy thay thế `your-deployment-id` bằng giá trị thực tế của trường `id` được trả về.  
Ví dụ:

your-deployment-id = 35403e3b-3e97-4d67-9fc7-08de9e75ce30

#### Gọi Endpoint `/status`

Sau khi bạn có `deployment id`, hãy gọi endpoint của API Gateway để kiểm tra trạng thái triển khai.

**Ví dụ gửi yêu cầu bằng `POSTMAN`:**

---

1. Lấy endpoint mặc định của bạn**

![](/images/4.test/002-checkstatus.png)  
![](/images/4.test/003-checkstatus.png)

---

2. Lấy `id` từ phương thức `/status`**

![](/images/4.test/004-checkstatus.png)

---

3. Kiểm tra **trạng thái triển khai** bằng POSTMAN**

GET "https://your-api-id.execute-api.ap-southeast-1.amazonaws.com/status?id=your-deployment-id"

Ví dụ: "https://j5eeru81c3.execute-api.ap-southeast-1.amazonaws.com/status?id=35403e3b-3e97-4d67-9fc7-08de9e75ce30"

![](/images/4.test/005-checkstatus.png)

---

#### Ví dụ phản hồi

Phản hồi thành công có thể giống như sau:

```json
{
  "status": "deployed"
}
```
Trường `status` (trạng thái) có thể là một trong các giá trị sau:

- `uploaded`: Mã nguồn đã được tải lên thành công  
- `deployed`: Đã triển khai thành công

Bạn có thể làm mới (gửi lại) yêu cầu để kiểm tra trạng thái cập nhật sau khi hàm Lambda Deploy hoàn tất quá trình thực thi.

---

Tiếp tục bước tiếp theo để tìm hiểu cách giám sát logs và sự kiện.

[Tiếp theo: Giám sát Logs và Events](../4.3-monitorlogs/)
