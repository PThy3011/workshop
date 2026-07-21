---
title: "Testing & Monitoring"
date: 2026-04-18
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### 1. Functional Testing
After the Backend and Frontend are successfully deployed:
1. Open the website link provided by AWS Amplify.
2. Enter a test input (Full Name, Date of Birth) and select the report generation function.
3. Wait for processing and check your Email inbox (or spam folder) to see if you received the PDF report file.

### 2. Checking System Logs
If an error occurs, debugging with the Serverless Framework is very easy:
- **View logs directly in Terminal:** You can pull logs directly from AWS to your local machine using the command:
  ```bash
  serverless logs -f numerology -t
  ```
  *(Replace `numerology` with the function name in the `serverless.yml` file)*
- **View via CloudWatch:** Navigate to AWS Console > **CloudWatch** > **Log groups**. You will see log streams recording the details of each Lambda function execution step, AI API response times, and PDF generation status.

### 3. Basic Monitoring (Metrics)
- Access the **AWS Lambda** console and switch to the **Monitor** tab.
- Here, AWS provides highly intuitive basic monitoring charts out of the box:
  - **Invocations:** The number of times the function is called.
  - **Duration:** The average time it takes to process a request.
  - **Error count:** Statistics if the code crashes or encounters external API connection errors.
