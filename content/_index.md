---
title : "Dewebdeploy: Deploy and host static website"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Work with Amazon System Manager - Session Manager

#### Overall
In this lab, you will build an advanced, fully serverless, event-driven deployment pipeline using AWS Elastic Beanstalk alongside supporting services such as S3, Lambda, API Gateway, EventBridge, Amplify, and DynamoDB. The workflow automates the retrieval of source code from GitHub, packaging and uploading via Lambda, and triggering deployments through EventBridge, while tracking deployment status in DynamoDB and exposing it through API Gateway endpoints.  
You will also configure S3 for static website hosting, integrate a frontend for deployment interaction, and apply secure IAM roles to follow best practices. Additionally, you will use AWS Systems Manager – Session Manager for secure, auditable EC2 access without requiring Bastion hosts or SSH.  
By completing this lab, you will gain hands-on experience in creating a production-ready deployment system that mirrors advanced Elastic Beanstalk strategies in a modern, serverless design.

![Architecture](/images/1.intro/architecture.png)

### Content
1. [Introduction](1-Introduce/)
2. [Preparation](2-Preparation/)
3. [Integration](3-Integration/)
4. [Manage S3 logs](4-s3log/)
5. [Deploy to AWS Amplify](5-deploytoamplify/)
6. [Clean up resources](6-cleanup/)