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

Load the product inventory into the database

cat > /db-load
USE ecomdb;

CREATE TABLE products 
  (
  id mediumint(8) unsigned NOT NULL auto_increment,
  Name varchar(255) default NULL,
  Price varchar(255) default NULL, 
  ImageUrl varchar(255) default NULL,
  PRIMARY KEY (id)
  ) 
  AUTO_INCREMENT=1;

INSERT INTO products 
  (Name,Price,ImageUrl) 
  VALUES 
  ("Laptop","100","c-1.png"),
  ("Drone","200","c-2.png"),
  ("VR","300","c-3.png"),
  ("Tablet","50","c-5.png"),
  ("Watch","90","c-6.png"),
  ("Phone Covers","20","c-7.png"),
  ("Phone","80","c-8.png"),
  ("Laptop","150","c-4.png");


