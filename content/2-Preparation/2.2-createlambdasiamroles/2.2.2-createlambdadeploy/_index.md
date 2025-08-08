---
title: "Create Deploy Lambda Function"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2.2 </b> "
---

In this step, you will create the **Deploy Lambda Function**.

This function is triggered by **EventBridge** once the upload process is complete. It will simulate or execute deployment logic such as reading from S3, updating status in DynamoDB, or starting other automation workflows.

---

#### Create Lambda Function

1. Go to the [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)
2. Click **Create function**

   ![Create Lambda](/images/2.preparation/001-createlambdadeploy.png)

3. In the configuration form, enter:
   - **Function name**: `deploy-function`  
   - **Runtime**: `Node.js 22.x`  
   - **Permissions**: Select `Create a new role with basic Lambda permissions`

   ![Create Deploy Function](/images/2.preparation/002-createlambdadeploy.png)
   ![Click Permissions](/images/2.preparation/003-createlambdadeploy.png)

4. Click **Create function**

   ![Click Create funtion](/images/2.preparation/004-createlambdadeploy.png)

---

#### Configure Basic Settings

1. After the function is created, go to the **Configuration** tab

   ![Go to the Configuration](/images/2.preparation/005-createlambdadeploy.png)

2. In the **General configuration** section, click **Edit** and update:
   - **Timeout**: `2 minutes`  
   - **Memory**: `1024 MB`

   ![Go to the Configuration](/images/2.preparation/006-createlambdadeploy.png)
   ![Edit Timeout and Memory](/images/2.preparation/007-createlambdadeploy.png)

3. Click **Save**

   ![Click Add](/images/2.preparation/008-createlambdadeploy.png)

---

#### Attach IAM Permissions

To allow the `deploy-function` to access DynamoDB and S3, attach the following permissions:
1. Go to the **Permissions** tab of the function
2. Click on the role name to open the IAM Console

   ![Go to the Permissions](/images/2.preparation/009-createlambdadeploy.png)

3. Click **Add permissions** and choose **Attach policy**

   ![Add permissions](/images/2.preparation/010-createlambdadeploy.png)

4. Attach the following AWS managed policies:
   - `AmazonDynamoDBFullAccess`
   - `AmazonS3FullAccess`
   - *(Optional)* `AmazonDynamoDBFullAccess_v2`

5. Click **Add permissions**

   ![Attach Deploy Policies](/images/2.preparation/011-createlambdadeploy.png)

> Note: You do not need to create an inline policy for S3 unless you want to restrict access to specific bucket paths.

---

#### Next Step

Continue to [Create EventBridge Rule](../../2.3-createeventbridge/)
