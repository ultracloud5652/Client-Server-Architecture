# CLIENT-SERVER-AECHITECTURE USING A MySQL RELATIONAL DATABASE MANAGEMENT SYSTEM

## Client-Server Architecture

Client-server architecture is an architecture of a computer network in which many clients (remote processors) request and receive service from a centralized server (host computer). Client computers provide an interface to allow a computer user to request services of the server and to display the results the server returns. Servers wait for requests to arrive from clients and then respond to them. Ideally, a server provides a standardized transparent interface to clients so that clients need not be aware of the specifics of the system (i.e., the hardware and software) that is providing the service. Clients are often situated at workstations or on personal computers, while servers are located elsewhere on the network, usually on more powerful machines. This computing model is especially effective when clients and the server each have distinct tasks that they routinely perform. In hospital data processing, for example, a client computer can be running an application program for entering patient information while the server computer is running another program that manages the database in which the information is permanently stored. Many clients can access the server’s information simultaneously, and, at the same time, a client computer can perform other tasks, such as sending e-mail. Because both client and server computers are considered intelligent devices, the client-server model is completely different from the old “mainframe” model, in which a centralized mainframe computer performed all the tasks for its associated “dumb” terminals.

Client Server Architecture

![client-server architecture](https://user-images.githubusercontent.com/117458922/218978909-1f96cac3-4d01-4e53-b5d9-9d054d0ff7ea.png)

The client/server architecture is about dividing up application processing into two or more logically distinct pieces. The database makes up half of the client/server architecture. The database is the “server”; any application that uses that data is a “client.” In many cases, the client and server reside on separate machines; in most cases, the client application is some sort of user-friendly interface to the database.

A graphical representation of a simple client/server system.

![client-server architecture](https://user-images.githubusercontent.com/117458922/218984343-f04ab40a-30e6-494f-9533-0e1e69fb06e1.png)

## Lets take a very quick example and see Client-Server communicatation in action.
* We open up out terminal and install *curl* if it doesnt exist.

```
sudo apt -y install curl
```

## In this example, the linux terminal will be the client, while www.propitixhomes.com will be the server

* Send a request from client (Linux Terminal) with the *curl* command below


```
curl -Iv www.google.com
```

## We should see the response from the remote server in below output.

![Screen Shot 2023-02-15 at 10 32 31 AM](https://user-images.githubusercontent.com/117458922/218989092-1e148a03-3d0d-4071-8577-35fb71ae2066.png)

# In this project we will be Implementing a Client Server Architecture using a Database Management System (MySQL).

**The instructions below will be followed to complete the project.**

* We are going to configure 2 new Linux servers in our Virtualbox

```
Server A - mysql server
Server B - mysql client
```

* On mysql server Linux Server, we will install the MySQL software.

```
sudo apt install mysql-server -y
```

When the installation is finished, log in to the MySQL console by typing:

```
sudo mysql
```

* It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

![Screen Shot 2023-02-15 at 12 43 36 PM](https://user-images.githubusercontent.com/117458922/219026084-d00f3fdc-9636-4478-8123-cd44243183b1.png)

* Now, we need to configure our mysql server installation using this command

```
sudo mysql_secure_installation
```

![Screen Shot 2023-02-15 at 12 44 37 PM](https://user-images.githubusercontent.com/117458922/219026254-1bae7415-5625-4de7-bcdb-143917ff4d60.png)

![Screen Shot 2023-02-15 at 12 44 49 PM](https://user-images.githubusercontent.com/117458922/219026345-65fcb969-c40f-4474-b05d-88283fc98af2.png)

* To test that our mysql server installation is successful we use this command:
 
 ```
 sudo mysql -p
 ```
 
 Created a user on the mysql server with the following command:
 
```
 mysql> CREATE USER 'krispie'@'%' IDENTIFIED WITH msql_native_password BY 'your_password';
```
```
mysql> CREATE DATABASE ultra_db;
```
```
mysql> GRANT ALL ON ultra_db.* TO 'krispie'@'%' WITH GRANT OPTION;
```
```
FLUSH PRIVILEGES;
```

We should see the output below;

![Screen Shot 2023-02-15 at 12 58 23 PM](https://user-images.githubusercontent.com/117458922/219029313-a2f615aa-410c-4ef6-bc3b-0d6b19b894b5.png)

* On the mysql Client Server, we will install the MySQL client software;

```
sudo apt install mysql-client -y
```

* By default, both of your EC2 virtual servers are located in the same local virtual network, so they can communicate to each other using local IP addresses. Use mysql server's local IP address to connect from mysql client. MySQL server uses TCP port 3306 by default, so you will have to open it by creating a new entry in ‘Inbound rules’ in ‘mysql server’ Security Groups. For extra security, do not allow all IP addresses to reach your ‘mysql server’ – allow access only to the specific local IP address of your ‘mysql client’.

Use this command to get IP Address details of the client_server;

```
ip addr show
```

![Screen Shot 2023-02-15 at 12 39 53 PM](https://user-images.githubusercontent.com/117458922/219030161-8af1e188-a1b5-4fff-820d-554be248833c.png)

* Then, use the ip address to edit inbound rule of the db_server as shown below;

![Screen Shot 2023-02-15 at 11 47 22 AM](https://user-images.githubusercontent.com/117458922/219031052-6d940109-93c9-439d-b803-fd5f3607a173.png)

* You might need to configure MySQL server to allow connections from remote hosts. Use the following command;

```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

Replace ‘127.0.0.1’ with ‘0.0.0.0’ like this:

![Screen Shot 2023-02-15 at 12 59 47 PM](https://user-images.githubusercontent.com/117458922/219031526-cb977ba8-dfe4-41e4-9a83-d24f5b1d0327.png)

* From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH. We must use the mysql utility to perform this action with the following command;

```
mysql -u krispie -h IP-address -p
```

* Check that you have successfully connected to a remote MySQL server and can perform SQL queries:

```
Show databases;
```

If everything works correctly, we should see something like this;

![Screen Shot 2023-02-15 at 1 08 46 PM](https://user-images.githubusercontent.com/117458922/219033182-1ea06bb6-ac30-4d6d-b1f2-0f04d4a7cdd1.png)
