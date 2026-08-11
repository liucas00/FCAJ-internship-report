---
title: "Database Tier & Security Configuration"
weight: 4
chapter : false
pre : " <b> 5.4. </b> "
---

### Core Objective

In this section, we will provision a relational database (Amazon RDS) safely isolated within a private network. Additionally, to avoid exposing sensitive credentials (like passwords and connection strings), all access configurations will be securely encrypted and centrally managed using AWS Secrets Manager.

---

### 1. Provisioning the Database with Amazon RDS

Instead of manually installing and maintaining a database on an EC2 instance, we will leverage Amazon RDS to offload the administrative overhead:

- Navigate to the **Amazon RDS** service from the AWS Console.
- First, create a **Subnet group** to define exactly where your database will reside. Select the `cloud-finance-vpc` and specify the **Private Subnets** (this ensures the database is completely shielded from direct internet access).
- Go to the **Databases** section on the left navigation pane and click on **Create database**.
- Select your preferred database engine (e.g., MySQL or PostgreSQL) and choose the Free tier template if you are using a practice account to minimize costs.
- Provide a DB instance identifier (such as `cloud-finance-db`), then configure your Master username and password.
- Under the **Connectivity** section, double-check that **Public access** is strictly set to `No`. Attach the appropriate Security Group to allow inbound connections exclusively from your ECS backend services.

{{<figure scr="https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/rds-postgres.png" title="RDS Setup">}}

### 2. Accelerating Performance with Amazon ElastiCache for Redis

To reduce the query load on our primary database and speed up API response times, we will deploy a Redis caching layer:

- Open the **Amazon ElastiCache** console.
- Just like with RDS, start by creating a **Subnet group**. Select your `cloud-finance-vpc` and assign the Private Subnets so the Redis cluster operates securely inside your internal network.
- Next, click on **Create Redis cluster**.
- Give your cluster a recognizable name (e.g., `cloud-finance-redis`).
- For the Node type (hardware configuration), select a smaller, cost-effective instance like `cache.t2.micro` or `cache.t3.micro` for this lab environment.
- In the **Security** section, attach the proper Security Group to allow your ECS containers to read and write data to the Redis cluster.

{{<figure scr="https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/elasticache-redis.png" title="ElastiCache Redis Setup">}}

### 3. Managing Credentials with AWS Secrets Manager

Hardcoding database passwords into your application source code poses a severe security risk. AWS Secrets Manager provides an elegant solution for this:

- Head over to the **AWS Secrets Manager** console and click **Store a new secret**.
- For the secret type, select **Credentials for Amazon RDS database**.
- Input the exact Master username and password that you configured during the RDS creation step.
- Scroll down to the database section and select your `cloud-finance-db` instance to link them together.
- Proceed to the next step and assign a logical name to your secret (for example, `cloud-finance/db-credentials`).
- Complete the remaining prompts to store the secret. Later on, when deploying your ECS tasks, the containers will automatically fetch these credentials at runtime without exposing any plain-text passwords.

{{<figure scr="https://vvinh118.github.io/fcaj-workshop/5-workshop/5.4-database-secret/secrets-manager.png" title="Secrets Manager Configuration">}}
