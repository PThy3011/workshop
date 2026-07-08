---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{}

# Building LunaGENZ – A Personalized Numerology System on AWS Serverless Architecture with Generative AI

After weeks of learning and hard work, our team has completed our final project: **LunaGENZ** – an AI-powered system that provides personalized Numerology readings.

This blog post is not just to showcase our work, but to document our architectural decisions, challenges we faced, and lessons learned. We hope this will be helpful for other students or developers working on similar Serverless + GenAI projects.

---

## 1. Why We Chose Serverless Architecture

Our main goals were to **minimize infrastructure management** and **keep costs as low as possible** for a student project with no stable revenue. Therefore, we decided to go fully Serverless:

- **Frontend**: Next.js deployed with **AWS Amplify**
- **Backend**: **API Gateway** + **AWS Lambda**
- **Database**: **Amazon DynamoDB** (On-demand mode)

The pay-as-you-go pricing model kept our infrastructure costs almost zero during development and testing. This architecture perfectly matched our current needs and budget.

---

## 2. Solving Timeout Issues with Amazon SQS

One of the biggest challenges we faced early on was **API Gateway timeout** (limited to 29 seconds). Generating AI content and exporting PDFs took longer than this limit, causing frequent failures.

**Our Solution**: Implement asynchronous processing using **Amazon SQS**.

- When a user submits a request, the API Lambda only pushes a message to the SQS queue and immediately returns “Processing...” to the user.
- A separate worker Lambda (triggered by SQS) picks up the message, calls the Generative AI model, generates the reading, creates a PDF, and sends the result via **Amazon SES** to the user’s email.

This approach completely eliminated timeout errors, improved user experience, and made the system more resilient.

---

## 3. Choosing the Right AI Model

We selected **Claude 3 Haiku** via **Amazon Bedrock** instead of larger models. Reasons:

- Our use case (Numerology interpretation in Vietnamese) does not require extremely complex reasoning.
- Haiku offers faster response times and significantly lower cost.
- With well-engineered prompts, the output quality remains excellent for our needs.

---

## 4. Security, Payment, and CI/CD

- Separated the **payment flow** into an independent Webhook Handler for better security.
- Stored all sensitive keys and credentials in **AWS Secrets Manager**.
- Fully automated deployment of both frontend and backend using **GitLab CI/CD**.
- Monitoring, logging, and performance tracking are handled by **Amazon CloudWatch**.

---

## Lessons Learned

This was our first time building a relatively complete Serverless system, so there are still areas for improvement:

- Error handling and retry logic for background Lambda workers need enhancement.
- Cost control mechanisms when scaling to real traffic are not yet fully tested.
- User experience for asynchronous processes (e.g., status polling or WebSocket notifications) can be improved.

Despite these challenges, the project gave us valuable hands-on experience with real-world Serverless design and Generative AI integration.

---

## Conclusion

**LunaGENZ** proves that with AWS Serverless services — such as Amplify, Lambda, API Gateway, SQS, Bedrock, and DynamoDB — students and individual developers can build practical, production-ready applications without high upfront costs.

We are very open to feedback from the community to further improve LunaGENZ.

Thank you for reading!

---