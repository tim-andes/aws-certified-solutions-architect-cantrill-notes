# Adrian Cantrill's AWS Certified Solutions Architect - Associate (SAA-C03) Course


# INTRODUCTION & SCENARIO

# Public Introduction - No Notes

# Course Resources
Course has GitHub Repository: https://github.com/acantril/aws-sa-associate-saac03
Walked through how to d/l Git to PC and clone repo for access.
To update to latest version: "git pull"

Walked through and recommended VS Studio Code install

# Site Tools & Features

## Quick tour of the learning platform
Products page, Slack channel, free GitHub repo: "Labs" link, mini projects in the GH repo, "More" tab for tech support

# AWS Exams / Certifications

## How to get started
Don't start with the Cloud Practitioner Foundational Cert, start with Associate level SA (Solutions Architect). The content overlaps.
After you finish SA Associate do the Role Based certs, then Specialty certs later. Get SA Professional prior to Specialties certs
- In Associate level, start with 1. SA before SysOps/Developer 2. then Developer Associate 3. then SysOps Associate (Hardest exam of the 3).
- In Professional level, tests are way harder. Longer questions, more questions. 1. Professional SA, 2. DevOps Pro exam

# Scenario - Animals4life

Animal rescue/awareness Org. Global company, 100 staff, 100 remote staff, etc etc. Small data-center is old, and data should be migrated out. 
Badly implemented AWS trial in SYD Region. Isolated Azure/GCP Pilots. All staff uses this infrastructure. Company runs lean but will get new tech
if it helps business. 
- On Premise: 192.168.10.0/24, Class C
- AWS Pilot: 10.0.0.0/16, Class B
- Azure Pilot: 172.31.0.0/16, Class B
Major offices NY, Seattle, London all use Head Office services for data
Field workers on laptop, 3g/4g/ satellite for email/files, chat/planning, research data

## Problems: Hardware failing, datacenter decommissioned in 18months, so business needs to migrate out. New investment needed, not sure if on premise, azure, aws, etc. Previous AWS/Azure attempts didn't pan out. Distance to datacenter is sub-optimal for much of company. Lean/appropriately sized, but trouble with peak traffic. IT team sucks at cloud.

## Ideal Outcomes: 
- Fast performance for all field workers
- Able to deploy into new regions quickly when required
- Low cost and scalable base infrastructure, cost close to 0 as possible while meeting reqs
- Agility - new marketing campaigns, social and progressive applications (IOT, Big Data, etc). Wants to make use of emerging technologies
- Automation - low base staffing costs

## Pay attention to which areas need more information, so you can ask the right questions.

# Connect with other students and your instructor - techstudyslack.com. Make sure you meet people in the industry--50% of jobs aren't posted anywhere.
- No better way to learn tech than help others

# Course upgrades: If you've already bought a course but want a bundle, you'll just have to pay the difference.


# COURSE FUNDAMENTALS AND AWS ACCOUNTS

## AWS Accounts
AWS Accounts are not only required to use AWS services, they are also one of the most important tools available to a solutions architect.
Many students confuse accounts with users inside the accounts. An org may use one account or many thousands. Bigger orgs generally use multiple AWS accounts.

At a high level, AWS Account is a container for Identities (users) (which you log in with) and Resources (which you provision).

When creating an AWS account you need to provide:
- Unique email address (for EACH AWS account); this creates a special type of identity: the account root user
- Provide a payment method, generally a Credit Card (No need to spend: You can choose a Free tier and create a zero-spend budget)

Root Users can only access their own accounts. Initially, it is also the only user. Root user has full control over the one specific AWS account and any resources inside it. Root user CANNOT be restricted in any way. Protect the root username and password.

### Billing 
Credit Card used to open account is the Account Payment Method. Any billable usage is charged to this CC. "Pay-as-you-go" platform. There is a free tier which we use in this course.

### Security
You can create restricted identities/users using Identity and Access Management (IAM): Users, Groups, and Roles can also be created and given FULL or LIMITED permissions. All of these ID's start off with NO access/permissions in the account. The IAM service is Account specific. Cross-account permissions are a possibility, as well (to be covered later).

### Boundary of the Account
AWS accounts are really good at containing what's inside the accounts; bad employee or bad actor, etc. Having separate AWS accounts for different uses (DEV, PROD, etc), you can limit overall damage.

By default, all access to an AWS account is denied except for the root user.

# TIP: Create new accounts for the course, don't use existing AWS accounts. The longer an AWS account exists, the more potential for configuration errors.


## DEMO: Creating the GENERAL AWS Account: https://learn.cantrill.io/courses/1820301/lectures/41301459
1. Create General AWS account (*MANAGEMENT). This account's root user will be what we log in with (root user = account specific).
2. Add root user MFA for security.
3. Create a Budget to protect against unintended costs.
4. Create an IAM user, IAMADMIN. Give permissions. Then we'll use this ID for the course.
5. Create a second accound, Production. Will also have IAMADMIN user.

## TIP: using one email for multiple accounts with Gmail. AWS accounts should be viewed as disposable, create as many as you need. Create a new account for each course. 
### TIP Example: email is catguy@gmail.com. You can use + sign in email address to create 'unique' email addresses. Ex: catguy+AWSAccount1@gmail.com, catguy+AWSAccount2@gmail.com, etc etc. This is called a Dynamic Alias.

Choose free tier AWS account after providing all account setup info (unique email, CC, verification.

Complete the prompted steps. Account will now be created.

### Account
- Always a good idea to update Alternate Contacts
- IAM User and Role Access to Billing Information, click "Edit", check Activate IAM Access
-- If this IAM box isn't checked, even an IAM ID will full admin permissions wouldn't be able to access the billing console

### Multi-Factor Authentication (MFA)
- Username and PW is step one
- MFA makes things more secure with OTP

Definition: Factors - Different pieces of evidence which prove identity

4 Common Factors:
- Knowledge (username / PW)
- Possession (debit card, MFA device, MFA app, etc)
- Inherent - Something you are: fingerprint, biometrics, etc.
- Location - Physical location, which network (corp or wifi)

More factors means more security and harder to fake. Also means less convenient. We're trying to strike a balance between security and convenience.

With AWS: 1. first, username and PW 2. MFA OTP (physical MFA or virtual via app ie. Google Authenticator)

To Activate MFA for a specific ID, like Root user, you activate MFA for that user. AWS generates secret key and other associated information (user it links to, service). All this information use all this information together to generate a QR code. Scan code using MFA app

### Securing an AWS Account
Attach MFA device to Root user.

In AWS Console... Account > Security Credentials to IAM console > locate "Assign MFA Device", follow steps.
- Log Out and test MFA login.

# REMEMBER: When setting up a new AWS account / Identity, you need to add another entry within your OTP application.

By end of this course, you should have a total of 4 virtual MFA's configured.

### Creating a Budget
Understand Free Tier and set up a budget.

AWS Free Tier: https://aws.amazon.com/free/
- Details allocations of free resources

Spend Details: Account > Billing Dashboard > click "Bills" (for spend details)

Billing Notification Preferences: Click "Billing Preferences" > check all boxes within "Invoice delivery preferences" and "Alert preferences" and Update

Create Cost Budgets: click "Budgets" > select Use a Template > select an appropriate option based on monthly spend budget (select Zero spend budget) > Budget Name "Monthly Zero Budget", enter Email Recipients for alerts ([EMAIL]+trainingawsgeneral@gmail.com) > click "Create Budget"
-- Budgets allow you to monitor spend and configure alerts when hitting spend targets

### Creating the Production Account
After creating General AWS account, we now need to create multiple AWS accounts and connect them with an AWS Organization.

#### Create Production AWS Account
Steps:
1. First, decide on email address to use [EMAIL]+trainingawsproduction1@gmail.com
2. Credit Card
3. Support Plan (Free Tier)
4. Secure AWS account with MFA to Root user of Production Account
5. Billing Preferences, check the boxes, adding email address for alerts
6. Create budget (Zero Spend Template)
7. Enable IAM User & Role Access to Billing (in Accounts)
8. Optional: Update alternate contacts in Account

### IAM (Identity and Access Management) Basics
We first need to understand the identity situation. Accounts created have Root user will have full access. AWS account and Root user can be thought of as the same thing. 

Generally, you want to give access to other people in the companies, but with restricted access -- ONLY GIVE THEM PERMISSIONS REQUIRED TO DO A JOB, called "Least Priveleged Access". 

EXAM: IAM is a GLOBALLY RESILIENT service, so any data is always secure across all AWS regions.

Any IAM's in an account are completely separate from any other accounts. IAM as a service can do as much as the Root user if given all permissions, exception being some billing stuff (but that can be activated).

Inside IAM, you can create multiple identities. 

IAM let's you create 3 types of identity objects:
- User
- Group
- Role

Users: Humans or applications that need access to your AWS account. An application that does backups of the account may also be an IAM user.

Group: Collections of related users. All dev team users, finance, HR, etc.

Roles: Can be used by AWS Services or if you want to grant external access to your account. Used to grant access to services in your account to an uncertain number of entities. Eg. If you want all EC2 instances in your account to access the Simple Storage Service (S3), you can create a role which grants access and allow instances to use that role. 

TIP: ROLES should be used when the number of entities needing access is *uncertain*.

### IAM Policy or Policy Document
Objects or documents to be used to Allow or Deny access to AWS services, only when attached to users, groups, or roles.

### High Level IAM
IAM has 3 main jobs:
1. IDP (ID Provider): Manages identities
2. Authentication Process: Authenticates identities (when anyone makes request to AWS, they're known as a Security Principle--they must prove their identity)
3. Authorization: Allowed or Denied access to resources. This is based on Policies associated with the identity that is authenticated with.

### Other IAM Key Points
- No cost for IAM
- Global service / Global Resilience (copes with failure of large parts of the AWS system)
- IAM only controls what its identities can do. Allow or Deny identities in account
- No direct control on external accounts or users. It only controls local accounts or users
- Identity federation (to be covered later) and MFA

Next, we'll create an IAM account with full permissions to take the place of the Root user. Root users should generally only be used to create an account. Afterward, best practice is to utilize an IAM User rather than account root user. We'll use this IAM user to create new identities with less permissions (only enough for the user to do a certain task)

## DEMO Adding an IAM Admin to GENERAL ACCOUNT
Set up AIM ID with Admin permissions

Search "IAM" > IAM Dashboard

To sign on with IAM identities, use sign-in URL: http://[account-id].signin.aws.amazon.com/console. 
-- To make friendlier URL, set alias.

### To set alias, make it globablly unique. 
1. Within IAM Dashboard, find right-side AWS Account info, find "Account Alias", click "Create".
- Must be a globablly unique ID. I am using "ta-cantrill-training-aws-general"
-- Now URL is https://ta-cantrill-training-aws-general.signin.aws.amazon.com/console

### Create IAM Admin ID
IAM Dashboard > left sidebar "Users" > Create user "iamadmin"
- Give Access to Console
- Create an IAM user (2nd option, 1st option to be covered later)
- Custom PW
- Give admin permissions "Attach policies directly" > check "AdministratorAccess"
- Create user
- Test login
- Confirm login with profile dropdown that will show account name
- Secure admin account with OTP > Security Credentials > Assign MFA
- Log out and test OTP

## DEMO Adding an IAM Admin to PRODUCTION ACCOUNT
Same as previous section.

## IAM Access Keys
Access AWS via command line or APIs. This is done using IAM access keys.

### IAM Access Keys
- long term credential (don't change or rotate regularly)
- IAM user has 1 username and 1 PW (cannot have more than 1). Password on IAM user is actually optional.
- Credential Leak: If someone knows your username (public) and password (private)
- Unlike username/PW, IAM user can have TWO access keys
- Access key actions: create, delete, made inactive, made active. Default: Active state
- Access keys are formed from two parts: 
1) Access Key ID 
2) Secret Access Key
--AWS provides both when key is created.
- Once the key is generated, you CANNOT access the Secret Access Key part again
- If leaked/lost, you need to delete ID and Secret Access Key and recreate completely
- If made inactive or deleted, CLI will stop working until re-active or new key is created
- Rotating Access Keys: delete old one make new one and replace old one
- NOT recommended: Don't give Root user Access Keys
- IAM Roles DO NOT use access keys

## DEMO Creating Access Keys and Setting Up AWS CLI v2 Tools

Once logged in with Admin user:
IAM Dropdown > Security Credentials > scroll down to "Create Access Key", click > Command Line Interface (CLI) > check box at bottom > Next > Set Decription Tag > "Create Access Key"

Once Access Key is created, you can use Actions dropdown to Deactivate, Activate, and Delete. If you ever lose access to a key, you need to deactivate & delete it, then create a new one.

### Download AWS CLI v2 
AWS CLI v2 (Windows) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html

AWS CLI v2 (macOS) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

AWS CLI v2 (Linux) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html

### Configure CLI
Configure a set of credentials which CLI will use to communicate with AWS. We will use the General IAMADMIN user for this one.

COMMAND: 'aws configure': configures default profile for CLI
COMMAND: 'aws configure --profile iamadmin-general' / 'aws configure --profile iamadmin-production': named profile for CLI

Upon entering the above Command:
- AWS Access Key ID
- AWS Secret Key
- Default Region Name: us-east-1
- Default output format (press Enter with blank field for default)

Test that this is successful with COMMAND 'aws s3 ls --profile [CLI profile name]'. This will error first as we need to specify named profile:
'aws s3 ls --profile iamadmin-general', which will currently return a blank string as there are no s3 buckets.

#### Configure for Production
COMMAND: 'aws configure --profile iamadmin-production'
COMMAND to test: 'aws s3 ls --profile iamadmin-production'

SECURITY REMINDER: Never share your SECRET KEY. If leaked, delete and create new set of keys and re-configure in CLI

TIP: If after you Configure CLI with credentials, you can delete the credential files (CSVs)


## AWS FUNDAMENTALS

### AWS Public VS Private Services
Architecture of both Public/Private Services. "Private"/"Public" refer to networking only. Private runs within VPC, Public is S3
- Both require Permissions / Configuration
3 Zones:
- 1. Public Internet Zone
- 2. AWS Private Zone: VPC's are Virtual Private Clouds. VPCs are isolated unless configured otherwise; can attach IGW (internet gateway) for access to internet
- 3. AWS Public Zone (runs between Public and Private zones). It's a network connected to the Public internet

#### AWS Public Service: What is true of an AWS Public Service? 1. Located in the AWS Public Zone 2. Anyone can connect, but permissions are required to access the service
#### AWS Private Service: What is true of an AWS Private Service? 1. Located in a VPC 2. Accessibly from the VPC it is located in 3. Accessible from other VPCs or on-premise networks as long as private networking is configured


### AWS Global Infrastructure
AWS have created a global public cloud platform which consists of isolated 'regions' connected together by high speed global networking.

Two types of Deployment at global level: 1) AWS Regions, 2) AWS Edge Locations (doesn't directly map to continent or country)
#### AWS Region: Geographically spread. Full compute, storage, DB, AI, Analytics
-- Three main benefits
--- 1. Geographically separate for physical reslience. Isolated Fault Domain
--- 2. Geopolitical Separation. Different governance
--- 3. Location Control. Performance
-- Inside regions: You can use Region Code or Region Name. Eg Sygney Australia. RC: ap-southeast-2, RN: Asia Pacific (Sydney)

#### AWS Availability Zone (AZ)
AZ's are located inside regions. Eg. for Sydney AU: ap-southeast-2a, ap-southeast-2b, ap-southeast-2c. If an issue is only in 1 availability zone (AZ), you'll still have functioning services in the other AZs

#### AWS Edge Location: Local distribution points closest to user. Content distribution services, edge computing. Eg. Netflix storing content close as possible to user. Edge locations for fast/efficient data transfer because they're closer to the user. Uses CloudFront

#### AWS AZ VS Edge Location
An Availability Zone is an isolated location within an AWS region. An edge location delivers cached content to the closest location to reduce latency for users.

NOTE: Visit: infrastructure.aws

Service Resilience 
- Globally Resilient: Operates globally with a single DB and replicated across multiple regions. World would need to fail to experience a full outage here. Eg. IAM
- Regionally Resilient: Operate in single region with one dataset in a region. Replicate data to AZs for resilience.
- Availability Zone Resilient: Prone to failure as they have less redundancies.

### AWS Default Virtual Private Cloud (VPC)
A Virtual Network inside AWS. VPCs are regional services; regionally resilient. They operate from multiple AZ's in a region. 
- A VPC is 1 account and 1 region, cann't be spread across multiple accounts/regions
- Private and isolated unless configured otherwise
- Default VPC (max 1 per region, pre-configured) and Custom VPCs (can have many)
- Can be used to connect AWS private networks to on-premise network. Or connecting during multi-cloud deployments

EXAM: VPCs are REGIONALLY resilient

#### Default VPC
There can only be one default VPC per region, and they can be deleted and recreated from the console UI. Unless configured otherwise, VPC is entirely private/isolated. 
- VPC CIDR: Start and end range of IP addresses VPC can use. If anything needs (and is allowed to) communicate with VPC, it needs to communicate to the VPC CIDR
- Default VPC only gets 1 CIDR IP range. Can't change it.
- Default VPC provides Internet Gateway (IGW), Security Group, and NACL
- VPC can be subdivided into subnetworks. Each subnet in VPC is located in one AZ. Default VPC has one subnet in each AZ by default
-- Each subnet uses part of the VPC CIDR range
-- Default VPC CIDR: always 172.31.0.0/16
-- Assigns public IPv4 addresses
--- /20 subnet in each AZ in the region. The higher the /#, the smaller the network. /17 is half the size of /16

QUIZ: How many subnets are in a default VPC? Default VPCs always have the same IP range and same '1 subnet per AZ' architecture. # Subnets = # AZ's in region

EXAM: Default VPC CIDR IP? 172.31.0.0/16

##### Default VPC - Create / Delete

To Locate: AWS Dashboard > Search "VPC" > Your VPCs

To Delete: check Default VPC > actions dropdown "Delete" > follow prompt

To Create Default VPC: If you've deleted Default VPC. In Your VPCs > Actions dropdown > Create Default VPC

### Elastic Compute Cloud (EC2) Basics
Basically the default compute service of AWS. It allows you to provision Virtual Machines known as Instances with resources you select and an operating system of your choosing.
- EC2 is IaaS, Infrastructure-as-a-service. Unit of consumption is the Instance. Instance is a configured O/S
- Private service by default, uses VPC networking
- Public access must be configured. The VPC it's running within must support Public access (if using custom VPC, you need to configure this in VPC)
- EC2 is AZ Resilient
- When launching an Instance, you can choose size and capability
- On-Demand Billing, by second or hour
- Storage Types: Local on-host storage, or network storage via Elastic Block Store (EBS)
- By default, AWS has a [soft] limit of 20 instances per region

EXAM: EC2 is AVAILABILITY ZONE resilient

#### EC2 instance has attribute called State
States to Know: Running, Stopped, Terminated
- When instance is launched and provisioned, it moves to Running. If instance is shut down, it is Stopped
- Instance can be terminated, but this cannot be reversed

These States influence the charges for an instance. 
- Stopped instance uses less resources, therefore less expensive. You won't be charged for "running" the instance
- Regardless of Running or Stopped, storage is still allocated and you'll still be charged for EBS storage even if instance is stopped
- To guarantee 0 cost on instance, you must Terminate. Termination is irreversible

#### Components for instance charge: running the instance, storage the instance uses, extras for any commercial software the instance is launched with

#### AMI: Amazon Machine Image
Image of an EC2 instance
- Can create EC2 instance
- Can be created FROM an EC2 instance

##### AMI contains attached permissions. Controls which accts can/can't use AMI:
- Public Type - Everyone allowed
- Owner - Implicit Allow
- Explicit - Allow specific AWS accounts

##### AMI includes the following:
- One or more Amazon Elastic Block Store (Amazon EBS) snapshots, or, for instance-store-backed AMIs, a template for the root volume of the instance (for example, an operating system, an application server, and applications).
- Launch permissions that control which AWS accounts can use the AMI to launch instances.
- A block device mapping that specifies the volumes to attach to the instance when it's launched.

##### NOT stored in AMI:
- Instance Settings
- Network Settings

EXAM: What is NOT stored in an AMI? Instance and Network Settings

Root Volume: AMI contains boot volume of instance, boots O/S

Block Device Mapping: Config that links volumes that AMI has and how they're presented to O/S. Ie. Which is boot volume, which is data volume

#### Connecting to EC2: 
- Connect to Windows instances using RDP (Remote Desktop Protocol), port 3389
- Connect to Linux distros use SSH protocol, port 22. Log in using SSH key pair

### DEMO: Create an EC2 Instance
https://learn.cantrill.io/courses/1820301/lectures/41301621
1. Create SSH Key Pair: Navigate to EC2 Console (search bar) > left sidebar > Network & Security > Key Pairs) > click "Create Key Pair"
- Note: For creating key pair, Private key file format choises are .pem and .ppk. For MacOS/Linux, always use .pem, if using modern Windows you can choose .pem. Older Windows or Putty terminal app, choose .ppk
2. Configure: Left sidebar "Instances" > click "Launch Instances" > select O/S (Amazon Linux) > select keypair login (A4L) > Network Settings: select Create Security Group > name/description "MyFirstInstanceSG" > leave Inbound security groups rules as defaults > Launch EC2 Instance

### DEMO: Connect to Terminal of an EC2 Instance
1. In EC2 Dashboard, Right Click your EC2 instance, select "Connect" > SSH Client
2. Open your local Terminal / Command Prompt and change directories to wherever your SSH private file key is (likely Downloads, it's a .pem file created previously)
3. Copy the command at the bottom of the SSH Client tab "ssh -i "A4L.pem" ec2-user@ec2-54-89-175-122.compute-1.amazonaws.com", verify fingerprint with "yes"
- Note: If using MacOS/Linux and "Permission Denied": paste in terminal "chmod 400 A4L.pem"
- More key file permissions help: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-private-key

### S3 Basics: Simple Storage Service
Global Storage Platform - regional based/resilient. Access from anywhere.
- Public service, can cope with unlimited data & multi-users
- Perfect for hosting large amounts of data
- Economical and accessed via UI/CLI/API/HTTP

#### S3 Delivers 2 things: Objects and Buckets

##### S3 Objects
What is an Object? An object is a file and any optional metadata that describes the file.

Two components and some associated metadata: 
1. Object Key. identifies object in a bucket
2. Value. data or contents of the object. Object size can range from 0 bytes to 5 terabytes (TB) in size.
Metadata: Version ID, Metadata, access control, subresources

NOTE: S3 = Default Storage Service in AWS

##### S3 Buckets (Simple Storage Service)
Containers created in a specific AWS region; default place to go to in order to configure S3
- Data inside a bucket has a primary home region. Never leaves this region unless configured to do so
- Blast radius of a failure is limited to a region
- Buckets can hold an unlimited number of objects; infinitely scalable
- S3 bucket has no complex structure; flat-structure; everything stored at same level; all stored at Root level (if you list out on Command, it'll look like there are folders, but there aren't Eg. /old/photo1.jpg). Folders are called 'prefixes' in S3.


# EXAM: Bucket name must be Globally Unique. Error where you can't create a bucket? Prolly not a unique name

# EXAM: More bucket name restrictions: 3-63 characters, all lowercase, no underscores, not formatted like IP addresses

# EXAM: Bucket limits: soft limit of 100 buckets per AWS account, hard limit of 1000 buckets (hard limit increased by connecting with Support). If you have more than 1000 users, you can't use 1 bucket per user, but you can use prefixes within a bucket to let multiple users use one bucket.

# EXAM: Unlimited Objects in a bucket, ranging from 0 bytes to 5TB in size

# EXAM: Object Structure: Key = Name, Value = Data

#### S3 Patterns and Anti-Patterns
- S3 is an Object Store system, NOT File System and NOT Block System
- S3 has no File System, it's flat. It's not Block storage, so you can't mount it as K:\ or /images
- Great for 'offload'
- S3 should be your default INPUT and/or OUTPUT to MANY AWS products

# EXAM: Where to store data in AWS? S3 should be default answer 

# QUIZ: What is true of Simple Storage Service (S3)
- S3 is an AWS Public Service
- S3 is an Object Storage System
- Buckets can store an unlimited amount of data

### DEMO: Creating an S3 Bucket
Create, interact with bucket, upload to bucket, interact with uploaded objects
- As S3 is Global, you can't select a Region in advance

STEPS: Move to S3 Console > click 'Create bucket' > name 'koalacampaign987654123' (must be globally unique) > select Region (default N.VA) > untick "Block *all* Public Access (this just enables you to Enable public access later) > click "Create Bucket" 

#### Amazon Resource Name (ARN): All resources in AWS have a unique identifier, the ARN. 
To see bucket ARN, Amazon S3 > Buckets > click the bucket you want > 'Properties' tab > Amazon Resource Name 

#### DEMO: Upload files to Bucket
Amazon S3 > Buckets > click the bucket you want > Objects, click Upload > Select Files > Use default settings > click Upload
- Now, you'll see these files in the Object tab

Note on creating a folder: it doesn't actually create a folder, it creates an object that appears to be a folder. They are just emulated using prefixes Eg. archive/koalazzz.jpg -> Not actually a file, but named to look like it
- Without versioning enabled, same name files can overwrite each other. With Versioning, they can't

#### DEMO: Delete Buckets in S3
Two step process:
1. Empty the bucket > select Bucket, click Empty
2. Re-select Bucket, click Delete

### CloudFormation (CFN) Basics
A tool which lets you create, update, delete infrastructure in AWS using Templates
- At its base, CFN uses templates. Can create/update/delete templates
- Template written in YAML or JSON

From the Documentation: AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you

#### What makes a template? Components:
- All templates have a list of resources. This is the only mandatory item 
- Description. Free text field for the author to provide details on template. (If you have AWSTemplateFormatVersion, Description MUST follow it in YAML/JSON
- Metadata. Can control the UI (groupings, order, labels, descriptions), as well as other things (to be covered later)
- Parameters. Value parameters, default values, etc.
- Mappings. Create lookup tables.
- Conditions. Allows decision making in the template. Step 1 create condition, Step 2 use condition 
- Outputs. Once template is finished it can present outputs like admin or setup adddress, instance ID

#### How does CFN use Templates?
Eg. Template that creates EC2 resource. Resources defined in CFN Templates are called Logical Resources. 
- When template is given to CFN, CFN creates a stack which is a living and active representation of a Template. Stack is created with CFN does something with a template.
- For any logical resources in the stack, CFN makes a corresponding physical resourse in your AWS account. It's CFNs job to keep logical and physical resources in sync. Physical resource: A resource created by creating a CloudFormation Stack
- If you delete a CFN Stack, its logical resources are deleted and CFN subsequently deletes the physical resources

# EXAM: In a CFN Template, if you have the AWSTemplateFormatVersion item, the Description MUST follow directly after in your YAML/JSON template file

### DEMO: Simple Automation w/ CFN; Creating EC2 with CFN

"CloudFormation" or CFN in Search > click "Create Stack" > Template is ready > Upload a Template File > use Demo file (ec2instance.yaml) > click "Next" > Name: "cnfdemo1" > leave the rest default > "Next" > skip config "Next" > Review cfndemo1: Capabilities, check the box 
- Template auto-creates an s3 bucket when you upload a Template
- YAML file: 
-- LatestAmiID: Instead of giving latest AMI ID, you can make Type a "latest version" AMI
-- CloudFormation Functions are used within YAML Outputs to get values like InstanceID, Availability Zone (AZ), Public IP of EC2, etc. Eg. !Ref, !GetAtt
-- Resources Component is the main one in the file. In this temmplate, an instance role and instance role profile are being created (SessionManagerRole, SessionManagerInstanceProfile) -- covered later. 
-- Also being created in the Resources portion of the template: EC2 instance, InstanceSecurityGroup. Port 22 (SSH)/Port 80 (HTTP)
-- Resources: EC2Instance: Properties: InstanceType: "t2.micro" -- Free tier elligible
- After Submitting stack to be created, you'll see that each Resource being created is done so by an Event, "CREATE_IN_PROGRESS", "CREATE_COMPLETE". This whole process takes some time before all of cnfdemo1 is showing CREATE_COMPLETE

#### EC2 Session Manager: EC2 Dashboard > Connect to Instance > Session Manager
- No need to SSH in now
- Two logical resources in YAML template configure this ability


## CloudWatch Basics
CloudWatch is a core supporting service within AWS which provides metric, log and event management services. Collects / manages operational data on your behalf.

### Three jobs:
1. Metrics. AWS Products, Apps, on-premises. Some metrics require extra installed CloudWatch Agent
2. CloudWatch Logs. AWS Products, Apps, on-premises. Almost anything logged can be ingested by Logs
3. CloudWatch Events. AWS Services & Schedules. If an AWS service does something, this will generate an event that can perform another action. Or you can set up a chrono-repeating event through here.

### Core Concepts
- Namespace: Container for monitoring data. There is a naming ruleset for naming. All AWS data foes into a special namespace AWS/[service]
- Metric: Collection of related data points in a time-ordered structure
- Datapoints: A single unit of a metric; consists of timestamp and a value
- Dimensions: Generally, a metric is a collection (Eg. CPU utilization comes from all EC2 instances, not just one). You can use dimensions to single out resources to see their individual metrics. "Separate datapoints for different things or perspectives within the same metric"
- Alarms: Taking actions based on metrics. States: OK or ALARM (ALARM can be SNS Notification or Action), and INSUFFICIENT DATA (when there's not yet enough data)


## DEMO: Monitoring with CloudWatch
https://learn.cantrill.io/courses/1820301/lectures/41301629
1. Create EC2 Instance: Nav to EC2 service > Launch Instance Defaults for all, but you can pay to Enable Detailed CloudWatch Monitoring
2. Create CloudWatch alarm: Nav to CloudWatch dashboard > All Alarms > Create Alarm
3. Select Metric > EC2 > Browse Tab (make sure you know last 4 of Instance ID number) > Last 4 of ID number, check box for CPUUTilization metric
4. Metrics / Contitions: Conditions: Static, Whenever CPU Util is Greater/Equal 15% > "Next" > Remove Notification > Alarm Name "cloudwatchtestHIGHCPU" > Next/Create Alarm
5. Back to EC2, connect to EC2 with Instance Connect
6. Need to install Stress app > command: sudo yum install stress -y
7. Stress Test: command: stress -c 1 -t 3600. Make sure CloudWatch alarm is OK status before entering this command. 
8. Clean up: Delete CloudWatch Alarm and Terminate EC2 instance. Delete EC2 Security Group 

Detailed CloudWatch Monitoring: Enables you to monitor, collect, and analyze metrics about your instances through Amazon CloudWatch. Additional charges apply if enabled. If no value is specified the value of the source template will still be used. If the template value is not specified then the default API value will be used.


## Shared Responsibility Model
Vendor and User shared responsibilities. This applies from a security perspective so you know which elements you and the vendor manage.
- Customer is responsible for security 'in' the cloud: client-side data encryption, server-side encryption, networking traffic protection, O/S, platform, IAM, apps
- AWS responsible for security 'of' the cloud 


## High-Availability (HA) vs Fault-Tolerance (FT) vs Disaster Recovery (DR)
### High-Availablily - Aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period. Doesn't aim to stop failure, but online and providing services as often as possible. Fix should be as quick as possible, often with automation to bring systems back into service quickly; maximizing a system's online time.
- System availability is in the form of percentage uptime. Three 9's -- Up 99.9% of the time==8.77 hours/year downtime. Five 9's==5.26 minutes/year down time
- Costs required to implement: design decisions and automation
### Fault Tolerance - The property that enables a system to continue operating properly in the event of the failure of some (one or more faults within) of its components. Fault tolerance systems work through failure with no disruption; operating through failure.
- Cost of fault tolerance can be expensive because of redundancies and failure toleration via duplicate system components
- Example: Plane operates with Fault Tolerance (more engines, electronic systems etc); can't tolerate failure in flight
### Disaster Recovery - Post-disaster recovery plan. A set of policies, tools, and procedures to enable recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster. When disaster occurs, you want to avoiding losing irreplaceable items.


## Route53 (R53) Fundamentals
AWS's managed DNS product. Global service, single database; no need to pick region in console UI. Globally resilient.

### R53: Two main services:
1. Register Domains
2. Host Zones... managed nameservers

### R53: Architecture
Register domains. To do this, it has relationships with all major domain registries (.com, .io, .net, etc)
1. Check if domain available 2. Zone File created for registering domain (DNS DB for domain) 3. Allocates managed nameservers for this zone (usually 4). get nameserver records added to top level domain zone

### R53: Zones
DNS Zones and Hosting for those zones. Hosted zone created if domain available (and allocates 4 NS's to host zone). HZ can be Public or Private (linked to VPCs, for sensitive DNS records). Hosted Zones stores records (recordsets).

## DEMO: R53 Register Domain - animals4life.org
Search / Nav to R53 console > Registered Domains > click "Register Domains" > Search for domain > Select domain you want > Proceed to Checkout (choose duration, auto-renew) > fill out Contact Info > Pricing (up front cost + monthly hosted fee) > click "Submit" > await domain registry
- Transfer Lock: Security feature, domain can't be transferred away from R53 without disabling this lock
- If you delete and recreate HZ, you'll be allocated 4 new Name Servers (would need to update some stuff if you weren't using R5#)


## DNS Record Types
- Nameserver Records (NS). Allows delegation to occur in DNS. Eg. .com zone
- A Records / AAAA Records. Map host names to IP addresses. A record = IPv4, AAAA = IPv6
- CNAME Record. Canonical name. Let's you create equivalent of DNS shortcuts; host-to-host records. CNAMEs reduce admin overhead. 
- MX Record. For email. How a server can find the mail server (SMTP) for a specific domain.
- TXT Records. Add arbitrary text to a domain; add additional functionality. Eg. Prove domain ownership. 

EXAM: CNAMEs cannot point directly at an IP address, only other names.

QUIZ: What is a CloudFormation Logical Resource? A resource defined in a CFN Template
QUIZ: How many DNS Root Servers Exist? 13
QUIZ: Who manages DNS Root Servers? 12 Large Organizations
QUIZ: Who manages DNS Root Zone? IANA
QUIZ: A Record = IPv4, AAAA Record = IPv6
QUIZ: DNS Record type is how the root zone delegates control of .org to the .org registry
QUIZ: Which type of organization maintains the zones for a TLD (e.g .ORG)? Registry
QUIZ: Which type of organization has relationships with the .org TLD zone manager allowing domain registration? Registrar
QUIZ: How many subnets in a default VPC? Equal to the number of Availability Zones in the region the VPC in located in

### TTL - Time To Live
Numeric value that can be set on DNS records. Getting result from authoritative source is an authoritative answer. If a 3600 TTL value is set, results of query are stored in resolver server for 3600 seconds (1 hour), creating a non-authoritative answer for delivery -- during this time, another query would receive this cached non-authoritative answer.
- Low value means more queries against your server. High value less queries but less control
- TIP: If doing any work to change DNS values, it's recommended that you lower the TTL value in advance (days/weeks in advance)


## IAM Identity Policies
Policies attached to identities in AWS. 
1. Understand their architecture 2. Gain ability to read/understand a policy 3. Learn to read/write your own

IAM Policy is a set of security statements to AWS, granting or denying product/features. 
- IAM Identity Policy Document: 1 or more statements, created using JSON
-- Statement Id or Sid: Let's you identify a statement and what it does
-- Action: Can be specific individual action, a wild card, or list of multiple independent actions
-- Resources: Wild cards, lists of individual resources (using ARN name)
-- Effect: Allow or Deny

NOTE: Action and Resource within IAM Policy must match for statement to execute.

### How to Handle Overlap Type Situations
Priorities:
1. Explicit DENY: Overrules everything.
2. Explicit ALLOW: Allows access to all actions on any S3 resource (overrules all but Explicit DENY).
3. Default DENY (Implicit): No explicit DENY or ALLOW, so this takes effect. IAM ID's are generally restricted access by default.
- DENY (explicit), ALLOW (explicit), DENY (implicit)

### Three types of Policies
- 1. Inline Policies - JSON policies applied to each IAM account individually. (Manually applying policies to each Identity)
- Managed Policies - Created as their own object. You can attach this policy to more than one identity. Best for Common Access Rights
-- 2. AWS managed or 3. Customer managed
-- Reusable
-- Low Management Overhead
When to use Inline Policies? For Special or exceptional Allows or Deny's


## IAM Users and ARNs (Amazon Resource Name)
### IAM Users: An identity used for anything requiring long-term AWS access eg. Humans, apps, service accounts. If you can picture one thing; named thing, 99% of the time use IAM
- Starts with the principal; an entity trying to access AWS account (ppl, svc, group of  these_
- Authenticate principal. Principal needs to prove identity against IAM (using Username/PW (humans usually) or Access Keys (app or human in CLI))
- Principal becomes Authenticated Identity
- Authorization for actions via IAM Policy (statements)

### ARN (Amazon Resource Name):
Uniquely identify resources within any AWS accounts. ARNs are used in IAM policies and have a defined format

### ARN Format
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id

Note: s3 is globally unique, so no need to specify region...
arn:aws:s3:::catgifs -> references s3 bucket ITSELF
arn:aws:s3:::catgifs/* -> references objects IN the bucket (thse two ARNs do not overlap)

# EXAM: MAX 5,000 IAM Users per account
# EXAM: IAM User can be a member of 10 groups maximum
System with more than 5,000 identities? Can't use IAM user for each identity. IAM Roles & Identity Federation fixes this (more later)


## DEMO - Simple Identity Permissions Policies in AWS
Assign some permissions to an IAM identity
- 1-click deployment https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0052-aws-mixed-iam-simplepermissions/demo_cfn.yaml&stackName=IAM
-- Create IAM user Sally and two s3 buckets

IAM PW - Min. 8 characters. Uppercase, lowercase, numbers

Steps:
1. open first link, create PW, create stack
2. Login to new IAM Sally with incognito window, change PW, check ec2 and s3 that the permissions are limited
3. Using the lesson's attached .zip, open s3_fulladmin.json and copy the code to clipboard
4. In ADMIN account > IAM dashboard > User: Sally > Permissions > "Add permissions" > Create inline policy > JSON tab, paste copied text > name "s3admininline" and click "Create policy"
5. In s3, you can prove permissions by uploading merlin/thor.jpg through Sally IAM account

### DEMO - Delete all CFN / IAM info above
1. Delete Managed Policy: IAM > Users > Sally > Permissions > remove "AllsAllS3ExceptCats"
2. s3 > select "catpics"/"animalpics" buckets > click "Empty" > type "permanently delete", submit
3. CFN > Stacks > Delete Stack. NOTE: If you don't see this stack, check your region to make sure youre in N.Virginia


## IAM Groups
IAM groups are containers for IAM users. Makes managing IAM users easier.
- Groups can have both Inline and Managed policies attached
- Soft limit: 300 Groups per account (you can get Support to increase this)
- Groups are NOT a True Identity; they can't be referenced as a PRINCIPAL in a policy (you can grant access to users, not groups)
- Can hold Identity Permissions

EXAM: You can't login to IAM Groups; no credentials/login of their own
EXAM: IAM User can be a member of up to 10 IAM Groups (hard limit)
EXAM: AWS Account has a 5,000 IAM user limit (hard limit)
- There is no effective limit for the number of Users in a single IAM Group
EXAM: There is no "All Members" group by default. In IAM, you could create and add all Users to a group
EXAM: Groups CANNOT have nesting. No Groups within Groups
EXAM: Groups are NOT a True Identity; they can't be referenced as a PRINCIPAL in a policy (you can grant access to users, not groups)

Eg. If Sally is a part of 2 IAM Groups, each with an attached policy, and she has an attached policy, she has 3 policies which become Merged Policies
- For figuring out overlapping, combined all policies and tally Allows/Deny's and undergo the same DENY-ALLOW-DENY pattern

### Resource Policy: Controls access to a specific resource, allowing/denying identities to access that bucket. Does this by referencing this ID's with ARNs


## DEMO - Permissions control using IAM Groups
How groups can be used to hold permissions for group members

1. After prep steps complete, remove catpic permissions from Sally IAM > Users > Sally > Permissions > check cat Policy, "Remove"
2. IAM > User Groups > click "Create group" > name "developers" > select policy name "IAMGROUPS-AllowAllS3ExceptCats-7OLPCURC1UQF"
3. IAM > User Groups > tab Users > Add Users > select Sally > Add Users

### IAM Groups DEMO: Tidy Up:
1. IAM > User Groups > Developers > Remove AllowAllS3ExceptCats policy
2. IAM > Users Groups > delete Developers
3. Empy s3 Buckets . s3 > Buckets > click and Empty cat/animals buckets
4. CloudFormation > Stacks > delete IAMGROUPS


## IAM Roles - The Tech
- Principal: Physical person, app, device, or process which wants to Authenticate with AWS.
- IAM User: If you can think of a single entity as a principal, then prolly use IAM User
- IAM Roles: If you don't know the number of principals. Or more than 5,000 principals.
- A Role doesn't represent 'you', it represents a level of access inside an AWS account. Permissions borrowed for a short period of time
- Roles can be referenced within Resource Policies.

### IAM Roles Policies - Two Types
1. Trust Policy - The trust policy specifies which trusted account members are allowed to assume the role.
2. Permissions Policy - The permissions policy grants the user of the role the needed permissions to carry out the intended tasks on the resource. 
- Temporary Security Credentials: Given when a Role gets assumed by something that is allowed to assume it. These are like access keys, but time limited.
-- Generated by STS, Secure Token Service. "sts:AssumeRole"
-- Checked against Permissions Policy


## IAM Roles: When to use IAM Roles
Examples for selecting when and when to not use IAM Roles.

- Example 1. Common use of Roles are for AWS Services themselves
-- Eg. AWS Lambda. Lambda function has no permissions by default, so it needs permissions to do things when it runs. Running Lambda Function is called "function invocation"/"function execution". We need to give this function permissions with access keys and there's a better way than hardcoding keys into script. To provide these permissions, we create an IAM Role called "Lambda Execution Role", which has a Trust Policy/Permissions Policy
-- This is good for a role because you'd have to hardcode into the function otherwise (security risk/update issues). Roles provide TSC (Temp security credentials)
-- For a given Lambda Function, you could have 0 to unknown number of copies running. Therefore, it makes sense to be a Role.

- Example 2. Emergency or out-of-the-usual situations
-- Eg. Group Helpdesk team given Read-Only access to a customer's AWS account to watch performance. Anything past read-only handled by a Senior team. However, if a customer calls at a time when Senior team is unavailable, the Helpdesk team may need more than read-only; Break Glass Situation. "Break glass for excepted access".
-- An emergency role can be assumed when Helpdesk user needs to "Break glass for more than read-only access"

- Example 3. Adding AWS to existing corporate environment
-- Eg. You have an existing physical network with an existing identity provider, Microsoft Active Directory. External Accounts / Identities cannot be used to directly access AWS Resources. For a corporate with more than 5,000 staff, you can't assign each employee an IAM (MAX 5000). Roles can re-use IAM Users
-- Allow IAM Role to be assumed by one of the External Entities (the identities in Microsoft Active Directory)
--- When Role is assumed, Temporary Security Credentials are used

TERM: ID Federation: Giving permissions to an external ID provider and allowing externals to assume a Role
TERM: Web Identity Federation. Eg. When you are given the option to login with Google, Facebook, etc (these are Web Identities), then use these to assume an IAM Role for AWS access.
-- Advantages: No AWS credentials on the external entity. Makes use of existing accounts. Scales to hundreds of millions of users and beyond.

EXAM: How you can architect solutions that will work for mobile apps: Use ID Federation
EXAM: External Accounts / External Identities cannot be used to directly access AWS Resources. They must assume a Role to gain access.

### IAM Roles: When to use Roles: Cross-Account Access
Eg. Two AWS accounts. Your Account and Partner Account
- Your account offers an application which processes scientific data and they want you to store data in Partner Account's s3 bucket. Your account has 1000s of ID's and they don't want this data in their account.  
- In this situation, use a Role in the Partner Account. Any objects uploaded by this Role into the Partner Account means the Partner Account owns these objects
- Roles can be used cross-account to access individual resources, or access to whole accounts


## Service-linked Roles (SLR) & PassRole (PR)
A service-linked role is a unique type of IAM role that is linked directly to an AWS service. Service-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf. The linked service also defines how you create, modify, and delete a service-linked role. A service might automatically create or delete the role. It might allow you to create, modify, or delete the role as part of a wizard or process in the service. Or it might require that you use IAM to create or delete the role.

### SLR: Key Difference between SLR and normal IAM Roles
- You can't delete a service linked role until it's no longer required / used within that AWS service

### SLR: Permissions needed to create - Policy
Key elements: top statement is Allow, action iam:CreateServiceLinkedRole, resource is NOT guessable--see link below
- https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html

### SLR: Role Separation
One group given ability to create roles, other group gets ability to use the SL Role

### PR: PassRole Permissions
To use pre-existing role with a service without having to create / edit a new role, you need to provide PassRole Permissions.

To pass a role (and its permissions) to an AWS service, a user must have permissions to pass the role to the service. This helps administrators ensure that only approved users can configure a service with a role that grants permissions. To allow a user to pass a role to an AWS service, you must grant the PassRole permission to the user's IAM user, role, or group.
- "Pass the role permissions" 
- A method inside AWS that gives you the ability to implement Role Separation
-- An important AWS security architecture


## AWS Organizations
A product that allows larger businesses to manage multiple AWS accounts in a cost-effective way with little to no management overhead

Large orgs need to manage many AWS accounts (100s or more). Without AWS Orgz, these accounts would each have their own pool of IAM users and separate payment methods. Beyond 5-10 accounts, this becomes unwieldy.

### AWS Org - How it's created
First, take a single / standard AWS account (not within an org) and with this create an AWS Organization. The Org isn't created IN the account, you're just using the account to create the AWS Org. This standard AWS account that created the Org then becomes the Management Account for the org (previously Master Account).

Using this management account, you can invite other standard AWS Accounts into the org. As they are existing accounts, they need to approve the Org invites. If they approve, they become part of the Org. Once these Standard Accounts join the Org, they become Member Accounts

### AWS Org - Hierarchy of Containers (which contain Members and other containers)
Structure in AWS Orgs is hierarchical (upside-down tree). Top of hierarchy is Root Container of Organization (not to be confused with Account Root User)--this is a container for AWS Accounts, Mgmt and Member Accounts. This Org Root container also can contain other containers, known as Organizational Units (OU's): can contain AWS accounts or other Organizational Units

#### Types of Accounts relating to AWS Orgs
- Management Account / Master Account. Account that created the AWS Organization and invites Account Members
- Standard Account. A standard AWS account that is not part of an AWS Org
- Member Account. A standard AWS account that joined an AWS Org
NOTE: Only ONE Management Account per AWS Org

### AWS Org - Management Account
- Only ONE Management Account per AWS Org
- Account that creates the Org
- Account that handles Consolidated Billing

#### AWS Org - Consolidated Billing
Consolidated Billing. Eg. AWS Org with 4 accounts: 1 Mgmt and 3 Members that would each have their own billing information. However, since they're in an AWS Org, the individual billing methods are REMOVED for member accounts. Instead, billing is passed through to Management Account of the AWS Org (AKA Payer Account)
- Payer Account - Management Account that contains the payment method for an AWS Organization
- This helps remove Financial Management Overhead
- Bulk discounts; consolidation of reservations and volume discounts

#### AWS Org - Service Control Policies (SCP)
Allows you to restrict what Member Accounts can do.

#### AWS Org - New Account within Org
For new account, you just need a valid, unique email address. This way, there is no invite process (like there is with having pre-existing accounts join an AWS Org).

### AWS Org Changes Best Practice for User Logins / Permissions
With Orgs, you don't need IAM users inside every AWS Account. Instead, use Roles to allow IAM Users to access other accounts. 
- Best practice is single account to handle all logins
- Large enterprise may use Identity Federation to pull in on-premise identities for logging in to login account
- Role Switch: Once Member accounts are logged in, they can Role Switch from login account into other Member Accounts

## DEMO - AWS Organizations
Steps:
1. The GENERAL account will become the MANAGEMENT / MASTER account for the organisation
2. We will invite the PRODUCTION account as a MEMBER account and create the DEVELOPMENT account as a MEMBER account.
3. Finally - we will create an OrganizationAccountAccessRole in the production account, and use this role to switch between accounts.

1. Nav to AWS Organization > "Create an Organization"
2. In Incognito Window, log in to the Production Account admin, copy Account ID > back to General AWS Management Account window > "Add an AWS account" > Invite Existing Account > Paste in ID / add message > Send Invitation
3. In Production Admin account > nav to AWS Organizations > Invitations > Accept Invitation
4. Manually adding a Role to an invited account > In Prod account nav to IAM > Roles > Create Role > Type of Entity: AWS Account > get account ID of General AWS Org Account > select Another AWS Account > Paste Account ID > Add Permissions: AdministratorAccess > Next > name "OrganizationAccountAccessRole" > Create Role. In IAM > Roles >  OrganizationAccountAccessRole > Trust Relationships, you'll see the General Account ID referenced as a Trusted Entity
5. Role Switch: From General to Production Account. Copy Production ID > Main Dropdown "Switch Role" > click "Switch Role" > paste Prod ID > name of Role created "OrganizationAccountAccessRole" > Display Name "Prod" > select color Red > Create / Switch Role. You'll see Display name "Prod" on top right menu drop down. You can also SWITCH BACK

6. Create new Account within Org. AWS Orgz > Add Account > Create an AWS Account > name "OrganizationAccountAccessRole" > Create 
7. After new Account created, copy its account ID > dropdown Switch Role > switch to DEV role


## Service Control Policies (SCPs)
- A feature of AWS Organizations which allow restrictions to be placed on MEMBER accounts in the form of permissions boundaries. Establish which permissions can be granted in an account.
- SCPs can be applied to the organization, to OU's or to individual accounts
- Member accounts can be effected, the MANAGEMENT account cannot. But, it can indirectly attach to Account Root User
- SCPs DON'T GIVE permission - they just control what an account CAN and CANNOT grant via identity policies
- SCP is a JSON document
- SCPs inherit down the Org tree. Eg. If attached to Root Container, all Org accounts affected. If attached to OU, it affects the OU and all units / members within

TIP: SCPs DON'T GRANT any permissions, they just establish boundaries / limit permissions

### SCP: Allow / Deny Lists
- Allow List. Block by Default and allow certain services
- Deny List. Allow be Default and block certain services (Deny List is Default list, and default policy attached is FullAWSAccess)

To implement Allow Lists, 1. Remove AWS FullAccess Policy, 2. Add Allowed services into a new SCP

Best practice is Deny List for less admin overhead.

### SCP: Identity Policies in Accounts VS SCPs
EXAM: There is an overlap of permissions between these two types of policies. The OVERLAPPED permissions are what are actually active


## DEMO - Using Service Control Policies (SCP)
Update the structure within the organization, add hierarchy (Root, Dev OU, Prod OU) - and apply an SCP to the PRODUCTION account to test their capabilities
- Follows the same DENY-ALLOW-DENY IDP pattern

1. Create OU: Be in Admin account > AWS Organizations > check Root container box, "Actions: Create New" > Org Unit Name "PROD" > Create OU.
2. Create OU: Repeat above for DEV
3. Move relevant accounts to new OUs: check Production account, dropdown "Move" > Select respective OU (PROD/DEV) > Move AWS Account
4. Add SCP to Production Account: Switch Role: PROD > nav to s3 > Create Bucket > name (must be globally unique) "catpics3453451" > region: us-e-1 > upload attached photo (proving we have admin access)
5. Restrict with SCP. Switch Back > AWS Orgz > Policies > click SCP, enable SCP > Create Policy > copy .json text content from lesson file denys3.json > replace JSON with copied text > name "Allow All Except S3" > create policy
6. AWS Orgz > AWS Accounts > click PROD OU > tab "Policies" > Attach Allow All Except S3 Policy
7. Detach FullAWSAccess. AWS Orgz > Account PROD > tab "Policies" > select "attached directly" FullAWSAccess > Detach > Detach Policy
8. We reverted everything back to normal (re-attached Full Access policy to PROD OU, emptied s3 bucket, deleted s3 bucket


## Cloudwatch Logs
- CloudWatch Logs is a public service which can accept logging data, store it and monitor it
- It is often the default place where AWS Services can output their logging
- CloudWatch Logs is a public service and can also be utilised in an on-premises environment and even from other public cloud platforms
- Built-in AWS Service integrations: EC2, VPC Flow Logs, Lambda, CloudTrail, R53, and more
- Unified Cloudwatch Agent: How anything outside AWS can log data to Cloudwatch
- Metric Filter: Can generate metrics based on logs

### Cloudwatch - What it looks like
First, it's a Regional Service. Starting point: Logging Sources; external compute, DB's, external APIs, AWS services. Log Events are created from data from logging sources. Log Events are stored inside Log Stream (an ordered sequence of log events from the same source). Then a Metric Filter takes Log Group/Stream data, distills metrics which can bet set with alarm notifications

EXAM: CloudWatch is a REGIONALLY resilient service

### Cloudwatch - Vocab
- Log Group: Container for multiple log streams for the same type of logging. Log Group also stored config settings (retention, permissions)
- Log Stream: An ordered sequence of log events from the same source. Log Streams inherit Log Group config settings.
- Log Events: Created from data from logging sources
- Logging Sources: external compute, DB's, external APIs, AWS services


## CloudTrail
- CloudTrail Is a product which logs API actions/calls and account events. Eg. Stop instance, change security group, delete S3 bucket--all logged.
- Very often used to diagnose security or performance issues, or to provide quality account level traceability
- Enabled by default in AWS accounts and logs free information with a 90 day retention
- It can be configured to store data indefinitely in S3 or CloudWatch Logs

### CloudTrail - Vocab
- CloudTrail Event: When CloudTrail logs API calls/activities, it logs them as CloudTrail Events; a record of an activity in an AWS account (action taken by user, role, or service)
- Event History: Record of activity, default stored for 90 days. Enabled by default, no cost for the 90 day history
- Trail: In order to customize CloudTrail service, you need to create 1 or more "Trails". Unit of configuration within CloudTrail. Logs events for the AWS region it's created in.
-- One-Region Trail: Only EVER in the region it's created in. Only logs events for this region
-- All-Regions Trail: Collection of Trails within every AWS Region, but logged as one trail. If AWS adds new regions, they get automatically added to All Region Trails
- Global Service Events: A very small number of services log events globally to ONE region (us-east-1). Eg. IAM, STS, CloudFront. A Trail needs this enabled in order to log these events. Should be enabled in the created Trail by default 

EXAM: CloudTrail is a REGIONAL Service. A Trail logs events for the AWS region it's created in

### CloudTrail - Event Types (3)
1. Management Events: Provide information about mgmt operations performed on resources in your AWS account; AKA Control Plane Operations. Eg. Creating VPC, terminating EC2 instance
2. Data Events: Contain information about resource operations performed on or in a resource. Eg. Objects loaded to s3, accessed from s3, lambda function being invoked
3. Insight Events (discussed later): Identify unusual activity, errors, or user behavior in your account
NOTE: By default, CloudTrail only logs Management Events

### CloudTrail - Trails
- One-Region Trail: Only EVER in the region it's created in. Only logs events for this region
- All-Regions Trail: Collection of Trails within every AWS Region, but logged as one trail. If AWS adds new regions, they get automatically added to All Region Trails
NOTE: Small number of services log events globally to ONE region (us-east-1). Eg. IAM, STS, CloudFront. These are called Global Service Events. So, Trails are either logged within the region they were created in, or to us-east-1 if it's a Global Service Event. Or to all regions if All-Region Trail
-- All events are captured by a Trail (management events by default, data events if manually enabled)
-- A Trail stores events in an S3 bucket by default. Logs generated and stored in an s3 bucket can be stored indefinitely; charged for storage in s3. Trail event files are small JSON files, however
-- Alternative to previous bullet, CloudTrail can integrate with CloudWatch Logs and deposit logged data there. Advantage here is being able to use CloudWatch Logs features

## CloudTrail - Continued
- Recent addition to CloudTrail, you can now create Organizational Trail. This means, if created from mgmt account, it can store all info from all accounts in the Org. Making it a single management point for all API and account events across every account in the Org.
- CloudTrail is enabled by default on AWS accounts. Free 90 day event history retention; no storage in s3 unless you configure a Trail
- Trails are how you can config s3 and CW Logs
- By default, only Management Events are logged in CloudTrail (creating, stopping, terminating instance, console login, any AWS interaction). Data events need to be enabled, but come at an extra cost

EXAM: Global Service Events: While most AWS services log data to the same region that service is in, there are a few True Global Services that are logged as GSE's in us-east-1; a Trail must be enabled to capture GSE data
EXAM: CloudTrail is NOT real-time. CT typically delivers log files within 15 minutes of the account activity occurring. CloudTrail is not the product choice you want if you need real time logging.

## CloudTrail Pricing - https://aws.amazon.com/cloudtrail/pricing/
- 90 day Event History is Free
- Get 1 copy of Management Events free in every region in each AWS account
- Beyond that, Management Events: $2.00 / 100,000 events (after the first free copy)
- Data Events: $0.10 / 100,000 events
- CloudTrail Insights $0.35 / 100,000 events analyzed

## DEMO - Implementing an Organizational Trail (CloudTrail)
This CloudTrail will be configured for all regions and set to log global services events.
We will set the trail to log to an S3 bucket and then enhance it to inject data into CloudWatch Logs.

NOTE: You can create individual trails in accounts, but it's always more efficient to use an Organizational Trail.
NOTE: By default when you create a Trail, it creates a Trail for all AWS Regions in your account

EXAM: S3 bucket names MUST be GLOBALLY UNIQUE

1. iamadmin login > CloudTrail > Trails > Create trail > Trail name "Animals4lifeOrg" > check "Enable for all accounts in my org" > uncheck Enable under "Log file SSE-KSM encryption (use this in production, not in this practice) > Enable CloudWatch Logs > CW Logs Role name "CloudTrailRoleForCloudWatchLogs_Animals4Life" > Next > select Event types to log: check Management Events > Next > Review / Create trail
- After creating, can take some time for data to start appearing
2. Open the s3 link on the new Trail > move down through CloudTrail/ > View json.gz (can decompress with Chat GPT) to verify Trail is working
3. In new tab, nav to CloudWatch > Log Groups > Log Streams all in us-east-1
- Account ID is contained within Log Stream file name. 
- In Cloud Trail Event History, this will log Events for 90 days even if you have no Trail created. Trails allow you to customize what happens to the data

- In this demo, we created a Trail 1) to store data in s3 2) to put it into CloudWatch Logs 

NOTE: s3 charges based on storage. If CloudTrail is enabled, the logs will accumulate possibly past Free Tier
- To Avoid logging events and incurring charges: Go to Trails, "Stop Logging"


## AWS Control Tower
AWS Control Tower offers a straightforward way to set up and govern an AWS multi-account environment, following prescriptive best practices. AWS Control Tower orchestrates the capabilities of several other AWS services, including AWS Organizations, AWS Service Catalog, and AWS IAM Identity Center (successor to AWS Single Sign-On), to build a landing zone in less than an hour. Resources are set up and managed on your behalf.

AWS Control Tower orchestration extends the capabilities of AWS Organizations. To help keep your organizations and accounts from drift, which is divergence from best practices, AWS Control Tower applies preventive and detective controls (guardrails). For example, you can use guardrails to help ensure that security logs and necessary cross-account access permissions are created, and not altered.
- Think of Control Tower as another evolution of AWS Organizations

### CT: Parts of Control Tower
- Landing Zone: Multi-account environment (what most people interact with). SSO/ID Fed, Centralized Logging, Auditing
- Guard Rails: Detect/Mandate rules/standards across all accounts
- Account Factory: Automates and standardizes new account creation
- Dashboard: Single page oversight of entire environment/org

#### CT: Landing Zone
A well-architected multi-account environment. Home Region is the one you deploy into and is always available.
- Built with AWS Orgz, Config, CloudFormation
- Security Organizational Unit (OU): Log Archive and Audit Accounts (CloudTrail / Config Logs)
- Sandbox OU: For testing and for less rigid security situations
- IAM ID Center (prev. AWS SSO): SSO, multiple accounts, ID Federation (using on-premise identity stores)
- Monitoring and Notifications: CloudWatch and SNS
- Service Catalog: End User account provisioning

#### CT: Guard Rails
- Rules for multi-account governance.
- Three types: Mandatory, Strongly Recommended, Elective
- GR functions in 2 Ways: 
-- Preventative: Stop you from doing things (AWS Org SCP). Enforced or not enabled. Eg. Allow/deny regions, disallow bucket policy changes (prevent things from happening)
-- Detective: Compliance checks (AWS Config Rules) for maintaining Best Practices. Types: Clear, In Violation, Not Enabled. Eg. Detect / confirm if CloudTrail has been enabled on  your account (identify things happening)

#### CT: Account Factory
- Automated account provisioning. Cloud Admins or End Users (w/ appropriate permissions)
- Guardrails automatically added
- Give admin permissions to a named user (IAM ID)
- Standard Account & Network standard configuration. Eg. IP addressing using VPC
- Allows accounts to be closed or repurposed
- Can be fully integrated with a business's Software Development Lifecycle

## AWS Control Tower (continued)
- Under Control Tower, AWS Organizations creates two Organizational Units (OU): Foundational/Security and Sandbox OU's
- Within each Foundational OU and Security OU, two accounts are created in each: Audit and Log Archive accounts
- Account Factory: Create/configure/delete accounts using Templates: Account Baseline (template) and Network Baseline (template)
- For Guardrails, AWS uses AWS Congfig and SCP
- Drift: Divergence from best practices


## S3 Security (Resource Policies & ACLs)
Bucket Policies: Type of AWS Resource Policy

EXAM: S3 is PRIVATE by default
- only ID with any initial access is Account Root User of account which owns the S3 Bucket
- Any other permissions must be explicity granted through a few ways:
-- S3 Bucket Policy, a form of Resource Policies. RP's: These are attached to Resources, not Identities
-- Resource Policies (RP) provide a resource perspective on permissions. Control access on a Resource
--- Controlling who can access a resource
- EXAM: Unlike ID Policies, Resource Policies's have presence of an explicit Principal Component.

NOTE: You can only attach IDP's to ID's in your OWN account. Only controlling security inside account
- Resource policies can be attached to its own account or DIFFERENT accounts. Inside this RP, you can reference any identities (whether in same or different account)

- RPs can ALLOW/DENY anonymous principals -- even those not authenticated by AWS; anonymous access

### S3 Sec: TL;DR Bucket Policies can grant access for other AWS accounts, and anonymous access 

RP's have one major difference to Identity Policies: The presence of an explicit Principal Component.
- The Principal part of an RP defines which Principals are affected by the policy (who is impacted?)

TERM: Principals. A person or application that uses the AWS account root user, an IAM user, or an IAM role to sign in and make requests to AWS. Principals include federated users and assumed roles.
- if a Resource Policy applies to you, you are the Principal
- Eg. "Principal": "*", --> Star is wildcard, which means ANY principal; applies to anyone accessing the Bucket

### S3 Sec: Other s3 Bucket Policy features / functions
Ex 1. Used to control who can access objects, even blocking specific IP addresses
Ex 2. Can Deny a Principal who isn't using MFA from accessing a Bucket
- Additional Examples: https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html

NOTE: There can only be ONE Policy on a bucket. But, this policy can have multiple statements.

### S3 Sec: Another Form - Access Control Lists (ACLs) - LEGACY
- Legacy (Use Bucket or Identity Policies instead). This is because ACLs are inflexible; no conditions, for example. Can only do 5 things.
- ACL is a subresource

### S3 Sec: Block Public Access Settings
Added in response to lots of public PR disasters; bad bucket configuration leading to data leaks. Until BPA, public/anons could access Bucket. BPA has setting which override Bucket Policies, BUT they apply to just Public Access
- These settings created when making Bucket, but can be adjusted later

EXAM: Identity Policies: Controlling different resources / prefer IAM / Same account only policies
EXAM: Resource Policies: For just controlling S3 / for anonymous or cross-account access
EXAM: Access Control Lists: NEVER unless required, as they are Legacy. AWS recommends against use of ACLs


## S3 Static Hosting
Accessing S3 is generally done via APIs. Static Website Hosting is a feature of the product which lets you define a HTTP endpoint, set index and error documents and use S3 like a website.
 - S3 Static Hosting allows access to s3 via HTTP - Eg. Blogs
 - Usage (2 Documents required): First enable, and in doing so, you have to set INDEX and ERROR documents
 - Index page is entry point to most websites
 - Error Document: When you access a page that isn't there, or other type of service side error that's when Error Doc is shown
 -- Index and Error docs need to be html documents as s3 Static Hosting reads HTML files
 - When Static Hosting is enabled, a static website hosting endpoint is created. Name of endpoint is based on bucket name and region
 -- Want a custom Domain? (via R53)... if so, bucket name matters. Name of Bucket MUST match domain name
 --- Eg. Want a site called top10.animals4life.org? Name your bucket "top10.animals4life.org"
 
 ### S3 Static Hosting: What else is S3 Static Hosting Good for (other than hosting static websites?
 - Example 1: Offloading. If you have a site with lots of images hosted by compute service, you can offload the media to an S3 bucket w/ static hosting to save money (compute is usually pricier). Offload large data to S3.
 - Example 2: Out-of-band pages. In IT, this means method of accessing something outside of the main way. Example: You want to perform server maintenance and the server needs to go down. You can put an "Under Construction" static page in S3 to put up when production server is down.
 
 ## S3 Pricing
 Pricing for S3 forms of a number of major components:
 - Cost to Store Data: per gigabyte per month charge
 - Data Transfer Free: for every Gb of data transferred out of S3, per gigabyte charge
 - Data Requests: GET, POST, list, port. Cost per 1,000 operations
 
### S3: What's FREE?
 - 5Gb monthly storage
 - 20,000 GET requests
 - 2,000 PUT requests
 
 
## DEMO Creating a Static Website with S3
 1. Create S3 Bucket > bucket name "[custom-globally-unique]" > uncheck "Block All Public Access" and acknowledge > Create Bucket
 2. Enable Static Website Hosting > access new bucket > Properties tab > scroll to bottom, Edit Static Website Hosting, Enable > Hosting Type: Static > Index Document "index.html" > Error Document "error.html" > In properties, scroll down and copy new static URL
 3. Upload some Objects to the bucket > Objects tab, "Upload" > Upload index.html, error.html, and "img" folder
 4. Paste copied URL into browser
 - You'll get a 403 Forbidden error (Access Denied) - Remember, S3 buckets are private by Default. We need to add permissions for anonymous/public users to visit site (no method to provide creds to S3)
 5. Give Permissions to un-authenticated uses to acess bucket > Access S3 bucket > Permissions tab > Bucket Policy > Edit > Grab JSON from .zip > Paste in, but replace the "Resource" value BEFORE the "/*" (mine now looks like "Resource":["arn:aws:s3:::top10catsever876.com/*"]) > Save
 6. You can now visit your website
 Extra: If you Registered a domain in R53, you can customize your URL. R53 > Hosted Zones > access your domain > Create Record > select Simple Routing > Record Name Eg. "top10".animals4life.io > choose Endpoint "Alias to S3 website endpoint" > Region: us-east-1 > S3 endpoint, select your bucket > click "Define simple record" > Create Records. Now Cantrill can go to top10.animals4life.io. Remember: Domain name and bucket name must match exactly to do this
 7. Clean Up: Empty bucket, delete bucket
 
 
 ## Object Versioning & MFA Delete (EXAM)
- Object versioning is a feature which can be enabled on an S3 bucket - allowing the bucket to store multi versions of objects
- These objects can be referenced by their version ID to interact directly - or omit this to reference the latest version of an object
- Objects aren't deleted - object deletion markers are put in place to hide objects.
- Object Versioning starts off in a Disabled state. Once enabled, you CANNOT disable it again. Instead, you can Suspend it. A suspended bucket can be re-enabled. 

EXAM: A bucket with Object Versioning enabled can NEVER have OV disabled again

Without versioning, Objects are identified solely by the Object's name, which is unique in the bucket. If you modify an object, the original version of the object is replaced. Versioning lets you store multiple versions of objects within a bucket/ 
- Operations which would modify an Object instead creates a new version
- Another attribute on an Object in a Bucket (other than Key (name)) is 'id'. A bucket without Versioning enabled has Object id's of 'null'
-- With Versioning enabled, id's are active. Modifying an object will create a new object with a new id. The newest Object version is called the Current or Latest Version
-- If an object is accessed without indicating to S3 which version is required, the Latest Version will be returned. You can access versions by specifying the id

### Object Versioning: Versioning Impacts Deletions
With Versioning enabled, if we indicate to S3 we want to delete the object without giving Version ID, S3 will create a new version of the object with a Delete Marker. In reality, the Object is just hidden. You CAN delete a Delete Marker, which re-activates previous versions.
- To truly delete a particular object, you need to specify the id

### Object Versioning: REMINDERS: 
- Versioning CANNOT be disabled after activating, only suspended (and suspending doesn't remove old versions, so you're still billed for all of it)
- Space is consumed by all versions of the object and you are billed for ALL versions
- Only way to return to reduced cost due to Versioning is to delete the bucket and re-add all content to another bucket that doesn't have Versioning enabled

### MFA Delete
Something enabled withing the Versioning config in a bucket. This makes MFA required to change a bucket's versioning state (To change from Enabled to Suspended, etc). 
- MFA is required to Delete Versions. When performing API calls to change/delete Version, you need to provide serial number of MFA token AND code, concatenated


## DEMO S3 Versioning
This lesson looks at a 'Animal of the week' website, and how to use versioning to recover when objects are changed and deleted accidentally or intentionally.

1. Create new S3 Bucket: Login to Mgmt/General Admin account > S3 > Buckets > Create Bucket > name [unique] "acbucket23425" > uncheck Block Public Access > Enable Bucket Versioning > Create Bucket
2. Enable Static Hosting: New bucket > Properties tab > Enable Static Website Hosting (bottom of page) > Index doc "index.html" > error doc "error.html" > Save changes
- REMEMBER: Just enabling Static Website Hosting is insufficient, you also need to add a Bucket Policy
3. Add Policy: Access new bucket > Permissions tab > edit Bucket Policy > copy text from bucket_policy.json (from demo .zip) > paste in json, edit Resource to look like " "Resource": "arn:aws:s3:::acbucket23425/*" ", except with your copied Bucket ARN instead
4. Upload files: acbucket > Upload > file "index.html" and folder "img" > click Upload
5. Versions: acbucket > Objects tab > toggle Show Versions > access winkie.jpg > Upload > Add Files > version 2/winkie.jpg > Upload > Access winkie.job object and see multiple versions if "Show versions" toggle is enabled
6. Delete Marker: Untoggle Show Versions within winkie.jpg Object > select winkie.jog > Delete > toggle on Show Versions > see Delete Marker > select Delete Marker and Delete
7. Delete Latest Version to Perma-Delete: acbucket Objects > toggle on Show Versions > select Latest Version of winkie.jpg > Delete
- NOTE: Whenever working with specific Versions of an object, this permanently deletes and makes next most recent version the new Latest / Current Version
8. Clean Up: Empty acbucket > Delete acbucket

REMEMBER: Versioning Enabled can incur significantly higher costs than Versioing turned off.


## S3 Performance Optimization
Single PUT Upload: Up to 5GB Max (don't trust single PUT with this much data), 1 blob of data. Single stream transfer uploaded using s3:PutObject API PUT call. If errors out/fails, full data stream has to restart, making it unreliable. Speed and reliability affected by this sub-optimal transfer. 

Multipart Upload: MINIMUM size 100MB. Improves speed and reliability compared to Single Put Upload. Breaks data stream into parts which can break and restart separately, making it more resilient. Always choose multipart beyond 100MB upload. 
- Upload can be split into max of 10,000 parts, parts ranging from 5MB -> 5GB. Each part can fail and restart in isolation; risk of uploading large amounts of data is reduce. Transfer rate is increased as you are uploading in parallel, more effectively using internet bandwidth
- The last remaining part can be less than 5MB

S3 Transfer Acceleration:
- How Global Transfer works: Data does not travel in the most efficient route, data can take indirect paths and potentially slows down from hop to hop. 
- S3 Transfer acceleration selects the closest, best-performing AWS Edge location and sends directly to S3 bucket. Edge Location transits data over AWS Global Network instead of via public internet (public internet is flexible and reliable over fast). Internet is like public transit with many layovers, whereas AWS Global Network is like a direct flight.
- By Default, Transfer Acceleration is Disabled on an S3 Bucket
- Bucket naming restrictions for Transfer Acceleration: no periods in name, must be DNS compatible


## DEMO S3 Performance
Enable Accelerated Transfer on an S3 bucket and review the AWS provided tool to complete Direct uploads vs Accelerated Transfer

Create s3 bucket (no periods in name, DNS naming compatible) > name "testac3464576" > Create Bucket > new Bucket Properties tab > edit Transfer Acceleration, Enable > Save changes
- NOTE: When Transfer Acceleration is Enabled, an Accelerated endpoint address is provided. You need to use this endpoint to get the benefit of Accel. Transfers.
- To compare upload speeds: http://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html


## Key Management Service (KMS)
AWS Key Management Service (AWS KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications. AWS KMS is a secure and resilient service that uses hardware security modules that have been validated under FIPS 140-2, or are in the process of being validated, to protect your keys.
- Regional & Public Service: every region isolated when using KMS. Note: KMS is capable of multizone (covered later)
- Public service, occupies AWS Public Zone and can connect from anywhere with access to this zone, with permissions
- KMS Mgmt allows you to CREATE, STORE, MANAGE keys
- Has both Symmetric and Asymmetric keys
- Capable of cryptographic operations, ENCRYPT, DECRYPT, etc
- KMS Keys NEVER leave the product; this is it's primary function. To keep keys in and securely held WITHIN the service

EXAM: FIPS 140-2: KMS Provides a service compliant with FIPS 140-2 Level 2, a US security standard
EXAM: KMS is REGIONAL and PUBLIC

### KMS: KMS Keys
Used by KMS within cryptographic operations. You, apps, and other AWS svcs can use these keys. KMS Key is a container for physical key material; it is Logical (representation of an encryption key)--the data contained is ID, date, policy, description, and state
- Every KMS Key backed by Physical Material (Actual key that is used to encrypt/decrypt). Physical Key material can be generated by KMS or imported
-- This 'material' is what is used to direct/encrypt (data up to 4KB)
- After picking region, user first performs CreateKey. Reminder: KMS performs all operations internally (KMS Keys NEVER leave KMS)
- TERM: Role Separation: Permissions to Encrypt, Decrypt, and Generate Key are all SEPARATE permissions

### KMS: Data Encryption Keys (DEK)
Earlier, it was noted that KMS Keys can only perform cryptoOps on data 4KB or less in size. KMS gets around this by generating Data Encyption Keys
- DEK is generated using KMS key using GenerateDataKey operation
- *** KMS doesn't store the DEK in any way. It provides it to you, then discards it. KMS does not do the encyption or decryption of data using DEKs, you or the service performs the DEK encrypt/decrypt.

### KMS: Key Concepts
- KMS Keys are ISOLATED to a REGION and never leave
- Multi-region keys discussed in a different lesson
- Within KMS, keys are either AWS owned or Customer owned. AWS Owned are for use in multiple accounts and operate in the background
-- Two types of Customer Owner 1) AWS Managed (auto-created by AWS services, like S3) 2) Customer Managed (created explicitly by customer to be used by app or AWS svc 
-- Customer Managed Customer Owned KMS Keys: More configurable. AWS Managed can't really be customized
- Aliases: shortcuts to keys. Aliases are PER REGION. Neither aliases or keys are Global, by default

### KMS: Key Rotation
When the physical backing material used to perform cryptoOperations is changed at regular intervals (usually once annually)
- KMS Keys support key rotation
- Customer Key Rotation is optional 
- When key is rotated, material (data) is changed and NOT the logical key

### KMS: Permissions (Policies / Security)
Account Trust is explicitly added to a Key Policy, or not.
- Key Policy (type of Resource Policy): Every KMS key has a policy. On Customer Managed keys, you can change the policy
- Keys have to explicitly be told they trust the account they're contained within
- Generally, KMS is managed using this combination: Key Policies trusting account + Identity Policies allowing IAM users to interact with key

REMINDER: Resource Policies require a PRINCIPAL in their JSON file, IDP's do not


## DEMO - KMS - Encrypting the battleplans with KMS
Run through the practical steps of creating and configuring a KMS Key, an Alias and we use that Key and the CLI tools to encrypt and decrypt some data

1. Generate KMS Key: Login to Mgmt/General Admin account > KMS > Create a key > Key Type: Symmetric > Next > create alias "catrobot" > Next > Define key admin permissions: check "iamadmin" (so iamadmin user can administer this key) > Next > Define key usage permissions: select "iamadmin" > Next > Review > Finish
2. Enable Key Rotation: Access catrobot key > Key Rotation tab > Check auto-rotate KMS key yearly, Save
3. Use Key / Create Battle Plan: access CloudShell (first icon on right-side main AWS menu, looks like Terminal icon) > Create plaintext battleplan:  || echo "find all the doggos, distract them with the yumz" > battleplans.txt ||
4. Encrypt message - Output will be the Encrypted not_battleplans.enc. Enter below lines into Shell
aws kms encrypt \
    --key-id alias/catrobot \
    --plaintext fileb://battleplans.txt \
    --output text \
    --query CiphertextBlob \
    | base64 --decode > not_battleplans.enc 
5. Receiver needs to Decrypt the cihpertext. Enter below lines into Shell:
aws kms decrypt \
    --ciphertext-blob fileb://not_battleplans.enc \
    --output text \
    --query Plaintext | base64 --decode > decryptedplans.txt
6. Clean Up: Select key > Key Actions: Schedule for deletion (waiting period 7-30 days, input 7) > Confirm > Schedule deletion 


## SSE-S3 (AES256)
Step through the various encryption options available within S3 and finish by looking at default bucket encryption settings
- Server-Side Encryption (SSE).
-- EXAM: Buckets are NOT encrypted, Objects are; encryption not defined at Bucket level. Encryption is defined at Object level
- Client-Side Encryption (CSE). S3 never sees plaintext

### SSE-S3: SSE VS CSE: How data is stored on disk in an encrypted way; encryption at rest
- Path: Users/App <-> S3 Endpoint <-> S3 Storage. 
-- In transit: On both SSE/CSE, Data in transit between User/S3 Endpoint is encrypted in transit.
-- AT REST is what we're focusing on. 
--- In CSE, Objects being uploaded are encrypted by the client before they ever leave client-side. AWS will never see data in plain text form. In CSE, you own keys, process, and tooling
--- In SSE, even though data is initially encrypted in-transit using HTTPS, the Objects themselves are NOT initially encrypted. From User > S3 Endpoint, data is in its original form. At S3 endpoint, the data gets encrypted and delivered to S3 Storage as ciphertext.

NOTE: AWS has made SSE mandatory, so you can no longer store objects in an unencrypted form on S3. You control what type of SSE is utilized

### SSE-S3 - Types of Server-Side Encryption within S3:
- SSE-C: SSE with Customer provided/managed Keys. Customer handles keys, S3 handles enc/dec. In-Transit data encrypted by HTTPS, plaintext otherwise
- SSE-S3: [The Default] SSE with Amazon S3 Managed Keys. AWS handles both enc/dec and key mgmt. Uses AES-256
-- Three problems with SSE-S3: 1) Not suitable strongly regulated environments 2) if you need Role Separation, not suitable 3) need to control Key Rotation? not suitable. AKA No Key Control, No Role Separation
- SSE-KMS: SSE with KMS Keys stored in the AWS Key Management Service. KMS service now managing the keys, meaning you can create a Customer Managed Key; isolated permissions, fully configurable. KMS Generates and delivers DE Keys to S3 (KMS does not store DEKs). Great for controlling Permissions, Role Separation and Key Rotation Control.
* Difference between methods is what parts of the process you trust S3 with and how encrypt process/key mgmt is handled
* High Level: Two components to SSE: 1) encrypt/decrypt process, 2) generation/mgmt of crypto keys (these two components handled differently in different SSE types)

### SSE-S3: Resources
- Visual of SSE Methods and Details: https://imgur.com/a/lCg5gmA
- https://docs.aws.amazon.com/AmazonS3/latest/user-guide/default-bucket-encryption.html
- https://docs.aws.amazon.com/kms/latest/developerguide/services-s3.html
- https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html
- https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html
https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html


## Demo - SSE-S3 - Object Encryption and Role Separation
Create an S3 bucket, and upload 3 images to the bucket using different encryption methods

1. Create S3 Bucket > name "catpics[random number]" > Create Bucket
2. Create Key: Nav to KMS > Create Key > Defaults > Alias "catpics" > Next > Don't set any Key Administrative Positions > Next > skip Key Usage Permissions > Finish
3. Upload SSE-S3 image: Back to S3 > catpics bucket > upload just sse-s3-dweez.jpg (must upload separate as we are configuring separate encryptions) > expand Properties accordian, Server-side encryption "Specify an en encryption key" > Encryption settings "Override bucket settings" > Encryption Key type "SSE-S3" > Upload
4. Upload SSE-KMS image w/ AWS managed default key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: choose the one ending "aws/s3", an AWS managed default key > Upload
5. Replace Step 4 Object, SSE-KMS image w/ KMS Generated Key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: alias "catpics" > Upload
6. Apply Deny policy on IAM, preventing KMS use > IAM Dashboard > Users > iamadmin > Permissions tab > Add Policy: Inline Policy > JSON tab > delete template > Paste in JSON provided in lesson > Review policy > name "denyKMS" > Create policy. Now you can open see-s3 image, but not the kms image. IAM > Remove DenyKMS
7. Set Default Bucket Encryption: catpics bucket > Properties tab > Default Encryption "edit" > key type: SSE-KMS > AWS KMS Key: Choose, "catpics"
8. Upload Default Merlin jpg with no encrypt settings: upload default-merlin.jpg without changing anything > Properties tab: Server-side encryption settings - see default stuff added from Step 7

EXAM: If you need to fully manage the keys used as part of S3 encryption process, you have to use SSE-KMS


## S3 Bucket Keys
Amazon S3 Bucket Keys reduce the cost of Amazon S3 server-side encryption using AWS Key Management Service (SSE-KMS). Bucket-level keys for SSE can reduce AWS KMS request costs by up to 99 percent by decreasing the request traffic from Amazon S3 to AWS KMS.
- Without bucket keys, you make a ton of calls to KMS API. Each object is a separate call for DEK to KMS. Also throttling issues--the generate DEK operation can only be run 5,500, 10,000, or 50,000 times per second--this is shared across regions. AKA Using a single KMS Key results in a scaling limit for PUTS per second per key.
-- Bucket Keys improve this situation. Instead of KMS Key generating each DEK, it generates a single time-limited bucket key. This bucket key lives in the bucket and for a period of time, generates DEKs... offloads work from KMS to S3, reducing cost and increasing scalability.
NOTE: Not retroactive, so previously created S3 bucket objects will still be KMS generated DEKs
- CloudTrail (CT) Events will now show the bucket ARN instead of your object ARN
- Offloading KMS to S3 means fewer CT KMS events in the logs
- Bucket keys work with same-region and cross-region replication; the object encryption is maintained. When S3 replicates an encrypted object, it generally preserves the encryption settings
- If replicating plaintext to a bucket using bucket keys, the object is encrypted at the destination side (ETAG changes between source/destination)


## S3 Object Storage Classes
### S3 Standard
### S3 Standard-IA
### S3 One Zone-IA
### S3 Glacier
### S3 Glacier Deep Archive
### Intelligent-Tiering

### Standard
The Default. Stored objects stored across AT LEAST 3 AZs; can cope with multi-AZ failure; this provides 11 9's of durability (if store 10mil objects, on avg you might lose 1 object every 10,000 years). 
- Should be used for frequently accessed data that is IMPORTANT and NON-REPLACEABLE
- Replication uses MD5 Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption
- Successful receipt and storage in S3? S3 API endpoint returns 'HTTP/1.1 200 OK'
- Most balanced class when looking at cost and features
- First byte latency of milliseconds, objects can be made PUBLICLY AVAILABLE (using S3 permissions or static website hosting site for public internet)
#### Standard - Billing
- GB per Month fee for data stored
- $1 per GB charge for transfer OUT (transfer IN is always free)
- Price per 1,000 requests
- NO retrieval fee, NO minimum duration, NO min size
EXAM: S3 Standard should be used for frequently accessed data that is IMPORTANT and NON-REPLACEABLE

### S3 Standard-IA
IA = Infrequent Access. This class is designed for infrequently accessed data that needs reliability and durability.
Data replicated over 3 AZ's. Similar durability and first byte latency. Same checksum and CRCs. Objects can be made publicly available.
### Standard-IA Billing
- Big difference from Standard billing: Storage costs are cheaper than S3 standard
-- New cost component compared to Standard: RETRIEVAL FEE: for every byte retrieved, there is a cost to retrieve IN ADDITION to transfer fee
- MINIMUM DURATION charge: However long you store this class, you're billed minimum of 30 days
- MINIMUM CAPACITY charge: Per object, you are charged as if they are each at least 128KB in size; don't use IA to store lots of tiny objects
- Per request charge, data OUT charge, same as Standard
- Transfer IN is free
EXAM: S3 Standard-IA should be used for LONG-LIVED DATA which is IMPORTANT, but access is INFREQUENT

### S3 One Zone-IA
Similar to Standard-IA in many ways. Cheaper than both Std-IA and Std. The compromise for cost reduction: Data stored using this class is only stored in ONE Availability Zone
- Still retrieval fee, still 30 day minimum billing (like std-IA), still min cap of 128KB (like std-IA)
- One Zone-IA does not provide the multi-AZ resilience model, instead, one AZ used within the region; cheaper storage but greater risk of data loss
- SAME DURABILITY: 11 9's of durability (unless the AZ fails). Data still replicated in the one AZ
EXAM: Used for LONG-LIVED data that is INFREQUENTLY accessed, but for which is NON-CRITICAL and EASILY REPLACED

### S3 Glacier
S3 Glacier, instant access to your data; instant retrieval. Like S3 Standard-IA but cheaper storage, more expensive retrieval, longer minimums. Designed for when you need data instantly, but not very often (like once a month).
- Minimum storage duration charge: 90 days

### S3 Glacier Flexible
Same 3 zone AZ architecture, 11 9's of durability
- Trade-off compared to previous classes:
-- Think of the objects store here as "cold objects"; not ready for use; not immediately available, can't be made public; a RETRIEVAL PROCESS is required
--- Retrieval Jobs, 3 Types (faster = more $:
--- 1. Expedited: data available in 1-5 minutes
--- 2. Standard: available in 3-5 hours
--- 3. Bulk: 5-12 hours
- MINIMUM BILLABLE DURATION: 90 days
- MINIMUM BILLABLE SIZE: 40KB
- No Public Access
EXAM: First Byte latency = minutes or hours. No public access. Glacier Flexible is for situations where you need to store archival data where frequent/real-time access isn't required (like once a year access)

### S3 Glacier Deep Archive
The cheapest form of S3 storage. The most restrictions.
- If Glacier Flexible data is in "chilled" state, Glacier Deep Archive data is "frozen"
- MINIMUM BILLABLE DURATION: 180 days
- MINIMUM BILLABLE SIZE: 40KB
- Objects are not publicly accessible; retrieval job required
-- Retrieval Jobs:
-- 1. Standard - 12 hours
-- 2. Bulk - up to 48 hours
EXAM: First byte latency = hours or days. Used for archival data that is very rarely accessed, if ever. Good for data that requires retention length, or secondary long-term backups

### Intelligent-Tiering
Different from all previous classes; it contains five different storage tiers.
- When you move objects into this class, tier is determined by monitoring the data's usage
- Tiers:
-- Frequent Access (less than 30 days between access)
-- Infrequent Access (30+ days between access)
-- Archive Instant Access (90+ days between access)
-- Archive Access (90 -> 270)
-- Deep Archive (180 -> 730)
Instead of a retrieval cost, Intelligent Tiering has a monitoring and automation cost per 1,000 objects (management fee). Only use this when your app can tolerate asynchronous access patterns.
EXAM: Intelligent-Tiering is designed for long-lived data where usage is CHANGING or UNKNOWN. Ideal for uncertain access and low admin overhead
- https://aws.amazon.com/s3/pricing/
- https://aws.amazon.com/s3/storage-classes/


## S3 Lifecycle Configuration
Allows objects storage classes to be changed and objects deleted automatically. Step through S3 lifecycle management/configuration/rules both in theory and via an S3 console example
- You can create lifecycle rules on S3 buckets which can auto-transition or expire objects in a bucket. Great for objects that have a life cycle (activity on object is predictable)
- Lifecycle Configuration is a set of RULES that consist of ACTIONS. Rules can be applied to a whole Bucket or groups of objects in a bucket if defined by prefixes/tags
- Two types of Actions applied (both work on versions if Object Versions are enabled on bucket): 
-- 1. Transition Actions: Change storage class of affected objects
-- 2. Expiration Actions: Delete objects/object versions
EXAM: S3 ONE ZONE-IA CANNOT transition into S3 Glacier-Instant Retrieval. Transition can't go up the waterfall of classes, only down. See waterfall visual
EXAM: Smaller objects can cost MORE (minimum size)
EXAM: If object initially placed in Standard class, there is 30 day minimum period where an object needs to remain on S3 Standard before transition down the waterfall
EXAM: A SINGLE rule CANNOT transition to Standard-IA or One Zone-IA and THEN to glacier classes within 30 days (duration minimum); must remain in IA class for min 30 days before moving to Glacier


## S3 Replication
S3 has two replication features which allow objects to be replicated between SOURCE and DESTINATION buckets in the same or different AWS accounts

### S3 Replication - Two Types:
- Cross-Region Replication (CRR) is the process used when Source and Destination are in different AWS regions
- Same-Region Replication (SRR) is used when the buckets are in the same region.

### S3 Replication - The Difference:
With Cross-Region Replication, The Destination Bucket, b/c it's in a different AWS account, doesn't trust the Source account or its IAM Role that gets created for Replication purposes by Source Bucket. If configuring replication between different accounts, you have to create a Bucket Policy in the Destination Bucket which allows the Source IAM role to write/replicate into the Destination bucket.

### S3 Replication - Options:
1st option: What you replicate. Default is entire Source bucket to Destination bucket (everything in it), OR subset. 
- For subset, create a rule that adds a filter to filter objects by prefix or tags
2nd: Storage Class to be used. The Default is to use the same class, but you can choose a cheaper class if this data is secondary.
EXAM: Default Storage Class to use for S3 Replication is to maintain the same storage class as found on the Source Bucket, but you can override that in the replcation configuration (good if Destination Bucket will contain secondary data)
3rd: Ownership. Define ownership of objects in the Destination Bucket. Default is that dest buckets are owned by same entity that owns Source - This may not work if Source/Dest buckets are in different accounts (Dest bucket may not be able to read objects if objects are owned by Source).
4th: Replication Time Control (RTC): Adds guaranteed 15 minute SLA onto this process. This is used to make sure Source/Destination are in sync as closely as possible.
EXAM: 15 minute replication mentioned on exam? Then you know you need Replication Time Control (RTC)

### S3 Replication - Considerations:
EXAM:
- By Default, Replication is NOT retroactive and Versioning needs to be ON. Eg. If you enable Replication on a bucket that already has objects, those objects will not be replicated.
- Both Source AND Destination bucket need Versioning enabled
- You can use S3 Batch Replication to replicate pre-existing objects (since Replication is NOT retroactive by default)
- One-way replication: If you manually add objects to Destination Bucket, they will NOT be replicated to Source
-- Bi-directional replication is a recently added feature, but is an additional setting that needs to be configured
- Replication Capability: can handle unencrypted, SSE-S3 & SSE-KMS (with extra config), SSE-C
- Source Bucket Owner needs Permissions on the objects which will replicate
- Will NOT replicate: System events, Glacier, or Glacier Deep Archive
- NO DELETE markers are NOT replicated by Default. You can enable with DeleteMarkerReplication

### S3 Replication - Why Use It?
- For SRR (same region): For log aggregation, synchronize PROD and TEST accounts, resilience with strict sovereignty requirements (some data cannot leave specific regions)
- For CRR (cross region): Global resilience improvements, latency reduction

### S3 Replication - Resources:
- https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html
- https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-s3-replication-time-control-for-predictable-replication-time-backed-by-sla/



## DEMO Cross-Region Replication of an S3 Static Website
Create 2 S3 buckets - one in N. Virginia, the other in N. California and configure Cross-Region Replication (CRR) between the two.

1. iamadmin account, N.VA region selected
2. Nav to S3 > Create Source Bucket > Create Bucket > name of source "sourcebucketta[random number]" > region us-east-1 > Create Bucket
3. Enable Static Website on Source > Properties Tab > Static website hosting: edit: Enable > type: static website > index doc "index.html"/error doc "index.html" > Save changes
4. Edit Source bucket Permissions for Public Access > Permissions tab > uncheck Block All Public Access > confirm > Save changes
5. To made Source Bucket public, add policy > Permissions tab > Bucket Policy "edit" > from lesson docs, paste JSON, replace Resource arn before the "/*" > Save
6. Create Destination Bucket & Set Permissions/Policy > Create Bucket > name of dest "destinationbucketta[random number]" > AWS Region: us-west-1 > uncheck Block All Public Access > Properties tab, Enable Static website hosting > Hosting type: static > index/error docs "index.html" > Save changes > Permissions tab, edit Bucket policy, paste JSON, update ARN, Save 
7. Enable Cross-Region Replication (CRR): Source Bucket Management tab > Create replication rule > Enable Versioning > Replication rule name "staticwebsiteDR" > Status "Enabled" > Choose Rule Scope: "Apply to All objects in the bucket" > Destination: Browse S3, find destination bucket, enable versioning > IAM Role: dropdown "create new role" > Create replication rule > Replicate Existing Obejcts? No (as we have no pre-existing objects)
8. Clean Up: Empty/Delete Destination Bucket > Empty/Delete Source Bucket > IAM: locate role staring with "s3crr_role[...]"


# S3 PreSigned URLs
Presigned URL's are a feature of S3 which allows the system to generate a URL with access permissions encoded into it, for a specific bucket and object, valid for a certain time period
- PreSigned URLs can be used for downloads (GET) or Uploads (PUT)

Eg. S3 bucket with NO public access configured. Currently, a user would have to authenticate in IAM and be authorized to access resource. If you need to give an unauthenticated user access to the bucket, there are 3 [un-ideal] solutions 1) give mystery user AWS ID 2) give myst.user credentials 3) make object public. 
- Better solution than all this is PreSigned URLs

NOTE: The PreSigned URL is used, the holder of the URL is interacting with S3 as the person who GENERATED the URL. In the example above, the mystery user would be iamadmin 

EXAM: You can create a URL for an object that you have NO ACCESS TO. But, since you have no access, the PreSigned URL won't either. Not an applicable use case, but possible
EXAM: When using a PreSigned URL, the permissions are the same as the CURRENT permissions of Identity that generated the PreSigned URL. (So Access Denied could mean the generating ID never had access, or doesn't now)
EXAM: Don't generate PreSigned URLs using an IAM Role (temp credentials of a Role can expire before temp access to PreSigned URL)


 ## DEMO S3 Creating and using PreSigned URLs
 Create a bucket, upload an object and generate a presignedURL allowing access for any unauthenticated identities.
 
 1. Create bucket > name "animals4lifemedia[randomnumber]" > Create bucket 
 2. Upload object > all5.jpv to new bucket
 3. Generate PreSigned ULR > Cloud Shell (terminal icon top right of AWS) > shell command "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 180"
 - 180 is in seconds, 3 mins
 4. Clean up: Empty/delete bucket
 
 NOTE: Interesting Aspects...
 1. Try "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 604,800"
 2. Nav to IAM > Users > iamadmin > Permissions: Add inline policy, copy JSON from lesson > save
 3. In CloudShell, try "aws s3 ls", you'll see Access Denied. This Explicit Deny overrules S3 permissions. Refresh PreSigned URL and see that access is now denied as the current permissions of iamadmin are restricted from S3
 4. iamadmin currently restricted from S3, but can still generated a PreSigned URL for it, even with no access. 
 - You can also generate a PreSigned URL on a non-existent object
 - If you generate a PreSigned URL with an assumed Role, the URL will stop working with the temporary creds for the Role stop working
 - Can now create PreSigned URL from AWS Dashbord s3 > bucket > object > Object Actions dropdown "Share with a presigned URL"
 
 
## S3 Select and Glacier Select
EXAM: Understand this architecture
S3 and Glacier Select allow you to use a SQL-Like statements to retrieve partial objects from S3 and Glacier.
- Ways you can retrieve PARTS of objects rather than the entire object
-- Both S3 and Glacier super scalable. S3 can store objects up to 5TB and store infinite number of these objects. Often, you don't need to retrieve the entire 5TB object
- With S3 Select, filtering occurs on the service/the source (S3); The data delivered by S3 is pre-filtered WITHIN S3, making it quicker and reducing costs


## S3 Events
The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. To enable notifications, you must first add a notification configuration that identifies the events you want Amazon S3 to publish and the destinations where you want Amazon S3 to send the notifications. You store this configuration in the notification subresource that is associated with a bucket
- Notifications generated when events occur in a bucket
- Can be delivered to SNS Topics, SQS Queues and Lambda Functions
- Types of events: object Created (Put, Post, Copy, CompleteMultiPartUpload), object Delete (*, Delete, DeleteMarkerCreated), object Restore (Post (Initiated), Completed), Replication 
- Events are generated by S3 Service, known as S3 Principal, so we also need to add Resource Policies to the destination services to allow S3 svc to interact 
- Events are JSON objects
- S3 Event notifications are dated and limited features. Can also use EventBridge which supports more events and wider svc integration. 
DEFAULT: use EventBridge as Default for S3 event notifications


## S3 Access Logs
Server access logging provides detailed records for the requests that are made to a bucket. Server access logs are useful for many applications. For example, access log information can be useful in security and access audits. It can also help you learn about your customer base and understand your Amazon S3 bill.
- You have a Source bucket where you want to track access. You have a Target bucket where you'll store tracked events. Can be enabled via Console UI or via PUT Bucket Logging
- S3 Logging managed by S3 Log Delivery Group
- Logs delivered as Log Files, consisting of Log Records
-- Each attribute within a record is space-delimited, and Records within in a file are newline-delimited
- Single Target bucket can be used for many Source buckets, separate logs using prefixes in Target bucket


## S3 Object Lock
You can use S3 Object Lock to store objects using a write-once-read-many (WORM) model. It can help you prevent objects from being deleted or overwritten for a fixed amount of time or indefinitely. You can use S3 Object Lock to meet regulatory requirements that require WORM storage, or add an extra layer of protection against object changes and deletion.
- WORM Model - wrote-once-read-many. Once Object Versions are created, they can't be overwritten or deleted (object versions are locked)
- User can enable on 'new' buckets, support ticket required for adding to existing bucket
- Object Lock required Versioning to be enabled. Once you create/enable Object Lock, you can't disable/delete OL or Versioning
- Can define Object Lock on objects, or a Bucket can have a default Object Lock Settings
- You can overlap the effects, Eg. Having a Legal Hold and Retention: Governance enabled on same object

Object Lock handles retention in TWO ways:
1. Retention Periods
2. Legal Holds
- Can have both, either, or none

### S3 Object Lock - Retention Period Methods - Retention Periods and Legal Holds
#### Retention Period: When you create lock, you specify retention period for DAYS / YEARS
Two Modes of Retention Period (EXAM):
- 1. Compliance Mode. Object version Can't be adjusted, deleted, overwritten for duration of period. Retention period duration can't be reduced. Retention Mode cannot be adjusted during period (EXAM: not even by Account Root User). This is the most strict Object Lock: Retention Period w/ Compliance Mode. 
- 2. Governance Mode. Set a retention period, but special permissions can be granted allowing Lock Settings to be adjusted during the retention period
-- EXAM: s3:BypassGovernanceRetention in order to allow settings adjustment, along with header along with request "x-amz-bypass-governance-retention:true" (console ui default)

### S3 Object Lock - Lock Legal Hold
With Legal Hold, you don't set a Retention Period at all. Instead, for an Object Version, you set Legal Hold ON or OFF; binary. NO RETENTION.
- While Legal Hold flag is on, no deletes and no changes until Legal Hold is removed
-- s3:PutObjectLegalHold required to add or remove
- Legal Hold can be used to prevent accidental deletion of critical object versions. Or if you need to flag an object version for a legal case/project etc


## S3 Access Points
Amazon S3 Access Points, a feature of S3, simplifies managing data access at scale for applications using shared data sets on S3. Access points are unique hostnames that customers create to enforce distinct permissions and network controls for any request made through the access point.
- You can have 1 bucket with many access points, each access point can have different policies
- Access Points can be limited in terms of WHERE they can be accessed from. Eg. VPC or internet
- Every Access Point has its own endpoint address
- EXAM: Access Point created via Console or with this shell command:
-- aws s3control create-access-point --name [name] --account-id [account-id] --bucket [bucket-name]
- Access Points can be thought of as mini buckets or different views of the bucket
- Each Access Point has a unique DNS that would be given to the users using it
- Access Point Policies control permissions for access via Access Point and are functionally equivalent to a Bucket Policy. Access Point Policy can restruct identities to certain prefixes, tags, or actions based on need
- IMPORTANT: Any permissions defined on an Access Point need to also be defined on the Bucket Policy

### S3 Access Points Resource: 
https://docs.aws.amazon.com/AmazonS3/latest/dev/creating-access-points.html#access-points-policies


## Demo S3 Multi-Region Access Points (MRAP)
Gain practical experience working with Multi-region access points

Amazon Simple Storage Service (S3) Multi-Region Access Points provide a global endpoint for routing Amazon S3 request traffic between AWS Regions. Each global endpoint routes Amazon S3 data request traffic from multiple sources, including traffic originating in Amazon Virtual Private Clouds (VPCs), from on-premises data centers over AWS PrivateLink, and from the public internet without building complex networking configurations with separate endpoints.

1. Create two buckets: S3 > Create bucket "multi-region-demo-sydney-[random-number]", region ap-southeast-2, Enable Bucket Versioning > Create > Create 2nd bucket "multi-region-demo-canada-[random-number]", region ca-central-1, Enable Bucket Versioning > Create
2. Create Multi-Region Access Point: S3 > Multi-Region Access Points > Create Multi-Region Access Points > name "reallyreallycriticalcatdata", add the 2 created buckets > Create (MRAP ARN arn:aws:s3::704310952405:accesspoint/m6s3xgw995fsb.mrap)
*NOTE: You CANNOT add or remove buckets to Multi-Region Access Point after it's cerated
3. Configure replication between the buckets: Access new MRAP > Replication & Failover tab > template:replicate among all specified buckets, Buckets: check both, Scope: Apply to all objects in bucket > Create replication rules
4. Test with CloudShell > Switch region to Tokyo > open CloudShell > enter "dd if=/dev/urandom of=test1.file bs=1M count=10" > copy ARN from MRAP dashboard, enter "aws s3 cp test1.file s3://[your-copied-mrap-arn]"
- Steps 3 and 4 generate a test file for upload, then uploads to the Sydney bucket. Replication of file to Canada bucket may take a few minutes
5. See remaining steps in the demo file in this repo
6. Clean up: s3 MRAP > select MRAP, delete > s3 buckets Empty and Delete


# VIRTUAL PRIVATE CLOUD (VPC) BASICS

## VPC Sizing and Structure
Step through the design choices around VPC design and IP planning. How to design an IP plan for a business; designing a VPC 

One of the first things to decide on is IP range; the VPC CIDR. 
- IMPORTANT: This planning is critical and is not easy to change later
- What size should VPC be? How many services need to fit, each service has an IP, each occupies space in VPC
- Are there any Networks we can't use, or need to interact with?
- Be mindful of IP ranges other VPC's used in other cloud env's in on-premise networks. Try to avoid IP ranges that other parties use that you might need to interact with
- Try to predict the future... How things may change
- VPC structure - Tiers, Resiliency (Availability) Zones

### VPC Sizing / Structure - Example: Animals4Life (A4L).
*NOTE: REVIEW IP RANGES: Network address, prefix, how they map to range of address
- 3 offices: London, NY, Seattle (3 IPs)
- Field workers (laptop, 3G, 4G, satellite, email, chat, file access, etc)
- Already has 3 existing networks. 192.168.10.0/24, 10.0.0.0/16, 172.31.0.0/16 (new AWS network design cannot use or overlap with these)
- Access/Migrate data
-- Avoid the following ranges:
--- 192.168.10.0/24 range is 192.168.10.0 -> 192.168.10.255
--- 10.0.0.0 (AWS) 10.0.0.0 -> 10.0.255.255
--- 172.31.0.0 (Azure) 172.31.0.0 -> 172.31.255.255 (this shares same IP address range as AWS defulat VPC, se we can't use default VPC for anthing production)
--- 192.168.15.0/24 (London) -> 192.168.15.255
--- 192.168.20.0/24 (NY) -> 192.168.20.255
--- 192.168.25.0/24 (Seattle) -> 192.168.15.255
--- 10.128.0.0/9 (google) -> 10.255.255.255
^ When designing an IP addressing plan, don't use any of the above 

### What IP ranges? How many networks does A4L need?
- VPC min /26 (16 IPs). max /16 (65536 IPs)
- Avoid common ranges to avoid future issues. 10.1 and 10.0 are common, avoid up to 10.10. Start at 10.16 per Cantrill's recommendation
- How many ranges a business requires? First, how many regions does AWS operate in? Since we're pre-allocating, overestimate for a buffer. A4L we don't really know how many regions they'll operate in, but we can make educated guess then add buffer. 
-- Suggest having at least 2 ranges in each regoin, in each AWS account
-- Assumed regions for A4L: 3 US, Europe, Australia (5) x2, and 4 AWS accounts. 3US + 1AU + 1EU = 5 Regions, 2 ranges ea. region, total of 10 IP ranges per account. Since there are 4 accounts, 10 ranges x 4 accounts = 40 IP ranges

#### IP Range Review: 
- We're going avoid 10.0 - 10.10 (too commonly used)
- Start at 10.16 per Cantrill
- Can't use 10.128 -> 10.255 because Google Cloud uses it
- Our Range: 10.16 -> 10.127 inclusive

### VPC Sizing
VPC Sizing Chart: https://imgur.com/a/cJhXTxx
- Deciding which to use on this chart? Two important Questions:
-- How many subnets will you need in each VPC?
-- How many IPs total? How many IPs per subnet?

#### VPC Sizing - How many Subnets?
- Services inside a VPC use subnets, which are where IP addresses are allocated from
- VPC Services run from within subnets
- A subnet is located in ONE availability zone

##### How many Availability Zones will your VPC use? 
- Start with 3 as DEFAULT, per Cantrill. And add at least 1 spare. DEFAULT: AT MINIMUM, always assume 4 AZ's
- Within VPCs, you also have tiers. Tiers for different types of infrastructure inside VPC; web tier, application tier, database tier... so 3, plus buffer. DEFAULT: assume 4 tiers.
-- 4 tiers, 4 AZ's. Each tier has a subnet in each AZ: 4x4 = 16 subnets. Using /16 VPC into 16 subnets, results in 1 smaller network ranges, each being /20. If we did /18 VPC prefix, each subnet would be /22
TOTAL: 16 subnets with /20 prefix

### VPC Sizing / Structure - Example: Animals4Life (A4L) - CONTINUED - PROPOSAL:
- A4L is a global org and could grow significantly (assume huge level of growth)
- Use the 10.16 -> 10.127 range (avoiding Google, common ranges, etc)
- 5 AZs
-- Start at 10.16 (US1), 10.32 (US2), 10.48 (US3), 10.64 (EU), 10.80 (AU) - each account has 1/4th of the range
--- total of 16 /16 network ranges for each region.
- 3 accounts: general, prod, dev. Add 1 more for buffer. 4 accounts total
-- Each account in each region gets 4 /16 ranges, enough for 4 VPCs per region per account
- /16 per VPC - 3AZ (+1), 3 tiers (+1) = 16 subnets for each VPC
- /16 splits into 16 subnets = /20 per subnet (4,091 IPs) - May seems excessive, but assume highest possible growth potential

### VPC Sizing & Structure Resources
https://aws.amazon.com/answers/networking/aws-single-vpc-design/
https://cloud.google.com/vpc/docs/vpc
https://github.com/acantril/aws-sa-associate-saac02/tree/master/07-VPC-Basics/01_vpc_sizing_and_structure


## Custom VPCs, includes DEMO
 Step through the architecture and features of Custom VPCs including the main issues which are raised in the exam
 - Learn to build a complex, mult-tier VPC
 
 In this multi-tier custom VPC build...
 - Using VPC us-east-1, 10.16.0.0/16
 - Inside VPC, 4 tiers in 4 AZs = 16 subnets.
 - We will create all 4 tiers: reserve, DB, app, web
 - We will only create 3 AZ's: A, B, C. We will not create subnets in the capacity reserved for the future AZ
 - We will be creating VPC, subnets, an internet gateway, NAT gateways, bastion host (using bastion host is bad practice - don't do it, not secure), NACLs
 
 
 ## DEMO - Custom VPCs - Create VPC - Overview
 - VPCs are regionally isolated and regionally resilient service. Operates from all AZs in that region.
 - Nothing is allowed IN or OUT of a VPC without explicit permission; provides isolated blast radius; if you have a proble inside a VPC, the impact is limited to that VPC and/or anything connected
 - Custom VPCs allow for simple or multi-tier; flexible configuration
 - Custom VPCs also provide Hybrid Networking
 - When you create VPC, you can pick DEFAULT or DEDICATED tenancy. AKA shared or dedicated hardware
 -- If you pick DEFAULT tenancy, you can choose on a per resource basis later on when provisioning resources whether it's shared or dedicated hardware
 -- If you pick DEDICATED tenancy at VPC level, it's locked in. Any resources created inside the VPC have to be on dedicated hardware (cost premium compared to Default)
 - By default, VPC uses IPv4 private/public IPs. The private CIDR block is main method of IP communication for VPC, & Puclic IPs (when you want make resources public)
 - VPC allocated ONE mandatory Private IPv4 CIDR Block
 -- Primary Block has two main restrictions: min /28 (16 IPs), max /16 (65,536 IPs)
 -- Optional to add secondary IPv4
 - Optional: VPC can use IPv6 by assigning /56 IPv6 CIDR to VPC (start appliny IPv6 as default as this is what's being adopted now)
 -- IMPORTANT: You can't pick a block of IP ranges like IPv4. Your range is either allocated by AWS, or customer can use their OWN IPv6 range 
 -- IPv6 doesn't have Public/Private concept, the range is all Publicly routable by default

 ### DEMO - Custom VPCs - Create VPC - DNS
 VPCs also have DNS. provided by R53
 - DNS is 'Base IP + 2', so if VPC is 10.0.0.0, then DNS IP is 10.0.0.2
 EXAM: 
 - Two critical options for how DNS functions in a VPC
 -- 1. First is a setting called enableDnsHostnames - Gives instances public DNS names
 -- 2. enableDnsSupport setting. Enables DNS resolution in VPC. Indicates whether DNS is enabled or disabled in VPC. If enabled, instances in VPC can use the DNS IP address
 
 ## DEMO pt.1 - Custom VPCs - Create/Configure VPC
 Steps through the architecture and features of Custom VPCs including the main issues which are raised in the exam
 
 ### STEPS pt.1
 1. Create the VPC: VPC > Your VPCs > Create VPC > select VPC Only > name tag "a4l-vpc1" > IPv4 CIDR "10.16.0.0/16" > IPv6 CIDR block "Amazon-provided IPv6 CIDR block", default us-east-1 > Tenancy set to Default > Create VPC
 2. VPC Settings: In VPC > Actions dropdown, "Edit VPC Settings" > DNS Settings check both Enable DNS Resolution and Enable DNS Hostnames < Save (for any resources in this custom VPC, if they have puclic IP addresses, they'll also get public DNS names)
 
 ## DEMO pt.2 - Custom VPCs - VPC Subnets
 Subnets are what services run from inside VPCs, within a particular Availability Zone. They're how you add function, structure, and resilience to VPCs
 NOTE: With AWS diagrams, color Blue is private and Green is for Public (green = Go = Public)
 - Subnets in a VPC start off Private and take config to make Public
 - Subnets are AZ Resilient. Created within on AZ and can never be changed. If AZ fails, subnet (and any contained services) fails
 EXAM: Subnet can NEVER be in multiple AZs. 1 subnet is in 1 AZ. An AZ can have 0 or more subnets
 - Default IP for subnet is IPv4 and is allocated an IPv$ CIDR, this CIDR is a subset of the VPC CIDR Block (has to be within VPC allocated range)
 EXAM: CIDR that a subnet uses cannot overlap with any other subnets in the VPC
 - Subnet can optionally be allocated IPv6 CIDR (/64 subset of the /56 VPC, space for 256 /64 ranges that each subnet can use. Note: VPC must also be config'd for IPv6
 - By default, subnets in a VPC can communicate with other subnets in the same VPC

 ### DEMO pt.2 - Custom VPCs - VPC Subnets - Subnet IP addressing
 - 5 IPs inside every VPC subnet are RESERVED
 -- Example: Subnet is 10.16.16.0/20, range of 10.16.16.0 -> 10.16.31.255
 --- Unusable Addresses: Network Address (10.16.16.0) - NOTE: Not just AWS, NOTHING uses first address on any IP networks
 --- Unusable Addresses: 'Network+1' Address (10.16.16.1) - VPC Router; logical network device that moves data between subnets
 --- Unusable Addresses: 'Network+2' Address (10.16.16.2) - Reserved VPC address, but generally for DNS
 --- Unusable Addresses: 'Network+3' Address (10.16.16.3) - Reserved Future Use
 --- Unusable Addresses: Network Broadcast Address (10.16.31.255) - LAST IP in subnet
 EXAM: if a subnet has 16 usable IPs... it actually only has 11, because 5 are reserved (3 for AWS (+1, +2, +3, 1 network (1st IP in range), one broadcast (last IP in range))
 - Dynamic Host Configuration Protocol (DHCP). VPC has a configuration object applied to it called DHCP Option Set. It's how computing devices receive IP address  automatically. 1 DHCP option set applied to a VPC at a time and flows through to Subnets. You can create DHCP option sets, but you CANNOT edit them. To change  settings, create a new DHCP and change the VPC allocation to the new DHCP Option Set.
 - On every subnet, you can define two IP Allocation Options: 1. auto-assign public IPv4 address 2. auto-assign an IPv6 address

 ### STEPS pt.2 - Creating lots of subnets
 3. Create Multiple Subnets with VPC multi-tier structure: VPC > Subnets > Create subnet > Select VPC (a4l-vpc1) > subnet name "sn-reserved-A" > IPv4 CIDR block "10.16.0.0/20" > IPv6 CIDR block, choose the one option, fill in unique IPv6 value for the respective subnet (00 for first one) > Add New Subnet > Repeat for each subnet in the AZ (4 total) > Verify Details in each > Create Subnet. Repeat for AZB, AZC.
 4. Auto allocate IPv6 Addressing: select sn-app-A > Actions drop down, "Edit Subnet Settings" > Auto-assign IP settings, check "Enable auto-assign IPv6 address" > Save > Do this for all new subnets
 
 ### Custom VPCs - Resources
 - VPC Limits https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html
 - Architecture https://raw.githubusercontent.com/acantril/aws-sa-associate-saac03/main/0800-VIRTUAL_PRIVATE_CLOUD(VPC)/00_LEARNINGAIDS/VPCStucture-1.png
 - CIDR review: https://aws.amazon.com/what-is/cidr/
 - Subnet Calculator : https://www.site24x7.com/tools/ipv4-subnetcalculator.html
 
 
 ## VPC Routing, Internet Gateway, & Bastion Hosts
Step through the architecture and functionality of Route Tables, Routes, Associations, the internet gateway and public IP v4 functionality within a VPC

### VPC Routing 
#### VPC Router
- VPC Router routes traffic between subnets. In every subnet, router has IP of network+1 address
- Every VPC has a VPC Router - Highly Available
- Controlled by Route Tables which influence what to do with traffic. Each subnet has one
- VPC created with what's known as a Main Route Table - subnet default (if you don't explicity associate a route table with a subnet, it gets the Main Route Table of the VPC). 
-- A subnet can only have ONE route table associated with it at any one time. But a Route Table can be associated with many subnets
-- If multiple routes match, the prefix is used as a priority. The higher the prefix value, the more specific the route, the more priority a route has. HOWEVER, Local Routes ALWAYS have priority.
-- All VPC's have at least one route: the local route. This matches the VPC CIDR Range

EXAM: Route tables are attached to 0 or more Subnets. A Subnet HAS to have a Route Table. It's either main route table of VPC or a custom route table. A route table controls what happens to data as it leaves the subnet(s). Local Routes are always present, un-editable, and match the VPC IPv4 or 6 CIDR range. For anything else, higher prefix values are more specific and have higher priority (except Local Route which always have highest priority)

### Internet Gateway
IGW is for data to exit-to and enter-from the Public Internet. A REGIONAL RESILIENT gateway attached to a VPC

EXAM: Internet Gateway (IGW) is a REGION RESILIENT gateway attached to a VPC. A VPC can have no IGW's or ONLY 1 IGW. An IGW can be created and not attached to a 
VPC (but again, it can only EVER be attached to ONE VPC at a time)

- IGW runs within the AWS Public Zone. IGW runs from the border of the Public Zone and VPC
- Gateways traffic between the VPC and the Internet/AWS Public Zone (S3..SQS..SNS..etc)
- Managed gateway; AWS handles the performance

#### Using an IGW
1. Create IGW
2. Attach IGW to VPC
3. Create custom Route Table
4. Associate Route Table to subnets
5. Then add IPv4 (and optionally IPv6) default routes to the route table with target being IGW
6. Config subnets to allocate IPv4 addressess (and optionally IPv6 addresses by Default)

### How IPv4 Addressing works inside a VPC
EXAM EXAM EXAM
Example: IPv4 EC2 Instance <-> IGW <-> Linux Update Server
- EC2 instance trying to send updates to Linux server.
-> The IPv4 instance has the private IP of 10.16.16.20, and IPv4 Public IP of 43.250.192.20. However, this isn't how it really works. what actually happens with public IPv4.. they never touch the actual services in a VPC. When you allocate a public IPv4 address, for example to this EC2 instance, a record is created which the IGW maintains, linking the instances Private IP to it's allocated Public IP
-> A packet for transit has Source and Destination IP addresses. At this point, packet is not configured with any public addressing (not currently routable accross public internet, could not currently reach the Linux update srever). Packet leaves instance, follows Default route to IGW. IGW sees packet is from EC2 based on source IP, and IGW knows the associated IPv4 address for this Source IP and changes Source address to IPv4 to be routable across internet. Linux Update server receives packet from Source IPv4 address. On the way back, the inverse happens

EXAM: At no point is the O/S on the EC2 instance aware of the public IP, it just knows of its Private IP (no IGW translation)
NOTE: Since IPv6 is publicly routable, the O/S on the EC2 instance would know it and it gets passed through IGW to sent without changing to a different IP (unlike IPv4 in the example above)

### Bastion Hosts (Jumpbox)
Bastion Hosts = Jumpbox. Entry point for private-only VPCs
- Instance in a public subnet
- Architecturally incoming managements connections arrive there
-- Once connected, can then go on to access internal-only VPC resources
- Generally the only entry point to a highly secure VPC


## DEMO - Configuring A4L public subnets and Jumpbox
Implement an Internet Gateway, Route Tables and Routes within the Animals4life VPC to support the WEB public subnets. Once the WEB subnets are public, we create a bastion host with public IPv4 addressing and connect to it to test.

** Jumpboxes are bad - but you need to understand how to spot bad things **

Currently in our VPC, all subnets are private and can't be used for communication with the internet or AWS Public Zone. We're going to reconfig the three "web" subnets to be public.

1. Create IGW: VPC > Internet Gateways > Create internet gateway > name "a4l-vpc1-igw" > Create
2. Attach IGW to VPC: In a4l-vpc1-igw, Actions dropdown "Attach to VPC" > select your VPC > Attach
3a. Make subnets Public, create Route Table (two Routes per subnet, IPv6 and IPv4): VPC > Route Tables, Create route table > Name "a4l-vpc1-rt-web" > select a4l VPC > Create
3b. Make subnets Public, config subnets: Route Table > select a4l rt > Subnet associations tab > Edit subnet associations > select web subnets (A,B,C) > Save > Routes tab
4. Add additional routes to Route Table (default routes for IPv4/6): VPC > Route Tables > select a4l rt > Routes tab, Edit Routes > Add Route > destination for IPv4 0.0.0.0/0 > target: internet gateway, select yours > Add another route, destination "::/0" (targets all IPv6), target: IGW > Save changes
5. Allocate resources with IPv4 public addresses: Subnets > select web A > ACtions > Edit Subnet Settings > check "Enable auto-assign public IPv4 address" > Save> Repeat for web B and C
6. Test configuration: EC2 > Launch Instance > name "A4L-BASTION" > Quickstart: Amazon Linux 2023 > Architecture: 64 bit, instance type: t2 micro, keypair: a4l > Netowkr Settings, VPC: A4L-VPC1, Subnet "sn-web-a", auto assign IPv4/6 "Enable", select "creat esecurity group" and name/description "A4L-BASTION-SG" > Launch Instance
7. Connect to Instance: Right-click instance, "Connect" > EC2 Connect > Connect > SSH tab, copy ssh command > Open Terminal, CD to Downloads, paste command to connect > Yes for fingerprint thing
8. Cleanup: Select A4L instance, Instance State: Terminate > VPC, select A4L vpc, Actions > Delete VPC

NOTE: When connecting to EX2 instances that have IPv4 address, you can use EC2 instance connect or Local SSH client
- Session Manager can connect you if you don't have IPv4 addressing


## Stateful vs Stateless Firewalls
TCP and IP Review: They work together.
- Transmission Control Protocol. Connection based protocol. When you make a TCP connection, each side is sending IP packets to each other (they have a srouce/destination IP). TCP is a Layer 4 Protocol that lies on top of IP. It adds error correction with the idea of ports. HTTP is TCP Port 80, HTTPS is TCP port 443

EXAM: Every CONNECTION between user/server has two parts: 1. REQUEST (initiation) 2. RESPONSE.

What actually happens:
Client pick temporary "ephemeral" port 2. client initiates server connection REQUEST using well-known port number (like Port 443 HTTPS) 3. Server RESPONDS using source port of tcp/443 and ephemeral port picked by client 4. 
- Directionality depends on your perspective. What is INBOUND/OUTBOUND -- Source/Dest swap depending on who's perspective. 

### Stateless Firewalls
Ex. Server is within a stateless firewall; meaning that it doesn't understand the state of connections (it sees REQUEST/RESPONSE as separate parts, so you need 2 rules needed for each connection). 
- TWO Rules needed for each connection, 1 IN 1 OUT
- Because firewall is stateless, it doesn't know which specific port is used for the response. You'll often have to allow the FULL RANGE of ephemeral ports to any destination
-- This makes security engineers uneasy, which is why Stateful Firewalls are preferred.

### Stateful Firewalls
A Stateful Firewall is intelligent enough to ID the REQUEST and RESPONSE components of a connection as being related
- ONE RULE per connection; Allowing the REQUEST (inbound or outbound) means the RESPONSE (IB or OB) is automatically allowed; this reduced admin overhead and the chance for mistakes
- You DO NOT need to allow full Ephemeral Port range


## Network Access Control Lists (NACLs)
A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC. 
- NACL only impacts data crossing the subnet boundary
- NACLs are STATELESS
- Can EXPLICITLY ALLOW AND EXPLICITLY DENY; you can block specific IPs/IP Ranges associated with bad actors
- NACLS not aware of Logical Resources. They only allow you to use IP and CIDR ranges, ports and protocols

First, NACLs are associated with Subnets. NACLs work with IB and OB traffic from VPC.
- Each network ACL contains TWO sets of rules. Inbound and Outbound rules/protocols. Rules match the destination (DST) IP/Range or the DST Port, together with the protocol and ALLOW or DENY based on that match
- NACL response to client requires using the ephemeral port range (chosen at random by client/requester)
- NACLs cannot be assigned to AWS resources, ONLY subnets
- Often used together with Security Groups to add an explicit DENY. Using SGs to ALLOW traffic, NACL to DENY
- Subnet can only have ONE NACL, but a NACL can be associated with many subnets

EXAM: NACLs filter traffic crossing the subnet boundary INBOUND or OUTBOUND. NACL only impacts data crossing the subnet boundary (communications between instances in the SAME subnet is not affected.
EXAM: NACLs offer both EXPLICIT ALLOWS and EXPLICIT DENIES. Rules are processed in order, lowest rule number first. Once a match occurs, processing STOPS. * is an implicit DENY if nothing else matches
EXAM: NACLs are stateless and require TWO RULES per connection: 1x OUTBOUND, 1x INBOUND

### NACLs and multi-tiered architecture (operating across multiple subnets)
Becomes more complex with multi-tiers. Internal communications also required IB/OB rules on the app subnet NACL. If you have a CLIENT (external), a WEB subnet and APP subnet, connection rules are required for all IB/OB movements whether in between web/app subnets or between client and web subnet
- For every single communication, the rule-pairs app port (IB) and ephemeral ports (OB) are needed on each NACL for each communication type which occurs 1) within a VPC 2) TO a VPC 3) FROM a VPC

### Default NACL. Default has IB/OB Rules with implicit deny (*) and a catch-all ALLOW ALL rule (0.0.0.0/0)
### Custom NACL. Created for a specific VPC and initially NOT associated with subnets. Only ONE IB/OB rule by default: implicit deny (*)--so at first, if you associate subnets, all traffic will be denied


## VPC Security Groups (SG)
Security Groups (SGs) are another security feature of AWS VPC ... only unlike NACLs they are attached to AWS resources, not VPC subnets. SGs offer a few advantages vs NACLs in that they can recognize AWS resources and filter based on them, they can reference other SGs and also themselves. But.. SGs are not capable of explicitly blocking traffic - so often require assistance from NACLs
- SGs are STATEFUL; if you allow IB/OB request, the response is automatically allowed
- Major limitation of SGs: no explicit deny. Can be used to allow traffic or NOT Allow traffic (which is an implicit Deny). This means they can't be used to block specific bad actors
-- This is why you use NACLs in conjunction with SGs, because NACLs are used to add the explicit denies
- Supports IP and CIDR, but also allows referencing AWS Logical Resources, including other SGs and ITSELF within rules
- SGs are NOT attached to Instances/Subnets, they are attached to Elastic Network Interfaces (ENI). An instance has a primary ENI

EXAM: Security groups are attached to ELASTIC NETWORK INTERFACES (AWS Resources), not instances/subnets
EXAM: SGs cannot EXPLICITLY DENY traffic, must be paired with NACL to have an Explicit Deny

### SG - Logical References
Ex. Within VPC, we have APP and WEB subnets. Both APP and WEB are protected by SGs. External User is accessing web app via port tcp/443, allowing 0.0.0.0/0. Web to App is using tcp/1337. How do you best allow communication between WEB and APP? To take advantage of extra SG features, we could reference the web security group within the APP SG. In this, the Source for the IB Rule on APP is specifically the logical resource reference of the WEB SG
- EXAM: An SG Reference applies to anything which has the SG attached. When you're referencing an SG from another SG, you're actually referencing any resources which have the SG associated with them

### SG - Self Referencing
Ex. Private Subnet in AWS with ever-changing number of app instances. An IB Rule in each instance can have its own SG referenced, allowing traffic between any other instances with that SG.
EXAM: SG Self referencing handles IP changes automatically
EXAM: Also allows for simplified management of any intra-app communications (Eg. Microsoft Domain Controls, or apps with high availability within clusters
EXAM: SGs cannot EXPLICITLY DENY traffic. Pair with NACL to explicitly deny bad actors


NOTE: A logical resource is an abstraction that doesn't cost you anything.  It's a definition.  Something becomes a physical resource when it starts to cost you in terms of compute and store. In terms of cloud formation, you can define logical resources that are then used to create physical resources.  Within the template, you refer to things using the logical name.  Once things are deployed, you'll see deployed resources having physical IDs. In essence, a physical resource in AWS is a realized resource that consumes AWS infrastructure and services rather than a logical representation of one.


## NAT (Network Address Translation) and NAT Gateway
What is NAT? A process of giving a private resource outgoing-only access to the internet. Set of processes which adjusts IP packets by changing their source or destination IP addresses from the private IPs to the Public NAT Gateway IP
- IGW performs a "Static NAT"; how a resource can be allocated with a public IPv4 address
- IP Masquerading. A subset of NAT that hides private CIDR Blocks behind ONE IP
- NAT is many private IPs to one single IP, this is popular as IPv4 addresses are running out. 
- Gives Private CIDR ranges OUTGOING internet access or AWS public services
- NAT is not required for IPv6, only IPv4. All IPv6 addresses are PUBLICLY ROUTABLE
- Need bi-directional connectivity on an instance? use IPv6 default route and point to IGW as target: ::/0 Route+IGW 
- Outgoing ONLY access for an IPv6 instance? You need ::/0 Route + "Egress-Only IGW"

AWS can provide NAT services in TWO ways:
1. EC2 instance config'd with NAT (cheaper)
2. NAT Gateway - Configured inside VPC (better)

### NAT Gateway (we'll use IP Masquerading interchangeably)
NAT Gateway is provisioned into a PUBLIC subnet (like WEB subnet, in our examples), which can use public IP addresses. The Private Subnet has a route table that can point all its instances to the NAT Gateway within the WEB subnet.
- NATGW contains a Translation Table, where all required packet data is stored: IP address, src, dst, port #, etc
- Has to be run from a PUBLIC subnet (obviously). To have Public Subnets, you need an IGW, IPv4 allocation enabled on subnets, and default routes for the subnets pointing at IGW
- Elastic IPs - NAT Gateways use Elastic IPs. These are IPv4 addresses that are static and don't change. NATGW is the only AWS service that uses Elastic IPs
- NATGW's are an AZ resilient service. To attain Region Resilience, you need a NATGW in EACH AZ, and have a Route Table in each AZ with that NATGW as the target. So, for every AZ you use, you need one NAT Gateway and one Route Table pointing at said NATGW

EXAM: NATGW's are a managed service. Scales to 45 Gbps. 
EXAM: NATGW's Billing: Hourly charge for running it (like 4 cents per hour, and partial hours are billed as full hours), data processing charge (per GB of processed data)
EXAM: FALSE - Exam may suggest 1 NATGW is sufficient, that 1 is regionally resilient. FALSE. If you want regional resilience, you have to deploy NATGW into each AZ you use.
EXAM: If you want to allow an EC2 instance to function as a NAT instance, Disable SOURCE/DESTINATION CHECKS
EXAM: NAT/NATGW isn't required/doesn't work with IPv6
EXAM: NATGW's are AVAILABILITY ZONE RESILIENT. If you want regional resilience, you have to deploy NATGW into each AZ you use.

### Scenarios where a NAT instance may be preferred over EC2+NATGW:
- If you value availability, bandwidth, low maintenance, and high performance choose NATGW
- NAT Instance will fail if AZ fails. A NATGW is highly available in 1 AZ--highly available (automatically recover and scale), but will still fail entirely if AZ fails entirely. For MAX Availability, have a NATGW in every AZ you use.
- If Cost is the primary issue, a NAT Instance can be cheaper. Especially at high volumes.

EXAM: NAT Instance can be used as a Bastion Server
EXAM: NATGW CANNOT be used as Bastion Server, cannot do port-forwarding, b/c you can't connect to its operating sysytem (AWS Managed)
EXAM: NATGW does NOT support Security Groups; you can only used NACLs with NATGW
EXAM: NATGW is NOT Free Tier eligible
EXAM: NAT Instances are just EC2 instances


## DEMO - NAT Gateways - Implementing private internet access using NAT Gateways
Implement a highly-available regionally resilient NAT Gateway solution within the Animals4life VPC. You will create three Nat Gateways, Route tables and Default Routes with the Nat Gateway as a target and finally associate those Route Tables with the Reserved, App and DB subnets in AZ A, B and C before testing the solution using the internal instance.

1. One-click deployment: click lesson link > acknowledge
2. Confirm resources done provisioning: CFN > Stacks Resources > A4L Resources tab > Click Instance ID for A4LINTERNATEST > On EC2, Connect to instance with Session Manager -- You'll see no internet connectoin
NOTE: Session Mgr allows connection to an EC2 instance that has no public internet connectivity
3. Connect to Internet with NATGW: VPC > NATGQ, Create NATGW > name "a4l-vpc1-natgw-A", subnet sn-web-A, Elastic IP: click 'Allocate' > Create NATGW > Repeat for B, C
4. Configure Routing, Route Table: VPC > Route Tables > Create route table > select VPC a4l-vpc1, name "a4l-vpc1-rt-privateA" > Create > repeat for B,C
5. Create Default route in each RT: select RT "privateA" > Routes tab > Edit routes > Add route > DST 0.0.0.0/0, target NATGW A > Save Changes > Repeat for B, C 
6. Associate Route Table with subnets: VPC Route Tables, select web-A, Edit subnet associations > select private subnets (app, db, reserved) > Save associations > Repeat for B, C
7. Cleanup: Edit subnet associations > uncheck all > save (x3) > Delete RTs > NATGWs: actions: delete (x3) > Elastic IPs: Release (x3) > CFN: Delete A4L stack



# EC2 Basics

## Virtualization 
Emulated Virtualization
Paravirtualization
Hardware Assisted Virtualization
SR-IOV

EC2 provides virtualization as a service (IaaS). It is dealing with the process of running more than one O/S on a piece of physical hardware. Within an O/S, parts of it, the kernel run in what's called Priveleged Mode -- meaning it can interact with the system's hardware. Above the O/S are applications that run in User Mode (or un-priveleged mode) (cannot interact with hardware). An app would have to make a SYSTEM CALL to the kernel to interact with hardware. IF anything but the O/S attempts to make a priveleged call, the system will detect and cause a system-wide error, generally crashing the system (or at min the app) <- THIS IS HOW IT WORKS WITHOUT VIRTUALIZATION
- Virtualization is a single piece of hardware running multiple O/S's
- Nowadays, with multiple O/S's on a single bit of hardware, all O/S's expect to be priveleged and this conflict can cause crashes -- Virtualization is the solution to this problem
- Virtualization used to have to be done as software and was slow
-- First way was EMULATED VIRTUALIZATION (included hypervisor capability performing Binary Translation, creating Virtual Machines) - super slow
-- PARA-VIRTUALIZATION. O/S's running in virtual machines, but instead of Binary Translation, they modify the guest O/S's to make Hypercalls. This requires O/S modification

### Hardware Assisted Virtualization
The major improvement to virtualization as it made the physical hardware became virtualization aware. When guest O/S's attempt priveleged instructions, they're trapped by CPU (which expects this) so the system does not halt. 

### SR-IOV
Single-root IO Virtualization. Allows a network card to present itself as several "mini cards". Splits a physical card into several logical cards to present to guest O/S's

SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. There is no additional charge for using enhanced networking. SR-IOV enables network traffic to bypass the software switch layer of the Hyper-V virtualization stack. 

### Virtualization Resources
http://www.brendangregg.com/blog/2017-11-29/aws-ec2-virtualization-2017.html


## EC2 Architecture and Resilience
Looking specifically at EC2 Hosts, how they are physically architected, why they are AZ resilient, and how the resilience of the Elastic Block Store (EBS) factors into our decisions as Solutions Architects.
- EC2 instances are Virtual Machines (VMs = O/S + Resources) 
- EC2 instances run on EC2 Hosts, they're either SHARED (across different AWS customers, Shared is Default) or DEDICATED hosts
- EC2 is AZ resilient service. If AZ fails, Host Fails, Instances Fail

### EC2 Hosts
EC2 hosts have some local hardware--CPU and memory, but also local storage called Instance Store. 
- They have two types of networking:
1. Storage Networking
2. Data Networking
When instances are provisioned into a specfic subnet within a VPC, a primary Elastic Network Interface is provisioned in a subnet which maps to the physical hardware on the EC2 host. 
- EC2 Host can connect to the Elastic Block Store (EBS). EBS also AZ Resilient. EBS let's you allocate volumes of portions of persistent storage, and these are allocated to instances in the same AZ.
- EBS = Network based storage
- An Instance runs on a specific host and if you restart the instance, it will stay on that host. An instance will stay on a host unless one of 2 things happens:
-- 1. If the host fails or is taken down for maintenance by AWS
-- 2. If an instance is STOPPED, then restarted (different than just restarting)

EXAM: An EC2 Host runs within a SINGLE AZ. They are AZ Resilient.
EXAM: EC2 Instances are locked inside one sepcific AZ. Same with EBS volumes
- Migrations to new AZs are 'possible', but it's copying an instance into a new AZ (snapshots and AMIs)
- Instances runnings on an EC2 Host share the host's resources. You can have instances of different size sharing host, but generally same size/type of EC2 instance shares a host

### What's EC2 Good For?
For traditional style workloads, for consistency, if you require an O/S...
- Great for when you have traditional O/S+Application compute needs
- Great for Long Running Conmpute needs.
- Server style application (traditional app in an o/s awaiting incoming connections)
- Great for occasional bursts in traffic and steady state load requirements
- For monolithic application stacks
- For migrating application workloads
- Disaster Recovery (creating this dis.rec. env)


## EC2 Instance Types
EC2 instance Categories, how to decode the instance type names (family, generation, features & size), hints and tips on remembering the Instance type differences
- Reminder: EC2 instance = O/S + allocation of resources
- You can select instance type/size for more control

Choosing a different instance type influences a few things...
- The raw amount of resources you get: virtual CPU, memory, local storage capacity, and type of storage
- Resource Ratios
- Storage and Data Network Bandwidth
- Influences system architecture and vendor
- Additional feature and capabilities differ between Instance Types. Ex. allocation of GPUs, certain capacity of field programmable gate arrays (FGPAs)

### EC2 Instances - Grouped into 5 Main Categories:
1 - General Purpose (Default): Diverse workloads, equal resource ratios
2 - Compute Optimized: Designed for media processing, high performance computing, modeling, gaming, ML; access to the latest high performance CPUs. Resource Ratio where more CPU is offered the memory 
3 - Memory Optimized: Inverse of Compute Optimized. Processing large in-memory datasets (Ex. in-memory caching), some database workloads
4 - Accelerated Computing: Dedicated GPUs for high scale parallel processing and modeling, custom programmable hardware known as field programmable gate arrays (FGPAs). Accelerated Computing category is often for niche requirements; you'll know when you need this category
5 - Storage Optimized: Large amounts of super fast, local storage. Massive amounts of IO operations/second, scale out transactional databases, data warehousing, Elasticsearch, analytics workloads. The Storage Optimized category is great for applications that have serious demands on sequential and random IO.

### EC2 Istance Types: Decoding the naming scheme
Ex. R5dn.8xlarge. <- Example of type of EC2 instance
- This is known as an Instance Type. If ops team member asks what instance type we need? You'd provide this full name
- Start letter, R, is the INSTANCE FAMILY
- 2nd character, 5, is the INSTANCE GENERATION. For example, a C4 would be the 4th generation of the C family of instance. Always select the most recent generation, with exception
- "8xlarge" is the size of the instance. Sizes: Nano, mirco, small, medium. large, xl, 2xl, 4xl, 8xl, and so on... Price premium on higher end... often better to scale system with large number of small sizes
- "dn" can vary... this collection of letters between family-generation and size may not always be present. These letters denote add'l capabilities. Ex. 'a' signifies AMD CPUs (you don't need to memorize these letters for the exam)

* Table / Visual of Instance Categories/Types/Details and Notes: https://imgur.com/a/LXpddQS
** 'c' stands for computer. Compute Optimized
** 'r' stands for RAM. Memory Optimized
** 'I' stands for I/O. Storage Optimized
** 'D' Dense Storage. Storage Optimized
** 'G' GPU. Accelerated Computing
** 'P' Parallel Processing. Accelerated Computing

### EC2 Instance Type Resources
- https://aws.amazon.com/ec2/instance-types/
- https://ec2instances.info/
- Table / Visual of Instance Categories/Types/Details and Notes: https://imgur.com/a/LXpddQS


## DEMO - EC2 SSH vs EC2 Instance Connect
Amazon EC2 Instance Connect provides a simple and secure way to connect to your Linux instances using Secure Shell (SSH). With EC2 Instance Connect, you use AWS Identity and Access Management (IAM) policies and principals to control SSH access to your instances, removing the need to share and manage SSH keys.

1. Make keypair for SSH: EC2 > Key Pairs, Create key pair > since we already have 'A4L' kp, we're good
2. 1-Click Deploy: Click 1-Click Deploy lesson link > Create Stack, Acknowledge, Create stack
3. Connect to Instance via SSH: EC2 > Instances > A4L, Connect, SSH Client > Open your Terminal > cd to directory with Key Pair .pem file > Paste command, Enter, 'Yes' for fingerprint
4. Connect with EC2 Instance Connect:  EC2 > Instances > A4L, Connect, EC2 Instance Connect
- NOTE: EC2 Instance Connect is not originating connections through your machine (not your IP)
5. Clean up > CFN > Delete Stack 


## Storage Refresher
### Key Terms:
- DIRECT (local) attached storage: Storage on the EC2 Host
- NETWORK attached storage: Volumes are created and attached to a device over the network. In AWS, uses EBS (Elastic Block Store). Highly resilient, separate from instance hardware
- EPHEMERAL storage: Temporary storage, non-persistent. This is the Instance Store, physical storage attached to an EC2 Host
- PERSISTENT storage: Permanent storage that lives past the lifetime of an instance.
EXAM: An example of Persistent Storage in AWS is the networked attached storage delivered by EBS. Know which types of storage are Ephemeral and Persistent

### Categories of Storage:
- BLOCK storage: Create a Volume (Ex. inside EBS) that is presented to the OS as a collection of blocks; NO STRUCTURE beyond that. Mountable. Bootable.
- FILE storage: Presented as a file share/file server WITH STRUCTURE. Mountable. NOT bootable.
- OBJECT Storage: Collection of objects. NO STRUCTURE; flat. NOT mountable. NOT bootable.

### Storage Performance 
These items don't exist in isolation. IOPS is like speed of engine a racecar runs at (revolutions per second), IO block size is like the size of the car's wheels, throughput is the top-speed of the racecar. 
- IO BLOCK SIZE: Size of the data you're writing to disk. 
- IOPS: Measures the number of I/O operations a storage system supports in a second (how many read/writes in a second)
- THROUGHPUT: Amount of data that can be transferred in a given second, MB/s. 
* IO x IOPS = Throughput
** Ex. 16KB IO block size x 100IOPS = 1.6MB/s throughput


## EC2 - EBS Service Architecture
Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. EBS volumes behave like raw, unformatted block devices. You can mount these volumes as devices on your instances. EBS volumes that are attached to an instance are exposed as storage volumes that persist independently from the life of the instance. You can create a file system on top of these volumes, or use them in any way you would use a block device (such as a hard drive).
- EBS can be encrypted using KMS
- When you attach a volume to an EC2 instance, the instance sees a Block Device, so raw storage.
- EBS volumes appear just like any other storage device to an EC2 instance
- EBS Volumes are attached to ONE instance at a time. However, can be detached and re-attached to a new instance. They are not lifecycle linked to one instance, they're persistent; if an instance moves to a new EC2 host, the volume follows it. EBS is persistent until you delete the volume (separate from the instance)
- Snapshot into S3: You can create a backup of a volume with a Snapshot into S3. This can be used to migrate volumes between AZs. 
- EBS can provision volumes based on different physical storage types: SSD, high-performance SSD, volumes based on mechanical disks, different size volumes, different performance profiles
- BILLING: Gigabyte/Month metric (and in some cases, performance)

EXAM: Storage is provisioned in ONE AVAILABILITY ZONE; Resilient in that AZ
EXAM: Snapshots are now REGIONALLY RESILIENT


### EBS Example - 1 region, 2 AZs (AZA, AZB), 1 S3 bucket.
EBS is AZ-based. So, with two AZs you have two separate EBSs. Same as EC2 hosts--per AZ
- EBS replicated data within an AZ. Failure of an entire AZ means failure of all volumes in that AZ. To fight this, you can Snapshot volumes into S3, creating more resilience, and you can create another volume in a new AZ from this snapshot (or even to a new region)
- For Global Resilience on volumes, copy snapshots over to different regions


## EC2 - EBS Volume Types 
General Purpose SSD — Provides a balance of price and performance. We recommend these volumes for most workloads.
- Volumes can very in size from 1GB -> 16TB
- When created, a volume is given an I/O credit allocation

### EBS Volume Types - General Purpose (GP):
1. GP2. GP2 is the default general purpose SSD based storage provided by EBS. CREDIT ARCHITECTURE
- GP2 gets 3 IO credits per second, per GB of volume size
- "Burst Rate": GP2 volume can burst up to 3,000 IOPS
- Max IOPS for GP2 is currently 16,000 IO credits per second (baseline performance) - Any volumes > 5.33TB in size achieves this rate constantly
- Great for: boot volumes, low latency interactive apps, dev/test environments
- GP2 auto scales on size

2. GP3. SSD based, but removed the credit architecture GP2 
- Every GP3 volume, regardless of size starts with 3,000 IOPS and 125MiB/s
- ~20% cheaper than GP2
- Need more performance? Can pay for up 1o 16,000 IOPS or 1,000 MiB/s
- GP3 does NOT auto-scale, you have to enable the upgrades

#### IO Credit. When you create a volume (size ranging from 1GB -> 16TB), it is created with an IO credit allocation. 
- An IO is one input/output operation
- IO credit is a 16KB chuck of data
- An IOP is one chuck of 16KB in one second
- Ex. If transferring a 160KB file, that's 10 IO blocks of data. If this is all done in 1 second, that's 10IOPS. (IO x IOPS = Throughput -> 10 x 1 = 10IOPS)
- 1 IOPS is 1 IO in 1 second
- IF you have NO credits in your IO "bucket" in the volume, you can't perform any IO on the disc
- IO Bucket has capacity of 5.4 million IO credits and "Fills at the rate of Baseline Performance"
- "Fills at the rate of Baseline Performance"... what does this mean? Every volume has baseline performance based on size, with a minimum
-- IO Bucket bills with minimum of 100 IO Credits per second REGARDLESS OF VOLUME SIZE

## EC2 - EBS Volume Types - Provisioned IOPS (io1, io2, io2 Block Express)
Provisioned IOPS SSD — Provides high performance for mission-critical, low-latency, or high-throughput workloads.
- Three types of provisioned IOPs SSD: io1, io2, io2 Block Express
- IOPS are configurable independent of volume size and designed for super high-performance situations
- Max 64,000 IOPS/volume
- io1/io2, 1,000MB/s throughput
- io2 Block Express: 256,000 IOPS, 4,000MB/s throughput
- Size: 4BG -> 16TB for io1/io2. io2 Block Express 4GB -> 64TB
- Size-to-performance ratio maximums: io1 50IOPS/GB, io2 500IOPS/GB, io2 Block Express 1000IOPS/GB
- Per Instance Performance restriction: the max performance between the EBS svc and an EC2 instance
- NUMBERS (all the specs for Provisioned IOPS): https://imgur.com/a/zYQk7G1

EXAM: Provisioned IOPS: Most consistent low latency and jitter. 
EXAM: Prov.IOPS for sub-millisecond latency, consistent latency, and higher performance.


### EC2 - EBS Volume Types - HDD-Based*
* Slower, only for specific situations
Types:
1. Throughput Optimized HDD (st1) — A low-cost HDD designed for frequently accessed, throughput-intensive workloads. For sequentially accessed data like streaming
-- Big data, data warehouses, log processing
2. Cold HDD (sc1) — The lowest-cost HDD design for less frequently accessed workloads. 
-- geared for max economy (lowest EBS cost option) with lowest performance

HDD Based EBS Volume Type METRICS: https://imgur.com/a/EcGVrx8


## EC2 - Instance Store Volumes - Architecture
An instance store provides TEMPORARY block-level storage devices for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for TEMPORARY storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type.

The virtual devices for instance store volumes are `ephemeral[0-23]`. Instance types that support one instance store volume have ephemeral0. Instance types that support two instance store volumes have `ephemeral0` and `ephemeral1`, and so on.

- ISV = HIGHEST STORAGE PERFORMANCE in AWS
- Physically connected to ONE EC2 host - isolated to host
- If instance moves between host, data that was stored on attached ephemeral[X] is lost and instance is re-attached to new ephemeral[X]
- Instance Store Volumes should NOT be used for anything the requires persistence
- More IOPS and Throughput VS EBS

EXAM: Local to an EC2 Host
EXAM: Data stored on Instance Store Volumes is lost on instance MOVE, RESIZE, or HARDWARE FAILURE
EXAM: HIGHEST STORAGE PERFORMANCE storage option in AWS, but can't provide persistence. TEMPORARY, for replaceable data
EXAM: Instance Store Volumes have to be ATTACHED AT LAUNCH OF INSTANCE, cannot happen after. Instances on this host only can access them

## Choosing between the EC2 Instance Store Volumes (ISV) and EBS
Resource: https://aws.amazon.com/ec2/instance-types/

Need...
Persistence? EBS (avoid ISV)
Resilience? EBS (avoid ISV)
Isolated from Instance Life Cycles? (to be able to un-attach and re-attach) EBS (avoid ISV)
Resilience w/App In-Built Replication... it depends
High Performance? Depends (ISV is super high performance)
Cost is main factor? ISV (it's often included in the price)

REMEMBER ALL OF THIS:
EXAM: Cost Efficacy? ISV ST1 or ISV SC1. For throughput + streaming? ST1
EXAM: Boot EC2 instances? NOT st1 or sc1
EXAM: GP2 / GP3: Has a max performance of 16,000 IOPS
EXAM: IO1 / IO2: Has max 64,000 IOPS (256,000 IOPS in io2 Block Express) - Max EBS performance with large instance (that is capable of providing this performance)
EXAM: RAID0 + EBS: Has max 260,000 IOPS
EXAM: Need anything greater than 260,000 IOPS? use ISV, not EBS. *No persistence
EXAM: EBS Automated Backups? Amazon Data Lifecycle Manager: To automate the creation, retention, and deletion of Amazon EBS snapshots

TL;DR EBS Volume VS Instance Store
- EBS volume is network attached drive which results in slow performance but data is persistent meaning even if you reboot the instance data will be there.
- Instance store instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer.
-- Data on an instance store volume persists only during the life of the associated instance; if an instance is stopped or terminated, any data on instance store volumes is lost.

SSD: General Purpose (gp2, gp3), Provisioned IOPS SSD volumes (io1, io2, io2 Block Express)
HDD: st1, sc1

## EC2 - EBS Snapshots, Restore & Fast Snapshot Restore (FSR)
- EBS Snapshots are backups of data consumed within EBS Volumes - Stored on S3.
- Snapshots are incremental, the FIRST COPY being a full backup - and any future snapshots being incremental. No massive risk of losing incremental backups (each increment is self-sufficient)
- Snapshots can be used to migrate data to different availability zones in a region, or to different regions of AWS.
- AZ Resilient (vulnerable to issues which impact entire AZ), but with a snapshot the data becomes Region Resilient
- Good for EBS Volume cloning, even moving / copying them across AZs
- BILLING: Gigabyte-month cost; but you're only paying for USED data, not allocated data

EXAM: Snapshot doesn't need to be initialized in a new EBS Volume, it's built-in
EXAM: Snapshots are restored LAZILY; fetched gradually
EXAM: Requested blocks are fetched immediately, you can do this initially to force rapid initialization so users have quickest access up front
EXAM: Fast Snapshot Restore (FSR): A setting to Enable that allows immediate restores instead of gradual
EXAM: Up to 50 FSRs per region. Set on the Snap & AZ, so 50 between AZs
EXAM: FSR costs extra


## DEMO - EC2 -  EBS Volumes
Commands for Terminal: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0004-aws-associate-ec2-ebs-demo/lesson_commands.txt
1. Create an EBS Volume: 1-Click Deploy link > Create Stack > EC2 EBS > Create Volume > select GP2, 10 GiB size, AZ us-east-1a, tag: kay "Name" value "EBSTestVolume" > Create
2. Mount it to an EC2 instance: Select new EBS Volume > Actions: Attach Volume > Choose Instance1 > Attach
3. Create and Mount a file system: Ec2 Instance > select A4L-EBS-INSTANCE1-AZB, Connect > EC2 Instance Connect > `sudo mkfs -t xfs /dev/xvdf`, Enter
4. Generate a test file: EC2 Connect > `sudo mkdir /ebstest`, Enter > Mount dev/xvdf to /ebstest directory `sudo mount /dev/xvdf /ebstest` > cd /esbstest > `sudo nano amazingtestfile.txt` > write text, ctrol+o, enter, ctrl+x > Reboot instance `sudo reboot`
5. Migrate volume with Snapshot: EC2 > Instances > Stop AZA Instance 1 and 2 > when stopped, Volumes: Detach Volume > right click EBS Volume, Create Snapshot > Right click Snapshot, Create Volume from Snapshot > Zone us-east-1b > Tag key "Name" value "EBSTestVolume-AZB" > Create 
6. Attach Volume to AZB instance: Volume > right click, Attach > ABZ Instance 1 > ATtach
7. Verify the filesystem and file are intact > EC2 Instance Connet on AZB Instance 1 > `lsblk` > `sudo mkdir /ebstest` > `sudo mount /dev/xvdf /ebstest`
8. Stop AZB Instance > Detach EBS Volume
9. Clean up > Detele Snapshopt > Volumes: delete test volumes > CloudFormation: Delete Stack
* The remaining DEMO is not FREE TIER
* On Instance Store Volumes, Instance reboot does not cause the data to be lost or moving to new host, but a Stop/Start changes hosts and you lose data


## EC2 - EBS Encryption
EBS Encryption provides AT REST encryption for volumes and snapshots.
- Uses KMS: AWS/EBS Keys or Customer Managed Keys
- Uses DEK

EXAM: AWS Accounts can be set to encrypt by default - Default KMS Key
EXAM: Each Volume uses ONE unique DEK. Snapshots and future volumes use the SAME DEK. Volume from scratch? New DEK
EXAM: There is NO WAY To remove an encryption from a volume, unless you clone data to a new volume
EXAM: O/S is not aware of the encryption (no performance loss)


## EC2 - Networks Interfaces, Instance IPs and DNS
Elastic Network Interfaces (ENIs) which can be allocated to EC2 instances - and the DNS, public, private and elastic IPs which can be assigned to those ENIs
- Each EC2 Instance starts with one ENI (primary ENI). You can attach more ENI's, but to different subnets
- Lots of things are attached to ENIs and not instances: Security groups, lots of IP stuff, Source/Destination checks
- You can detach secondary ENIs and move them to different instances
- ENIs contain...
-- Primary Private IPv4 address
-- Secondary Private IPv4 address
-- Optionally, 1 public IPv4 address
-- Optionally, 1 or more Elastic IP addresses

### EC2 - Elastic IP address
Allocated to your AWS account. If Elastic IP assigned, it removes the Public IPv4 and replaces with the Elastic IP

EXAM: If you assign Elastic IP and remove it, can you get the original, replaced IPv4 address back? NO, you get a different one back
EXAM: Secondary ENIs + MAC addresses = Licensing that can move between instances
EXAM: Multi-homed (subnets) Management & Data: An instance with an ENI in two different subnets (maybe use one for management and one for data)
EXAM: Security Groups are attached to ENIs, not instances. Different rules needed for different groups? Set up multiple ENIs with SGs on each
EXAM: THE OPERATING SYSTEM NEVER SEES THE PUBLIC IPv4; it's configured on the ENI
EXAM: IPv4 Public IPs are DYNAMIC... Stop/Start instance means IP de-allocation/changes. Restarting instance maintains same IP. To avoid this, assign Elastic IP address
EXAM: Public DNS given to the instance for the public IPv4 IP address resolves to the PRIMARY PRIVATE IPv4 address from within the VPC. This happens so that if you've got instance-to-instance communication, it never leaves the VPC. Outside the VPC, DNS will resolve to the PUBLIC address


## DEMO - EC2 -  Manual Install of Wordpress on EC2 - NOTE-INCOMPLETE DEMO, IT BROKE 
Use EC2, install MariaDB, Apache & libraries and then download and install wordpress.
- Learning how NOT to do things through a manual installation

Steps:
1. 1-Click Deployment in lesson > Wait for stack to hit CREATE COMPLETE
2. Install WP: EC2 > Instances Running > right-click A4L, Connect, Instance Connect
3. Create Variables in Console > 
DBName='a4lwordpress'
DBUser='a4lwordpress'
DBPassword='4n1m4l$4L1f3'
DBRootPassword='4n1m4l$4L1f3'
> Paste each, press Enter, paste the next, Enter
4. Install system software - including Web and DB: `sudo yum install -y mariadb-server httpd wget` > install PHP/MariaDB `sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2`
5. Web and DB Servers Online - and set to startup: 
sudo systemctl enable httpd >
sudo systemctl enable mariadb >
sudo systemctl start httpd >
sudo systemctl start mariadb
6. Set Mariadb Root Password: `mysqladmin -u root password $DBRootPassword`
7. Install Wordpress: `sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html` > `cd /var/www/html` > `sudo tar -zxvf latest.tar.gz` (to extract tar file) > `sudo cp -rvf wordpress/* .` (copy data from WP file to current file '.') > `sudo rm -R wordpress` > `sudo rm latest.tar.gz`
8. Configure Wordpress: 
sudo cp ./wp-config-sample.php ./wp-config.php (rename template config file to be actual) > 
sudo sed -i "s/'database_name_here'/'$DBName'/g" wp-config.php (search and replace to update config file > 
sudo sed -i "s/'username_here'/'$DBUser'/g" wp-config.php >
sudo sed -i "s/'password_here'/'$DBPassword'/g" wp-config.php >
sudo chown apache:apache * -R (making sure web server has access to all file folders, owned by apache)
9. Create Wordpress DB: 
echo "CREATE DATABASE $DBName;" >> /tmp/db.setup (create WP DB) >
echo "CREATE USER '$DBUser'@'localhost' IDENTIFIED BY '$DBPassword';" >> /tmp/db.setup >
echo "GRANT ALL ON $DBName.* TO '$DBUser'@'localhost';" >> /tmp/db.setup >
echo "FLUSH PRIVILEGES;" >> /tmp/db.setup >
mysql -u root --password=$DBRootPassword < /tmp/db.setup
sudo rm /tmp/db.setup
*** UNSUCCESSFUL DEMO--Somewhere this messed up and the system couldn't see tmp/db.setup, then it could, so the commands got duplicated - 
10. Clean up Account: CFN > delete stack


## EC2 - Amazon Machine Image (AMI)
Amazon Machine Images (AMI) are the images which can create EC2 instances of a certain configuration. In addition to using AMI's to launch instances, you can customize an EC2 instance to your bespoke business requirements and then generate a template AMI which can be used to create any number of customized EC2 instances.
- AMIs are used to launch EC2 instances, even the Default EC2 instance launch is used via AMI. AMI's can be AWS or Community Provided
- Marketplace AMIs are available
- AMIs are REGIONAL... Unique ID for each AMI in each region Eg. "ami-0a887...."
- AMI controls permissions (scope: Public, Your Account, Specific Accounts)
- Not only can you create EC2 Instance from AMI, can create AMI from EC2 instance you want to template
- BILLING: billed for the storage cost... the data of the EBS snapshots contained

AMI Lifecycle: 
1. Launch Instance: AMI launches EC2 instance. 
2. Configure Instance: Can take launched instance and provide customizations (Eg. O/S, instance with config'd volumes, etc). 
3. Create New AMI: Can create an AMI from your configured/customized Instance (make a template)
4. Launch NEW Template instance: Launch new instance with templace AMI

EXAM: AMI = ONE REGION. Only works in that region
EXAM: AMI Baking: Creating an AMI from a configured instance + application
EXAM: AMI CAN NOT be edited. Instead, launch instance, change configs, make new AMI
EXAM: AMI CAN be COPIED between regions (includes its EBS Volume Snapshots)
EXAM: Default AMI permissions: Default is your account only. (Can be private, public, or grant access to specific accounts)


## DEMO - EC2 -  Creating A4L AMI (AMI Baking)
Create WP EC2 instance. Improve EC2 login screen. Create AMI from custom instance and deploy a new instance.

Steps: 
1. Set up WP Instance: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0007-aws-associate-ec2-ami-demo/lesson_commands.txt > Create Stack
***UNSUCCESSFUL DEMO: Failed to complete. Cantrill says it works but I couldn't get it 


## EC2 Purchase Options (Launch Types)
ON-DEMAND: Default/Shared. Per second billing. Resources like consume capacity bill regardless of instance state. Price defined up front, no discounts
-- Suitable for short term workloads, or unknown workloads

SPOT: Spot pricing is AWS selling unused EC2 Host Capacity for up to 90% discount. Spot price based on the space capacity at a given time
-- Customer sets max price they're willing to pay. If a Spot price exceeds your max willing payment, you'll lose the Spot
-- NEVER use a Spot for workloads which can't tolerate interruptions
-- Best for things that are non-time critical. Anything which can tolerate interruption and just be rerun. Anything that has a bursty capacity need. 

RESERVED: Form a part of most larger deployments in AWS. For long-term, consistent usage of EC2. Purchase a reservation to remove/reduce the per second price.
-- An unused reservation is still billed. Can be locked to AZ or region. Partial coverage of a larger instance, not billed for full thing.
-- Reservations terms: 1 year or 3 years. You pay for the entire term up front (no per/s fee, greatest discount of all reserved options). Or Partial Upfront, or No-Upfront (per/s fee)
-- For when you need lowest cost, consistent usage, and can't tolerate any interruption

DEDICATED INSTANCES: Instances run on an EC2 host that you don't own or share. Extra charges for instances, but dedicated hardware
-- Fees: 1 off hourly fee for any regions using dedicated instances. Fee for the instances themselves
-- For when you can't share infrastructure

DEDICATED HOST: EC2 host allocated to you in its entirety. You need to manage capacity, however, and unused capacity is wasted. 
-- 'Host Affinity' links instances to hosts
-- For Strict Licensing requirements. Reason to use this purchase option: For socket and core licensing requirements
-- You pay for the HOST, no instance charges. 

EXAM: On demand, reserved, spot


## EC2 - Reserved Instances - The Rest
Scheduled Reserved Instances, the differences between zonal and regional reservations and on-demand capacity Reservations. For if you need access to the cheapest EC2 that runs 24/7/365.

### Scheduled Reserved Instances: For long term useage which doesn't run constantly. Eg. Batch processing running daily for 5 hours. Eg 2 weekly data, like every friday for 24 hours
- DOES NOT support all instance types
- 1,200 hours min per year (100 hours per month)
- 1 year minimum

### Zonal: Only applies to one Availability Zone, providing billing discounts and capacity reservation in that one AZ
- 1 or 3 year term

### Regional: Provides a billing discount for valid instances launched in any AZ in that region
- While flexible, they don't reserve capacity within an AZ, which is risky during major faults when capacity can be limited
- 1 or 3 year term

### On-Demand Capacity Reservations: Can be booked to ensure you always have access to capacity in an AZ when you need it, but at FULL ON-DEMAND price.
- NO TERM LIMITS, but you pay whether or not you use it

### Savings Plan: Kind of like a reserved instance purchase, but instead of particular type of instance, it's a 1 to 3 year commit to AWS in terms of hourly spend. Eg. Minimum spend 20$/hr for 1 or 3 years, you get a reduction in price. If you go above your savings plan ($20), you begin paying 
- Can make a reservation of general compute amounts, 60% discount
- EC2 savings plan, which must be used for EC2 but 72% discount
- General Compute valid for things like EC2, fargate, lambda. These products have both on-demand rate and savings plan rate


## EC2 - Instance Status Checks & Auto Recovery
Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues. You can view the results of these status checks to identify specific and detectable problems.

You can create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair. 
- Terminated instances cannot be recovered. 
- A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata

### Short Demo - When you first start an instance, these are the "2/2 checks passed"
Each of these checks is a separate set of tests.  First, system status check. Second, instance status check.
- If there's a failure, you can set Auto Recover and other actions. Other actions like setting notification alarms (you can include actions in this alarm; recover, reboot, stop, terminate)
- Auto-Recovery ONLY works on EBS Volumes, not instance store


## DEMO - EC2 - Shutdown, Terminate & Termination Protection
Right-click instance > Instance Settings > Change Termination Protection > Enable
- role separation: can permit users to disable termination protection, and permit users to terminate
- Error if not permitted: "Failed to terminate instance: The instance [id] may not be terminated. Modify its 'disableApiTermination' instance and try again"


## EC2 - Horizontal & Vertical Scaling
Two ways which systems have to deal with increasing or decreasing user-side load. Each has pros and cons but handles the act of scaling radically differently.
- Adding or removing resources from a system

### Vertical Scaling
Resizing an EC2 instance when you scale, which can cause DOWNTIME. Can only scale during pre-agreed times, like outage windows, which can cause DISRUPTION
CONS: Larger instances carry a premium. There is an upper cap on performance; instance size
PROS: No app modification required. Works for ALL applications, even monoliths (since it all runs on one instance)

### Horizontal Scaling
Instead of increasing the size of the instance, HS adds more instances.
- Many copies of the instance running together and sharing the load; need LOAD BALANCER
- It's all about SESSIONS (state of your interaction with a session, like browsing YouTube). With HS, sessions don't work great since you move between instances during your interaction
CONS: Requires off-host sessions to save Session data. HS instances are 'dumb' instances
PROS: Balances / Evens out the load. No disruption while scaling, even when scaling down. No real limit to scaling horizontally. Often less expensive (since using many small instances). More granular; can increase in smaller increments.


## EC2 - Instance Metadata - EXAM
Instance metadata is data about your instance that you can use to configure or manage the running instance. Instance metadata is divided into categories, for example, host name, events, and security groups.
- EC2 svc provides data to instances. Accessible to all instances.


EXAM: IP Address to access Instance Metadata: 169.254.169.254
- URL http://169.254.169.254/latest/meta-data/
EXAM: Meta data service is NOT AUTHENTICATED and NOT ENCRYPTED; anyone who can connect to an instance and gain access to Linux Shell can access meta data

### DEMO - Instance Metadata
1. 1-Click Deploy. 2600:1f18:5421:7603:dc5e:6920:45eb:8f84
Commands for EC2 Connect session: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0009-aws-associate-ec2-instance-metadata/lesson_commands.txt
2. Download Instance Metadata functionality: 
- wget http://s3.amazonaws.com/ec2metadata/ec2-metadata (download)
- chmod u+x ec2-metadata (make usable)
- ec2-metadata --help (see list of commands)

EXAM: Never within lifecycle of instance is the public IPv4 address within the O/S. Remember, the internet gateway handles the public IPv4
- Can use meta data commands to make public IP visible



# CONTAINERS AND ECS

## Introduction to Containers
Another type of compute, container computing. Reminder, Virtualization is multiple O/S's operating on a single collection of hardware (guest O/S's). Containerization improves on Virtualization by aggregating and avoiding duplicating O/S's on different Virtual Machines in a system.
- With containerization, you have Host Hardware at the bottom, Host O/S on that, then a Container Engine (think Docker) atop the Host O/S. Now apps/whatever can run within isolated containers in the Container Engine. Each app no longer requires a full O/S, so they run lighter and allow more apps running on single piece of hardware
- Container is a running copy of a Docker Image, a Docker Container adds read/write capability to Docker Image. Similar to how an EC2 instance is a running copy of an EBS Volume. Docker Images are set up in layers which are read only, changes to layers are tracked using differential architecture (only tracks changes from 1 layer to another)
- Collections of Container Images are kep in a Container Registry Eg. Docker Hub
- Dockerfiles used to create Docker Images
- Great substitute for VMs if you don't need a full O/S for the container

## DEMO - Creating 'container of cats' Docker Image
Create a docker image containing the 'container of cats' application.
- Prereq: Create a DockerHub account
1. 1 Click Deploy.
2. Nav to new EC2 instance > Connect > Session Manager
3. Commands https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0030-aws-associate-ec2docker/lesson_commands.txt
- `sudo amazon-linux-extras install docker` - Install Docker
- `sudo service docker start` - Start Docker
- `docker ps` - Test Docker. Expect a permissions error
- `sudo usermod -a -G docker ec2-user` - Add permissions
- `exit` and reopen a Session Manager
- `sudo su - ec2-user` - Log in as EC2 user
- `docker ps` now works
- `cd container`, `ls -la`
- `docker build -t containerofcats .` - Build container image
- `docker images --filter reference=containerofcats` - Show images in this container
- `docker run -t -i -p 80:80 containerofcats` - Map port 80 on container to port 80 on ec2 instance with cats image
- Log in to docker hub
docker login --username=YOUR_USER
docker images
docker tag IMAGEID YOUR_USER/containerofcats
docker push YOUR_USER/containerofcats:latest


## ECS - Elastic Container Service - Concepts
ECS is to containers as EC2 is to virtual machines. A managed container-based compute service
- Runs in two modes 1. EC2 2. Fargate
- ECS let's you create a cluster. A Cluster is where you container runs from. 
- Elastic Container Registry is the ECS Container Registry
- Container Definition: Defines Images and Ports
- Task Definition: A self contained application; the app as a whole. Stores a Task Role, an IAM Role. 
- Task Role: IAM Role which the TASK assumes

EXAM: Task Roles are the best practice way giving containers within ECS permission to interact with AWS Resources
- ECS Service. Config'd with Service Definition: Tells how a task will scale and determines high availability. Can use load balancer. Restarts.
EXAM: Cluster Modes available within ECS: Network Only (Fargate), EC2 Linux + Networking, EC2 Windows + Networking
EXAM: Benefits of containers: Fast to start up, Portable, Lightweight

## ECS - Cluster Mode
ECS is capable of running in EC2 mode or Fargate mode. EC2 mode deploys EC2 instances into your AWS account which can be used to deploy tasks and services. 
- With EC2 mode you pay for the EC2 instances regardless of container usage. 
- Fargate mode uses shared AWS infrastructure, and ENI's which are injected into your VPC. 
- You pay only for container resources used while they are running.


The Two Modes when running ECS: EC2 Mode, Fargate Mode
- Main differentiator: What you manage VS what AWS manages

### EC2 Mode
- Creates EC2 instances as Container Hosts; You'll be paying for these Hosts/Instances
- EC2 Mode for when you want to use containers in your infrastructure but you NEED to manage container host capacity and availability

### Fargate Mode
- No management of EC2 instances as Container Hosts; no servers to manage.
- Not paying for EC2 instances.
- The main difference is how containers are Hosted: Fargate Shared Infrastructure instead of EC2 instances.
-- Tasks / Services run from the Shared Insfrastructure and are injected in
- Only pay for the container Resources that you consume

EXAM: When to use EC2 vs ECS (EC2) vs Fargate
- EC2 VS ECS. Containers? ECS. Containers great for isolating applications
- EC2? Large consistent workload, price conscious, make use of existing reservations
- Overhead conscious? Fargate. Less mgmt overhead. 
- Small / Burst / Batch / Periodic workloads? Fargate (since you only pay for consumed resources)

## DEMO ECS - Deploying 'container of cats' using Fargate
Create a Fargate Cluster, create a task and container definition and deploy the world renowned 'container of cats' Application from Dockerhub into Fargate.

1. Create Cluster: ECS Console > Clusters > Create Cluster > Networking Only option > name "allthecats", (don't tick New VPC box, use Default VPC instead by not clicking) > Create. If you get ECS error, redo these steps
2. Create Task Definition (deploy container): Task Definitions > New > Compatibility: Fargate > Next Step > def name "containerofcats", no task role needed, operating system family: linux, task size: 1bg memory, 0.5vCPU > click "Add Container": name "containerofcatsweb", image "docker.io/acantril/containerofcats", Memory Limit Soft 1024, Port Mappings: 80 tcp > Add
3. Run it: Clusters > allthecats > Tasks tab > Launch type: fargate, OS family: linux, select VPC: Cluster VPC: default selection, subnet: select 2 at random > Create/Add
4. Cleanup > Stop Task Definition > Task: Actions: Deregister > Cluster: allthecats: Delete


## ECR - Elastic Container Registry
Like Docker Hub but the AWS version. A managed Container Image Registry service
- Each AWS account has a public and private registry and can have many repositories
-- Public = Public Read only, R/W requires permissions
-- Private = Permissions required for any R/O or R/W
- In each repo you can have many container images
- Images can have several tags

### Benefits of ECR
- Integreated with IAM for Permissions
- Offers security scannings, Basic and Enhanced Scanning (enh. uses Inspector product)
- Near real-time metrics delivered into CloudWatch
- Logs API actions into CloudTrail
- Generates events deliverd to EventBridge
- Offers Replication (cross region and cross account)

## Kubernetes - K8
Open source container orchestration system. Cloud agnostic product - can use on many platforms
- Cluster: Highly available cluster of compute resources
-- Vocab: Cluster Control Plane, Cluster Nodes, containerd, kubelet, Kubernetes API
-- The control plane orchestrates containerized applications which run on nodes
- Pods: Smallest unit of computing in K8's, often seeing one-container-one-pod. Pods are NON-PERMANENT; view them as temporary things that are created for job and gone when job is done
- Cluster: A deployment of K8's
- Node: Resources within cluster; pods are placed on nodes to run
- Pods: Smallest unit in K8s, often 1 container to 1 pod
- Service; Abstraction running on 1 or more pods; what you'll understand as an application
- Job: ad-hoc, creates one or more pods until completion
- Ingress: How something external to the cluster can access the service
- Ingress Controller: Used to provide ingress (Eg. AWS Load Balance Controller)
Default storage in K8s is ephemeral by default, provided locally by a node. Like ISVs on EC2
- Persistent Storage (PV) : Volume whose lifecycle lives beyond any 1 pod using it

## Elastic Kubernetes Service (EKS)
Amazon Elastic Kubernetes Service (Amazon EKS) is a fully-managed, Kubernetes implementation that simplifies the process of building, securing, operating, and maintaining Kubernetes clusters on AWS.
- open-source and cloud agnostic
- K8s Control Plane scales and runs on multiple AZs
- Integrates with AWS svc's: ECR, Elastic Load Balancer, IAM, VPC
- EKS Cluster = EKS Control Plane & EKS Nodes
- etcd: the key-value store that k8's uses, is distributed across multiple AZs
- Nodes: can be Self-Managed (ec2 instance), Managed Node Groups (ec2 instance), or Fargate pods
- For Persistent Storage, EKS can use EBS, EFS, FSx Lustre, FSx for NetApp ONTAP

### EKS Resources
- https://docs.aws.amazon.com/eks/latest/userguide/eks-compute.html
- https://docs.aws.amazon.com/eks/latest/userguide/fargate.html


# ADVANCED EC2
## Bootstrapping EC2 using User Data
EC2 Bootstrapping is the process of configuring an EC2 instance to perform automated install & configuration steps 'post launch' before an instance is brought into service. With EC2 this is accomplished by passing a script via the User Data part of the Meta-data service - which is then executed by the EC2 Instance OS
- tl;dr this allows you to bring and EC2 instance up in a pre-configured state
- EC2 Bootstrapping = EC2 Build Automation
- This process uses User Data via meta-data IP (http://169.254.169.254/latest/user-data) - Note, this is instead of /meta-data
-- EC2 doesn't interpret this data, the OS needs to understand the User Data
- This boostrapping ONLY happens on Launch. If you update User Data after the fact, it won't be applied
- User Data is OPAQUE to EC2, its just a block of data to EC2
- User Data is NOT secure; don't use it for PWs or long term creds
- User Data limited to 16KB in size
- If you want to update User Data... stop instance, update data, and restart 

EXAM: Boot-time-to-Service-Time: how quickly you can bring an instance into service and have it ready for use by customers
- measured in minutes

## DEMO - Bootstrapping WP Installation (parts 1 and 2)
Bootstrap two EC2 instances with WordPress and the 'cowsay' login banner customizations.
- The first, directly using User Data via the console UI
- the second, using CloudFormation

Steps:
1. 1-click deploy > Create stack
2. EC2 > Launch Instance (x2) > Name "A4L-MANUALWORDPRESS" > keypair: proceed without > Network Settings, Edit
3. Instance Network Settings: VPC, select a4l-vpc1 > subnet, select sn-web-A > Select Existing Security Group, BOOTSTRAP-[etc] > Advanced Details, User Data, paste in .txt file provided > Launch Instance
4. EC2 Instance Connect > Will see custom Banner above normal stuff if you wait long enough. Paste in the commands in the command file to see user data
Note: Within EC2 Connect, "cd /var/log" you can use the cloud-init-output.log and cloud-init.log to diagnose any bootstrapping issues
5. CloudFormation > 1-click deploy > etc etc
6. Clean up > Terminate EC2 instance > Delete CFN stack


## EC2 Instance Roles & Profile
EC2 Instance Roles/Profiles are how applications running on an EC2 instance can be given permissions to access AWS resources on your behalf. Short-term temporary creds are available via the EC2 instance Metadata and are renewed automatically by the EC2 and STS Services

Instance Role Architecture uses an IAM role that allows EC2 instance to assume it. There is an InstanceProfile wrapper that actually attached to the instance. Creds delivered within metadata
- creds used to give InstanceProfile IAM role access are inside meta data
-- iam/security-credentials/role-name
-- creds always valid/auto-rotated
- BEST PRACTICE: Always use Roles when possible, better security. CLI tools will use role creds automatically

## DEMO - Using EC2 Instance Roles
Create an EC2 Instance Role, apply it to an EC2 instance and learn how to interact with the credentials this generates within the EC2 instance metadata.

Steps:
1. 1-click deploy
2. EC2 > instance connect > EC2 Instance Connect > test command `aws s3 ls` > need creds
3. Create IAM Role > IAM > Roles > Create Role > Trust Entity, AWS service: select `EC2` > Next, Add Permissions, search `s3`, select AmazonS3ReadOnlyAccess > Next, Role name "A4LInstanceRole" > Create Role
4. Attach Role to Instance: EC2 > Right-click instance, Security: Modify IAM Role > Choose Role A4LInstanceRole
5. You can now `aws s3 ls` command in EC2 Connect because you have applied the IAM Role that has the S3ReadOnly permission to the EC2 instance
6. Clean up > IAM: Delete A4LInstanceRole > EC2: Security: Modify IAM, select NO IAM Role > CFN: Delete Demo stack

## EC2 - SSM Parameter Store 
The SSM Parameter store is a service which is part of Systems Manager which allows the storage and retrieval of parameters - string, stringlist or secure string.
- The service supports encryption which integrates with KMS, versioning and can be secured using IAM.
- The service integrates natively with many AWS services - and can be accessed using the CLI/APIs from anywhere with access to the AWS Public Space Endpoints.

As previously mentioned, passing secret data through to EC2 instance with User Data is bad practice. 
- SSM is storage for configuration and secrets 
- Parameter store can store the following: String, StringList, SecureString
-- There are hierarchies and Versioning of parameters
-- Can be stored as plaintext and ciphertext (integrating with KMS)
- Public Parameters are available, like the latest AMIs per region

## DEMO - Parameter Store
Create some Parameters in the Parameter Store and interact with them via the command line - using individual parameter operations and accessing via paths.

Steps:
1. Nav to Systems Manager in AWS Console > Parameter Store > Create parameter
2. Parameter 1 details: Name "/my-cat-app/dbstring" > value "db.allthecats.com:3306" > description "Connection string for cat app" > create
- the fwd slashes create hierarchy in Parameter Store 
3. Parameter 2: Name "/my-cat-app/dbuser" > value: "bosscat" > create 
4. Param 3 (secure): Name "/my-cat-app/dbpassword" > Type: SecureString > value: amazingsecretpassword1337 (encrypted)
5. Param 4: Name "/my-dog-app/dbstring" > value: "db.ifwereallymusthavedogs.com:3306"
6. Param 5: Name "/rate-my-lizard/dbstring" > value "db.thisisprettyrandom.com:3306"
7. CloudShell (top menu) > try these commands:
aws ssm get-parameters --names /rate-my-lizard/dbstring 
aws ssm get-parameters --names /my-dog-app/dbstring 
aws ssm get-parameters --names /my-cat-app/dbstring 
aws ssm get-parameters-by-path --path /my-cat-app/ 
aws ssm get-parameters-by-path --path /my-cat-app/ --with-decryption
8. Clean up: Select all params > Delete

## System and Application Logging on EC2
CloudWatch is for metrics*
CloudWatch Logs is for logging and interpreting that logged data*
* Neither of these natively capture data inside an instance
- CloudWatch Agent is required for CW/CW Logs to natively capture data in an instance (plus config and permissions)
-- Configured / Permitted CW Agent pulls logs from Instance and sends to CW / CW Logs
-- The permissions the Agent needs will use an IAM Role

## DEMO - Logging and Metrics with CloudWatch Agent
Download and install the CloudWatch Agent and configure it to capture 3 log files from an EC2 instance: /var/log/secure, /var/log/httpd/access_log, /var/log/httpd/error_log

Steps:
1. 1-click deploy
2. Connect to instance: EC2 instance connect
3. Install CW Agent to Instance connect with `wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm`
4. Use IAM to create Role/Permissions for Agent: IAM > Roles > Create Role > select options: AWS service/EC2 > select (2) policies `CloudWatchAgentServerPolicy` And `AmazonSSMFullAccess` > next > name "CloudWatchRole" > Create Role
5. Connect Role to Instance: EC2 Instances > right-click instance, Security, Modify IAM role > Select CloudWatchRole > Update IAM Role
6. EC2 Connect to Start CW Agent config wizard: Default OS, Enter > Default region (EC2), enter > user: root, enter > enter statsd, enter statsd port > interval, enter > enter for everything until "Which default metrics config do you want? input `3` for Advanced... [FOLLOW VIDEO for rest of this crap, it's mostly pressing Enter for defaults] - https://learn.cantrill.io/courses/1820301/lectures/41301605
7. Store Config in Parameter Store: Press enter more for Defaults. Note: Most all of it is defaults, pay attn to the few that aren't
8. CloudWatch Console > Log Groups. Look for the three file paths you created 
9. Cleanup > EC2, security: remove CW Role > IAM, Roles, Delete role > CFN, delete Stack

## EC2 Placement Groups
Allows you to choose placement of EC2 instances, so you can ensure that they're physically close together or not.

3 placement groups available within AWS:
1. Cluster (PERFORMANCE)
2. Spread (Resilience)
3. Partition (Topology Awareness)

- Cluster. For highest EC2 performance. Launch these all at the same time for similar placement/capacity, will be launched into single AZ. Instances in Cluster group have fast direct connections to each other. Cluster achieves 1-Gbps per single stream instead of the standard 5Gbps/stream. Lowest latency and max Packets-per-second possible in AWS (when paired with Enhanced Networking)
EXAM: CLUSTER Placement Groups are ONE AZ ONLY, which is locked when launching the first instance. Close prox is what gives them best Performance of placement groups 
EXAM: VPC peers in cluster placement groups can span AZs, but this impacts performance
EXAM: Cluster PGs not supported on all instance types
EXAM: Launch all instances within cluster group at same time as best practice
EXAM: 10Gbps single stream performance; highest performance, lowest latency, best throughput

- Spread. For max availability and resilience for an application; span AZs to accomplish this. Use case: small number of critical instances that need to be kept separate from each other
EXAM: Spread PG instance LIMIT: 7 INSTANCES per AZ (HARD limit)
EXAM: Spread PGs provide "infrastructure isolation" to provide max availability and resilience
EXAM: Each instance runs from a different rack, each rack has its own network and power source
EXAM: Not supported for Dedicated Instances or Hosts

- Partition. Designed for when you have more than 7 instances per AZ but you still need to be able to separate those instances into separate fault domains. Designed for huge-scale parallel processing systems
EXAM: For when you need max availability/resilience but MORE THAN 7 instances per AZ
EXAM: Max 7 PARTITIONS per AZ, but each partition can contain more than 7 instances
EXAM: Each partition has its own rack
EXAM: Instances can be placed into a specific partition or can be auto-placed
EXAM: for 'TOPOLOGY' aware applications; Eg: HDFS, HBase, Cassandra

## EC2 - Dedicated Hosts
It's an EC2 Host dedicated only to you. Dedicated hosts are EC2 Hosts which support a certain type of instance which are dedicated to your account. Eg: a1, c5, m5
- Billing: No EC2 instance charges, you pay for the host
- You can pay an on-demand or reserved price for the hosts and then you have no EC2 instance pricing to pay for instances running on these dedicated hosts.
- Generally dedicated hosts are used for applications which use physical core/socket licensing

### How they work: Host is designed for a specific family and size of instance. Eg. a1 dedicated host has 1 socket and 16 cores

### Dedicated Host Limitations (things that aren't supported)
- AMI limits - Not supported: RHEL, SUSE Linux, Windows AMIs
- Cannot used Amazon RDS instances
- Placement Groups not supported

Note: Using RAM (resource access manageR) product, hosts CAN BE shared with other ORG accounts

## EC2 - Enhanced Networking & EBS Optimized
Enhanced networking is the AWS implementation of SR-IOV, a standard allowing a physical host network card to present many logical devices which can be directly utilized by instances.
- This means lower host CPU usage, better throughput, lower and consistent latency
- EBS optimisation on instances means dedicated bandwidth for storage networking - separate from data networking.
- Resource: https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/enhanced-networking.html

### Enhanced Networking
A feature designed to improve overall performance of EC2 networking--required for high performance things like Cluster Placement Groups.
- Uses technique called SR-IOV so that the network interface inside EC2 is aware of virtualization. This all increases IO, lower host CPU usage, more bandwidth, and higher packets-per-second (PPS), consistent lower latency

### EBS Optimized Instances
What we know about EBS already: EBS is block storage over the network. EBS Optimized means DEDICATED capacity for EBS


# Route 53 - Global DNS

## R53 Public Hosted Zones
### R53 Hosted Zones (HZs):
- An R53 Hosted Zone is a DNS DB for a domain
- GLOBALLY RESILIENT
- HZs are created automatically when you register a domain using R53. But HZs can be created separately
- HZs are what the DNS system references; authoritative source to confirm a domain Eg. animals4life.org
- Two types of hosted zones in R53: public and private

### Public Hosted Zones
A PUBLIC hosted zone is a container that holds information about how you want to route traffic on the internet for a specific domain which is accessible from the public internet
- Creating a Public HZ creates 4 R53 Nameservers that are all accessible from public internet and VPCs
- Monthly cost for hosting public HZ and small cost for queries against it

## R53: Private Hosted Zones
A private hosted zone is a container that holds information about how you want Route 53 to respond to DNS queries for a domain and its subdomains within one or more VPCs that you create with the Amazon VPC service
- Private Hosted Zones are ALWAYS associated with a VPC and are only accessible within those VPCs
- Enabled split-view (overlap public / private) for PUBLIC and INTERNAL use with the same zone name (eg. only intranet for internals but see same thing via public route if external)
- To gain access to a private hosted zone, you need to be querying from within a VPC, AND that VPC needs to be explicity associated with the private host

## R53: CNAME vs R53 Alias
The issue with only using CNAMEs: `A` record maps a NAME to IP Address ie. catagram.io => 1.3.3.7. CNAME on the other hands, maps NAME to NAME (ie. www.catagram.io => catagram.io)
- Problem: can't use a CNAME for the apex of a domain, also known as the naked domain. AWS services like ELB only use DNS names, so just a CNAME like catagram.io would be invalid within ELB
- Solution: R53 Alias records let you iuse CNAME for domain apex

### R53 Alias
- ALIAS records map a NAME to an AWS Resource
- ALIAS records can be used for naked/apex and normal records. Alias functions like CNAME for non-apex/non-naked domains
- No charge for ALIAS requests pointing at AWS resources
EXAM: For AWS Services, ALIAS should be your default choice

## R53: Simple Routing
Simple routing lets you configure standard DNS records, with no special Route 53 routing such as weighted or latency. With simple routing, you typically route traffic to a single resource, for example, to a web server for your website.
- Simple Routing supports 1 record per name (www)
- Each record can have multiple values
- Simple Routing does not support health checks
EXAM: Use Simple Royuting when you want to route requests towards ONE SERVICE such as a web server

## R53 Health Checks
Amazon Route 53 health checks monitor the health and performance of your web applications, web servers, and other resources. 
- Each health check that you create can monitor one of the following:
-- The health of a specified resource, such as a web server
-- The status of other health checks
-- The status of an Amazon CloudWatch alarm

- Health checkers are located GLOBALLY
- Health Checks occur every 30s (or every 10s if you pay more)
- States: Healthy or Unhealthy
- Globally, you have distributed health checkers. If 18%+ of health checkers report status as healthy, the health check returns healthy
- In most cases, an UNHEALTHY record is NOT returned in queries

## R53 - Failover Routing
Failover routing lets you route traffic to a resource when the resource is healthy or to a different resource when the first resource is unhealthy
- Use when you want to configure "active passive failover"

# DEMO - Using R53 and Failover Routing - NOTE: This demo requires an R53 registered domain 
Create Failover routing and private hosted zones. https://learn.cantrill.io/courses/1820301/lectures/41301585

## R53 - Multi Value Routing
Multivalue value routing lets you configure Amazon Route 53 to return multiple values, such as IP addresses for your web servers, in response to DNS queries. You can specify multiple values for almost any record, but multivalue answer routing also lets you check the health of each resource, so Route 53 returns only values for healthy resources
- Improves availability, but NOT a replacement for load balancing
- Up to 8 healthy records are returned. If you have more than 8 records, 8 at random are returned

## R53 - Weighted Routing
Weighted routing lets you associate multiple resources with a single domain name (catagram.io) and choose how much traffic is routed to each resource. This can be useful for a variety of purposes, including load balancing and testing new versions of software.
- Can assign weights to each hosted zone. Eg. 3 Hosted Zones, 40, 40, 20, totalling 100. First 2 each get 40% of traffic, last only gets 20% of traffic. This doesn't need to add to 100
- A 0 weight means record is never returned unless all are 0, then all are considered

## R53 - Latency Routing
Should be used when trying to optimize for performance and user experience
- Latency-based routing supports one record with the same name in each region
- In the background, AWS mantains a latency table between users and regions and matched user to lowest latency
- Latency DB is NOT real time

## R53 - Geolocation Routing
Geolocation routing lets you choose the resources that serve your traffic based on the geographic location of your users, meaning the location that DNS queries originate from. 
- Geolocation records are tagged with a location
- Does not return the closest record, but that which are applicatble or the default or no answer. "Default" is backup answer
- Good for regional restrictions, language specific content, or laod balancing across regional endpoints
- To route traffic based on customer location. Not proximity, but based on tag and specificity
EXAM: Geolocation routing NOT about closest recoird, but returns RELEVANT locations only 

## R53 - Geoproximity Routing
Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources. 
- You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a bias.
-- A BIAS expands or shrinks the size of the geographic region from which traffic is routed to a resource. Can define a plus or minus bias + / -

## R53 Interoperability
How Route53 provides Registrar and DNS Hosting features and steps through architectures where it is used for BOTH, or only one of those functions - and how it integrates with other registrars or DNS hosting.

R53 does two things: 1) Domain Registrar 2) Domain Hosting. It can do both or either, user choice

### R53 - When you REGISTER domain [Domain Hosting / Domain Registrar]
1. Accepts your money (domain registration fee) [DR]
2. Allocates 4 name servers (NS) [DH]
3. Creates a Zone File (domain hosting) on the above NS's [DH]
4. R53 communicates with registry of TLD (domain registrar) [DR]

## R53 - DNSSEC
DNSSEC strengthens authentication in DNS using digital signatures based on public key cryptography. With DNSSEC, it's not DNS queries and responses themselves that are cryptographically signed, but rather DNS data itself is signed by the owner of the data.


# Relational Database Service (RDS)
## Database Refresher & Models
DBs are systems which store and manage data: 
DB Types: 
1) Relational Database Management System (RDBS, commonly SQL) 
- RDBS has a structure in & between tables of data; rigid schema
- Fixed relationship between tables. These relationships are defined in advance
2) Non-relational (NoSQL); more relaxed schemas
- Common Examples of Non-relational DBs:
-- Key-value DB's: just key/value pairs and no schema otherwise. Highly scalable and fast. Good for in-memory caching
-- Wide Column Store: Every item in table has same key layout (Partition Key, + other key). Items in a table can have differing attributes. Eg. DynamoDB
-- Document Database. Good for DBs of orders or contact list. Key/Value but the value is the accessible document+data
-- Column Store (AKA OLTP, good for transactional processes like collections of orders) and Row Store (RedShift; good for analytics)
-- Graph. Data and the relationships of data stored in DB

## RDS - ACID vs BASE
This lesson steps through the ACID and BASE Database transaction models and introduces the CAP Theorem
- transaction models AKA define a few things about transactions to and from a DB
- CAP Theorem - Consistency, Availability, Partition Tolerant (resilience). CAP Theorem says that any DB product only capable of delivering a max of TWO of these factors
-- ACID focuses on consistency, BASE focuses on Availability

### ACID - atomic, consistent, isolated, durable
EXAM: 'ACID' mentioned in exam? RDS based DB. Acid limits DB scalability
- Atomic: either all or NO components of a transaction succeed or fail
- Consistent: transactions move DB from one VALID state to another; nothing in-between is allowed
- Isolated: if multiple transactions occur at once, they don't interfere with each other
- Durable: once committed, transactions are durable; stored on non-volatile memory and are resilient to outages/crashes

### BASE - Basically available, soft state, eventually consistent
- Basically Available: Read / Write ops are available 'as much as possible' but without any consistency guarantees
- Soft State: The DB doesn't enforce consistency, this is offloaded onto the application/user
- Eventually Consistent: If we wait long enough, reads from the system will be consistent
BASE = highly scalable, Eg DynamoDB
EXAM: BASE = noSQL

## RDS - Databases on EC2
NOTE: Running DB on EC2 is generally bad practice as there is usually a better alternative
Why you might run DB on EC2...
- If you need access to the DB instance OS
- Advanced DB Option tuning (DBROOT)
- Vendor/decision maker demands
- Need to run DB or DB Version AWS doesn't provide
- Need a specific OS/DB combo or architecture AWS doesn't provide

Why you SHOULD NOT run DB on EC2
- Admin overhead is high to manage on EC2 and DBHost
- Backups / disaster recovery management becomes more difficult
- EC2 is a single AZ. If zone fails, DB access fails
- Features. AWS DB products are great and you could be missing out
- EC2 is ON or OFF. No serverless easy scaling
- Replication.
- Performance. AWS invests time into optimisation / features that you're missing

## Demo - RDS - Splitting Wordpress Monolith => APP & DB
- Moving DB to new AZ, separate from Webserver/App 

Steps: 
1. 1 click deploy > Create complete
2. Copy WP instance IP, paste to browser > Title "The Best Cats!!", user "admin", PW "an1m4ls4l1f3", email test@test.com > Install
3. A4L-WordPress, ec2 connect `mysqldump -u root -p a4lwordpress > a4lwordpress.sql` > PW an1m4ls4l1f3
4. Inject a4lwordpress.sql into new DB `mysql -h privateipof_a4l-mariadb -u a4lwordpress -p a4lwordpress < a4lwordpress.sql`
5.... Error at step 4. 
6. Clean up > CFN > Delete Stack

## RDS - Architecture
- Known as "DBaaS", but more accurately RDS is a DBSaaS "DB Server as a Service"
- RDS provides multiple databases on one DB Server (instance)
- RDS is a managed service, so no access to OS or SSH Access
- RDS operates within a VPC
- RDS Instance can have more than 1 DB in it, and each RDS Instance has its own Dedicated EBS-provided storage 
NOTE: Amazon Aurora is DIFFERENT from RDS
Cost: Billed for resource allocation
-- Cost #1: instance size/type
-- Cost #2: Multi-AZ or not
-- Cost #3: Storage type/amount
-- Cost #4: Data transferred
-- Cost #5: Backups & Snapshots
-- Cost #6: Licensing

## RDS - DEMO - Migrating EC2 DB into RDS
Create a MySQL RDS instance and migrate the Wordpress Database from the self-managed MariaDB server running on EC2 into this RDS instance.

Steps:
1. 1 click deploy
2. Set up website: EC2 > A4L-Wordpress instance, copy IPv4 address, paste into browser > title "The Best Cats!!", username "admin", PW "4n1m4ls4L1f3", email "test@example.com" > install WP
3. Set Up data to move: Blog Post > Posts > delete Hello World > Add New > H1 "The Best Cats Ever!!" > add Gallery widget and upload zipped file, Publish
4. Set up RDS DB: RDS > Subnet Groups > Create a DB Subnet Group "a4lsngroup" for title/descrip > VPL a4l > Add subnets, select us-east-1a/b/c > Pick your subnets > go to VPC, Subnets and look for full names of sn-db-A/B/C to select those ones > Create
5. Provision DB: RDS > DB > Create DB > Standard Create > select MySQL > engine version (currently 8.0.32 in demo video) > Template, Free Tier > DB instance identifier "a4lwordpress" > admin "a4lwordpress" > PW "4n1m4ls4L1f3" > Storage, uncheck "Enable storage autoscaling" > Connectivity, select a4l-vpc1 > VPC security group (firewall), Create New > name "a4lvpc-rds-sg" > Add'l Configuration, Initial DB Name "a4lwordpress" > Create DB
6. Config Security Group so RDS DB is connected: RDS > DB's > a4lwordpress > Connecitivity & Security tab, click the VPC SG link and open in new tab > find your SG > Inboud Rules > Edit > Add Rule, Type MYSQL/Aurora, Source (magnifying glass icon) "MIGRATE2RDS-Instance..." > Save Rule
7. Migrate Data to new RDS DB, create backup file to move: EC2 Connect with A4L-Wordpress > 
`mysqldump -h PRIVATEIPOFMARIADBINSTANCE -u a4lwordpress -p a4lwordpress > a4lwordpress.sql` -> replace private IP with Private IPv4 of a4l DB instance > Enter > use PW above > Enter
8. Move backup SQL DB instance into RDS: `mysql -h CNAMEOFRDSINSTANCE -u a4lwordpress -p a4lwordpress < a4lwordpress.sql` -> Replace CNAME with Endpoint name in RDS db instance > Enter
9. Point WP at RDS instance: 
`cd /var/www/html` >
`sudo nano wp-config.php` -> Go to Database Hostname and replace the IPv4 pointing at the WB DB EC2 instance with the Endpoint name of the RDS instance...
Looks like...
/** Database hostname */
define( 'DB_HOST', 'a4lwordpress.cloy7bpdvh9v.us-east-1.rds.amazonaws.com' ); > ctrl+o to Save, ctrl+x to Exit nano
10... Demo broke at this stage
11. Cleanup: RDS > Delete DB > VPC > Delete Security group "a4lvpc-rds-sg" > Cloufformation > Delete Stack

## Relational Database Service (RDS) MultiAZ - Instance and Cluster Deployments
MultiAZ is a feature of RDS which provisions a HIGHLY AVAILABLE instance set.
- The product provides MultiAZ instance where a standby replica is kept in sync Synchronously with the primary instance.
-- The standby replica cannot be used for any performance scaling, only availability.
- MultiAZ cluster mode: where a write and two reader instances are kept in sync Synchronously. The reader instances can be used for read operations allowing for limited read scaling.
- Backups, software updates and restarts can take advantage of MultiAZ to reduce user disruption.

## MultiAZ Instance Deployments
- Synchronous replication of the primary DB to the standby DB
- Standby is only for backups and is never accessed unless a failover is required. Failover can take 60-120s
- Not free
- Only ONE standby replica due to architecture
- Same region only, but different AZs in region
- Backups taken from Standby to improve Primary performance

## MultiAZ Cluster Deployments
NOTE: Keep in mind the differences between MultiAZ Cluster Deployments and Amazon Aurora
- ONE Writer replicates to TWO reader instances, all in different AZs. With Aurora, you can have more than 2 reader instances
- These Readers (called Standby in Instance Deployment) can be used for Read operations, allowing for some read scaling
- Faster Hardware than Instance Deployment
- Faster failover, ~35s
- Writes considered "committed" when 1 of the readers has confirmed it

## RDS Automatic Backup, RDS Snapshots and Restore
- RDS is capable of performing Manual Snapshots and Automatic backups
-- Manual snapshots are performed manually and live past the termination of an RDS instance
-- Automatic backups can be taken of an RDS instance with a 0 (Disabled) to 35 Day retention.
- Automatic backups also use S3 for storing transaction logs every 5 minutes - allowing for point in time recovery.
- Snapshots can be restored .. but create a new RDS instance.
EXAM: RDS Backups live in S3 but are AWS Managed, so you never seem them

### RDS Backup - Snapshots (Manual)
- First snapshot is full copy, after that it's incremental copies
- Snapshots DON'T expire, they live beyond the termination of an RDS instance -- you have to delete them manually
- Technically, you could reach a 5 minute Recovery Point Objective

### RDS Backup - Automated Backups
- Occur once per day
- Think of them as automated snapshots
- If using single AZ, plan for a small IO pause and do it during downtime
- Every 5 mins, Transaction Logs are recorded to S3. With these plus snapshots; you have a 5 Minute Recovery Point Objective 
- Retention Period. 0 - 35 days before AWS deletes the automated backups. If you select 35 days, you can restore to any point in time over that 35 day period
- To avoid losing data beyond 35 days, you need to do a final manual snapshot

### RDS Backups - Cross-Region Replication
- RDS can replicate backups to another region (both snapshots and transaction logs)
- Charges apply for the cross-region data copy and for the storage in the destination region
- This feature must be enabled

### RDS Backsup - Restores
- Creates a new RDS instance when you restore an automated backup or manual snapshot
- Snapshot restore is a single point in time, at the time of creation of the snapshot
- Automated backups are restorable to any 5 minute point in time

## RDS Read Replicas
RDS Read Replicas can be added to an RDS Instance - 5 direct per primary instance.
- READ-ONLY
- They can be in the same region, or cross-region replicas.
- They provide read performance scaling for the instance, but also offer low RTO recovery for any instance failure issues
- They don't help with data corruption as the corruption will be replicated to the RR
- Asynchronous replication
EXAM: Synchronous is MultiAZ, asynchronous is Read Replicas

### Read Replicas - Why do they matter?
- Read performance and read scaling. 
-- You get 5 direct read-replicas per DB instance, each providing add'l instance of read performance
-- Read-replicas can have read-replicas, but then lag starts to be a problem
-- Global performance improvements
- Recovery Point and Recovery Time Objective benefits
-- Snapshots/Backups improve RPO, with RR's offering a near 0 RPO (little potential for data loss)
-- RR's have low RTO. NOTE: For Failure only, not corruption. The corruption is also likely replicated
- Read-replicas are Read-only until promoted (until activated), then they become a normal RDS instance
- Since you can cross-region replicate, you get Global Resilience

## Demo - RDS - MultiAZ & Snapshot Restore with RDS
Working with RDS Multi AZ mode and snapshot restores

Steps:
1. 1 click deploy
2. Set up WP (The Best Cats!!, admin, 4n1m4ls4L1f3, test@test.com), create blog post
3. Create snapshot: RDS > select DB > Actions, Take snapshot > name "a4lwordpress-with-cat-post-mysql-8032" > Take snapshot
4. Enable MultiAZ: RDS > select database > Modify > Enable MultiAZ (this part costs money so I'm not doing it) 

Demo 2 - Restore RDS in the case of data corruption
Steps:
1. Change WP blog post text to simulate 'corrupted' data
2. RDS > Snapshots > select snap, Actions, Restore Snapshot > name "a4lwordpress-restore" > select burstable somethings > select RDSsecurity for SG > Create/Restore
NOTE: Restoring RDS from snapshot creates a NEW instance
3. Point to new DB: EC2 connect > cd /var/www/html >
`sudo nano wp-config.php` >
Get new restored RDS endpoint and prepare to paste it into DB hostname in nano > paste into correct spot > ctrl+o to save/write > ctrl+x to exit
4. Cleanup > Delete restore snapshot > CFN delete stack

## RDS - Security
- In transit encryption (SSL/TLS) available for RDS and can be set to Mandatory on a per user basis
- At Rest encrpytion available via KMS and EBS encryption
- Transparent Data Encryption: Encryption handled within the database engine
-- RDS Oracle supports TDE using CloudHSM (even more secure as the key management is customer now AWS)

### RDS - Security - IAM Authentication
You can configure RDS to use IAM user authentication against a DB
- AUTHORIZATION is still handled internally by DB engine
- Storage, logs, snapshots, and replicas all encrypted
- Encryption can't be removed

## Amazon RDS Custom
Amazon RDS Custom is a managed database service for applications that require customization of the underlying operating system and database environment.
- fills the gap between RDS and EC2 running a DB engine
- RDS is fully managed, so OS/engine access is limited. DB on EC2 is self-managed, but has overhead. RDS Custom bridges this gap
- RDS Custom works for MS SQL and Oracle
- Can connect using SSH, RDP, Session Manager
- Customizing RDS Custom? Make sure to look at RDS DB Automation settings to ensure no disruptions (pause automation, customize, restart automation)

## Aurora Architecture
Aurora [Provisioned] is a AWS designed relational database engine officially part of RDS. Aurora implements a number of radical design changes which offer significant performance and feature improvements over other RDS database engines.
- Uses a "cluster", which other RDS engines don't have. Cluster contains a primary instance + 0 or more replicas which have read capability during normal operation
- For storage, Aurora uses a Cluster Volume, not local storage; faster provisioning, higher availability, better performance
- Max cluster volume space of 128 TiB
- Can have up to 15 Replicas
- Storage is SSD based; high IOPS, low latency

### Aurora - Billing
- "High watermark billing" -- If you scale up to 50 TiB and then scale down to 40, you'll still be paying for the full 50. Freed up storage can be re-used
- No free-tier option
- Aurora does not support micro-instances. Beyond RDS SingleAZ (micro), Aurora offers better value
- 100% Database size in backups are included
- Backup restores create a new cluster
- Backtrack: A rollback feature that lets you roll back to your existing cluster but to a previous point in time. "in place rewinds"

## Aurora Serverless
Serverless VS Provisioned
Aurora Serverless provides a version of the Aurora DB product where you don't need to statically provision DB instances of a certain size or worry about managing DB instances
- Removes the overhead of managing individual DB instances
- Uses concept of Arurora Capacity Units (ACUs)
- Serverless cluster has a min and max ACU tht you choose, can go to 0 and be paused, cluster adjusts based on load
- Same resilience as Provisioned (6 copies across AZs)

### Aurora Serverless - Uses
- For infrequently used applications
- New applications (where you're unsure of load levels)
- For variable workloads / unpredictable workloads
- For dev and test databases (since it can pause itself)
- Multi-tenant applications (like subscribing to app), where load is directed related to customer use/revenue

## DEMO - Migrating to Aurora Serverless. Advised to not actually do per tutorial, just watch

## Aurora Global Database
Aurora global databases are a feature of Aurora Provisioned clusters which allow data to be replicated globally providing significant RPO and RTO improvements for business continuity and disaster recovery planning. Additionally, global databases can provide performance improvements for customers .. with data being located closer to them, in a read-only form.
- Global level Aurora, primary region and 5 secondary region. Secondary clusters are read-only. Each secondary region has up to 16 replicas
EXAM: Great for Cross-Region Disaster Recovery and Business Continuity. ~1s replication times
EXAM: Global Read Scaling: Low latency performance improvements to global customers
EXAM: ~1s replication or less between regions. Recovery Point Objective (RPO) of 1 second and a Recovery Time Objective (RTO) of less than 1 minute

## Aurora Provisioned - Multi-master writes
Allows Aurora cluster to have multiple instances that are all capable of both reads and writes
- No lengthy failovers since replicas already have R/W capability

## RDS Proxy
Amazon RDS Proxy is a fully managed, highly available database proxy for Amazon Relational Database Service (RDS) that makes applications more scalable, more resilient to database failures, and more secure.
- Why do you want RDS Proxy? Opening/Closing connections consumes resources, takes time which creates latency. Esp true with serverless. Handling failure of DB is difficult
- RDS proxy changes your architecture by creating long term connection pools; instead of your app connecting to a DB every time its used, its connected to a proxy which are already open to a pool of DB connections
- Abstracts client away from DB failure

### RDS Proxy - When to use?
- too many connection errors esp. if using small/burst instances
- when using AWS Lambda: time saved, connection reuse, IAM auth
- Long running connections (SaaS apps) needing low latency
- Where resilience to DB failure is a priority
- To further reduce failover time
- Make DB transparent to application

### RDS Proxy - Key Facts (EXAM)
- Fully managed DB proxy for RDS/Aurora
- Auto-scaling, highly available by default
- Provides connection pooling to reduce DB load
- RDS proxy only accessibly from a VPC
- Accessed via a proxy endpoint; no app changes
- can enfore SSL/TLS
- Can reduce failover time by over 60%
- Abstracts failure away from your applications

## RDS - Database Migration Service (DMS)
- The Database Migration Service (DMS) is a managed service which allows for 0 data loss, low or 0 downtime migrations between 2 database endpoints.
- The service is capable of moving databases INTO or OUT of AWS.
- Runs using a replication instance via EC2, requiring Source/Destination endpoints and Source/Target Databases
- ONE of the endpoints must be running on AWS. Endpoints store connection info for source/target DBs
- Replication Instance runs one or more Replication Tasks
- Jobs can be 1 of 3 types: 
1. Full Load (one-off full-data migration), 
2. Full Load + CDC (change data capture, for ongoing replication), 
3. or CDC only (to replicate only data changes, using native tools to bulk move initial data outside of DMS)
- Schema Conversion Tool assists with schema conversion
EXAM: DB Migration question? Default to DMS as answer, especially if talking about "no-downtime migration"

### DMS - Schema Conversion Tool
- Used when converting one DB engine to another
- NOT USED for moving between COMPATIBLE DB ENGINES

#### DMS and Snowball devices
- A physical device for moving data physically
- Larger migrations (multi-TB in size) over networks takes times and consumes capacity, so DMS can utilize Snowball


## Network Storage & Data Cycle - EFS (Elastic File System)
The Elastic File System (EFS) is an AWS managed implementation of NFS which allows for the creation of shared 'filesystems' which can be mounted within multi EC2 instances.
- For scalability / resiliency
- EFS is an implementation of NSFv4 (network file system version 4)
- Can be mounted in EC2 linux and shared between many EC2 instances
- EFS is private service that mounts targets inside a VPC
- Can be accessed from on-premises via VPN or AWS Direct Connect (DX)
- Uses POSIX permissions (a linux thing)
EXAM: EFS is Linux ONLY
EXAM: 2 performance modes: 1. General Purpose 2. Max I/O
EXAM: 2 throughput modes: 1. Bursting 2. Provisioned
EXAM: 2 storage classes: 1. Standard 2. Infrequent Access (IA) - S3 Lifecycle policies can be used with these

## DEMO - Implementing EFS
Implement a simple EFS file system in a VPC, configure mount targets and configure two EC2 instances to mount the file system within a mount point.

Video: https://learn.cantrill.io/courses/1820301/lectures/41301666

Steps:
1. 1 click deploy
2. Create EFS: EFS > Create File System > Customize > name "A4L-EFS", storage class Standard, disable Encryption of data at rest, pPrformance Settings: Bursting > Next
3. EFS Network Settings: Create mount targets > Delete default SG's (blue bloxes) > Attach APP subnets: us-east-1a, "sn-app-A" etc > Security Group x3 "IMPLEMENTINGEFS[...]" > Next > Skip File System policy (optional) > Next > Review and CREATE
NOTE: any AZs within a VPC you're consuming the services provided by EFS, you should be creating a mount target
4. EC2 Instances > duplicate EC2 instance tab > tab 1, EC2 connect to instance A, tab 2 connect to B
5. EC2 Connect Instance A > `sudo mkdir -p /efs/wp-content` (creates file as well as any paths like /efs/ with the -p) >
`sudo dnf -y install amazon-efs-utils` package of tools which allows this instance to interact with EFS >
`cd /etc` >
`sudo nano /etc/fstab` >
Paste this into 3rd line of nano: `file-system-id:/ /efs/wp-content efs _netdev,tls,iam 0 0` > 
6. Paste EFS file system ID of A4L EFS into the nano text above, replacing 'file-system-id`
7. Save Nano: ctrl+o to save, Enter, ctrl+x to exit
8. `df -k` still not showing anything. Time to mount file system: `sudo mount /efs/wp-content`, now `df -k` will show it >
`cd /efs/wp-content` (move into new file system) >
`sudo touch amazingtestfile.txt` (create test file)
9. Instance B Connect: 
df -k >
sudo dnf -y install amazon-efs-utils >
sudo mkdir -p /efs/wp-content >
sudo nano /etc/fstab >
file-system-id:/ /efs/wp-content efs _netdev,tls,iam 0 0 >
sudo mount /efs/wp-content >
cd /efs/wp-content/ >
ls -la -- you'll see amazingtestfile.txt in the directory which was created in instance A 
10. Clean up: EFS > Delete file system > Cloudformation > Delete stack

## AWS Backup
Use AWS Backup to centralize and automate data protection across AWS services and hybrid workloads. AWS Backup offers a cost-effective, fully managed, policy-based service that further simplifies data protection at scale. AWS Backup also helps you support your regulatory compliance or business policies for data protection. Together with AWS Organizations, you can use AWS Backup to centrally deploy data protection policies to configure, manage, and govern your backup activity across your company’s AWS accounts and resources.
- fully managed data-protection
- consolidate backups across accounts/regions into one place

### AWS Backup - Components
- Backup Plans: frequency, window, lifecycle, vault, region copy
- Backup resources: the resources being backed up
- Vaults: destination for backups (container). Assign KMS key for encryption
- Vault Lock: WORM write-one-read-many, 72 hour cool off, then even AWS can't delete
- On-Demand backups when you require
- PITR: Point in time recovery


# HA & Scaling

## Regional and Global AWS Architecture
Global Components - Global Svc Location/Discovery, Content Delivery+optimization, global health checks/failover
Regional Components - Regional entry point, scaling/resilience, app svc's/components

## Evolution of Elastic Load Balancer (ELB)
Currently 3 types of ELBs available in AWS split between v1 (avoid this) and v2 (use this). "ELB" refers to all 3.
- Version 1: Classic Load Balancer (CLB), 2009. Not really layer 7, only one SSL per CLB
- Version 2: 
-- v2-1. Application Load Balancer (ALB): HTTP/HTTPS/WebSocket. Layer 7 device
-- v2-2. Network Load Balancer (NLB): TCP, TLS, UDP. For apps that don't use HTTP/HTTPS, like email or SSH servers
- Version 2 is faster, cheaper, supports target groups and rules

## Elastic Load Balancer (ELB) 
Job of a Load Balancer is to accept connections from a user and distribute that connection to the backend of the app
- "dual stack" means using both IPv4/6
- config'd to run in 2+ AZ's. 1+ nodes are placed into a subnet in each AZ and scale with load
- Each ELB confg'd with an A record DNS name which resolves to the ELB nodes. Requests distributed to nodes, nodes scale within AZ
EXAM: ELB can be internet-facing (given public and private IP Addresses) or internal (given only private IP addresses)
EXAM: Internet-Facing LB can still access both public AND private EC2 instances
EXAM: /27 or larger subnet is minimum for load balancer. /28 is 2nd most correct answer

### ELB - Cross-Zone Load Balancing
- Load Balancer Nodes can send requests across an AZ to any other registered instance in other AZs for further balancing
- Comes enabled as default

## ELB EXAM
EXAM: ELB is a DNS A Record pointing at 1+ Nodes per AZ
EXAM: Nodes can scale per subnet
EXAM: Internet-facing nodes have public IPv4 IPs
EXAM: Internal-facing nodes have only Private IPs
EXAM: EC2 instance does NOT need to be public to work with an internet-facing LB
EXAM: Listener Config controls WHAT the LB does
EXAM: ELBs required 8+ free IPs per subnet, and at least /27 subnet to allow scaling


## Application Load balancing (ALB) vs Network Load Balancing (NLB)
When to pick ALB vs NLB.
- Remember, always avoid Version 1 Classic Load Balancer -- does not scale.

### Version 2, APPLICATION Load Balancers: 
- Layer 7 LB's. Listens on either HTTP and/or HTTPS
- Doesn't listen to any other Layer 7 protocols (SMTP, SSH, Gaming, etc)
- Can't listen to TCP/TLS/UDP
- Can't do end-to-end unbroken SSL encryption as the request is terminated on ALB and new connection is made from ALB -> App
NOTE: if you need unbroken encryption, you need to use a Network Load Balancer
- ALBs using HTTPS must have an SSL cert on that LB
- ALBs are slower than NLB as they're more complex
- As they are Layer 7, they can do health checks at Layer 7
- "Rules" - Direct connections which arrive at a listener, rules processed in priority order, there is a final Default Rule as a catch-all
- "Rule Conditions"
- "Actions" - follows rules
NOTE: if you need unbroken encryption, you need to use a Network Load Balancer

### Version 2: NETWORK Load Balancers
- Layer 4 LBs: TCP, TLS, UDP, TCP_UDP
- No visibility or understanding of HTTP/S; can't see headers, cookies, session stickiness
- NLBs are super fast, about 25% of ALB latency
- Good for SMTP, SSH, game servers which don't use web protocols, financial apps which don't use web protocols
- health checks not app aware, they just check ICMP/TCP handshakes
- can have static IPs which is useful for whitelisting
- can forward TCP to instances for UNBROKEN ENCRYPTION
- used for PRIVATE LINK to provide services to other VPCs

EXAM: Need unbroken encryption? Network Load Balancer
EXAM: Need highest performance LB? NLB
EXAM: Need Private Link? NLB
EXAM: Static IP? NLB

EXAM--
### ALB VS NLB
- Need unbroken encryption? Network Load Balancer
- Static IP for whitelisting? NLB
- Best performance? NLB
- Operate on non-HTTP/S? NLB
- Private Link? NLB
- Otherwise... ALB

## EC2 Launch Configuration and Templates
Both alllow you to define config of an EC2 instance in advance
- Including....
-- AMI, instance type, storage & keypair, networking and SGs, userdata and IAM role
- Configs are NOT editable; defined one. But, Launch Templates have versions
- LT came after LC so it has newr features like T2/T3 unlimited, placement ggroups, capacity reserveations, elastic graphics
NOTE: AWS recommends using Launch Templates over LCs
- LC's have one use: only used as part of Auto Scaling groups

## Auto Scaling Groups
Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also enables you to use Amazon EC2 Auto Scaling features such as health check replacements and scaling policies. Both maintaining the number of instances in an Auto Scaling group and automatic scaling are the core functionality of the Amazon EC2 Auto Scaling service.
- "seal healing" for EC2
- uses launch templates or configs to launch all scaled instances
- Auto-scaling group has three important values: Minimum size, desired capacity, maximum size (eg 1:2:4), called min/desired/max or x/y/z
- Auto-scaling keeps running instances at the DESIRED capacity by provisioning/terminating instances
- Scaling Policies automate based on metrics like CPU load

### Auto-Scaling Groups - Scaling Policies
Scaling policies are rules. Three ways you can scale auto-scaling groups:
1. Manual Scaling. Manually adjust min/desired/max
2. Scheduled Scaling. Time-based adjustment
3. Dynamic Scaling (3 subtypes). Rules which react to something and change 
- a. Simple Scaling. Often a pair of rules: "CPU above 50%,  +1. CPU below 50%, -1."
- b. Stepped Scaling. Bigger +/- based on difference (generally use this over Simple unless simplicity is the priority)
- c. Target Tracking. Eg.. Desired aggregate CPU to stay at 40%
Cooldown Periods: How long to wait at the end of a scaling action before doing another

### ASG - Health
ASG performs healths checks using EC2 status checks
- Self healing: If ASG detects downed instance, it will replace the downed instance with a newly provisioned one

### ASG - ASG + Load Balancers
- Uses Target Groups
- Can use Load Balancer health checks instead of EC2 health checks; application aware health checks (which ec2 health checks are not)

### ASG - Scaling Processes
- LAUNCH and TERMINATE (can SUSPEND / RESUME) any process, like suspending the Launch process to not scale out if event takes place
- AddToLoadBalancer - Add to LB on launch
- AlarmNotification - Accept notification from CloudWatch
- AZRebalance - Balances instances evenly across all AZs
- HealthCheck - health checks on/off
- ReplaceUnhealthy
- ScheduledActions
- Standby or InService

### ASG - Final Points
EXAM: Autoscaling groups are free; only the resources created are billed (use cooldowns to avoid rapid scaling and increased costs)
EXAM: Think about using more smaller instances for granularity - higher control and more cost-effective
EXAM: Use with Application Load Balancers for elasticity; abstraction
EXAM: ASG defines WHEN/WHERE, Launch Templates/Configs define WHAT

## ASG - Scaling Policies
Scaling policies are NOT REQUIRED on ASGs
- Manual - When you set Min / Desired / Max. Best for Testing or when urgent
- Step / Simple scaling: you choose scaling metrics and threshold values for the CloudWatch alarms that trigger the scaling process. You also define how your Auto Scaling group should be scaled when a threshold is in breach for a specified number of evaluation periods
-- Step / Simple scaling require you to create CloudWatch alarms for the scaling policies. Both require you to specify the high and low thresholds for the alarms
-- Step / Simple scaling require you to define whether to add or remove instances, and how many, or set the group to an exact size
- Scaling based on SQS - ApproximateNumerOfMessagesVisible

## ASG - Lifecycle Hooks
Lifecycle hooks enable you to perform custom actions by pausing instances as an Auto Scaling group launches or terminates them. When an instance is paused, it remains in a WAIT state either until you 1. complete the lifecycle action using the complete-lifecycle-action command or 2. the CompleteLifecycleAction operation, or 3. until the timeout period ends (one hour by default) then CONTINUE or ABANDON.
- Configure Custom Actions on instances during ASG actions (launch or terminate transitions)
- Can be config'd with EventBridge or SNS Notifications

## ASG - Health Check Comparison: EC2 VS ELB
Amazon EC2 Auto Scaling can determine the health status of an instance using one or more of the following: 
- Amazon EC2. To identify hardware and software issues that may impair an instance. This is the Default for ASG
- Elastic Load Balancing (ELB). Disabled by default. ELB health checks can be application aware (Layer 7)
- Custom Health Checks. Instances marked Healthy/Unhealthy by an external system

EXAM: Health Check Grace Period (default 300s); a delay before starting health checks which first allows system to launch, bootstrap, application start 

## Elastic Load Balancer - SSL Offload & Session Stickiness
Three ways a load balancer handles secure connections: Bridge, Pass Through, Offloading
- Bridging (default). SSL encrypt/decrypt happens at ELB, but instances still need SSL certs and compute required for crpyto operations
- Pass Through. No encypt/decrpyt happens at ELB, instead each instance has SSL Cert installed
- Offload. SSL decrypted at ELB and then only plain text HTTP goes through to instance. Instance doesn't need SSL cert or crypto compute capability

### ELB - Connection Stickiness 
- With no stickiness, connections are distributed across all in-service backend instances
- With stickiness, a cookie is generated (AWSALB) which locks the device to a single backend instance for a set duration: 1 second to 7 days
NOTE: Instead of worrying about this, just make sure servers are stateless and state is stored elsewhere like the DB

## DEMO - EMB - Seeing Session Stickiness in Action
How session stickiness works with Application Load Balancers
Video: https://learn.cantrill.io/courses/1820301/lectures/43242687

## ADVANCED DEMO - Architecture Evolution
Stage 1 - Setup the environment and manually build wordpress - https://learn.cantrill.io/courses/1820301/lectures/41301448
Stage 2 - Automate the build using a Launch Template
Stage 3 - Split out the DB into RDS and Update the LT
Stage 4 - Split out the WP filesystem into EFS and Update the LT
Stage 5 - Enable elasticity via a ASG & ALB and fix wordpress (hardcoded WPHOME)
Stage 6 - Cleanup

## Gateway Load Balancer (GWLB)
Gateway Load Balancers enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It combines a transparent network gateway (that is, a single entry and exit point for all traffic) and distributes traffic while scaling your virtual appliances with the demand.
- At high level, GWLBs have two main components:
1. Endpoints. Traffic enters/leaves via these endpoints
2. The GWLB itself; balances packets across multiple backend instances

- Traffic and metadata is tunneled using GENEVE protocol
- GWLB = network security at scale


## Serverless and Application Services 

### Architecture Deep Dive - Event-Driven Architecture
Types of architecture:
- MONOLOTHIC: everything is built together and coupled; everything is always running and incurring charges even if not being used; if one part fails, whole thing fails
- TIERED: monolith broken apart into tiers that can be on same server or different servers. Tiers still coupled as they each connect to endpoint of next tier. Benefits are that tiers can be vertically scaled independently (server size of each tier can be increased).
-- if you add load balancers between tiers, this abstracts tiers meaning that you can now horizontally scale tiers by adding instances (the tiers are no longer connected to each other but to LBs. Still not decoupled though.
- QUEUE-BASED Decoupled Architecture: The queue would sit between components (tiers) to decouple, the components no longer require answers; now the components are using async communications
- MICROSERVICE Architecture: tiers/components become Microservices that can be duplicated. There are Producers, Consumers, and Both
-- Producers produce data, Consumers consume data/messages, 'Both' does ..both
--- Events are what are consumed. Queues can be used to communicate events
- EVENT DRIVEN Architecture: Event Producers / Event Consumers. You can have components that can do Both
-- Best-practice Event-driven arch's have Event Routers, which are highly available central exchange points for Events. Nothing is sitting around waiting, they are activated when an Event is sent to them; only consumes resources while handling events (serverless)

### Lambda
- FaaS: Function as a Service - short running and focused
- Lambda function: piece of code that lambda runs
- Functions use a runtime like Python 3.8
- Functions loaded into a runtime environment; env has a direct memory (indirect CPU) allocation
- Billing: for the duration that the function runs
- Lambda is a key part of Serverless architectures
- Lambda Function: Think of it as the code + association wrappings/config; a deploment package. Stateless
- You define Lambda resources like Memory (128MB -> 10240MB in 1MB steps), which then scales how much CPU you'll get (you can't directly control how much CPU). Storage in Lambda stored in /tmp 512MB -> 10240MB

EXAM: Lambda function timeout 900s (15 minutes). Anything beyond 15 mins can't use Lambda directly

#### Common Uses of Lambda
- Serverless applications 
- File processing
- Database triggers
- Serverless CRON
- Real time stream data processing (kinesis + lambda)

#### Lambda Networking Modes
1. Public (Default)
2. VPC

1. Public: Could access Public AWS svc's like SQS, DynamoDB, or external like IMDB
- Lambda functions have no access to VPC unless public IPs are provided and security controls allow external access
2. Private (in VPC): Lambda functions running in a VPC obey ALL VPC networking rules (can't access external stuff unless configured as such). Eg. Could use a gateway endpoint to access dynamodb

#### Lambda - Security
- Execution Role: For Lambda env to access AWS p&s it needs an Execution Role to gain the role's permissions based on the role policy
- Lambda Resource Policies: similar to bucket policy on S3 which controls WHO/WHAT can interact with a specific Lambda function. Eg. services like SNS or S3 being allowed to invoke the function

### Lambda - Logging
Lambda uses CloudWatch, CloudWatch Logs, and X-Ray
- Logs from Lambda executions -> CloudWatch Logs
- Metrics like invocation success/failures, retries, latency -> CloudWatch
- Distributed Tracing Capability -> X-Ray. Eg. Trace the path of a user through an application
NOTE: CloudWatch Logs requires permissions via the Execution Role

### Lambda - Invocation
Types:
- Synchronous
- Asynchronous
- Event Source Mappings

Synchronous: CLI/API invokes lambda function and then CLI/API WAITS for a response. Errors/Retries/Reprocessing must happen on the client side. Synchronous is generally invoked by a human

Asynchronous: Typically used when AWS svc's invoke lambda functions. Reprocessing is handled by Lambda
- Lambda function needs to be idempotent; reprocessing a result should have the same end-state. Eg. Adding +$10 to an account or Setting account to $10 explicitly. If adding fails in a certain way, you could end up with 20, 30, 40 etc. Idempotent failures still explicitly set the account to $10 value over and over
- Events can be sent to DLQ's (dead letter queues) after repeated failed processing
- Lambda support destinatoins where successful or failed events can be sent like SQS, SNS, Lambda & EventBridge

Event Source Mapping: Typically used on streams or queues which don't support event generation to invoke Lambda (Kinesis data stream, DynamoDB streams, SQS queues, Amazon Managed streaming for Apache Kafka). Event Source Mapping polls these streams/queues looking for data and getting back 'source batches', split based on batch size, sent to Lambda function

### Lambda - Versions 
Lambda can have versions... v1, v2, v3. The VERSION of Lambda function is 'code + config'
- Versions are immutable when published and has its own ARN. $Latest points at the ..latest... version
- Lambda functions can have aliases like DEV, STAGE, PROD which can be changed

### Lambda - Startup times
- An 'execution context' is the environment a lambda function runs in
- A 'cold start' is a full creation and configuration including function download
- A 'warm start' can occur if another lambda function is invoked shortly after a first, now it doesn't have to rebuild the execution context (no build process)
- Event source mapping uses permissions from the Execution Role to access the source svc that it pulls data from


## CloudWatch Events and EventBridge
CloudWatch Events and EventBridge have visibility over events generated by supported AWS services within an account.
- They can monitor the default account event bus - and pattern match events flowing through and deliver these events to multiple targets.
- They are also the source of scheduled events which can perform certain actions at certain times of day, days of the week, or multiple combinations of both - using the Unix CRON time expression format.

EventBridge is replacing CW Events as EventBridge can do all the same things but also handle third-party and custom app events (AWS recommending using EventBridge)

### Key Concepts, CloudWatch Events and EventBridge
- If X happens, or at Y times... do Z
- EventBridge is basically CW Events v2
- A default Event Bus exists on an AWS account for both CW Events and EB
- In CW Events, only 1 event bus. In EB you can have add't event busses
- Rules created match incoming events (or schedules)
-- Two rule types: 1) Event Pattern Rule 2) Schedule Rule 


## DEMO - Automated EC2 Control Using Lambda and Events
Gain experience of using Lambda for some simple account management tasks.

1. 1 click deploy
2. Give Lambda Permissions: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0024-aws-associate-lambda-eventdrivenlambda/lambdarole.json > IAM > Role >  Create Role > Entity Type, AWS Service, select Lambda > Next
3. Create IAM Role Policy: Click 'Create Policy' > JSON tab > Paste JSON provided > Next > Policy name "Lambdastartandstop" > Create Policy
4. Create IAM Role with Policy: IAM Role tab > Select Policy for IAM Role > Role name "EC2StartStopLambdaRole" > Create Role
5. EC2 > Copy both instance ID's to notepad/clipboard
6. Create Lambda Function: Lambda > Create function > select Author from Scratch > name "EC2Stop" > runtime "Python 3.9" > dropdown "Change default exec role", select Use Existing, select the IAM Role you created > Create Function > paste in code to Lambda code block from file lambda_instance_stop.py > click Deploy
7. Creat env variable for EC2Stop: Lambda function, configuration tab > Environment Variables "Edit" > click "Add env variable" > key: EC2_INSTANCES, value: "ec2_instance_ID_1,ec2_instance_ID_2"
8. Test Event: EC2Stop Lambda Function, Test tab > Event name "test" > Test. Observe EC2 instances being stopped.
9. Create second function "EC2Start" > Lambda, Functions "Create Function" > name "EC2Start" > Existing IAM Role > Create function > add new code from lambda_instance_start.py > Paste code, Deploy >  Environment Variables "Edit" > click "Add env variable" > key: EC2_INSTANCES, value: "ec2_instance_ID_1,ec2_instance_ID_2" > Save
10. Test Event: EC2Start Lambda Function, Test tab > Event name "test" > Test. Observe EC2 instances being started.
11. Set up Event-driven Lambda Function: Lambda > New Function name "EC2Protect" > Runtime python 3.9 > Select IAM role that we created > Create function > Add code from file "lambda_instance_protect.py", Deploy
12. Create EventBridge Rule for Lambda to receive: EventBridge > New Rule name "EC2Protect" > desc "Start protected instance" > select "rule with an event pattern" > Event Source "AWS events or EventBridge partner events" > Event pattern "AWS Services", "EC2", event type: EC2 Instance State-change Notification, Specific States: Stopped > Specific Instance IDs, paste instance 1 ID > Next > Target 1 AWS Svc, "Lambda function", Function: EC2Protect > Create Rule
13. Clean up: Lambda, delete functions > EventBridge, delete Rules > IAM Policies, delete Lambda policy > Delete Lambda IAM Role > CloudFormation, delete Stack 

## Serverless Architecture
The Serverless architecture is a evolution/combination of other popular architectures such as event-driven and microservices.
- Aims to use 3rd party services where possible and FAAS products for any on-demand computing needs.
- Using a serverless architecture means little to no base costs for an environment - and any cost incurred during operations scale in a way with matches the incoming load

### Serverless - Key Concepts
- Serverless isn't one single thing; aiming to manage few, if any, servers for lower overhead
- Stateless and Ephemeral env's; duration billing
- Function as a Service; FaaS used where possible for Compute functionality
- Managed Services are used where possible; web Id providers, S3 for storage, etc.
- Event-driven; consumption only when being used

### Serverless: TL;DR and Architecture
Aim should be to consume as a service whatever you can, code as little as possible, use function as a service for any general compute needs

## SNS - Simple Notification Service
The Simple Notification Service or SNS is a PUB / SUB style notification system which is used within AWS products and services but can also form an essential part of serverless, event-driven and traditional application architectures.
- Public AWS Service; network connectivity with a Public Endpoint
- Publishers send messages to TOPICS
- Subscribers receive messages SENT to TOPICS
- Messages are <= 256KB payloads
- SNS supports a wide variety of subscriber types including other AWS services such as LAMBDA and SQS
- SNS is REGIONALLY RESILIENT. Highly available and scalable
- Can provide delivery STATUS and delivery RETRIES
- SNS capable of server-side encryption
- SNS can be cross-account with a TOPIC POLICY

## AWS Step Functions
AWS Step Functions addresses some problems within Lambda. 
- Lambda is FaaS, each Lambda should be as simple as possible; you'd never put a full application in a Lambda Function (execution duration limit: 15 minutes). Theoretically, you can chain Lambda functions but this gets messy at scale
- Lambda runtime env's are stateless (can't hold state through different Lambda functions)

Step Functions let you create STATE MACHINES (a workflow with start point and end point). START -> STATES -> END
- States are THINGS which occur
- Max Duration of State Machines is 1 YEAR
- Two workflows in State Machines:
1. Standard Workflow (default); 1 YEAR execution limit
2. Express Workflow: designed for high-volume, event-processing workloads, etc for UP TO 5 MINUTES
- You can Export your State Machine as a JSON template called "Amazon States Language (ASL)"
- IAM Role used for permissions

### Step Functions: State Machines: Types of States
- Succeed and Fail.
- Wait. Wait for certain period of time to elapse, or for a particular date/time that was set. Holds / Pauses workflow until duration passes
- Choice. State Machine can take different paths depending on input
- Parallel. Create parallel branches within a state machine
- Map. Takes list of items and performs action/set of actions on each item in list
- Task. Represents a Single unit of work performed by a State Machine

## API Gateway 101
API Gateway is a managed service from AWS which allows the creation and management of API Endpoints, Resources & Methods. Endpoint/entry-point for applications
- The API gateway integrates with other AWS services - and can even access some without the need for dedicated compute.
- It serves as a core component of many serverless architectures using Lambda as event-driven and on-demand backing for methods.
- It can connect to legacy monolithic applications and act as a stable API endpoint during an evolution from a monolith to microservices and potentially through to serverless.
- API Gateway sites between applications and integrations (services)
- Can connect to svc's/endpoints in AWS or ON-PREMISES
- HTTP APIs / REST APIs / WEB SOCKET APIs

### API Gateway - Authentication
- Can use COGNITO user pools for authentication
- Can use LAMBDA for authentication 

### API Gateway - Endpoint Types
- Edge-optimized. Incoming requests routed to nearest CloudFront POP (point of presence)
- Regional. Clients in the same region
- Private. Endpoint accessible only within a VPC via interface endpoint

### API Gateway - Stages
- When you deploy an API config in API gateway, you do so in a stage. APIs are deployed to stages, each stage has one deployment. Eg. prod and dev stages

### API Gateway - ERRORS
EXAM - Memorize numbers
- Error codes generated by API gateway 2 categories:
1. 4xx - 400 series client-side error
2. 5xx - 500 series server-side error
- Error Codes:
-- 400: Bad request; generic; many root causes possible
-- 403: Access Denied; authorizer denies or WAF filtered
-- 429: Throttling is occuring in API Gateway
-- 502: Bad gateway excption; bad output returned by Lambda
-- 503: Service unavailable. Backing endpoint offline or major service issues
-- 504: Integration Failure/Timeout - 29s limit for any requests to API gateway
Resource: https://docs.aws.amazon.com/apigateway/latest/api/CommonErrors.html

### API Gateway - Caching
- Caching is configured per Stage
- Cache TTL default: 300 seconds; configurable min/max 0s/3600s
- Can be encrypted
- Cache size: 500MB -> 237GB

## DEMO - Build a Serverless App - Skipping for now

## Simple Queue Service (SQS)
SQS queues are a managed message queue service in AWS which help to decouple application components, allow Asynchronous messaging or the implementation of worker pools.
- SQS comes in 2 types: 
1) Standard - best efforts; messages could be received out of order
2) FIFO - guarantees the order
- Like SNS, messages <= 256KB in size
- Polling: When a client checks for messages on a queue
EXAM -- Received messages are HIDDEN (VisibilityTimeout - amount of time a msg is hidden). If the message isn't explicitly deleted, it will reappear (retry) in the queue
- Dead-Letter Queue: Can be used for problem messages. Eg if message is received 5 or more times
- SQS good for scaling: ASG's can scale based off SQS, Lambdas can invoke based on queue length -> This is good for ASG Worker Pool Architecture
EXAM - Fanout Architecture: SNS fans messages out to multiple SQS queues

### Delivery Methods - Standard / FIFO
- Standard = guaranteed to deliver 'at-least-once' with no promise on order of delivery
- FIFO = guaranteed to deliver 'exactly-once' and guarantee message order
-- FIFO performance is lower: 3,000 messages / second with batching or 300 messages/second without batching. Not as good for scaling as Standard
- Billing: Based on "requests". A request can be 1-10 messages up to 64KB total
- Polling Types (2)
1) Short Polling (immediate)
2) Long Polling (waitTimeSeconds, up to 20s) - BEST PRACTICE; more cost effective as less requests per message. Will poll for a 20s duration collecting up to 10 messages and 64KB in data 
- SQS supports encryption at rest (KMS) and in-transit
- Can add Queue policies

## SQS -  SQS Standard vs FIFO Queues
### Standard
- Multi-lane highway. Scalable, nearly unlimited Transactions per second
- Best-efforts ordering; no rigid order
- Best for decoupling, worker pools, Batch for future processing
### FIFO
- Single-lane highway (performance limited by width of lanes). 300 TPS w/o batching, 3,000 TPS with
- Delivered in a guaranteed order
EXAM - FIFO queues Must have a .fifo suffix
- Exactly-once processing: removes chance of duplicate message delivery

## SQS - Delay Queues
Delay queues provide an initial period of invisibility for messages; postpone delivery to consumers. Predefined periods can ensure that processing of messages doesn't begin until this period has expired.
- A message is automatically hidden once it hits a queue
- NOT the same as Visibility Timeout; VT is automatic re-processing of problem messages whereas this is an initial delay in processing of all messages 
- DelaySeconds min is 0, it has to be non-zero to be a Delay Queue
- NOT SUPPOERTED ON FIFO QUEUES

## SQS - Dead-Letter Queues (DLQ)
Dead letter queues allow for messages which are causing repeated processing errors to be moved into a dead letter queue.
- Eg. Message received but keeps re-appearing after visibility timeout and not explicitly deleted (this could technically happen forever unless you set up a DLQ)
-- Each time a message re-appears in queue after timeout, the ReceiveCount tally is incremented
-- when ReceiveCount > maxReceiveCount && message is NOT deleted, it's moved to DLQ

## Kinesis Data Streams
Kinesis data streams are a real-time, scalable streaming service within AWS designed to ingest large quantities of data and allow access to that data for consumers
- Ideal for dashboards and large scale real time analytics needs
- Kinesis data firehose allows the long term persistent storage of kinesis data onto services like S3
- Producers send data into a kinesis STREAM, which can scale from low to near infinite data rates
-- Streams store a 24-hour moving window of data
--- This storage is included and can be increased to MAX 365 days of moving data window (add'l costs)
--- Multiple consumers access data from this moving window

### Kinesis VS SQS
- SQS = decoupling, asynchronous communications. No message persistence, no window of data stored
- Kinesis = huge-scale data ingestion, real-time data streaming. Made for multiple consumers and has a rolling window of stored data for persistence (default 24 hrs, up to 365 days for add'l cost)

## Kinesis Data Firehose
Fully managed service to load data for data lakes, data stores (like S3), and analytics svc's -> This lets data be persisted beyond the rolling window of Kinesis Data Streams
- Auto scaling, fully serverless, resilient
EXAM - NEAR real-time delivery (~60s) which is unlike the main Kinesis Data Stream which offers real-time delivery
- Firehose supports transformation of data on the fly using Lambda
- Valid destination endpoints for Firehose: HTTP, Splunk, Redshift, ElasticSearch, S3

## Kinesis Data Analytics
Amazon Kinesis Data Analytics is the easiest way to analyze streaming data, gain actionable insights, and respond to your business and customer needs in real time.
- Real-time processing of data using SQL
- Ingests from Kinesis Data Streams or Firehose
- Destinations of analyzed data: Firehose (and subsequently S3, Redshift, ElasticSearch, Splunk), AWS Lambda, Kinesis Data Streams
-- If OUTPUT to firehose, data becomes NEAR REAL-TIME. If output to Kinesis Data Streams or Lambda data stays REAL-TIME

### When to use Kinesis Data Analytics
- streaming data needing real-time SQL processing
- time-series analytics like elections, esports
- real-time dashboards like leaderboard for games
- real-time metrics like for security/response teams

## Kinesis Video Streams
Amazon Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), playback, and other processing. Kinesis Video Streams automatically provisions and elastically scales all the infrastructure needed to ingest streaming video data from millions of devices
- ingest LIVE video data from things like security cameras, phones, cars, drones, time-serialised audio, thermal, depth, RADAR
- consumers can access data frame-by-frame or as-needed
- Can PERSIST and ENCRYPT (in-transit and at-rest)
EXAM: CANNOT directly access the data via storage, only via APIs
- Integrates with other AWS svc's like REKOGNITION and CONNECT

## Amazon Cognito - User and Identity Pools
A user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app through Amazon Cognito
- Users can also sign in through social identity providers like Google, Facebook, Amazon, or Apple, and through SAML identity providers
- Whether your users sign in directly or through a third party, all members of the user pool have a directory profile that you can access through a Software Development Kit (SDK).
- Amazon Cognito identity pools (federated identities) enable you to create unique identities for your users and federate them with identity providers. With an identity pool, you can obtain temporary, limited-privilege AWS credentials to access other AWS services. 

Cognito provides the following for web/mobile apps:
- authentication
- authorization
- user management

Cognito has 2 components:
1. User pools: for sign-in. You get a JSON Web Token (JWT) if successful (but most AWS svc's don't use this JWT)
- user directory mgmt/profiles, sign up and sign in (with UI), MFA and other security features
- most AWS services CANNOT be accessed using JWT via User Pools
- can use internal or social logins for sign in
2. Identity pool: Swap external ID for temporary AWS credentials. 
- Unauthenticated ID's; guest users

USER POOLS = SIGN IN / SIGN UP
IDENTITY POOLS = ABOUT SWAPPING ID TOKENS (with Google, Apple, etc) for temporary tokens to access AWS services

### Cognito - Web ID Federation (using User Pools and Identity Pools in conjunction)
- First, User Pool JWT replaces all the different external token configs you'd need for handling different external IDs (User Pool removes admin overhead of handling all external social logins)
- Next, app can pass this User Pool token through to an Identity Pool
- Federated Identities can swap (Eg. give Google creds to swap for AWS creds)

## AWS Glue
- Fully managed SERVERLESS extract, transform, and load (ETL) service which makes it easy for customers to prepare and load their data for analytics
-- Can create and run an ETL job with a few clicks in the AWS Management Console.
- Simply point AWS Glue to your data stored on AWS, and AWS Glue discovers your data and stores the associated metadata (e.g. table definition and schema) in the AWS Glue Data Catalog. Once cataloged, your data is immediately searchable, queryable, and available for ETL.
- Moves/transforms data between source/destination
- Data Sources: Stores: S3, RDS, JDBC Compatible, DynamoDB. Data Sources: Streams: Kinesis Data Stream, Apache Kafka
- Data Targets: S3, RDS, JDBC Databases
- Crawls data sources and generates the AWS Glue Data Catalog

### AWS Glue Data Catalog
- Persistent metadata about data sources within a region
- One catalog per region per account
- Configure crawlers for data sources

### Glue Jobs
Extract, transform (using script), and load Jobs
- Can be initiated manually or via EVENTS using EventBridge

### Glue VS Data Pipeline (both do ETL)
- Glue is serverless, ad-hoc, more cost-effective
- Data Pipeline requires a server

## Amazon MQ
AmazonMQ is an open-source message broker; an AWS implementation of Apache ActiveMQ. Like a merge of SNS/SQS
- Supports open standards such as JMS, AMQP, MQTT, OpenWire and STOMP
-- If you need to support any of these, and use QUEUES and TOPICS - AmazonMQ is the tool to use.
- Provides Queues and Topics (like SQS/SNS); one-to-one or one-to-many
EXAM: Amazon MQ is NOT a public service; runs on a VPC and requires private networking to access it
EXAM: AWS Integration required? Use SNS/SQS and not MQ. 
EXAM: Migrate from an existing system with little to no app change? Amazon MQ
EXAM: Need APIs like JMS or protocols like AMQP, MQTT, OpenWire, STOMP needed? Amazon MQ

## Amazon AppFlow
Amazon AppFlow is a fully managed integration service that enables you to securely transfer data between Software-as-a-Service (SaaS) applications like Salesforce, SAP, Zendesk, Slack, and ServiceNow, and AWS services like Amazon S3 and Amazon Redshift, in just a few clicks. 
- With AppFlow, you can run data flows at enterprise scale at the frequency you choose: on a schedule, in response to a business event, or on demand. 
- You can configure data transformation capabilities like filtering and validation to generate rich, ready-to-use data as part of the flow itself, without additional steps. 
- AppFlow automatically encrypts data in motion, and allows users to restrict data from flowing over the public Internet for SaaS applications that are integrated with AWS PrivateLink, reducing exposure to security threats.
-- Can use AppFlow Custom Connector SDK to build your own integration if the integration doesn't already exist
- Exchange data between applications (connectors) using FLOWS; SYNC or AGGREGATE data
- PUBLIC endpoints, but works with PrivateLink
- CONNECTIONS store config/creds to access apps. Connections can be reused across many flows


# GLOBAL CONTENT DELIVERY AND OPTIMIZATION
## Cloudfront Architecture
CloudFront is a Content Delivery network (CDN) within AWS.
- Origin: The source location of your content (can be S3 or custom origin)
- Distribution: The 'configuration' unit of CloudFront
- Edge Locations: Local cache of your data
- Regional Edge Cache: Larger version of an Edge Location, provides another layer of caching
NOTE: Can use SSL certs with CloudFront as it integrates with AWS Certificate Manager (ACM) for HTTPS
NOTE: CloudFront is for DOWNLOAD operations only, uploads go directly to Origin with NO WRITE CACHING. CloudFront does Read-Only caching

## CloudFront (CF) - Behaviors
CloudFront Behaviors control much of the TTL, protocol and privacy settings within CloudFront
- Behaviors have caching options, and restrict viewer access options
- Distribution can have multiple behaviors, but there is one Default(*) behavior

## CloudFront - TTL and Invalidations
How CloudFront handles object expiry and invalidation
- Covering

- TTL: Object considered not expired when within its TTL
Default TTL: 24 hours (validity period)
Minimum TTL / Maximum TTL can be set

You can specify TTLs using headers.
-- Origin Header Types:
--- Cache-Control max-age (seconds until expiry)
--- Cache-Control s-maxage (seconds until expiry)
--- Expires (Date & Time for expiry)

- Cache Invalidation: Performed on a distribution and applied to all Edge Locations 
-- immediately expires objects regardless of their TTL based on the invalidation pattern that you specify
-- Instead of Cache Invalidation, you can use Versioned File Names (whiskers1_v1.jpg // _v2.jpg // _v3.jpg) which is a better practice

## AWS Certificate Manager
A service which allows the creation, management and renewal of certificates. It allows deployment of certificates onto supported AWS services such as CloudFront and ALB.
- HTTP was/is simple and insecure. HTTPS introduced a layer of encryption to HTTP encrypting the data in-transit. HTTPS also allows for servers to prove their identity with Certificates using SSL/TLS
-- These certificates get signed by a trusted authority AKA Chain of Trust

- ACM can be a Public or Private Certificate Authority (CA)
EXAM - ACM can generate or import certificates. If self-generated, it can auto-renew. If imported, you are responsible for renewal
EXAM - Certificates can only be deployed out to SUPPORTED services (Eg. pretty much just CloudFront and ALBs, specifically NOT EC2)
EXAM - Reminder, cannot use ACM with EC2
EXAM - Certs can't leave the region they are generated/imported into; cert are region specific
EXAM - To use a cert with an ALB in ap-southeast-2, you need a CERT IN ACM in ap-southeast-2
- EXAM -- GLOBAL services like CloudFront operate as though within us-east-1

## Cloudfront and SSL/TLS
- Each CloudFront distribution gets a Default Domain Name (CNAME DNS record) when created
- SSL supported by default as long as you use *.cloudfront.net cert
-- Can have Alternate Domain Names Eg. cdn.catagram.com
--- You need to verify ownership using a matching certificate
- Global service? Cert must be in us-east-1, Eg. CloudFront

When using CloudFront, you actually have TWO SSL connections:
1. Viewer => CloudFront
2. CloudFront => Origin
- Both need valid PUBLIC certificates. Self-signed certs don't work with CloudFront

## CloudFront (CF) - Origin Types & Origin Architecture
CloudFront origins store content distributed via edge locations.
- The features available differ based on using S3 origins vs Custom origins

### Origin Categories
- S3 Buckets
- AWS Media Package Channel Endpoints
- AWS Media Store Container Endpoints
- Everything else (web servers); Custom Origins. Note: An S3 as a static website is treated not as S3 but as a Web Server aka custom origin

## DEMO - CloudFront (CF) - Adding a CDN to a static Website
Implement a CloudFront distribution using an S3 bucket as the origin.

Steps:
1. 1-click deploy. At this point, site in demo is static S3
2. Host site on CloudFront: CloudFront > Create Distro > Origin domain, select s3 bucket "cfands3-top10cats[...]" > Cache key and origin requests, select "CachingOptimized" > Default root object "index.html" > Deploy/Create
Note: You can now access CDN cached files that are cached in Edge Locations. You can Invalidate (billed per Inval., do it less frequently). In this part, we changed merlin.jpg file to new image and played with caching in CloudFront. 
3. Add custom Domain name: Didn't have custom Domain made in R53 so had to watch at this point
4. SSL via ACM:

## Securing CF and S3 using OAI
Origin Access Identities (OAI) are a feature where virtual identities can be created, associated with a CloudFront Distribution and deployed to edge locations.
- Access to an s3 bucket can be controlled by using these OAI's - allowing access from an OAI, and using an implicit DENY for everything else.
-- They are generally used to ensure no direct access to S3 objects is allowed when using private CF Distributions.

### Origin-side Security
#### S3 Origin
You can have S3 Origin, or Custom Origin (S3 static website).
OAI's are a type of Identity that are associated with CF Distros to 'become' that OAI to be used in S3 Bucket Policies ; S3 Origin is locked down to only be accessible by this OAI, all else Implicit Denied. 
- Explicit Allow on S3 Policy for OAI
- Best practice: Create 1 OAI for 1 CF Distro
#### Custom Origin - Custom Headers or Traditional Firewall
1. Utilize custom headers and Viewer control policy (HTTPS), then a related Origin Control Policy that has a required Custom Header attached. Origin requires the custom header
2. Traditional Security Method: IP Ranges of CloudFront with access to a Firewall

## CloudFront - Private Distribution & Behaviours
### Signed URLs and Signed Cookies
CloudFront can be Public access or Private Access (requiring signed Cookie or signed URL)
- CF Distro is created with ONE behavior for the whole distro, which is public or private
- It'll end up having multiple behaviors, private and public
Old way required a CloudFront KEY created by account root user and account is added as a TRUSTED SIGNER
New way is TRUSTED KEY GROUPS added which can be managed with CloudFront API

### Signed URLs VS Cookies
- SignedURLs provided access to ONE object
- Signed Cooked for access to GROUPS of objects
- SignedURLs if client doesn't support cookies
- Maintain your URL? Signed Cookies

## DEMO - CloudFront (CF) - Using Origin Access Control (OAC) (new version of OAI) - SKIPPING

## Lambda@Edge
Lambda@Edge allows cloudfront to run lambda function at CloudFront edge locations to modify traffic between the viewer and edge location and edge locations and origins.
- Not the full feature-set of Lambda: only Node.js and Python as run times. No VPC based resources. Lambda Layers not supported. Different limits than Lambda.
- You can run the Lambda@Edge functions at 4 points: 1. Viewer request 2. Origin request 3. Origin response 4. Viewer response

### Lambda@Edge Use Cases:
- A/B Testing (Viewer Request)
- Migration between S3 Origins (Origin Request)
- Different Objects delivered based on Device (Origin Request)
- Content by Country (Origin Request)

## AWS Global Accelerator
AWS Global Accelerator is designed to improve global network performance by offering entry point onto the global AWS transit network as close to customers as possible using Anycast IP addresses
- Designed to optimize the flow of data from user to AWS infrastructure
- Reduce number of "hops"
- When to use CloudFront VS Global Accelerator? 
-- CloudFront is focused on improving content delivery to end-users via Edge Caching. Question mentions caching? Prolly CloudFront
-- Global Accelerator is focused on optimizing traffic routing to your applications -- by entering the network closer to the customer. Question mentions TCP/UDP? Prolly Global Accelerator
Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover.

### Global Accelerator Resource: https://aws.amazon.com/global-accelerator/faqs/


# ADVANCED VPC Networking
## VPC Flow Logs
VPC Flow logs is a feature allowing the monitoring of traffic flow to and from interfaces within a VPC
- VPC Flow logs can be added at a VPC, Subnet or Interface level.
- Flow Logs DON'T monitor packet contents ... that requires a packet sniffer.
- Flow Logs can be stored on S3 or CloudWatch Logs
NOTE: VPC flow logs ONLY CAPTURE METADATA, NOT CONTENTS

Flow Logs can monitor at 3 levels: 1. VPC 2. Subnet 3. ENIs directly. And these logs capture from capture point and down (so if VPC flow log, it also captures Subnet and ENIs)
EXAM:  - Flow Logs NOT real time
- Log Destinations: S3 or CloudWatch Logs
-- Athena can query the logs in S3
- Flow Logs can capture ACCEPTED, REJECTED, or ALL METADATA

## Egress-Only Internet gateway
Egress-Only internet gateways allow OUTBOUND (and response) only access to the public AWS services and Public Internet for IPv6 enabled instances or other VPC based services
- TL;DR Egress-Only is OUTBOUND-ONLY for IPv6

## VPC Endpoints - Gateway
- Gateway endpoints are a type of VPC endpoint which allow private access to public svc's S3 and DynamoDB WITHOUT using PUBLIC addressing. (normally S3 and DynamoDB are public)
- Gateway endpoints add 'prefix lists' to route table, allowing the VPC router to direct traffic flow to the public services via the gateway endpoint.
-- Gateway Endpoint => 1 per service, per region
-- REGION RESILIENT: Highly Available across all AZs in a region by default
- Endpoint Policy can control what it can access (like certain S3 buckets)
- CANNOT access cross-region services

### VPC Endpoints uses
- Private VPC that needs private access to S3/DynamoDB
- Preventing Leaky Buckets: S3 buckets can be set to private only by allowing access ONLY from a gateway endpoint

## VPC Endpoints - Interface
Interface endpoints are used to allow private IP addressing to access public AWS services.
- DynamoDB is handled by gateway endpoints - other supported services are handled by interface endpoints. S3 now supported by interface endpoints
- Added to specific subnets, an ENI. Not Highly Available
-- For HA, you need an endpoint in each subnet in each AZ used in VPC
EXAM - TCP and IPv4 ONLY
- uses PrivateLink: allows AWS or 3rd party svc's to be injected into your vpc and be given network interfaces
- Apps can access Interface Endpoints via Regional DNS, Zonal DNS, or Private DNS (that overrives default DNS)
-- Private DNS associates a private R53 hosted zone to the VPC changing the default svc DNS to resolve to the interface endpoint IP

## DEMO - VPC Endpoints - Interface - PART1 / PART2 / PART3 - Skipping for now

## VPC Peering
VPC peering is a software defined and logical networking connection between two [AND ONLY TWO] VPC's
- VPCs in the same or different accounts and the same or different regions.
EXAM - TWO VPCs connected only
- If VPCs in same region, SGs can reference peer SGs
EXAM - VPC Peering does NOT support transitive peering (AKA A -> B peering, then B -> C peering... C is not auto peered to A)
- With peering, you're basically setting up gateways in each VPC which requires Routing Configuration on EACH side. SGs/NACLs must be set up to allow traffic through
EXAM - 4 VPCs... how many peering connection to connect all? 6
EXAM - IP ranges of VPC Peers CANNOT OVERLAP

## DEMO - VPC Peering - Skipping for now


# HYBRID ENVIRONMENTS AND MIGRATION
## Border Gateway Protocol 101
Introduction to the Border Gateway Protocol (BGP) which is a routing protocol used by some AWS services such as Direct Connect and Dynamic Site to Site VPNs.
- BGP made of AS (autonomous systems). Routers controlls by one entity; a network in BGP. Your whole company's network system is a 'black box' abstraction, BGP only cares about ingress/egress
-- Autonomous System Numbers (ASNs) are unique and allocated by IANA (0-65535), 64512-65534 are PRIVATE
- BGP operates over tcp/179 -- reliable
- BGP not automatic, peering is manually configured
- BGP is a PATH-VECTOR protocol; it exchanges the best path to a destination between peers...best path (AKA shortest path) is called ASPATH
- iBGP (internal routing within an AS) - most common, eBGP (external routing between ASs)
- ASPATH prepending: A way to make a shorter but slower path look worse than a longer but faster path (by just addking more ASs to the path route)

## IPSec VPN Fundamentals
IPsec VPN negotiation occurs in two phases:
1. In Phase 1, participants establish a secure channel in which to negotiate the IPsec security association (SA)
2. In Phase 2, participants negotiate the IPsec SA for authenticating traffic that will flow through the tunnel and use IPSec Keys to exchange 'interesting traffic'
- sets up secure tunnels across insecure networks
- provides authentication and encryption; a secure connection over an insecure network
- asymmetric encryption used to establish symmetric encryption

### IPSec - Two Phases
IKE Phase 1: Internet Key Exchange. IKE v1 and IKE v2 (v2 is newer)
- authentication with asummetric encryption to agree on and create a shared symmetric key
- "Diffie-Helman Private Key"/DH Key created by both sides in Phase 1.. this is what actually creates the symmetrical key for phase 2
IKE Phase 2: Getting VPN up and running 
- built on phase one using the symmetric key created in phase 1
- Phase 2 can be town down and rebuilt when needed, phase 1 can stay

### IPSec - VPN Types (2)
1. Policy Based. Rule sets match traffic. More difficult to configure, but more flexible than Route Based
2. Route Based. Target matching based on prefix
- difference being how they match 'interesting traffic'

## AWS Site-to-Site VPN. AWS <-> on-premises VPN
AWS Site-to-Site VPN is a hardware VPN solution which creates a highly available IPSEC VPN between an AWS VPN and external network such as on-premises traditional networks. 
- Quickest way to create network link between AWS and non-AWS (less than an hour)
- VPNs are quick to setup vs direct connect, don't offer the same high performance, but do encrypt data in transit. 
- Runs over the public internet (unlessw otherwise specificed)
EXAM - Highly Available

### AWS Site-to-Site VPN - Components
- VPC. VPC connected to external network via VPN
- Virtual Private Gateway (VGW). The target one or more route tables
- Customer Gateway (CGW): Logical piece of config and the thing that the config represents
- VPN Connection

### Static VS Dynamic VPN
- Static uses BGP, Border Gateway Protocol (customer router must support this). Static networking config, static routes
- Dynamic VPN: Need Direct-Connect? Dynamic. Multiple VPN connections for Higher Avail and traffic distribution
- "Route Propagation": if enabled, means routes are added to RTs automatically

EXAM - AWS speed limitation of VPNs 1.25Gbps
EXAM - Latency is inconsistent as it is through Public Internet. If need low latency, maybe Direct Connect

## Direct Connect (DX) Concepts
AWS Direct Connect links your internal network to an AWS Direct Connect location over a standard Ethernet fiber-optic cable. One end of the cable is connected to your router, the other to an AWS Direct Connect router. With this connection, you can create virtual interfaces directly to public AWS services (for example, to Amazon S3) or to Amazon VPC, bypassing internet service providers in your network path. 

An AWS Direct Connect location provides access to AWS in the Region with which it is associated. You can use a single connection in a public Region or AWS GovCloud (US) to access public AWS services in all other public Regions.

Direct connect = physical connection. Between business premises <-> DX Location <-> AWS Region
- 1, 10, or 100GBps
- when you order DC, you're really ordering a Port Allocation at the DX Location
- Cannot access internet
- DX Location is NOT owned by AWS (just has AWS space/equipment in it - called a "cage". And you'll have customer or comms partner Cage -- need to connect AWS / Customer router)
- Low latency, high speeds. No resilience (at it's literally 1 cable)
- requires VIFs (virtual interfaces) for the networking over DX to AWS

## Direct Connect (DX) Resilience
Initially, DX has NO resilience as it only has 1 cable. For resilience, you need to lay multiple DX connections / provision multiple ports. Lots of single points of failure by default.
- Best practice... multiple DX Connect Locations... Multiple Customer Premises. Two ports in each DX location, dual routers at customer locations (2)
- At DX Connect Location... Multiple AWS routers, multiple customer routers

## Direct Connect (DX) - Public VIF + VPN (Encryption)
How to use these things to achieve end-to-end encrypted access to private VPC networks across Direct Connect
- Neither public or private VIFS offer any form of encryption.
- Public VIFs+IPSec VPN is a way to provide access to private VPC resources, using an encrypted IPSEC tunnel for transit.

## Transit Gateway
The AWS Transit gateway is a network gateway which can be used to significantly simplify networking between VPC's, VPN and Direct Connect.
- It can be used to peer VPCs in the same account, different account, same or different region and SUPPORTS TRANSITIVE ROUTING between networks.
- Single network object that is highly available and scalable
- create "attachements" to other network types: valid attachments -> VPC, site-to-site VPN, DX Gateway
- Can use "peering attachments" to ve cross-region/cross-account (cross acct = AWS Ram)
- Supports transitive routing (which is basically why it exists, since VPCs don't which causes too much complexity)
EXAM - REMEMBER: TRANSIT gateway supports TRANSITIVE ROUTING (which VPC peering can't do) -- this simplifies vpc-to-vpc

## Storage Gateways - Volume, Tape, File
## Storage Gateway - Volume
Storage gateway is a product which integrates local infrastructure and AWS storage such as S3, EBS Snapshots and Glacier.

### Storage Gateway - Volume Stored Mode
EXAM - ALL stored locally, which means low latency access
- Data copied into S3 with EBS Snapshots
EXAM - Use: Full disk backups of servers
EXAM - Use: Assists with disaster recovery; created EBS volumes in AWS
EXAM - VSM does NOT improve or extend data center capacity
- Something something iSCSI

### Storage Gateway - Volume Cached Mode
Instead of having a local storage volume on prem, you have a local cache. Actual data stored in S3, and does EBS Snapshot backups
EXAM - Use Case: To extend your data center (since data is stored in S3 and only cached locally)

## Storage Gateway - Tape (VTL) - Virtual Tape Library
Storage gateway in VTL mode allows the product to replace a tape based backup solution with one which uses S3 and Glacier rather than physical tape media
- Max size of virtual tape is 5 TiB, same as size of S3 bucket
- Pretends to be an iSCSI tape library, changer, and drive. S3 serves as Virtual Tape Library, Glacier is the Virtual Tape Shelf
- Uses: Backup platform migrations or data center extensions

## Storage Gateway - File
File gateway bridges local file storage over NFS (linux)/SMB(windows) with S3 Storage
- It supports multi site, maintains storage structure, integrates with other AWS products and supports S3 object lifecycle Management
- Files stored this way (to mount point) are visible as objects in an S3 bucket
- Read/Write caching ensure LAN-like performance
- 1 file share + 1 S3 = 1 bucket share. Can have 10 Bucket Shares per file gateway
- Primary data stored in S3
- File Gateway doesn't support Object Locking--use Read Only Mode on other shares or tightly control file access

## Snowball / Edge / Snowmobile [NEW VERSION COMING SOON]
Snowball, Snowball Edge and Snowmobile are three parts of the same product family designed to allow the physical transfer of data between business locations and AWS.

### Snowball
- Order physical device from AWS. Encrypted using KMS. 50TB or 80TB. 
EXAM - Range of data to use it for 10TB - 10PB
EXAM - Can order multiple devices / to multiple premises
EXAM - STORAGE ONLY, no compute
### Snowball Edge
EXAM - Has both storage and compute
- Larger capacity VS snowball
- Faster networking with Edge
- 3 types of Edge: 1. Storage Optimized 2. Compute Optimized 3. Compute Optimized with GPU
EXAM - Ideal for remote sites or where data processing on ingestion is needed
### Snowmobile
Portable data center within a shipping container on a truck (mobile, duh)
- Ideal for single location with 10PB+ is required
- 10PB - 100PB
- NOT for multi-site (unless HUGE) or sub 10PB

## Directory Service
What are directories? Identity and asset info storage. Stores objects with structure (inverse tree). 
- Multiple trees grouped into a FOREST
- Commonly used with Windows environments
- Users, devices, groups, servers, file shares -- things that can be objects in a directory

 AWS Directory Service is an AWS managed implementation of a directory that runs in a VPC
- High availability, deploy into multiple AZs
- Amazon Workspaces NEEDS the AWS Directory Svc to function
- can be isolated or integrated with an on-premise system

### Directory Service - Three Modes
1. Simple AD - An implementation of Samba 4 (compatibility with basics AD functions)
- cheapest / simplest mode
- 500 - 5000 users
- Simple AD is based off of Samba 4 (an open-source version of Microsoft AD)
- Simple AD designed to be used in isolation
2. AWS Managed Microsoft AD - An actual Microsoft AD DS Implementation
- AWS presense while having an existing on-premises directory
- Primary location is at AWS. TRUST relationships created between AWS and on-premmise
3. AD Connector which proxies requests back to an on-premises directory
- An entity made to integrate with AWS services. It has NO local functionality - great for hosting Workspaces
- If private connectivity fails, AD fails and AWS-side related svd would be interrupted

### When to pick one of the 3 ADs?
Simple AD -  The default. Simple reqs. A directory in AWS
Microsoft AD - Apps in AWS which req MS AD, or you need to TRUST AWS AD Directory Service
AD Connector - To use AWS p&s that require a directory without actually housing one on AWS side (as you have it on prem), use AD connector

## DataSync
AWS DataSync is a product which can orchestrate the movement of large scale data (amounts or files) from on-premises NAS/SAN into AWS or vice-versa
- Data transfer service To and FROM AWS
- Designed to work at HUGE scale
- Keeps metadata (permissions/timestamps)
- Built-in data validation
- Scalable: 10Gbps/agent (~100TB/day)
- FEATURES EVERYWHERE... Bandwidth limiters, incremental/scheduled xfer options, compression and encryption, auto recovery from transit errors, svc integration with S3 EFS FSx, bidirectional transfer
EXAM - The DataSync agent needs to be intalled LOCALLY on-prem
EXAM - communicates via NFS/SMB w/ on-prem storage

### DataSync Components
- tasks: a "job"
- agent: the software living on-prem that reads/writes to on-prem data stores using NFS/SMB
- location: every task has a TO and FROM location

## FSx for Windows Servers
FSx for Windows Servers provides a native windows file system as a service which can be used within AWS, or from on-premises environments via VPN or Direct Connect
- FSx is an advanced shared file system accessible over SMB, and integrates with Active Directory (either managed, or self-hosted).
- It provides advanced features such as VSS, Data de-duplication, backups, encryption at rest and forced encryption in transit.
- Integrats with Directory Service or Self-Managed Active Directory
- Single or Multi-AZ within a VPC
- on-demand/scheduled backups
- accessible using VPC, peering, VPN, Direct Connect
- FSx is dedicated to Windows Environments, the similar EFS is for Linux/Unix
- File level versioning; support volume shadow copies; file-level restores
EXAM - Key words to look for: VSS (user driven restores), native file system over SMB (SMB=windows), uses Windows permissions model, supports DFS (distributed file system), integrates with Directory Service and YOUR OWN directory

## FSx For Lustre
FSx for Lustre is a managed file system which uses the FSx product designed for high performance computing
- It delivers extreme performance for scenarios such as BIG DATA, MACHINE LEARNING and FINANCIAL MODELING
-- FSx for Lustre is a managed Lustre high compute system. Linux clients (POSIX)
- Two deploment types: Persistent or Scratch
-- Scratch: highliy optimized for short-term. No replication and fast. not HA
-- Persistent: Longer term, high avail in one AZ, self-healing
EXAM - If Lustre, POSIX mentioned... FSx for Lustre, ML/big data/fin-modeling

## AWS Transfer Family
Managed file transfer service using these protocols: SFTP, FTP, FTP Transfer, AS2
EXAM - supports transferring data over the following protocols: SFTP, FTPS, and FTP transfer
- Managed File Transfer Workflows (MFTW) - serverless file workflow engine (for tagging and stuff)
- Using FTP? Since not secure, you can only use FTP protocol within VPC (not public)

# SECURITY, DEPLOYMENT & OPERATIONS
## AWS Secrets Manager
AWS Secrets manager is a product which can manage secrets within AWS. There is some overlap between it and the SSM Parameter Store - but Secrets manager is specialised for secrets.
EXAM - Secrets manager is capable of automatic CREDENTIAL ROTATION using LAMBDA.
- For supported services it can even adjust the credentials of the service itself.
- Secrets encrypted using KMS
- Integrates with RDS

EXAM Secrets Manager VS Parameter Store? SM is designed for SECRETS (passwords, API Keys), SM auto rotation of secrets with Lambda, 
- Parameter store stores strongs, secure strings--for config info

## Application Layer (L7) Firewall
L7 firewalls are capable of inspecting, filtering and even adjusting data up to Layer 7 of the OSI model. They have visibility of the data inside a L7 connection. For HTTP this means content, headers, DNS names .. for SMTP this would mean visibility of email metadata and for plaintext emails the contents.
- WAF is an L7 Firewall

## Web Application Firewall (WAF), WEBACLs, Rule Groups and Rules
AWS WAF is an L7 web application firewall that helps protect your web applications or APIs against common web exploits and bots that may affect availability, compromise security, or consume excessive resources.
- cross-scripting attacks, SQL Injection, ALLOW/DENY lists, XSS, HTTP Flood, IP Reputation, bots
- Actual unit of configuration within WAF is the WEB Access Control List (ACL)
- Web ACLs use Rules/Rule Groups
-- Rule components: Type, Statement, Action
--- Rule types: Regular or Rate-based
--- Statement: WHAT to match/count... even down to matching body (first 8192 bytes ONLY)
--- Action: Allow, Block, Count, custom respon, label

## AWS Shield
For DDoS protection. AWS Shield provides always-on detection and automatic inline mitigations that minimize application downtime and latency, so there is no need to engage AWS Support to benefit from DDoS protection. 

You can use AWS WAF web access control lists (web ACLs) to help minimize the effects of a Distributed Denial of Service (DDoS) attack. For additional protection against DDoS attacks, AWS also provides AWS Shield Standard and AWS Shield Advanced. AWS Shield Standard is automatically included at no extra cost beyond what you already pay for AWS WAF and your other AWS services.
- Shield Standard is free. Automatically provided with CloudFront and R53
- AWS Shield Advanced (not free) provides expanded DDoS attack protection for your Amazon EC2 instances, Elastic Load Balancing load balancers, CloudFront distributions, Route 53 hosted zones, and AWS Global Accelerator standard accelerators.
-- Advanced requires manual configuration, explicit enabling. Has const protection incurred from attacks
--- Advanced Shield USES WAF for L7 DDoS protection

## CloudHSM
CloudHSM - an AWS provided Hardware Security Module products. Similar to KMS... creates/manages/secures crypto keys
- CloudHSM is required to achieve COMPLIANCE with certain SECURITY STANDARDS such as FIPS 140-2 Level 3

### When to use KMS over CloudHSM
- KMS is a SHARED service and AWS has certain level of access to it. KMS is mostly Level 2 FIPS
EXAM - CloudHSM is a SINGLE TENANT HSM (hardware security module). CloudHSM is aws provisioned but fully customer managed. CloudHSM is LEVEL 3 FIPS compliant. 
* EXAM - Need CloudHSM if need access by industry standard APIs (not AWS api's); JCE, PKCS#11, CryptoNG
EXAM - Need to enable Transparent Data Encryption (TDE) for Oracle DBs? CloudHSM
EXAM - Protect private keys for an issuing CA (cert authority)

## AWS Config 
AWS Config is a service which records the configuration of resources over time (configuration items) into configuration histories.
- All the information is stored regionally in an S3 config bucket.
- AWS Config is capable of checking for compliance .. and generating notifications and events based on compliance.
- Terms: config item, config history, config rules, config stream, config notifications (via eventbridge or sns)
### AWS Config - Two main jobs
1. Record configuration changes over time on resources
2. Auditing of changes, compliance with standards
NOTE: AWS Config DOES NOT prevent changes from happening; no protectoin, just watches

## Amazon Macie
Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS.
- protect personally identifiable information of stuff in S3 buckets
- Can have Managed (built in, ML\patterns) or Custom Data Identifiers (regex based)
- checks s3 buckets

## Amazon Inspector
Inspect for COMPLIANCE. Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS. Amazon Inspector automatically assesses applications for exposure, vulnerabilities, and deviations from best practices
- checks EC2 instances and the instance OS, and containers
- creates security reports ordered by priority
- Does Network Reachability (with or without Agent--agent means more info)
- Packages: Host Assessments, Common Vulnerabilities/Exposures (CVE), Center for Internet Security (CIS) Benchmarks, Security Best Practices for Amazon Inspector

## Amazon Guardduty
Guard Duty is an automatic threat detection service which reviews data from supported services and attempts to identify any events outside of the 'norm' for a given AWS account or Accounts. 
- CONTINUOUS SECURITY MONITORING SERVICE
- Ingests Logs and Events

### Inspector VS GuardDuty: If we try to describe it in a chronological fashion, you can have Inspector set up at the start when you deploy your applications, and then GuardDuty immediately after that in order to receive alerts on potential threats. Amazon Inspector provides you with security assessments of your applications’ settings and configurations while Amazon GuardDuty helps with analysing the entirety of your AWS accounts for potential threats.


# Infrastructure as Code (CloudFormation)
## CloudFormation Physical & Logical Resources
- CloudFormation defines logical resources within TEMPLATES (using YAML or JSON). 
-- The logical resource defines the WHAT, and leaves the HOW up to the CFN product. 
- A CFN stack creates a physical resource for every logical resource - updating or deleting them as a template changes.
- TEMPLATES create STACKS. A stack creates/modifies/deletes physical resources based on the logical resources in the template

## CloudFormation - Template and Pseudo Parameters
Template and Pseudo Parameters are two methods to provide INPUT to a template, which can influence what resources are provisioned, and the configuration of those resources.
- Pseudo parameters. These params are injected and made available by AWS. Template params are user made with YAML/JSON

## CloudFormation Intrinsic Functions
AWS CloudFormation provides several built-in functions that help you manage your stacks. Use intrinsic functions in your templates to assign values to properties that are not available until runtime.
- !Ref & Fn::GetAtt. Ref is primary value, attributes are secondaries. !GetAtt
- Fn::Join & Fn::Split
- Fn::GetAZs & Fn::Select
- Conditions Fn::IF,And,Equals,Not,Or
- Fn::Base64 & Fn::Sub. Base64 outputs base64 encoded text
- Fn::Cidr. Creating a cider range based on parent VPC CIDR range

## CloudFormation Mappings
The optional Mappings section matches a key to a corresponding set of named values. For example, if you want to set values based on a region, you can create a mapping that uses the region name as a key and contains the values you want to specify for each specific region
- Use the Fn::FindInMap intrinsic function to retrieve values in a map.
- Mapping -> key:value
- Mappings Improves Template Portability

## CloudFormation Outputs
The optional Outputs section declares output values that you can import into other stacks (to create cross-stack references), return in response (to describe stack calls), or view on the AWS CloudFormation console. 
- For example, you can output the S3 bucket name for a stack to make the bucket easier to find.
- Output section is optional
- Visible as outputs from CLI, console UI, parent stack, can be exported to other stacks (cross-stack references)
- Components: Description and Value

## DEMO - Template v2 - Portable - Skipping for now

## CloudFormation Conditions
The optional Conditions section contains statements that define the circumstances under which entities are created or configured. You might use conditions when you want to reuse a template that can create resources in different contexts, such as a test environment versus a production environment.
- Conditions evaluated to True or False and are processed BEFORE resources are created
- In your template, you can add an EnvironmentType input parameter, which accepts either prod or test as inputs. 
- Conditions are evaluated based on predefined pseudo parameters or input parameter values that you specify when you create or update a stack. 
- Within each condition, you can reference another condition, a parameter value, or a mapping. 
- Components: Parameter, Conditions, Resources

## CloudFormation DependsOn
With the DependsOn attribute you can specify that the creation of a specific resource follows another. When you add a DependsOn attribute to a resource, that resource is created only after the creation of the resource specified in theDependsOn attribute.

## CloudFormation Wait Conditions & cfn-signal
CreationPolicy, WaitConditions and cfn-signal can all be used together to prevent the status if a resource from reaching create complete until AWS CloudFormation receives a specified number of success signals or the timeout period is exceeded.
- The cfn-signal helper script signals AWS CloudFormation to indicate whether Amazon EC2 instances have been successfully created or updated.
- After you define all your conditions, you can associate them with resources and resource properties in the Resources and Outputs sections of a template
- tl;dr resource create paused until expected signal(s) received


## CloudFormation Nested Stacks
Nested stacks allow for a hierarchy of related templates to be combined to form a single product
- A ROOT STACK can contain and create nested stacks .. each of which can be passed parameters and provide back outputs.
- Nested stacks should be used when the resources being provisioned ****share a lifecycle**** and are related.
- Single stacks have resource limits of 500, use nested to overcome this
- Stacks are isolated; can't easily reference each other. Nested stacked can reference outputs from parents, however
- Nested stacks for modular-type template re-use. Cross-reference stacks are for resource re-use

## CloudFormation CloudFormation Cross-Stack References
- Nested stacks for modular-type template re-use. CloudFormation Cross-Stack References are for resource re-use
-- Outputs in one stack reference logical resources or attributes in that stack
-- Outputs can be exported, and then using the !ImportValue intrinsic function, referenced from another stack.
--- Exports must be UNIQUELY NAMED in region

## CloudFormation Stack Sets
StackSets are a feature of CloudFormation allowing infrastructure to be deployed and managed across MULTIPLE REGIONS and MULTIPLE ACCOUNTS from a single location. 
- Additionally it adds a dynamic architecture - allowing automatic operations based on accounts being added or removed from the scope of a StackSet.
- StackSets are containers in an admin account which contain stack instances which REFERENCE stacks
-- Stack instances and stacks are in TARGET ACCOUNTS
- Each stack is 1 region 1 account

### CFN StackSet Terms
- Concurrent Accounts. How many concurrent stacks are created together. Eg. If you have 10 stacks to make, you set concurrnet acct to 2... you'll create stacks in 5 pairs.
- Failure Tolerance. Amount of individual deployments that can fail before StackSet is considered failed
- Retain Stacks. Delete stacks FROM YOUR stack set, but save them so they continue to RUN INDEPENDENTLY of your stack set by choosing the Retain Stacks option. You can then manage retained stacks outside of your stack set in AWS CloudFormation. "cut it loose"

## CloudFormation Deletion Policy
With the DeletionPolicy attribute you can preserve or (in some cases) backup a resource when its stack is deleted. You specify a DeletionPolicy attribute for each resource that you want to control. If a resource has no DeletionPolicy attribute, AWS CloudFormation deletes the resource by default.
- cut the resource loose from the Stack b/c resource deletion can sometimes cause data loss
- Deletion Policies: Delete, Retain, or Snapshot (if supported)
-- Snapshots continue past stack lifetime

## CloudFormation Stack Roles
Stack roles allow an IAM role to be passed into the stack via PassRole
- A stack uses this role, rather than the identity interacting with the stack to create, update and delete AWS resources.
- It allows ROLE SEPARATION and is a powerful security feature

## CloudFormation Init (CFN-INIT)
CloudFormationInit and cfn-init are tools which allow a desired state configuration management system to be implemented within CloudFormation
- Another way to provide config info into EC2 instance
- Use the AWS::CloudFormation::Init type to include metadata on an Amazon EC2 instance for the cfn-init helper script. If your template calls the cfn-init script, the script looks for resource metadata rooted in the AWS::CloudFormation::Init metadata key. cfn-init supports all metadata types for Linux systems & It supports some metadata types for Windows
- AWS::CloudFormation::Init which is procedural (you tell it how to bootstrap itself)
-... or CFN-INIT which is where you tell the system WHAT you want and it builds it out (this one is idempotent). It is run ONCE as a part of bootstrapping; if CloudFormation::Init is updated, cfn-init isn't re-run (which is where cfn-hup comes in, see below)

## CloudFormation cfn-hup
The cfn-hup helper is a daemon that detects changes in resource metadata and runs user-specified actions when a change is detected (Ie. re-running cfn-init). This allows you to make configuration updates on your running Amazon EC2 instances through the UpdateStack API action.

## CloudFormation ChangeSets - CFN stack update dry runs (like Find/Replace dry runs in WordPress)
When you need to update a stack, understanding how your changes will affect running resources before you implement them can help you update stacks with confidence. Change sets allow you to preview how proposed changes to a stack might impact your running resources, for example, whether your changes will delete or replace any critical resources, AWS CloudFormation makes the changes to your stack only when you decide to execute the change set, allowing you to decide whether to proceed with your proposed changes or explore other changes by creating another change set.

## CloudFormation Custom Resources
Custom resources enable you to write custom provisioning logic in templates that AWS CloudFormation runs anytime you create, update (if you changed the custom resource), or delete stacks
- AKA Custom Resources let CFN integrate with anything it doesn't yet, or doesn't natively support

# NOSQL Databases & DynamoDB
## DynamoDB - Architecture
DynamoDB is a NoSQL fully managed Database-as-a-Service (DBaaS) product available within AWS. This is the traditional serverless DB route in AWS
- uses Key/Value &/or Document data. "Wide column DB"
- no self-managed servers or infrastructure
- Highly resilient and can be optionally Globally resilient
- Single digit millisecond speeds -- SSD based
- manual or auto scaling or on-demand (set and forget)
- RCU - read capacity units, WCU - write capacity units

### DynamoDB - Tables
- Table is a grouping of ITEMS with the same PRIMARY key. Item is like a row in a traditional DB
-- item max size 400KB. item can have all, none, or some of the attibutes/columns in an item(row)
- Table has two primary keys to pick from: 
1. Partition key. made up of just a partition key
2. Composite primary key. made up of a partition key and a sort key

### DynamoDB - Backups
Two types of backups:
1. On-demand backup. Full copy of table retained until removed
2. Point-in-time Recovery. Not enabled by default. 35 day window to restore to 1 second granularity, PER table restores
EXAM - NoSQL mentioned? DynamoDB
EXAM - Key/Value DB mentioned? DynamoDB
EXAM - Relational Data/DB? NOT DynamoDB

## DynamoDB - Operations, Consistency and Performance
Key elements of READS and WRITES to DynamoDB and step through how the QUERY AND SCAN operations work.
- When you create a DynamoDB table, you choose from two capacity modes: on-demand and provisioned
-- On-Demand: If you need low admin overhead or traffic is unknown/unpredictable. Price per million R or W units. More expensive
-- Provisioned: RCU/WCU capacity set per table basis
- 1 RCU = 1 x 4KB read ops per second, 1 WCU is 1 x 1KB write ops per second
-- Every table has RCU/WCU Burst Pool (300 seconds)

### DynamoDB - Query and Scan
- Query. One way to retrieve data. Accepts a single PK value and optionally an SK or range.
- Scan. Least efficient but most flexible way to get data in DynamoDB. Scans through table item-by-item - consumed capacity is all items read/scanned

### DynamoDB - Consistency model in DynamoDB
In DynamoDB, each piece of data is replicated into different AZs known as Storage Nodes, and one is the Leader storage node. Leader storage nodes receive the reads/writes and write updates are replicated by leader to other nodes
- Eventually Consistent Reads. You are not guaranteed to see the most updated data if you're send to a node that hasn't received the replicated new data yet. Cheaper option
- Strongly Consistent Reads. Always reads from Leader node to guarantee data up to date
NOT: Not every app can tolerate eventual consistency (some things MUST be accurate)

### Calculate WCU
Problem: Need to store 10 items per second, 2.5K average size per item
1. Round up average size to nearest whole number. 2.5K -> 3
2. Multiply item size x # items/sec. 3 x 10 = 30
= 30 WCU required

### Calculate RCU
Problem: Need to retrieve 10 items per second, 2.5K average size per item
1. Divide Item size / 4 then round up. 2.5K/4K rounded up is 1.
2. Multiply item size x # items/sec. 1 x 10 = 10
= 10 RCU required for Strongly Consistent. Eventual is 50% cost, so 5RCU required for Eventually Consistent Reads

## DynamoDB - Local and Global Secondary Indexes
Local Secondary Indexes (LSI) and Global Secondary Indexes (GSI) allow for an alternative presentation of data stored in a base table.
- Indexes improve the efficiency of operations in DynamoDB
- LSI allow for alternative Sort Key's (SAME PK) whereas with GSIs you can use alternative PK and SK.
-- LSIs only created at Table creation
- GSIs can be created any time. 20 limit of GSIs per base table. Uses alternate PK and SK. GSIs are ALWAYS eventually consistent, so to use GSI your tables needs to be able to cope with eventualy consistency
NOTE: Use GSI as default and LSI only when STRONG consistency index is required

## DynamoDB - Streams & Lambda Triggers
DynamoDB Streams are a 24 hour rolling window of time ordered list of changes to ITEMS in a DynamoDB table
- Streams have to be enabled on a per table basis , and have 4 view types:
1. KEYS_ONLY. Only keys of item that changed
2. NEW_IMAGE. New item after change
3. OLD_IMAGE. Old item before change
4. NEW_AND_OLD_IMAGES. Both old and new states
- Lambda can be integrated to provide trigger functionality - invoking when new entries are added on the stream.

### DDB - Triggers
- Streams are the foundation of Triggers
- Triggers allow fo actions to take place in the event of data change, use can use Lambda to perform a compute action in response

## DynamoDB - Global Tables
DynamoDB Global Tables provides multi-master global replication of DynamoDB tables which can be used for performance, High Avail or Disaster Recovery/Biz Continuity reasons.
- GLOBAL table and then multiple regions with tables becoming REPLICA tables
- LAST WRITER WINS is used for conflict resolution; the most recent Write is what is replicated to other tables
- Global app must tolerate eventual consistency. However, region reads in the same region as writes are strongly consistent 

## DynamoDB - Accelerator (DAX)
DynamoDB Accelerator (DAX) is an in-memory cache designed specifically for DynamoDB. It should be your default choice for any DynamoDB caching related questions.
- Global table has sub-second replication between table replicas
- DAX is less overhead than normal caching
- Can scale up or out (bigger or more DAX instances)
- Supports "write-through"
- Good for read-heavy work loads

## DynamoDB - TTL
Amazon DynamoDB Time to Live (TTL) allows you to define a per-item timestamp to determine when an item is no longer needed. 
- Shortly after the date and time of the specified timestamp, DynamoDB deletes the item from your table without consuming any write throughput. 
- TTL is provided at no extra cost as a means to reduce stored data volumes by retaining only the items that remain current for your workload’s needs.

## Amazon Athena
Amazon Athena is serverless querying service which allows for ad-hoc questions where billing is based on the amount of data consumed.
- Athena is an underrated service capable of working with unstructured, semi-structured or structured data.
- tl;dr take data stored in S3 and perform ad-hoc queries on that data. Pay only for the data consumed while running query (and s3 storage)
- Uses process called "schema-on-read", a table-like translation --- original data on S3 never changed
EXAM - Best option for querying AWS logs; VPC flow logs, CloudTrail, ELB Logs, cost reports, Glue, Web Server, etc
- Athena Federated Query -- a way for Athena to query outside S3
- Athena = ad-hoc. Redshift is not ad-hoc

## Elasticache
Elasticache is a managed in-memory cache which provides a managed implementation of the redis or memcacheD engines. Useful for READ-HEAVY workloads that demand low latency, scaling reads in a cost effective way and allowing for externally hosted user session state
- in-memory database for high performance
- Two engines: 
1. Redis. supports advanced data structures. Multi-AZ. Backup and restore.
2. Memcached. Supports simple data structures. No backups. Multi-threaded
- reduces database workloads
EXAM - Can store Session Data (for stateless servers)
EXAM - Elasticash requires application code changes to work

## Redshift Architecture
Redshift is a column based, petabyte-scale, data warehousing product within AWS
- It's designed for OLAP products within AWS/on-premises to add data to for long term processing, aggregation and trending. (Not OLTP which is row/transaction; inserts/modifies/deletes)
- Redshift Spectrum. Direct Query S3 without having to load it into redshift in advance
- Federated Query. Query data in remote data sources
- Redshift has Enhanced VPC Routing; VPC networking for advanced networking control
- AZ specific

## Redshift DR and Resilience
- RedShift only exists in 1 AZ. There are a number of recovery features:
- snapshots. Either automatic (1-35 day retention) or manual (no retention period). Since data is backed up to S3, you have S3 protections against failure
-- snapshots can be sent to other regions for disaster recovery with a separate configurable retention period
- SERVER based

# MACHINE LEARNING
## Amazon Comprehend 
Amazon Comprehend is a natural-language processing (NLP) service that uses machine learning to uncover valuable insights and connections in text.
- input document and it parses and develops insights (like name, addresses, PII, phrases, common elements, sentiment)
- pre-trained or custom models
- realtime for small workloads, async for larger workloads
- confidence 0.0 - 1.0 (1 being wholly confident)

## Amazon Kendra
Amazon Kendra is an intelligent search service powered by machine learning (ML).
- designed to mimic interacting with a human expert
- suppports wide range of question types: factoid, descriptive, keyword
- Kendra is a backend service that you'd API-integrate with your app for search functionality
### Kendra Concepts
- Index. Searchable data 
- Data source. Where your data lives; S3, Google Workspace, RDS, Salesforce, FSx, etc etc
- Documents. Structured and unstructured indexable items

## Amazon Lex
Amazon Lex is a fully managed artificial intelligence (AI) service with advanced natural language models to design, build, test, and deploy CONVERSATIONAL interfaces in applications.
- interactive chat bots
- backend service that you'll use to add capabilities to your application
- POWERS THE ALEXA SERVICE
- Automatic Speesh Recognition (ASR); sppech-to-text, Natural Language Understanding (NLU); intent, 
- Chatbots, Voice Assistance, Q&A Bots, Phone bots

## Amazon Polly
Amazon Polly is a service that turns text into lifelike speech text to speech TTS), allowing you to create applications that talk, and build entirely new categories of speech-enabled products.
- polly - parroting text to speech. NO TRANSLATION
- two types of TTS.. .standard and neural. Standard concatenates phenomes, neral much more complex but more natural

## Amazon Rekognition
Amazon Rekognition offers pre-trained and customizable computer vision (CV) capabilities to extract information and insights from your IMAGES and VIDEOS.
- deep learning based
- ID objects, people, text, activities, face detection/analysis/comparison, pathing, much more
- Can analyze live video by integrating with kinesis video streams

## Amazon Textract
Amazon Textract is a machine learning (ML) service that automatically extracts text, handwriting, and data from scanned documents. It goes beyond simple optical character recognition (OCR) to identify, understand, and extract data from forms and tables
- input documents = JPG, PNG, PDF, TIFF
- output: extracted text, structure, and analysis
- types of analysis: document, receipts, identity documents
- backend style service that can be intergrated with your apps or with other AWS services

## Amazon Transcribe
Amazon Transcribe is an automatic speech recognition (ASR) service that uses machine learning models to convert audio to text. You can use Amazon Transcribe as a standalone transcription service or to add speech-to-text capabilities to any application.
- input Audio, output Text
- Use Cases: full text indexing to allow searching of audio, create meeting notes, subtitles/captions/transcripts
-- call analytics (sentiment, characteristics, etc)

## Amazon Translate
Amazon Translate is a neural machine translation service that delivers fast, high-quality, affordable, and customizable language translation.
- one word at a time translation and outputs semantic representation or meaning, decorder reads meaning and writes target language
- backend style service that integrates with other services/apps/platforms

## Amazon Forecast
Amazon Forecast is a fully managed service that uses statistical and machine learning algorithms to deliver highly accurate time-series forecasts.
- Predicting retail demand, supply chain, staffing, web traffic. 
- Import historical & related data, understand what's normal, output forecasts and forecast explainability
- backend style service that integrates with your apps or you can use web console, CLI. And APIs, Python SDK

## Amazon Fraud Detecto
Amazon Fraud Detector is a fully managed fraud detection service that automates the detection of potentially fraudulent activities online. These activities include unauthorized transactions and the creation of fake accounts. Amazon Fraud Detector works by using machine learning to analyze your data.
- online fraud, transactional fraud, account takeover (phishing etc)
- backend style service that integrates into your apps

## Amazon SageMaker
Amazon SageMaker is a fully managed machine learning service. With SageMaker, data scientists and developers can quickly and easily build and train machine learning models, and then directly deploy them into a production-ready hosted environment.
- implementation of a fully managed ML service: fetch, clean, prepare, train, eval, deploy, monitr/collect -- the whole ML lifecycle
- SageMager Studio - Dev environment for the ML lifecycle
- SageMaker Domain - olation or groupings / container for a project
- Containers. Docker containers deployed to ML EC2 instances
- Hosting. Can host ML models
- SageMaker has no cost, the resources it creates do

## AWS Local Zones
AWS Local Zones are a type of infrastructure deployment that places compute, storage, database, and other select AWS services close to large population and industry centers.
- physical distance affects latency and performance. AWS Local Zones brings infrastructure physically closer for super low latencies
- Local Zones support DX (direct connect)
- Local Zones have Private networking with their parent region
- Not all products support Local Zones
- HIGHEST PERFORMANCE REQUIRED? Local Zones 
