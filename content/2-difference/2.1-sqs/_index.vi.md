---
title : "Amazon SQS"
date :  "r Sys.Date()" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### 1. Producer và Cusomter trong kiến trúc của Amazon SQS
  - **Producer** là các ứng dụng hoặc hệ thống sản xuất và gửi thông điệp (message) vào hàng đợi (queue). Trong SQS, một producer có thể đẩy nhiều message không giới hạn vào queue. Việc producer chỉ cần gửi message mà không cần quan tâm đến thời điểm hay cách thức message được xử lý sau đó chính là điểm mạnh của kiến trúc decoupling.

  - **Consumer** là các ứng dụng hoặc hệ thống nhận và xử lý message từ hàng đợi. Trong SQS, consumer chủ động lấy (pull) các message từ hàng đợi trong khoảng thời gian nhất định. Số lượng message mỗi lần consumer có thể lấy phụ thuộc vào thiết lập (polling) của hệ thống, có thể là một hoặc nhiều message.

  - Trong hình vẽ, giả sử ta có 3 producer gửi các message m1, m2 và m3 vào Queue. Có 3 customer thực hiện vào để lấy message ra trong 1 khoảng interval. Mỗi lần lấy có thể là 1 hoặc nhiều message. Customer 1 có thể lấy m1, m2 cùng lúc, customer 2 có thể lấy m3, ...

  ![sqs](https://ngxquang.github.io/aws-ws1-sqs-sns/images/2.difference/sqs.png)

#### 2. SQS giúp giải quyết vấn đề Async (bất đồng bộ)
  - SQS hỗ trợ mô hình bất đồng bộ (asynchronous), nơi các producer gửi message mà không cần phải đợi các consumer xử lý chúng ngay lập tức, cho phép các thành phần của hệ thống hoạt động độc lập, không phụ thuộc vào nhau về mặt thời gian. 
  
  - Hệ thống chỉ cần chắc chắn rằng thông điệp được gửi vào Queue, và consumer sẽ xử lý sau.

#### 3. Các tính chất của SQS

##### 3.1 Liên quan đến Pull/Poll message

  - SQS không tự động đẩy message đến consumer, thay vào đó, consumer **phải chủ động** vào hàng đợi để lấy message. Quá trình này gọi là **polling**. Consumer sẽ gửi yêu cầu tới SQS để lấy message, và queue sẽ trả về các message có sẵn.

  - Thông thường trong các kiến trúc Async thì sẽ xử lý phần message được producer đưa vào luôn nhưng đối với kiến trúc này thì tách biệt 2 phần xử lý → Kiến trúc liên quan đến Queue nói chung và SQS nói riêng được gọi là **Decoupling**

  ![decoupling](https://ngxquang.github.io/aws-ws1-sqs-sns/images/2.difference/decoupling.jpg)


##### 3.2 Các loại Queue trong SQS

  - Khi các Consumer chui vào lấy message thì **không có khả năng tự chọn** message để lấy. Việc Queue trả về message nào thì tùy vào tính chất của Queue.

  - Có 2 loại Queue:
    - FIFO Queue
  ![fifo](https://ngxquang.github.io/aws-ws1-sqs-sns/images/2.difference/sqs-fifo.png)

    - Standard Queue

##### 3.3 Persistent

  - Các message trong SQS được lưu trữ trong hàng đợi và được xem là **persistent** (tồn tại lâu dài) cho đến khi chúng được một consumer xử lý thành công. Message có thể lưu trữ trong SQS tối đa 14 ngày. Nếu không được xử lý trong khoảng thời gian này, message sẽ bị tự động xóa.


##### 3.4 Quan hệ 1-1 giữa Message và Consumer

  - Trong kiến trúc SQS, một message chỉ có thể được xử lý bởi một consumer duy nhất tại một thời điểm. Điều này đảm bảo rằng mỗi message chỉ được xử lý một lần (đối với FIFO queue hoặc khi đã xử lý thành công đối với Standard queue).

