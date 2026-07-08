---
title: "Bản đề xuất"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# LunaGenZ - Serverless Numerology Web Application
## Hệ thống Ứng dụng Thần Số Học tự động hoá trên nền tảng AWS Serverless

### 1. Tổng quan dự án (Overview)
LunaGenZ là nền tảng ứng dụng Thần Số Học (Numerology) được xây dựng dành cho giới trẻ, cho phép người dùng tra cứu các chỉ số cá nhân hóa dựa trên ngày sinh và họ tên. Hệ thống tự động tạo ra báo cáo chi tiết dưới dạng PDF và gửi trực tiếp qua email cho người dùng. 

Để đảm bảo tính linh hoạt, sự ổn định và tối ưu chi phí cho giai đoạn MVP (Minimum Viable Product), nền tảng áp dụng kiến trúc **100% AWS Serverless** và sử dụng công nghệ tạo PDF nội bộ mạnh mẽ thay vì phụ thuộc vào các dịch vụ Generative AI của bên thứ ba.

### 2. Vấn đề cần giải quyết & Giải pháp
#### Vấn đề hiện tại
Thị trường hiện nay có rất nhiều ứng dụng bói toán, thần số học, nhưng đa số yêu cầu người dùng trả phí ngay từ đầu hoặc thiết kế không thân thiện với tập khách hàng trẻ (Gen Z). Ban đầu, nhóm dự định sử dụng Generative AI (như Amazon Bedrock) để tạo ra các báo cáo cá nhân hóa. Tuy nhiên, việc tích hợp LLM (Large Language Models) tiềm ẩn rủi ro về mặt chi phí không thể kiểm soát đối với một dự án MVP và làm tăng độ trễ (latency) khi sinh báo cáo.

#### Giải pháp kỹ thuật (Fallback Strategy)
LunaGenZ quyết định chuyển hướng (Pivot) sang xây dựng một hệ thống tạo báo cáo nội bộ (Internal PDF Generation) vững chắc. Giải pháp này sử dụng kiến trúc Event-Driven hoàn toàn Serverless:
- **Frontend (Next.js)** được hosting hoàn toàn trên AWS Amplify.
- **Amazon API Gateway** và **AWS Lambda (Node.js)** xử lý logic tính toán thần số học và khởi tạo PDF.
- **Amazon DynamoDB** lưu trữ thông tin request và metadata.
- **Amazon S3** lưu trữ các file báo cáo PDF sau khi được tạo.
- **Amazon SES** gửi email tự động đính kèm báo cáo tới hòm thư người dùng.

### 3. Lợi ích và Hoàn vốn đầu tư
Chiến lược sử dụng trình tạo PDF nội bộ mang lại một hệ thống có tính ổn định cực cao (chi phí bằng $0 cho việc call API AI bên thứ ba), thời gian phản hồi nhanh và kiểm soát được 100% định dạng báo cáo đầu ra. Kiến trúc Serverless giúp hệ thống chịu tải tốt, tự động scale khi có lượng lớn người dùng tra cứu cùng lúc (ví dụ khi có trend trên TikTok), đồng thời giúp hạ tầng có chi phí ban đầu gần như bằng $0 nhờ tận dụng tốt Free Tier.

### 4. Kiến trúc giải pháp

#### Các Dịch vụ AWS sử dụng
- **AWS Amplify:** Hosting cho ứng dụng web Next.js với tính năng CI/CD tự động, giúp deploy nhanh chóng các phiên bản Frontend mới.
- **Amazon API Gateway:** Đóng vai trò là cửa ngõ tiếp nhận HTTP requests từ Frontend.
- **AWS Lambda:** Chạy các hàm xử lý logic (Node.js) tính toán các con số thần số học, render ra file PDF và kích hoạt luồng gửi mail.
- **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL tốc độ cao, lưu trữ lịch sử tra cứu của khách hàng.
- **Amazon S3:** Object Storage lý tưởng để lưu trữ an toàn các file báo cáo PDF tĩnh sau khi xuất.
- **Amazon SES (Simple Email Service):** Dịch vụ gửi thư điện tử tự động, đính kèm file báo cáo PDF về cho khách hàng nhanh chóng.

#### Luồng hoạt động (Workflow)
1. Khách hàng nhập **Họ tên** và **Ngày sinh** trên giao diện Next.js.
2. Frontend gọi API đẩy dữ liệu qua **Amazon API Gateway**.
3. **AWS Lambda Function** tiếp nhận request, tính toán các chỉ số cá nhân, gọi thư viện tạo PDF để render báo cáo.
4. Payload của request được ghi nhận lại trong **Amazon DynamoDB**.
5. File PDF sau khi tạo thành công được đẩy trực tiếp lên **Amazon S3 Bucket**.
6. Lambda gọi **Amazon SES** để lên lịch và gửi email chứa báo cáo cho người dùng.

### 5. Ước tính ngân sách & Chi phí
Vì hệ thống được cấu trúc 100% dựa trên Serverless, ngân sách duy trì hàng tháng trong năm đầu (giai đoạn MVP) là cực kì thấp nhờ tận dụng AWS Free Tier:
- **AWS Lambda:** Tối đa 1 triệu requests/tháng ($0)
- **Amazon API Gateway:** 1 triệu REST API calls/tháng ($0)
- **Amazon DynamoDB:** 25GB lưu trữ, 25 WCU/RCU ($0)
- **Amazon S3:** 5GB Standard storage ($0)
- **Amazon SES:** 62.000 emails/tháng (nếu request từ EC2/Lambda) ($0)
- **AWS Amplify:** 1000 build minutes/tháng, 5GB storage ($0)

**Tổng chi phí ước tính:** ~$0/tháng trong giai đoạn đầu tiên (giai đoạn chứng minh năng lực MVP).

### 6. Đánh giá rủi ro
- **Rủi ro 1:** Tín nhiệm gửi email của Amazon SES ở chế độ Sandbox bị giới hạn.
  - *Giải pháp:* Gửi yêu cầu lên bộ phận AWS Support để xin thoát khỏi chế độ Sandbox, xác thực Domain trước khi chính thức Launch hệ thống ra công chúng.
- **Rủi ro 2:** Vấn đề "Cold Start" của AWS Lambda khi không có người dùng thời gian dài, làm chậm tốc độ xuất PDF.
  - *Giải pháp:* Tối ưu hóa code Node.js, sử dụng các thư viện tạo PDF dung lượng nhẹ và set Provisioned Concurrency nếu cần thiết ở giai đoạn scale.