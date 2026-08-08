---
title: "Workshop"
date: 2026-07-29
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Cloud Deployment for Finance Platform: Automated CI/CD and Secure Storage on AWS

#### Overview

**Amazon Web Services (AWS)** provides a robust and highly scalable toolset, making it the ideal infrastructure to transition the **Cloud Finance Platform** project from a development environment to production.

In this workshop, we will practice integrating our existing Backend-as-a-Service architecture with AWS infrastructure. The core objective is to establish a zero-touch automated deployment pipeline (CI/CD) for the Web Dashboard (ReactJS), while simultaneously building an independent, highly secure storage system on AWS to manage sensitive files (e.g., user transaction receipts and invoices).

We will focus on the in-depth setup and configuration of two core services:

+ **AWS Amplify (CI/CD & Hosting):** Establish an automated pipeline that detects source code changes from the repository (GitHub/GitLab) to build and deploy the Web Dashboard. This process includes configuring secure Environment Variables to connect with the Supabase database, setting up Redirect/Rewrite rules for the Single Page Application (SPA), and associating a Custom Domain with a free SSL/TLS certificate.
+ **Amazon S3 (Static & Document Storage):** Build an Object Storage system to complement the current infrastructure. We will create dedicated Private Buckets designed specifically for storing transaction receipt images. This section dives deep into configuring CORS (Cross-Origin Resource Sharing) to allow Direct Uploads from the Client (Web/Mobile) via Pre-signed URLs, and enforcing strict IAM/Bucket Policies to block all public access, ensuring absolute security for user financial data.

#### Workshop Contents

1. [Overview of AWS Deployment Architecture for the Finance Platform](5.1-Architecture-overview/)
   - Integration Architecture Map: Client (Flutter/React) - AWS Amplify - S3 - Supabase.
2. [Environment Prerequisites and Access Security](5.2-Prerequisites/)
   - Initializing IAM User/Role with Least Privilege permissions.
   - Preparing the GitHub Repository and Environment Variables (Supabase URL, API Keys).
3. [Lab 1: Deploying the Web Dashboard with AWS Amplify](5.3-Deploy-Amplify/)
   - Connecting the `main` branch to the Amplify Console.
   - Configuring Build settings (`amplify.yml`) for the ReactJS/TypeScript project.
   - Handling 404 errors for SPA using Rewrite Rules.
4. [Lab 2: Configuring Amazon S3 for the Transaction Receipt System](5.4-S3-Storage/)
   - Creating a Private Bucket with default Server-Side Encryption.
   - Enforcing Block Public Access.
5. [Lab 3: CORS Configuration and Upload API Integration](5.5-CORS-Integration/)
   - Configuring the CORS JSON file to grant access to the Amplify domain.
   - Implementing the upload/download flow via Pre-signed URLs connected to the Client.
6. [Integration Testing and Resource Cleanup](5.6-Testing-Cleanup/)
   - End-to-End Testing: Adding a new transaction with an attached receipt image.
   - Teardown instructions to prevent incurring unexpected AWS charges.