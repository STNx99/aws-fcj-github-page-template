---
title: "Delete S3 Bucket and DynamoDB Table"
date: "`r Sys.Date()`"
weight: 11
chapter: false
pre: " <b> 6.2 </b> "
---

In this step, you will delete the **S3 bucket** and **DynamoDB table** used in your deployment system.

Resources to be deleted:

- S3 bucket: `awsdeplybucket12345`
- DynamoDB table: (the table you created with partition key `id`)

---

#### Delete the S3 Bucket

1. Go to the [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/)

2. In the **Buckets** list, search for `awsdeplybucket12345`

3. Click the bucket name to open it

![](/images/6.clean/001-deletes3dynamodb.png)

4. Before you can delete the bucket, you must empty it:
   - Click **Empty**
   - Confirm the deletion by typing the bucket name
   - Click **Empty bucket**

![](/images/6.clean/002-deletes3dynamodb.png)
![](/images/6.clean/003-deletes3dynamodb.png)

5. After the bucket is empty, return to the bucket overview page

6. Click **Delete**

![](/images/6.clean/004-deletes3dynamodb.png)

7. Confirm the deletion by typing the bucket name again, then click **Delete bucket**

![](/images/6.clean/005-deletes3dynamodb.png)

---

#### Delete the DynamoDB Table

1. Go to the [DynamoDB Console](https://console.aws.amazon.com/dynamodb/)

2. In the left-hand menu, click **Tables**

![](/images/6.clean/006-deletes3dynamodb.png)

3. Find the table you created (likely named something like `DeploymentUploaded`)

![](/images/6.clean/007-deletes3dynamodb.png)

4. Click the table name to open its details

5. In the top-right corner, click **Actions** → **Delete table**

![](/images/6.clean/008-deletes3dynamodb.png)

6. Confirm the deletion by typing the table name

7. Click **Delete**

![](/images/6.clean/009-deletes3dynamodb.png)

---

Once both the S3 bucket and DynamoDB table are deleted, your core storage resources will be fully removed from your AWS account.

---

#### Next Step

Continue to [6.3 – Delete EventBridge Resources](../6.3-deleteeventbridge/)
