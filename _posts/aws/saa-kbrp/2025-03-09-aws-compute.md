---
title: "Intro to AWS Compute Options: EC2, ECS, EKS, Fargate, Lambda"
layout: post
date: 2025-03-09
categories: [aws]
tags: [cloud, computing, notes]
---

AWS has got many different compute options:

- **EC2 or Elastic Compute Cloud**: this is the VM offering of AWS. VMs are virtual computers running in the cloud. Basically like running a server at home, but with the benefits of the cloud: scalability, availability, low overhead, no maintenance, and pay-as-you-go pricing. 

- **Container Services: ECS and EKS**. These are services to run Docker containers on AWS. 
    - With ECS the containers run on a cluster of EC2 instances (VMs), for which the user is responsible for provisioning, 
    - with EKS they run on a Kubernetes cluster, managed by AWS.
    
- **Serverless: Fargate, Lambda**. 

    Serverless is a type of service where the user only has to maintain the application and everything else is managed by AWS, from the OS up all the way to updates, patches, scalability, availability, and so on.

    It's a turnkey solution to deploy applications to the cloud.
    
    The beauty of serverless is that the resources are used only when the application is called from the user, which is completely different from EC2 or ECS/EKS, where the underlying layers is still a "server", meaning a group of resources which run continuously and you pay for by the hour. 
    
    With serverless this is turned on its head and the resources are only used (and paid for) when the app is called for by the user (i.e when the user visits the app url).

     - **Fargate** is a serverless container service completely managed by AWS: choose the container and deploy it. That's it. It works with both ECS and EKS and basically sits on top of it handling the provisioning and scaling of the EC2 instances (for ECS) and cluster (for EKS).

     - **Lambda** is a serverless compute service: upload the code and it will run every time it is called, but not when it isn't. This is a great choice for services that need to run only when certain things happen (for example: "resize an image when the user uploads it").

This is just a brief overview. I'll maybe go into more detail in later posts.
