---
title: "Create DynamoDB Table"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.1.2 </b> "
---

In this step, you will create a **DynamoDB table** to store deployment status information. This table will later be accessed and updated by the Lambda functions as part of the deployment tracking workflow.

---

#### Create DynamoDB Table

1. Go to the [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodb/)

2. Click **Create table**

   ![Click Create Table](/images/2.preparation/001-createdynamodb.png)

3. Configure the table:

   - **Table name**: `DeploymentUploaded`  
   - **Partition key**: `id` (Type: `String`)  
   - Leave the rest of the options as default:
     - **Sort key**: *None*
     - **Capacity mode**: `On-demand`
     - **Table class**: `Standard`

   ![Configure table settings](/images/2.preparation/002-createdynamodb.png)

4. Click **Create table**

   Once created, your table will appear in the list.

   ![Table created](/images/2.preparation/003-createdynamodb.png)

---

#### Notes

- The `id` attribute will act as the unique identifier for each deployment record.
- You can later extend the table with additional attributes like `status`, `timestamp`, or `log_url`.

---

#### Next Step

Continue to [Create Lambda Functions and IAM Roles](../2.2-createlambdasiamroles/)