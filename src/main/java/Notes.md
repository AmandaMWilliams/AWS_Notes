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

