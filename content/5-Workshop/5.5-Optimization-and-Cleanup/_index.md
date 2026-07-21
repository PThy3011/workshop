---
title: "Optimization & Cleanup"
date: 2026-04-18
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### 1. Optimization of the Lab Process
Instead of manually configuring dozens of services—which is time-consuming and error-prone—the **Serverless Framework** optimizes the entire application lifecycle.
- **Environment variable management:** Values like the Bucket Name (`PDF_BUCKET_NAME`) and API keys are dynamically and safely referenced from the `.env` file directly into Lambda without manual entry on the Console.
- **Automated IAM permissions:** The `iam.role.statements` block in the `serverless.yml` file helps automatically generate the strictest security rules (principle of least privilege) without the practitioner needing deep IAM knowledge.

### 2. System Clean-up
One of the biggest nightmares when practicing Cloud is forgetting to turn off services, leading to financial loss. This Lab helps you clean up incredibly easily and with absolute safety.

1. **Backend Clean-up (Crucially Important):**
   - Open Terminal in the `lunaclone/LunaGenZ/be` directory.
   - First, make sure your **S3 Bucket** is emptied. The CloudFormation deletion process will not allow deleting a bucket if it still contains files. Go to AWS Console > S3 > Select the report Bucket > Click **Empty**.
   - After emptying S3, run the following command in the Terminal:
     ```bash
     serverless remove
     ```
   - Wait a few minutes. This tool will automatically go to AWS and **cleanly delete everything** it created: Lambda functions, API Gateway, DynamoDB tables, and even the S3 Bucket. Leaving behind no resource "trash."
   
2. **Frontend Clean-up:**
   - Access **AWS Amplify**.
   - Select the app you just deployed, navigate to the `App settings` > `General` tab and click **Delete app**.

With just 2 simple steps, your account is completely swept clean back to its original state, eliminating the risk of unwanted incurred costs!
