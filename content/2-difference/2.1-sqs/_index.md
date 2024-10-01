---
title: "Amazon SQS"
date: "r Sys.Date()"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

#### 1. Producer and Consumer in the Architecture of Amazon SQS
  - **Producer** refers to applications or systems that produce and send messages into the queue. In SQS, a producer can push an unlimited number of messages into the queue. The strength of the decoupling architecture is that the producer only needs to send messages without worrying about when or how those messages are processed afterward.

  - **Consumer** refers to applications or systems that receive and process messages from the queue. In SQS, the consumer actively pulls messages from the queue within a certain timeframe. The number of messages a consumer can pull at a time depends on the system's polling configuration and can be one or multiple messages.

  - In the illustration, suppose we have three producers sending messages m1, m2, and m3 into the Queue. There are three consumers that pull messages within a certain interval. Each pull can be one or multiple messages. Consumer 1 might pull m1 and m2 at the same time, while consumer 2 might pull m3, and so on.

  ![sqs](https://ngxquang.github.io/aws-ws1-new/images/2.difference/sqs.png)

#### 2. SQS Helps Solve Async Problems
  - SQS supports an asynchronous model where producers send messages without needing to wait for consumers to process them immediately, allowing system components to operate independently of each other in terms of time.

  - The system only needs to ensure that the messages are sent to the Queue, and consumers will handle them later.

#### 3. Properties of SQS

##### 3.1 Related to Pull/Poll Messages

  - SQS does not automatically push messages to consumers; instead, consumers **must actively** poll the queue for messages. This process is known as **polling**. The consumer will send a request to SQS to retrieve messages, and the queue will return the available messages.

  - Typically, in asynchronous architectures, messages produced are processed immediately, but in this architecture, the processing is separated → The architecture related to the Queue in general and SQS in particular is referred to as **Decoupling**.

  ![decoupling](https://ngxquang.github.io/aws-ws1-new/images/2.difference/decoupling.jpg)

##### 3.2 Types of Queues in SQS

  - When consumers pull messages, they **cannot select** which messages to retrieve. The messages returned by the Queue depend on the nature of the Queue.

  - There are two types of queues:
    - FIFO Queue
  ![fifo](https://ngxquang.github.io/aws-ws1-new/images/2.difference/sqs-fifo.png)

    - Standard Queue

##### 3.3 Persistent

  - Messages in SQS are stored in the queue and are considered **persistent** until they are successfully processed by a consumer. Messages can be stored in SQS for a maximum of 14 days. If not processed within this timeframe, the messages will be automatically deleted.

##### 3.4 One-to-One Relationship Between Message and Consumer

  - In the SQS architecture, a message can only be processed by a single consumer at any given time. This ensures that each message is processed only once (for FIFO queues or when successfully processed for standard queues).
