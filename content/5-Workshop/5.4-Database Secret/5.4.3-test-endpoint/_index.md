---
title: "Configure AWS Secrets Manager"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b> 5.4.3. </b>"
---

### Secure Configuration Management
To enhance system security, AWS Secrets Manager is utilized in place of traditional local `.env` files for storing sensitive configuration values. This approach ensures that application containers securely retrieve these credentials at runtime, eliminating the risk of exposing sensitive data within the source code.

#### Configuration Steps
Follow these instructions to securely store the application's credentials:

1. Navigate to the **AWS Secrets Manager** console.
2. Click on **Store a new secret**.
3. For the secret type, select **Other type of secret**.
4. Define the following key-value pairs representing the required sensitive configurations:
   * `DATABASE_URL`
   * `GEMINI_API_KEY`
   * `JWT_SECRET_KEY`
5. Specify the secret name exactly as: `cloud-finance/production-secrets`
6. Review the configuration and complete the secret creation process.

![Secrets Manager Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/secrets-manager.png)