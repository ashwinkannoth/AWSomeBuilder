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

Let us cover the key components that will be installed, and what they do:

- [x] [VPC](https://aws.amazon.com/vpc/?vpc-blogs.sort-by=item.additionalFields.createdDate&vpc-blogs.sort-order=desc): a service that lets you launch the AWS resources in a logically isolated virtual network.
- [x] An architecture hosted across two [Availability Zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) ensuring high availability. 
- [x] [EC2](https://aws.amazon.com/ec2/?ec2-whats-new.sort-by=item.additionalFields.postDateTime&ec2-whats-new.sort-order=desc) instances providing compute capacity in the cloud. The instances are placed within an [Auto Scaling Group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html), enabling them to scale up or down with demand ensuring efficient price/performance. 
- [x] [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) to enable instances in the private subnets to connect to the internet. 
- [x] [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) to distribute incoming traffic across multiple targets, in this case EC2 instances. 
- [x] [Cognito](https://aws.amazon.com/cognito/) to provide simple and secure user sign-up and sign-in
- [x] [Systems Manager Sesssion Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) enabaling 


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
