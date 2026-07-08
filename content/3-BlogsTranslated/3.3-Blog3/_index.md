---
title: "Blog 1"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# Building a Numerology System (LunaGENZ) on a Serverless AWS Architecture with GenAI

Hi everyone, after a while of self-study and grinding, our team has started our capstone project: LunaGENZ – a system that uses AI to generate personalized numerology readings.

I'm writing this post not to show off, but to record our architectural decision-making process, along with the mistakes we ran into – hoping it helps anyone working on a similar project, and we'd really appreciate feedback from more experienced folks so the team can keep learning.

## 1. Why We Chose a Serverless Architecture

Our initial goal was to avoid managing servers ourselves, while keeping costs appropriate for a student project without stable revenue. The team chose:

- Frontend: Next.js, deployed via AWS Amplify
- Backend: API Gateway + AWS Lambda
- Database: Amazon DynamoDB (On-demand mode)

The pay-per-use model kept infrastructure costs very low during the testing phase, which fit a product with no real users yet. This works well for the team's specific situation at this stage, not as a general conclusion for every project — as traffic grows, the serverless model comes with its own cost trade-offs that the team is still learning about.

## 2. The Timeout Problem and How We Solved It with Amazon SQS

Initially, the system called the AI to generate content and export PDFs within the same request. Since these steps took a long time, the system kept hitting timeout errors due to API Gateway's 29-second limit.

How the team fixed it: we decoupled the processing flow using Amazon SQS. A user request just pushes a message into the queue and returns a "processing" response. A separate background Lambda pulls the message, calls the AI, generates the PDF, and then sends it to the user's email via Amazon SES. This eliminated the timeouts and reduced the risk of data loss when errors occur during processing.

## 3. Choosing the AI Model

The team used Claude 3 Haiku via Amazon Bedrock instead of larger models. The reasoning is that our Vietnamese-text interpretation task doesn't require overly complex reasoning, so a smaller model with faster responses and lower cost was a more sensible choice than using the most powerful model available.

## 4. Security and CI/CD

- The payment flow was separated into its own Webhook Handler, independent from the AI interpretation logic.
- Sensitive keys are stored in AWS Secrets Manager, not hardcoded in the code.
- The entire frontend and backend are automatically deployed via GitLab CI/CD. Errors and performance are monitored with CloudWatch.

## A Few Things the Team Learned

This is the first time our team has applied a serverless architecture at a fairly complete scale, so there are certainly things that aren't optimized yet – for example, handling errors when the background-processing Lambda fails, or controlling costs at real scale, are problems the team hasn't tested at a large scale yet.

Since this is also our first project involving external users, we're sure there are plenty of mistakes we haven't caught. We'd love for more experienced folks to share feedback so we can improve. Thank you all for taking the time to read this post.
