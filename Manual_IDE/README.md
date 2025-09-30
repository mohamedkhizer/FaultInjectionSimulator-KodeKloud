# AWS Fault Injection Simulator (FIS) Workshop Setup

Welcome to the AWS Fault Injection Simulator (FIS) Workshop! This guide will walk you through the setup process, which includes creating the necessary IAM role, launching an EC2 instance, installing dependencies, and cloning the required GitHub repositories. By the end of this guide, you'll be ready to dive into the workshop and start experimenting with AWS FIS.


## ⚠️ Warning
Note: Running this lab will INCUR COSTS. Please review your resources and budgeting before proceeding. Additionally, be sure to follow the Cleanup Process outlined in the Conclusion section to avoid unnecessary charges after completing the lab

## Table of Contents

##Khizer

- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. Create IAM Role](#1-create-iam-role)
  - [2. Launch EC2 Instance](#2-launch-ec2-instance)
  - [3. Install Git on the EC2 Instance](#3-install-git-on-the-ec2-instance)
  - [4. Clone GitHub Repository and Run Setup Script](#4-clone-github-repository-and-run-setup-script)
  - [5. Clone FIS Workshop Experiments](#5-clone-fis-workshop-experiments)
- [License](#license)

## Prerequisites

Before you begin, ensure you have the following:

- An AWS account with appropriate permissions to create IAM roles, EC2 instances, and run CloudFormation templates.
- Basic knowledge of AWS services and the AWS Management Console.
- SSH access to an EC2 instance.

## Setup Instructions

### 1. Create IAM Role

First, you need to create an IAM role that will be used by your EC2 instance.

- **Role Name:** `fisworkshop-admin`
-  **Important:** The naming convention (`fisworkshop-admin`) is crucial for the rest of the lab to work properly.
  - **Create role with EC2 permissions** 
- **Permissions:** Select AWS Service > EC2 > Administrator access. Once role is created, edit trust policy as below.  

  
 	 ```bash
	{
		"Version": "2012-10-17",
		"Statement": [
			{
				"Effect": "Allow",
				"Principal": {
					"Service": [
						"ec2.amazonaws.com",
						"ssm.amazonaws.com"
					]
				},
				"Action": "sts:AssumeRole"
			}
		]
	}
	```
- - **Policies** Add AmazonSSMManagedInstanceCore into permission policies .
   
### 2. Launch EC2 Instance

Next, launch an EC2 instance: name fisidereplec2
Size:30 GB
Instance Type: m5.xlarge


- Choose your preferred region.
- Assign the `fisworkshop-admin` IAM role to this EC2 instance.
### 3. Login to EC2 instance and switch to root 

Once your EC2 instance is up and running, SSH into it and install Git:

```bash
sudo su -
```

### 3. Install Git on the EC2 Instance

Once your EC2 instance is up and running, SSH into it and install Git:

```bash
yum update -y
yum install git -y
```

### 4. Clone GitHub Repository and Run Setup Script

Now, clone your GitHub repository and run the setup script to install all necessary dependencies:

```bash
git clone https://github.com/nasiaullas/FaultInjectionSimulator-KodeKloud.git
```
```bash
cd FaultInjectionSimulator-KodeKloud/Manual_IDE
```
```bash
chmod 777 pre-req-manual-ide.sh
```
```bash
./pre-req-manual-ide.sh
```

### 4. Clone FIS Workshop Experiments

Next, clone the FIS Workshop experiments repository:

```bash
mkdir -p ~/environment/workshopfiles && git clone https://github.com/aws-samples/aws-fault-injection-simulator-workshop-v2.git ~/environment/workshopfiles/fis-workshop
```


Please go to https://catalog.us-east-1.prod.workshops.aws/workshops/eb89c4d5-7c9a-40e0-b0bc-1cde2df1cb97/en-US/environment/bring-your-own  (Deploy Application) section to continue configuration 





