---
title: "Deep Dive on AWS Storage Services"
layout: post
date: 2025-03-11
categories: [aws]
tags: [cloud, storage]
---
## Introduction

### On-prem Storage vs AWS Cloud Storage

When buying on-prem storage you usually start from the actual data capacity and work backwards to find the total capacity you need to buy to account for backup snapshots, data growth, formatting, RAID, OS, etc, and then buy and pay said total capacity.

When buying cloud storage you only pay for the actual capacity you consume or you allocate, depending on the pricing model of the service you choose.

AWS has two models for storage capacity: consumed storage and allocated capacity. The core service selected determines the method used. 

Capacity is billed based on time that the capacity is used.

Some services, such as S3, are billed based on the amount of storage capacity consumed, others, such as Block Storage (EBS), are billed based on the capacity you allocate, independently of how much you use (similar to Google Drive).

### Primary Storage Types:

- Block
    - Block storage is raw storage in which the hardware storage device or drive is a disk or volume that is formatted and attached to the compute system for use. The storage is formatted into predefined continuous segments on the storage device. These segments are called blocks. The blocks are the basic fixed storage units used to store data on the device.
    
    Storage devices can be hard disk drives (HDDs), solid state drives (SSDs), or newer types of storage devices, such as Non-Volatile Memory Express (NVMe). 

- File
    - File storage is built on top of block storage, typically serving as a file share or file server. File storage is created using an operating system that formats and manages the reading and writing of data to the block storage devices. The name file storage comes from the primary use of storing data as files typically in a directory tree hierarchy.
    
    The two most common storage protocols for file storage are Server Message Block (SMB) and Network File System (NFS). You can use the network protocols to communicate with remote computers and servers. You can also use server resources or share, open, and edit files.
    
    The file system can be Windows Server, Linux, or a specialized operating system used on network attached storage (NAS) devices or clustered NAS systems.
- Object
    - Object storage is also built on top of block storage. Object storage is created using an operating system that formats and manages the reading and writing of data to the block storage devices. The name object storage comes from the primary use of storing the data within a binary object. Unlike file storage, object storage does not differentiate between types of data. The type of data or the file type becomes part of the data's metadata.
    
    An object is made up of a larger set of blocks organized by using a predetermined size. For example, one object storage system uses binary object sizes of 128 megabytes (MB). Smaller files or data are stored at a binary level within the object. Larger data files are stored by spreading the data across multiple objects.
    
    Object storage is recognized for its inherent availability of the file objects. Some systems support file versioning, file tracking, and file retention.

### Intro to AWS Cloud Storage Services

Each application has different needs and thus needs a different storage solution.

- Some applications need dedicated, low latency storage for each host. This is a perfect use case for Block Storage.

- Some apps need access to shared files and require a file system, like content repositories, media stores or home directories. This is a use case for File Storage.

- Applications developed in the cloud often take advantage of object storage's scalability and metadata characteristics. Object storage solutions are ideal for building modern applications from the beginning that require scale and flexibility.  Amazon S3 is offered with different storage classes or tiers to match your price, access, and availability requirements. Amazon S3 Glacier, for example, is used for archival storage at a lower cost per gigabyte (GB).

### Identifying the Right Storage Solution in the CLoud

The optimal storage solution depends on a series of factors:
- types of access (block, file, object)
- Patterns of access (random or sequential)
- throughput (IOPS)
- frequency of access
- frequency of update
- availability and durability

## Core AWS Storage Services

### Block Storage: Amazon EBS



### FIle Storage Overview

#### File Storage: EFS

#### File Storage: FSx for Lustre

#### File Storage: Amazon FSx for Windows File Server

#### File Storage: Amazon FSx for NetApp ONTAP

#### File Storage: Amazon FSx for OpenZFS

### Object Storage: Amazon S3









