---
title: "Upload Source Code via Lambda Upload"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

In this step, you will test the **Lambda Upload function**, which is responsible for:

- Cloning source code from a GitHub repository  
- Uploading a zip file to an S3 bucket  
- Sending a custom event to EventBridge to initiate the deployment process

This Lambda function **must be pre-created and properly configured**, including:

- GitHub integration (via Lambda Layer or bundled library)
- Permissions to access S3, DynamoDB, and EventBridge
- A timeout of 2 minutes
- A runtime environment (Node.js or Python) that supports `git` (via Lambda layer or bundling)

---

#### Update Lambda Upload Source Code (if not yet available)

The `upload` Lambda should perform the following steps:

1. Clone the GitHub repository (e.g., [TanPhat23/awscode](https://github.com/TanPhat23/awscode))

![](/images/4.test/001-uploadlambda.png)
![](/images/4.test/002-uploadlambda.png)

2. Zip the source code upload on `awscode/lambdacode`

![](/images/4.test/003-uploadlambda.png)
![](/images/4.test/004-uploadlambda.png)

3. Upload the zip file to S3

![](/images/4.test/005-uploadlambda.png)
![](/images/4.test/006-uploadlambda.png)
![](/images/4.test/007-uploadlambda.png)
![](/images/4.test/008-uploadlambda.png)
![](/images/4.test/009-uploadlambda.png)

4. Send a custom event to EventBridge

![](/images/4.test/010-uploadlambda.png)
![](/images/4.test/011-uploadlambda.png)

If the test result is like below then it is correct.

![](/images/4.test/012-uploadlambda.png)

If your Lambda function does not yet include the GitHub cloning logic, update it using the sample repo:  
https://github.com/TanPhat23/awscode

---

#### Upload the .zip (Deploy package) to Lambda

Before testing, you need to:

1. Build and zip the Lambda `upload` source code (if you’ve made changes)
2. Go to the [Lambda Console](https://console.aws.amazon.com/lambda/)
3. Select the `upload` function, then click **Upload from** → **.zip file**
4. Upload the updated zip file (you can create it with `zip -r function.zip .` from your project folder)

---

#### Invoke the Upload Lambda Function (Manual Test)

You can test the Lambda function in two ways: directly from the AWS Lambda Console or later via API Gateway.

**Steps to test manually:**

1. Go to the [Lambda Console](https://console.aws.amazon.com/lambda/)
2. Select the function named `upload-function`

![](/images/4.test/005-uploadlambda.png)

3. Open the **Test** tab

![](/images/4.test/010-uploadlambda.png)

4. Create a new test event with the following content:

```json
{
  "httpMethod": "POST",
  "path": "/deploy",
  "body": "{\"repoUrl\": \"https://github.com/TanPhat23/staticwebsite\"}"
}
```

![](/images/4.test/013-uploadlambda.png)

**Note:** This test data mimics a request sent via API Gateway.  
Make sure your Lambda code handles `event.body` properly  
(for example: `JSON.parse(event.body)` if using Node.js).

5. Click **Test** to invoke the Lambda function.

![](/images/4.test/014-uploadlambda.png)

If the test result is like below then it is correct.

![](/images/4.test/015-uploadlambda.png)

---

#### Expected Results if Successful

- Source code is **cloned from GitHub**
- Code is **zipped**
- Zip file is **uploaded to the S3 bucket** (e.g., `awsdeplybucket12345`)
- A **custom event** is sent to EventBridge with `source: dewebdeploy.upload`

---

#### Verify Upload in S3

1. Go to the [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home)
2. Open the bucket `awsdeplybucket12345`

![](/images/4.test/016-uploadlambda.png)

3. Check whether the zip file (containing the source code) has been uploaded

![](/images/4.test/017-uploadlambda.png)

---

#### Verify EventBridge Event

1. Go to the [Amazon EventBridge Console](https://console.aws.amazon.com/events/)
2. Open **Event Buses**, and select the event bus named `upload`

![](/images/4.test/018-uploadlambda.png)

3. Go to the **Monitoring** tab, then click **View metrics in CloudWatch**

![](/images/4.test/019-uploadlambda.png)

4. Check the invocation graph or logs to verify that the event was sent

![](/images/4.test/020-uploadlambda.png)

---

After completing this step, the `deploy` Lambda function should be automatically triggered  
if the EventBridge rule has been correctly configured.

Continue to the next step to check the deployment status:

[Next: Check Deployment Status via API](../4.2-checkstatus/)