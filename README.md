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

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e447c47041b7fcb9b0cdd2f6502e112fab8b969e/img/Create%20Public%20Route%20Table.png)

Add Internet Route

Edit Routes → Add Route

Destination	Target

0.0.0.0/0      	Internet Gateway

Select:

ThreeTier-IGW

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/6c71f1265c36973c0c4c3f20700736525b7f70ce/img/Add%20Internet%20Route.png)

Associate Public Subnets

Subnet Associations → Edit

Select:

•	Public-Subnet-1 

•	Public-Subnet-2

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/8e69a29a9972c5d6e9cd275d14dfec6915b39223/img/Associate%20Public%20Subnets.png)

Now public subnets can access internet.

# STEP 7 — Create Elastic IP

NAT Gateway requires Elastic IP.

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/ff58bbaafeffd33ae4c32267d459ddceb7febebd/img/Create%20Elastic%20IP.png)

# STEP 8 — Create NAT Gateway

Private servers need internet for:

•	Updates 

•	Package installs 

But should remain private

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/08807e029b1e7d4a894565ff5b2452a3ddc2a6da/img/Create%20NAT%20Gateway.png)

# STEP 9 — Create Private Route Table

Private subnet traffic should go through NAT.

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/c7780f533d87c04ad02d2b02083a6c547852bdfb/img/Create%20Private%20Route%20Table.png)

Add Route

Destination	Target

0.0.0.0/0      	NAT Gateway

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/35b2a16b8b708b0f89526637ce684856a1fe33f3/img/Add%20NAT%20Route%20.png)

Associate Private Subnets

Select:

•	Private-App-1 

•	Private-App-2 

•	Private-DB-1 

•	Private-DB-2

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/a9c45e3276caab88cb6784ae2d85fe94c3804259/img/Associate%20Private%20Subnets.png)

# STEP 10 — Create Web Security Group

Purpose

Allows:

•	User traffic 

•	SSH

Create SG

Add Rules

Type	    Port      Source
HTTP	    80	      Anywhere
HTTPS	    443	      Anywhere
SSH	      22	      Anywhere

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e399b3bbf3e527d883e5fb4a85ef800fe4eff70d/img/Create%20Web%20Security%20Group.png)








