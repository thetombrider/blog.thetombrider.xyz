---
title: "Deep Dive on AWS Compute Services"
layout: post
date: 2025-03-11
categories: [aws]
tags: [cloud, computing, notes]
---
### Comparison between AWS Compute options

### EC2

**Amazon EC2** offers granular control for managing your infrastructure. It gives you the choice of over 500 instance types, with the latest processors, storage, OSs, and networking. An EC2 instance is a virtualized server running in the cloud. Whatever options you customize for a physical server can also be customized for EC2 instances. Amazon EC2 also offers instances that are optimized for certain performance needs or workload functions. Therefore, your applications can start on an instance built to accommodate that workload type.

EC2 offers granularity of control because, being a VM, the user can control everything about it.

EC2 also offers high availability, and many combinations of compute, storage and IOPS to choose from. Also, it is entirely possible to change instance types to increase capacity as an app grows.

EC2 is the most versatile option, but also the one that requirest the most management, configuration and administration.

### Containers

**Containers** provide a standard way to package your application's code, configurations, and dependencies into a single object. Containers share an OS installed on the server and run as resource-isolated processes, for quick, reliable, and consistent deployments, regardless of environment.

Containers provide portability because, being self-contained, they run the same on any host.

Containers have no latency on startup, and have no size limit.

Containers are particularly suitable for the following use cases:

- Compute intensive apps
- When breaking down monoliths in microservices
- When scalability is a priority
- When you need to quickly deploy an on-prem app to the cloud without altering the code

Beware of apps that need persistent storage: these are less suitable for containers, as if you move the container you need to reconfigure storage. This is because storage either lives inside the container, but then is lost every time the container is terminated, or lives outside, in a volume, but then needs to be moved as well when moving the container to a different OS or host.

### Serverless

One of the major benefits of cloud computing is its ability to abstract (hide) the infrastructure layer. Therefore, you don't need to manually manage the underlying physical hardware. In a serverless environment, the abstraction is one layer higher. Not only is the physical infrastructure abstracted, but the instances and the operating systems on which AWS Lambda is running, are also abstracted. With this higher level abstraction in place, you can focus on the code for your applications without spending time building, maintaining, and patching the underlying infrastructure, hosts, and operating systems.

When to choose serverless services like Lambda:

- When the app is not compute intensive
- When runtime is less than 15 minutes
- When your code needs to interact with other AWS services

### Other Compute Services

### Step Functions

**Step Functions** is a managed service used to coordinate the components of distributed applications and microservices using a visual workflow editor. You can connect small apps that perform small discrete tasks together in complex workflows. Step Functions are smart, meaning they have auto-retry on errors and logs to inspect when things go wrong.

### AWS Batch

**Batch computing** is the running of a program without manual intervention, meaning that the input parameters are defined through scripts.

AWS Batch is the batch management offering of AWS. It is useful to run hundreds of thousands of batch computing jobs on AWS. AWS batch provisions the necessary infra based on the volume and resource requirements of the batch jobs defined by the user (CPU, memory, storage)

AWS Batch plans, schedules and runs batch computing workloads using EC2 or Fargate or Fargate Spot.

### AWS Elastic Beanstalk

**Elastic Beanstalk** is a tool that delegates deployment completely to AWS. Users can only upload their application code and AWS does everything else (provisioning, load balancing, auto-scaling, monitoring).

Users can then specify other parameters such as VPCs to further customize their setup.

There is no additional charge to Elastic Beanstalk, you only pay for what you use at the compute level.

This makes it ideal to quickly deploy APIs, backend servers, microservices or even entire web applications.

Elastic Beanstalk supports all major programming languages.

### Amazon Lightsail

**Lightsail** is a managed VPS service, meaning that it provides the user compute storage and networking needed to deploy and maange web apps in the cloud. Lightsail bundles all these things up in a fixed monthly price. This makes it similar to services like Digital Ocean Droplets. You only choose which app to host and which resource combo to host it with and AWS does the rest, all for a fixed monthly price.

### How to choose between compute options? - For Startups

When starting out, the best compute option is the one that allows you to move the fastest to validate market demand for your application.

#### Example 1 - Starting from Scratch

To quickly prototype serverless is probably the best solution: no management and infite scalability so that the team can focus on business logic and features.

#### Example 2 - Team already working with Containers

Use ECS with Fargate so you only need to define compute and memory requirements.

#### Example 3 - Existing monolith

Use Elastic Beanstalk as it will make it easier to just upload the application and automate deployment. This will make deployments fast without giving up control on the infrastracture.
