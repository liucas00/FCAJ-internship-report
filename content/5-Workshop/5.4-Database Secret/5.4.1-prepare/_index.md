---
title: "Create Amazon RDS PostgreSQL"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b> 5.4.1. </b>"
---

### Provisioning the Primary Database
In this step, an Amazon RDS PostgreSQL instance is provisioned to serve as the primary database for the Cloud Finance Platform.

#### Configuration Steps
Follow these instructions to create the database instance via the AWS Management Console:

1. Navigate to the **Amazon RDS** console and select **Create database**.
2. Choose the **Standard create** creation method.
3. Define the engine and instance settings:
   * **Engine options:** Select PostgreSQL 15 or later.
   * **Templates:** Choose Free Tier or Dev/Test.
   * **DB instance identifier:** Enter `cloud-finance-postgres`.
   * **Master username:** Enter `postgres`.
   * **Master password:** Configure a strong, secure password.
4. Configure the network connectivity:
   * **Virtual private cloud (VPC):** Select the `cloud-finance-vpc`.
   * **Public access:** Disable this option.
   * **VPC security groups:** Assign the `rds-sg` security group.
5. Click **Create database** to initiate the provisioning process.

#### Database-per-Service Implementation
Once the RDS instance status changes to **Available**, it is required to create separate logical databases to implement the **Database-per-service pattern**:

* `auth_db`
* `finance_db`
* `ai_db`
* `notifications_db`
* `planning_db`
* `recurring_db`

*Architecture Note:* Adopting this architecture significantly improves microservice isolation and overall system scalability.

![RDS Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/rds.png)