---
title : "Prerequisites"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

#### Environment Preparation

Before deploying the system, I prepare the required development environment to ensure the workshop can be completed smoothly.

#### Prerequisites

The following resources are required:

+ An AWS account with sufficient IAM or Administrator permissions to provision AWS resources.
+ Docker and Docker Compose installed for building and testing Docker images locally.
+ AWS CLI installed and configured using the `aws configure` command.
+ Visual Studio Code installed for source code development.
+ The project source code, including:
  + A frontend application built with ReactJS and Vite.
  + Nine backend microservices developed with FastAPI:
    + Gateway
    + Auth
    + Finance
    + AI Agent
    + Notification API
    + Notification Worker
    + Planning
    + Recurring
    + OCR

After completing these prerequisites, I can proceed with building the AWS infrastructure and deploying the entire Cloud Finance Platform.