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

![](/images/6.clean/001-deleteamplify.png)

3. Review the attached policies

4. Detach any managed policies if necessary

![](/images/6.clean/002-deleteamplify.png)

5. Click **Delete** and confirm

![](/images/6.clean/003-deleteamplify.png)

6. Repeat the same steps for `deploy-function-role`

![](/images/6.clean/004-deleteamplify.png)
![](/images/6.clean/005-deleteamplify.png)
![](/images/6.clean/006-deleteamplify.png)

---

#### Delete Custom Inline Policies (if needed)

If you created any custom inline policies manually:

1. In the **Roles** page, click the role name

![](/images/6.clean/007-deleteamplify.png)

2. Scroll to the **Permissions policies** section

3. If you see any custom policy, click its name

4. Choose **Remove**

![](/images/6.clean/008-deleteamplify.png)
![](/images/6.clean/009-deleteamplify.png)

> **Note:** Managed policies (like `AmazonS3FullAccess`) do not need to be deleted unless you created a custom version.

---

#### Cleanup Completed

You have now successfully removed all resources created for your deployment pipeline.