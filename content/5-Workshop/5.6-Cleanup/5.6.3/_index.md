---
title : "Create Task Definitions and ECS Services"
date : 2026-07-31
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

#### Create Task Definitions and ECS Services

Finally, I create Task Definitions and deploy the ECS Services.

The deployment process includes:

1. Create a Task Definition for each microservice.
2. Select **AWS Fargate** as the launch type.
3. Use the `awsvpc` network mode.
4. Configure container images from Amazon ECR.
5. Expose port `8000` for the Gateway service.
6. Retrieve sensitive configuration from AWS Secrets Manager.
7. Create ECS Services from the Task Definitions.
8. Attach the services to the Application Load Balancer.
9. Enable Service Connect for internal service communication.

After deployment, all ECS Services are running and ready to handle application requests.

![service](/images/5-Workshop/5.6-ECS/service.png)