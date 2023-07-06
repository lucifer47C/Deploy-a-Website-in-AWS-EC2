# Task 1
 Our first task is to create our AWS EC2 virtual machine that will host our WordPress and all software needed to deploy it. 
 - In the AWS console, let's access the EC2 service by navigating to **Service -> Compute -> EC2**. On the EC2 main page on top, we need to choose the region where we want to deploy our virtual machines.<br>The best practice is to choose a region close to your users.
 - Click on  **"Launch instance"** to launch a new instance.

   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/2.jpg>

 - We need to follow some steps to create our instance.
   * Instance machine image with the OS version will want for our project. I will choose **Ubuntu**.
   * We need to choose the instance configuration like CPU and memory.
   * We need to define the security group AWS already sets the SSH port to be used for all sources IP defined by 0.0.0.0/0. We will create a new rule to use the HTTP and HTTPS ports from any source to make our WordPress website available and accessible by HTTP/HTTPS URLs in a Web browser.
   * Create the key pair. Key Pair is a secure key we will need to access our instance later.
   * We need to define storage for our instance.
   * We can define some tags.

 - To use our instance we need to wait for the "Instances state" to be "Running" and "Status Check" to be "2/2".

   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/3.jpg>

 - Assign an elastic IP address. The reason we want to assign an elastic IP to this instance is that if we were to reboot this instance the public IPv4 address is going to change every time we reboot this virtual computer but we don't want that to happen we want the IP address to be static.

   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/4.jpg>

# Task 2
 Now you are going to connect to the EC2 instance.
 - Once we have a Linux instance, we will connect to our instance using an SSH client, or using the Web browser SSH client.<br> 
   (Select our instance and click on "Connect". In EC2 Instance Connect, click Connect again at the bottom.)
   
   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/5.jpg>
   I have connected using the Web browser SSH client.

 - Install Apache server on Ubuntu
   ```
   sudo apt install apache2
    ```
   Yes, to confirm.
   <br><br>
   To verify if our Apache website is working, copy our instance public IP address and paste it into another tab in the web browser. We can see Apache's default web page, 
   it means our web server is working.
   <br><br>
   It is good practice to run *<span style='color: red;'>sudo apt-get update</span>* before installing any packages.
   

   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/6.jpg>

 - Install PHP runtime and php mysql connector
   ```
   sudo apt install php libapache2-mod-php php-mysql
   ```  
   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/7.jpg>
   
# Task 3
 Now you are going to connect to the EC2 instance and install the MySQL database, which is the database we will use in our WordPress website installation.
 - Install MySQL server
   ```
   sudo apt install mysql-server
   ```
   Yes, to confirm
   <br>
 - We also need to create a user to be used for WordPress and the database
   * Login to MySQL server
       ```
       sudo mysql -u root
       ```
   * Change authentication plugin to mysql_native_password
       ```
       ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Testpassword@123';
       ```
   * Create a new database user for wordpress
       ```
       CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';
       ```              
   * Create a database for wordpress
       ```
       CREATE DATABASE wp;
       ```      
   * Grant all privilges on the database 'wp' to the newly created user
       ```
       GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
       ```
   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/8.jpg>
   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/9.jpg>

# Task 3
 Now we are going to install WordPress.
 - Download wordpress
   ```
   cd /tmp
   wget https://wordpress.org/latest.tar.gz
   ```
 - Unzip
   ```
   tar -xvf latest.tar.gz
   ```
   <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/11.jpg>
   
  - Move wordpress folder to the Apache document root
    ```
    sudo mv wordpress/ /var/www/html
    ```
    <img src=https://github.com/lucifer47C/Deploy-a-Website-in-AWS-EC2/blob/main/WordPress%20Website/Images/12.jpg>
  -  
