---
title: "Triển khai dự án lên Amplify"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.2 </b> "
---

Trong bước này, bạn sẽ học cách triển khai dự án của mình lên AWS Amplify. Quá trình này sẽ giúp bạn lưu trữ ứng dụng và làm cho nó có thể truy cập được trên Internet.

### Chuẩn bị trước khi triển khai

1. Triển khai lên GitHub:

- Truy cập repository đã clone từ `https://github.com/TanPhat23/awscode`
- Tìm thư mục `webdeploy`
- Mở terminal tại thư mục `webdeploy`
- Tạo repository mới trên GitHub:
  - Truy cập [GitHub](https://github.com)
  - Nhấn vào biểu tượng "+" ở góc phải trên cùng và chọn "New repository"
  - Đặt tên repository (ví dụ: `dewebdeploy`)
  - Chọn chế độ public hoặc private tùy ý
  - Nhấn "Create repository"
- Chạy các lệnh sau trong thư mục chứa `webdeploy`:
  ```bash
  git init
  git add .
  git commit -m "Initial commit"
  git branch -M main
  git remote add origin `Your repository URL`
  git push -u origin main
  ```

2. Triển khai lên Amplify:

- Truy cập [AWS Amplify Console](https://console.aws.amazon.com/amplify/home)
- Nhấn "Deploy an app"
  ![Deploy an app](/images/5.github/001-amplify.png)
- Chọn "GitHub" làm nguồn mã nguồn
- Nhấn "Next"
  ![Connect GitHub](/images/5.github/002-github.png)
- Ủy quyền cho AWS Amplify truy cập tài khoản GitHub của bạn
- Chọn repository bạn vừa tạo (ví dụ: `dewebdeploy`)
- Chọn nhánh muốn triển khai (thường là `main`)
- Nhấn "Next"
  ![Configure build settings](/images/5.github/003-amplify.png)
- Cấu hình biến môi trường:
  - Nhấn "Edit" trong phần Environment variables
  - Thêm các biến môi trường sau:
    - `NEXTAUTH_SECRET`
    - `NEXTAUTH_URL` = `a`
    - `GITHUB_CLIENT_ID`
    - `GITHUB_CLIENT_SECRET`
    - `NEXT_PUBLIC_AWS_API_GATEWAY`
    - `NEXT_PUBLIC_AWS_BUCKET_URL`
  - Thiết lập giá trị cho các biến này theo file `.env` của bạn
    ![Configure environment variables](/images/5.github/004-amplify.png)
- Nhấn "Next"
- Kiểm tra lại cấu hình và nhấn "Save and deploy"

3. Cấu hình build settings:

- Vào phần "Build settings" trong "Hosting"
  ![Configure build settings](/images/5.github/005-amplify.png)
- Nhấn "Edit" để chỉnh sửa build settings
  ![Edit build settings](/images/5.github/006-amplify.png)
- Thêm đoạn cấu hình build sau:
  ```yaml
  version: 1
  frontend:
    phases:
      preBuild:
        commands:
          - npm ci --cache .npm --prefer-offline
      build:
        commands:
          - echo "NEXTAUTH_SECRET=$NEXTAUTH_SECRET" >> .env
          - echo "GITHUB_CLIENT_ID=$GITHUB_CLIENT_ID" >> .env
          - echo "GITHUB_CLIENT_SECRET=$GITHUB_CLIENT_SECRET" >> .env
          - echo "NEXTAUTH_URL=$NEXTAUTH_URL" >> .env
          - echo "NEXT_PUBLIC_AWS_API_GATEWAY=$NEXT_PUBLIC_AWS_API_GATEWAY" >> .env
          - echo "NEXT_PUBLIC_AWS_BUCKET_URL=$NEXT_PUBLIC_AWS_BUCKET_URL" >> .env
          - npm run build
    artifacts:
      baseDirectory: .next
      files:
        - '**/*'
    cache:
      paths:
        - .next/cache/**/*
        - .npm/**/*
  ```
- Nhấn "Save" để lưu thay đổi
  ![Configure build settings](/images/5.github/007-amplify.png)

4. Cập nhật biến môi trường trong Amplify Console:
- Vào phần "Environment variables" trong "Hosting"
- Nhấn "Edit" để chỉnh sửa biến môi trường
- Cập nhật giá trị cho biến sau:
  - `NEXTAUTH_URL` = `https://your-amplify-app-id.amplifyapp.com`
- Cập nhật Github OAuth:
  - Vào phần cài đặt OAuth App trên GitHub
  - Cập nhật "Homepage URL" thành `https://your-amplify-app-id.amplifyapp.com`
  - Cập nhật "Authorization callback URL" thành `https://your-amplify-app-id.amplifyapp.com/api/auth/callback/github`
  - Nhấn "Update application"
- Sau khi cập nhật biến môi trường và build settings, quay lại Amplify Console
- Nhấn "Redeploy this version" để áp dụng thay đổi
  ![Redeploy this version](/images/5.github/008-amplify.png)

5. Thêm domain vào chính sách CORS của API Gateway:
- Truy cập [API Gateway Console](https://console.aws.amazon.com/apigateway/home)
- Chọn API của bạn (ví dụ: `DeployAPI`)
- Vào phần "CORS"
- Thêm domain sau vào danh sách allowed origins:
  - `https://your-amplify-app-id.amplifyapp.com`
- Lưu thay đổi
![Add domain to API Gateway CORS Policy](/images/5.github/009-amplify.png)

6. Kiểm tra ứng dụng:
- Mở trình duyệt và truy cập đường dẫn Amplify app của bạn (ví dụ: `https://your-amplify-app-id.amplifyapp.com`)
- Nhấn nút "Sign in with GitHub"
- Bạn sẽ được chuyển hướng đến GitHub để xác thực
- Sau khi xác thực thành công, bạn sẽ được chuyển về ứng dụng
- Bây giờ bạn đã có thể truy cập ứng dụng được lưu trữ trên AWS Amplify

### Kết luận
Chúc mừng! Bạn đã triển khai thành công ứng dụng Next.js của mình lên AWS Amplify. Ứng dụng của bạn đã trực tuyến và có thể truy cập từ Internet. Bạn có thể tiếp tục phát triển và đẩy các thay đổi lên repository GitHub, Amplify sẽ tự động triển khai các thay đổi đó cho bạn.