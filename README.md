# DevOps-prerequisites-project

## Introduction

## Deployment Pre-requisites


Install and configure the database

```
sudo apt update
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb
```

Setup the firewall rules for the database

```
sudo ufw allow 3306\tcp
sudo ufw reload
```

Configure the database

```
sudo mysql
CREATE DATABASE ecomdb;
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
FLUSH PRIVILEGES;
```



