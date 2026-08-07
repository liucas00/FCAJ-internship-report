---
title : "Create Amazon ECR Repositories"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.5.1. </b> "
---

#### Create Amazon Elastic Container Registry

I create Amazon ECR repositories to store Docker images for each backend microservice.

The repositories include:

+ `cloud-finance/gateway`
+ `cloud-finance/auth`
+ `cloud-finance/finance`
+ `cloud-finance/ai-agent`
+ `cloud-finance/notification-api`
+ `cloud-finance/notification-worker`
+ `cloud-finance/planning`
+ `cloud-finance/recurring`
+ `cloud-finance/ocr`

After creating the repositories, I:

1. Authenticate to Amazon ECR using AWS CLI.
2. Build Docker images locally.
3. Tag each image for the corresponding ECR repository.
4. Push the images to Amazon ECR.

Once completed, the images are ready for deployment on Amazon ECS Fargate.

![ecr](/images/5-Workshop/5.5-ECR/ecr.png)