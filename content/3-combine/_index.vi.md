---
title : "Áp dụng trong các kiến trúc phức tạp"
date :  "r Sys.Date()" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

Kiến trúc phổ biến khi áp dụng SQS và SNS là **Fanout**. Fanout Architecture nhằm mục đích tăng cường khả năng mở rộng (scaling) và tối ưu hóa chi phí.

#### 1. Fanout Architecture

- Fanout trong kiến trúc hệ thống có nghĩa là một thông điệp (message) từ một nguồn (SNS topic) sẽ được phân phối tới nhiều đích (SQS Queues). Điều này có nghĩa rằng thay vì chỉ có một nơi tiếp nhận và xử lý, thông điệp có thể được gửi đến nhiều nơi, giúp xử lý các công việc khác nhau một cách độc lập.

-  Ví dụ: Một SNS topic có thể nhận các thông điệp từ nhiều ứng dụng hoặc hệ thống khác nhau. Sau khi thông điệp được nhận, nó sẽ phân tán (fan out) đến nhiều hàng đợi (queues) khác nhau để các hệ thống khác có thể xử lý chúng theo cách riêng.

#### 2. Luồng hoạt động trong Fanout Architecture

- SNS Topic: Đây là nơi nhận thông điệp từ các ứng dụng hoặc người dùng. Ví dụ: một hệ thống có thể gửi thông điệp với nội dung là thông tin khách hàng, trong đó có một trường dữ liệu đặc biệt là ```book-type```

```
{
    book-type: "detective" | "romantic" | "horror",
    metadata: ...
}
```

- Minh họa bằng hình ảnh: 
  ![fanout](https://ngxquang.github.io/aws-ws1-sqs-sns/images/3.combine/combine.png)

- Trong kiến trúc trên, giả sử các publisher A, B, C gửi message có cấu trúc như trên vào SNS. SNS có 1 cơ chế là filter. Filter này có thể lọc các thông điệp dựa trên các trường dữ liệu cụ thể. Ở ví dụ trên là ```book-type```

- Nhờ vào khả năng này, message sẽ được phân loại và gửi tới đúng các hàng đợi (queues) tương ứng. Ví dụ:
    - message có ```book-type```: "detective" sẽ được chuyển tới Queue 1.
    - message có ```book-type```: "romantic" sẽ được chuyển tới Queue 2.
    - message có ```book-type```: "horror" sẽ được chuyển tới Queue 3.

- Mỗi Queue (Queue 1, Queue 2, Queue 3) sẽ có máy chủ riêng poll để nhận thông điệp và xử lý theo loại sách (book-type).

- Điều này có nghĩa rằng các hệ thống có thể được tối ưu hóa và mở rộng độc lập dựa trên khối lượng công việc của từng loại sách:
    - Ví dụ, người đọc ưa thích loại romantic có thể yêu cầu một hệ thống xử lý mạnh hơn, có nhiều tài nguyên hơn.
    - người đọc loại detective có số lượng ít có thể được xử lý bởi một hệ thống ít tài nguyên hơn vì yêu cầu của họ không cao.

#### 3. Giải quyết bài toán chi phí

- Fanout Architecture giúp tối ưu chi phí bằng cách phân tán các tác vụ xử lý dựa trên đặc thù từng loại dữ liệu, giúp hệ thống không phải tiêu tốn quá nhiều tài nguyên để xử lý tất cả mọi thứ trong một khối monolithic.

- Thay vì dồn tất cả các thông điệp vào một hệ thống duy nhất để xử lý, có thể chia nhỏ công việc ra thành nhiều phần, mỗi phần xử lý một khối lượng công việc cụ thể. Cho phép scale từng phần của hệ thống dựa trên nhu cầu thực tế, thay vì phải mở rộng toàn bộ hệ thống cùng một lúc.

- Ví dụ, nếu số lượng người đọc loại detective lớn hơn các loại khác, chỉ cần mở rộng các tài nguyên xử lý cho Queue 1, mà không cần tốn chi phí cho các hệ thống xử lý khác.