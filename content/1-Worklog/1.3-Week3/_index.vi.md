---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---



### Mục tiêu tuần 3:
* **Kiến thức:** Hiểu rõ cơ chế phân giải tên miền lai Hybrid DNS, tính năng VPC Peering kết nối mạng nội bộ song phương, kiến trúc Transit Gateway quản lý mạng tập trung và giải pháp sao lưu tự động AWS Backup.
* **Kỹ năng:** Biết cách cấu hình tự động hóa hạ tầng bằng mã lệnh thông qua mẫu thiết kế CloudFormation Template.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Thiết lập kiến trúc Hybrid DNS sử dụng dịch vụ Route 53 Resolver <br> - Khởi tạo Key Pair bảo mật và viết cấu trúc hạ tầng dạng mã với CloudFormation Template | 01/05/2026 | 02/05/2026 | AWS Documentation |
| 3 | - Định cấu hình nhóm tường lửa Security Group để kiểm soát luồng dữ liệu <br> - Thiết lập kết nối đầu cuối đến máy chủ nhảy RDGW (Remote Desktop Gateway) | 03/05/2026 | 03/05/2026 | AWS Documentation |
| 4 | - Triển khai dịch vụ thư mục Microsoft Active Directory (Microsoft AD) trên nền mây và thiết lập các bản ghi phân giải hệ thống DNS nội bộ | 04/05/2026 | 04/05/2026 | AWS Documentation |
| 5 | - Nghiên cứu điều kiện tiên quyết và thiết lập kết nối vùng mạng thông suốt qua **VPC Peering** <br> - Định cấu hình bảng định tuyến Route Table, dải bảo mật kiểm soát mạng Network ACL và bộ định tuyến ảo để tối ưu hóa liên kết | 05/05/2026 | 06/05/2026 | AWS Documentation |
| 6 | - Triển khai mô hình kết nối lưới nâng cao thông qua bộ định tuyến trung tâm **AWS Transit Gateway** <br> - Tạo mối gắn kết tài nguyên mạng Transit Gateway Attachments và thiết lập phân phối luồng đi nội bộ <br> - Xây dựng chiến lược sao lưu dữ liệu tập trung tự động bằng **AWS Backup**, cấu hình lưu trữ vòng đời trên S3 Bucket, kiểm tra và chạy thử nghiệm quy trình khôi phục sự cố | 07/05/2026 | 07/05/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:
* Triển khai thành công giải pháp Hybrid DNS tích hợp Route 53 Resolver, thiết lập kết nối xác thực Active Directory đồng bộ hóa hạ tầng.
* Làm chủ công cụ hạ tầng dạng mã (IaC) **AWS CloudFormation**, tự động hóa cấu hình tường lửa Security Group và khởi tạo hạ tầng qua template nhanh chóng.
* Thiết lập thông suốt mạng nội bộ thông qua VPC Peering và mở rộng mạng phân tán quy mô lớn bằng Transit Gateway.
* Hoàn thiện quy trình sao lưu an toàn toàn diện với AWS Backup trên bộ lưu trữ S3, kiểm tra thành công khả năng khôi phục hệ thống.