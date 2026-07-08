---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Tự động hóa triển khai Oracle Database@AWS bằng Terraform

Việc triển khai các hệ thống cơ sở dữ liệu Oracle trên nền tảng đám mây luôn là bài toán đòi hỏi sự cân bằng giữa hiệu năng, khả năng mở rộng và tính nhất quán trong quản lý hạ tầng. Với Oracle Database@AWS (ODB@AWS), Oracle đã mang nền tảng Exadata – hệ thống phần cứng được tối ưu dành riêng cho Oracle Database – vào trực tiếp trung tâm dữ liệu của AWS, cho phép doanh nghiệp khai thác hiệu năng cao của Oracle đồng thời tận dụng hệ sinh thái dịch vụ phong phú của AWS.

Tuy nhiên, để xây dựng hoàn chỉnh một môi trường Oracle Database@AWS, người quản trị phải thực hiện nhiều bước cấu hình như thiết lập ODB Network, triển khai Exadata Infrastructure, tạo VM Cluster và kết nối với Amazon VPC. Nếu thực hiện hoàn toàn trên AWS Console, quy trình này khá phức tạp, mất nhiều thời gian và dễ xảy ra sai sót khi số lượng môi trường triển khai tăng lên.

Trong bài viết này, chúng ta sẽ tìm hiểu cách sử dụng Terraform để tự động hóa toàn bộ quá trình triển khai Oracle Database@AWS. Thông qua mô hình Infrastructure as Code (IaC), doanh nghiệp có thể chuẩn hóa hạ tầng, giảm thiểu lỗi cấu hình và triển khai hệ thống một cách nhanh chóng, nhất quán.

---

## Hướng dẫn kiến trúc

Oracle Database@AWS được thiết kế để kết hợp hiệu năng của Oracle Exadata với khả năng mở rộng và tính linh hoạt của AWS. Thay vì vận hành Oracle Database trên hạ tầng riêng biệt, doanh nghiệp có thể triển khai trực tiếp trên cơ sở hạ tầng AWS nhưng vẫn sử dụng các tính năng tối ưu của Exadata.

Trong mô hình này, Terraform đóng vai trò là công cụ điều phối toàn bộ quá trình tạo tài nguyên. Các thành phần hạ tầng được mô tả bằng mã nguồn HCL và được Terraform tự động triển khai theo đúng thứ tự phụ thuộc, giúp đảm bảo tính nhất quán giữa các môi trường.

Giải pháp bao gồm bốn thành phần chính:

- ODB Network: Mạng chuyên dụng kết nối giữa AWS và Oracle Cloud Infrastructure (OCI), cung cấp đường truyền riêng có độ trễ thấp.
- Oracle Exadata Infrastructure: Hạ tầng phần cứng Exadata được triển khai trực tiếp trong Availability Zone của AWS để cung cấp khả năng xử lý dữ liệu hiệu năng cao.
- Exadata VM Cluster: Cụm máy ảo chạy Oracle Grid Infrastructure và Oracle Database.
- ODB Peering Connection: Kết nối mạng riêng giữa Amazon VPC và ODB Network, cho phép các ứng dụng trên AWS truy cập Oracle Database một cách an toàn.


> *Hình 1. Kiến trúc tổng thể; những ô màu thể hiện những dịch vụ riêng biệt.*

Sau khi các thành phần trên được tạo thành công, doanh nghiệp có thể triển khai Oracle Database với đầy đủ khả năng mở rộng, tính sẵn sàng cao và khả năng tích hợp với các dịch vụ AWS.

---

## Vì sao nên sử dụng Terraform?

Terraform là một trong những công cụ Infrastructure as Code phổ biến nhất hiện nay. Thay vì thao tác trực tiếp trên giao diện quản trị AWS, toàn bộ hạ tầng được mô tả dưới dạng mã nguồn HCL (HashiCorp Configuration Language). Terraform sẽ đọc các tệp cấu hình này và tự động tạo tài nguyên theo đúng trình tự phụ thuộc.

Việc áp dụng Terraform mang lại nhiều lợi ích:

- Tự động hóa hoàn toàn quá trình triển khai hạ tầng.
- Loại bỏ các thao tác cấu hình thủ công trên AWS Console.
- Đảm bảo cấu hình đồng nhất giữa các môi trường Development, Testing và Production.
- Dễ dàng quản lý thay đổi thông qua Git.
- Có thể tái sử dụng cấu hình cho nhiều dự án khác nhau.
- Hỗ trợ mở rộng và cập nhật hạ tầng mà không ảnh hưởng đến các tài nguyên hiện có.

Đối với các tổ chức triển khai nhiều hệ thống Oracle Database hoặc áp dụng DevOps, Terraform giúp giảm đáng kể thời gian triển khai và tăng khả năng kiểm soát hạ tầng.

---

## Điều kiện trước khi triển khai

Trước khi chạy Terraform, cần đảm bảo đã hoàn tất các bước chuẩn bị sau:

### 1 Đăng ký Oracle Database@AWS

Doanh nghiệp cần đăng ký dịch vụ Oracle Database@AWS thông qua AWS Marketplace và hoàn tất quy trình Onboarding với Oracle.

### 2 Liên kết tài khoản

AWS Account phải được liên kết với Oracle Cloud Infrastructure (OCI Tenancy) để Terraform có quyền quản lý tài nguyên trên cả hai nền tảng.

  1. Cấu hình Terraform Provider

Terraform cần cấu hình đồng thời hai Provider:
- AWS Provider
- OCI Provider

Hai Provider này cho phép Terraform giao tiếp với API của AWS và Oracle Cloud.

### 3 Thiết lập quyền IAM

Tài khoản sử dụng Terraform cần có đầy đủ quyền tạo, cập nhật và xóa tài nguyên trên AWS cũng như Oracle Cloud.

Sau khi hoàn tất các điều kiện trên, người quản trị có thể bắt đầu triển khai hạ tầng Oracle Database@AWS bằng Terraform.

---

## Quy trình triển khai bằng Terraform

Terraform sẽ tạo các thành phần của Oracle Database@AWS theo đúng trình tự phụ thuộc. Mỗi thành phần được định nghĩa dưới dạng một Resource trong Terraform.

### Bước 1. Khởi tạo ODB Network

### 

Bước đầu tiên là tạo Oracle Database Network, đóng vai trò thiết lập kết nối mạng riêng giữa AWS và Oracle Cloud Infrastructure.

Ví dụ cấu hình Terraform:


resource "aws_odb_network" "example" {
  display_name         = "odb-my-net"
  availability_zone_id = "use1-az6"
  client_subnet_cidr   = "10.2.0.0/24"
  backup_subnet_cidr   = "10.2.1.0/24"
  s3_access            = "DISABLED"
  zero_etl_access      = "DISABLED"
  tags = {
    "env" = "dev"
  }
}

