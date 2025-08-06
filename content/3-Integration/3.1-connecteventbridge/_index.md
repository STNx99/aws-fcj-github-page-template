---
title: "Connect EventBridge Rule to Deploy Lambda"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

In this step, you will connect the EventBridge rule `uploaded_success` to the Lambda function `deploy-function`.

This integration ensures that once a deployment package is uploaded to S3 by the `upload-function`, an event will be emitted and automatically trigger the `deploy-function`.

---

#### Navigate to EventBridge Console

1. Go to the [Amazon EventBridge Console](https://console.aws.amazon.com/events/home)

2. In the sidebar, click **Event buses**

  ![](/images/3.integration/001-connecteventbridge.png)

3. Select the custom event bus named **`upload`**

  ![](/images/3.integration/002-connecteventbridge.png)

---

#### Configure the Rule Target

1. Click the **Rules** tab under the selected event bus

2. Find and click on the rule named **`uploaded_success`**

![](/images/3.integration/003-connecteventbridge.png)

3. Scroll to the **Targets** section

![](/images/3.integration/004-connecteventbridge.png)

4. If not yet set, click **Add another target**. Otherwise, click **Edit**

   - **Target type**: `AWS service`
   - **Service**: `Lambda function`
   - **Function**: `deploy-function`
   - Leave other options as default

![](/images/3.integration/005-connecteventbridge.png)
![](/images/3.integration/006-connecteventbridge.png)
![](/images/3.integration/007-connecteventbridge.png)

5. Click **Skip to review and update**.

![](/images/3.integration/008-connecteventbridge.png)

6. Paste the following event pattern:

```json
   {
     "source": ["dewebdeploy.upload"],
     "detail-type": ["DeploymentUploaded"]
   }
```

7. Click **Update rule**.

![](/images/3.integration/009-connecteventbridge.png)

---

#### Expected Outcome
After this setup:
  - upload-function emits a DeploymentUploaded event to the upload event bus
  - EventBridge matches this event via the uploaded_success rule
  - The deploy-function is invoked automatically

---

#### Next Step
Continue to [Configure Complete IAM Roles](../3.2-completeiamrole/)