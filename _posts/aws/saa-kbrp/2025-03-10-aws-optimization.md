---
layout: post
title:  "AWS Solution Optimization: ELB and Auto Scaling"
date:   2025-03-10
categories: [aws]
tags: [cloud, optimization, notes]
---

To handle demand it's possible to automate the scaling of our solutions. Scaling manually is not sustainable as spinning instances up instances and down is repetitive and time consuming. Also, managing replication and redirection of requests manually can get very complex very quickly. 

To solve these two problems we have two solutions:

- For scaling EC2 instances there's a service called Amazon EC2 Auto scaling. 

- For redirection to access the different instances we need something better that the different IP addresses as this does not allow us to handle the dynamic spin-up and spin-down of our instances. Instead, we need to use a Elastic Load Balancer.

### **Elastic Load Balancing**

The ELB sits between the Internet Gateway and the subnets inside our VPC.

ELB is highly available and a regional service meaning its replicated throughout AWS regions. 

ELB is managed in the EC2 console. 

ELBs can be internal (to route traffic inside the VPC) or internet-facing. 

There's different load balancers available:

- Application Load Balancer:
    - used to redirect HTTP/HTTPS traffic
    - operates on the Application Layer, Layer 7 of the OSI Model
    - 3 components:
        - Listener: checks for requests. Needs a port and protocol (ex. 80 and HTTP)
        - Target group: type of backend to direct traffic to (EC2, IPs, Lambda functions). Each resource needs a health check to allow the ALB to verify the resource is available before sending traffic to it.
        - Rule: define how requests are routed to the targets.
    - can respond with fixed responses and redirects.
    - can authenticate users using OIDC, SAML, LDAP, Microsoft AD and other protocols.
    - access can be restricted via security groups (similar to instances)

- Network Load Balancer
    - used to handle TCP/UDP/TLS traffic.
    - operates on Layer 4 of the OSI model.

- Gateway Load Balancer
    - used to redirect between IPs, even between cloud and on prem servers (called Hybrid Mode)
    - operates on layer 3 and 4 of the OSI model.


### **Amazon EC2 Auto Scaling**

Auto Scaling allows to automatically add and remove EC2 instances using user-defined scaling policies.

Auto Scaling is especially useful if we are using a horizontal scaling approach, meaning we deploy more identical instances to meet demand. Vertical scaling on the other side means increasing instance size of the one instance running the app. The vertical approach has an upper limit, the horizontal limit doesn't.

Auto Scaling has 3 main components:

- **Launch Template or Configuration**: configure all the parameters needed to define the EC2 instances that are going to be deployed (AMI, instance type, security group, volumes, etc). Launch templates support versioning.

- **Auto Scaling Group**: used to define where Auto Scaling deploys resources. Here users specify VPCs and subnets where the instances are going to be launched. Here the user can also decide whether to use On-Demand or Spot instances.

- **Scaling policies**: there are 3 types of scaling policies:

    - **Simple Scaling Policy**: use a CloudWatch alarm to add or remove instances. Only has one step, meaning it can only have one condition like "if CPU utilization is above 65%, add X instances".

    - **Step Scaling Policy**: same as above but has multiple steps like "if CPU utilization is above 65% add X instances and if above 85% add 2X instances".

    - **Target Tracking Scaling Policy**: scales instances based on a target value of a specified metric, for example average CPU utilization and deploys or spins down instances to follow the specified target metric. 




