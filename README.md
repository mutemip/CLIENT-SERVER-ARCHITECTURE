# CLIENT-SERVER-ARCHITECTURE

PROJECT 5: CLIENT/SERVER ARCHITECTURE USING A MYSQL RELATIONAL DATABASE MANAGEMENT SYSTEM


Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.
![c-s](https://user-images.githubusercontent.com/64135078/196065133-501774e5-933a-43a9-ab4d-af01c2b708b9.png)

Curl -lv http://mutemip.com  - A machine accessing a website using the ‘curl’ command and it sends HTTP requests to the web server.

![more](https://user-images.githubusercontent.com/64135078/196065208-da9e6a83-8822-43a5-abc2-09b24d747c9c.png)

Self study:

Ping: 

Traceroute: A traceroute provides a map of how data on the internet travels from its source to its destination. 
A traceroute works by sending Internet Control Message Protocol (ICMP) packets, and every router involved in transferring the data gets these packets. The ICMP packets provide information about whether the routers used in the transmission are able to effectively transfer the data.


To run traceroute: 
Open instance terminal and write: “traceroute [hostname]”
Difference between ping and traceroute:
Ping tells you if the server is reachable and time it takes to transmit and receive data while traceroute details the precise route info, router by router as well as time it took for each hop.


Step 1:
Create 2 EC2 instances - db-server and client-server
![ec2-ins](https://user-images.githubusercontent.com/64135078/196065265-1232882d-7277-460b-8a50-cf30c9ff7184.png)

Connect to db-server and run update the install mysql-server software
  sudo apt update -y && sudo apt install mysql-server -y
The enable mysql server using: 
  sudo systemctl enable mysql
  ![enable-mysql](https://user-images.githubusercontent.com/64135078/196065338-a00c6d84-058a-42bb-bf2f-85455413e2a3.png)

Step 2:
Connect to client-server and install mysql-client software
sudo apt update -y && sudo apt install mysql-client -y

NB: 
By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.
To get ip address for client server run: ip addr show command

![rule5](https://user-images.githubusercontent.com/64135078/196065382-cc495b70-af92-450e-9e97-33e37b475df9.png)

Important:
Prepare mysql-server instance by running mysql security scripts command: 
sudo mysql_secure_installation and set up right configuration
- login to mysql:
	Create user and database
CREATE USER <username> and CREATE DATABASE <test_db>:

And grant all permissions to the user.

grant all on test_db.* to 'mutemip'@'%' with grant option;


To see available databases run SHOW DATABASES
![test-db](https://user-images.githubusercontent.com/64135078/196065441-46dd611a-b7c8-413e-be2f-cfafe25deda2.png)

To view available table on test-db run:
USE test-db;
SHOW TABLES;

Configure mysql server to allow connection from remote hosts
Replace ‘127.0.0.1’ to ‘0.0.0.0’
![remote-conn](https://user-images.githubusercontent.com/64135078/196065480-0384901c-7c1a-4587-ab61-315641fce7e0.png)

Then restart mysql server: 
Sudo systemctl restart mysql

From the mysql client Linux Server connect remotely to the mysql server Database Engine without using SSH. You must use the mysql utility to perform this action:
sudo mysql -u ‘mutemip’ -h <ip-address of mysql-server> -p

Check successful connection to mysql-server from client-server:
Run: show databases;
![sucess](https://user-images.githubusercontent.com/64135078/196065530-0a77a876-6020-4fe9-a861-42b8e2996107.png)

From here (client-server)… you can see a test_db database which we created in mysql-server of ip: 172.31.94.34 as shown:
![mysql-server](https://user-images.githubusercontent.com/64135078/196065579-6c554c8d-4b14-4945-a74f-74aad3e8674e.png)





