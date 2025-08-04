---
title: "Verify API Gateway Integration with Lambda"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3 </b> "
---

In this step, you will verify that the API Gateway is correctly integrated with the Lambda functions. You will test both endpoints (`/deploy` and `/status`) to ensure requests from clients are routed properly and handled as expected.

---

#### 1. Test `/status` Endpoint

##### Purpose:
Ensure the `upload-function` is responding correctly to incoming HTTP requests.

##### How to test:

- Use **Postman**, **curl**, or your frontend
- Send a `GET` request to your API Gateway:

```bash
curl -X GET https://<api-id>.execute-api.<region>.amazonaws.com/prod/status
```
Expected result:
You should receive a 200 OK response with a JSON body similar to:
```json
{
  "status": "ready"
}
```
---
#### 2. Test /deploy Endpoint
Purpose:
Trigger the upload-function through a POST /deploy request and verify it performs the following:
- Clones the GitHub repository
- Zips the contents
- Uploads to the S3 bucket
- Sends an event to EventBridge

How to test:
```bash
curl -X POST https://<api-id>.execute-api.<region>.amazonaws.com/prod/deploy \
-H "Content-Type: application/json" \
-d '{}'
```
Expected result:
You should receive a 200 OK response with a message like:
```json
{
  "message": "Upload and event published successfully."
}
```
CloudWatch verification:
In the AWS CloudWatch console:
- Navigate to Logs
- Open the log group for the upload-function
- Confirm logs show:
    - GitHub repository cloned
    - Files zipped and uploaded to S3
    - EventBridge event published
You can also check the log group for deploy-function to verify that it was triggered after the event was received.

---

#### 3. Test from Frontend (Optional)
If you're developing a frontend app (e.g., on http://localhost:3000), you can test integration via JavaScript:

```js
fetch("https://<api-id>.execute-api.<region>.amazonaws.com/prod/deploy", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({})
})
.then(res => res.json())
.then(console.log)
.catch(console.error);
```
Make sure that your API Gateway has proper CORS configuration to allow requests from http://localhost:3000.

---

#### Final Result
After completing this step, you should have confirmed that:
- The /status and /deploy endpoints are accessible via API Gateway
- The upload-function handles incoming requests correctly
- EventBridge successfully triggers the deploy-function
- CloudWatch logs confirm the sequence of actions

You are now ready to proceed to Chapter 4: Run Deployment Pipeline.

