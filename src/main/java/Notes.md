# AWS Level 1 Course Notes
#### Started Jan 27, 2021

## AWS
* Amazon Web Services
* Global cloud platform
* Allows users to host and manage services on the internet
* Infrastructure as a Service (IaaS)
  * Users do not need to manage the back-up, storage, or power supply of servers
  
* Platform as a Service (PaaS)
  * Users do not have to manage the binary of their application languages (Java, Python, etc.)
  
* Software as a Service (SaaS)
  * Users get email and queuing capabilities

<hr><hr>

## IAM (Global)
* Identity and Access Management
* Users & Groups
* Permissions can be assigned to Users &&/|| Groups
  * MINIMUM PERMISSION PRINCIPLE: allow the least amount of access necessary to any one user or group.
  Unused access should be removed.
* Can create a password policy/ requirement
* MFA (Multi-factor authentication
    * Virtual MFA Device: phone or computer token
    * U2F: Yubikey - token stored on thumb-drive looking device
    * Hardware Key Fob: numeric code refreshed periodically
  
<hr>

### IAM Shared Responsibility Model
#### AWS 
* Infrastructure (Global Network Security)
* Configuration & vulnerability analysis
* Compliance validation

#### User
* Users, groups, roles, & policies management & monitoring
* Enable MFA on all accounts
* Rotate keys often
* User IAM tools to apply appropriate permissions
* Analyze access patterns & review permissions

<hr><hr>

## EC2 (Regional)
* Elastic Compute Cloud (Infrastructure as a Service)
* Rent virtual machines (EC2)
* Store data on virtual drives (EBS)
* Distribute load access machines (ELB)
* Scaling the services using auto-scaling group (ASG) 
  <br><br>
  
* Instances available : t2.micro, t2.xlarge, c5d.4xlarge, r5.16xlarge, m5.8xlarge 
  * choose based on how much CPU, Memory, Bandwidth you need.
  
<br>
* AMI (Amazon Machine Image): a template that contains software configurations
  <br><br>
* EC2 Security Groups: control how traffic is allowed into and out of EC2 instances
<br><BR>
  
#### Ports to know:
* <b>22</b> = SSH (Secure Shell) : Long into Linux instance
* <b>21</b> = FTP (File Transport Protocol) : Upload files into a file share
* <b>22</b> = SFTP (Secure File Transport Protocol) :  Upload files using SSH
* <b>80</b> = HTTP : Access unsecured websites
* <b>443</b> = HTTPS : Access secured websites
* <b>3389</b> = RDP (Remote Desktop Protocol) : Log into Windows instance

<hr>

### EC2 Shared Responsibility Model
#### AWS
* Infrastructure (Global Network Security)
* Isolation on physical hosts
* Replacing faulty hardware
* Compliance validation

#### User
* Security groups rules
* OS patches and updates
* Software and utilities installed on the EC2 instance
* IAM roles assigned to EC2 & IAM user access management
* Data security of your instance

<hr><hr>

### EBS Snapshot 
* Used for EC2 storage
* a "snapshot" is a back-up of what is in storage
* To move from one EC2 instance to another: 
  1. Disconnect EBS from instance 1 
  2. Take a snapshot of the volume
  3. Attach snapshot to instance 2
  
<hr>

### AMI (Regional)
* Amazon Machine Image
* A ready-to-use customization of an EC2 instance
  * customer adds their own software configuration, software licenses, OS, monitoring, etc.
  * faster boot because software is prepackaged through the AMI
  
* AMI are built for specific regions but can be copied across regions
  <br><br>
  
Public AMI : provided by AWS<br>
Your own AMI : you make and maintain the AMI yourself<br>
AWS Marketplace AMI :  AMI made by someone else (a vendor)<br>

1. Launch an EC2 instance in a region
2. Stop the instance for data integrity
3. Create an AMI (also creates an EBS snapshot)
4. Launch from the AMI to a new region (essentially making a copy of the EC2 instance)

<hr>

### EC2 Image Builder (Regional)

* Like a template/recipe for EC2 instances that can be duplicated over other regions?
* Used to automate the creation of Virtual Machines or container images
* Automate the creation, maintain, validate and test EC2 AMIs
* Can return on a schedule (weekly, whenever packages are updated, etc)
* Free service (only pay for the underlying resources)

<hr>

### EC2 Instance Store

* EBS volumes are network drives with good but limited performance
* If you need a high-performance hardware disk, use EC2 Instance Store <br><br>

* Better I/O performance
* EC2 Instance Store lose their storage if they are stopped (ephemeral)
* Good for buffer/cache/scratch data/temporary client
* Risk of data loss if hardware fails

<hr>

### EFS - Elastic File System

* A shared file of data that can be accessed in multiple Availability Zones simultaneously
* Managed NFS (network file system) that can be mounted in 100s of EC2
* EFS works with Linux EC2 instances in multi-AZ

<hr>

### EC2 Storage Shared Responsibility Model
#### AWS
* Infrastructure (Global Network Security)
* Replication for data for EBS volumes and EFS drives
* Replacing faulty hardware
* Ensuring their employees cannot access customer data

#### User
* Setting up backup/snapshot procedures
* Setting up data encryption
* Responsibility for any data on the drives
* Understanding the risk of using EC2 Instance Store

<hr><hr>

### Vertical Scalability
* Increasing the size of your instance (from nano to XL, for example)
* good for databases
  
### Horizontal Scalability
* increasing the number of instances/systems for the application

### High Availability
* running application/system in at least 2 availability zones (works hand in hand with horizontal scalability)

<hr>

## ELB - Elastic Load Balancing

* Load balancers are services that forward internet traffic to multiple servers
* ELB is a managed load balancer
  * AWS guarantees it will be working
  * AWS takes care of upgrades, maintenance, high availability
  
* 3 Kinds :
  * Application Load Balancer (HTTP/HTTPS only) - Layer 7
  * Network Load Balancer (ultra high performance, allows for TCP) - Layer 4
  * Classic Load Balancer (slowly retiring) - Layer 4 & 7

<hr><hr>

## Amazon S3 (Global)
* "Infinitely Scaling" storage

* Used for:
  * Backup and storage
  * Disaster recovery
  * Archive
  * Hybrid Cloud storage
  * Application hosting
  * Media hosting
  * Data lakes & big data analytics
    
* Store objects (files) in "buckets" (directories)
* Objects have a key: the full path (prefix + object Name)

Durability: how often will you not lose a file, high durability
Availability: how readily available a service is, high availability

<hr>

### S3 Shared Responsibility Model
#### AWS
* Infrastructure (global security, durability, availability, sustain concurrent loss of data in two facilities)
* Configuration and vulnerability analysis
* Compliance validation

#### User
* S3 Versioning
* S3 Bucket Policies
* S3 Replication Setup
* Logging and Monitoring
* S3 Storage classes
* Data encryption at rest and in transit

<hr><hr>

## Databases
### AWS RDS 
* Relational Database Services
* Managed service : Automated provisioning, OS patching
* cannot SSH into instances

### Amazon Aurora
* not open sourced
* PostgreSQL and MySQL both supported

### Read replicas
* Scale the read workload of your DB
* Can create up to 15 Read Replicas
* Data is only written to the main DB

### Multi-AZ
* Failover in case of AZ outage (high availability)
* Data is only read/written to the main database
* Can only have 1 other AZ as failover

### Multi-Region
* save as Multi-AZ but in a different region instead of different AZ
* replication cost

### ElastiCache
* get managed Edis or Memcached
* in-memory databases with high performance, low latency

### DynamoDB
* NoSQL database - non-relational
* Scales to massive workloads
* Fast and consistent
* Single-digit millisecond latency - low latency retrieval
* Integrated with IAM for security, authorization and administration
* Low cost and auto scaling capabilities
* Key-value database
* DynamoDB Accelerator - DAX
  * Fully Managed in-memory cache for DynamoDB
  * 10x performance improvement
  * Secure, highly scalable & highly available
  * DAX is only used for and is integrated with DynamoDB, while ElastiCache can be used for other databases
  
### Redshift
* OLAP - online analytical processing (analytics and data warehousing)
* SQL interface
* pay as you go

### Amazon EMR
* Elastic MapReduce
* Hadoop cluster

### Athena
* Fully serverless database is SQL capabilities
* Used to query data in S3
* Pay per query
* log analytics

### QuickSight
* Serverless machine learning-powered business intelligence service to create interactive dashboards
* Business analytics, Building visualizations, Perform ad-hoc analysis, Get business insights using data
* Integrated with RDS, Aurora, Athena, Redshift, S3

### DocumentDB
* the same for MongoDB (NoSQL database)
* Used to store, query and index JSON data

### Neptune
* Fully managed graph database

### QLDB
* Quantum Ledger Database
* Used to review history of all the changes made to your application data
* immutable system
* Vs Amazon Managed Blockchain: no decentralization component

### Amazon Managed Blockchain
* Blockchain makes it possible to build applications where multiple parties can 
execute transactions without the need for a trusted, central authority
  
* compatible with the e Hyperledger Fabric and Ethereum

<hr><hr>

### Docker
* A software development platform to deploy apps
* Apps are packaged in containers
* Scale containers on-demand

### ECS

* Elastic Container Service
* Launch Docker containers on AWS
* You <b>must</b> provision and maintain the infrastructure

### Fargate
* Launch Docker containers on AWS
* You do <b>not</b> provision the infrastructure (no EC2 instances to manage) - simpler!
* Serverless

### ECR
* Elastic Container Registry
* Private Docker Registry on AWS
* Where you store your Docker images so they can be run by ECS or Fargate

### Serverless
* FaaS
* Developers dont have to manage the servers

### Lambda
* Virtual functions - no servers to manage
* Limited by time - short executions
* Run on-demand
* Scaling is automated!
* Pay per request and compute time after 1,000,000 AWS Lambda request (calls) 
  and 400,000 GBs of compute time (duration)
* Event-Driven: functions get invoked by AWS when needed
* Easy monitoring through AWS CloudWatch
* Lambda Container Image: ECS and Fargate is preferred over this LCI
* Used to create thumbnails for images uploaded to S3, or to run a serverless cron job

### Amazon API Gateway
* a serverless API
* Fully managed service for developers to easily create, publish, maintain,
  monitor, and secure APIs
  
* Serverless and scalable
* Supports RESTful APIs WebSocket APIs


### Lightsail
* Virtual servers, storage, database, and networking
* Low & predictable pricing
* Simpler alternative to using EC2, RDS, ELB, EBS, Route 53
* Great for people with little cloud experience
* simple web applications (LAMP, Nginx, MEAN, Node.js)
* Websites
* Dev/Test environment
* high availablity but no auto-scaling, limited AWS integrations
* Not good unless you're new to the cloud

<hr><hr>

## Elastic Beanstalk
* PaaS
* A developer centric view of deploying an application on AWS
* It uses all the component's we've seen before: EC2, ASG, ELB, RDS, etc.
* All in one view that's easy to make sense of
* We still have full control over the configuration
* Free but you pay for the underlying instances

* Managed service : Users only have to manage the application code

* Supports multiple platforms (Go, JavaSE, Java, etc.)
* Health agent pushes metrics to CloudWatch, checks for app health, 
  publishes health events

## CodeStar
### CodeDeploy
* moves EC2 instances applications or servers from V1 to V2

### CodeCommit
* Github
* Stores code in a version control repository

### CodeBuild
* Allows you to build your code, tests, and packages in the cloud
* fully managed, and serverless
* Only pay for the time your code is being built
* Continuously scalable

### CodePipeline
* Orchestrates the steps to have the code automatically pushed to production
* Continuous integration & Continuous Delivery

### CodeArtifact
* Stores and retrieves dependencies (artifact management) to make code

### CodeStar
* Unified UI to easily manage software development activities in one place
* Sets up CodeCommit, CodePipeline, CodeBuild, CodeDeploy, Elastic Beanstalk, etc.

## Cloud9
* A cloud IDE for writing, running and debugging code


<hr><hr>

## Route 53
* Managed DNS (Domain Name System)
* DNS is a collection of rules and records which helps clients understand 
  how to reach a server through URLs.
  
Simple Routing Policy - no health checks
Weighted Routing Policy- percentages
Latency Routing Policy - routes to a different region based on where the user is
Failover Routing Policy - Disaster recovery

## CloudFront
CDN - Content Delivery Network
* Improves read performance, content is cached at the edge
* Improves users experience
* DDoS protection, integration with Shield AWS Web Application Firewall
* WAF - web access controls :  prevents web attacks
* An intermediate access point between the user and your origin (S3 or AWS HTTP). 
If content is cached in the Edge, the origin does not need to be tapped for info

## AWS Outposts
* EC2 instances can run on your own physical outpost rack that has AWS 
capabilities but lives in your own data center. 
* Like a harddrive that has AWS on it. 
* Extends the cloud to your own infrastructure.

<hr><hr>

SQS
* Cloud-native
* used to decouple applications using a queue
* Webservers > requests >> SQS queue >> video processing
* messages kept up to 14 days

SNS
* Cloud-native
* notification service
* Pub/Sub
* Buying service > SNS > sends message to all the subscriptions/subscribers needed without the 
  buying service having to do it individually
  
* No message retention
  
Kinesis
* real-time big data streaming

MQ
* managed Apache ActiveMQ
* Used only if the company is migrating to the cloud from on-premesis and needs to use SQS or SNS
* does not scale as much as SQS or SNS

<hr><hr>

## Cloud Monitoring
### CloudWatch Metrics
* billing metric only available in us-east-1

### CloudWatch Alarms
* alarm when a certain condition is met

### CloudWatch Logs
* Collects log files : writes the actions of the application
* Can collects from Elastic Beanstalk, ECS, Lambda, CloudTrail, EC2 Machines, etc
* must be added to EC2 instances

### CloudWatch Events/EventBridge
* Schedule: Cron jobs (scheduled scripts), send a log once every hour (example)
* Event Pattern: send a log when a specific event happens
* EventBridge is the next evolution of Events
* EventBridge has "buses"

### CloudTrail
* provides governancy, compliance and audit for you AWS account
* enabled by default
* Get a history of events/API calls made by SKD, CLI, Console (AWS) or AWS IAM users

### CloudTrail Insights
* Analyzes CloudTrail events and detects unusual activity
* not free

### CloudTrail Events Retention
* Events are stored for 90 days by default
* anything beyond, log to s3 and use Athena table to query the records

### X-Ray
* troubleshooting and debugging

### Service Health Dashboard
* general overview of all service health

### Personal Health Dashboard
* Shows personalized health for applications that directly impact you

<hr><hr>

## VPC and Networking

### VPC

* VPC : Virtual Private Cloud - private network to deploy your resources (regional)
* Subnets allow you to partition your network inside you VPC, tied to an AZ
* Public subnet is accessible from the internet, private is not
* Route tables define subnet access

### VPC Flow Logs
* captures info about IP trafficking going into your interfaces

### VPC Peering
* Connect to VPC privately using AWS network and make them behave as if 
  they were in the same network

### VPC Endpoints
* Provide private access to AWS Services within VPC

### NACL 
* Stateless, subnet rules for inbound and outbound

### Site to Site VPN
* Connect on-premises VPN to AWS
* goes over the public internet
* On Premises - need a Customer Gateway (CGW)
* AWS - need a VGW

### Direct Connect (DX)
* establish a physical connection between on-premises and AWS
* Goes over a private network
* takes at least a month to establish

### Transit Gateway
* Connect thousands of VPC and on-premises networks together

<hr><hr>

## Security & Compliance
### Shared Responsibility Model

#### AWS
* Responsible for the security of the cloud and protecting infrastructure

#### User
* Responsible for how products are used 

<hr>

### DDOS Attack
* Distributed Denial-of-Service
* Bots overwhelm the server and users cannot access it
* AWS Sheild Standard (free, protects layer 3 & 4 attacks SYN/UDP) and 
  Shield Advanced (24/7 
  premium, $3000 per month)
  
### AWS WAF - Web Application Firewall
* Protects web applications from common web exploits (Layer 7)
* Layer 7 = HTTP, Layer 4 = TCP
* Web ACL (Web Access Control List)

### Penetration Testing
* When you carry out security assessments on your own AWS infrastructure
* Cannot do DDoS, DoS, DNS, or Port Flooding

### KMS
* Key management service
* AWS manages the encryption keys
* Auto enabled : CloudTrail Logs, S3 Glacier, Storage Gateway
* Opt-in : EBS Volumes, S3 buckets, Redshift, RDS, EFS

### CloudHSM
* AWS provisions the encryption hardware, but you manage your own 
  encryption keys
* Uses HSM (Hardware security something)

* CMK : Customer Master Keys
  * Customer managed CMK
  * AWS managed
  * AWS owned (you cant view the keys)
  * CloudHSM Keys (custom keystore)

### Secrets Manager
* Capability to force rotation of secrets every N days

### Artifact
* Portal that provides customers with on-demand access to AWS 
  compliance documentation and AWS agreements
  
### GuardDuty
* Intelligent Threat discovery to protect AWS account

### Inspector
* Analyze the running OS against known vulnerabilities

<hr><hr>

## Machine Learning
### Rekognition
* Finds objects, people, text, scenes in images and videos using 
    Machine Learning
* Facial analysis and facial search to do user verification, people 
  counting

### Transcribe
* Converts speech into text
* Uses deep learning process called ASR automatic speech recognition

### Polly
* Turn text into lifelike speech

### Translate
* Language translation

### Lex & Connect
* Same technology that powers Alexa
* ASR
* Helps build chatbots, call center bots
* Connect : recieve calls, create contact flows, cloud-based virtual 
contact center
  
*No upfront payments

### Comprehend
* NLP Natural Language Processing
* Uses machine learning to find insights and relationships (like 
  language, tone, topic, etc.)
  
### SageMaker
* Fully managed service for devs/data scientists to build Machine 
  Learning models
  
* Difficult to do all the processes in one place

<hr><hr>

## Account Management, Billing, and Support
### Organizations (Global)
* Allows to manage multiple AWS accounts
* Consolidated billing across all accounts, single payment method
* Pooling of reserved EC2 instances for optimal savings
* API is available to automate AWS account creation
* Restrict account privileges using SCP Service Control Policies
* SCP does not allow anything by default

### Control Tower
* Easy way to setup and govern a secure and compliant multi-account AWS 
  environment without having to manually setup up permissions.
  
### Pricing
* Pay as you go
* Free : IAM, VPC, Consolidated Billing, EC2 t2.micro instance free 
    for a year
  

<hr><hr>

## Advanced Identity
### Cognito
* Provides identity for you web and mobile applications users

### Microsoft Active Directory (AD)
* Database of objects : user accounts, computers, printers, file shares,
  security groups.
  
### SSO
* Single Sign-on
* One log in for multiple accounts
* Integrates with AWS Organizations

<hr><hr>

## Other
### WorkSpaces
* DaaS (Desktop as a Service)
* Great to eliminate management of on-premise VDI (Virtual Desktop 
  Infrastruture)
  
### AppStream2.0
* Desktop Application Streaming Service
* Application streamed from within a web browser without acquiring or 
  provisioning the app
  
### Sumerian
* Create and run virtual reality (VR), augmented reality (AR) and 3D 
  applications

### IoT Core 
* Internet of Things
* Allows you to easily connect IoT devices into the cloud

### Elastic Transcoder
* 