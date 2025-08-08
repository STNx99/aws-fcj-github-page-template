---
title: "Kiểm tra kết nối API Gateway với Lambda"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3 </b> "
---

Trong bước này, bạn sẽ xác minh rằng API Gateway đã được tích hợp đúng với các hàm Lambda. Bạn sẽ kiểm tra cả hai endpoint (`/deploy` và `/status`) để đảm bảo các yêu cầu từ client được định tuyến và xử lý chính xác.

---

#### 1. Kiểm tra endpoint `/status`

##### Mục đích:
Đảm bảo Lambda `upload-function` phản hồi đúng với các yêu cầu HTTP gửi đến.

##### Cách kiểm tra:
- Tìm **API Gateway endpoint** trong AWS Management Console:
  - Vào **API Gateway** > **HTTP APIs**
  - Chọn API của bạn và tìm **default endpoint** URL (ví dụ: `https://<api-id>.execute-api.<region>.amazonaws.com`)
  ![API endpoints](/images/3.integration/010-connecteventbridge.png)
- Sử dụng **Postman**, **curl**, hoặc frontend của bạn
- Gửi yêu cầu `GET` đến API Gateway:

```bash
curl -X GET https://<api-id>.execute-api.<region>.amazonaws.com/status
```
Kết quả mong đợi (Lambda mặc định):
Bạn sẽ nhận được phản hồi 200 OK với JSON tương tự:
```json
{
  "message": "Hello from Lambda"
}
```
---
#### 2. Kiểm tra endpoint `/deploy`
##### Mục đích:
Kích hoạt upload-function qua POST /deploy và xác nhận Lambda thực hiện các bước sau:
- Clone repository GitHub
- Nén file (zip)
- Upload lên S3 bucket
- Gửi sự kiện đến EventBridge

##### Cách kiểm tra:
```bash
curl -X POST https://<api-id>.execute-api.<region>.amazonaws.com/deploy \
-H "Content-Type: application/json" \
-d '{}'
```
Kết quả mong đợi (Lambda mặc định):
Bạn sẽ nhận được phản hồi 200 OK với nội dung như:
```json
{
  "message": "Hello from Lambda"
}
```
Xác minh trên CloudWatch:
Trong AWS CloudWatch console:
- Vào Logs
- Mở log group của upload-function
- Kiểm tra log có các dòng:
    - Đã clone repository GitHub
    - Đã nén file và upload lên S3
    - Đã gửi sự kiện EventBridge
Bạn cũng có thể kiểm tra log group của deploy-function để xác nhận nó đã được kích hoạt sau khi nhận sự kiện.

---

#### 3. Kiểm tra từ frontend (Tùy chọn)
Nếu bạn phát triển frontend (ví dụ: http://localhost:3000), có thể kiểm tra tích hợp bằng JavaScript:

```js
fetch("https://<api-id>.execute-api.<region>.amazonaws.com/prod/deploy", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({})
})
.then(res => res.json())
.then(console.log)
.catch(console.error);
```
Đảm bảo API Gateway đã cấu hình CORS cho phép truy cập từ http://localhost:3000.

---

#### Kết quả cuối cùng
Sau khi hoàn thành bước này, bạn cần xác nhận:
- Endpoint /status và /deploy truy cập được qua API Gateway
- upload-function xử lý yêu cầu đúng
- EventBridge kích hoạt deploy-function thành công
- Log CloudWatch xác nhận chuỗi hành động trên

Bạn đã sẵn sàng chuyển sang Chương 4: Chạy thử pipeline triển khai.