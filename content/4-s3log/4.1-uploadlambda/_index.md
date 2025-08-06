---
title: "Upload Source Code via Lambda Upload"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

In this step, you will test the **Lambda Upload function** which is responsible for downloading the source code from GitHub, uploading it to S3, and triggering an event to EventBridge to begin the deployment process.

This Lambda function should already be created and configured with:
- GitHub integration via a Lambda Layer
- Permissions to access S3, DynamoDB, and EventBridge
- A timeout of 2 minutes

---

#### Invoke Upload Lambda Function

There are two ways to trigger the upload Lambda: via the Lambda Console or through API Gateway (which you will configure later). In this step, we will manually test it in the AWS Console.

1. Go to the [Lambda Console](https://console.aws.amazon.com/lambda/)

2. Select the function named `upload`  
   You should see your Lambda configuration including environment variables, layers, and permissions.

   ![](/images/4.test/001-lambda-upload.png)

3. Click on the **Test** tab

   ![](/images/4.test/002-lambda-test.png)

4. Create a new test event with the following JSON input (replace the repo info accordingly):

  ```json
   {
     "repository": "https://github.com/your-username/your-repo",
     "branch": "main"
   }
  ```

5. Click Test to invoke the Lambda function

6. If successful, you will see:

  - The source code downloaded from GitHub

  - Files uploaded to your S3 bucket (awsdeplybucket12345)

  - A custom event sent to EventBridge with source dewebdeploy.upload

---

#### Verify Upload in S3

- Go to [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
- Open the bucket `awsdeplybucket12345`
- You should see the uploaded source code or zipped deployment files in the root directory or inside a folder, depending on your Lambda logic

  ![](/images/4.test/005-s3-files.png)

---

#### Verify EventBridge Event

- Go to [Amazon EventBridge Console](https://console.aws.amazon.com/events/)
- Choose **Event Buses**, then select the custom event bus named `upload`
- Navigate to **Monitoring** and click **View metrics in CloudWatch**
- You should see invocation metrics if the event was sent successfully

  ![](/images/4.test/006-eventbridge.png)

---

After this step, the **Deploy Lambda function** should automatically be triggered, assuming your EventBridge rule is correctly configured.

Continue to the next step to check the deployment status.

[Next: Check Deployment Status via API](../4.2-checkstatus/)