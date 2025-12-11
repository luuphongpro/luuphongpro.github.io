# Roommate App
## Unified AWS Serverless Solution for Real-Time Rental Management and Roommate Matching

### 1. Executive Summary
RoomMate is a platform designed to support students and landlords in searching for and managing rental rooms. The system leverages AWS Serverless architecture to optimize cost, scalability, and operational simplicity.

The platform enables landlords to post listings, manage room information (create – update – delete), and receive periodic reports. Renters can search based on multiple criteria such as location, price, and amenities; save favorite rooms; and communicate directly with landlords through an integrated mini-chat feature.

The system architecture uses **Next.js** for the frontend, **API Gateway + Lambda** for the backend, **DynamoDB** for structured data storage, along with secure authentication services. A key highlight of RoomMate is the integration of **OpenAI** to automate tasks such as sending notifications when matching rooms become available, generating analytical reports, and improving user engagement.

### 2. Problem Statement  
*Current Challenges*  
- Traditional room-searching methods (bulletin boards, social media groups) lack **advanced filtering**, have scattered information, and are often filled with spam posts.  
- Communication between students and landlords typically relies on phone/Zalo, creating **friction** and making conversation history difficult to track.  
- There is **no automated notification mechanism** alerting users when new rooms match their criteria.  
- Landlords **lack analytical tools** to understand market demand and listing performance.

*Solution*  
The **RoomMate** platform provides a centralized solution for room search and rental management, integrating an internal **mini-chat** system and **automated notifications** (via n8n) based on personal preferences.
- **AWS Serverless Architecture**: Using **API Gateway + Lambda**, DynamoDB (for rooms, users, chat), and **S3** (for images) to ensure scalability with optimized cost through the AWS Free Tier.  
- **Key Differentiators**: Unlike generic classified or chat apps, RoomMate focuses on an enhanced rental experience with an AI chatbot recommending rooms based on personalized criteria.

*Benefits & Return on Investment (ROI)*  
- **Benefits**: Provides a highly practical solution for students. Reduces communication friction through the internal chat feature. Builds a platform with **high scalability** (easily extendable to maps, reviews). Meets all 5 core objectives of a modern tech project (serverless, CI/CD, monitoring, security, data pipeline).  
- **ROI**: Extremely low development and operational cost thanks to AWS Free Tier (Lambda, DynamoDB, S3). Delivers a fully functional and practical product enhanced by automation and built-in chat capabilities.

### 3. Solution Architecture
The platform applies AWS Serverless architecture to build a data management and analytics system. Amazon API Gateway and AWS Lambda handle business logic processing. The web interface is delivered globally through CloudFront, acting as the single access point for both static content and API calls. Data is stored securely in Amazon S3 (for images/files) with protected buckets, while Amazon DynamoDB handles structured data. The entire deployment pipeline is fully automated via AWS CodePipeline connected to GitHub, and the system is monitored through Amazon CloudWatch.

![Roommate App Platform Architecture](/images/2-Proposal/platform_architecture.jpg)

*AWS Services Used*  
- **AWS Lambda**: Executes backend business logic.  
- **Amazon API Gateway**: Receives, authenticates, and routes API requests to AWS Lambda.  
- **Amazon S3**:  
  - S3 – Frontend: Stores static web content deployed by CodePipeline.  
  - S3 – Image Storage: Stores protected user-uploaded images/files.  
- **Amazon DynamoDB**: Stores structured NoSQL data such as users and metadata.  
- **AWS CodePipeline**: Automates the CI/CD deployment to S3 – Frontend and Lambda/API Gateway.  
- **Amazon Cognito**: Handles identity management and access control for API Gateway.  
- **Amazon CloudFront**: Global distribution of web content and routing API traffic to API Gateway.  
- **Amazon CloudWatch**: Logging, monitoring, and alerting for the entire system.

*Component Design*  
- **Frontend**: Web application hosted on S3 – Frontend and delivered globally via CloudFront.  
- **API Layer**: API Gateway + Lambda process requests after Cognito authentication.  
- **Data Storage**: Images/files stored in S3 – Image Storage. Structured data stored in DynamoDB.  
- **Deployment Pipeline**: CodePipeline automates build, test, and deploy from GitHub to S3-Frontend and Lambda/API Gateway.  
- **Security & Monitoring**: Protected S3 buckets, CloudWatch for system monitoring, Cognito for access management.

### 4. Technical Implementation  
*Implementation Phases*  
The project is deployed in four phases:
1. **Research & Architecture Design**: Study API Gateway, Lambda, DynamoDB, S3, CloudFront, Cognito, and CodePipeline. Design the serverless multi-layer architecture (Frontend – API – Data – CI/CD).  
2. **Cost Estimation & Feasibility**: Use AWS Pricing Calculator to estimate S3, Lambda, API Gateway, DynamoDB, and CloudFront costs. Adjust architecture based on security and cost requirements.  
3. **Architecture Optimization & Deployment Pipeline**: Optimize the API Gateway → Lambda → DynamoDB flow, configure global CloudFront distribution, create multi-bucket S3 architecture, and refine CodePipeline.  
4. **Development – Testing – Deployment**: Develop Lambda backend, configure API Gateway, build the web UI and upload to S3-Frontend, create DynamoDB schema, set up Cognito, implement CodePipeline, conduct end-to-end testing, and deploy to production.

*Technical Requirements*  
- **Web Application & Content Delivery**  
  - The frontend must be deployed as static build files on S3 – Frontend.  
  - CloudFront is required for global distribution and API routing.  
  - User images/files must be stored in S3 – Image Storage with protected access.  

- **API Layer & Business Logic**  
  - All API requests must pass through API Gateway and be authenticated via Cognito.  
  - AWS Lambda handles backend logic (CRUD, metadata, validation).  
  - APIs must follow REST and return JSON.

- **Data Storage**  
  - Structured data stored in DynamoDB with optimized Partition/Sort Key design.  
  - Two S3 buckets required:  
    - S3 – Frontend: web build files  
    - S3 – Image Storage: user uploads via presigned URLs  

- **CI/CD & Automation**  
  - Build–test–deploy must run via CodePipeline with GitHub source.  
  - Pipeline deploys both frontend (S3) and backend (Lambda + API Gateway).  
  - All changes must be logged via CloudWatch.

- **Security & Monitoring**  
  - Cognito for authentication and access control.  
  - CloudWatch for Lambda logs, API Gateway errors, and infrastructure metrics.  
  - S3 must have “Block Public Access” enabled.  
  - APIs must require authentication and be accessible only through CloudFront.

### 5. Roadmap & Milestones  
- **Pre-internship (Month 0)**: 1 month of system planning and evaluation.

- **Internship (Month 1–3)**:  
  - **Month 1 – AWS Fundamentals**  
    - Understand core AWS services (API Gateway, S3, Lambda, …).  
    - Strengthen CI/CD, logging, and foundational security knowledge.  
  - **Month 2 – Architecture Design & Refinement**  
    - Design system architecture.  
    - Optimize frontend hosting, backend APIs, storage, and security.  
    - Adjust architecture based on mentor feedback and real use-cases.  
  - **Month 3 – Deployment, Testing & Production Rollout**  
    - Deploy AWS infrastructure based on finalized architecture.  
    - Perform functional and performance testing.  
    - Fix issues, optimize resource usage and cost.  
    - Launch pilot version.

- **Post-deployment (1 year)**  
  - Maintain and optimize the system.  
  - Study advanced AWS services (Auto Scaling, WAF, CloudFormation, EKS…).  
  - Propose improvements and new features based on real user needs.

### 6. Budget Estimation  

*Infrastructure Cost*  
- AWS CloudFront: 0.00 USD (20–50 GB)  
- AWS Lambda: 0.00 USD/month (50,000 requests, 100 GB compute)  
- S3 – Frontend: 0.00 USD/month (6 GB)  
- S3 – Image Storage: 0.35–0.6 USD/month (15–25 GB)  
- Amazon API Gateway: 0.02 USD/month (20,000 requests)  
- Amazon DynamoDB: 0.00 USD (<10,000 read/write, <1 GB)  
- Amazon Cognito: 0.00 USD (<50 users)  
- AWS CodePipeline: 0 USD (20–50 builds/month)  
- Amazon CloudWatch Logs: 0.5–3.0 USD (2–15 GB logs)

**Total: 0.87–1.12 USD/month → 10.44–13.44 USD/year**

### 7. Risk Assessment  

*Risk Matrix*  
- Network outage: Medium impact, medium likelihood  
- Budget overrun: Medium impact, low likelihood  
- Realtime chat failure: Medium impact, medium likelihood  
- Map integration failure or expired API key: Medium impact, low likelihood  

*Mitigation Strategies*  
- Network: CloudFront for low-latency global content delivery  
- System health: Regular monitoring  
- Cost control: AWS budget alerts, service optimization  

*Contingency Plans*  
- Fall back to manual data collection if AWS experiences outages  
- Use CloudFormation to restore configurations  
- Switch to text-based address display or alternative APIs (Mapbox / OpenStreetMap)  
- If chatbox fails, fallback to offline messages or contact form  

### 8. Expected Outcomes  
*Technical Improvements*: Real-time data and analytics replace manual workflows. Improved accuracy of AI chatbot when recommending rooms.

*Long-term Value*: One year of data for AI research, reusable for future projects.
