---
title : "Create Amazon RDS PostgreSQL"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

#### Create Amazon RDS PostgreSQL

I create an Amazon RDS PostgreSQL instance to serve as the primary database for the Cloud Finance Platform.

1. Open **Amazon RDS** and choose **Create database**.
2. Select **Standard create**.
3. Configure the following settings:

+ **Engine:** PostgreSQL 15 or later.
+ **Template:** Free Tier or Dev/Test.
+ **DB Instance Identifier:** `cloud-finance-postgres`
+ **Master Username:** `postgres`
+ **Master Password:** a strong password.

4. Configure connectivity:

+ Select the `cloud-finance-vpc`.
+ Disable **Public Access**.
+ Assign the `rds-sg` security group.

5. Choose **Create database**.

After the database becomes available, I create separate logical databases using the Database-per-service pattern:

+ `auth_db`
+ `finance_db`
+ `ai_db`
+ `notifications_db`
+ `planning_db`
+ `recurring_db`

This architecture improves service isolation and scalability.

![rds](/images/5-Workshop/5.4-Database/rds.png)