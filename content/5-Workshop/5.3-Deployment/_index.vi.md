---
title: "Triển khai end-to-end"
date: 2026-04-18
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Hướng dẫn triển khai (Step-by-step)

Với việc sử dụng **Serverless Framework**, quy trình triển khai Backend phức tạp đã được thu gọn lại thành các thao tác cực kỳ đơn giản. Ai cũng có thể làm theo một cách dễ dàng.

#### Bước 1: Chuẩn bị Backend
1. Mở Terminal (Command Prompt/PowerShell), di chuyển vào thư mục backend của dự án:
   ```bash
   cd lunaclone/LunaGenZ/be
   ```
2. Cài đặt các thư viện cần thiết:
   ```bash
   npm install
   ```
3. Tạo file `.env` bằng cách copy từ file mẫu:
   ```bash
   cp .env.example .env
   ```
4. Mở file `.env` và điền các thông tin của riêng bạn (ví dụ: `SES_FROM_EMAIL`, khóa API AI `GEMINI_API_KEY`, v.v.).

#### Bước 2: Deploy lên AWS
Đảm bảo bạn đã cấu hình AWS CLI hợp lệ (`aws configure`), sau đó chạy lệnh thần thánh:
```bash
serverless deploy
```
- Công cụ sẽ tự động đóng gói mã nguồn, tạo CloudFormation Stack.
- Tự động tạo các bảng DynamoDB (`lunagenz-users`, `lunagenz-numerology`, `lunagenz-lenormand`).
- Tự tạo S3 Bucket.
- Triển khai các hàm Lambda và API Gateway tương ứng.
- *Kết quả trả về:* Ở cuối terminal, bạn sẽ thấy danh sách các **Endpoints (URL)**. Hãy copy URL đó lại.

#### Bước 3: Triển khai Frontend
1. Di chuyển sang thư mục frontend:
   ```bash
   cd ../fe
   ```
2. Mở file `.env` (nếu có) hoặc sửa trực tiếp trong code cấu hình để cập nhật **URL của API Gateway** vừa lấy ở Bước 2.
3. Đẩy (Push) code Frontend lên GitHub.
4. Truy cập **AWS Amplify** trên console, chọn **Host web app**, kết nối với kho lưu trữ GitHub của bạn.
5. Nhấn **Save and Deploy**. Hệ thống Amplify sẽ tự động build ứng dụng Next.js và cung cấp cho bạn một đường link website chạy thực tế.
