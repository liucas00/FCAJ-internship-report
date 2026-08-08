---
title: "Deploying on ECS Fargate & ALB"
weight: 6
chapter : false
pre : " <b> 5.6. </b> "
---

### Core Objective

This lab guides you through initializing a serverless ECS Cluster. Next, we will set up an Application Load Balancer to efficiently distribute incoming traffic, as well as define Task Definitions to run our microservices. A key highlight here is configuring the system to automatically fetch sensitive credentials from AWS Secrets Manager instead of hardcoding them.

---

### 1. Initializing the Amazon ECS Cluster

To begin, you need to create a centralized environment to manage your containers:

- From the main AWS Console interface, navigate to the **Amazon ECS** service.
- On the left-hand menu, select **Clusters**, then click on the **Create cluster** button.
- In the setup form, provide a name for your cluster, such as `cloud-finance-cluster`.
- Under the **Infrastructure** section: Make sure to check **AWS Fargate**. This serverless compute engine allows you to run containers without having to manage underlying physical servers or EC2 instances.
- Finally, hit **Create** to let the system provision your new cluster.

![Create ECS Cluster](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/ecs-cluster.png)

### 2. Setting Up the Application Load Balancer (ALB)

Implementing a Load Balancer is essential for load distribution and safely routing external traffic to your internal services:

- Open the **EC2** service, scroll down to the **Load Balancing** section on the left navigation pane, and choose **Load Balancers**. Then, click **Create Load Balancer**.
- Select **Application Load Balancer** from the available options.
- You will need to provide the following basic configurations:
  - **Name:** Set this to `cloud-finance-alb`.
  - **Scheme:** Choose `Internet-facing` so the load balancer can receive requests from the public internet.
  - **VPC & Subnets:** Select the `cloud-finance-vpc` and assign 2 corresponding Public Subnets.
  - **Security groups:** Attach the `alb-sg` security group to safely control inbound and outbound traffic.
- Next, create Target Groups (for example, name it `tg-gateway`, listening on port `8000`, with the health check path set to `/health`). Save these settings to complete the ALB creation process.

![Create ALB](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/alb.png)

### 3. Configuring Task Definitions and Running ECS Services

The final step is to define the blueprint for your containers and launch the actual service on your cluster:

- Head back to the ECS Console, navigate to **Task definitions**, and select **Create new task definition**.
- Specify a task family name, for instance, `cloud-finance-gateway-task`. Choose **AWS Fargate** as the launch type and set the network mode to `awsvpc`.
- For the **Container Definitions** section, configure the following parameters:
  - Point to the container image path previously stored in ECR.
  - Set the port mapping to `8000`.
  - In the `secrets` block, set up the references so the system automatically pulls secure values from AWS Secrets Manager and injects them into the container's environment variables upon startup.
- Once your Task Definition is ready, return to the `cloud-finance-cluster` management screen. Click on **Create Service** to deploy the actual running service. Attach this service to the ALB you created in step 2, and remember to enable **Service Connect** to optimize internal communication among your microservices.

![Configure ECS Services](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.6-ecs-deployment/ecs-services.png)