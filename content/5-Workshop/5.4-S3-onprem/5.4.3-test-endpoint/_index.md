---
title : "Configure AWS Secrets Manager"
date : 2026-07-31
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

#### Configure AWS Secrets Manager

To improve security, I use AWS Secrets Manager instead of storing sensitive configuration values in local `.env` files.

The configuration process includes:

1. Open **AWS Secrets Manager**.
2. Choose **Store a new secret**.
3. Select **Other type of secret**.
4. Create the following key-value pairs:

+ `DATABASE_URL`
+ `GEMINI_API_KEY`
+ `JWT_SECRET_KEY`

5. Name the secret:

`cloud-finance/production-secrets`

6. Complete the secret creation process.

The application containers can retrieve these values securely during startup, eliminating the need to expose sensitive credentials in the source code.

![secret](/images/5-Workshop/5.4-Database/secrets-manager.png)