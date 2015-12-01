# docker-bamboo-server

Atlassian bamboo server, version 5.1.37

This repository builds a docker container for the Atlassian Bamboo server with the
MySQL JDBC driver pre-installed.  It is suitable for production use.

## Getting Started

### Prerequisites

Make sure you have the following installed before continuing these instructions:

* docker 1.9.1
* docker-compose 1.5.1

### Simple launch

#### 1. launch containers 

```
docker-compose up -d
```

This command will launch containers in daemon mode so they continue running even
after you've closed the shell that launched them.  Without the ```-d```, the 
containers run interactively, so if you close the shell or hit ctrl-c, the containers
will be stopped.

#### 2. create mysql database

```
docker exec -it $(docker-compose ps | grep mysql | awk '{print $1}') /bin/bash 
```

This command uses ```docker-compose ps``` to find the mysql container and exec the
```/bin/bash``` command into it.  

Once inside the mysql container, execute the mysql command line as follows:

```
mysql -u root -ppassword
```

Once you've launched the command line for mysql, execute the following sql as per
the [Atlassian Bamboo documentation](https://confluence.atlassian.com/bamboo/mysql-289276817.html)

````
CREATE USER bamboo;
CREATE DATABASE bamboo CHARACTER SET utf8 COLLATE utf8_bin;
GRANT ALL PRIVILEGES ON bamboo.* TO 'bamboo'@'%' IDENTIFIED BY 'password';
```

### 3. open browser to port 8085 on your docker host

And follow the instructions to complete the installation of bamboo.

* The database has the following configurations:
    * username - ```bamboo```
    * password - ```password```
    * url - ```jdbc:mysql://mysql:3306/bamboo?autoReconnect=true```
* The name of the database host is mysql and it's port is 3306.
* In most cases, the default directories provided should be sufficient
* You may need to obtain a license from Atlassian to use bamboo

### 4. You should be good to go
 
## What's Inside the Bamboo Server Container
 
The bamboo-server container is intended to provide a minimal base installation 
 for bamboo and contains the following:
 
* Oracle Java 8
* Atlassian Bamboo 5.1.37
* MySQL JDBC drivers pre-installed
* Bamboo data directory has been pre-configured

The docker-compose script is intended to simplify the process of deploying bamboo to 
any host.

## Things to Note

The configuration provided by docker-compose configures a number of useful properties
for bamboo:

* The bamboo data directory will be mounted on the docker hosts as ```/bamboo/bamboo-data```
* The mysql data directory is mounted on the docker host a ```/bamboo/var/lib/mysql```
* Taking a snapshot of the ```/bamboo``` directory is essentially backing up the system
 
