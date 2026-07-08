---
title : "Overview"
date : 2026-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Introduction to LunaGenZ

**LunaGenZ** is an innovative Numerology application designed to calculate and generate comprehensive personal numerology reports. To ensure high availability, scalability, and cost-effectiveness, the entire application is built on a Serverless architecture on AWS.

#### Architecture Overview

In this workshop, you will deploy the following components:
1. **Frontend (Amazon S3 & CloudFront)**: The static user interface built with HTML/CSS/JS (or a framework like React/Vue). It's hosted on S3 and distributed globally via CloudFront.
2. **Backend (Amazon API Gateway & AWS Lambda)**: The core calculation logic for numerology is handled by AWS Lambda functions, which are triggered securely via API Gateway.
3. **PDF Generation (AWS Lambda)**: A dedicated Serverless function that automatically compiles the calculated numerology results into a downloadable PDF report.

#### What you will build

By the end of this workshop, you will have a fully functioning Serverless application deployed on AWS, complete with a frontend interface, backend calculation logic, and automated PDF reporting capabilities. Let's get started!
