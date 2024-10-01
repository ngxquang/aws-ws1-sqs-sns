---
title: "Serverless Services"
date: "r Sys.Date()"
weight: 1
chapter: false
pre: " <b> 1.2 </b> "
---

#### 1. No Infrastructure Management
  - Both Amazon SQS and SNS do not require users to manage servers or physical infrastructure. AWS automatically handles provisioning, scaling, and server management, allowing users to focus on application logic rather than maintaining physical resources.

#### 2. Auto-scaling
  - With a serverless architecture, SQS and SNS automatically scale according to workload. As message traffic increases, the system processes it automatically without the need for manual configuration or management.

#### 3. Flexible Cost Structure (Pay-as-you-go)
  - With serverless, users only pay for the resources actually used. **In SQS**, users only pay for the number of messages sent and received. **In SNS**, users only pay for the messages sent. This model helps optimize costs as there is no need to maintain resources continuously even when there is no workload.

#### 4. Regional Scope
  - **AWS regional scope** refers to how AWS services are deployed and managed in specific geographical areas (regions). Each region is a collection of isolated data centers, allowing users to choose where their resources will be deployed to meet performance requirements, regulatory compliance, or data redundancy.

  - Serverless services such as AWS Lambda, Amazon SQS, Amazon SNS, and DynamoDB are all services that fall under regional scope.

  - AWS regional scope is closely related to serverless services because they all require choosing a region for deployment and usage.
