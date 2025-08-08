---
title: "Create Lambda Functions and IAM Roles"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

In this step, you will create two **Lambda functions** that form the foundation of your automated deployment pipeline:

- `upload-function`: Clones source code from GitHub and uploads it to S3, then triggers an EventBridge event.
- `deploy-function`: Handles the actual deployment process (e.g., updating environments, modifying states, writing to DynamoDB).

You will also create and configure the **IAM roles** that allow these Lambda functions to interact with AWS services securely.

---

### Content

- [2.2.1 Create Upload Lambda Function](2.2.1-createlambdaupload/)
- [2.2.2 Create Deploy Lambda Function](2.2.2-createlambdadeploy/)