---
title: "Create Amazon ElastiCache for Redis"
date: 2026-07-31
weight: 2
chapter: false
pre: "<b> 5.4.2. </b>"
---

### Provisioning the In-Memory Data Store
Following the database setup, Amazon ElastiCache for Redis is deployed to provide high-speed, in-memory data storage. This component is critical for caching and enabling asynchronous processing, which significantly improves the overall performance and responsiveness of the application.

#### Configuration Steps
Execute the following steps to provision the Redis cluster:

1. Navigate to the **Amazon ElastiCache** service console.
2. Select **Redis Caches** from the navigation pane and click to create a new cluster.
3. Define the cluster specifications:
   * **Cluster Name:** Enter `cloud-finance-redis`.
   * **Node Type:** Select `cache.t4g.micro`.
   * **Number of Replicas:** Set to `0`.
4. Configure the network integration:
   * **VPC:** Ensure the `cloud-finance-vpc` is selected.
   * **Security Group:** Assign the predefined `redis-sg`.
5. Review the settings and create the Redis cluster.

![Redis Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/redis.png)