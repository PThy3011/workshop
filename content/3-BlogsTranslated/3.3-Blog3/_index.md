---
title: "Blog 3"
date: 2026-06-21
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---



# Building LunaGENZ: A Serverless Numerology Platform with Generative AI on AWS

As Generative AI continues to transform the way applications are built, many developers are exploring how to combine large language models with cloud-native architectures to create scalable and cost-effective solutions.

In this project, our team developed **LunaGENZ**, a personalized numerology interpretation platform that leverages **Generative AI** and a **serverless architecture on AWS**. The system automatically generates personalized numerology reports based on user information, converts the results into PDF documents, and delivers them via email without requiring manual intervention.

This blog shares the architectural decisions behind LunaGENZ, the challenges encountered during development, and how AWS serverless services helped us build a scalable and reliable solution.

---

## Project Overview

LunaGENZ was designed with three primary objectives:

- Generate personalized numerology reports using Generative AI.
- Minimize infrastructure management through a fully serverless architecture.
- Optimize operational costs while maintaining scalability and reliability.

Instead of deploying traditional virtual machines or container clusters, the application relies entirely on managed AWS services that automatically scale according to demand.

> *Figure 1. Overall architecture of the LunaGENZ platform.*

---

## Why We Chose a Serverless Architecture

At the beginning of the project, our team evaluated several deployment options. Because LunaGENZ is an academic project with unpredictable traffic, we wanted to avoid managing servers while keeping infrastructure costs as low as possible.

The final architecture consists of:

- **Frontend:** Next.js deployed with AWS Amplify Hosting
- **API Layer:** Amazon API Gateway
- **Business Logic:** AWS Lambda
- **Database:** Amazon DynamoDB (On-Demand Mode)
- **Message Queue:** Amazon SQS
- **AI Service:** Amazon Bedrock (Claude 3 Haiku)
- **Storage:** Amazon S3
- **Email Delivery:** Amazon SES

This architecture allows every service to scale independently while charging only for actual usage.

Some of the key benefits include:

- No server administration.
- Automatic scaling.
- High availability.
- Lower operational costs during development.
- Faster deployment cycles.

---

## Overall System Architecture

The LunaGENZ platform follows an **event-driven serverless architecture**, where each AWS service is responsible for a specific task.

The overall request flow is as follows:

1. Users submit personal information through the web application.
2. Amazon API Gateway validates the request.
3. AWS Lambda processes the business logic.
4. Payment status is verified through Amazon DynamoDB.
5. A processing request is published to Amazon SQS.
6. A background Lambda function consumes the message.
7. Amazon Bedrock generates the personalized numerology interpretation.
8. A PDF report is created.
9. The report is stored in Amazon S3.
10. Amazon SES sends the download link to the user's email.

By separating each stage into independent services, the platform becomes more scalable and resilient.

---

## Solving the API Gateway Timeout Challenge

One of the biggest technical challenges we encountered involved the **29-second timeout limit** imposed by Amazon API Gateway.

Initially, the application attempted to perform every operation within a single HTTP request:

- Generate AI content.
- Render the PDF report.
- Upload the PDF to Amazon S3.
- Send the email.

Because Generative AI inference and PDF generation require several seconds to complete, the API frequently exceeded the timeout limit.

To overcome this limitation, we redesigned the workflow using **Amazon Simple Queue Service (Amazon SQS)**.

Instead of waiting for the entire report generation process, the API now performs the following steps:

1. Validate the request.
2. Verify payment status.
3. Publish a message to Amazon SQS.
4. Immediately return a "Processing" response to the client.

A separate Lambda function is automatically triggered by Amazon SQS to process the request asynchronously.

This asynchronous architecture provides several advantages:

- Eliminates API timeout errors.
- Improves user experience.
- Prevents request loss during temporary failures.
- Supports processing large numbers of requests simultaneously.

---

## Generating Personalized Reports with Amazon Bedrock

The core intelligence of LunaGENZ is powered by **Amazon Bedrock**, using the **Claude 3 Haiku** foundation model.

Instead of selecting a larger and more computationally expensive model, our team chose Claude 3 Haiku because:

- Response time is significantly faster.
- Operating costs are lower.
- The numerology interpretation task does not require complex reasoning.
- Vietnamese language generation quality is sufficient for our use case.

The AI receives:

- User name
- Date of birth
- Numerology dictionary
- System prompt
- User prompt

The model then generates a personalized interpretation in Vietnamese, which becomes the content of the final report.

---

## Security and Infrastructure Management

Although LunaGENZ is an academic project, security remained an important consideration throughout development.

Several AWS services were used to protect application resources:

### AWS Secrets Manager

Sensitive credentials such as webhook secrets and third-party API tokens are stored securely in AWS Secrets Manager instead of being hardcoded into the application.

### AWS Identity and Access Management (IAM)

Dedicated IAM Roles were created for each Lambda function following the principle of least privilege, ensuring that every component only accesses the resources it requires.

### Amazon Cognito

Amazon Cognito manages user authentication and authorization by issuing JWT tokens that secure the REST APIs exposed through Amazon API Gateway.

---

## Report Delivery

After Amazon Bedrock completes the AI-generated interpretation, a background Lambda function generates a PDF document containing the personalized report.

The report is then:

1. Uploaded to Amazon S3.
2. Stored securely.
3. Delivered to the user via Amazon SES.

This asynchronous workflow ensures that users receive their reports even if report generation takes several minutes.

---

## Cost Optimization

One of the primary goals of LunaGENZ was minimizing infrastructure costs.

Several AWS services contributed to this objective:

- DynamoDB On-Demand pricing eliminates unnecessary database capacity planning.
- AWS Lambda charges only for execution time.
- Amazon SQS decouples workloads without requiring dedicated servers.
- Amazon S3 stores reports with low operational cost.
- Lifecycle policies automatically archive older PDF reports into Amazon S3 Glacier.

During the testing phase, the total infrastructure cost remained close to **USD 1**, demonstrating the cost efficiency of a serverless architecture for low-volume workloads.

---

## Lessons Learned

Building LunaGENZ provided valuable experience in designing cloud-native applications with Generative AI.

Some of the most important lessons include:

- Serverless architectures significantly reduce operational overhead.
- Asynchronous processing is essential for AI workloads that exceed API timeout limits.
- Smaller language models can provide better cost-performance trade-offs than larger models for domain-specific applications.
- Infrastructure as Code and managed AWS services simplify deployment and maintenance.

Although the project successfully achieved its objectives, there are still opportunities for future improvement, including enhanced monitoring, better failure recovery for background processing, and more comprehensive cost optimization under large-scale production workloads.

---

## Conclusion

LunaGENZ demonstrates how AWS serverless technologies and Generative AI can be combined to build intelligent, scalable, and cost-effective applications.

By integrating **Amazon API Gateway**, **AWS Lambda**, **Amazon SQS**, **Amazon Bedrock**, **Amazon DynamoDB**, **Amazon S3**, and **Amazon SES**, the platform automates the entire workflow—from user request to AI-generated PDF report delivery—without requiring traditional server management.

For development teams exploring AI-native applications on AWS, LunaGENZ highlights how an event-driven serverless architecture can simplify operations while providing the flexibility needed to support future growth.