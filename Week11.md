# Creating OPAC Cataloging Module
- Goals: Add records to exsisting opac using MySQL to create a searable catalog

**Creating the HTML Page**

Create new directory for moduele 

```
cd /var/www/html
sudo mkdir cataloging
```

Add content via nano

`cd cataloging
sudo nano index.html`

```
<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="date" id="copyright" name="copyright">

        <input type="submit" value="Submit">
    </form>
</body>
</html>

```

View current opac using this site `http://34.16.129.98/cataloging/`

**Adding data to catalog using PHP**

```
<?php

// Load MySQL credentials
require_once '../login.php';

// Establish connection
$conn = mysqli_connect($db_hostname, $db_username, $db_password) or
  die("Unable to connect");

// Open database
mysqli_select_db($conn, $db_database) or
  die("Could not open database '$db_database'");

// Prepare and bind SQL statement
$stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
$stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

// Set parameters and execute statement
$author = $_POST["author"];
$title = $_POST["title"];
$publisher = $_POST["publisher"];
$copyright = $_POST["copyright"];

if ($stmt->execute() === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->error;
}

// Close statement and connection
$stmt->close();
$conn->close();

echo "<p>Return to the cataloging page: <a href='http://34.16.129.98/cataloging/'>http://34.16.129.98/cataloging/</a></p>";
?>

```

**Adding Security**

To ensure not anyone can enter data, you need to limit access. 

Set account and password

```
sudo htpasswd -c /etc/apache2/.htpasswd libcat
New password: 
Re-type new password: *****
Adding password for user libcat

```

Create copy of apache and use nano to open apache2.conf file to set pass control

`sudo nano /etc/apache2/apache2.conf`

In file change line 172 to allow all 

```
<Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride None
  Require all granted
</Directory>
```
Use new nano file called .htaccess to change cataloging directory

```
cd /var/www/html/cataloging
sudo nano .htaccess

AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

Check if config file is good by running `apachectl configtest` and syntax returns OK 

```
apachectl configtest
Syntax OK
```

**Adding Records**

Using `http://34.16.129.98/cataloging/` , log in and begin adding records

Check basic OPAC to see the new records added 

**Permissions**






