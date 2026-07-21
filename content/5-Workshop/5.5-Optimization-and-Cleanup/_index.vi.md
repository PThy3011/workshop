---
title: "Tối ưu & Cleanup"
date: 2026-04-18
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### 1. Tối ưu quá trình thực hành
Thay vì cấu hình bằng tay hàng tá dịch vụ gây tốn thời gian và dễ sai sót, **Serverless Framework** đã tối ưu toàn bộ vòng đời ứng dụng.
- **Quản lý biến môi trường:** Các giá trị như Tên Bucket (`PDF_BUCKET_NAME`), khóa API được tham chiếu động từ file `.env` thẳng vào Lambda một cách an toàn mà không cần nhập tay trên Console.
- **Phân quyền IAM tự động:** Khối lệnh `iam.role.statements` trong file `serverless.yml` giúp tự động sinh ra các Rule bảo mật chặt chẽ nhất (nguyên tắc đặc quyền tối thiểu) mà người thực hành không cần có kiến thức sâu về IAM.

### 2. Dọn dẹp hệ thống (Clean-up)
Một trong những ác mộng lớn nhất khi thực hành Cloud là quên tắt dịch vụ dẫn đến mất tiền. Bài Lab này giúp bạn dọn dẹp (clean-up) vô cùng dễ dàng và an toàn tuyệt đối.

1. **Dọn dẹp Backend (Cực kỳ quan trọng):**
   - Mở Terminal tại thư mục `lunaclone/LunaGenZ/be`.
   - Trước tiên, hãy đảm bảo **S3 Bucket** của bạn đã được làm trống (Empty). Trình xóa của CloudFormation sẽ không cho phép xóa bucket nếu bên trong vẫn còn file. Hãy lên AWS Console > S3 > Chọn Bucket báo cáo > Nhấn **Empty**.
   - Sau khi làm trống S3, chạy lệnh sau ở Terminal:
     ```bash
     serverless remove
     ```
   - Chờ một vài phút. Công cụ này sẽ tự động lên AWS và **xóa sạch sẽ mọi thứ** nó đã tạo ra: Các hàm Lambda, API Gateway, các bảng DynamoDB, và cả S3 Bucket. Không để lại bất kì "rác" tài nguyên nào.
   
2. **Dọn dẹp Frontend:**
   - Truy cập **AWS Amplify**.
   - Chọn ứng dụng bạn vừa triển khai, chuyển sang tab `App settings` > `General` và nhấn **Delete app**.

Chỉ với 2 bước đơn giản, tài khoản của bạn đã được dọn sạch hoàn toàn về nguyên trạng ban đầu, loại bỏ rủi ro phát sinh chi phí ngoài ý muốn!
