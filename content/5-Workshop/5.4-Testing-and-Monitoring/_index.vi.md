---
title: "Kiểm thử & Đo lường"
date: 2026-04-18
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. Kiểm thử tính năng (Testing)
Sau khi Backend và Frontend được deploy thành công:
1. Mở đường link website do AWS Amplify cung cấp.
2. Nhập một thông tin thử nghiệm (Họ tên, Ngày sinh) và chọn chức năng tạo báo cáo.
3. Chờ xử lý và kiểm tra hòm thư Email (hoặc thư mục rác/spam) xem đã nhận được file PDF báo cáo hay chưa.

### 2. Kiểm tra Logs hệ thống
Nếu có lỗi xảy ra, việc debug với Serverless Framework rất dễ dàng:
- **Xem log trực tiếp trên Terminal:** Bạn có thể kéo log trực tiếp từ AWS về máy cá nhân bằng lệnh:
  ```bash
  serverless logs -f numerology -t
  ```
  *(Thay `numerology` bằng tên function trong file `serverless.yml`)*
- **Xem qua CloudWatch:** Truy cập AWS Console > **CloudWatch** > **Log groups**. Bạn sẽ thấy các luồng log (Log streams) ghi lại chi tiết từng bước thực thi của hàm Lambda, thời gian phản hồi API AI, và trạng thái sinh PDF.

### 3. Đo lường cơ bản (Metric)
- Truy cập vào giao diện của **AWS Lambda**, chuyển sang tab **Monitor**.
- Tại đây, AWS cung cấp sẵn các biểu đồ giám sát cơ bản vô cùng trực quan:
  - **Invocations:** Số lần hàm được gọi.
  - **Duration:** Thời gian trung bình để xử lý 1 request.
  - **Error count:** Thống kê nếu code bị crash hoặc gặp lỗi kết nối API bên ngoài.
