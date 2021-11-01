+++
title = "Week 1"
weight = 11
+++

#coursera/AWScloudessentials/regions

# Regions!
1. AWS region considerations:
	1. Compliance
		1. Enterprise companies often need to comply with regulations that require customer data to be stored in a specific geo territory.
	2. latency
		1. Simply put, choose the region that offers the least amount of latency.
	3. pricing
		1. some regions are more expensive than others, so be aware of that
	4. service availability.
		1. Not all services are available everywhere so be concious to verify what services you require.
2. The first real bit of information this week discusses is the physical layout of their infrastructure. A data center exists inside of a zone, a zone is a group of redundant data centers. A region is a group of redundant zones. Each zone is labled by the physical area the inhabit... more or less.
3. AWS regions are independant of eachother. So your data doesnt leave a region without your explicit consent.
4. Services within AWS are deployed either within an AZ, a region or globally so look it ip.


#coursera/AWScloudessentials/api

# Interacting with AWS
1. How to interact with the AWS API:
	1. AWS Management console
	2. AWS command line interface
	3. AWS software development kits (SDK)


#coursera/AWScloudessentials/security



