---
title: "Thiết kế kiến trúc"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Sơ đồ kiến trúc

![Architecture Diagram](/images/5-Workshop/5.4-S3-onprem/InterfaceEndpointArchitecture.png)

Đây là sơ đồ kiến trúc mà mình cùng các bạn trong nhóm đã triển khai cho dự án LunaGenZ.

### 2. Các dịch vụ AWS cốt lõi
Hệ thống này sử dụng một kiến trúc 100% Serverless rất thân thiện cho người mới bắt đầu:
- **AWS Amplify:** Hosting để chạy giao diện người dùng tĩnh (Frontend Next.js/React).
- **Amazon API Gateway (HTTP API):** Cổng kết nối siêu tốc và chi phí thấp để định tuyến request.
- **AWS Lambda:** Môi trường thực thi code backend (Node.js) làm nhiệm vụ gọi API AI, tính toán số học và tạo file PDF.
- **Amazon DynamoDB:** Bảng cơ sở dữ liệu phi quan hệ (NoSQL) dùng để lưu thông tin người dùng (`UsersTable`, `NumerologyTable`, `LenormandTable`).
- **Amazon S3:** Bucket để lưu trữ các tệp tin PDF kết quả (`PdfBucket`).

### 3. Tại sao chọn cấu trúc này cho bài Lab?
- **Triển khai cực nhanh:** Thay vì click chuột thủ công từng dịch vụ trên AWS Console, file `serverless.yml` sẽ định nghĩa và tự động hóa toàn bộ việc tạo Lambda, quyền IAM, bảng DynamoDB và S3 Bucket.
- **Không sợ quên xóa tài nguyên:** Người mới học AWS rất hay quên xóa các dịch vụ dẫn đến bị trừ tiền oan. Với Serverless Framework, mọi thứ được quản lý chung qua CloudFormation, chỉ cần lệnh `remove` là tự dọn sạch sẽ 100%.
- **Chi phí bằng 0:** Tất cả dịch vụ trong lab đều hỗ trợ mức Free Tier dồi dào. Nếu không có lượng truy cập lớn, bạn sẽ không mất một đồng phí nào.
