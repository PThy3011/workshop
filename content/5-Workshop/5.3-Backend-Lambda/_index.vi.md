---
title : "Backend (Lambda)"
date : 2026-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Triển khai Backend Thần Số Học

Chức năng cốt lõi của LunaGenZ là tính toán các chỉ số thần số học (VD: Con số chủ đạo, Con số sứ mệnh, Con số linh hồn) dựa trên đầu vào của người dùng (Họ tên và Ngày sinh).

Để triển khai Backend Serverless này:

1. **Tạo AWS Lambda Function**:
   - Truy cập AWS Management Console và mở dịch vụ Lambda.
   - Chọn **Create function**, chọn "Author from scratch".
   - Đặt tên hàm là `LunaGenZ-Calculation`.
   - Chọn môi trường chạy phù hợp (VD: Node.js 20.x hoặc Python 3.12).

2. **Tải mã nguồn lên**:
   - Nén code logic tính toán của bạn thành file `.zip`.
   - Tải file nén này lên hàm Lambda.

3. **Cấu hình API Gateway**:
   - Để Frontend có thể gọi hàm Lambda, bạn cần thiết lập API Gateway.
   - Tạo một REST API hoặc HTTP API mới.
   - Thêm phương thức POST và liên kết nó với hàm Lambda `LunaGenZ-Calculation`.
   - Kích hoạt **CORS** để Frontend có thể gửi yêu cầu đến API này mà không bị lỗi cross-origin.
   - Triển khai (Deploy) API vào một stage (VD: `prod`) và lưu lại đường dẫn **Invoke URL**.
