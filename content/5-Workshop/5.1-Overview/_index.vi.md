---
title : "Tổng quan"
date : 2026-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về LunaGenZ

**LunaGenZ** là một ứng dụng Thần Số Học sáng tạo, được thiết kế để tính toán và tạo ra các báo cáo thần số học cá nhân chi tiết. Để đảm bảo tính sẵn sàng cao, khả năng mở rộng và tối ưu chi phí, toàn bộ ứng dụng được xây dựng trên kiến trúc Serverless của AWS.

#### Tổng quan Kiến trúc

Trong workshop này, bạn sẽ triển khai các thành phần sau:
1. **Frontend (Amazon S3 & CloudFront)**: Giao diện người dùng tĩnh (được xây dựng bằng HTML/CSS/JS hoặc Framework). Nó được lưu trữ trên S3 và phân phối toàn cầu qua CloudFront.
2. **Backend (Amazon API Gateway & AWS Lambda)**: Logic tính toán cốt lõi của thần số học được xử lý bởi các hàm AWS Lambda, được kích hoạt an toàn thông qua API Gateway.
3. **Tạo báo cáo PDF (AWS Lambda)**: Một hàm Serverless chuyên dụng tự động tổng hợp các kết quả tính toán thành một tệp báo cáo PDF có thể tải xuống.

#### Bạn sẽ xây dựng những gì?

Vào cuối workshop này, bạn sẽ có một ứng dụng Serverless hoàn chỉnh đang chạy trên AWS, với giao diện Frontend, logic Backend, và khả năng tự động tạo báo cáo PDF. Hãy cùng bắt đầu nhé!
