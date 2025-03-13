---
title: "Deep Dive on AWS Storage Services"
layout: post
date: 2025-03-11
categories: [aws]
tags: [cloud, storage, notes]
---

> To be split into 4 parts:
- intro
- block
- file
- object (also include the subsequent deep dive course on S3)

## Introduction

### On-prem Storage vs AWS Cloud Storage

When buying on-prem storage you usually start from the actual data capacity and work backwards to find the total capacity you need to buy to account for backup snapshots, data growth, formatting, RAID, OS, etc, and then buy and pay said total capacity.

When buying cloud storage you only pay for the actual capacity you consume or you allocate, depending on the pricing model of the service you choose.

AWS has two models for storage capacity: consumed storage and allocated capacity. The core service selected determines the method used.

Capacity is billed based on time that the capacity is used.

Some services, such as S3, are billed based on the amount of storage capacity consumed, others, such as Block Storage (EBS), are billed based on the capacity you allocate, independently of how much you use (similar to Google Drive).

### Primary Storage Types:

- **Block**

  - Block storage is raw storage in which the hardware storage device or drive is a disk or volume that is formatted and attached to the compute system for use. The storage is formatted into predefined continuous segments on the storage device. These segments are called blocks. The blocks are the basic fixed storage units used to store data on the device.

  Storage devices can be hard disk drives (HDDs), solid state drives (SSDs), or newer types of storage devices, such as Non-Volatile Memory Express (NVMe).
- **File**

  - File storage is built on top of block storage, typically serving as a file share or file server. File storage is created using an operating system that formats and manages the reading and writing of data to the block storage devices. The name file storage comes from the primary use of storing data as files typically in a directory tree hierarchy.

  The two most common storage protocols for file storage are Server Message Block (SMB) and Network File System (NFS). You can use the network protocols to communicate with remote computers and servers. You can also use server resources or share, open, and edit files.

  The file system can be Windows Server, Linux, or a specialized operating system used on network attached storage (NAS) devices or clustered NAS systems.
- **Object**

  - Object storage is also built on top of block storage. Object storage is created using an operating system that formats and manages the reading and writing of data to the block storage devices. The name object storage comes from the primary use of storing the data within a binary object. Unlike file storage, object storage does not differentiate between types of data. The type of data or the file type becomes part of the data's metadata.

  An object is made up of a larger set of blocks organized by using a predetermined size. For example, one object storage system uses binary object sizes of 128 megabytes (MB). Smaller files or data are stored at a binary level within the object. Larger data files are stored by spreading the data across multiple objects.

  Object storage is recognized for its inherent availability of the file objects. Some systems support file versioning, file tracking, and file retention.

### Intro to AWS Cloud Storage Services

Each application has different needs and thus needs a different storage solution.

- Some applications need dedicated, low latency storage for each host. This is a perfect use case for Block Storage.
- Some apps need access to shared files and require a file system, like content repositories, media stores or home directories. This is a use case for File Storage.
- Applications developed in the cloud often take advantage of object storage's scalability and metadata characteristics. Object storage solutions are ideal for building modern applications from the beginning that require scale and flexibility.  Amazon S3 is offered with different storage classes or tiers to match your price, access, and availability requirements. Amazon S3 Glacier, for example, is used for archival storage at a lower cost per gigabyte (GB).

### Identifying the Right Storage Solution in the Cloud

The optimal storage solution depends on a series of factors:

- types of access (block, file, object)
- Patterns of access (random or sequential)
- throughput (IOPS)
- frequency of access
- frequency of update
- availability and durability

## Core AWS Storage Services

### Block Storage: Amazon EBS

AWS offers 2 kinds of Block Storage:

- EC2 Instance Storage

  - An instance store provides temporary (ephemeral) block-level storage for
    your instance. This storage is located on disks that are physically
    attached to the host computer where the compute instance is. Only specific Amazon EC2 instance types support instance stores.
  - Instance store is ideal for the following use cases:
    - Temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content
    - Data that is replicated across a fleet of instances, such as a load-balanced pool of web servers
  - As **ephemeral storage**, instance stores are not replicated or spread
    across multiple devices to improve durability and availability. An
    instance store is nonpersistent and is **terminated when the associated EC2 instance is terminated**.

- Amazon Elastic Block Store (EBS)
    - Amazon EBS is an easy-to-use, high performance, block storage service. It is designed for use with Amazon EC2 compute instances for both throughput and transaction-intensive workloads at any scale. 
    - EBS volumes are well suited for use as the primary storage for file systems, databases, or any applications that require fine granular updates and access to raw, unformatted, block-level storage.  
    - EBS volumes that are attached to an EC2 instance are exposed as raw block storage volumes that **persist independently from the life of the instance**. You can create a file system on top of these volumes or use them in any way you would use a block device (such as a hard drive). 
    - You can dynamically change the configuration of a volume attached to an EC2 instance, unlike traditional disk drives that come in fixed sizes.

    There are mainly two types of EBS volumes:
    - SSD-based volumes include two levels to meet your application requirements: General Purpose SSD volumes and Provisioned IOPS SSD volumes.
    - HDD-based volumes include Throughput Optimized HDD (st1) for frequently accessed, throughput-intensive workloads and the lowest cost Cold HDD (sc1) for less frequently accessed data.

    There is also the possibility to use Elastic Volumes, which adapt dynamically to the needs of the application.

    EBS volumes are designed to be highly available, reliable, and durable. You can create your EBS volumes as encrypted volumes to meet a wide range of data-at-rest encryption requirements for regulated/audited data and applications.

    You can create point-in-time snapshots of EBS volumes, which are persisted to Amazon S3. You can use snapshots to restore your data to new volumes, expand the size of a volume, or move volumes across Availability Zones. 

Amazon FSx for NetApp ONTAP also offers block storage services over a different protocol, but we will cover it later.

### FIle Storage Overview

#### File Storage: EFS

Amazon EFS is a scalable, elastic, cloud-native file system for Linux. Amazon EFS supports the Network File System (NFS) protocol.

Amazon EFS file systems can grow to petabyte scale, drive high levels of throughput, and allow massively parallel access from compute instances to your data. 

Multiple compute modules can access an Amazon EFS file system at the same time. These modules include include Amazon EC2, AWS Lambda, Amazon ECS, and Amazon EKS.

With Amazon EFS, you pay only for the storage used by your file system.

There are two main types of storage classes:

- Standard storage classes - multi AZ for durability
- One Zone storage classes - single AZ for cost saving

You can start saving on your storage costs by enabling EFS lifecycle management for your file system and choosing an age-off policy of 7,14, 30, 60, or 90 days. With EFS lifecycle management policies enabled, files automatically move to less expensive storage classes to save on cost.

Access is managed with VPCs, security groups and IAM policies.

Use Cases include: containers, serverless data storage, enterprise app file systems, analytics, content management, media storage, db backups.

#### File Storage: FSx for Lustre

Amazon FSx for Lustre is an AWS fully managed parallel file system built on Lustre for high performance computing (HPC) workloads. FSx for Lustre supports the Lustre POSIX-compliant protocol.

The open-source Lustre file system is designed for compute-intensive applications that require a fast storage system capable of meeting throughput requirements. FSx for Lustre was built to process large datasets quickly and cost-effectively and scale to meet growing demands. An FSx for Lustre file system is capable of delivering hundreds of gibibytes (GiB) per second of throughput and millions of IOPS.

You can integrate FSx for Lustre with Amazon Simple Storage Service (Amazon S3) to process datasets with the FSx for Lustre file system. When linked to an S3 bucket, an FSx for Lustre file system transparently presents S3 objects as files and allows you to write changed data back to Amazon S3.

Use Cases: 

- Horizontal Use Cases include machine learning and high performance computing (HPC) workloads.
- Vertical Use Cases include the following: Life science genomics, Financial models, Industrial design simulation, Media special effects and rendering, Seismic and reservoir exploration

#### File Storage: Amazon FSx for Windows File Server

Amazon FSx for Windows File Server is an AWS fully managed file system for Windows environments. FSx for Windows File Server supports the Server Message Block (SMB) protocol.

Amazon FSx for Windows File Server provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system.

FSx for Windows File Server is built on Windows Server. The service provides a rich set of administrative features that include user file restore, user quotas, and access control lists (ACLs).

You can access SMB file shares from Linux and macOS, any application. You can access the storage regardless of operating system. 

To control user access, Amazon FSx integrates with your on-premises Microsoft Active Directory and with AWS Microsoft Managed AD.

FSx for Windows File Server can connect your file system to the following AAWS services or resources:
  - Amazon Elastic Compute Cloud (Amazon EC2)
  - Amazon Elastic Container Service (Amazon ECS)
  - VMware Cloud on AWS
  - Amazon WorkSpaces
  - Amazon AppStream 2.0 instances

FSx for Windows File Server provides storage of up to 64 TB per file system. You can use Distributed File System (DFS) namespaces to create shared common namespaces spanning multiple FSx for Windows File Server file systems. Consequently, you can scale out storage and throughput to virtually unlimited levels.

#### File Storage: Amazon FSx for NetApp ONTAP

Amazon FSx for NetApp ONTAP is the NetApp ONTAP operating system implemented as a fully managed service. FSx for NetApp ONTAP support iSCSI for block storage, NFS protocol for POSIX-compliant access, and SMB protocol for Windows-compatible access.

FSx for ONTAP offers high-performance file storage that’s broadly accessible from Linux, Windows, and macOS compute instances via the industry-standard NFS, SMB, and iSCSI protocols. It allows you to use ONTAP’s widely adopted data management capabilities. You can create snapshots, clones, and replication, with the click of a button. In addition, it provides low-cost storage capacity that’s fully elastic and virtually unlimited in size. FSx for ONTAP supports data compression and deduplication to help you further reduce storage costs.

FSx for ONTAP offers high-performance SSD storage with sub-millisecond latencies, and makes it quick and easy to manage your data by enabling you to snapshot, clone, and replicate your files with the click of a button. It also automatically tiers your data to lower-cost, elastic storage, eliminating the need to provision or manage capacity and allowing you to achieve SSD levels of performance for your workload while only paying for SSD storage for a small fraction of your data.

FSx for ONTAP use cases are similar to those for Amazon EFS, Amazon FSx for Windows File Server, and Amazon FSx for OpenZFS. The key difference is that they apply multi-protocol access for applications and workflows using NFS and SMB protocols with an option for block storage using the iSCSI protocol. If you plan to use applications with multi-protocol access or migrated your existing NetApp ONTAP storage, FSx for ONTAP is your logical choice.

#### File Storage: Amazon FSx for OpenZFS

Amazon FSx for OpenZFS is an AWS fully managed implementation of the Open Zettabyte File System (ZFS). FSx for OpenZFS supports NFS and SMB protocols for a wide range of application implementations. 

FSx for OpenZFS delivers one of the lowest file storage latencies available in the cloud.

FSx for OpenZFS is built on the AWS Graviton family of processors, supporting up to 12.5 gigabytes per second (GB/s) of throughput and up to 1 million IOPS for frequently accessed cached data.

FSx for OpenZFS use cases are similar to those for Amazon EFS, Amazon FSx for Windows File Server, and Amazon FSx for NetApp ONTAP. The key difference is that they apply multi-protocol access for applications and workflows using NFS and SMB protocols. If you plan to use applications with multi-protocol access or migrated your existing OpenZFS storage, FSx for OpenZFS is your logical choice.

### Object Storage: Amazon S3

Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance.

Amazon S3 has a simple web service interface that you can use to store and retrieve any amount of data from anywhere on the web. Amazon S3 uses standards-based REST APIs designed to work with any internet-development toolkit. 

Data is stored as objects within resources called buckets. A single object can be up to 5 terabytes in size.

S3 features include the following capabilities:

- Appending metadata tags to objects
- Moving and storing data across different S3 storage classes
- Configuring and enforcing data access controls
- Securing data against unauthorized users
- Running big data analytics
- Monitoring data at the object or bucket levels
- Viewing storage usage and activity trends across your organization

Amazon S3 has a flat, non-hierarchical structure. All objects are stored in S3 buckets and can be organized with shared names called prefixes.

Performance scales per prefix, so you can use as many prefixes as you need in parallel to achieve the required throughput. You can have a virtually unlimited number of prefixes. Amazon S3 performance supports at least 3,500 requests per second to add data and 5,500 requests per second to retrieve data. Each S3 prefix can support these request rates, making it simple to increase performance significantly.

Storage Classes

Amazon S3 offers a range of storage classes designed for different use cases. Every S3 storage class supports a specific data access level at corresponding costs or geographic location. S3 storage classes include:

- S3 Standard for general-purpose storage of frequently accessed data
- S3 Standard-Infrequent Access (S3 Standard-IA) for less frequently accessed data
- S3 One Zone-Infrequent Access (S3 One Zone-IA) for less frequently accessed data and lower availability requirements
- S3 Intelligent-Tiering for data with unknown or changing access patterns
- Amazon S3 Glacier Instant Retrieval for lower-cost archival storage that may require retrieval at any time.  
- Amazon S3 Glacier Flexible Retrieval for low-cost archival storage with retrieval time from minutes to hours
- Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive) for lowest-cost storage with retrieval times up to 12 hours
- Amazon S3 on Outposts for on-premises hybrid data storage and satisfying data residency requirements. 

Amazon S3 also offers capabilities to manage your data throughout its lifecycle. When an S3 lifecycle policy is set, your data transfers to a different storage class automatically without any changes to your application.

You can use S3 Storage Class Analysis to monitor access patterns across objects to discover data that should be moved to lower-cost storage classes. Then, you can use this information to configure an S3 Lifecycle policy that makes the data transfer. 

S3 Lifecycle policies can also be used to expire objects at the end of their lifecycles.