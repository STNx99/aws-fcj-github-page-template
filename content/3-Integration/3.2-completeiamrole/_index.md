---
title: "Set Up Complete IAM Access (Lambda Permissions)"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 3.2 </b> "
---

In this step, you will ensure that both Lambda functions have the correct IAM permissions to interact with AWS services such as **S3**, **DynamoDB**, and **EventBridge**.

---

#### IAM Role for `upload-function`

This function needs access to:
- Upload files to the S3 bucket
- Write deployment status to DynamoDB
- Publish events to EventBridge

##### Attach the following managed policies:
- `AmazonDynamoDBFullAccess`
- `AmazonDynamoDBFullAccess_v2` (optional)
- `AmazonEventBridgeFullAccess`

##### Add the following inline policy for scoped S3 access:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::awsdeplybucket12345/*"
    }
  ]
}
```
#### Instructions:
  1. Go to the IAM Console – Roles
  2. Find the role attached to the upload-function
  3. Click Add permissions → Attach policies
  4. Select the managed policies listed above
  5. Add the inline policy shown above to restrict S3 access

---

#### IAM Role for deploy-function
This function needs access to:
  - Read deployment package from S3
  - Update deployment status in DynamoDB

#### Attach the following managed policies:
  - AmazonS3FullAccess
  - AmazonDynamoDBFullAccess
  - AmazonDynamoDBFullAccess_v2 (optional)

#### Instructions:
  1. Go to the IAM Console – Roles
  2. Find the role attached to the deploy-function
  3. Click Add permissions → Attach policies
  4. Select the listed managed policies

> Note: No inline policy is required unless you want to restrict access to specific resources.

---

#### Final IAM Role Review
Make sure that:
  - Each Lambda function is associated with the correct IAM role
  - No excessive permissions are granted (principle of least privilege)
  - The role includes the AWSLambdaBasicExecutionRole for CloudWatch logging

---

#### Expected Result
After completing this step, both Lambda functions will have the necessary permissions to:
  - Upload and retrieve objects from S3
  - Read and write to DynamoDB
  - Publish and receive events from EventBridge
  - Send logs to CloudWatch

---

#### Next Step
Continue to [Test API Gateway and Lambda Integration](../3.3-testapigateway/)