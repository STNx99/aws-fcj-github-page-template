---
title: "Create EventBridge Event Bus and Rule"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

In this step, you will set up the **EventBridge Event Bus** and a **Rule** to connect the `upload-function` with the `deploy-function`.

Once completed, the event-driven flow will look like:

> `upload-function` → (sends event) → `EventBridge` → (rule matched) → `deploy-function`

---

#### Create Event Bus

1. Go to the [Amazon EventBridge Console](https://console.aws.amazon.com/events/home)

2. In the left menu, click **Event buses**

  ![Click Event Bus](/images/2.preparation/001-createbus.png)

3. Click **Create event bus**

  ![Create Event Bus](/images/2.preparation/002-createbus.png)

4. Enter the following:
   - **Name**: `upload`
   - Leave other settings as default

  ![Enter the following name](/images/2.preparation/003-createbus.png)

5. Click **Create event bus**

  ![Click Create event bus](/images/2.preparation/004-createbus.png)

---

#### Create Event Rule: `uploaded_success`

1. Go to the [EventBridge Rules Console](https://console.aws.amazon.com/events/home#/rules)

2. Make sure the **upload** event bus is selected

3. Click **Create rule**

  ![Click Create rule](/images/2.preparation/005-createbus.png)

4. Enter rule details:
   - **Name**: `uploaded_success`
   - **Event bus**: `upload`
   - **Rule type**: `Rule with an event pattern`

  ![Enter rule](/images/2.preparation/006-createbus.png)

5. Click **Next**

  ![Click Next](/images/2.preparation/007-createbus.png)

---

#### Add Event Pattern

1. At **Events**:
  - **Event source**: `Other`

2. Under **Event pattern**, select:  
   - **Custom pattern (JSON editor)**
   
3. Paste the following event pattern:

```json
   {
     "source": ["dewebdeploy.upload"],
     "detail-type": ["DeploymentUploaded"]
   }
```

  ![Add Event Pattern](/images/2.preparation/008-createbus.png)

4. Click **Next**

  ![Click Next](/images/2.preparation/009-createbus.png)

5. Set Target to Deploy Lambda

In the Target section:

  - Target type: AWS service

  - Service: Lambda function

  - Function: deploy-function

  ![Set Target to Deploy Lambda](/images/2.preparation/010-createbus.png)

6. Click **Next**

  ![Click Next](/images/2.preparation/011-createbus.png)

7. Review the rule configuration and click **Next**

  ![Review the rule configuration](/images/2.preparation/012-createbus.png)

8. Click **Create rule**

  ![Click Create rule](/images/2.preparation/013-createbus.png)

Now, when the upload-function emits a DeploymentUploaded event, EventBridge will automatically trigger the deploy-function.

---

#### Next Step
Continue to [Create API Gateway and Configure CORS](../2.4-createapigateway/)