---
title: "Blog 3"
date: 2026-06-21
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---



# Xây dựng hệ thống Thần Số Học (LunaGENZ) trên kiến trúc Serverless AWS kết hợp Generative AI

Sự phát triển của Generative AI đã mở ra nhiều cơ hội để xây dựng các ứng dụng thông minh với khả năng tạo nội dung tự động. Tuy nhiên, để triển khai các ứng dụng AI trong thực tế, ngoài việc lựa chọn mô hình ngôn ngữ phù hợp còn cần một kiến trúc hạ tầng có khả năng mở rộng, tối ưu chi phí và giảm thiểu công tác vận hành.

Trong dự án **LunaGENZ**, nhóm chúng tôi xây dựng một hệ thống luận giải Thần số học cá nhân hóa bằng cách kết hợp **Generative AI** với kiến trúc **Serverless trên AWS**. Hệ thống cho phép người dùng nhập thông tin cá nhân, tự động sinh nội dung luận giải bằng AI, tạo báo cáo PDF và gửi kết quả qua email mà không cần bất kỳ thao tác thủ công nào.

Bài viết này chia sẻ quá trình thiết kế kiến trúc của LunaGENZ, các thách thức gặp phải trong quá trình phát triển cũng như cách các dịch vụ AWS được kết hợp để xây dựng một hệ thống linh hoạt, dễ mở rộng và tiết kiệm chi phí.

---

## Tổng quan về hệ thống

LunaGENZ được xây dựng với ba mục tiêu chính:

- Tự động hóa quá trình luận giải Thần số học bằng Generative AI.
- Giảm thiểu việc quản lý hạ tầng thông qua mô hình Serverless.
- Tối ưu chi phí triển khai trong giai đoạn phát triển và thử nghiệm.

Thay vì triển khai trên máy chủ truyền thống, toàn bộ hệ thống được xây dựng bằng các dịch vụ được quản lý hoàn toàn trên AWS. Điều này giúp nhóm phát triển tập trung vào nghiệp vụ thay vì dành nhiều thời gian cho việc cấu hình và vận hành hạ tầng.

> *Hình 1. Kiến trúc tổng thể của hệ thống LunaGENZ.*

---

## Kiến trúc Serverless cho LunaGENZ

Ngay từ đầu, nhóm xác định rằng LunaGENZ là một dự án có lượng truy cập chưa ổn định và ngân sách triển khai còn hạn chế. Vì vậy, việc lựa chọn kiến trúc Serverless giúp giảm đáng kể chi phí cũng như công sức quản trị hệ thống.

Giải pháp bao gồm các thành phần chính sau:

- **Frontend:** Next.js triển khai trên AWS Amplify Hosting.
- **API Layer:** Amazon API Gateway.
- **Business Logic:** AWS Lambda.
- **Database:** Amazon DynamoDB (On-Demand Mode).
- **Message Queue:** Amazon SQS.
- **AI Service:** Amazon Bedrock (Claude 3 Haiku).
- **Storage:** Amazon S3.
- **Email Service:** Amazon Simple Email Service (Amazon SES).

Kiến trúc này cho phép từng thành phần hoạt động độc lập và tự động mở rộng theo nhu cầu sử dụng thực tế.

Một số lợi ích nổi bật của mô hình Serverless gồm:

- Không cần quản lý máy chủ.
- Tự động mở rộng tài nguyên.
- Chỉ trả phí theo lượng sử dụng thực tế.
- Dễ dàng triển khai và bảo trì.
- Phù hợp với các dự án có lưu lượng truy cập thay đổi liên tục.

---

## Luồng xử lý của hệ thống

LunaGENZ được xây dựng theo mô hình **Event-Driven Architecture**, trong đó mỗi dịch vụ chỉ đảm nhận một vai trò riêng biệt.

Quy trình xử lý gồm các bước sau:

1. Người dùng nhập thông tin cá nhân trên giao diện web.
2. Amazon API Gateway tiếp nhận và xác thực yêu cầu.
3. AWS Lambda xử lý nghiệp vụ ban đầu.
4. Kiểm tra trạng thái thanh toán trong Amazon DynamoDB.
5. Đưa yêu cầu vào Amazon SQS.
6. Lambda xử lý nền tự động nhận message từ SQS.
7. Amazon Bedrock sinh nội dung luận giải Thần số học.
8. Hệ thống tạo báo cáo PDF.
9. Báo cáo được lưu trên Amazon S3.
10. Amazon SES gửi email chứa liên kết tải báo cáo cho người dùng.

Việc tách toàn bộ quy trình thành nhiều bước giúp hệ thống dễ mở rộng, tăng khả năng chịu lỗi và giảm sự phụ thuộc giữa các thành phần.

---

## Giải quyết bài toán Timeout bằng Amazon SQS

Trong quá trình phát triển, nhóm gặp phải một vấn đề phổ biến khi xây dựng các ứng dụng AI là thời gian xử lý của mô hình ngôn ngữ thường vượt quá giới hạn **29 giây** của Amazon API Gateway.

Ban đầu, hệ thống thực hiện toàn bộ các bước trong cùng một request:

- Gọi AI sinh nội dung.
- Tạo báo cáo PDF.
- Lưu file lên Amazon S3.
- Gửi email cho người dùng.

Do quá trình sinh nội dung và tạo PDF mất nhiều thời gian nên API thường xuyên bị Timeout.

Để giải quyết vấn đề này, nhóm đã chuyển sang mô hình xử lý bất đồng bộ bằng **Amazon SQS**.

Thay vì chờ toàn bộ quy trình hoàn tất, Lambda chỉ thực hiện:

1. Kiểm tra dữ liệu đầu vào.
2. Xác minh trạng thái thanh toán.
3. Đưa yêu cầu vào Amazon SQS.
4. Trả về phản hồi "Đang xử lý" ngay lập tức.

Một Lambda khác sẽ được kích hoạt tự động thông qua SQS để tiếp tục xử lý toàn bộ công việc phía sau.

Giải pháp này mang lại nhiều lợi ích:

- Loại bỏ hoàn toàn lỗi Timeout.
- Tăng khả năng mở rộng khi có nhiều yêu cầu đồng thời.
- Tránh mất dữ liệu khi xảy ra lỗi.
- Cải thiện trải nghiệm người dùng.

---

## Tích hợp Generative AI với Amazon Bedrock

Thành phần quan trọng nhất của LunaGENZ là khả năng tạo nội dung luận giải bằng Generative AI.

Hệ thống sử dụng **Claude 3 Haiku** thông qua **Amazon Bedrock** thay vì các mô hình lớn hơn.

Việc lựa chọn Claude 3 Haiku dựa trên các tiêu chí:

- Thời gian phản hồi nhanh.
- Chi phí thấp.
- Chất lượng sinh tiếng Việt đáp ứng tốt yêu cầu của dự án.
- Không cần các khả năng suy luận quá phức tạp.

Thông tin gửi tới mô hình AI bao gồm:

- Họ và tên.
- Ngày sinh.
- Dữ liệu từ điển Thần số học.
- System Prompt.
- User Prompt.

Sau khi xử lý, Amazon Bedrock trả về nội dung luận giải hoàn chỉnh bằng tiếng Việt để sử dụng trong báo cáo cuối cùng.

---

## Bảo mật và quản lý hạ tầng

Mặc dù LunaGENZ là một dự án học tập, nhóm vẫn áp dụng các nguyên tắc bảo mật cơ bản nhằm đảm bảo an toàn cho hệ thống.

### AWS Secrets Manager

Các thông tin nhạy cảm như API Key, Webhook Secret và Access Token đều được lưu trong AWS Secrets Manager thay vì hardcode trong mã nguồn.

### AWS Identity and Access Management (IAM)

Mỗi Lambda được cấp một IAM Role riêng theo nguyên tắc **Least Privilege**, chỉ được phép truy cập vào những tài nguyên cần thiết.

### Amazon Cognito

Amazon Cognito được sử dụng để quản lý người dùng, hỗ trợ đăng ký, đăng nhập và cấp phát JWT Token để bảo vệ các API.

---

## Tạo và phân phối báo cáo

Sau khi Amazon Bedrock hoàn tất việc sinh nội dung, Lambda xử lý nền sẽ tiếp tục tạo báo cáo PDF.

Quy trình phân phối gồm các bước:

1. Sinh file PDF.
2. Lưu báo cáo lên Amazon S3.
3. Gửi email qua Amazon SES.
4. Người dùng nhận liên kết tải báo cáo.

Quá trình này diễn ra hoàn toàn tự động mà không cần bất kỳ thao tác thủ công nào từ phía quản trị viên.

---

## Tối ưu chi phí vận hành

Một trong những mục tiêu quan trọng của LunaGENZ là giảm chi phí triển khai.

Một số giải pháp được áp dụng gồm:

- DynamoDB On-Demand giúp không cần dự báo trước dung lượng.
- AWS Lambda chỉ tính phí theo thời gian thực thi.
- Amazon SQS giúp xử lý bất đồng bộ mà không cần máy chủ trung gian.
- Amazon S3 lưu trữ báo cáo với chi phí thấp.
- S3 Lifecycle Policy tự động chuyển các báo cáo cũ sang Amazon S3 Glacier nhằm tiết kiệm chi phí lưu trữ.

Trong giai đoạn thử nghiệm, tổng chi phí vận hành của toàn bộ hệ thống chỉ khoảng **1 USD**, cho thấy mô hình Serverless phù hợp với các dự án quy mô nhỏ và trung bình.

---

## Bài học rút ra

Thông qua quá trình xây dựng LunaGENZ, nhóm đã tích lũy được nhiều kinh nghiệm về việc thiết kế hệ thống AI trên nền tảng đám mây.

Một số bài học quan trọng gồm:

- Kiến trúc Serverless giúp giảm đáng kể công tác quản trị hạ tầng.
- Các tác vụ AI nên được xử lý bất đồng bộ để tránh giới hạn thời gian của API Gateway.
- Việc lựa chọn mô hình AI cần cân bằng giữa chi phí và hiệu năng thay vì chỉ ưu tiên mô hình mạnh nhất.
- Các dịch vụ được quản lý trên AWS giúp đơn giản hóa quá trình triển khai và vận hành.

Trong tương lai, nhóm dự kiến sẽ tiếp tục cải thiện khả năng giám sát, xử lý lỗi của Lambda xử lý nền và tối ưu chi phí khi hệ thống mở rộng ở quy mô lớn hơn.

---

## Kết luận

LunaGENZ là một ví dụ về việc kết hợp thành công giữa **Generative AI** và **kiến trúc Serverless trên AWS** để xây dựng một ứng dụng thông minh có khả năng mở rộng, vận hành ổn định và tối ưu chi phí.

Thông qua việc tích hợp **Amazon API Gateway**, **AWS Lambda**, **Amazon DynamoDB**, **Amazon SQS**, **Amazon Bedrock**, **Amazon S3** và **Amazon SES**, toàn bộ quy trình từ tiếp nhận yêu cầu, sinh nội dung AI, tạo báo cáo PDF đến gửi kết quả cho người dùng đều được tự động hóa hoàn toàn.

Đối với các nhóm phát triển đang tìm hiểu cách xây dựng ứng dụng AI trên nền tảng AWS, LunaGENZ là một ví dụ thực tế cho thấy kiến trúc Serverless kết hợp Generative AI có thể giúp giảm đáng kể chi phí vận hành, đơn giản hóa việc triển khai và tạo nền tảng thuận lợi để mở rộng hệ thống trong tương lai.