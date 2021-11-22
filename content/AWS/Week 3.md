+++
title = "Week 3"
weight = 13
+++

#coursera/AWScloudessentials/storage

# Block vs File Storage
## Storage Types
### File Storage
File Storage is closer to the traditional windows settup in an heirarchy.
Common use cases for file storage include: 

* Large  content repositories
* Development  environments
* User  home directories

### Block Storage
File storage treats files as a singular unit, block storage splits files into fixed-size chunks of data called blocks that have their own addresses. Since each block is addressable, blocks can be retrieved efficiently.

### Object Storage
![[Pasted image 20211116213714.png]]
Objects, much like files, are also treated as a single unit of data when stored. However, unlike file storage, these objects are stored in a flat structure instead of a hierarchy. Each object is a file with a unique identifier. This identifier, along with any additional metadata, is bundled with the data and stored.

With object storage, you can store almost any type of data, and there is no limit to the number of objects stored, making it easy to scale. Object storage is generally useful when storing large data sets, unstructured files like media assets, and static assets, such as photos.

## EC2 Instance Store
This is the temporary block level storage for an instance. This gets tied directly to the EC2 instance that its associated with. If the instance gets deleted than the storage also gets deleted as well. 

#### So when is this a good idea? 
This storage solution is idealif you are hosting applications that replicate data to other EC2 instances, such as a hadoop cluster. For cluster based workloads, having the *speed* of locally attached volumes and the resiliency of replicated data helps you achieve data distribution at high performance. 
Also ideal for temporary storage of information.

## EBS Volumes
AKA, Amazon Elastic lock Storage, So your storage is seperate from your EC2 instance and remain persistant. EBS volumes act just like external drives in more ways than one. 
*  EBS can be connected to either a single instance in a one-to-one relationship with an EC2 instance. Amazon has also released a EBS multi-attached feature that enables volumes to be attached to multiple EC2 instances simultaneously. This feature is not available for all instance types and must be in the same availability zone.
*  Be mindful that this is in fact seperate from the EC2 instances so if something goes wrong with the instance the EBS volume wont suffer the same fate.
*  Your limited to the size of the external drive, since it has a fixed limit to how scalable it can be. 

These instances are also scalable in 2 ways
1. Increase the volume size, as long as it doesnt increase above the maximum amount of storage (16TB), that can be divided up so long as to not exceed 16TB.
2. You can attach multiple volumes to a single EC2 instance. 

### Benefits of Using Amazon EBS
Here are the following benefits of using Amazon EBS (in case you need a quick cheat sheet).

* High availability: When you create an EBS volume, it is automatically replicated within its Availability Zone to prevent data loss from single points of failure.
* Data persistence: The storage persists even when your instance doesn’t.
* Data encryption: All EBS volumes support encryption.
* Flexibility: EBS volumes support on-the-fly changes. You can modify volume type, volume size, and input/output operations per second (IOPS) capacity without stopping your instance.
* Backups: Amazon EBS provides you the ability to create backups of any EBS volume.

#### so when is this a good idea?
Really this is useful when you need to retrieve data quickly and have data persistent long-term. These are typically used for:
* *Operating Systems:* Boot/root volumes to store an operating system. this is typically refered to as an EBS-backed AMI.
* *Databases:* A storage layer for databases running on Amazon EC2 that rely on transactional reads and writes.
* *Enterprise applications:* For reliable block storage...
* *Throughput-intensive applications:* Applications that perform long, continuous reads and writes.  
