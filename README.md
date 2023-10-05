# Project: Deploy a High-Availability Web App using CloudFormation

## 1. Diagram about this Project
https://lucid.app/lucidspark/28893646-7f2a-4593-b72d-157b1689d40b/edit?viewport_loc=-867%2C-633%2C3437%2C1583%2C0_0&invitationId=inv_08b6b91d-7485-40cb-8ca6-b764a64a454c

## 2. Have 5 file Yaml to create stack
- File: networks.yml --> To Configure the network (VPCs, Subnets, route tables,...)
* File: s3bucket.yml --> To Configure the S3 bucket
+ File: IAMRole.yml --> To Configure the IAM Role and Policy
- File: servers.yml --> To Configure servers EC2 Loadbanlancer, Autoscaling,...
* File: bastion-host.yml --> To Configure bastion Host to connect with instance into private subnets

## 3. Run sequence the commands
	aws cloudformation create-stack --stack-name $1 --region $2 --template-body file://$3

### networks
	aws cloudformation create-stack --stack-name networks --region us-east-1 --template-body file://infrastruture/networks.yml --parameters file://parameters/networks-parameters.json

### s3bucket
		aws cloudformation create-stack --stack-name s3bucket --region us-east-1 --template-body file://infrastruture/s3bucket.yml --parameters file://parameters/s3bucket-parameters.json

### IAMRole
	aws cloudformation create-stack --stack-name IamRole --region us-east-1 --template-body file://infrastruture/IAMRole.yml --parameters file://parameters/IAMRole-parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"

### servers
	aws cloudformation create-stack --stack-name servers --region us-east-1 --template-body file://infrastruture/servers.yml --parameters file://parameters/servers-paramters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"

### bastion host
	aws cloudformation create-stack --stack-name bastionHost --region us-east-1 --template-body file://infrastruture/bastion-host.yml --parameters file://parameters/bastion-host-parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"

## 4. The HTTP DNS of LoadBalaner
  http://serve-WebSe-10VUHYMAXJX71-1945665452.us-east-1.elb.amazonaws.com




