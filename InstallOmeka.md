# Installing Omeka

Goals: install software + create a site + customize site

**Installing**

- run `sudo apt install imagemagick` to install ImageMagick
- Run `sudo a2enmod rewrite` to enable moduling rewrite and restart by running `systemctl restart apache2`

**Steps to set up Omeka**

Log into SQL w root user
```
sudo su
root@main-ubuntu1:/home/wardah# mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 194
Server version: 8.0.36-0ubuntu0.20.04.1 (Ubuntu)
```

Set up user name and password 

```
mysql> create user 'omeka'@'localhost' identified by 'xxxxxxxx';
Query OK, 0 rows affected (0.02 sec)

```
Create the database + allow permissions

```
mysql> create database omeka;
Query OK, 1 row affected (0.02 sec)

mysql> grant all privileges on omeka.* to 'omeka'@'localhost';
Query OK, 0 rows affected (0.01 sec)
```
Navigate to the directory and use the wget command to download omeka

```
wardah@main-ubuntu1:/var/www/html$ sudo wget https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
--2024-04-08 04:52:25--  https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
Resolving github.com (github.com)... 140.82.112.3
...
```

Install unzip command 

```
sudo apt install unzip
Reading package lists... Done
Building dependency tree       
Reading state information... Done
```

Unzip the omeka download

```
sudo unzip omeka-3.1.2.zip
Archive:  omeka-3.1.2.zip
   creating: omeka-3.1.2/
   creating: omeka-3.1.2/admin/
   creating: omeka-3.1.2/admin/themes/
   creating: omeka-3.1.2/admin/themes/default/
   creating: omeka-3.1.2/admin/themes/default/appearance/
...
```

Rename the directory from omeka-3.1.2 to omeka and change to that directory

```
wardah@main-ubuntu1:/var/www/html$ sudo mv /var/www/html/omeka-3.1.2 /var/www/html/omeka
wardah@main-ubuntu1:/var/www/html$ cd /var/www/html/omeka
```
Open nano text editor for db.ini and put in relevent info 

```
sudo nano db.ini

; To configure your database, replace the X's with your specific
; settings. If you're unsure about your database information, ask
; your server administrator, or consult the documentation at
; <http://omeka.org/codex/Database_Configuration_File>.

[database]
host     = "localhost"
username = "omeka"
password = "xxxxxxxxx"
dbname   = "omeka"
prefix   = "omeka_"
charset  = "utf8"
;port     = ""

```

Change file owner with chown command + restart apache2 and mysql

```
sudo chown -R www-data:www-data /var/www/html/omeka
wardah@main-ubuntu1:/var/www/html/omeka$ sudo systemctl restart apache2
wardah@main-ubuntu1:/var/www/html/omeka$ sudo systemctl restart mysql

```

**Setting up Omeka Website**

- Set up Omeka account (like Wordpress) by accessing this website <http://34.16.129.98/omeka/>
- Change theme
- Add book items into items and add a few fetured collections (I added my March + April book reads)

**Reflection**

I had a few hiccups but it was mostly from typing in the commands wrong or missing a step. For the most part I followed the steps from last week and took my time. Overall I am proud I remembered the process and was able to go through this set up smoothly!






