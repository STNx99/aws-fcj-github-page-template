---
title: "Delete Lambda Functions"
date: "`r Sys.Date()`"
weight: 10
chapter: false
pre: " <b> 6.1 </b> "
---

In this step, you will delete the **Lambda functions** that were created for the deployment system, specifically:

- `upload-function`
- `deploy-function`

This is usually done during cleanup or when re-deploying with significant changes.

---

#### Open the Lambda Console

1. Go to the [AWS Lambda Console](https://console.aws.amazon.com/lambda/)

2. In the left-hand menu, click **Functions**

---

#### Delete the `upload-function`

1. In the search bar, type `upload-function`

2. Click on the function name to open its details

3. In the top-right corner, click the **Actions** dropdown

4. Select **Delete**

5. In the confirmation popup, type the function name and click **Delete**

---

#### Delete the `deploy-function`

1. Return to the **Functions** list

2. In the search bar, type `deploy-function`

3. Repeat the same steps:
   - Click the function name
   - Go to **Actions** → **Delete**
   - Confirm by entering the function name and click **Delete**

---

Once deleted, the Lambda functions will no longer be available in your AWS account, and any triggers (such as EventBridge rules) referencing them will no longer work until reconfigured.

---

#### Next Step

Continue to [6.2 – Delete EventBridge Resources](../6.2-deletes3dynamodb/)