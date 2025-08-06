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

---

#### Call the /status Endpoint

Once you have the deployment `id`, call the API Gateway endpoint:

Example request using `curl`:

```bash
curl -X GET "https://your-api-id.execute-api.ap-southeast-1.amazonaws.com/prod/status?id=your-deployment-id"
```

Or test it directly in the API Gateway console using the `/status` method with `id` as a query string parameter.

---

#### Response Example

A successful response might look like this:

```json
{
  "id": "abc123",
  "status": "uploaded",
  "timestamp": "2025-08-06T09:23:45Z"
}
```

The `status` field could be one of the following:

- `uploaded`: Source code uploaded successfully
- `deploying`: Deployment process in progress
- `success`: Deployment completed successfully
- `failed`: Deployment encountered an error

You can refresh the request to get the updated status after the Deploy Lambda finishes execution.

Continue to the next step to learn how to monitor logs and events.

[Next: Monitor Logs and Events](../4.3-monitorlogs/)