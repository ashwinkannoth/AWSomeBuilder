# AWSomeBuilder Project

## Abstract 
This project creates a highly available and scalable architecture to host a single page web application. It consists of, but is not limited to, the following features: Amazon Aurora as a backend database, EFS as a NFS backend storage, S3 to store logs or streaming data, and a fully integrated CI/CD pipeline. 


- [Introduction](#introduction)

- [Architecture Diagram](#architecturediagaram)

- [Prerequisites](#prerequisites)

- [Deployment](#deployment)

- [Next Steps & Testing](#NextSteps&Testing)

- [Contact](#contact)

## Introduction
This project will provide you with the resources to build and deploy your own single page web application. The architecture is portrayed in the diagram shown in the following section (nb. VPN Gateway Branch + Fleet/IoT GW is not implemented due to practical reasons). 

Let us cover the key components that will be installed, and the role they play in this architecture:

- [x] [Amazon VPC](https://aws.amazon.com/vpc/?vpc-blogs.sort-by=item.additionalFields.createdDate&vpc-blogs.sort-order=desc): a service that lets you launch the AWS resources in a logically isolated virtual network.
- [x] [Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html), allowing communication between VPC and the internet.  
- [x] [Amazon CloudFront](https://aws.amazon.com/cloudfront/), a fast CDN service that securely delivers data, and applications to customers with low latency and high transfer speeds.   
- [x] [Amazon Web Application Firewall](https://aws.amazon.com/waf/), to protect the web application against common web exploits and bots that may affect availability, compromise security, or consume excessive resources. 
- [x] An architecture hosted across two [Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) ensuring high availability. 
- [x] [Amazon EC2](https://aws.amazon.com/ec2/?ec2-whats-new.sort-by=item.additionalFields.postDateTime&ec2-whats-new.sort-order=desc) instances providing compute capacity in the cloud. This is where the web server will be run. The instances are placed within an [Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html), enabling them to scale up or down with demand ensuring efficient price/performance. 
- [x] [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) to enable instances in the private subnets to connect to the internet. 
- [x] [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) to distribute incoming traffic across multiple EC2 instances. 
- [x] [Amazon Cognito](https://aws.amazon.com/cognito/) to provide simple and secure user sign-up and sign-in for the web application. 
- [x] [AWS Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) enables interactive, browser-based management of the EC2 instances. 
- [x] [Amazon Aurora](https://aws.amazon.com/rds/aurora/?aurora-whats-new.sort-by=item.additionalFields.postDateTime&aurora-whats-new.sort-order=desc) a MySQL and PostgreSQL compatible relational database built for the cloud. 
- [x] [Amazon EFS](https://aws.amazon.com/efs/), an elastic file system that does not require provisioning and managing storage. Enables connection to multiple EC2 instances simultaneously. 
- [x] [Amazon S3](https://aws.amazon.com/s3/) buckets to store data. 
- [x] [VPC Flowlogs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html) sent automatically to S3. 
- [x] [Amazon Kinesis Firehose](https://aws.amazon.com/kinesis/data-firehose/?kinesis-blogs.sort-by=item.additionalFields.createdDate&kinesis-blogs.sort-order=desc) to enable near real time streaming of information into data lakes, such as S3. 
- [x] [Amazon Athena](https://aws.amazon.com/athena/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc) is an interactive query service that analyze data in S3 using standard SQL. 
- [x] [AWS CodePipeline](https://aws.amazon.com/codepipeline/), a fully managed continuous delivery service that enables automatic release pipelines for fast and reliable application updates. Stores code in [AWS CodeCommit](https://aws.amazon.com/codecommit/), a fully managed source code control service that hosts secure git-based repositories. CodePipeline will then use [AWS CodeDeploy](https://aws.amazon.com/codedeploy/) to deploy the service into the ASG.   

## Architecture Diagram

![AB Proposal-2(1)-Copy of Copy of Page-2](https://user-images.githubusercontent.com/32502465/114927451-78923080-9dff-11eb-9de3-07ede5d99611.jpg)

## Prerequisites

Please ensure the following prerequisites are met prior to deploying this application:
- [x] Basic knowledge of the AWS Console, CLI and Git. 
- [x] Permissions to deploy CloudFormation templates within your AWS account. 
- [x] Valid domain names along with certificates. Replace Cognito callback URL + CloudFormation URL with appropriate DNS names. Replace certificate values with appropriate certificates. [Amazon Route53](https://aws.amazon.com/route53/) can be used for DNS related tasks. [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/) can be used for provisioning and managing certificates. 

## Deployment

1. Navigate to the CloudFormations page within your AWS Console. ![Screen Shot 2021-04-16 at 3 37 25 PM](https://user-images.githubusercontent.com/32502465/115130541-8c37c580-9fbe-11eb-83f0-eebc0f6e60ec.png)

2. Click _Create stack_. ![Screen Shot 2021-04-16 at 3 37 44 PM](https://user-images.githubusercontent.com/32502465/115130547-98238780-9fbe-11eb-994c-ceea5785cfc5.png)

3. Select _Template is ready_ and _Upload a template file_. Choose the AB.yml file. Hit next when complete. ![Screen Shot 2021-04-16 at 3 38 32 PM](https://user-images.githubusercontent.com/32502465/115130560-aec9de80-9fbe-11eb-95f0-49a392b7c5d2.png)

4. Enter a _Stack name_. Edit the parameters as needed. Once complete, click _Next_. Please note the following:
    - Ensure AMI ID is valid in your region of choice. 
    - Default PW for Aurora is "password". 
    - Bucket names must be globally unqiue. 
    - Replace the certificates with ones which are unique to your use case. 
    - Replace the CloudFront domain name with one which is unique to your use case. ![Screen Shot 2021-04-16 at 3 45 34 PM](https://user-images.githubusercontent.com/32502465/115130565-b5585600-9fbe-11eb-9091-2889b3ee2a3e.png)

5. Leave all options as default, scroll down and click _Next_. ![Screen Shot 2021-04-16 at 3 46 08 PM](https://user-images.githubusercontent.com/32502465/115130573-be492780-9fbe-11eb-852d-5b8db13be0a1.png)

6. Review your Stack. Select the checkbox acknowledging the creation of IAM resources with custom names. Click _Create Stack_. ![Screen Shot 2021-04-16 at 3 47 32 PM](https://user-images.githubusercontent.com/32502465/115130577-c3a67200-9fbe-11eb-850a-de452bc8bdbe.png)

7. Complete stack creation will take approximately: 30 minutes. You may view the progress of individual events in the Events tab. You can view the progress of resource creation in the Resources tab. 
8. The _Status_ of the stack will go from 'CREATE_IN_PROGRESS' to 'CREATE_COMPLETE' when successfully completed. ![Screen Shot 2021-04-16 at 3 49 08 PM](https://user-images.githubusercontent.com/32502465/115130587-d91b9c00-9fbe-11eb-8192-cfb2047dde11.png)

9. Congratulations! You are now complete. ![Screen Shot 2021-04-16 at 4 26 12 PM](https://user-images.githubusercontent.com/32502465/115130589-dd47b980-9fbe-11eb-8a01-d820efccabd2.png)


## Next Steps & Testing
The functionality of this architecture can be tested in various ways. The following list contains a few suggested methods: 

- Test the Firehose delivery stream by sending demo data to the S3 bucket. Instructions can be found [here](https://docs.aws.amazon.com/firehose/latest/dev/test-drive-firehose.html). 
- Terminate an EC2 instance to observe how the ASG reacts. 
- Use Athena to query the VPC flowlogs found in S3. Instructions and tips can be found [here](https://docs.aws.amazon.com/athena/latest/ug/vpc-flow-logs.html). 
- Connect to individual EC2 instances using Systems Manager Session Manager. Experiment with EFS and Aurora DB. 
- Connect your repository to AWS CodeCommit by following the instructions [here](https://docs.aws.amazon.com/codecommit/latest/userguide/how-to-connect.html). Once a commit has been made and pushed, you can observe the pipeline progress using AWS CodePipeline. A sample web page has been provided in this repository. It is designed with two files, one which requires authentication via Cognito. 
- When accessing the website created via the CodePipeline, click the link to the Secret Page. Authenticate via Cognito to access this page. 

## Contact

If you have any questions feel free to contact me at: kannotha@amazon.com



