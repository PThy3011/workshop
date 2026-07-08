---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{}

# Xây dựng LunaGENZ – Hệ thống Thần Số Học cá nhân hóa trên kiến trúc Serverless AWS kết hợp Generative AI

Sau một thời gian học tập và thực hành, team chúng mình đã hoàn thành đồ án cuối khóa: **LunaGENZ** – một hệ thống sử dụng AI để luận giải Thần số học một cách cá nhân hóa và chuyên sâu.

Bài viết này không chỉ ghi lại hành trình phát triển mà còn chia sẻ những quyết định kiến trúc, thách thức đã gặp phải cùng cách giải quyết. Hy vọng những kinh nghiệm này sẽ hữu ích cho các bạn đang làm dự án Serverless hoặc tích hợp Generative AI.

---

## 1. Lý do chọn kiến trúc Serverless

Với một dự án sinh viên không có nguồn thu ổn định, mục tiêu quan trọng nhất là **giảm thiểu chi phí vận hành** và **không muốn quản lý server**. Vì vậy, team quyết định đi theo hướng Serverless hoàn toàn:

- **Frontend**: Next.js, triển khai qua **AWS Amplify**
- **Backend**: **API Gateway** + **AWS Lambda**
- **Database**: **Amazon DynamoDB** (On-demand mode)

Mô hình pay-as-you-go giúp chi phí hạ tầng gần như bằng không trong giai đoạn phát triển và test. Đây là lựa chọn phù hợp nhất với quy mô và ngân sách hiện tại của dự án.

---

## 2. Giải quyết vấn đề Timeout với Amazon SQS

Một trong những vấn đề lớn nhất lúc đầu là **timeout**. Vì quy trình bao gồm gọi AI sinh nội dung + xuất file PDF khá tốn thời gian, hệ thống thường xuyên gặp lỗi do API Gateway giới hạn **29 giây** cho một request.

**Giải pháp**: Áp dụng kiến trúc asynchronous processing.

- Khi người dùng gửi request → Lambda chỉ đẩy message vào **Amazon SQS** và trả về ngay phản hồi “Đang xử lý”.
- Một Lambda worker (trigger bởi SQS) sẽ lấy message ra, gọi Generative AI, sinh nội dung, tạo PDF và gửi kết quả qua **Amazon SES** đến email người dùng.

Nhờ đó, hệ thống không còn bị timeout, trải nghiệm người dùng tốt hơn và giảm nguy cơ mất dữ liệu khi có lỗi.

---

## 3. Lựa chọn mô hình AI

Team chọn **Claude 3 Haiku** qua **Amazon Bedrock** thay vì các model lớn hơn (như Claude 3 Opus hoặc Sonnet). Lý do:

- Bài toán luận giải Thần số học bằng tiếng Việt không đòi hỏi reasoning quá phức tạp.
- Model nhỏ cho tốc độ phản hồi nhanh hơn và chi phí thấp hơn đáng kể.
- Vẫn đảm bảo chất lượng đầu ra tốt với prompt được tối ưu.

---

## 4. Bảo mật, Tích hợp Thanh toán và CI/CD

- Tách biệt luồng **thanh toán** thành Webhook Handler riêng để tăng tính an toàn.
- Lưu trữ các secret (API keys, Bedrock credentials…) trong **AWS Secrets Manager**.
- Triển khai tự động toàn bộ frontend + backend qua **GitLab CI/CD**.
- Giám sát log, lỗi và performance thông qua **Amazon CloudWatch**.

---

## Những bài học rút ra

Đây là dự án đầu tiên team áp dụng Serverless ở quy mô khá đầy đủ, nên vẫn còn một số hạn chế:

- Xử lý lỗi retry khi Lambda worker fail chưa tối ưu.
- Chưa có cơ chế kiểm soát chi phí chặt chẽ khi traffic tăng cao.
- Cần cải thiện trải nghiệm người dùng khi xử lý asynchronous (ví dụ: thêm polling status hoặc WebSocket thông báo).

Tuy nhiên, qua dự án này, team đã học được rất nhiều về việc thiết kế hệ thống scalable, chi phí hiệu quả và cách tích hợp Generative AI một cách thực tế.

---

## Kết luận

**LunaGENZ** là minh chứng rằng với các dịch vụ Serverless của AWS (Amplify, Lambda, API Gateway, SQS, Bedrock, DynamoDB…), sinh viên và developer cá nhân hoàn toàn có thể xây dựng được những sản phẩm có tính thực tiễn cao mà không tốn quá nhiều chi phí ban đầu.

Chúng mình rất mong nhận được góp ý từ cộng đồng để tiếp tục cải tiến LunaGENZ trong thời gian tới.

Cảm ơn mọi người đã đọc bài viết!

---
