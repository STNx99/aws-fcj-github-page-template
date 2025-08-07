---
title: "Check Deployment Status via API"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

In this step, you will check the status of a deployment request by calling the **/status** endpoint through API Gateway. This endpoint queries the status of a deployment stored in the DynamoDB table using the `id`.

The Lambda Upload function should have created a new item in the DynamoDB table with a unique `id` and associated metadata (status, timestamp, etc.).

---

#### Retrieve Deployment ID

Before checking the status, you need to know the deployment `id`. You can find it in one of the following ways:

- In the Lambda Upload function logs on [CloudWatch](https://console.aws.amazon.com/cloudwatch/)
- As part of the response body when the upload API is triggered
- In the DynamoDB table `DeploymentStatus`

  ![](/images/4.test/007-dynamodb-record.png)

When triggering the `/deploy` endpoint in POSTMAN with:

POST https://j5eeru81c3.execute-api.ap-southeast-1.amazonaws.com/deploy

```json
{
    "repoUrl": "https://github.com/TanPhat23/staticwebsite"
}
```
 
if successful, you will receive a response similar to the example below:

![](/images/4.test/001-checkstatus.png)


In the next step, replace `your-deployment-id` with the actual value of the `id` returned, for example:

your-deployment-id = 35403e3b-3e97-4d67-9fc7-08de9e75ce30

#### Call the /status Endpoint

Once you have the deployment `id`, call the API Gateway endpoint to check the status.

**Example request using `POSTMAN`:**

1. Get your **default endpoint**

![](/images/4.test/002-checkstatus.png)
![](/images/4.test/003-checkstatus.png)

2. Get `id` from `/status` method

![](/images/4.test/004-checkstatus.png)

3. Test **Deployment's status** with **POSTMAN**

GET "https://your-api-id.execute-api.ap-southeast-1.amazonaws.com/status?id=your-deployment-id"
Example: "https://j5eeru81c3.execute-api.ap-southeast-1.amazonaws.com/status?id=35403e3b-3e97-4d67-9fc7-08de9e75ce30"

![](/images/4.test/005-checkstatus.png)

---

#### Response Example

A successful response might look like this:

```json
{
  "status": "deployed"
}
```

The `status` field could be one of the following values:

- `uploaded`: Source code uploaded successfully
- `deployed`: Deployed successfully

You can refresh the request to get the updated status after the Deploy Lambda function finishes execution.

---

Continue to the next step to learn how to monitor logs and events.

[Next: Monitor Logs and Events](../4.3-monitorlogs/)