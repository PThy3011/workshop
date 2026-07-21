---
title: "Architecture Design"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

### 1. Architecture Diagram

![Architecture Diagram](/images/5-Workshop/architecture.png)

This is architecture diagram for LunaGenZ project.

### 2. Core AWS Services
This sample system uses a 100% Serverless architecture which is very beginner-friendly:
- **AWS Amplify:** Hosting to run the static user interface (Frontend Next.js/React).
- **Amazon API Gateway (HTTP API):** An ultra-fast, low-cost gateway to route requests.
- **AWS Lambda:** The backend code execution environment (Node.js) tasked with calling AI APIs, calculating numbers, and generating PDFs.
- **Amazon DynamoDB:** Non-relational database (NoSQL) tables used to store user information (`UsersTable`, `NumerologyTable`, `LenormandTable`).
- **Amazon S3:** A bucket to store the resulting PDF files (`PdfBucket`).

### 3. Why choose this structure for the Lab?
- **Extremely fast deployment:** Instead of manually clicking through each service on the AWS Console, the `serverless.yml` file defines and automates the entire creation of Lambda, IAM permissions, DynamoDB tables, and S3 Buckets.
- **No fear of forgetting to delete resources:** AWS beginners often forget to delete services, leading to unexpected charges. With the Serverless Framework, everything is managed collectively via CloudFormation; just a `remove` command cleans up 100%.
- **Zero Cost:** All services in the lab generously support the Free Tier. Without heavy traffic, you will not incur a single dime of cost.
