---
title: "Configure AWS Secrets Manager"[cite: 14]
date: 2026-07-31[cite: 14]
weight: 3[cite: 14]
chapter: false[cite: 14]
pre: "<b> 5.4.3. </b>"[cite: 14]
---

### Secure Configuration Management
To enhance system security, AWS Secrets Manager is utilized in place of traditional local `.env` files for storing sensitive configuration values[cite: 14]. This approach ensures that application containers securely retrieve these credentials at runtime, eliminating the risk of exposing sensitive data within the source code[cite: 14].

#### Configuration Steps
Follow these instructions to securely store the application's credentials:

1. Navigate to the **AWS Secrets Manager** console[cite: 14].
2. Click on **Store a new secret**[cite: 14].
3. For the secret type, select **Other type of secret**[cite: 14].
4. Define the following key-value pairs representing the required sensitive configurations[cite: 14]:
   * `DATABASE_URL`[cite: 14]
   * `GEMINI_API_KEY`[cite: 14]
   * `JWT_SECRET_KEY`[cite: 14]
5. Specify the secret name exactly as[cite: 14]: `cloud-finance/production-secrets`
6. Review the configuration and complete the secret creation process[cite: 14].

![Secrets Manager Configuration](https://vvinh118.github.io/fcaj-workshop/images/5-Workshop/5.4-Database/secrets-manager.png)