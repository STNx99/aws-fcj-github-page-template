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

3. Select the custom event bus named **`upload`**

---

#### Configure the Rule Target

1. Click the **Rules** tab under the selected event bus

2. Find and click on the rule named **`uploaded_success`**

3. Scroll to the **Targets** section

4. If not yet set, click **Add target**. Otherwise, click **Edit**

   - **Target type**: `AWS service`
   - **Service**: `Lambda function`
   - **Function**: `deploy-function`
   - Leave other options as default

5. Click **Update** or **Add** to save changes

---

#### Event Pattern (Reminder)

This rule listens for custom events from the `upload-function` using the following pattern:

```json
{
  "source": ["dewebdeploy.upload"],
  "detail-type": ["DeploymentUploaded"]
}
```
This event is emitted by the upload-function after it successfully uploads code to the S3 bucket.

---

#### Expected Outcome
After this setup:
  - upload-function emits a DeploymentUploaded event to the upload event bus
  - EventBridge matches this event via the uploaded_success rule
  - The deploy-function is invoked automatically

---

#### Next Step
Continue to [Configure Complete IAM Roles](../3.2-completeiamrole/)