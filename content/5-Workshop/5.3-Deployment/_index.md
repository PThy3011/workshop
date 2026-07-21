---
title: "End-to-End Deployment"
date: 2026-04-18
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Deployment Guide (Step-by-step)

By utilizing the **Serverless Framework**, the complex Backend deployment process has been condensed into extremely simple operations. Anyone can easily follow along.

#### Step 1: Prepare the Backend
1. Open your Terminal (Command Prompt/PowerShell) and navigate to the backend directory:
   ```bash
   cd lunaclone/LunaGenZ/be
   ```
2. Install the necessary libraries:
   ```bash
   npm install
   ```
3. Create a `.env` file by copying the template:
   ```bash
   cp .env.example .env
   ```
4. Open the `.env` file and fill in your own information (e.g., `SES_FROM_EMAIL`, AI API key `GEMINI_API_KEY`, etc.).

#### Step 2: Deploy to AWS
Ensure you have a valid AWS CLI configuration (`aws configure`), then run the magic command:
```bash
serverless deploy
```
- The tool will automatically package the source code and create a CloudFormation Stack.
- It automatically creates the DynamoDB tables (`lunagenz-users`, `lunagenz-numerology`, `lunagenz-lenormand`).
- Automatically creates the S3 Bucket.
- Deploys the respective Lambda functions and API Gateway.
- *Output:* At the end of the terminal, you will see a list of **Endpoints (URLs)**. Copy that URL.

#### Step 3: Deploy the Frontend
1. Navigate to the frontend directory:
   ```bash
   cd ../fe
   ```
2. Open the `.env` file (if any) or directly edit the config code to update the **API Gateway URL** obtained in Step 2.
3. Push the Frontend code to GitHub.
4. Access **AWS Amplify** on the console, select **Host web app**, and connect to your GitHub repository.
5. Click **Save and Deploy**. The Amplify system will automatically build the Next.js app and provide you with a live website link.
