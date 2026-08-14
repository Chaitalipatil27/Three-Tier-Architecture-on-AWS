# Three-Tier-Architecture-on-AWS

# Project Overview:-Designed secure 3-tier architecture using AWS services for scalability, security, and high availability

STEP 1 :-Create VPC

Why?

VPC creates your private AWS network.

Without VPC:

•	Resources cannot communicate properly. 

Create VPC:-

CIDR defines IP address range.

10.0.0.0/16

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/9fb8c8d06c3a90380b4c6f3487a377309b2c1bf6/img/Create%20VPC.png)

STEP 2 — Create Public Subnets

Why?

Public subnet gives internet access.

Used for:

•	Load Balancer 

•	Web Server

Create two public subnet 

With CIDR Rang 

First subnet Rang 10.0.1.0/24

Second subnet Rang 10.0.2.0/24

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e9bee5061e63dd323af91a80fea5aed88445c2a7/img/Create%20Public%20Subnets.png)
