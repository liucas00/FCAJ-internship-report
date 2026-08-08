---
title: "Create Amazon ElastiCache for Redis"[cite: 12]
date: 2026-07-31[cite: 12]
weight: 2[cite: 12]
chapter: false[cite: 12]
pre: "<b> 5.4.2. </b>"[cite: 12]
---

### Provisioning the In-Memory Data Store
Following the database setup, Amazon ElastiCache for Redis is deployed to provide high-speed, in-memory data storage[cite: 12]. This component is critical for caching and enabling asynchronous processing, which significantly improves the overall performance and responsiveness of the application[cite: 12].

#### Configuration Steps
Execute the following steps to provision the Redis cluster:

1. Navigate to the **Amazon ElastiCache** service console[cite: 12].
2. Select **Redis Caches** from the navigation pane and click to create a new cluster[cite: 12].
3. Define the cluster specifications[cite: 12]:
   * **Cluster Name:** Enter `cloud-finance-redis`[cite: 12].
   * **Node Type:** Select `cache.t4g.micro`[cite: 12].
   * **Number of Replicas:** Set to `0`[cite: 12].
4. Configure the network integration[cite: 12]:
   * **VPC:** Ensure the `cloud-finance-vpc` is selected[cite: 12].
   * **Security Group:** Assign the predefined `redis-sg`[cite: 12].
5. Review the settings and create the Redis cluster[cite: 12].

![Redis Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/redis.png)