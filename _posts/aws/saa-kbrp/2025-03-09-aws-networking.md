---
title: "AWS Networking: VPCs, route tables, internet gateway, ACLs and security groups"
layout: post
date: 2025-03-09
categories: [aws]
tags: [cloud, security, networking, notes]
---

AWS is made of a ton of different services and resources. These resources need to talk to each other. How? Via networks of course, just like any other resource on the internet.

So, how does AWS Networking actually work?

AWS resources talk to each other through VPCs, **Virtual Private Clouds**.

These are virtual networks that connect resources together and are defined by defining an IP range, a list of IP addresses, using CIDR notation.

When starting a new account on AWS, a default VPC is provided. This VPC is okay to get started but makes EVERYTHING publicly accessible by default, so it probably isn't the best solution. 

VPCs can be easily created in the AWS console and can be divided into **Subnets**, which are subsets of the VPC itself. 

Subnets are defined by **IP ranges**, which are lists of IP addresses, which must be subsets of the IP range of the VPC (since these subnets are inside the VPC it makes sense that they include only IP addresses that are already in the VPC, like a russian matrioska).

When creating a new VPC, it is not accessible via the internet by default.

To make a VPC accessible via the internet, two things need to happen:

- You need to attach an Internet Gateway to the VPC via the AWS console.

- You need to create a route table to link the subnets in the VPC to the internet gateway. If you don't have any subnets, and all your resources are in the VPC at the "root" level, then attaching the internet gateway will be sufficient. However, this is not recommended, as some resources shouldn't be accessible via the internet, but only by other resources in the VPC, such as databases.


