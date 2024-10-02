---
title: "Application in Complex Architectures"
date: "r Sys.Date()"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

A common architecture when applying SQS and SNS is **Fanout**. The Fanout Architecture aims to enhance scalability and optimize costs.

#### 1. Fanout Architecture

- Fanout in system architecture means that a message from a source (SNS topic) will be distributed to multiple destinations (SQS Queues). This means that instead of having a single point of reception and processing, messages can be sent to various locations, allowing different tasks to be processed independently.

- For example, an SNS topic can receive messages from multiple applications or systems. After receiving a message, it will fan out to different queues for various systems to process them in their own way.

#### 2. Workflow in Fanout Architecture

- SNS Topic: This is where messages are received from applications or users. For instance, a system might send a message containing book type information, with a specific data field being ```book-type```.

```
{ 
    book-type: "detective" | "romantic" | "horror", metadata: ... 
}
```

- Illustrated with an image: 
  ![fanout](https://ngxquang.github.io/aws-ws1-sqs-sns/images/3.combine/combine.png)

- In the above architecture, suppose publishers A, B, and C send messages structured as shown to SNS. SNS has a filtering mechanism. This filter can filter messages based on specific data fields, such as ```book-type``` in this example.

- Thanks to this capability, messages will be categorized and sent to the corresponding queues. For instance:
    - A message with ```book-type```: "detective" will be directed to Queue 1.
    - A message with ```book-type```: "romantic" will be directed to Queue 2.
    - A message with ```book-type```: "horror" will be directed to Queue 3.

- Each Queue (Queue 1, Queue 2, Queue 3) will have its own polling server to receive messages and process them according to book type.

- This means that systems can be optimized and scaled independently based on the workload of each book type:
    - For example, readers who prefer romantic books may require a more powerful processing system with more resources.
    - Readers of detective books, who are fewer in number, can be handled by a less resource-intensive system since their demands are not high.

#### 3. Cost Optimization

- The Fanout Architecture helps optimize costs by distributing processing tasks based on the characteristics of each type of data, preventing the system from overusing resources to handle everything in a monolithic block.

- Instead of funneling all messages into a single system for processing, tasks can be broken down into smaller parts, with each part handling a specific workload. This allows for scaling each part of the system based on actual demand, rather than needing to scale the entire system all at once.

- For example, if the number of readers for detective books is larger than for other types, only the processing resources for Queue 1 need to be expanded, without incurring costs for other processing systems.
