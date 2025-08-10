---
title: "Introduce"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

This guide walks you through building an advanced deployment pipeline using **AWS Elastic Beanstalk** with supporting services such as **S3**, **Lambda**, **API Gateway**, **EventBridge**, **Amplify** and **DynamoDB**. The goal is to simulate a fully serverless, event-driven deployment workflow where deployment artifacts are uploaded and automatically deployed, with deployment status tracked and accessible via API.

Unlike basic Elastic Beanstalk workflows that rely on ZIP upload through the console or CLI, this guide enables:

- Automated source code retrieval from GitHub
- Upload and packaging through Lambda
- Trigger-based deployments via EventBridge
- Status tracking with DynamoDB
- Frontend integration using API Gateway (HTTP API)

To support secure infrastructure management, we also leverage **Session Manager** — an AWS Systems Manager feature — for secure, auditable instance access **without the need for Bastion hosts or SSH**. This helps ensure best practices in environments that may still include EC2 resources or require manual intervention.

#### Key Features of This Architecture
  ![Architecture](/images/1.intro/architecture.png)
- **Fully automated deployment flow** using event-driven architecture
- **Modular Lambda functions** to handle upload and deployment logic
- **API Gateway endpoints** for invoking deployments and checking status
- **S3 static website hosting** for serving deployed frontend content
- **DynamoDB tracking** for deployment metadata
- **Secure IAM roles** with scoped permissions
- **Frontend integration** for user interaction with the deployment system

By the end of this tutorial, you will have a working deployment system that mirrors key patterns used in **Elastic Beanstalk Advanced Deployment Strategies**, adapted into a modern, serverless design suitable for both production and experimentation.

---
