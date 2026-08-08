---
title : "Introduction"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Workshop Introduction

Welcome to the workshop **Building and Deploying an AI-Powered Personal Finance Management System on AWS (Cloud-Native Microservices)**.

This workshop demonstrates how to build and operate the **Cloud Finance Platform**, an intelligent personal finance management system powered by AI, Natural Language Processing (NLP), and Optical Character Recognition (OCR). I will deploy the complete solution using a cloud-native microservices architecture on AWS.

#### Workshop Overview

In this workshop, I will learn how to:

+ Prepare the development environment and AWS account.
+ Build secure networking infrastructure using Amazon VPC, Subnets, and Security Groups.
+ Provision the data layer with Amazon RDS PostgreSQL, Amazon ElastiCache for Redis, and AWS Secrets Manager.
+ Build and push Docker images for backend microservices to Amazon ECR.
+ Deploy backend services on Amazon ECS Fargate with an Application Load Balancer.
+ Deploy the frontend application to Amazon S3 and Amazon CloudFront.
+ Configure a CI/CD pipeline using GitHub Actions for automated deployments.
+ Clean up AWS resources after completing the workshop to avoid unnecessary costs.

#### Architecture Overview

The system architecture for the **Cloud Finance Platform** is designed for high availability, security, and scalability using AWS cloud-native services:

* **Edge & Frontend Layer:** Users access the web or mobile application via **Amazon CloudFront**, which securely delivers the Single Page Application (SPA) stored in an **Amazon S3** origin. **AWS WAF** is attached to CloudFront to mitigate malicious traffic.
* **Network & Load Balancing:** The infrastructure resides within an **Amazon VPC**. Incoming traffic flows through an Internet Gateway to an **Application Load Balancer (ALB)** deployed in the Public Subnets, which routes requests to the backend.
* **Application Layer (Microservices):** Backend services (Gateway, Auth, Finance, AI Agent, Planning, Notification, OCR, etc.) are hosted on **Amazon ECS on AWS Fargate** within Private Application Subnets. The AI Agent Service connects to external AI services like the **Gemini LLM API**.
* **Data & Storage Layer:** Located in the Private DB Subnets, the system utilizes **Amazon RDS for PostgreSQL** for robust relational database storage per microservice, and **Amazon ElastiCache for Redis** for caching and message queues. An additional S3 bucket is provisioned for handling receipts and exports.
* **CI/CD Pipeline:** The CI/CD flow uses **GitHub Actions** to automatically build and push container images to **Amazon ECR**, which triggers deployment updates on Amazon ECS.
* **Observability & Security:** **AWS Secrets Manager** securely stores configuration data, **Amazon CloudWatch** handles central logging and metrics, and **Amazon SES** manages outgoing emails (e.g., OTPs and notifications).

![System Architecture](/FCAJ-internship-report/images/5-Workshop/5.1-Workshop-overview/architect.jpg)