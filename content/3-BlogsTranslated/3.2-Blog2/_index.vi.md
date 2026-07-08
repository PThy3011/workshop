---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

{}

# Provision Oracle Database@AWS resources using Terraform

**Terraform** cho phép bạn tự động hóa việc provision các tài nguyên Oracle Database@AWS một cách nhất quán, repeatable và có thể kiểm soát phiên bản. Bài viết này hướng dẫn cách sử dụng Terraform để triển khai các thành phần chính của Oracle Database@AWS bao gồm ODB network, Oracle Exadata infrastructure, Exadata VM clusters và Autonomous VM clusters.

Bài đăng blog này tập trung vào việc áp dụng Infrastructure as Code (IaC) cho Oracle Database@AWS. Bạn có thể truy cập các code samples và Terraform templates tại [GitHub repository](https://github.com/aws-samples/sample-odb-launch-using-terraform) để tham khảo.

---

## Giới thiệu về Oracle Database@AWS

[Oracle Database@AWS](https://docs.aws.amazon.com/odb/latest/UserGuide/what-is-odb.html) (ODB@AWS) mang đến hạ tầng Oracle Exadata được quản lý bởi Oracle Cloud Infrastructure (OCI) ngay trong data center của AWS. Giải pháp này giúp doanh nghiệp di chuyển cơ sở dữ liệu Oracle lên AWS trong khi vẫn tận dụng hiệu suất cao, khả năng mở rộng và các tính năng tiên tiến của Exadata.

Oracle Database@AWS tích hợp sâu với các dịch vụ AWS bản xứ như Amazon S3, zero-ETL pipelines và AWS KMS. Các database Oracle có thể chạy song song với ứng dụng trên Amazon EC2, ECS, EKS và nhiều dịch vụ khác.

Hiện tại, Oracle Database@AWS hỗ trợ hai dịch vụ chính:
- Oracle Autonomous AI Database on Dedicated Exadata Infrastructure (ADB-D)
- Oracle Exadata Database Service on Dedicated Infrastructure (ExaDB-D)

---

## Hướng dẫn kiến trúc

**Terraform** là công cụ Infrastructure as Code mạnh mẽ cho phép định nghĩa hạ tầng dưới dạng file cấu hình dễ đọc, có thể version và chia sẻ. Việc sử dụng Terraform giúp chuẩn hóa quy trình provision, giảm lỗi thủ công và tăng tốc độ triển khai môi trường mới.

**Các bước provision chính trong Oracle Database@AWS:**

1. Tạo **ODB Network**
2. Tạo **Oracle Exadata Infrastructure**
3. Tạo **Exadata VM Cluster** hoặc **Autonomous VM Cluster**
4. Tạo **ODB Peering Connection**

> *Hình 1. Kiến trúc tổng thể Oracle Database@AWS với Terraform.*

---

## Prerequisites

Trước khi bắt đầu, hãy đảm bảo bạn đã chuẩn bị:

- Hiểu biết cơ bản về **Terraform**
- Đã hoàn tất **onboarding** Oracle Database@AWS (chấp nhận Private Offer qua AWS Marketplace và liên kết tài khoản AWS với OCI tenancy)
- IAM principal có quyền cần thiết để provision Oracle Database@AWS resources
- Đã cài đặt Terraform CLI

---

## Lựa chọn công nghệ và Terraform resources

| Tài nguyên                          | Terraform Resource                                      | Mô tả |
|-------------------------------------|---------------------------------------------------------|-------|
| ODB Network                        | `aws_odb_network`                                       | Mạng riêng cho Exadata và Autonomous VM clusters |
| Exadata Infrastructure             | `aws_odb_cloud_exadata_infrastructure`                  | Hạ tầng phần cứng Exadata |
| Exadata VM Cluster                 | `aws_odb_cloud_vm_cluster`                              | Cluster cho Exadata Database Service |
| Autonomous VM Cluster              | `aws_odb_cloud_autonomous_vm_cluster`                   | Cluster cho Autonomous Database |
| ODB Peering Connection             | `aws_odb_network_peering_connection`                    | Kết nối riêng tư giữa VPC và ODB Network |

---

## Core Terraform configurations

### 1. Tạo ODB Network

```hcl
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
...
```
--- 

### 2. Tạo Oracle Exadata Infrastructure

```hc2
resource "aws_odb_cloud_exadata_infrastructure" "example" {
  display_name         = "my-exa-infra"
  availability_zone    = "use1-az6"
  shape                = "exadata.oci.x11m"
  database_server_type = "X11M"
  storage_server_type  = "X11M-HC"
  maintenance_window {
    custom_action_timeout_in_mins = 16
    days_of_week = [{ name = "MONDAY" }, { name = "TUESDAY" }]
    hours_of_day = [11, 16]
    is_custom_action_timeout_enabled = true
    lead_time_in_weeks = 3
    months = [{ name = "FEBRUARY" }, { name = "MAY" }, { name = "AUGUST" }, { name = "NOVEMBER" }]
    patching_mode = "ROLLING"
    preference = "CUSTOM_PREFERENCE"
    weeks_of_month = [2, 4]
  }
  tags = {
    "env" = "dev"
  }
}
...
```
