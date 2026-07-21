---
title: "Bản đề xuất"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# LunaGenZ - Serverless Numerology Web Application

### 1. Tổng quan dự án
LunaGenZ là nền tảng ứng dụng Thần Số Học và Lenormand (Numerology & Lenormand) được xây dựng dành cho giới trẻ, cho phép người dùng tra cứu các chỉ số cá nhân hóa dựa trên ngày sinh và họ tên, đồng thời cũng có thể xem cho bạn bè và người thân, hay thậm chí là người yêu, crush cũng được. Hệ thống tự động tạo ra báo cáo chi tiết dưới dạng PDF và gửi trực tiếp qua email cho người dùng.
Dự án được xây dựng trên kiến trúc **100% AWS Serverless** nhằm đảm bảo tính linh hoạt, khả năng mở rộng tự động và tối ưu chi phí.

### 2. Mục tiêu
- **Output mong muốn:** Một trang web hoàn chỉnh cho phép người dùng nhập thông tin, sau đó hệ thống tạo file PDF báo cáo thần số học và gửi qua email.
- **Tiêu chí đánh giá thành công:** Hệ thống hoạt động trơn tru end-to-end (từ frontend đến backend), tự động scale khi có lượng lớn người truy cập, và chi phí duy trì hàng tháng ở mức thấp nhất (tận dụng Free Tier).

### 3. Vấn đề cần giải quyết
Thị trường hiện nay có rất nhiều ứng dụng bói toán, thần số học, nhưng đa số yêu cầu trả phí ngay từ đầu hoặc thiết kế không thân thiện với tập khách hàng trẻ. Việc tích hợp Generative AI tiềm ẩn rủi ro về chi phí không thể kiểm soát đối với một dự án MVP và làm tăng độ trễ khi sinh báo cáo. LunaGenZ giải quyết bài toán này bằng cách dùng hệ thống tạo PDF nội bộ nhanh chóng, miễn phí và ổn định dựa trên Serverless.

### 4. Kiến trúc giải pháp
- **AWS Amplify:** Hosting cho ứng dụng web Next.js với tính năng CI/CD tự động.
- **Amazon API Gateway:** Đóng vai trò là cửa ngõ tiếp nhận HTTP requests từ Frontend.
- **AWS Lambda:** Chạy logic tính toán thần số học, render ra file PDF và kích hoạt gửi mail.
- **Amazon DynamoDB:** Lưu trữ lịch sử tra cứu của khách hàng.
- **Amazon S3:** Lưu trữ an toàn các file báo cáo PDF sau khi xuất.
- **Amazon SES:** Dịch vụ gửi email tự động đính kèm báo cáo.

### 5. Timeline
- **Tuần 1 - 5:** Tìm hiểu kiến trúc AWS, tham gia onboarding, thiết lập tài khoản, thực hành các dịch vụ cơ bản (VPC, EC2, IAM, S3).
- **Tuần 6 - 8:** Nghiên cứu nâng cao các dịch vụ CloudFront, RDS, AutoScaling và CloudWatch.
- **Tuần 9 - 10:** Bắt đầu phát triển dự án LunaGenZ, phân công công việc, viết code Frontend (Next.js) và Backend (Node.js).
- **Tuần 11:** Hoàn thiện tích hợp, test luồng end-to-end và chính thức deploy lên hạ tầng AWS.
- **Tuần 12:** Viết báo cáo thực tập, xây dựng tài liệu hướng dẫn (Workshop).

### 6. Ngân sách dự kiến (Giai đoạn MVP)

Hệ thống được thiết kế hoàn toàn theo kiến trúc **Serverless**, giúp tối ưu hóa triệt để chi phí cơ sở hạ tầng. Bằng việc không sử dụng các máy chủ chạy 24/7 (như EC2), dự án loại bỏ hoàn toàn chi phí nhàn rỗi. 

Trong giai đoạn MVP (Minimum Viable Product), toàn bộ luồng xử lý đều được thiết kế để nằm gọn trong giới hạn của gói **AWS Free Tier**. Dưới đây là bảng phân tích chi tiết mức sử dụng tài nguyên:

| Dịch vụ AWS | Vai trò trong kiến trúc | Giới hạn AWS Free Tier (Hàng tháng) | Chi phí dự kiến |
| :--- | :--- | :--- | :--- |
| **AWS Amplify** | Lưu trữ và tự động triển khai Frontend | 1.000 phút build, 5GB lưu trữ, 15GB băng thông | **$0** |
| **Amazon API Gateway** | Cổng định tuyến API (REST/HTTP API) | 1.000.000 lượt gọi (Requests) | **$0** |
| **AWS Lambda** | Môi trường tính toán (Logic & Report) | 1.000.000 request & 400.000 GB-giây tính toán | **$0** |
| **Amazon DynamoDB** | Cơ sở dữ liệu lưu lịch sử và IP người dùng | 25GB dung lượng, 25 WCU & 25 RCU | **$0** |
| **Amazon S3** | Lưu trữ tài liệu kết quả PDF/JSON | 5GB lưu trữ tiêu chuẩn, 20.000 GET requests | **$0** |
| **Amazon SES** | Hệ thống gửi Email thông báo tự động | 3.000 email (Gói miễn phí 12 tháng) | **$0** |

**Tổng chi phí ước tính: ~$0/tháng**

### 7. Rủi ro
- **Rủi ro 1:** Giới hạn gửi email của Amazon SES do tài khoản nằm trong chế độ Sandbox.
  - *Giải pháp:* Gửi yêu cầu (ticket) lên bộ phận AWS Support để xin thoát khỏi Sandbox, trong khi đó sử dụng Nodemailer của Google để dự phòng và đặt vòng try catch ở trong, khi nếu được duyệt SES rồi thì sử dụng không thì sử dụng Nodemailer làm dự phòng.
- **Rủi ro 2:** Vấn đề "Cold Start" của AWS Lambda khi hệ thống không có request trong thời gian dài.
  - *Giải pháp:* Tối ưu hóa code, sử dụng các thư viện tạo PDF dung lượng nhẹ để giảm thiểu thời gian init.
- **Rủi ro 3:** Vấn đề tài khoản chưa được cho phép hoặc viết ticket giúp đỡ nhưng chưa được duyệt sử dụng được dịch vụ AWS Bedrock.
  - *Giải pháp:* Sử dụng API AI bên ngoài thay cho AI trong thời gian chờ cấp phép dự phòng.
