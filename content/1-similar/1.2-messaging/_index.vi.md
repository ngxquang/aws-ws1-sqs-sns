---
title: "Dịch vụ messaging"
date: "r Sys.Date()"
weight: 1
chapter: false
pre: " <b> 1.1 </b> "
---

**Amazon Simple Queue Service (SQS)** và **Amazon Simple Notification Service (SNS)** đều là các dịch vụ messaging của AWS, được sử dụng để trao đổi thông điệp giữa các hệ thống và ứng dụng phân tán. Mặc dù SQS và SNS có những cách tiếp cận khác nhau trong cách chúng xử lý và truyền tải thông điệp, nhưng chúng đều được thiết kế nhằm mục tiêu đảm bảo tính nhất quán, khả năng mở rộng, và giảm tải khi truyền thông điệp giữa các hệ thống.

![2](https://ngxquang.github.io/aws-ws1-sqs-sns/images/1.similar/2.png)

#### 1. Tăng khả năng mở rộng - Scalability
  - Cả SQS và SNS đều cho phép các hệ thống xử lý thông điệp một cách không đồng bộ. Các hệ thống không cần phải đợi nhau để hoàn thành việc xử lý, mà có thể tiếp tục hoạt động, giảm thiểu tắc nghẽn.

#### 2. Tính phân tán - Decoupling
  - Messaging giúp phân tán các thành phần hệ thống, giúp cho các hệ thống không phụ thuộc trực tiếp vào nhau. Với messaging, các dịch vụ có thể giao tiếp mà không cần biết hệ thống phía sau đang thực hiện những gì hoặc thời gian xử lý thông điệp ra sao.

#### 3. Đảm bảo thứ tự và tính toàn vẹn của thông điệp
  - Cả SNS và SQS đều hỗ trợ việc đảm bảo thứ tự thông điệp (đặc biệt trong trường hợp SQS FIFO queues) và khả năng giao tiếp với nhiều dịch vụ, hệ thống khác nhau mà không làm mất đi sự nhất quán.


![messaging](https://ngxquang.github.io/aws-ws1-sqs-sns/images/1.similar/messaging.jpg)
