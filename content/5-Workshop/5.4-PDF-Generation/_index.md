---
title : "PDF Generation"
date : 2026-01-01 
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### Automating PDF Reports

Once the numerology calculations are completed, the application needs to generate a beautiful, downloadable PDF report for the user.

1. **Create the PDF Generator Lambda**:
   - Create a second Lambda function named `LunaGenZ-PDFGenerator`.
   - This function will take the JSON output from the calculation Lambda, format it into an HTML template, and convert it to a PDF document using libraries like `Puppeteer` (for Node.js) or `pdfkit`.

2. **Grant Permissions**:
   - Ensure this Lambda function has permissions to write to an **Amazon S3 bucket** (e.g., `lunagenz-reports-bucket`).
   - Create an IAM Policy allowing `s3:PutObject` on this bucket and attach it to the Lambda function's Execution Role.

3. **Return the Download URL**:
   - After the PDF is generated and saved to S3, the function should generate a **Pre-signed URL**.
   - Return this Pre-signed URL back to the Frontend through the API Gateway, allowing the user to securely download their personalized numerology report.
