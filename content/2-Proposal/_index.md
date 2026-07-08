---
title: "Proposal"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# LunaGenZ - Serverless Numerology Web Application
## Automated Numerology Application System on AWS Serverless Platform

### 1. Project Overview
LunaGenZ is a Numerology application platform built for young audiences, allowing users to look up personalized metrics based on their date of birth and full name. The system automatically generates a detailed report in PDF format and sends it directly via email to the user.

To ensure flexibility, stability, and cost optimization for the MVP (Minimum Viable Product) phase, the platform adopts a **100% AWS Serverless** architecture and utilizes a powerful internal PDF generation technology instead of relying on third-party Generative AI services.

### 2. Problem Statement & Solution
#### Current Problem
There are many fortune-telling and numerology applications in the current market, but most require users to pay upfront or feature a design that is not friendly to the young customer base (Gen Z). Initially, the team planned to use Generative AI (such as Amazon Bedrock) to generate personalized reports. However, integrating LLMs (Large Language Models) poses risks of uncontrollable costs for an MVP project and increases latency during report generation.

#### Technical Solution (Fallback Strategy)
LunaGenZ decided to pivot to building a robust internal PDF generation system (Internal PDF Generation). This solution uses an entirely Serverless Event-Driven architecture:
- **Frontend (Next.js)** is fully hosted on AWS Amplify.
- **Amazon API Gateway** and **AWS Lambda (Node.js)** handle the numerology calculation logic and PDF initialization.
- **Amazon DynamoDB** stores request information and metadata.
- **Amazon S3** stores the static PDF report files after they are generated.
- **Amazon SES** automatically sends an email with the report attached to the user's inbox.

### 3. Benefits and ROI
The strategy of using an internal PDF generator provides a highly stable system (zero cost for third-party AI API calls), fast response times, and 100% control over the output report format. The Serverless architecture allows the system to handle heavy loads, automatically scaling when there is a large number of simultaneous lookups (e.g., during a TikTok trend), while keeping the initial infrastructure cost close to $0 by effectively leveraging the Free Tier.

### 4. Solution Architecture

#### AWS Services Used
- **AWS Amplify:** Hosting for the Next.js web app with automated CI/CD features, allowing rapid deployment of new Frontend versions.
- **Amazon API Gateway:** Acts as the gateway receiving HTTP requests from the Frontend.
- **AWS Lambda:** Runs logic processing functions (Node.js) that calculate numerology numbers, render the PDF file, and trigger the email workflow.
- **Amazon DynamoDB:** High-speed NoSQL database storing customer lookup history.
- **Amazon S3:** Ideal Object Storage for securely storing static PDF report files after export.
- **Amazon SES (Simple Email Service):** Automated email service quickly attaching PDF reports for customers.

#### Workflow
1. The customer enters their **Full Name** and **Date of Birth** on the Next.js interface.
2. The Frontend calls the API pushing data through **Amazon API Gateway**.
3. **AWS Lambda Function** receives the request, calculates personal metrics, and calls the PDF library to render the report.
4. The request payload is recorded in **Amazon DynamoDB**.
5. The successfully generated PDF file is directly pushed to the **Amazon S3 Bucket**.
6. Lambda calls **Amazon SES** to schedule and send an email containing the report to the user.

### 5. Budget Estimation & Costs
Since the system is structured 100% on Serverless, the monthly maintenance budget in the first year (MVP phase) is extremely low thanks to leveraging the AWS Free Tier:
- **AWS Lambda:** Up to 1 million requests/month ($0)
- **Amazon API Gateway:** 1 million REST API calls/month ($0)
- **Amazon DynamoDB:** 25GB storage, 25 WCU/RCU ($0)
- **Amazon S3:** 5GB Standard storage ($0)
- **Amazon SES:** 62,000 emails/month (if requested from EC2/Lambda) ($0)
- **AWS Amplify:** 1000 build minutes/month, 5GB storage ($0)

**Estimated total cost:** ~$0/month in the initial phase (MVP capacity proving phase).

### 6. Risk Assessment
- **Risk 1:** Amazon SES email sending trust is limited in Sandbox mode.
  - *Mitigation:* Submit a request to AWS Support to exit Sandbox mode and verify the Domain before officially launching the system to the public.
- **Risk 2:** "Cold Start" issue of AWS Lambda when there are no users for a long time, slowing down PDF export speed.
  - *Mitigation:* Optimize Node.js code, use lightweight PDF generation libraries, and set Provisioned Concurrency if necessary during the scaling phase.