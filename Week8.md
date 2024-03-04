# Installing the Apache Web Server
- background on HTTP server basics [here](https://httpd.apache.org/docs/2.4/getting-started.html)
- Apache: most popular web server application, free open source

Search Apache2 package

```
apt search apache2 | head

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
Sorting...
Full Text Search...
apache2/focal-updates,focal-security 2.4.41-4ubuntu3.15 amd64
  Apache HTTP Server
apache2-bin/focal-updates,focal-security 2.4.41-4ubuntu3.15 amd64
  Apache HTTP Server (modules and other binary files)
apache2-data/focal-updates,focal-security 2.4.41-4ubuntu3.15 all
  Apache HTTP Server (common files)
```
To show more detailed info on package run `show` command

```
apt show apache2

Package: apache2
Version: 2.4.41-4ubuntu3.15
Priority: optional
Section: web
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Apache Maintainers <debian-apache@lists.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 544 kB
Provides: httpd, httpd-cgi
...
```
Installing Apache2

```
sudo apt install apache2

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  apache2-bin apache2-data apache2-utils libapr1 libaprutil1
  libaprutil1-dbd-sqlite3 libaprutil1-ldap libjansson4 liblua5.2-0
  ssl-cert
...
```
Check Apache2 is running w `systemctl` command

```
systemctl status apache2

● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor>
     Active: active (running) since Sun 2024-03-03 21:04:28 UTC; 4min 21s>
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 29443 (apache2)
      Tasks: 55 (limit: 1134)
     Memory: 4.9M
     CGroup: /system.slice/apache2.service
             ├─29443 /usr/sbin/apache2 -k start
             ├─29445 /usr/sbin/apache2 -k start
             └─29446 /usr/sbin/apache2 -k start

Mar 03 21:04:28 main-ubuntu1 systemd[1]: Starting The Apache HTTP Server.>
Mar 03 21:04:28 main-ubuntu1 systemd[1]: Started The Apache HTTP Server.
lines 1-14/14 (END)
```
## Default Apache2 Web Page

- Can view default apache web page on text based browser (w3m) or graphical (chrome)

**Text Bases Browser**

Install w3m 

`sudo apt install w3m`

Install elinks 

`sudo apt install elinks`

Vist default site using local host 

`w3m 127.0.0.1` *or* `w3m localhost`

Both work if returns 

`Apache2 Ubuntu Default Page
It works!`

**Graphical Browser**

Get external IP address from Google Cloud Console > VM instances > click on Exernal IP address > Apache2 Ubuntu Default Page


<img width="400" alt="Screen Shot 2024-03-03 at 4 27 26 PM" src="https://github.com/Obakoush/OBICT690/assets/142951646/299b74af-47c7-47e9-bfa7-1f4d2ab61e88">

## Create a Webpage
- Apache serves web pages by default from document root /var/www/html/
- run `ls` to see doc root has index.html file already

Rename index.html file + create new file
  ```
  cd /var/www/html/
sudo mv index.html index.html.original
sudo nano index.html
```
Command breakdown

```
Navigate to the directory w HTML files CHANGE DIRECTORY TO "/var/www/html/"
Rename the existing 'index.html' to 'index.html.original' RENAME FILE "index.html"
TO "index.html.original" Open nano to create new 'index.html' file
```
Here enter in HTML code 

```
<html>
<head>
<title>My first web page using Apache2</title>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my web site.
I created this site using the Apache2 HTTP server.</p>

</body>
</html>
```
Results in:

<img width="400" alt="Screen Shot 2024-03-03 at 4 50 05 PM" src="https://github.com/Obakoush/OBICT690/assets/142951646/f27a1ca7-4355-4569-a0c3-9e5c5de5fee4">

Personal customization for fun 

```
<html>
<head>
<title>My first web page using Apache2</title>
<style>
body{background-color:lightpink;
color:white;
text-align:center;
font-family:Arial,sans-serif;}

h1{font-size:40px;}

p{font-size:18px;
background-color:#ffc0cb;
padding:10px;}

footer{background-color:#ffc0cb;
color:white;
font-size:14px;
padding:5px;
position:fixed;
bottom:0;
width:100%;}
</style>
</head>
<body>

<h1>Welcome</h1>

<p>Welcome to my web site that I created with Apache2 HTTP server :)</p>
    
<footer>-Oraida</footer>
    
</body>
</html>

```
Result

<img width="400" alt="Screen Shot 2024-03-03 at 5 07 25 PM" src="https://github.com/Obakoush/OBICT690/assets/142951646/7ae4ec6c-9c49-4e4f-a284-d0deedcef410">

View Orginal put `http://34.16.129.98/index.html.original` web adress


# Installing and Configuring PHP

- PHP enhances web functionality, allows server-side scripting

Install PHP 

`sudo apt install php libapache2-mod-php`

Read package details 

```
apt show php libapache2-mod-php

Package: php
Version: 2:7.4+75
Priority: optional
Section: php
Source: php-defaults (75)
Origin: Ubuntu
...
```

Intergate w Apache + restart run

`sudo systemctl restart apache2`

Check for any errors

```
systemctl status apache2
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor pr>
     Active: active (running) since Sun 2024-03-03 22:25:27 UTC; 56s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 37475 ExecStart=/usr/sbin/apachectl start (code=exited, status=>
   Main PID: 37479 (apache2)
      Tasks: 6 (limit: 1134)
     Memory: 9.5M
     CGroup: /system.slice/apache2.service
             ├─37479 /usr/sbin/apache2 -k start
             ├─37480 /usr/sbin/apache2 -k start
             ├─37481 /usr/sbin/apache2 -k start
             ├─37482 /usr/sbin/apache2 -k start
             ├─37483 /usr/sbin/apache2 -k start
             └─37484 /usr/sbin/apache2 -k start

Mar 03 22:25:27 main-ubuntu1 systemd[1]: Starting The Apache HTTP Server...
Mar 03 22:25:27 main-ubuntu1 systemd[1]: Started The Apache HTTP Server.
```

**Check Install**

Create PHP file to check that it's been installed + working with Apache

Use `cd` to change directory to /var/www/html/ + open nano to create info.php file 

`cd /var/www/html/
sudo nano info.php`

Add text

`<?php
phpinfo();
?>`

Go to file via [external ip](http://34.16.129.98/info.php)

<img width="400" alt="Screen Shot 2024-03-03 at 5 37 20 PM" src="https://github.com/Obakoush/OBICT690/assets/142951646/cbfc3b03-b2d8-4340-b381-7767fabdb9e6">

## Basic Configurations

Change directory

`cd /etc/apache2/mods-enabled/`

Run `ls` to see dir.conf.bak file

```
 ls

access_compat.load  authz_host.load  dir.conf.bak      mpm_prefork.load  setenvif.conf
alias.conf          authz_user.load  dir.load          negotiation.conf  setenvif.load
alias.load          autoindex.conf   env.load          negotiation.load  status.conf
auth_basic.load     autoindex.load   filter.load       php7.4.conf       status.load
authn_core.load     deflate.conf     mime.conf         php7.4.load
authn_file.load     deflate.load     mime.load         reqtimeout.conf
authz_core.load     dir.conf         mpm_prefork.conf  reqtimeout.load
```

Create copy of dir.conf.bak file using `cp`

`sudo cp dir.conf dir.conf.bak`

Configure Apache to default to info.php instead of index.html 

   - run `sudo nano dir.conf` to open nano
   - change directory index to `DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm`
   - use `apachectl` to check configuration
      ```
     apachectl configtest
      Syntax OK
     ```
   - Reload Apache2 configuration `sudo systemctl reload apache2` + restart `sudo systemctl restart apache2`

**Create Index.php file**

 - Use nano + create php file, add in textbook code

```
<html>
<head>
<title>Broswer Detector</title>
</head>
<body>
<p>You are using the following browser to view this site:</p>
<?php
$user_agent = $_SERVER['HTTP_USER_AGENT'];
if(strpos($user_agent, 'Edge') !== FALSE) {$browser = 'Microsoft Edge';} elseif(strpos($user_agent, 'Firefox') !== FALSE) {$browser = 'Mozilla Firefox';} elseif(strpos($user_agent, 'Chrome') !== FALSE) {$browser = 'Google Chrome';} elseif(strpos($user_agent, 'Opera Mini') !== FALSE) {$browser = "Opera Mini";} elseif(strpos($user_agent, 'Opera') !== FALSE) {$browser = 'Opera';} elseif(strpos($user_agent, 'Safari') !== FALSE) {$browser = 'Safari';} else {$browser = 'Unknown';} if(strpos($user_agent, 'Windows') !== FALSE) {$os = 'Windows';} elseif(strpos($user_agent, 'Linux') !== FALSE) { $os = 'Linux';} elseif(strpos($user_agent, 'Mac') !== FALSE) {$os = 'Mac';} elseif(strpos($user_agent, 'iOS') !== FALSE) {$os = 'iOS';}elseif(strpos($user_agent, 'Android') !== FALSE) {$os = 'Android';} else {$os ='Unknown';}if($browser === 'Unknown' || $os === 'Unknown') {echo 'No browser detected.';} else {echo 'Your browser is ' . $browser . ' and your operating system is ' . $os . '.';}?>
</body>
</html>
```
returns this on extneral ip

<img width="400" alt="Screen Shot 2024-03-03 at 6 01 32 PM" src="https://github.com/Obakoush/OBICT690/assets/142951646/c8194f17-89ba-48ec-bcb7-c1a8d9d49699">

# Installing and Configuring MySQL

Install SQL server `sudo apt install mysql-server` *(I already have it installed)*

```
 sudo apt install mysql-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
mysql-server is already the newest version (8.0.36-0ubuntu0.20.04.1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

```
Check SQL running 

```
systemctl status mysql 
● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor p>
     Active: active (running) since Sun 2024-03-03 23:06:31 UTC; 20s ago
   Main PID: 38362 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 1134)
     Memory: 355.5M
     CGroup: /system.slice/mysql.service
             └─38362 /usr/sbin/mysqld

Mar 03 23:06:30 main-ubuntu1 systemd[1]: Starting MySQL Community Server.>
Mar 03 23:06:31 main-ubuntu1 systemd[1]: Started MySQL Community Server.
```
Run security check 

```
sudo mysql_secure_installation

sudo mysql_secure_installation

Securing the MySQL server deployment.

Connecting to MySQL using a blank password.
The 'validate_password' component is installed on the server.
The subsequent steps will run with the existing configuration
of the component.
...

Answer N, Y, Y, Y, Y
```

Make yourself root user 

```
sudo su
root@main-ubuntu1:/var/www/html# whoami
root
root@main-ubuntu1:/var/www/html#
```
Log in as MySQL user 

```
root@main-ubuntu1:/var/www/html# mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 8.0.36-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```
Request database list

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.05 sec)

```

**Set Up Regular User Account**

Use `create` command to set up account, account name, and set up password

```
create user 'wardah'@'localhost' identified by 'XXXXXXXXX';

Query OK, 0 rows affected (0.01 sec)
```

## Create Practice Database

Create databbase 
```
mysql> create database opacdb;
Query OK, 1 row affected (0.01 sec)

```

Give yourself access
```
mysql> grant all privileges on opacdb.* to 'wardah'@'localhost';
Query OK, 0 rows affected (0.01 sec)
```
Check new database appears on list 

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| opacdb             |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)
```

exit mysql by running `\q`

## Creating Tables
  - log in w `mysql -u wardah -p`
  - after running `show databases` run `use opacdb`

Create Tables
```
mysql> create table books (
    -> id int unsigned not null auto_increment,
    -> author varchar(150) not null,
    -> title varchar(150) not null,
    -> copyright date not null,
    -> primary key (id)
    -> );
Query OK, 0 rows affected (0.03 sec)

```
Show table and feilds

```

mysql> show tables;
+------------------+
| Tables_in_opacdb |
+------------------+
| books            |
+------------------+
1 row in set (0.00 sec)

mysql> describe books;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| id        | int unsigned | NO   | PRI | NULL    | auto_increment |
| author    | varchar(150) | NO   |     | NULL    |                |
| title     | varchar(150) | NO   |     | NULL    |                |
| copyright | date         | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
4 rows in set (0.01 sec)
```
**Adding Records**

Populate using `insert`

```
insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022-04-05'),
('Imbolo Mbue', 'How Beautiful We Were', '2021-03-09'),
('Lydia Millet', 'A Children\'s Bible', '2020-05-12'),
('Julia Phillips', 'Disappearing Earth', '2019-05-14');
```
View the records populated 

```

mysql> select * from books;
+----+----------------+-----------------------+------------+
| id | author         | title                 | copyright  |
+----+----------------+-----------------------+------------+
|  1 | Jennifer Egan  | The Candy House       | 2022-04-05 |
|  2 | Imbolo Mbue    | How Beautiful We Were | 2021-03-09 |
|  3 | Lydia Millet   | A Children's Bible    | 2020-05-12 |
|  4 | Julia Phillips | Disappearing Earth    | 2019-05-14 |
+----+----------------+-----------------------+------------+
4 rows in set (0.00 sec)
```

**Commands**
  
    - a few of the examples ran

Table of author + books

```
mysql> select author, title from books;
+----------------+-----------------------+
| author         | title                 |
+----------------+-----------------------+
| Jennifer Egan  | The Candy House       |
| Imbolo Mbue    | How Beautiful We Were |
| Lydia Millet   | A Children's Bible    |
| Julia Phillips | Disappearing Earth    |
+----------------+-----------------------+
4 rows in set (0.00 sec)

```

Table of authors in order of copywrite

```
mysql> select author from books order by copyright;
+----------------+
| author         |
+----------------+
| Julia Phillips |
| Lydia Millet   |
| Imbolo Mbue    |
| Jennifer Egan  |
+----------------+
4 rows in set (0.00 sec)

```

Books where author named "Mbue"

```
mysql> select title from books where author like '%mbue%';
+-----------------------+
| title                 |
+-----------------------+
| How Beautiful We Were |
+-----------------------+
1 row in set (0.00 sec)

```


**Extra commands**

Most recent book by copyright data

```
mysql> SELECT * FROM books ORDER BY copyright DESC LIMIT 1;
+----+---------------+-----------------+------------+
| id | author        | title           | copyright  |
+----+---------------+-----------------+------------+
|  1 | Jennifer Egan | The Candy House | 2022-04-05 |
+----+---------------+-----------------+------------+
1 row in set (0.00 sec)
```

Books between specfic dates

```
SELECT * FROM books WHERE copyright BETWEEN '2018-01-01' AND '2021-12-31';
+----+----------------+-----------------------+------------+
| id | author         | title                 | copyright  |
+----+----------------+-----------------------+------------+
|  2 | Imbolo Mbue    | How Beautiful We Were | 2021-03-09 |
|  3 | Lydia Millet   | A Children's Bible    | 2020-05-12 |
|  4 | Julia Phillips | Disappearing Earth    | 2019-05-14 |
+----+----------------+-----------------------+------------+
3 rows in set (0.00 sec)
```

Books titles that start with H

```
SELECT * FROM books WHERE title LIKE 'H%';
+----+-------------+-----------------------+------------+
| id | author      | title                 | copyright  |
+----+-------------+-----------------------+------------+
|  2 | Imbolo Mbue | How Beautiful We Were | 2021-03-09 |
+----+-------------+-----------------------+------------+
1 row in set (0.00 sec)
```

## Install PHP + MySQL Support
  - installed PHP support
  - restarted apache 2 and mysql

Change permissons of file + add credentials login.php file

```
sudo touch login.php
wardah@main-ubuntu1:/var/www/html$ sudo chmod 640 login.php
wardah@main-ubuntu1:/var/www/html$ sudo chown :www-data login.php
wardah@main-ubuntu1:/var/www/html$ ls -l login.php
-rw-r----- 1 root www-data 0 Mar  4 00:11 login.php
wardah@main-ubuntu1:/var/www/html$ sudo nano login.php
```

Created opac.php file and added in php code

**Test Syntax**

- Run `sudo php -f login.php` if no returns than no errors
- Run `sudo php -f opac.php` to get the HTML

```
sudo php -f opac.php
<html>
<head>
<title>MySQL Server Example</title>
</head>
<body>
<h1>A Basic OPAC</h1>
<p>We can retrieve all the data from our database and book table
using a couple of different queries.</p>
<h2>Query 1: Retrieving Publisher and Author Data</h2>PHP Notice:  Undefined index: publisher in /var/www/html/opac.php on line 32
<p>Publisher  published a book by Jennifer Egan.</p>PHP Notice:  Undefined index: publisher in /var/www/html/opac.php on line 32
<p>Publisher  published a book by Imbolo Mbue.</p>PHP Notice:  Undefined index: publisher in /var/www/html/opac.php on line 32
<p>Publisher  published a book by Lydia Millet.</p>PHP Notice:  Undefined index: publisher in /var/www/html/opac.php on line 32
<p>Publisher  published a book by Julia Phillips.</p><h2>Query 2: Retrieving Author, Title, Date Published Data</h2><p>A book by Jennifer Egan titled <em>The Candy House</em> was released on 2022-04-05.</p><p>A book by Imbolo Mbue titled <em>How Beautiful We Were</em> was released on 2021-03-09.</p><p>A book by Lydia Millet titled <em>A Children's Bible</em> was released on 2020-05-12.</p><p>A book by Julia Phillips titled <em>Disappearing Earth</em> was released on 2019-05-14.</p>
</body>
</html>
```

### Overview:
- All the sections went smoothly thankfully, I use SQL moderately for work so I am excited to learn new skills. Overall this was a fun section, although I am not really advanced at building websites I will always remember how to make the background light pink. 











  




     
     
    








