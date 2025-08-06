---
title: "Tạo GitHub OAuth, kiểm tra trên local và tạo một dự án GitHub"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.1 </b> "
---

Trong bước này, bạn sẽ học cách tạo một ứng dụng OAuth trên GitHub, kiểm tra luồng xác thực trên máy cục bộ, và thiết lập một dự án GitHub mới. Quá trình này rất quan trọng để kích hoạt xác thực an toàn và tích hợp ứng dụng của bạn với các dịch vụ GitHub, hỗ trợ cho việc triển khai và cộng tác sau này.

---

#### Thiết lập OAuth trên GitHub và tạo dự án mới

1. Truy cập [github](github.com)

2. Vào phần cài đặt (Settings)
   ![Github settings](/images/5.github/001-github.png)

3. Vào phần Developer settings
   ![Dev settings] (/images/5.github/002-github.png)

4. Nhấn vào OAuth Apps và chọn New OAuth App
   ![New OAuth Apps] (/images/5.github/003-github.png)

5. Thiết lập OAuth:

   - Nhập tên ứng dụng (ví dụ: webdeploy)
   - Homepage URL: http://localhost:3000
   - Authorization callback URL: http://localhost:3000/api/auth/callback/github
   - Nhấn Register application
     ![Creating a Auth] (/images/5.github/004-github.png)

6. Tạo client secret

   - Nhấn Generate a new client secret
   - Sao chép client secret và lưu trữ ở nơi an toàn
     ![Generate Client Secret] (/images/5.github/005-github.png)

7. Truy cập repository đã clone từ `https://github.com/TanPhat23/awscode`:
   - Nếu bạn chưa clone repository, hãy chạy:
     ```bash
     git clone
     ```
   - Vào thư mục `webdeploy` và tạo file `.env`.
   - Mở file `.env` ở thư mục gốc của dự án.
   - Thêm các dòng sau vào file `.env`:
     ```plaintext
     NEXTAUTH_SECRET=
     NEXTAUTH_URL=http://localhost:3000
     GITHUB_CLIENT_ID= your_client_id
     GITHUB_CLIENT_SECRET= your_client_secret
     NEXT_PUBLIC_AWS_API_GATEWAY= your_aws_api_gateway
     NEXT_PUBLIC_AWS_BUCKET_URL= your_aws_bucket_url/dist
     ```
   - Thay `your_client_id` và `your_client_secret` bằng giá trị bạn đã lấy từ GitHub.
   - Với `NEXTAUTH_SECRET`, bạn có thể tạo một chuỗi ngẫu nhiên hoặc sử dụng công cụ quản lý secret an toàn.
   - Lưu file `.env`.
8. Khởi động server phát triển:

   - Mở terminal và chuyển đến thư mục `webdeploy`.
   - Đảm bảo bạn đã cài đặt Node.js và npm, nếu chưa hãy truy cập [NodeJS](https://nodejs.org/en) để cài đặt.
   - Chạy lệnh sau để khởi động server phát triển:
     ```bash
     npm run dev
     ```
   - Ứng dụng Next.js sẽ chạy tại `http://localhost:3000`.

9. Kiểm tra luồng xác thực:
   - Mở trình duyệt và truy cập `http://localhost:3000`.
   - Nhấn nút "Sign in with GitHub".
   - Bạn sẽ được chuyển hướng đến GitHub để xác thực.
   - Sau khi xác thực thành công, bạn sẽ được chuyển về ứng dụng.
   - Nhấn để hiển thị tất cả repository của bạn.
   - Bạn sẽ thấy danh sách repository GitHub hiển thị trong ứng dụng.
     ![List repository](/images/5.github/006-github.png)

#### Tạo dự án React để triển khai lên GitHub

1. Truy cập một thư mục trống trên máy tính nơi bạn muốn tạo dự án GitHub.
2. Mở terminal tại thư mục đó và chạy các lệnh sau:

   ```bash
   npm create vite@latest my-react-app
   ```

   - Lệnh này sẽ yêu cầu bạn chọn framework. Chọn `React` và tiếp tục chọn `JavaScript` hoặc `TypeScript` tùy ý.
   - Sau khi tạo xong dự án, chuyển vào thư mục dự án:

   ```bash
   cd my-react-app
   npm install
   npm run dev
   ```

   - Lệnh trên sẽ tạo dự án React sử dụng Vite, cài đặt các phụ thuộc cần thiết và khởi động server phát triển.

3. Tạo file cấu hình vite ở thư mục gốc dự án:

   - Tạo file tên `vite.config.js` ở thư mục gốc dự án.
   - Thêm nội dung sau vào file `vite.config.js`:

     ```javascript
     import { defineConfig } from "vite";
     import react from "@vitejs/plugin-react";

     // https://vitejs.dev/config/
     export default defineConfig({
       plugins: [react()],
       base: process.env.VITE_BASE_PATH || "./",
     });
     ```

   - Cài đặt package dotenv để quản lý biến môi trường:

   ```bash
   npm install dotenv
   ```

   - Cấu hình này giúp Vite sử dụng React và chỉ định base path cho ứng dụng.

4. Tạo dự án GitHub:

   - Truy cập [github](https://github.com) và tạo repository mới.
   - Đặt tên repository (ví dụ: staticwebsite).
   - Khởi tạo repository với file README.
   - Nhấn "Create repository".
     ![Create staticwebsite](/images/5.github/007-github.png)
   - Sau khi tạo repository, vào thư mục dự án và chạy các lệnh sau để đẩy dự án lên GitHub:

     ```bash
     git init
     git add .
     git commit -m "first commit"
     git branch -M main
     git remote add origin `Your repository URL`
     git push -u origin main
     ```

   - Thay `Your repository URL` bằng URL repository bạn vừa tạo.

5. Kiểm tra tính năng triển khai:

   - Vào dự án NextJS trong thư mục `webdeploy` và chạy dự án
   - Sau khi dự án chạy, mở trình duyệt và truy cập `http://localhost:3000`.
   - Chọn repository `staticwebsite` bạn vừa tạo.
   - Nhấn nút `Upload` (Đảm bảo bạn đã cấu hình CORS trong API Gateway để thao tác này hoạt động).

   ![Deploying a static website](/images/5.github/008-github.png)

6. Sau khi upload hoàn tất, bạn có thể xem website tĩnh của mình bằng cách nhấn vào liên kết được cung cấp trong ứng dụng.
   ![Deployment](/images/5.github/009-github.png)
