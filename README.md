# Springfield Carshare Website Architecture

## Abstract 
This project creates a highly available and scalable architecture to host a single page web application. It consists of, but is not limited to, the following features: Amazon Aurora as a backend database, EFS as a NFS backend storage, S3 to store logs or streaming data, and a fully integrated CI/CD pipeline. 


- [Introduction](#introduction)

- [Prerequisites](#heading-1)
  * [Sub-heading](#sub-heading-1)
    + [Sub-sub-heading](#sub-sub-heading-1)
- [Heading](#heading-2)
  * [Sub-heading](#sub-heading-2)
    + [Sub-sub-heading](#sub-sub-heading-2)

## Introduction
This project will provide you with the resources to build and deploy your own single page web application. The architecture is portrayed in the diagram shown below (nb. VPN Gateway Branch + Fleet/IoT GW is not implemented due to practical reasons). 

![Architecture Diagaram](https://user-images.githubusercontent.com/32502465/114913033-b2a70680-9dee-11eb-859f-4a0cd311682e.jpg)

Let us cover the key components that will be installed, and the role they play in this architecture:

- [x] [VPC](https://aws.amazon.com/vpc/?vpc-blogs.sort-by=item.additionalFields.createdDate&vpc-blogs.sort-order=desc): a service that lets you launch the AWS resources in a logically isolated virtual network.
- [x] An architecture hosted across two [Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) ensuring high availability. 
- [x] [EC2](https://aws.amazon.com/ec2/?ec2-whats-new.sort-by=item.additionalFields.postDateTime&ec2-whats-new.sort-order=desc) instances providing compute capacity in the cloud. The instances are placed within an [Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html), enabling them to scale up or down with demand ensuring efficient price/performance. 
- [x] [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) to enable instances in the private subnets to connect to the internet. 
- [x] [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) to distribute incoming traffic across multiple targets, in this case EC2 instances. 
- [x] [Cognito](https://aws.amazon.com/cognito/) to provide simple and secure user sign-up and sign-in
- [x] [Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) enabling interactive, browser-based management of EC2 instances. 
- [x] [Amazon Aurora](https://aws.amazon.com/rds/aurora/?aurora-whats-new.sort-by=item.additionalFields.postDateTime&aurora-whats-new.sort-order=desc) a MySQL and PostgreSQL compatable relational database built for the cloud. 
- [x] [EFS](https://aws.amazon.com/efs/), a simple, serverless, elastic file system that enables you to share file data without provisioning and managing storage. Enables connection to multiple EC2 instances simultaniousley. 
- [x] [VPC Flowlogs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) sent automatically to S3. 
- [x] [Kinesis Firehose](https://aws.amazon.com/kinesis/data-firehose/?kinesis-blogs.sort-by=item.additionalFields.createdDate&kinesis-blogs.sort-order=desc) to enable near real time streaming of information into data lakes, such as S3. 
- [x] [Athena](https://aws.amazon.com/athena/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc) is an interactive query service that analyze data in S3 using standard SQL. 
- [x] [CodePipeline](https://aws.amazon.com/codepipeline/), a fully managed continuious delivery service that enables automatic release pipelines for fast and reliable application updates. Stores code in [CodeCommit](https://aws.amazon.com/codecommit/), a fully managed source code control service that hosts secure git-based repositories. CodePipeline will then use [CodeDeploy](https://aws.amazon.com/codedeploy/) to deploy the service into the ASG.   


### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading

## Heading

This is an h1 heading

### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading

## Heading

This is an h1 heading

### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading
