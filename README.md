# Three-Tier-Architecture-on-AWS

# Project Overview:-Designed secure 3-tier architecture using AWS services for scalability, security, and high availability

# STEP 1 :-Create VPC

VPC creates your private AWS network.

Without VPC:

•	Resources cannot communicate properly. 

Create VPC:-

CIDR defines IP address range.

10.0.0.0/16

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/9fb8c8d06c3a90380b4c6f3487a377309b2c1bf6/img/Create%20VPC.png)

# STEP 2 — Create Public Subnets

Public subnet gives internet access.

Used for:

•	Load Balancer 

•	Web Server

Create two public subnet 

With CIDR Rang 

First subnet Rang 10.0.1.0/24

Second subnet Rang 10.0.2.0/24

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e9bee5061e63dd323af91a80fea5aed88445c2a7/img/Create%20Public%20Subnets.png)

# STEP 3 — Create Private App Subnets

Application servers should remain private.

Create two private subnet

With CIDR Rang

First subnet Rang 10.0.3.0/24

Second subnet Rang 10.0.4.0/24

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/67ac845502a01f4d23a4546d7a0e6b28d00e2996/img/Create%20Private%20App%20Subnets.png)

# STEP 4 — Create Private DB Subnets

Database must be highly secure.

Create two private subnet

With CIDR Rang 

First subnet Rang 10.0.5.0/24

Second subnet Rang 10.0.6.0/24

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/59b4a068c583aed87444b3193d37cedbfe440b72/img/Create%20Private%20DB%20Subnets.png)

# STEP 5 — Create Internet Gateway

Internet Gateway allows internet communication.

Without IGW:

•	Public EC2 cannot access internet.

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/b32c00d5985bf04d2fc7ae6ad1fcbc8fd421e0af/img/Create%20Internet%20Gateway.png)

Attach IGW to VPC

Actions → Attach to VPC

Select:

My-vpc-01

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/1ef3b15e0849e3f49319f2c9481f939180b0ddd1/img/Attach%20IGW%20to%20VPC.png)

# STEP 6 — Create Public Route Table

Route table controls traffic

![image alt]()




