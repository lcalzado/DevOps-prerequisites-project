# Welcome to this DevOps prerequisites project

## Introduction

This project is a LAMP stack application using Linux, Apache, Mysql and Php.
It is a final work part of a DevOps prerequisites course developed by KodeKloud.
Here we put in practice the most important skills and must have knowledge 
before deep dive into the DevOps world.

The original project was deployed on CentOS linux distribution but I adapted, deployed and tested
on Ubuntu server 24.04

**Note:** All the code and files are provided by KodeKloud
Here is the public repo: https://github.com/kodekloudhub/learning-app-ecommerce.git


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

```

Update the working dir

```
sudo rm -rf /var/www/html/*
sudo git clone https://github.com/lcalzado/DevOps-prerequisites-project.git /var/www/html/
```

Update the index.php

The index.php given is attempting to connect to 172.20.1.101 ip address
but since we have configured the database on the same host we have to replace
the value for 'localhost' so the fromt end can connect successfully to the database.
```
<section class="best_business_area row">
            <div class="check_tittle wow fadeInUp" data-wow-delay="0.7s" id="product-list">
                <h2>Product List</h2>
            </div>
            <div class="row it_works">
              <?php

                        $link = mysqli_connect('172.20.1.101', 'ecomuser', 'ecompassword', 'ecomdb');
```

You can modify that with the following command:
```
sudo sed -i 's/172.20.1.101/localhost/g' var/www/html/index.php
```

Reload the service

```
sudo systemctl reload apache2
```

Test
```
sudo curl http://localhost
```
