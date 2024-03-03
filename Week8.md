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

### Overview
- Apache installation and tasks went smoothly. Overall this was a fun section, although I am not really advanced at building websites I will always remember how to make the background light pink. 




