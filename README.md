# DevOps-prerequisites-project

## Introduction



### Install and configure the database.

```
sudo apt update
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb
```


Configure the database.

```
sudo mysql
Mariadb[none]> CREATE DATABASE ecomdb;
Mariadb[none]> CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
Mariadb[none]> GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
Mariadb[none]> FLUSH PRIVILEGES;
```

Load the product inventory into the database. 
The file is on assest directory within this repository

```
sudo mysql < db-script.sql
```

It creates a table call 'products' and insert data on it.
The db-script file contains the below sql query:

```
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
```

Validate the information has been added.

```
sudo mysql
Mariadb[none]> SHOW databases;
Mariadb[none]> USE ecomdb;
Mariadb[none]> SHOW TABLES;
Mariadb[none]> SELECT * FROM products;
```

### Deploy and configure the web service

Install the apache and php packages

```
sudo apt update
sudo apt install -y apache2 php php-mysql libapache2-mod-php
```

Configure apache

```
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

Download the source code

```
sudo apt update
sudo apt install -y git
sudo git clone 
