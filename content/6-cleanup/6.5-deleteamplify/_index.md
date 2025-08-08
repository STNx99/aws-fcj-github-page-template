---
title: "Delete IAM Roles and Policies"
date: "`r Sys.Date()`"
weight: 14
chapter: false
pre: " <b> 6.5 </b> "
---

In this final cleanup step, you will delete the **IAM roles and custom policies** that were created for the Lambda functions and EventBridge integration.

This will help keep your AWS environment clean and reduce any unnecessary security risks.

---

#### Identify Roles to Delete

You may have created or used the following IAM roles:

- `upload-function-role` – attached to `upload-function`
- `deploy-function-role` – attached to `deploy-function`

These roles may include attached managed policies such as:

- `AmazonDynamoDBFullAccess`
- `AmazonEventBridgeFullAccess`
- `AmazonS3FullAccess`

And a **custom inline policy** like:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::awsdeplybucket1234/*"
    }
  ]
}
```

#### Delete IAM Roles

1. Go to the [IAM Console – Roles](https://console.aws.amazon.com/iamv2/home#/roles)

2. In the search bar, enter `upload-function-role` and select it

3. Review the attached policies

4. Detach any managed policies if necessary

5. Click **Delete** and confirm

6. Repeat the same steps for `deploy-function-role`

---

#### Delete Custom Inline Policies (if needed)

If you created any custom inline policies manually:

1. In the **Roles** page, click the role name

2. Scroll to the **Permissions policies** section

3. If you see any custom policy, click its name

4. Choose **Delete policy**

> **Note:** Managed policies (like `AmazonS3FullAccess`) do not need to be deleted unless you created a custom version.

---

#### Cleanup Completed

You have now successfully removed all resources created for your deployment pipeline.