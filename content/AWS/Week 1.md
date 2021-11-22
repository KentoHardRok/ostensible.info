+++
title = "Week 1"
weight = 11
+++

#coursera/AWScloudessentials/regions

# Regions!
1. AWS region considerations:
	1. **Compliance**
		1. Enterprise companies often need to comply with regulations that require customer data to be stored in a specific geo territory.
	2. **latency**
		1. Simply put, choose the region that offers the least amount of latency.
	3. **pricing**
		1. some regions are more expensive than others, so be aware of that
	4. **service availability**
		1. Not all services are available everywhere so be conscious to verify what services you require.
2. The first real bit of information this week discusses is the physical layout of their infrastructure. A data center exists inside of a zone, a zone is a group of redundant data centers. A region is a group of redundant zones. Each zone is labeled by the physical area the inhabit... more or less.
3. AWS regions are independent of each other. So your data doesn't leave a region without your explicit consent.
4. Services within AWS are deployed either within an AZ, a region or globally so look it ip.


#coursera/AWScloudessentials/api

# Interacting with AWS
1. How to interact with the AWS API:
	1. AWS Management console
	2. AWS command line interface
	3. AWS software development kits (SDK)

# AWS Identity and Access Management
## IAM
### How it works
![[Pasted image 20211105123552.png]]

This is what a section of a policy looks like. This is much like many other places that have this. Its a role based method of allowing people access to perform actions on AWS. Obviously this has no bearing on your application that you build.
-   The **Version** element defines the version of the policy language. It specifies the language syntax rules that are needed by AWS to process a policy. To use all the available policy features, include "Version": "2012-10-17" before the "Statement" element in all your policies.
    
-   The **Effect** element specifies whether the statement will allow or deny access. In this policy, the Effect is "Allow", which means you’re providing access to a particular resource.
    
-   The **Action** element describes the type of action that should be allowed or denied. In the above policy, the action is "*". This is called a wildcard, and it is used to symbolize every action inside your AWS account.
    
-   The **Resource** element specifies the object or objects that the policy statement covers. In the policy example above, the resource is also the wildcard "*". This represents all resources inside your AWS console.=

and here is yet a more granular policy:

```
{
"Version": "2012-10-17",
	"Statement": [{
		"Effect": "Allow", 
		"Action": [ "iam: ChangePassword", 
		"iam: GetUser" 
		]
	"Resource": "arn:aws:iam::123456789012:user/${aws:username}" 
}]
```


### IAM Roles
Roles can be assumed by many different identities and are temporary in nature. This really is focused on setting a sort of RBA for users without explicitly creating each user in IAM. For a hybrid deployment for example you can assign roles to internal groups so as users within your pre-established enterprise require access, they will be automatically assign resources based on their group association. IAM best practices also tries to follow general user account best practices such as:
- Lock down the Root user account
- Least privilege
- appropriate use only
- and use when possible
- consider using an identity provider
- there is also AWS SSO


#coursera/AWScloudessentials/security


### Application Diagram
![[Pasted image 20211105133311.png]]

