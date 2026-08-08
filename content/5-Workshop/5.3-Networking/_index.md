---
title: "Building Network and Security Infrastructure"
date: 2026-07-30
weight: 3
chapter: true
pre: "<b> 5.3. </b>"
---

### Network Architecture Goals

To ensure the security of the application and databases, I prepare a well-isolated Virtual Private Cloud (VPC) with clear network boundaries. 

The strategy is to divide the network into two distinct layers:

*   **Public Subnet**: The internet-facing zone. I place the Load Balancer here to handle incoming external traffic.
*   **Private Subnet**: A highly secure, isolated zone with no direct internet access. All application containers and databases reside here.

### Provisioning the VPC

I set up the base network using the automated configuration tool in AWS. The steps are as follows:

1. Log in to the AWS Management Console and navigate to the **VPC** service.
2. From the **VPC Dashboard**, click **Create VPC**.
3. Select the **VPC and more** option so AWS handles the routing tables and subnets automatically.
4. Configure the following network parameters:
    *   **Name tag auto-generation**: `cloud-finance-vpc`
    *   **IPv4 CIDR block**: `10.0.0.0/16`
    *   **Tenancy**: `Default`
    *   **Number of Availability Zones (AZs)**: `2` (selecting zones like `ap-southeast-1a` and `ap-southeast-1b` for redundancy).
    *   **Number of public subnets**: `2`
    *   **Number of private subnets**: `4` (allocating 2 for ECS workloads and 2 for Databases).
    *   **NAT gateways**: Select `1 NAT gateway` (kept in a Single AZ to optimize costs).
    *   **VPC endpoints**: None.
5. Click **Create VPC** and wait for the infrastructure to be provisioned.

![VPC Creation Process](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/vpc-created.png)

### Configuring Security Groups

Next, I define 4 specific Security Groups. By applying the principle of least privilege, I ensure that resources can only communicate with authorized components.

*   **`alb-sg` (For Load Balancer):** Allows inbound traffic from anywhere (`0.0.0.0/0`) on port `80` (HTTP) and port `443` (HTTPS).
*   **`ecs-sg` (For Microservices):** Restricts inbound traffic to port `8000`, accepting requests only from the `alb-sg`. Internal communication among services within this group is permitted.
*   **`rds-sg` (For PostgreSQL):** Allows inbound connections on port `5432` strictly from `ecs-sg`. This database is completely inaccessible from the public internet.
*   **`redis-sg` (For ElastiCache Redis):** Similar to the RDS instance, opens port `6379` only to incoming traffic from `ecs-sg`, serving the Notification Worker.

![Security Groups Configuration](https://vvinh118.github.io/fcaj-workshop/5-workshop/5.3-networking/security-groups.png)