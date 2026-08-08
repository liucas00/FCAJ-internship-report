---
title: "Building Network and Security Infrastructure"
date: 2026-07-30
weight: 3
chapter: true
pre: "<b> 5.3. </b>"
---

### 1. Network Architecture Goals

To properly secure our application and databases, we need a well-isolated Virtual Private Cloud (VPC) with clear network boundaries. 

The strategy is to divide our network into two distinct layers:
- **Public Subnet**: The internet-facing zone. We will place our Load Balancer here to catch incoming external traffic.
- **Private Subnet**: A highly secure, isolated zone with no direct internet access. All application containers and databases will reside here.

### 2. Provisioning the VPC

Let's set up the base network using the automated configuration tool in AWS.

**Steps to configure:**
1. Log in to the AWS Management Console and go to the **VPC** service.
2. From the **VPC Dashboard**, click on **Create VPC**.
3. Select the **VPC and more** option so AWS handles the routing tables and subnets automatically.
4. Input the following network parameters:
   - **Name tag auto-generation**: `cloud-finance-vpc`
   - **IPv4 CIDR block**: `10.0.0.0/16`
   - **Tenancy**: `Default`
   - **Number of Availability Zones (AZs)**: `2` (select zones like `ap-southeast-1a` and `ap-southeast-1b` for redundancy).
   - **Number of public subnets**: `2`
   - **Number of private subnets**: `4` (we will allocate 2 for ECS workloads and 2 for the Databases).
   - **NAT gateways**: Select `1 NAT gateway` (kept in a Single AZ to minimize demo costs).
   - **VPC endpoints**: None.
5. Click **Create VPC** and wait a few moments for the infrastructure to be provisioned.

![VPC Creation Process](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/vpc-created.png)

### 3. Configuring Security Groups (Firewalls)

Next, we must define 4 specific Security Groups. By applying the principle of least privilege, we ensure that resources can only communicate with the exact components they are supposed to.

- **`alb-sg` (For the Load Balancer):** 
  - Allow inbound traffic from anywhere (`0.0.0.0/0`) on port `80` (HTTP) and port `443` (HTTPS).
- **`ecs-sg` (For Microservices):** 
  - Restrict inbound traffic to port `8000`, and only accept requests originating from the `alb-sg`. Internal communication among services within this group is permitted.
- **`rds-sg` (For PostgreSQL):** 
  - Allow inbound connections on port `5432` strictly from `ecs-sg`. This database must remain completely inaccessible from the public internet.
- **`redis-sg` (For ElastiCache Redis):** 
  - Similar to the RDS instance, open port `6379` only to incoming traffic from `ecs-sg`. This is specifically required for the Notification Worker.

![Security Groups Configuration](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/security-groups.png)