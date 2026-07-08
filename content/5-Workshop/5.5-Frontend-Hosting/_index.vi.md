---
title : "Hosting Frontend"
date : 2026-01-01 
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Lưu trữ Frontend trên AWS

Để ứng dụng LunaGenZ có thể được truy cập từ khắp nơi trên thế giới với độ trễ thấp và tính sẵn sàng cao, chúng ta sẽ lưu trữ các file frontend tĩnh bằng Amazon S3 và phân phối thông qua Amazon CloudFront.

1. **Tạo S3 Bucket**:
   - Tạo một S3 bucket mới (VD: `lunagenz-frontend-web`).
   - Kích hoạt tính năng **Static website hosting** trong phần thuộc tính của bucket.
   - Tải lên các file HTML, CSS, và JS của bạn vào bucket này.

2. **Cấu hình Amazon CloudFront**:
   - Tạo một CloudFront distribution mới.
   - Đặt Origin Domain trỏ về website endpoint của S3 bucket.
   - Kích hoạt **Origin Access Control (OAC)** để chặn truy cập công khai trực tiếp vào S3 bucket, đảm bảo người dùng chỉ truy cập được trang web thông qua CloudFront.
   - Chờ quá trình deploy distribution hoàn tất.

3. **Kết nối Frontend với Backend**:
   - Đảm bảo mã JavaScript ở Frontend đã được cấu hình để gọi đến **Invoke URL** của API Gateway mà bạn đã tạo ở bước 5.3.
   - Sau khi deploy thành công, bạn có thể truy cập ứng dụng LunaGenZ của mình thông qua tên miền CloudFront (VD: `d123456abcdef8.cloudfront.net`).
