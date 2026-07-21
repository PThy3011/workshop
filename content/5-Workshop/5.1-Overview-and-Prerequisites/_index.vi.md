---
title: "Tổng quan và Điều kiện tiên quyết"
date: 2026-04-18
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### 1. Tổng quan (Overview)
Trong Workshop này, chúng ta sẽ thực hành triển khai một hệ thống Thần Số Học (Numerology) đơn giản mang tên **LunaGenZ** lên AWS.

Mục tiêu của bài thực hành này là giúp bạn làm quen với việc triển khai hạ tầng dưới dạng mã (Infrastructure as Code - IaC) bằng công cụ **Serverless Framework**. Nhờ công cụ này, việc tạo ra các tài nguyên phức tạp như Lambda, API Gateway, DynamoDB hay S3 trở nên cực kỳ đơn giản và tự động, đồng thời việc dọn dẹp (Clean-up) cũng chỉ tốn 1 dòng lệnh.

### 2. Điều kiện tiên quyết (Prerequisite)
Để bắt đầu, bạn cần chuẩn bị:
- **Tài khoản AWS:** Đã kích hoạt và thiết lập cấu hình với AWS CLI (chạy lệnh `aws configure`).
- **Môi trường phát triển:**
  - Cài đặt [Node.js](https://nodejs.org/en) (phiên bản 18 hoặc 20).
  - Cài đặt **Serverless Framework** bằng lệnh: `npm install -g serverless`
- **Mã nguồn (Source Code):**
  - Dự án mẫu `LunaGenZ` bao gồm thư mục backend (`be`) và frontend (`fe`).
