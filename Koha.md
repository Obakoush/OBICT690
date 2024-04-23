# Installing Koha 

The goals for this week is to install and configure Koha, an intergrated library system 

**Create New VM**

Our current VM can not support Koha so we need to create a new instance on Gcloud
Create the new VM but make the following changes
- Change series to E2
- Change Machine Type to 2 vCPU with 4BG
  
After creating the new VM, create a firewall rule in GCloud to allow Koha to use port 8080 once installed

  - Using the three horizontal lines icon on the top left corner navigate to **VPC Network**
  - Click on **Firewall**
  - Create **Firewall Rule** ( **do not choose policy**)
  - Name the rule **Koha** and the description **Open Port 8080**
  - Tick the box that says **All Instances in the network**
  - In the box titled **Source IPv4 ranges** type **0.0.0.0/0**
  - Click on **Specified protocols and ports** and tick **TCP box** and type **8080** in Ports
  - Click **Create**

## Koha Prep

**Prepinng the VM**

Before installing Koha, we have to log in and prep the new VM

Update and upgrade the server by running

```
sudo apt update
sudo apt upgrade
```
Free up disk space by removing unneeded packages by running 

`sudo apt autoremove -y && sudo apt clean`

Next install gnupg2 to create digital signatures, encrypt data, and aid in secure communication

`sudo apt install gnupg2`

Reboot the VM 

`sudo reboot now`

**Creating a new Koha Repository**

Create a Koha repository to sycronize the current Koha data and staying up to date with Koha updates
Log in as the root user to make it easier since most of the commands require administrator access

`sudo su`

Add the Koha repository to our server

`echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list`

Add the digital signature

`wget -q -O- https://debian.koha-community.org/koha/gpg.asc | sudo apt-key add -`


## Installing Koha

Update /sync the new repository with the Koha remote repository

`apt update`


View the Koha package info 

`apt show koha-common`


Install the Koha package 

`apt install koha-common`


**Configure Koha**

In order to use Koha, we need to configure some of its files in nano

`nano /etc/koha/koha-sites.conf`


In the nano file change line `INTRAPORT="80"` to `INTRAPORT="8080"`


Set up MySQL and set root user password

`apt install mysql-server`


Set user password

`mysqladmin -u root password wardah27P`


Apache2 was installed with Koha but needs to be activated. We need to enable URL rewriting and CGI functionality.

```
a2enmod rewrite
a2enmod cgi
```

Restart Apache 2

`systemctl restart apache2`

Create database for Koha 

`koha-create --create-db bibliolib`


Configure the file to tell Apache2 to listen on port 8080

`nano /etc/apache2/ports.conf`

Make sure the changes in Apache work

`apachectl configtest`

If no error restart Apache 

`systemctl restart apache2`


Disable the default Apache2 setup, enable traffic compression using deflate, enable the bibliolib site, and then reload Apache2's configurations and restart again

```
a2dissite 000-default
a2enmod deflate
a2ensite bibliolib
systemctl reload apache2
systemctl restart apache2
```

## Koha Web Installer 

Get Koha username and password in the following file

`nano /etc/koha/sites/bibliolib/koha-conf.xml`


Visit the web installer by accessing [http://IP-ADDRESS:8080] http://34.162.112.205:8080

Should look like this

<img width="300" alt="Screen Shot 2024-04-23 at 1 20 20 AM" src="https://github.com/Obakoush/OBICT690/assets/142951646/d518e3e3-1d1f-4974-8d42-922a61c7bd41">

Follow the instructions on Koha Instillation Process <https://koha-community.org/manual//22.11/en/html/installation.html>

**Public Opac**

To view the OPAC public
- Click on **More** in the navigation bar dropdown
- Click on **Administration**
- Click on **System Preferences**
- Click on **OPAC** from the left navigation bar
- Scroll down until you find a line that says **OPACBaseURL**
- Enter IP address of your server: **http://IP-ADDRESS**
- Click on **Save all OPAC Preferences**


## Conclusion + Addtional Tasks

Once everything is installed correctly you can now mess around with Koda to create patron accounts, create bibliographic records, check out books to patrons or delete patron circulation history
