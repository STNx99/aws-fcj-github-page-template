---
title: "Clean Up Resources"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 6 </b> "
---

In this final step, you will learn how to properly clean up all the AWS resources created during this lab. This ensures you do not incur unexpected charges and keep your AWS environment tidy.

#### Cleanup Overview

The cleanup process includes:

- Deleting all Lambda functions created for upload and deployment.
- Removing the S3 bucket and DynamoDB table used for storing deployment files and tracking status.
- Deleting the EventBridge event bus and associated rules.
- Removing API Gateway and all related resources.
- Deleting the AWS Amplify application if it was used for frontend deployment.

Make sure to carefully follow each sub-step to avoid leaving behind unused resources.

After completing the deployment and integration steps, it’s essential to clean up your AWS resources to avoid unnecessary charges and keep your environment tidy.\

---

#### Content  
[6.1 Delete Lambda Functions](6.1-deletelambdafunctions/)  
[6.2 Delete S3 Bucket and DynamoDB Table](6.2-deletes3dynamodb/)  
[6.3 Delete EventBridge Bus and Rules](6.3-deleteeventbridge/)  
[6.4 Delete API Gateway and Related Resources](6.4-deleteapigateway/)  
[6.5 Delete AWS Amplify Application](6.5-deleteamplify/)