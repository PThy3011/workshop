---
title : "Frontend Hosting"
date : 2026-01-01 
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### Hosting the Frontend on AWS

To make the LunaGenZ application accessible to users worldwide with low latency and high availability, we will host the static frontend files using Amazon S3 and distribute them via Amazon CloudFront.

1. **Create an S3 Bucket**:
   - Create a new S3 bucket (e.g., `lunagenz-frontend-web`).
   - Enable **Static website hosting** in the bucket properties.
   - Upload your HTML, CSS, and JS files to the bucket.

2. **Configure Amazon CloudFront**:
   - Create a new CloudFront distribution.
   - Set the Origin Domain to your S3 bucket's website endpoint.
   - Enable **Origin Access Control (OAC)** to restrict direct public access to your S3 bucket, ensuring users only access the site through CloudFront.
   - Wait for the distribution to deploy.

3. **Connect Frontend to Backend**:
   - Make sure your Frontend JavaScript code is configured to send requests to the API Gateway **Invoke URL** you created in step 5.3.
   - Once deployed, you can access your LunaGenZ application using the CloudFront domain name (e.g., `d123456abcdef8.cloudfront.net`).
