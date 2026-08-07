---
title : "Deploy Frontend to Amazon S3 and CloudFront"
date : 2026-07-31
weight : 1
chapter : false
pre : " <b> 5.7. </b> "
---

#### Deploy Frontend

After completing the backend deployment, I deploy the frontend application.

The deployment process includes:

1. Create an Amazon S3 bucket for static website hosting.
2. Enable **Block all public access**.
3. Build the React application using:

```bash
npm run build
```

4. Upload the `dist` directory to the S3 bucket.
5. Create a new Amazon CloudFront distribution.
6. Configure the S3 bucket as the origin.
7. Enable **Origin Access Control (OAC)** so that CloudFront is the only service allowed to access the bucket.
8. Forward `/api/*` and `/ws/*` requests to the Application Load Balancer.
9. Integrate AWS WAF to improve application security.

After deployment, users can access the application through the CloudFront domain with improved performance and scalability.

![cloudfront](/images/5-Workshop/5.7-Frontend/cloudfront.png)