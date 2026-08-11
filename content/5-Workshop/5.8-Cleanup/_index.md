---
title: "Clean Up Resources"
weight: 8
chapter : false
pre : " <b> 5.8. </b> "
---

### Purpose

Once you have completed the workshop, deleting the resources you provisioned is a crucial step to avoid any unexpected charges on your AWS bill. The general rule of thumb for cleanup is to tear down the infrastructure in the reverse order of how it was built.

---

### 1. Cleaning up the Frontend (CloudFront & S3)

- **CloudFront:** Navigate to the CloudFront console and select your newly created distribution. First, you must click **Disable** (this propagation takes a few minutes). Once the status completely changes to disabled, you can safely select it again and hit **Delete**.
- **S3 Bucket:** Move over to the S3 service. Keep in mind that AWS prevents you from deleting a bucket that still contains objects. Therefore, select your `cloud-finance-frontend-<account-id>` bucket, click **Empty** to clear all static files, and then click **Delete** to remove the bucket itself.

### 2. Tearing down the Compute Layer (ECS & ALB)

- **Amazon ECS:**
  - Head over to your `cloud-finance-cluster`.
  - Select the running Service and update the 'Desired tasks' value down to `0`.
  - Wait for the active tasks to stop entirely, delete the Service, and finally delete the Cluster.
- **Load Balancer (ALB):**
  - Open the EC2 Dashboard, go to the Load Balancers section, select `cloud-finance-alb`, and click **Delete**.
  - Scroll down to Target Groups on the left pane, select your `tg-gateway` group, and delete it.

### 3. Deleting Docker Images (ECR)

- Access the **Elastic Container Registry (ECR)** console.
- Select your backend project's repository. Similar to the S3 logic, you must manually delete all the images stored inside first before you are allowed to delete the registry folder itself.

### 4. Removing Database & Secrets

- **Amazon RDS:** Go to RDS > Databases. Select your database instance and click **Delete**. Be sure to uncheck the "Create final snapshot" option (unless you intend to pay for backup storage), acknowledge the prompt, and confirm the deletion.
- **Secrets Manager:** Locate the secret storing your DB credentials and select **Delete secret**. (AWS enforces a waiting period before permanent deletion; you can schedule it for the minimum of 7 days).

### 5. Deleting Networking Infrastructure (VPC)

The final step sweeps away the underlying network foundation:
- Head to the **VPC Dashboard** > **Your VPCs**.
- Select `cloud-finance-vpc` and click **Actions** > **Delete VPC**. This action is highly convenient as it automatically detects and removes all associated dependencies, including Subnets, the Internet Gateway, Route Tables, and Security Groups.
