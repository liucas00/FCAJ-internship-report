---
title : "Clean Up Resources"
date : 2026-07-31
weight : 8
chapter : true
pre : " <b> 5.8. </b> "
---

#### Clean Up Resources

After completing the workshop, I remove the AWS resources created during the deployment to avoid unnecessary charges.

The cleanup process is performed in the following order:

1. Scale all Amazon ECS Services down to `0` running tasks.
2. Delete the Application Load Balancer and its Target Groups.
3. Remove the Amazon RDS PostgreSQL instance and the Amazon ElastiCache for Redis cluster.
4. Delete the NAT Gateway and release the associated Elastic IP address.
5. Remove the Amazon CloudFront distribution and the Amazon S3 bucket used for frontend hosting.

Once these steps are completed, all resources created for the workshop are removed, ensuring that no additional AWS costs are incurred.