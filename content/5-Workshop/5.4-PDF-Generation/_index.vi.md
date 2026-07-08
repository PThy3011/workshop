---
title : "Tạo báo cáo PDF"
date : 2026-01-01 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Tự động hóa báo cáo PDF

Sau khi các tính toán thần số học hoàn tất, ứng dụng cần tạo ra một báo cáo PDF đẹp mắt để người dùng có thể tải về.

1. **Tạo Lambda sinh PDF**:
   - Tạo một hàm Lambda thứ hai có tên `LunaGenZ-PDFGenerator`.
   - Hàm này sẽ nhận kết quả JSON từ hàm tính toán, định dạng nó vào một template HTML và chuyển đổi thành tài liệu PDF bằng các thư viện như `Puppeteer` (cho Node.js) hoặc `pdfkit`.

2. **Cấp quyền (Permissions)**:
   - Đảm bảo hàm Lambda này có quyền ghi (write) file vào một **Amazon S3 bucket** (VD: `lunagenz-reports-bucket`).
   - Tạo một IAM Policy cho phép `s3:PutObject` vào bucket này và gắn nó vào Execution Role của hàm Lambda.

3. **Trả về đường dẫn tải xuống**:
   - Sau khi file PDF được tạo và lưu trữ trên S3, hàm sẽ tạo một **Pre-signed URL**.
   - Trả Pre-signed URL này về cho Frontend thông qua API Gateway, cho phép người dùng tải xuống báo cáo thần số học cá nhân của họ một cách an toàn.
