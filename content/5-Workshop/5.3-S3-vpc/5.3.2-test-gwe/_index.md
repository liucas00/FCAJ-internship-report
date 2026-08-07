---
title : "Configure Security Groups"
date : 2026-07-30
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

#### Configure Security Groups

After creating the VPC, I configure Security Groups to control network traffic between the AWS resources.

The following Security Groups are created:

+ **alb-sg**
    + Allows inbound HTTP (80) and HTTPS (443) traffic from the Internet.

+ **ecs-tasks-sg**
    + Allows inbound traffic on port 8000 from the Application Load Balancer.
    + Enables communication between backend microservices.

+ **rds-sg**
    + Allows PostgreSQL (5432) connections only from `ecs-tasks-sg`.
    + Blocks all public Internet access.

+ **redis-sg**
    + Allows Redis (6379) connections only from `ecs-tasks-sg`.

With these Security Groups in place, all components communicate through controlled network rules, improving the overall security of the Cloud Finance Platform.

![security-group](/images/5-Workshop/5.3-Networking/security-groups.png)