---
author: Ash
pubDatetime: 2023-02-03T1:20:00Z
title: Setup a LAMP server in ubuntu
postSlug: setup-a-lamp-server-in-ubuntu
featured: true
draft: false
tags:
  - linux
ogImage: ""
description: How to setup a LAMP server in ubuntu
---

# Setup a LAMP server in ubuntu

- A LAMP server is a web server that uses Linux as its operating system, Apache as its web server, MariaDB or MySQL as its database management system, and PHP as its server-side scripting language. The acronym "LAMP" stands for the components used: Linux, Apache, MariaDB or MySQL, and PHP.
- LAMP servers are commonly used to host dynamic websites and web applications, and are a popular choice due to the ease of setup, low cost, and the availability of a large number of open-source tools and libraries. The combination of these components provides a flexible, scalable, and secure platform for serving web content.

### 1. Install Apache web server

- The Apache web server is an open-source HTTP server that can serve dynamic web pages. You can install it by running the following command in the terminal:

```sh
   sudo apt-get install apache2 -y
```

### 2. Install MariaDB

- MariaDB is a fork of the MySQL database management system, and it is commonly used with LAMP servers. You can install it by running the following command in the terminal:

```sh
   sudo apt-get install mariadb-server mariadb-client -y
```

### 3. Start and secure MariaDB:

- Once MariaDB is installed, start the service and secure it by running the following command:

```sh
   sudo systemctl start mariadb

   sudo mysql_secure_installation
```

### 4. Install PHP:

- PHP is a server-side scripting language that is used to create dynamic web pages. You can install it by running the following command in the terminal:

```sh
   sudo apt-get install php libapache2-mod-php -y
```

### 5. Test the LAMP server:

- To test the LAMP server, create a PHP file named "info.php" in the "html" directory of Apache and add the following code to it:

```sh
     <?php
     phpinfo();
     ?>
```

##### Note:

- If you can’t find the apache2 directory follow these steps to navigate:
- From your root directory enter the following commands

```sh
   cd /etc
   ls  (you should see apache2 folder here)
   cd /var/www/html
   sudo nano /var/www/html/info.php
```

- Inside nano editor paste the php code mentioned above, then hit ctrl+s to save finally ctrl+x to quit nano

- Next get your ip by entering the following command:

```sh
   hostname -I
```

- Copy the ip address and enter the following in web browser of your choice

```sh
   http://your_server_IP/info.php
```

##### If you see a page with information about your PHP installation, your LAMP server is up and running successfully.
