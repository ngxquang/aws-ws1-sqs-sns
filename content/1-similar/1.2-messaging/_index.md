---
title: "Messaging Services"
date: "r Sys.Date()"
weight: 1
chapter: false
pre: " <b> 1.1 </b> "
---

**Amazon Simple Queue Service (SQS)** and **Amazon Simple Notification Service (SNS)** are both messaging services from AWS, used to exchange messages between distributed systems and applications. Although SQS and SNS take different approaches in how they handle and deliver messages, they are designed to ensure consistency, scalability, and offloading when communicating between systems.

![2](https://ngxquang.github.io/aws-ws1-new/images/1.similar/2.png)

#### 1. Enhanced Scalability
  - Both SQS and SNS allow systems to process messages asynchronously. Systems do not need to wait for each other to complete processing and can continue to operate, reducing congestion.

#### 2. Decoupling
  - Messaging helps decouple system components, allowing systems not to depend directly on each other. With messaging, services can communicate without needing to know what the backend system is doing or how long message processing will take.

#### 3. Ensuring Message Order and Integrity
  - Both SNS and SQS support ensuring message order (especially in the case of SQS FIFO queues) and can communicate with various services and systems without losing consistency.

![messaging](https://ngxquang.github.io/aws-ws1-new/images/1.similar/messaging.jpg)
