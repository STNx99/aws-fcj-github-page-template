---
title: "Integration"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice info %}}
In this section, you will integrate all previously created components — including Lambda, EventBridge, IAM roles, and API Gateway — into a functioning deployment pipeline. This ensures that services communicate securely and effectively.
{{% /notice %}}

Once completed, your system will be ready to accept deployment requests via API, automatically upload and deploy code, and log deployment status.

---

### Content

- [3.1 Connect EventBridge Rule to Deploy Lambda](3.1-connecteventbridge/)
- [3.2 Configure Complete IAM Roles for Lambda](3.2-completeiamroles/)
- [3.3 Verify API Gateway to Lambda Integration](3.3-testapigateway/)