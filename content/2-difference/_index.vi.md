---
title : "Điểm khác"
date :  "r Sys.Date()" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

Amazon SNS (Simple Notification Service) và Amazon SQS (Simple Queue Service) đều là các dịch vụ messaging của AWS, nhưng chúng phục vụ cho những mục đích và kiến trúc khác nhau. 

Trong khi **SNS hoạt động theo mô hình push** để phân phối thông báo tới nhiều subscriber thông qua cơ chế broadcast, thì **SQS sử dụng mô hình pull** để lưu trữ và xử lý thông điệp thông qua các hàng đợi độc lập.

### Nội dung
  - [Amazon SQS](2.1-sqs/)
  - [Amazon SNS](2.2-sns/)