# AWS Level 1 Course Notes
#### Started Jan 27, 2021

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

