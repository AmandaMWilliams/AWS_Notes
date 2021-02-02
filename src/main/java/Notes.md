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
* AMI (Amazon Machine Image): a template that contains software configurations
  <br><br>
* EC2 Security Groups: control how traffic is allowed into and out of EC2 instances
<br><BR>
  
#### Ports to know:
* 22 = SSH (Secure Shell) : Long into Linux instance
* 21 = FTP (File Transport Protocol) : Upload files into a file share
* 22 = SFTP (Secure File Transport Protocol) :  Upload files using SSH
* 80 = HTTP : Access unsecured websites
* 443 = HTTPS : Access secured websites
* 3389 = RDP (Remote Desktop Protocol) : Log into Windows instance

<hr>

### EC2 Shared Responsibility Model
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
