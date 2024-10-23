# Database Management with Amazon RDS (Relational Database Service)

In this project, we will go through the practical process of creating an AWS RDS database, connecting it to an EC2 instance, and accessing the contents of the database and its tables.

### Goals:

- Help a company manage its expanding data needs with a reliable database solution.

- Teach how to set up and manage databases using Amazon RDS.


### Learning Outcomes: 

-  Develop hands-on expertise in creating and setting up scalable databases using Amazon RDS.

- Understand the importance of managing client data and project details

- Learn to navigate and utilize the AWS Management Console for efficient database setup.

- Discover essential database security and user access control.

- Practice troubleshooting and optimizing database performance.

### *Lets explain a few terms:*

### What is a database?

A database is like a digital filing cabinet where all kinds of information can be stored. Databases are designed to store, manage, and provide access to large amounts of data.

### What is database management?

Imagine your data is a precious garden. Database management is the process of nurturing and tending to that garden, ensuring it remains healthy, organized, and productive.
It is all about making sure the information in the database is well-organized, secure and easy to access.

### What is Database management system? 

Database management system is a toolbox that is used  to manage and organize the database. Its just like having a toolbox that you use to nurture and care for you garden.

### Relational database management systems(RDBMS)

A Relational Database Management System (RDBMS) is a type of database management system that organizes data into tables with well-defined relationships between them.

*Let's move on to the implementation phase:*

1. Locate the search bar on the AWS console

a) Type "RDS" in the search bar, when it comes up,click on it.
![](./RDS/1a.%20RDS.png)

b) Once another page comes up, locate "Databases" and click on it.

![](./RDS/2a.png)

c) Select "Standard Create" as the database creation method.

![](./RDS/3.png)

d) Select the "MySQL" engine.

![](./RDS/3a.png)

e) Select the latest engine version or any one you prefer.

- Go ahead and select the "free tier template"

![](./RDS/3b.png)

f)  Type in your DB instance name.

![](./RDS/3d.png)

g) Type in a master username of choice

h) Select the credentials management as "Self managed"

i) Enter the master password for the database and confirm it by re-typing it in the "Confirm master password" field.

![](./RDS/3e.png)

#### *Note*
Make sure to save the username and password you entered in a safe place. Misplacing or loosing them could result in being unable to access the database you've created.

j) Choose DB instance class as "db.t3.micro."

![](./RDS/3f.png)

k) Do well to maintain the default setting for the other configurations.

![](./RDS/3g.png)

l) Choose the VPC you have created in the project or choose your VPC with proper configurations

![](./RDS/3h.png)

m) Select the "Public access" as "yes".

#### *Note -* 
It's not a recommended practice to keep your database public, but for the purpose of this exercise,we'll be configuring it as public.

n) For "VPC security group (firewall)" select the "Choose existing".

o) Go ahead and choose your pre-created security group in the "Existing VPC security groups" section.

![](./RDS/3i.png)



p) Choose any of the Availability zones.

![](./RDS/3j.png)

q) Leave the other settings as default

![](./RDS/3k.png)

r) Go ahead and click on  "Create database"

![](./RDS/3l.png)


2.If you receive an error message indicating that your VPC does not support DNS resolution, DNS hostname, or both, please locate the VPC in question, update its settings, and try again

![](./RDS/3m.png)

a)To resolvethis error start by locating your VPC.

![](./RDS/3n.png)

b) Click on your VPC

c)Click "Action

d) Select "Edit VPC settings"

![](./RDS/3o.png)

e) Make sure to enable both the DNS resolution and DNS hostnames and then click "Save"

![](./RDS/3p.png)

f) RDS successfully created.

![](./RDS/3q.png)

#### *Note -* 
Ensure that the security group attached to your database permits inbound traffic on port 3306.

If the security group is not configured, set it up by selecting the attached security group and add an inbound rule for MySQL/Aurora on port 3306, allowing traffic from the 0.0.0.0/0 CIDR range.

3. Let's go ahead and edit.

a) Locate the security group attached to your database

![](./RDS/4a.png)

b) Select "Inbound  on port 3306rule" then click "edit inbound rule"

![](./RDS/4b.png)

c) Click the "add rule button".
![](./RDS/4c.png)

d) Select the MYSQL/Aurora, allowing traffic from 0.0.0.0/0. Then click "save"

![](./RDS/4e.png)

4. Moving on, select the database you just created. Scroll down and on the right side, you will find an endpoint. Copy the endpoint.

![](./RDS/4f.png)

a) Save this endpoint along with your username and password in a safe place.

![](./RDS/4g.png)

5. We have already created an EC2 instance with an Amazon Linux image.

![](./RDS/6a.png)

a) Connect to the instance and the execute the following commands:

```
sudo wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm

```

![](./RDS/6b.png)

b) 

```
sudo yum localinstall mysql57-community-release-el7-11.noarch.rpm
```

![](./RDS/6c.png)

#### *Note* 
Whenever prompted, please inpute "yes" or "no", type y for yes.

![](./RDS/6d.png)

c) 

```
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```

![](/RDS/6cc.png)

d) 
```
sudo yum install mysql-community-server
```

![](./RDS/6e.png)

![](./RDS/6f.png)

e)
```
sudo systemctl start mysqld.service

sudo systemctl enable mysqld.service

status mysqld.service
```

![](./RDS/6g.png)

#### *Note-* 

Press "q" to quit after running the status command.


6.Finally! Itstime to connect your RDS to your ec2 instance.

#### mysql-h [Endpoint] -P [Port] -u [Username] -p[Password]

a) Make sure to execute the commands according to your database setup.

![](./RDS/6hh.png)

```
mysql -h first-rds-database.c9ua2ig4a7zx.eu-north-1.rds.amazonaws.com -P 3306 -u admin -pCampus22
```

#### Note-

Please make sure the -P after enpoint is in "CAPS". Another point to note is to make sure there are no spaces between "-p" and your password. If your password is "Campus22" It should be written as "-pCampus22". 

![](./RDS/6i.png)

b) To view all databases, run:

```
SHOW DATABASES
```

To use the database you have created, execute:

```
USE mysql;
```

c) If you want to show tables inside the database,

```
SHOW TABLES;
```


Congratulations! Database has been successfully set up and connected to the EC2 instance.















