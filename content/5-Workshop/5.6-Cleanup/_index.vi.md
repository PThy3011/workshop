---
title : "Dọn dẹp"
date : 2026-01-01 
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Dọn dẹp tài nguyên

Để tránh phát sinh các khoản phí không mong muốn trên tài khoản AWS của bạn, việc xóa các tài nguyên đã tạo trong workshop này là rất quan trọng.

1. **Xóa S3 Buckets**:
   - Làm trống (Empty) và xóa bucket `lunagenz-reports-bucket`.
   - Làm trống (Empty) và xóa bucket `lunagenz-frontend-web`.
2. **Xóa CloudFront Distribution**:
   - Trước tiên hãy Vô hiệu hóa (Disable) CloudFront distribution (quá trình này có thể mất vài phút).
   - Sau khi đã Disabled, hãy chọn nó và nhấn Delete.
3. **Xóa API Gateway**:
   - Truy cập giao diện API Gateway.
   - Chọn LunaGenZ API của bạn và nhấn Delete.
4. **Xóa Lambda Functions**:
   - Xóa các hàm `LunaGenZ-Calculation` và `LunaGenZ-PDFGenerator`.
5. **Xóa IAM Roles và Policies**:
   - Truy cập giao diện IAM và xóa bất kỳ Roles hay Policies tùy chỉnh nào đã được tạo riêng cho workshop này.