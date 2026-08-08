---
title: "Proposal"
date: 2026-07-15
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Finance Platform  
## Cross-Platform Real-Time Financial Management Solution  

### 1. Executive Summary  
The Cloud Finance Platform is a financial management system designed to address the issue of scattered cash flows across multiple payment channels. This platform offers a comprehensive solution featuring a mobile application and a web dashboard, enabling users to track income and expenses, synchronize wallets, and manage transactions in real time. The system leverages a Backend-as-a-Service (BaaS) architecture using Supabase, paired with Flutter (Dart) for mobile devices and ReactJS (TypeScript) for the web. This stack ensures high performance, robust data security, and flexible scalability.  

### 2. Problem Statement  
*Current Issues*  
Transacting through various payment channels, e-wallets, and banks (such as Techcombank, MoMo, Cake, and ShopeePay) leads to fragmented cash flows. Tracking transaction history, aggregating expenses, and monitoring budgets are currently handled mostly manually. This process is time-consuming and prone to errors. Existing market solutions often lack the customization needed for personalized data flows or are overly complex to operate.  

*The Solution*  
This project builds a unified cloud finance platform. The system uses the Supabase ecosystem (PostgreSQL, Auth, Storage) as its central data processing hub. Users interact with the platform through two main touchpoints: a dedicated Mobile App (Flutter) for quick wallet synchronization, updates, and daily transaction tracking, and a Web Dashboard (ReactJS + TypeScript) optimized for in-depth data visualization, statistics, and analytical reports.  

*Benefits and ROI*  
Digitizing and automating the reconciliation process across different funding sources provides clear financial transparency. Utilizing an open-source Cloud/BaaS architecture keeps operational expenses (OpEx) for servers to an absolute minimum. Furthermore, the platform establishes a highly structured database, laying the groundwork for future research, behavioral analysis algorithms, and cash flow forecasting.  

### 3. Solution Architecture  
The platform follows a Client-Server architecture that strictly separates the user interface from data processing logic, taking full advantage of Cloud Services to maintain real-time synchronization.  

![Architecture Diagram](https://vvinh118.github.io/fcaj-workshop/2-proposal/architecture.png)

*Services & Technologies*  
- **Frontend (Mobile):** Flutter (Dart) – Manages the wallet synchronization UI and transaction flows (wallet/transaction screens).  
- **Frontend (Web):** ReactJS with TypeScript – Powers the administrative and analytical dashboard, hosted via services like AWS Amplify or Vercel.  
- **Backend & Database:** Supabase – Provides the PostgreSQL database, Row Level Security (RLS), and Realtime subscriptions.  
- **Authentication:** Supabase Auth – Handles user identity and secure login sessions.  

*Component Design*  
- *Data Model:* An optimized database schema containing core entities: `Users`, `Wallets` (Banks, E-wallets), `Transactions`, and `Categories`.  
- *Devices & Interfaces:* The mobile app is tailored for rapid data entry and tracking wallet balances. The web app provides a broader workspace for viewing financial charts and tables.  
- *Data Processing:* Balance calculations and data logic are managed directly via PostgreSQL or integrated API functions.  

### 4. Technical Implementation  
*Deployment Phases*  
The project is structured into four main phases to maintain progress and ensure code stability:  
1. *Research & System Design:* Draft the Entity-Relationship Diagram (ERD), define UI/UX flows, and outline the repository structure (`cloud-finance-platform`).  
2. *Backend Initialization:* Provision the Supabase project, configure the database schema, and apply Row Level Security (RLS) to enforce data privacy.  
3. *Mobile App Development:* Build the Flutter application, focusing heavily on the Supabase integration module, user authentication, and wallet management screens.  
4. *Web Dashboard Development & Testing:* Finalize the web interface using ReactJS/TypeScript, connect the APIs, execute end-to-end testing across the entire platform, and deploy.  

*Technical Requirements*  
- *Mobile/Web:* Practical knowledge of ReactJS component structures, state management in Flutter, and handling asynchronous operations.  
- *Backend/Cloud:* Proficiency in the Supabase API and writing SQL logic for financial transactions to guarantee data integrity (ACID properties).  

### 5. Roadmap & Milestones  
- *Phase 1 (Design & Initialization):* Finalize the database architecture, provision the Supabase environment, and design UI/UX mockups.  
- *Phase 2 (Core Development):* Deliver the MVP for the Flutter app with full CRUD capabilities for transactions and balance synchronization.  
- *Phase 3 (Web & Expansion):* Develop the Web Dashboard using ReactJS and integrate statistical reporting modules.  
- *Phase 4 (Operation & Evaluation):* Conduct security audits, optimize overall performance, and launch the platform for practical use.  

### 6. Budget Estimation  
By adopting a BaaS architecture, upfront infrastructure costs are strictly optimized.

*Estimated Infrastructure Costs*  
- **Supabase (Database/Auth):** $0.00/month (Utilizing the Free Tier, which supports up to 500MB Database storage and 50,000 MAUs).  
- **Web Hosting (Vercel/Amplify):** $0.00/month (Basic tier for the web platform).  
- **Domain Name:** Estimated at ~$1.00 - $1.50/month.  

*Total Operating Cost:* ~$1.50/month (during the initial MVP phase for personal use).  

### 7. Risk Assessment  
*Risk Matrix*  
- *Information Security:* High impact, low probability. (Mitigation: Enforce strict Supabase RLS configurations; banking credentials will never be stored in plaintext).  
- *Data Inconsistency (Balance mismatch):* High impact, medium probability. (Mitigation: Implement rigorous Database Transactions for any tasks involving cash flow modifications).  
- *Free-tier Resource Limits:* Medium impact, low probability. (Mitigation: Actively monitor database storage capacity and prepare an upgrade path for service plans when necessary).  

### 8. Expected Outcomes  
*Deliverables:* A cohesive financial management application ecosystem that operates smoothly and synchronously across both mobile devices and web browsers.  
*Long-term Value:* Digitizing the user's entire spending history establishes a solid, structured dataset. This data will serve as the foundation for integrating Machine Learning models to analyze spending behaviors and forecast financial trends in future iterations.