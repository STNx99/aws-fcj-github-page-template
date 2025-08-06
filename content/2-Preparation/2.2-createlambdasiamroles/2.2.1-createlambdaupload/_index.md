---
title: "Create Upload Lambda Function"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.2.1 </b> "
---

In this step, you will create the **Upload Lambda Function**.

This function is responsible for:
- Cloning a GitHub repository
- Packaging the source code into a ZIP file
- Uploading it to an S3 bucket (`awsdeplybucket12345`)
- Publishing an EventBridge event (`DeploymentUploaded`) to trigger the deployment process

---

#### Create Lambda Function

1. Go to the [AWS Lambda Console](https://console.aws.amazon.com/lambda/home)

2. Click **Create function**

   ![Create Lambda Function](/images/2.preparation/001-createuploadlambda.png)

3. In the configuration form, enter:

   - **Function name**: `upload-function`  
   - **Runtime**: `Node.js 22.x`  
   - **Permissions**: Select `Create a new role with basic Lambda permissions`

   ![Create Lambda Function](/images/2.preparation/002-createuploadlambda.png)

4. Click **Create function**

   ![Create Lambda Function](/images/2.preparation/003-createuploadlambda.png)

---

#### Configure Basic Settings

1. After the function is created, go to the **Configuration** tab

   ![Click Configuration](/images/2.preparation/004-createuploadlambda.png)

2. In the **General configuration** section, click **Edit** and update:

   - **Timeout**: `2 minutes`  
   - *(Optional)* **Memory**: `1024 MB` (recommended for handling larger Git repos)

   ![Click Edit](/images/2.preparation/005-createuploadlambda.png)
   ![Edit Timeout and Memory](/images/2.preparation/006-createuploadlambda.png)

3. Click **Save**

   ![Click Save](/images/2.preparation/007-createuploadlambda.png)

---

#### Add Git Layer

1. Scroll down to **Layers** section, click **Add a layer**

   ![Add a layer](/images/2.preparation/001-addgitlayer.png)

2. Choose:
   - **Specify an ARN**
   - Paste this ARN:
     ```
     arn:aws:lambda:ap-southeast-1:553035198032:layer:git-lambda2:8
     ```

   ![Paste ARN](/images/2.preparation/002-addgitlayer.png)

3. Click **Add**

   ![Click Add](/images/2.preparation/003-addgitlayer.png)

---

#### Attach IAM Policies

1. Go to the **Permissions** tab of the function

2. Click on the role name to open the IAM console

   ![Click on the role name](/images/2.preparation/008-createuploadlambda.png)

3. Attach the following AWS managed policies:
   - `AmazonS3FullAccess`
   - `AmazonDynamoDBFullAccess`
   - `AmazonEventBridgeFullAccess`

   ![Add Attach](/images/2.preparation/009-createuploadlambda.png)
   ![Choose Attach](/images/2.preparation/010-createuploadlambda.png)

4. Add a custom inline policy to allow uploading to the S3 bucket:

   - In the role page, click **Add permissions** then click **Create inline policy**

   ![Create inline policy](/images/2.preparation/011-createuploadlambda.png)

   - At Select a service, click **choose a service**

   ![Click choose a service](/images/2.preparation/012-createuploadlambda.png)

   - Select **S3**

   ![Select S3](/images/2.preparation/013-createuploadlambda.png)

   - Copy this json:

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
   - In the Create policy screen, switch to the **JSON tab** and **paste the following JSON**:

   ![Paste the following JSON](/images/2.preparation/014-createuploadlambda.png)

   - Click **Next**

   ![Click Next](/images/2.preparation/015-createuploadlambda.png)

   - Enter `upload` for policy name and click **Create Policy**

   ![Create policy](/images/2.preparation/016-createuploadlambda.png)

---

#### Next Step
Continue to [Create Deploy Lambda Function](../2.2.2-createlambdadeploy/)