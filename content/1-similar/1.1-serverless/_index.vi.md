---
title: "Dịch vụ Serverless"
date: "r Sys.Date()"
weight: 1
chapter: false
pre: " <b> 1.2 </b> "
---

#### 1. Không cần quản lý cơ sở hạ tầng
  - Cả Amazon SQS và SNS đều không yêu cầu người dùng phải quản lý máy chủ hoặc cơ sở hạ tầng vật lý. AWS sẽ tự động lo việc provisioning, scaling, và quản lý server, giúp người dùng tập trung vào logic ứng dụng thay vì lo về việc duy trì các tài nguyên vật lý.

#### 2. Tự động mở rộng (Auto-scaling)
  - Với kiến trúc serverless, SQS và SNS tự động mở rộng theo khối lượng công việc. Khi lưu lượng thông điệp tăng lên, hệ thống sẽ tự động xử lý mà không cần cấu hình hoặc quản lý thủ công.

#### 3. Tính chi phí linh hoạt (Pay-as-you-go)
  - Với serverless, người dùng chỉ phải trả tiền cho tài nguyên thực sự được sử dụng. **Trong SQS**, chỉ cần trả cho số lượng thông điệp gửi và nhận. **Trong SNS**, chỉ cần trả cho thông báo (message) được gửi đi. Mô hình này giúp tối ưu chi phí vì không cần phải duy trì các tài nguyên liên tục ngay cả khi không có lưu lượng công việc.

#### 4. Regional Scope
  - **AWS regional scope** đề cập đến cách các dịch vụ AWS được triển khai và quản lý trong các khu vực địa lý cụ thể (regions). Mỗi region (khu vực) là một tập hợp các trung tâm dữ liệu được phân lập, cho phép người dùng lựa chọn nơi tài nguyên của họ sẽ được triển khai để đáp ứng yêu cầu về hiệu suất, tuân thủ quy định hoặc dự phòng dữ liệu.

  - Các dịch vụ serverless như AWS Lambda, Amazon SQS, Amazon SNS, DynamoDB đều là dịch vụ thuộc regional scope

  - AWS regional scope có liên quan mật thiết đến các dịch vụ serverless vì chúng đều yêu cầu việc chọn lựa region để triển khai và sử dụng.

