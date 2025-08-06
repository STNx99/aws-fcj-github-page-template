---
title: "Preparation"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice info %}}
In this section, you will provision all the necessary AWS resources to support a serverless deployment workflow. These include an S3 Bucket for static file hosting, a DynamoDB Table to track deployment status, Lambda functions for automation, IAM roles to manage permissions, an EventBridge event bus for triggering deployments, and an API Gateway for public HTTP access.
{{% /notice %}}

By the end of this section, your foundational infrastructure will be fully in place and ready for integration, testing, and deployment in the next stages.

---

#### Content

- [2.1 Create S3 Bucket and DynamoDB Table](2.1-createlambdafunctions/)
- [2.2 Create Lambda Functions and IAM Roles](2.2-createlambdasiamroles/)
- [2.3 Create EventBridge Event Bus and Rules](2.3-createeventbridge/)
- [2.4 Create API Gateway and Configure Endpoints & CORS](2.4-createapigateway/)
