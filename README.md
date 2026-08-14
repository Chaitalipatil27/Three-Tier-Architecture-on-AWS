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

Create App Security Group

Purpose

Allows traffic only from web server.

Add Rule

Type	   Port	      Source

TCP  	   8080	      Web-SG

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/27d575d73649d208feceb7bf071d280b31ad6ebc/img/Create%20App%20Security%20Group.png)

Create DB Security Group

Purpose

Only app server accesses DB.

Add Rule

Type	  Port	  Source

MySQL	  3306	  App-SG

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/b257a203f1668b5911ca7d58fa6646ea25b96d1c/img/Create%20DB%20Security%20Group.png)

# STEP 11 — Launch Web EC2

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e62cd92ff8055ae02c18764a0d8b505f7429bd6f/img/Launch%20Web%20EC2.png)

# STEP 12 — Connect Web Server

Using Git Bash:

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/b46dd70bd4c2de4e797c2ea557215a5d1a120c80/img/Connect%20Web%20Server.png)

# STEP 13— Install Apache

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/8f539b112d7539b890583ec997c52e8ac9ab3f20/img/Install%20Apache.png)

Start Apache

systemctl start httpd

systemctl enable httpd

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/7578abf170b33fd2972a514b8d70a6c3cdef9ea5/img/Start%20and%20Enable%20apache.png)

# STEP 14— Deploy Frontend Website

Go to:

cd /var/www/html

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/86d4fc1daadffa9247ed1f04335e9ecdb5b69ee6/img/Go%20to%20var.www.html.png)

Create HTML File

vi index.html

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/8564858539de64ae1c94a089dc78169a3f7a57be/img/Create%20HTML%20File.png)

Add:

<h1>Welcome to AWS Three Tier Architecture</h1
                                            
Save file.

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/28230b92b7acb13b87e3dafe509cc44c575ae3e5/img/Save%20file..png)

# STEP 15— Test Website

Open browser:

Hit Public-IP

Website opens.

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/b36d5e46d9e1ba5b4803dc68d9bc599d5eddc377/img/Test%20Website.png)

# STEP 16— Launch App EC2 for DEPLOY APPLICATION LAYER

Place inside:

•	Private subnet 

Configuration

Option	  Value
	
Subnet   	Private-App-1

Public    IP	Disable

SG	      App-SG

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/e1682b8c734214f3c8ac8fccc5cb96f3e131b011/img/Launch%20App%20EC2%20for%20DEPLOY%20APPLICATION%20LAYER.png)

# STEP 17 — Connect App Server

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/5482fb8e269944e2da6789de3b93325668605dc9/img/Connect%20App%20Server.png)

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/ea28a6b5f3c381e9bac9c70ef5454bb4933af07d/img/Connect%20app%20server%202.png)

# STEP 18— Install NodeJS

curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
(This command is used to prepare the server for installing Node.js 18)

sudo yum install nodejs -y

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/c58b183a11c563ac7581e1c67947e8057e700723/img/Install%20NodeJS.png)

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/13a2b44a1a8a0b8a89f3249260f00aab7202f46c/img/nodejs%20installation.png)

# STEP  19— Create Backend App

mkdir app

cd app

nano app.js

# Add Backend Code

const http = require('http');

const server = http.createServer((req,res)=>{

res.write("Backend Running");

res.end();

});

server.listen(8080);

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/96a4cdf7ef35a66fcc5f2dc1e79c5d65dc1ffcf8/img/Create%20Backend%20App.png)

# STEP 20 — Test Backend

From Web Server:

curl http://APP-PRIVATE-IP:8080

Output:

Backend Running

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/30aaa934b324b5f47cc5edc4e1c204e78068d058/img/Test%20Backend.png)

Its not show output on this new terminal open new terminal

Terminal	     Purpose

Terminal 1	   Run backend

Terminal 2	   Test backend

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/dcce7e8f8802852513477cb313b13828ec7b4962/img/open%20new%20terminal%20%20.png)

# STEP 21— DATABASE LAYER Create RDS

Choose

Option	                Value

Engine	                MySQL

Public Access	        No

Security Group	        DB-SG

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/710a4fef966055a5dd35a1c7d6027cda22e65c4d/img/DATABASE%20LAYER%20Create%20RDS.png)

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/8738b9cb93c621afcc7371446c4ed48bb1ee9843/img/Public%20Access.png)

# STEP 22 — Connect Database

From App Server:

mysql -h database-2.cotq24mgo12g.us-east-1.rds.amazonaws.com -u admin -p

password

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/1f05736f6befd4fc69fcec341618db2160514724/img/Connect%20Database.png)

Show database

SHOW DATABASES;

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/595c8b45d0d02fb48dbb90526e8349ff9f05f6a2/img/Show%20database.png)

Create Database

CREATE DATABASE company;

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/595c8b45d0d02fb48dbb90526e8349ff9f05f6a2/img/Create%20Database.png)

Create Table

CREATE TABLE users(

id INT,

name VARCHAR(50)

);

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/595c8b45d0d02fb48dbb90526e8349ff9f05f6a2/img/Create%20Table.png)

INSERT INTO users VALUES(1,'chaitali');

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/595c8b45d0d02fb48dbb90526e8349ff9f05f6a2/img/INSERT%20INTO%20.png)

# STEP 23— LOAD BALANCER (Create Target Group)

Add:

•	Web EC2 instances

Target group

![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/86eb4b8647484345892f065532c59686bc916378/img/Target%20group.png)

# STEP 24— Create Application Load Balancer

Configuration

 Option     	 Value

 Type	         Internet-facing

 Subnets	     Public Subnet

 Attach:

 Target Group

 ![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/86eb4b8647484345892f065532c59686bc916378/img/Create%20Application%20Load%20Balancer.png)

 ![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/86eb4b8647484345892f065532c59686bc916378/img/Load%20balncer%20created.png) 

 ![image alt](https://github.com/Chaitalipatil27/Three-Tier-Architecture-on-AWS/blob/86eb4b8647484345892f065532c59686bc916378/img/Test%20application.png)

 
# The purpose of this project is to build a secure, scalable, and highly available application architecture on AWS by separating the web layer, application layer, and database layer into different tiers using public and private subnets. This improves security, performance, fault tolerance, and manageability.


































