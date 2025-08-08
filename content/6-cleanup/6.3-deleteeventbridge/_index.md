---
title: "Delete EventBridge Resources"
date: "`r Sys.Date()`"
weight: 12
chapter: false
pre: " <b> 6.3 </b> "
---

In this step, you will delete the **EventBridge** resources that were used to connect the `upload-function` and `deploy-function`.

Resources to delete:

- Event rule: `uploaded_success`
- Event bus: `upload`

---

#### Delete Event Rule

1. Go to the [Amazon EventBridge Console – Rules](https://console.aws.amazon.com/events/home#/rules)

2. In the top-left dropdown, select the **upload** event bus

![](/images/6.clean/001-deleteeventbridge.png)

3. Find the rule named `uploaded_success`

4. Click the checkbox next to the rule

5. Click **Delete**

![](/images/6.clean/002-deleteeventbridge.png)

6. Confirm the deletion by clicking **Delete**

![](/images/6.clean/003-deleteeventbridge.png)

---

#### Delete Event Bus

1. Go to the [Amazon EventBridge Console – Event Buses](https://console.aws.amazon.com/events/home#/event-buses)

2. Locate the custom event bus named `upload`

![](/images/6.clean/004-deleteeventbridge.png)

3. Click the checkbox next to it

4. Click **Delete**

![](/images/6.clean/005-deleteeventbridge.png)

5. Confirm the deletion by clicking **Delete**

![](/images/6.clean/006-deleteeventbridge.png)

> Note: You must delete all rules attached to the event bus before deleting the bus itself.

---

Once both the rule and the custom event bus have been deleted, the EventBridge integration will be fully removed.

---

#### Next Step

Continue to [6.4 – Delete API Gateway](../6.4-deleteapigateway/)