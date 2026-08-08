---
title : "Containerization and Pushing to ECR"
date : 2026-07-31
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### Establishing Container Registries

To prepare the application for deployment on ECS Fargate, I require a secure, centralized registry to host the system's container images. Reflecting our microservices architecture, I provision 9 individual repositories within Amazon Elastic Container Registry (ECR) for the backend services.

The complete list of created repositories is as follows:
* `cloud-finance/gateway`
* `cloud-finance/auth`
* `cloud-finance/finance`
* `cloud-finance/ai-agent`
* `cloud-finance/notification-api`
* `cloud-finance/notification-worker`
* `cloud-finance/planning`
* `cloud-finance/recurring`
* `cloud-finance/ocr`

![Amazon ECR Repositories](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.5-containerization/ecr-repositories1.png)

### The Build and Push Workflow

With the storage foundation in place, I proceed to containerize the source code through a systematic sequence:

1. **Authentication:** I utilize the AWS CLI to securely authenticate my local Docker client with the Amazon ECR registry.
2. **Image Building:** I build the Docker images for all the backend microservices locally.
3. **Image Tagging:** I apply tags to the newly built images, ensuring they precisely match their target ECR repository URIs.
4. **Uploading (Push):** Finally, I push these tagged images up to their respective repositories in Amazon ECR.

At this stage, all system components are fully containerized, properly versioned, and staging securely in ECR, making them completely ready for deployment onto the Amazon ECS Fargate infrastructure.