---
title: "Create Amazon RDS PostgreSQL"[cite: 10]
date: 2026-07-31[cite: 10]
weight: 1[cite: 10]
chapter: false[cite: 10]
pre: "<b> 5.4.1. </b>"[cite: 10]
---

### Provisioning the Primary Database
In this step, an Amazon RDS PostgreSQL instance is provisioned to serve as the primary database for the Cloud Finance Platform[cite: 10].

#### Configuration Steps
Follow these instructions to create the database instance via the AWS Management Console:

1. Navigate to the **Amazon RDS** console and select **Create database**[cite: 10].
2. Choose the **Standard create** creation method[cite: 10].
3. Define the engine and instance settings[cite: 10]:
   * **Engine options:** Select PostgreSQL 15 or later[cite: 10].
   * **Templates:** Choose Free Tier or Dev/Test[cite: 10].
   * **DB instance identifier:** Enter `cloud-finance-postgres`[cite: 10].
   * **Master username:** Enter `postgres`[cite: 10].
   * **Master password:** Configure a strong, secure password[cite: 10].
4. Configure the network connectivity[cite: 10]:
   * **Virtual private cloud (VPC):** Select the `cloud-finance-vpc`[cite: 10].
   * **Public access:** Disable this option[cite: 10].
   * **VPC security groups:** Assign the `rds-sg` security group[cite: 10].
5. Click **Create database** to initiate the provisioning process[cite: 10].

#### Database-per-Service Implementation
Once the RDS instance status changes to **Available**, it is required to create separate logical databases to implement the **Database-per-service pattern**[cite: 10]:

* `auth_db`[cite: 10]
* `finance_db`[cite: 10]
* `ai_db`[cite: 10]
* `notifications_db`[cite: 10]
* `planning_db`[cite: 10]
* `recurring_db`[cite: 10]

*Architecture Note:* Adopting this architecture significantly improves microservice isolation and overall system scalability[cite: 10].

![RDS Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/rds.png)