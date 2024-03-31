# Installing Wordpress

Goal for this week: install wordpress, set up wordpress website, mess around with the customizations and get more comfortable.

**Install**
- Confirm SQL and PHP version are compatiable by running `php --version // mysql --version`
- Add on PHP modules to use wordpress more effectively 
 ```
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  fontconfig-config fonts-dejavu-core fonts-droid-fallback
  fonts-noto-mono fonts-urw-base35 ghostscript gsfonts
...
```
- Restart both Apache2 and MySql by running `sudo systemctl restart apache2 // sudo systemctl restart mysql`
- At the **end** reboot system

**Downloading + Extracting Wordpress**

- run `cd /var/www/html` to change directories 
- use `wget` command to download wordpress

```
sudo wget https://wordpress.org/latest.tar.gz
--2024-03-31 19:00:57--  https://wordpress.org/latest.tar.gz
Resolving wordpress.org (wordpress.org)... 198.143.164.252
Connecting to wordpress.org (wordpress.org)|198.143.164.252|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 24482912 (23M) [application/octet-stream]
Saving to: ‘latest.tar.gz’

latest.tar.gz   100%[====>]  23.35M  32.3MB/s    in 0.7s    

2024-03-31 19:00:58 (32.3 MB/s) - ‘latest.tar.gz’ saved [24482912/24482912]
```
- Run `sudo tar -xzvf latest.tar.gz` to unpack the zip file and view contents
- These commands will create wordpress directory, use `cd /var/www/html/wordpress` to access

**Create Database + User**

- Switch to linux root user + log into sql w root
  
```
sudo su
root@main-ubuntu1:/var/www/html/wordpress# mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
```

- Create wordpress database

```
mysql> create user 'wordpress'@'localhost' identified by 'Swif23xOP!X';
Query OK, 0 rows affected (0.01 sec)
```

- Create wordpress database

```
mysql> create database wordpress;
Query OK, 1 row affected (0.01 sec)
```
- Grant all privileges

```
mysql> grant all privileges on wordpress.* to 'wordpress'@'localhost';
Query OK, 0 rows affected (0.02 sec)
```

- Check to see if database added successfully

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
| wordpress          |
+--------------------+
6 rows in set (0.02 sec)

```

**Set up wp-config.php**

- Run `cd /var/www/html/wordpress` 
- Run `sudo cp wp-config-sample.php wp-config.php` to copy + rename the wp-config-sample.php file to wp-config.php
- Open nano `sudo nano wp-config.php` and change the lines w database name to wordpress, user to wordpress, and passwords to the new password
- Add `define('FS_METHOD','direct');` to the end of the nano text file to disable FTP uploads

**Change File Ownership**
- Run `sudo chown -R www-data:www-data wordpress/` to change file ownership and run `ls -l` to confirm the changes

```
ls -l
total 232
-rw-r--r--  1 www-data www-data   405 Feb  6  2020 index.php
-rw-r--r--  1 www-data www-data 19915 Jan  1  2023 license.txt
-rw-r--r--  1 www-data www-data  7399 Jul  5  2023 readme.html
-rw-r--r--  1 www-data www-data  7211 May 12  2023 wp-activate.php
drwxr-xr-x  9 www-data www-data  4096 Jan 30 19:27 wp-admin
-rw-r--r--  1 www-data www-data   351 Feb  6  2020 wp-blog-header.php
-rw-r--r--  1 www-data www-data  2323 Jun 14  2023 wp-comments-post.php
-rw-r--r--  1 www-data www-data  3013 Nov 15 17:47 wp-config-sample.php
-rw-r--r--  1 www-data www-data  3031 Mar 31 19:14 wp-config.php
drwxr-xr-x  4 www-data www-data  4096 Jan 30 19:27 wp-content
-rw-r--r--  1 www-data www-data  5638 May 30  2023 wp-cron.php
drwxr-xr-x 27 www-data www-data 12288 Jan 30 19:27 wp-includes
-rw-r--r--  1 www-data www-data  2502 Nov 26  2022 wp-links-opml.php
-rw-r--r--  1 www-data www-data  3927 Jul 16  2023 wp-load.php
-rw-r--r--  1 www-data www-data 50927 Jan 16 03:23 wp-login.php
-rw-r--r--  1 www-data www-data  8525 Sep 16  2023 wp-mail.php
-rw-r--r--  1 www-data www-data 26409 Oct 10 14:05 wp-settings.php
-rw-r--r--  1 www-data www-data 34385 Jun 19  2023 wp-signup.php
-rw-r--r--  1 www-data www-data  4885 Jun 22  2023 wp-trackback.php
-rw-r--r--  1 www-data www-data  3154 Sep 30  2023 xmlrpc.php
```

**Access Wordpress + Personalize**

- access wordpress site using <http://34.16.129.98/wordpress/>
- Set up user *Obakoush* and password *saved on googledrive*








