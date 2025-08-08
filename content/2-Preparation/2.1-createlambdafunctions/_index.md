---
title: "Create S3 Bucket and DynamoDB Table"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

In this step, you will prepare the storage and database services that support the serverless deployment workflow.

Specifically, you will:
- Create an **S3 bucket** (`awsdeplybucket1234`) to store deployment packages  
- Create a **DynamoDB table** with `id` as the partition key to track deployment statuses

These resources are the foundation for the Lambda functions and event-driven pipeline that will be configured in the next steps.

---

### Content

- [2.1.1 Create S3 bucket](2.1.1-creates3bucket/)
- [2.1.2 Create DynamoDB table](2.1.2-createdynamodb/)