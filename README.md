# Create-and-Host-a-Wordpress-Website-on-AWS-EC2-with-your-own-domain-name
Create and Host a Wordpress Website on AWS EC2 with your own domain name!
YouTube video link: https://youtu.be/8Uofkq718n8


1. Install Apache server on Ubuntu
sudo apt install apache2

2. Install php runtime and php mysql connector
sudo apt install php libapache2-mod-php php-mysql

3. Install MySQL server
sudo apt install mysql-server 

4. Login to MySQL server
sudo mysql -u root

5. Change authentication plugin to mysql_native_password (change the password to something strong)
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Testpassword@123';

6. Create a new database user for wordpress (change the password to something strong)
CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';

7. Create a database for wordpress give name (wp is the name of database)
CREATE DATABASE wp;

8. Grant all privilges on the database 'wp' to the newly created user (wp_user username)
GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;

9. Download wordpress
cd /tmp
wget https://wordpress.org/latest.tar.gz

ls

10. Unzip
tar -xvf latest.tar.gz
ls 
11. Move wordpress folder to apache document root
sudo mv wordpress/ /var/www/html
ls
cd /var/www/html   (we will see wordpress)

## go to google and check ip_adress/wordpress and configure database 
## go to wordpress directly /var/www/html/wordpress  create a new file here Ex wp-config.php and paste all code here which you copied  above when you got error on webpage and login and again check ip_adress/wordpress and but u want to use only ip_address so we have to change configuration file

cd /etc/apache2/sites-avaliable 
ls  (2 file is there)
sudo vi 000-default.conf  (edit this file)
## change in    DocumentRoot /var/www/html/wordpress    (and savre this)
12. Command to restart/reload apache server
sudo systemctl restart apache2
OR
sudo systemctl reload apache2
## for domain name we have to change some in this use sudo vi 000-default.conf  (edit this file)
sudo vi 000-default.conf 
## add  ServerName sachinparmar.local        (domain name use)
##      ServerAlias www.sachinparmar.local
...........................................................
## we can use this like we have to change 

<VirtualHost *:80>

        ServerName sachinparmar.local
        
        ServerAdmin webmaster@localhost
        
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
.......................................................

sudo systemctl restart apache2
sudo apt updaye -y

13. Install certbot (secure connecting we use this )
sudo apt-get update
sudo apt install certbot python3-certbot-apache

14. Request and install ssl on your site with certbot
sudo certbot --apache

----------------------------------------------------------------------
## we can check also other link  https://www.linuxshelltips.com/install-wordpress-on-ubuntu/ 
