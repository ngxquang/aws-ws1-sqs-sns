---
title: "Amazon SNS"
date: "r Sys.Date()"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

#### 1. Topic and Difference from Queue

  - The difference from SQS:
    - SNS does not use a queue like SQS, but instead uses the concept of a Topic. While SQS uses queues to temporarily store messages until they are pulled by consumers, SNS uses topics to manage and distribute messages immediately to subscribers.

  - In SNS, messages are not stored in the topic but are sent directly to subscribers upon receipt.

#### 2. Publisher and Subscriber

  - **Publisher**: Publishers play the role of sending messages into a topic. A publisher can be any service or system capable of emitting messages that need to be conveyed to recipients (subscribers).

  - **Subscriber**: Subscribers register to receive messages from a specific topic. A topic can have multiple subscribers, and when a message is published, all subscribers will **receive the message simultaneously**.

  - In the example illustrated, there is one publisher sending a message to the topic. This topic will broadcast the message to all subscribers at once.

  ![sns](https://ngxquang.github.io/aws-ws1-new/images/2.difference/sns.png)

#### 3. Properties of SNS

##### 3.1 Push Model

  - The Push Model is a significant difference between SNS and SQS. In SNS, instead of consumers having to actively pull messages from a queue, messages are pushed immediately from the topic to all subscribers.

  - This push mechanism greatly enhances the speed of information transmission as messages are distributed instantly, making it suitable for real-time applications.

##### 3.2 Broadcast

  - The SNS model operates in a broadcast manner: meaning a message from the publisher will be sent to all subscribers registered with the topic. This allows SNS to distribute messages to multiple destinations at once, creating a one-to-many (1-n) message transmission model.

##### 3.3 Non-persistent

  - SNS does not store messages (non-persistent). This means that when a message is sent to a topic, it is immediately distributed to the subscribers, and there is no mechanism for retaining that message in the topic. If no subscribers are registered or if a subscriber fails to receive the message, the message will not be retained for later processing.

##### 3.4 One-to-Many Relationship

  - In the SNS model, a topic can have multiple subscribers. This creates a one-to-many relationship, where a publisher sends a message to a topic, and that message will be distributed to all registered subscribers. This differs from SQS, where each message is typically processed by a single consumer (one-to-one relationship).

  - This difference makes SNS suitable for use cases where messages need to be sent to multiple services or multiple recipients simultaneously.
