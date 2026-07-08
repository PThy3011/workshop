---
title: "Worklog Tuần 6"
date: 2026-05-22
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:
* **Kiến thức:** Nắm vững các tiêu chuẩn bảo mật điện toán đám mây quốc tế bao gồm AWS Foundational Security Best Practices, bộ quy chuẩn trung tâm CIS AWS Foundations Benchmark và tiêu chuẩn bảo mật dữ liệu thẻ thanh toán PCI DSS.
* **Kỹ năng:** Thành thạo công cụ quản trị an ninh trung tâm AWS Security Hub, thiết lập hàm xử lý phi máy chủ AWS Lambda để tự động hóa tài nguyên và thiết lập ranh giới phân quyền nâng cao với IAM Permission Boundary.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Nghiên cứu tổng quan về trung tâm bảo mật tổng hợp **AWS Security Hub** và các bộ tiêu chuẩn kiểm tra an ninh hạ tầng tự động đám mây | 22/05/2026 | 22/05/2026 | <https://000018.awsstudygroup.com/vi/> |
| 3 | - Phân tích chi tiết quy chuẩn kiểm định an toàn thông tin AWS Foundational Security Best Practices và bộ tiêu chuẩn đánh giá lỗ hổng hệ thống CIS AWS Foundations Benchmark | 23/05/2026 | 24/05/2026 | <https://000018.awsstudygroup.com/vi/> |
| 4 | - Tìm hiểu tiêu chuẩn bảo mật thông tin bắt buộc dành cho ngành dữ liệu thẻ thanh toán tài chính PCI DSS và các bước kích hoạt quét kiểm tra hệ thống trên AWS Security Hub | 25/05/2026 | 25/05/2026 | <https://000018.awsstudygroup.com/vi/> |
| 5 | - Nghiên cứu cách viết mã nguồn kiểm soát với kiến trúc xử lý phi máy chủ **AWS Lambda** nhằm áp dụng vào việc quét dọn, quản lý và tối ưu chi phí hạ tầng máy chủ ảo AWS | 26/05/2026 | 26/05/2026 | <https://000022.awsstudygroup.com/vi/> |
| 6 | - Thực hành phân bổ nhãn quản lý tài nguyên thông qua Resource Groups và hệ thống Tags <br> - Thực hành cấu hình giới hạn quyền hạn nâng cao cho tài khoản IAM User bằng giải pháp **IAM Permission Boundary** <br> - Thiết lập cơ chế bảo mật mã hóa dữ liệu ở trạng thái lưu trữ tĩnh bằng dịch vụ quản lý khóa **AWS KMS** | 27/05/2026 | 28/05/2026 | <https://000027.awsstudygroup.com/vi/> <br> <https://000028.awsstudygroup.com/vi/> <br> <https://000030.awsstudygroup.com/vi/> <br> <https://000033.awsstudygroup.com/vi/> |

### Kết quả đạt được tuần 6:
* Kích hoạt và vận hành thành thạo bảng điều khiển AWS Security Hub, tuân thủ nghiêm ngặt các quy chuẩn bảo mật đám mây hàng đầu: CIS Benchmark, PCI DSS và AWS Best Practices.
* Làm chủ mô hình Serverless với dịch vụ AWS Lambda, viết code tự động hóa các thao tác quản lý vòng đời và kiểm soát thẻ định danh (Tagging) trên tài nguyên EC2.
* Nâng cao tính an toàn tài khoản bằng cách thiết lập tường lửa phân quyền IAM Permission Boundary và áp dụng thành công mã hóa dữ liệu lưu trữ (Data at rest) bằng các lớp khóa mật mã sinh ra từ dịch vụ AWS KMS.