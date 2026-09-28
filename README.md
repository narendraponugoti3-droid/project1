# project1

### Project Design 
<img width="838" height="479" alt="image" src="https://github.com/user-attachments/assets/30dc1b5c-2fab-41a8-92ed-bb00e40ed0b3" />


### Implemention 
1. Create Azure RG
2. Create a VN with 2 Subnets (websubnet- 10.0.1.0/24 , DBSN -10.0.2.0/24) Then Create VN
3. Create VM with Name: webVM and select the VN and Subent :websubnet and then create the VM and enable public IP Address
4. Connect this VM with public IP
           $sudo su -
           $apt update
           $apt install apache2 -y
           $systemctl status apache
           $http://public-ip-address
           /var/www/html --> index.html
                             $mkdir css images
                             $cd images
   Using WINSCP --> Copy the images from local to VM
   $scp ./potato.jpg devopsuser@ip-address:/tmp
   $mv onion.jpg potato.jpg tomato.jpg /var/www/html/images/
   $cd var/www/html/images
   #chmod 644 *.jpg
   $cd css/
   $vi style.css
   $vi index.html (delete content :%d)
   $sudo systemctl restart apache2

   
6.  Create VM with Name : DBVM and select the VN and subnet: DBSN and disable the public IP address then Create it
7.  Then go to Netwrok Setting of VM and add the mysql port with priority 110
8.  Then Create a NAT Gateway and attached to DBSN subnet
9.  Then Connect the DBVM using webVM (ssh devopsusersipaddress)
               $apt update
               #apt install mysql-server -y
               $system enable mysql
               $systemctl status mysql
10. if you want to access mysql from webvm , we need to modify mysql configuration file
         $cd /etc/mysql/mysql.conf.d/
         $ls
         $mysqld.cnf
         $vi mysqld.cnf
           bind-address  =0.0.0.0 // everyone can access this mysql
        $systemctl restart mysql
        $ cd ~
        $mysql
        $create database blinkit;
         $use blinkit ;
        #CREATE TABLE vegetables (
         id INT AUTO_INCREMENT PRIMARY KEY,
         name VARCHAR(100)
         price DECIMAL(10,2),
         description TEXT ,
         image VARCHAR(255));
11. Create User (CREATE USER 'blinkituser'@'%' IDENTIFIED BY 'StrongPassword123';)
12. gives all privileges (GRANT ALL PRIVILEGES ON blinkit.* TO 'blinkituser'@'%';)
13. FLUSH PRIVILEGES;
