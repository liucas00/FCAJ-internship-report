---
title: "7 IAM Best Practices to Secure Your AWS Account"
date: 2026-08-07
draft: false
description: "Learn 7 crucial IAM best practices to secure your AWS account, from limiting Root User access and enabling MFA to applying Least Privilege, using IAM Roles, and monitoring with CloudTrail."
categories:
  - AWS
image: "/images/blogs/iam-best-practices.png"
---

When getting started with AWS, many people focus on creating EC2 instances, storing data on S3, or deploying databases using Amazon RDS. However, before worrying about how fast the system runs, we need to answer a more crucial question:

> **Who is allowed to access the resources, and what actions are they permitted to perform?**

This is the role of **AWS Identity and Access Management (IAM)**.

IAM helps you manage identities, authenticate users, and control access to resources within your AWS Account. When a user or application makes a request, AWS evaluates the identity, policies, actions, and associated resources before allowing or denying that request.

In this article, we will explore **7 IAM Best Practices** to make your AWS Account safer and easier to manage.

---

## 1. Do Not Use the Root User for Everyday Tasks

The Root User is created alongside the AWS Account and has unrestricted access to all resources, account information, and billing. Therefore, AWS strongly recommends **against using the Root User for everyday tasks** such as:

- Creating EC2 instances
- Modifying Security Groups
- Managing S3 Buckets
- Configuring services

After creating an account, you should:

- Set a strong password
- Enable MFA for the Root User
- Do not create Access Keys for the Root User
- Only log in as the Root User when absolutely necessary

For standard administrative tasks, use **AWS IAM Identity Center** or an IAM Role with appropriate scoped permissions.

---

## 2. Enable Multi-Factor Authentication (MFA)

Even strong passwords can be compromised through phishing or data breaches. MFA adds an extra authentication layer that significantly reduces the risk of unauthorized access.

You should enable MFA for:

- The Root User
- Administrators
- Users with permissions to modify IAM
- Any active IAM Users

AWS currently supports:

- Passkeys
- Security Keys
- Authenticator apps (OTP)

AWS recommends prioritizing Passkeys or Security Keys whenever possible.

---

## 3. Apply the Principle of Least Privilege

The **Least Privilege** principle means granting only the exact permissions needed to complete a task.

For example, if an application only needs to read images from an S3 Bucket, you should only grant:

```text
s3:ListBucket
s3:GetObject
```

Instead of:

```text
AdministratorAccess
```

Example IAM Policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example-image-bucket"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-image-bucket/*"
    }
  ]
}
```

When building IAM Policies, avoid using:

```json
"Action": "*"
```

or

```json
"Resource": "*"
```

Also, regularly review permissions as your system evolves.

---

## 4. Prioritize Temporary Credentials

Long-term Access Keys remain valid until they are deleted or deactivated. If compromised, anyone can use them.

AWS recommends using **Temporary Credentials** via IAM Roles.

Workflow:

```text
User logs in
        ↓
Assumes an IAM Role
        ↓
AWS issues Temporary Credentials
        ↓
Accesses resources within the permitted scope
```

Since these credentials only exist for a short period, security risks are significantly reduced.

---

## 5. Use IAM Roles for Applications

A very common mistake is hardcoding Access Keys directly into the source code or `.env` files.

```text
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
```

If the repository accidentally becomes public or the source code is shared, your credentials will be exposed.

Instead, use IAM Roles:

- EC2 → Instance Profile
- ECS → Task Role
- Lambda → Execution Role

For instance:
If an ECS Task only needs to upload invoices to S3, its Task Role only needs the `s3:PutObject` permission restricted to the specific invoice directory. 

There is no need to store Access Keys in the source code, and permissions are managed much more transparently.

---

## 6. Manage Access Keys Carefully

In some special cases, systems outside of AWS may still require Access Keys. 

When this happens, keep in mind:

- Never store Access Keys in source code
- Never commit `.env` files to GitHub
- Do not share a single key across multiple applications
- Grant only the minimum required privileges
- Delete keys that are no longer in use
- Rotate keys immediately if you suspect a breach

AWS also strictly advises against creating Access Keys for the Root User.

---

## 7. Review Permissions and Monitor Activity

IAM configuration shouldn't stop once a Policy is created.

### IAM Access Analyzer

IAM Access Analyzer helps you:

- Detect resources shared outside your account
- Provide recommendations for scaling down permissions
- Facilitate the application of Least Privilege

### AWS CloudTrail

CloudTrail records all activities made via:

- AWS Console
- AWS CLI
- SDKs
- APIs

CloudTrail helps answer these questions:

- Who performed the action?
- What action was performed?
- When did it happen?
- On which resource?

CloudTrail Event History stores Management Events for the **past 90 days** in each Region. For longer retention, use CloudTrail Trail or CloudTrail Lake.

---

## Quick AWS Account Security Checklist

Before you finish, run through this quick self-check:

- Is MFA enabled for the Root User?
- Does the Root User have any Access Keys?
- Are EC2, ECS, and Lambda using IAM Roles?
- Are there any unnecessary AdministratorAccess policies?
- Are there any unused Access Keys?
- Have you reviewed IAM Access Analyzer findings?
- Is CloudTrail enabled?

---

## Conclusion

IAM is the fundamental pillar of AWS security. A well-designed system can still be at risk if the Root User is used regularly, Access Keys are hardcoded, or excessive permissions are granted.

The seven crucial best practices to remember are:

1. Limit Root User usage
2. Enable MFA for critical identities
3. Apply the Principle of Least Privilege
4. Prioritize Temporary Credentials
5. Use IAM Roles for workloads
6. Strictly manage Access Keys
7. Combine IAM Access Analyzer and CloudTrail for system auditing

With just simple changes like enabling MFA, removing unused Access Keys, narrowing down IAM Policies, and correctly utilizing IAM Roles, your AWS Account's security posture can be drastically improved.

---

## References

- Security best practices in IAM
- Root user best practices for your AWS account
- AWS Multi-factor authentication in IAM
- Manage access keys for IAM users
- What is AWS CloudTrail?

{{<figure src="https://vvinh118.github.io/fcaj-workshop/3-blogsposted/3.1-blog3/blog1.png" title="Proof on AWS Study Group VN">}}