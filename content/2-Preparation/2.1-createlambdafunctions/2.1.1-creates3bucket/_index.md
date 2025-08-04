---
title: "Create S3 Bucket"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1.1 </b> "
---

In this step, you will create an **Amazon S3 bucket** that will store the deployment packages and host your static website. This bucket will later be used by Lambda functions to upload deployment files, and by the frontend to serve the deployed content.

---

#### Create S3 bucket

1. Go to the [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)

2. Click **Create bucket**

   ![Create Bucket](/images/2.preparation/001-createbucket.png)

3. Configure the bucket:

   - **Bucket name**: `awsdeplybucket12345`  
     *(Make sure the name is globally unique)*
   - **Region**: Choose the same region where your Lambda functions will run (e.g., `Asia Pacific (Singapore) ap-southeast-1`)
   - Leave the rest of the options as default:
     - **Block all public access**: ON *(we will configure public access for website hosting later)*
     - **Versioning**: OFF

   ![Bucket Config](/images/2.preparation/002-createbucket.png)
   ![Turn off Block](/images/2.preparation/003-createbucket.png)

4. Scroll down and click **Create bucket**

   Once created, your bucket will appear in the bucket list.

   ![Create Bucket](/images/2.preparation/004-createbucket.png)

---

#### Enable Static Website Hosting

1. Click on the newly created bucket name in the S3 Console.

![Click on the newly created bucket name in the S3 Console](/images/2.preparation/005-createbucket.png)

2. Navigate to the **Properties** tab.

![Navigate to the Properties tab](/images/2.preparation/006-createbucket.png)

3. Scroll down to the **Static website hosting** section.

![Scroll down to the Static website hosting](/images/2.preparation/007-createbucket.png)

4. Click **Edit**, then select:
   - **Hosting type**: `Host a static website`
   - **Index document**: `index.html`
   - *(Optional)* **Error document**: `error.html`

![Setup Static website hosting](/images/2.preparation/008-createbucket.png)

5. Click **Save changes**.

![Click Save changes](/images/2.preparation/009-createbucket.png)

> **Note**: You will also need to configure a bucket policy to allow public read access later in the deployment step.

---

#### Next Step

Continue to [Create DynamoDB Table](../2.1.2-createdynamodb/)
