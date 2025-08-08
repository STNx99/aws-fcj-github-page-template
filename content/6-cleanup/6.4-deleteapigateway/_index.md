---
title: "Delete API Gateway"
date: "`r Sys.Date()`"
weight: 13
chapter: false
pre: " <b> 6.4 </b> "
---

In this step, you will delete the **API Gateway** that was created to expose the Lambda functions via HTTP endpoints.

You may have configured the following endpoints:

- `POST /deploy` → calls `upload-function`
- `GET /status` → calls `upload-function`

---

#### Open API Gateway Console

1. Go to the [Amazon API Gateway Console](https://console.aws.amazon.com/apigateway/)

2. In the left-hand menu, choose **APIs**

3. Locate the API you created (for example, `DeployAPI`)

![](/images/6.clean/001-deleteapigateway.png)

---

#### Delete the API

1. Click on the API name to open its details

2. In the left menu, scroll down and click **Stages**

3. Take note of the API ID and stage name (optional, for documentation)

![](/images/6.clean/002-deleteapigateway.png)

4. Return to the main API settings

![](/images/6.clean/003-deleteapigateway.png)

5. In the top-right corner, click **Delete**

![](/images/6.clean/004-deleteapigateway.png)

6. Confirm the deletion by clicking **Delete**

![](/images/6.clean/005-deleteapigateway.png)

---

After this step, the API endpoints will no longer be accessible publicly, and HTTP access to your Lambda functions will be removed.

---

#### Optional: Delete CORS Configuration

If you added CORS headers to your API manually or via console, those settings will be removed automatically with the API.

No additional steps are needed.

---

#### Next Step

Continue to [6.5 – Delete IAM Roles and Policies](../6.5-deleteiam/)
