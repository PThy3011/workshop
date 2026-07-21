---
title: "Project Proposal"
date: 2026-04-18
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# LunaGenZ - Serverless Numerology Web Application

Link website: https://www.lunagenz.sbs/

### 1. Project Overview
LunaGenZ is a Numerology & Lenormand application platform built for young people, allowing users to look up personalized metrics based on their date of birth and full name. It can also be used to check metrics for friends, relatives, or even romantic interests and crushes. The system automatically generates a detailed report in PDF format and sends it directly via email to the user.
The project is built on a **100% AWS Serverless** architecture to ensure flexibility, automatic scalability, and cost optimization.

### 2. Objectives
- **Desired Output:** A fully functional website that allows users to input their information, after which the system generates a PDF numerology report and emails it.
- **Success Criteria:** The system operates smoothly end-to-end (from frontend to backend), scales automatically during high traffic, and maintains minimal monthly maintenance costs (leveraging the Free Tier).

### 3. Problem to Solve
The current market has many fortune-telling and numerology applications, but most require upfront payment or have designs that are not youth-friendly (Gen Z). Integrating Generative AI poses uncontrollable cost risks for an MVP project and increases latency when generating reports. LunaGenZ solves this problem by using a fast, free, and stable internal PDF generation system based on Serverless architecture.

### 4. Solution Architecture
- **AWS Amplify:** Hosting for the Next.js web application with automatic CI/CD.
- **Amazon API Gateway:** Acts as the gateway receiving HTTP requests from the Frontend.
- **AWS Lambda:** Runs the numerology calculation logic, renders the PDF file, and triggers the email sending process.
- **Amazon DynamoDB:** Stores customer lookup history.
- **Amazon S3:** Safely stores the exported PDF report files.
- **Amazon SES:** Automatically sends emails with the attached reports.

### 5. Timeline
- **Weeks 1 - 5:** Learn AWS architecture, participate in onboarding, set up accounts, practice basic services (VPC, EC2, IAM, S3).
- **Weeks 6 - 8:** Advanced research on CloudFront, RDS, AutoScaling, and CloudWatch.
- **Weeks 9 - 10:** Start developing the LunaGenZ project, delegate tasks, write Frontend (Next.js) and Backend (Node.js) code.
- **Week 11:** Finalize integration, test end-to-end flow, and officially deploy to AWS infrastructure.
- **Week 12:** Write internship reports, build workshop documentation.

### 6. Estimated Budget (MVP Phase)

The system is designed entirely on a **Serverless** architecture, which thoroughly optimizes infrastructure costs. By avoiding the use of 24/7 running servers (such as EC2), the project completely eliminates idle costs.

During the MVP (Minimum Viable Product) phase, the entire processing flow is designed to fit well within the limits of the **AWS Free Tier**. Below is a detailed breakdown of resource usage:

| AWS Service | Role in Architecture | AWS Free Tier Limit (Monthly) | Estimated Cost |
| :--- | :--- | :--- | :--- |
| **AWS Amplify** | Hosting and automated Frontend deployment | 1,000 build minutes, 5GB storage, 15GB bandwidth | **$0** |
| **Amazon API Gateway** | API routing gateway (REST/HTTP API) | 1,000,000 Requests | **$0** |
| **AWS Lambda** | Computing environment (Logic & Report) | 1,000,000 requests & 400,000 GB-seconds compute | **$0** |
| **Amazon DynamoDB** | Database storing user history and IP | 25GB storage, 25 WCU & 25 RCU | **$0** |
| **Amazon S3** | Storage for PDF/JSON result documents | 5GB standard storage, 20,000 GET requests | **$0** |
| **Amazon SES** | Automated notification Email system | 3,000 emails (12-month free tier) | **$0** |

**Total Estimated Cost: ~$0/month**

### 7. Risks
- **Risk 1:** Amazon SES email sending limit due to the account being in Sandbox mode.
  - *Solution:* Submit a ticket to AWS Support to request removal from the Sandbox. Meanwhile, use Google's Nodemailer as a fallback. Implement a try-catch block to use SES if approved; otherwise, it will automatically fall back to Nodemailer.
- **Risk 2:** AWS Lambda "Cold Start" issue when the system has no requests for a long period.
  - *Solution:* Optimize code and use lightweight PDF generation libraries to minimize initialization time.
- **Risk 3:** The AWS account has not been permitted to use the AWS Bedrock service, or a support ticket was written but has not yet been approved.
  - *Solution:* Use external AI APIs as a fallback instead of Bedrock while waiting for permission approval.
