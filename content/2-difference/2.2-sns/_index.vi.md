---
title : "Amazon SNS"
date :  "r Sys.Date()" 
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

#### 1. Topic và sự khác biệt với Queue

  - Sự khác biệt với SQS:
    - SNS không sử dụng Queue như SQS, mà sử dụng khái niệm Topic. Trong khi SQS sử dụng hàng đợi (queue) để lưu trữ tạm thời các thông điệp cho đến khi chúng được các consumer lấy ra, SNS sử dụng các topic để quản lý và phân phối thông điệp ngay lập tức cho các subscriber.

  - Trong SNS, các message không lưu trữ trong topic mà sẽ được gửi trực tiếp tới các subscriber khi nhận được.


#### 2. Publisher và Subscriber

  - **Publisher**: Các publisher đóng vai trò gửi thông điệp vào topic. Publisher có thể là bất kỳ dịch vụ, hệ thống nào có khả năng phát ra các thông điệp cần truyền tải đến người nhận (subscriber).

  - **Subscriber**: Các subscriber đăng ký nhận thông điệp từ một topic cụ thể. Một topic có thể có nhiều subscriber, và khi có thông điệp từ publisher, tất cả các subscriber sẽ **nhận được thông điệp cùng một lúc**.

  - Xét ví dụ trong hình, có 1 publisher gửi message tới topic. Topic này sẽ bắn message tới tất cả các subscriber cùng lúc

  ![sns](https://ngxquang.github.io/aws-ws1-sqs-sns/images/2.difference/sns.png)


#### 3. Các tính chất của SNS

##### 3.1 Push Model

  - Push Model là điểm khác biệt lớn giữa SNS và SQS. Trong SNS, thay vì các consumer phải chủ động lấy (pull) thông điệp từ hàng đợi, message được đẩy (push) ngay lập tức từ topic đến tất cả các subscriber.

  - Đem lại lợi ích lớn khi cơ chế push này giúp tăng cường tốc độ truyền tải thông tin khi thông điệp được phân phối ngay lập tức, phù hợp với các ứng dụng đòi hỏi thời gian thực.

##### 3.2 Broadcast

  - Mô hình của SNS hoạt động theo kiểu broadcast: tức là một thông điệp từ publisher sẽ được gửi tới tất cả các subscriber đã đăng ký với topic. Điều này cho phép SNS phân phối thông điệp đến nhiều đích nhận cùng lúc, tạo nên mô hình truyền tin kiểu 1 - n (một thông điệp gửi tới nhiều người).

##### 3.3 Non-persistent

  - SNS không lưu trữ thông điệp (non-persistent). Điều này có nghĩa là khi một thông điệp được gửi vào topic, nó sẽ được phân phối ngay lập tức đến các subscriber và không có cơ chế lưu trữ lại thông điệp đó trong topic. Nếu không có subscriber nào đăng ký hoặc nếu một subscriber không nhận được thông điệp, thông điệp sẽ không được giữ lại để xử lý sau.

##### 3.4 Quan hệ 1 - N

  - Trong mô hình của SNS, một topic có thể có nhiều subscriber. Điều này tạo ra mối quan hệ 1 - n, tức là một publisher gửi một thông điệp đến topic, và thông điệp đó sẽ được phân phối đến tất cả các subscriber đã đăng ký. Điều này khác với SQS, nơi mà mỗi thông điệp thường chỉ được xử lý bởi một consumer duy nhất (quan hệ 1 - 1).

  - Sự khác biệt này giúp SNS trở nên phù hợp với các trường hợp sử dụng mà cần thông điệp được gửi đến nhiều dịch vụ hoặc nhiều người nhận cùng lúc.