---
title: "Kiểm tra kết nối API Gateway với Lambda"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3 </b> "
---

### 🎯 Mục tiêu

Sau khi thiết lập API Gateway với các endpoint `/deploy` và `/status`, bước này sẽ giúp bạn kiểm tra xem các kết nối từ client (Postman, curl, hoặc frontend) đến Lambda đã hoạt động chính xác chưa.

---

### 1. Kiểm tra endpoint `/status`

#### Mục đích:
Xác nhận rằng Lambda `upload-function` đang hoạt động và có thể phản hồi yêu cầu HTTP.

#### Cách kiểm tra:

- Mở **Postman** hoặc sử dụng **curl**
- Gửi yêu cầu `GET` đến endpoint:

```bash
curl -X GET https://<api-id>.execute-api.<region>.amazonaws.com/prod/status
```
Kỳ vọng: Trả về mã 200 OK cùng với phản hồi dạng JSON (ví dụ: { "status": "ready" } hoặc tương tự)

2. Kiểm tra endpoint /deploy
Mục đích:
Kích hoạt Lambda upload-function thông qua endpoint POST /deploy để kiểm tra luồng upload + gửi sự kiện EventBridge.

Cách kiểm tra:
Sử dụng Postman hoặc curl để gửi POST request:

curl -X POST https://<api-id>.execute-api.<region>.amazonaws.com/prod/deploy \
-H "Content-Type: application/json" \
-d '{}'

 Kỳ vọng:

Nhận phản hồi 200 OK

Trong CloudWatch logs, bạn sẽ thấy log clone repo, zip và upload vào S3

Nếu thành công, EventBridge sẽ tự động gọi deploy-function

3. Kiểm tra trong CloudWatch
Để xác minh hoạt động thực tế:

Vào CloudWatch Logs

Xem log của Lambda upload-function

Kiểm tra xem có log thông báo như:

“Cloning repository…”

“Uploading to S3…”

“Publishing Event…”

Tùy chọn: Kiểm tra từ frontend
Nếu bạn có frontend chạy local (VD: localhost:3000), thử gọi 2 API trên bằng JS/axios hoặc fetch để xác nhận CORS đã hoạt động đúng.

Kết quả mong đợi
Cả hai endpoint /deploy và /status hoạt động đúng

Lambda nhận và xử lý yêu cầu thành công

EventBridge nhận sự kiện từ upload và kích hoạt deploy Lambda

Bạn đã hoàn tất bước tích hợp – hệ thống serverless CI/CD đã sẵn sàng chạy thử nghiệm thực tế 🎉

Tiếp theo: Chạy thử quy trình deploy
