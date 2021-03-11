# Fetch Rewards

# Introduction
![Topology](https://github.com/alexlop00/Fetch-Rewards/blob/main/FetchRewards.PNG) 

## Scope
The purpose of the provided Python script is to deploy a Linux AWS EC2 instance with two volumes and two users.

As per the scope of this script, the included YAML template deploys:
* a Virutal Private Cloud (VPC) with CIDR block 192.168.2.0/24
* a Subnet with CIDR block 192.168.2.0/26
* an Internet Gateway, and allocates the resource to the VPC
* a Route Table and Routes, and associates the resource to the Subnet
* a Network Access Control List (ACL) and Entries, and associates the resource to the Subnet
* a Security Group
* an EC2 instance with the following properties:
  * Instance Type: t2.micro
  * Image Properties:
    * ami_type: amzn2
    * architecture: x86_64
    * root_device_type: ebs
    * virtualization_type: hvm 
  * two volumes: 10 GiB, 100 GiB (mounted in / & /data)
  * two users: user1, user2 (with configured public keys)
* an Elastic IP address and associates it to the EC2 instance

## Warning

The script defaults to the "us-east-2a" availability zone. Adjust the value according to your configuration.

Location of All Availability Zone Configurations (by Logical ID):
* Subnet1 ... AvailabilityZone: us-east-2a
* EC2Instance1 ... AvailabilityZone: us-east-2a

Adjust the RoleARN value in the response parameter (located at the end of the script) to your configuration. 

## Security Considerations

This script is intended for demonstration purposes. Open access (i.g. 0.0.0.0/0) is enabled by default. 
Adjust this value as necessary to your configuration. 

Location of All Security Warnings (by Logical ID):
* RoutetoAllowTraffic1 ... DestinationCidrBlock: "0.0.0.0/0" 
* NetworkACLEntry1 ... CidrBlock: "0.0.0.0/0"
* NetworkACLEntry2 ... CidrBlock: "0.0.0.0/0"
* SecurityGroup1 ... CidrIp: "0.0.0.0/0"

Additionally, a key pair has not been assigned to the created EC2 instance. Access is via the EC2 Instance Connect console. If you would like to configure a key pair, add the KeyName property to EC2Instance1 (by Logical ID). 

# Prerequisites

Software: 
* Python 3 
* Boto 3
* Amazon Web Services (AWS) Command Line (CLI)
  * Configure AWS with User Access Key

Permissions:
An AWS role providing CloudFormation access to the necessary services (e.g. EC2 & VPC) is required. 
* Note: Adjust the RoleARN value in the response parameter (located at the end of the script) to your configuration. 

# Deploy

Configure the necessary prerequisites (i.g. software, AWS role).

Adjust the Availability Zone values. 
Adjust the RoleARN value (located at the end of the script). 

Optional: Restrict access (i.g. ACL, Routes, Security Group).

Run the script: python3 automateDeployment.py

# Proof of Concept

Run the script.

![Script](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/RunScript.PNG)

View AWS CloudFormation.

![CloudFormation](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/CloudFormation.PNG)

Access EC2 Instance via EC2 Connect.

![EC2 Connect](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/EC2Connect.png)

View created users.

![Created Users](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/createdUsers.PNG)

Access user accounts via SSH private key.

![SSH](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/SSHAccess.PNG)

View volume mounts.

![Mounts](https://github.com/alexlop00/Fetch-Rewards/blob/cd138f8e3e81f9b096c548a546f5f82add8efc21/ProofofConcept/blockmounts.PNG)


