+++
title = "Week 2"
weight = 12
+++

# AWS compute
## Running compute stuff in AWS
This is simply refering to the background services supporting the applications you stand ip in  AWS. This is the storage and memory that give horsepower to your applications running in this cloud. In AWS you are given 3 options: virtual machines, containers, and serverless.
Although amazon uses the term web service to refer to these instances, it doesnt mean that your simply limited to that. 
In AWS EC2 instances are closer to virtual machines than anything else. Amazon Machine Image AMI is an image available on AWS, Amazon supplies these or you can create and supply one on your own. They have images that are optimized for different things so be mindful of this. The name of these dictate the type of image followed by the size. 
You can also create an AMI from one of your existing EC2 instances and resuse that image when necessary. Every AMI on the amazon market place has a unique AMI ID. These IDs are unique to each region!
When you launch an EC2 instance from an AMI it transitions to to pending then running.  Now it can be stoped, restarted, stop-hibernate, or shutdown
![[Pasted image 20211105145947.png]]

When running you are billed for that instance. You are not billed for everystate so thats why this is important. When an intance is stopped you are not billed for it. Although you are still billed for any storage that is being used by that instance. 

#aws/ec2
## EC2 instance
This is really just running linux services in the cloud. closest to running vms locally. These servers power your application by providing CPU, memory, and networking capacity to process users’ requests and transform them into responses. For context, common HTTP servers include:

* Windows options, such as Internet Information Services (IIS).
* Linux options, such as Apache HTTP Web Server, Nginx, and Apache Tomcat.

### autoscaling
The autoscalling of the EC2 instances can happen as a result of conditions you can set yourself.

### image builder
this works to reduce the effort necessary to keep images up to date. It offers a simple graphical interface with built-in automation, and AWS provided security settings. 

### lightsail
preconfigured packages for making ec2 instances easier to deploy


## Container services
This includes AWS ECS and AKS. ECS manages a cluster of ec2 instances that act as hosts for the containers. a cluster can consist of several ec2 instances. 

Amazon EKS is conceptually similar to Amazon ECS, but there are some differences.

* An EC2 instance with the ECS Agent installed and configured is called a container instance. In Amazon EKS, it is called a worker node.
* An ECS Container is called a task. In the Amazon EKS ecosystem, it is called a pod.
* While Amazon ECS runs on AWS native technology, Amazon EKS runs on top of Kubernetes.

#/aws/beanstalk
### Elastic Beanstalk
[AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and Internet Information Services (IIS).

You can simply upload your code, and AWS Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, and auto scaling to application health monitoring. At the same time, you retain full control over the AWS resources powering your application and can access the underlying resources at any time.



## Serverless
Every  of serverless mentions four aspects.

* No servers to provision or manage.
* Scales with usage.
* You  pay for idle .
* Availability and fault  are built-in.


#aws/fargate
### Explore Serverless Containers with AWS Fargate
Amazon ECS and Amazon EKS enable you to run your containers in two modes.

* Amazon EC2 mode
* AWS Fargate mode

### Fargate
[AWS Fargate](https://aws.amazon.com/fargate/) is a compute engine for Amazon ECS that allows you to run [containers](https://aws.amazon.com/containers/) without having to manage servers or clusters. With AWS Fargate, you no longer have to provision, configure, and scale clusters of virtual machines to run containers. This removes the need to choose server types, decide when to scale your clusters, or optimize cluster packing. AWS Fargate removes the need for you to interact with or think about servers or clusters. Fargate lets you focus on designing and building your applications instead of managing the infrastructure that runs them.

#/aws/lambda
### Lambda
This allows you to run code on demand in the cloud and only get charged for what you run when you run it. You can setup triggers for the code to run as a result of some actions in connection to other amazon services such as uploading a document in an S3 bucket.

#### How Lambda Works
There are three primary components of a Lambda function: the trigger, code, and configuration.

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/6Ex5RS8xTD-MeUUvMbw_8Q_825bc71e35344d209eda6a4abde927da_image-18-.png?expiry=1637107200000&hmac=1-jjseWJtBqlfRGo4YzIRj9IcckDOBen46bQ9JJLL4A)

The code is source code, that describes what the Lambda function should run. This code can be authored in three ways.

* You create the code from scratch.
* You use a blueprint that AWS provides.
* You use same code from the AWS Serverless Application Repository, a resource that contains sample applications, such as “hello world” code, Amazon Alexa Skill sample code, image resizing code, video encoding, and more.



#coursera/AWScloudessentials/vpc

# AWS Networking
  A VPC operates inside a region. Once in a region you create the VPC by setting the ip range and cidr notation for subnet. Now create subnets. To create the subnet you need a name, Availability Zone, and ip range.
![[Pasted image 20211115095746.png]]
## Subnets
#aws/internet_gateway
### Internet Gateways
This just facilitates an internet connection for your newely created VPC, without this you get no internet.

#aws/vgw
#### VGW 
This can be used to create a connection for a hybrid network where the cloud is directly connect to your on prem solution. 

#aws/route_table
### Route tables
In a VPC, any subnets created inside of a single VPC are assumed routable to eachother. This is the local route for the entire vpc. Subnets can be more granular. You can create custom route tables then associate them with subnets. 
#### ACL
 This is just the IPtables for the route table. The route tables are kind of treated like an independant element that can be associated with other services. This ACL gets associated with a route table and is used to protect subnets. 
 
 ### Security Groups
 Here is where you can create firewalls that either block or permit all network traffic. This are stateful so it will acknowledge flows starting / originating from within the VPC network / EC2 instance. default setting is to block all incoming traffic but allow all outgoing traffic. 