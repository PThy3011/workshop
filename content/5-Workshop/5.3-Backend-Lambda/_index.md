---
title : "Backend (Lambda)"
date : 2026-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Deploying the Numerology Backend

The core functionality of LunaGenZ involves calculating numerology indicators (e.g., Life Path Number, Destiny Number, Soul Urge Number) based on user input (Name and Date of Birth).

To deploy this Serverless backend:

1. **Create an AWS Lambda Function**:
   - Go to the AWS Management Console and open the Lambda service.
   - Click **Create function**, choose "Author from scratch".
   - Name it `LunaGenZ-Calculation`.
   - Select the appropriate runtime (e.g., Node.js 20.x or Python 3.12).

2. **Upload the Source Code**:
   - Compress your calculation logic code into a `.zip` file.
   - Upload it to the Lambda function.

3. **Configure API Gateway**:
   - To make this Lambda function accessible to the Frontend, you must set up an API Gateway.
   - Create a new REST API or HTTP API.
   - Add a POST method and link it to your `LunaGenZ-Calculation` Lambda function.
   - Enable **CORS** so your Frontend can make requests to this API without cross-origin issues.
   - Deploy the API to a stage (e.g., `prod`) and copy the **Invoke URL**.
