---
title: "Deploying Frontend to S3 & CloudFront"
weight: 7
chapter : false
pre : " <b> 5.7. </b> "
---

### Lab Objective

In this phase, we will host our Single Page Application (built with ReactJS) on AWS. Instead of running a traditional web server, we will utilize Amazon S3 to store the static frontend assets. To ensure high-speed global delivery, we will set up Amazon CloudFront as our Content Delivery Network (CDN).

For security, the S3 bucket will be completely blocked from direct public access. CloudFront will be the sole entry point, securely fetching content via the Origin Access Control (OAC) mechanism. Additionally, we will integrate AWS WAF to shield the application from potential cyber attacks.

---

### 1. Setting Up the S3 Bucket for Frontend Hosting

The first step is to create a secure storage space for our compiled frontend code:

- Navigate to the **Amazon S3** service in the AWS Console and click on **Create bucket**.
- Give your bucket a globally unique name (for instance, `cloud-finance-frontend-<account-id>`). Crucially, leave the **Block all public access** option enabled. This guarantees that your static files cannot be accessed directly from the internet, preventing unintended data exposure.
- Next, on your local machine, build your ReactJS source code by running the `npm run build` command.
- Finally, upload the entire contents of the generated `dist` folder into your newly created S3 bucket.

{{<figure scr="https://vvinh118.github.io/fcaj-workshop/5-workshop/5.7-frontend-deployment/s3-buckets.png" title="S3 Buckets Interface">}}


### 2. Configuring the Amazon CloudFront Distribution

Now that our code resides safely in S3, we need to configure CloudFront to serve it to our users efficiently and securely:

- Head over to the **Amazon CloudFront** service and click on **Create distribution**.
- For the **Origin domain**, select the S3 bucket where you just uploaded your frontend assets.
- Under **Origin access**, select **Origin access control (OAC)**. You will need to create a new OAC configuration. This setting ensures that only CloudFront has the necessary permissions to read files directly from your S3 bucket.
- In the **Behavior configuration** section, you need to set up routing rules:
  - Default requests for static files (HTML, CSS, JS) should be routed to the S3 origin.
  - Create additional behaviors for any requests with prefixes like `/api/*` or `/ws/*` (e.g., backend API calls or WebSockets) to be forwarded directly to your **Application Load Balancer (ALB)**.
- Lastly, integrate **AWS WAF** (Web Application Firewall) with your CloudFront distribution to filter out malicious traffic and protect your web application right at the edge.

{{<figure scr="https://vvinh118.github.io/fcaj-workshop/5-workshop/5.7-frontend-deployment/cloudfront.png" title="CloudFront Configuration">}}