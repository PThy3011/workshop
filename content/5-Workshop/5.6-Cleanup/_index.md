---
title : "Clean up"
date : 2026-01-01 
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Cleaning Up Resources

To avoid incurring unwanted charges on your AWS account, it is crucial to delete the resources you created during this workshop.

1. **Delete S3 Buckets**:
   - Empty and delete the `lunagenz-reports-bucket`.
   - Empty and delete the `lunagenz-frontend-web` bucket.
2. **Delete CloudFront Distribution**:
   - Disable the CloudFront distribution first (this may take a few minutes).
   - Once disabled, select it and click Delete.
3. **Delete API Gateway**:
   - Go to the API Gateway console.
   - Select your LunaGenZ API and choose Delete.
4. **Delete Lambda Functions**:
   - Delete `LunaGenZ-Calculation` and `LunaGenZ-PDFGenerator` functions.
5. **Delete IAM Roles and Policies**:
   - Navigate to the IAM console and delete any custom Roles and Policies created for this workshop.