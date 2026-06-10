---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
{}


### Mục tiêu tuần 2:

* **Về mặt kiến thức (Knowledge Objectives):**
  * Hiểu rõ cơ chế phân quyền, quản lý danh tính và các phương thức bảo mật tài khoản nâng cao thông qua dịch vụ **AWS IAM**.
  * Nắm vững các cấp độ hỗ trợ kỹ thuật và thời gian phản hồi (SLA) của các gói **AWS Support**.
  * Làm chủ kiến trúc mạng đám mây **VPC (Virtual Private Cloud)**, bao gồm cách phân chia hệ thống mạng con (Subnet), định tuyến dữ liệu và thiết lập các lớp tường lửa bảo mật.
  * Hiểu sâu về cách thức vận hành, các loại cấu hình máy chủ ảo **Amazon EC2** và cơ chế lưu trữ đi kèm của ổ đĩa **Amazon EBS**.

* **Về mặt kỹ năng thực hành (Practical Skills):**
  * Triển khai thành thạo các chính sách phân quyền (IAM Policies) cho nhóm người dùng và thực hành kỹ thuật chuyển đổi vai trò (Assume Role) an toàn.
  * Khởi tạo máy chủ ảo EC2, cấu hình địa chỉ IP tĩnh (Elastic IP) và thực hiện kết nối SSH bảo mật từ máy tính cá nhân.
  * Thiết lập và cấu hình hạ tầng mạng nâng cao: kết nối mạng riêng tư an toàn qua **NAT Gateway**, thiết lập kênh truyền mã hóa **Site-to-Site VPN** và kết nối trực tiếp vào phân vùng mạng kín thông qua **EC2 Instance Connect Endpoint**.

### Các công việc cần triển khai trong tuần này:

#### TUẦN 2 (Từ 24/04/2026 – 30/04/2026)

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu về **AWS Support**: Các gói hỗ trợ từ thấp đến cao theo từng mục đích sử dụng <br> - Nghiên cứu các loại yêu cầu được phép hỗ trợ, cơ chế thay đổi gói và thời gian phản hồi của AWS | 24/04/2026 | 24/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Kiểm soát chi tiết quyền truy cập tài nguyên thông qua **AWS IAM** <br> - Nghiên cứu khái niệm: Users, Groups, Policies, Roles <br> - **Thực hành:** Triển khai bảo mật, tạo IAM Groups, áp dụng IAM Policies để phân quyền và quản lý IAM Users theo nhóm, cấu hình chuyển đổi IAM Role | 25/04/2026 | 26/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Nghiên cứu thiết kế và triển khai hệ thống mạng **VPC (Virtual Private Cloud)** theo tiêu chuẩn mô hình *AWS Well-Architected Framework* <br> - Cấu hình các thành phần bảo mật mạng, thiết lập kết nối an toàn giữa môi trường tại chỗ (on-premise) và đám mây AWS | 27/04/2026 | 27/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Tìm hiểu dịch vụ điện toán đám mây **Amazon EC2**: Khái niệm Instance types, AMI, EBS volume <br> - **Thực hành:** Khởi tạo máy chủ ảo EC2 Instance, gắn thêm ổ đĩa EBS volume và thực hiện kết nối SSH an toàn | 28/04/2026 | 29/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **Thực hành nâng cao hạ tầng mạng:** <br>&emsp; + Tạo và cấu hình NAT Gateway <br>&emsp; + Sử dụng EC2 Instance Endpoint để kết nối an toàn vào các máy chủ trong Private Subnet <br>&emsp; + Cấu hình kết nối Site-to-Site VPN và thiết lập tường lửa VPC <br> - Đánh giá, tổng kết tiến độ và hoàn thành báo cáo thực tập tuần 2 | 30/04/2026 | 30/04/2026 | <https://cloudjourney.awsstudygroup.com/> |

---

### Kết quả đạt được tuần 2:
* Phân biệt rõ ràng phạm vi hỗ trợ và thời gian phản hồi (SLA) của các gói AWS Support (Developer, Business, Enterprise).
* Thành thạo quản lý định danh với **AWS IAM**: Thiết lập phân quyền theo nguyên tắc đặc quyền tối thiểu (Least Privilege), tạo Group, phân Policy cho User và thực hành đóng vai (Assume Role).
* Hiểu sâu kiến trúc mạng **VPC**, phân biệt Public/Private Subnet và thiết lập luồng đi của dữ liệu qua Route Table và Internet Gateway.
* Khởi tạo, quản lý vòng đời của máy chủ ảo **Amazon EC2**, cấu hình dải IP tĩnh với Elastic IP và thực hiện kết nối bảo mật SSH qua Key Pair.
* Triển khai thành công hạ tầng kết nối an toàn nâng cao: Cấu hình hệ thống dịch thuật địa chỉ mạng qua NAT Gateway, thiết lập kênh truyền bảo mật mã hóa Site-to-Site VPN và kiểm soát luồng dữ liệu thông qua tường lửa Security Group và Network ACLs.