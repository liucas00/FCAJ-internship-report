---
title : "Create Amazon VPC"
date : 2026-07-30
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

#### Create Amazon VPC

First, I create a dedicated Amazon Virtual Private Cloud (VPC) to host the entire Cloud Finance Platform.

1. Sign in to the **AWS Management Console** and open the **Amazon VPC** service.
2. Choose **Create VPC** and select **VPC and more**.
3. Configure the following settings:

+ **Name tag:** `cloud-finance-vpc`
+ **IPv4 CIDR block:** `10.0.0.0/16`
+ **Availability Zones:** 2
+ **Public Subnets:** 2
+ **Private Subnets:** 4 (2 for application services and 2 for databases)
+ **NAT Gateway:** 1 (Single AZ)
+ Leave **VPC Endpoints** unconfigured for this step.

4. Choose **Create VPC** and wait for AWS to provision the networking resources.

After the VPC has been created, the networking infrastructure is ready for deploying the application services.

![vpc](/images/5-Workshop/5.3-Networking/create-vpc.png)