---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

{}

# Cara tiên phong AI chuyên ngành cho môi giới bảo hiểm doanh nghiệp với AWS

Ngành bảo hiểm là một thị trường toàn cầu trị giá 8 nghìn tỷ USD, đang phải đối mặt với gánh nặng từ quy trình thủ công và tình trạng thiếu hụt nhân tài nghiêm trọng. **Cara** – một giải pháp AI-native được xây dựng trên AWS – đang thay đổi cách các công ty môi giới bảo hiểm vận hành back-office bằng cách tự động hóa mạnh mẽ các quy trình phức tạp.

Bài viết này khám phá hành trình của Cara trong việc xây dựng một nền tảng AI chuyên sâu dành riêng cho lĩnh vực bảo hiểm, đồng thời phân tích kiến trúc kỹ thuật và giá trị kinh doanh mà giải pháp mang lại.

---

## Thách thức của ngành bảo hiểm

Các nhân viên môi giới bảo hiểm thường mất hàng giờ đồng hồ mỗi ngày cho những công việc lặp lại như:
- Hoàn thiện đơn xin bảo hiểm
- Phân tích và so sánh phạm vi bảo hiểm giữa các hãng
- Nhập liệu lại giữa nhiều hệ thống
- Trao đổi thông tin giữa khách hàng và công ty bảo hiểm

Trong bối cảnh thiếu hụt nhân sự ngày càng nghiêm trọng, các công ty môi giới cần tìm cách mở rộng doanh thu mà không phải tăng tỷ lệ nhân sự tương ứng. AI thông thường (generic AI) không thể đáp ứng được yêu cầu khắt khe của ngành: độ chính xác cao, khả năng kiểm toán, tuân thủ quy định và xử lý dữ liệu nhạy cảm.

---

## Hành trình của Cara

Đội ngũ sáng lập Cara (Vic Yeh, Nikhil Kansal và Jon Patel) từng xây dựng một công ty môi giới bảo hiểm kỹ thuật số và bán lại cho The McGowan Companies. Trong quá trình đó, họ phát triển một AI Copilot nội bộ dựa trên Large Language Models (LLMs) và nhận thấy hiệu quả vượt trội. Từ đó, họ quyết định xây dựng Cara như một sản phẩm độc lập, tập trung vào AI chuyên ngành cho môi giới bảo hiểm.

---

## Kiến trúc giải pháp trên AWS

Cara được thiết kế với tiêu chí **bảo mật, khả năng mở rộng và tuân thủ quy định**. Kiến trúc chính bao gồm:

### 1. Compute và Orchestration
- Sử dụng **Amazon Elastic Kubernetes Service (Amazon EKS)** để điều phối microservices.
- Triển khai đa Availability Zone, hỗ trợ scale tự động theo tải.
- Mỗi khách hàng (tenant) chạy trong namespace riêng biệt để đảm bảo cách ly hoàn toàn.

### 2. AI và Inference Layer
- **Amazon Bedrock** là nền tảng cốt lõi, cho phép truy cập các foundation models mà không cần quản lý hạ tầng GPU.
- Các tính năng AI nổi bật:
  - So sánh báo giá và phân tích chênh lệch phạm vi bảo hiểm
  - Tự động điền form ACORD và các biểu mẫu bổ sung
  - Tạo proposal và tài liệu renewal chuyên nghiệp
  - Workflow thông minh dựa trên kiến thức chuyên ngành (carrier appetite, guideline của agency…)

### 3. Bảo mật và Tuân thủ
- Triển khai theo mô hình account riêng cho từng khách hàng
- Cách ly dữ liệu hoàn toàn
- Mã hóa dữ liệu tại rest và in-transit
- Tích hợp AWS IAM để kiểm soát truy cập

### 4. Tích hợp hệ thống
Cara kết nối mượt mà với các hệ thống Agency Management System (AMS) và CRM, giúp giảm thiểu việc nhập liệu trùng lặp.

> *Hình 1. Kiến trúc tổng thể Cara trên AWS.*

---

## Kết quả kinh doanh

Cara đã mang lại những con số ấn tượng:

| Chỉ số                        | Kết quả đạt được |
|-------------------------------|------------------|
| Thời gian tiết kiệm mỗi user  | ~10 giờ/tuần |
| Tốc độ onboarding             | Trong vòng vài giờ |
| Khả năng xử lý đồng thời      | Hàng nghìn user và workflow |
| Số lượng khách hàng           | Hàng trăm công ty môi giới lớn |

Những kết quả này đến từ việc tự động hóa workflow chuyên sâu và khả năng truy xuất kiến thức theo ngữ cảnh của từng agency.

---

## Kết luận

Cara là minh chứng điển hình cho việc áp dụng AI chuyên ngành (domain-specific AI) trên nền tảng AWS. Bằng cách kết hợp **Amazon EKS** cho orchestration và **Amazon Bedrock** cho inference, Cara đã xây dựng được một nền tảng vừa mạnh mẽ, vừa an toàn và dễ mở rộng – đáp ứng đúng nhu cầu khắt khe của ngành bảo hiểm.

Giải pháp không chỉ giúp các công ty môi giới tiết kiệm thời gian và chi phí vận hành mà còn giúp nhân viên tập trung vào giá trị cốt lõi: xây dựng mối quan hệ với khách hàng.

Để tìm hiểu thêm về Cara, bạn có thể truy cập [www.getcara.ai](https://www.getcara.ai/). Các doanh nghiệp quan tâm đến việc xây dựng giải pháp AI trên AWS có thể bắt đầu với Amazon Bedrock và Amazon EKS.

---