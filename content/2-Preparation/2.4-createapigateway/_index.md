---
title: "Create API Gateway and Configure Endpoints with CORS"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 2.4 </b> "
---

In this step, we will create an **API Gateway** to expose HTTP endpoints that invoke the Lambda functions. We will set up two endpoints:

- **POST /deploy** → triggers the Upload Lambda function  
- **GET /status** → retrieves deployment status (handled by the Upload Lambda function as well)  

We will also configure **CORS** to allow requests from `http://localhost:3000`.

---

#### Step 1: Create a HTTP API

1. Go to the [API Gateway Console](https://console.aws.amazon.com/apigateway/home)
2. Click **Create API**

   ![Create API](/images/2.preparation/001-createapigateway.png)

3. Choose **HTTP API** (not private)
4. Click **Build**

   ![Build HTTP API](/images/2.preparation/002-createapigateway.png)

---

#### Step 2: Configure API

1. Enter **API name**: `DeployAPI`
2. Click **Create API**

   ![Create API](/images/2.preparation/003-createapigateway.png)
   ![](/images/2.preparation/004-createapigateway.png)
   ![](/images/2.preparation/005-createapigateway.png)
   ![](/images/2.preparation/006-createapigateway.png)

---

#### Step 3: Create Routes and Integrations (HTTP API)

##### Create `/deploy` route

1. Select or create your HTTP API
2. In the left menu, choose **Routes**
3. Click **Create**

   ![](/images/2.preparation/007-createapigateway.png)

4. Enter:
   - **Method**: `POST`
   - **Resource path**: `/deploy`
5. Click **Create**

   ![](/images/2.preparation/008-createapigateway.png)

##### Attach Lambda Integration to `/deploy`

1. In the **Routes** tab, select the new `/deploy` route
2. Under **Integration**, click **Attach integration**

   ![](/images/2.preparation/009-createapigateway.png)

3. Click **Create and attach an integration**

   ![](/images/2.preparation/010-createapigateway.png)

3. Choose **Lambda function**
4. Select region and type the function name: `upload-function`

   ![](/images/2.preparation/011-createapigateway.png)

5. Click **Create**

   ![](/images/2.preparation/012-createapigateway.png)

---

##### Create `/status` route

1. Go back to **Routes** and click **Create**

   ![](/images/2.preparation/013-createapigateway.png)

2. Method: `GET`
3. Path: `/status`
4. Click **Create**

   ![](/images/2.preparation/014-createapigateway.png)

##### Attach Lambda Integration to `/status`

1. Select the new `/status` route
2. Click **Attach integration**

   ![](/images/2.preparation/015-createapigateway.png)

3. Select `upload-function`
4. Click **Attach Integration**

   ![](/images/2.preparation/016-createapigateway.png)

---

#### Step 4: Enable CORS

1. In the left menu, go to **CORS**
2. Click Configure for both `/deploy` and `/status` methods

   ![](/images/2.preparation/017-createapigateway.png)

3. Configure CORS settings:
   - **Access-Control-Allow-Origin**: `http://localhost:3000`
   - **Access-Control-Allow-Headers**: `content-type`
   - **Access-Control-Allow-Methods**: `GET,POST`
4. Click **Add**

   ![](/images/2.preparation/018-createapigateway.png)

5. Click **Save**

   ![](/images/2.preparation/019-createapigateway.png)
---

#### Summary

Your HTTP API Gateway now exposes two routes:

| Method | Path     | Lambda Function | Description                   |
|--------|----------|------------------|-------------------------------|
| POST   | /deploy  | upload-function  | Upload source & emit event    |
| GET    | /status  | upload-function  | Check deployment status       |

These endpoints are CORS-enabled to accept requests from `http://localhost:3000`.

---

#### Next
You can now move on to [**Chapter 3: Connect and Test Your Deployment Flow**.](../../3-Integration/)
