---
title : "Create Amazon ElastiCache for Redis"
date : 2026-07-31
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

#### Create Amazon ElastiCache for Redis

Next, I deploy Amazon ElastiCache for Redis to provide high-speed in-memory data storage.

The configuration steps are:

1. Open **Amazon ElastiCache**.
2. Select **Redis Caches** and create a new Redis cluster.
3. Configure:

+ **Cluster Name:** `cloud-finance-redis`
+ **Node Type:** `cache.t4g.micro`
+ **Replicas:** `0`

4. Select the `cloud-finance-vpc` and assign the `redis-sg` security group.
5. Create the Redis cluster.

Redis is used for caching and asynchronous processing, improving the application's overall performance.

![redis](/images/5-Workshop/5.4-Database/redis.png)