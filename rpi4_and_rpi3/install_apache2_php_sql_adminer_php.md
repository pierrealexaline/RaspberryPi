# How to install Apache2, PHP7, Mysql [Mariadb] on a RPI4b 

## Presentation

* **Apache**
Apache is the most widely used web server software. 
Developed and maintained by Apache Software Foundation and available for free. 
It runs on 67% of all webservers in the world. 
It is fast, reliable, and secure and  can be highly customized.
* **PHP**
PHP is a server side scripting language used to develop websites or web applications. 
* **Mysql**
A query language and Sql database management system created by Oracle.
* **Adminer.php**
A light alternative to phpmyadmin, an online GUI for manage Mysql.

## Prerequisites
A Rpi model 4b and Raspbian Buster pre-installed

## Installation

Before all : 

        sudo apt update && sudo apt upgrade -y


### Install Apache2

Install apache2 :

        sudo apt install apache2

Test installation :

        service --status-all

If you see apache2 in the list, well done !
Now we need to manage apache2 :

Start / Restart apache2 :

        sudo systemctl start apache2
        sudo /etc/init.d/apache2 restart
        sudo systemctl restart apache2

Stop apache2 :

        sudo systemctl stop apache2 

#### Minimum configuration Apache2

Set permission on www/html/

        sudo chown -R pi:www-data /var/www/html/
        sudo chmod -R 770 /var/www/html/

#### Most advanced configuration
TODO

### Install php

Just simple, type : 

        sudo apt install php php-mysql php-mbstring

Add a file in www/html/ named index.php and write : 

        <?php phpinfo(); ?> 

at the begin of the file. Save the file. 
Open the file with a web browser (localhost/index.php)
if you see the page phpinfo we'll done ! 
php is correctly installed.

### Add or activate a php-mod 


Add some dependencies for future installation of frameworks like symfony :

        sudo apt install php-curl php-gd php-imap php-json php-mcrypt php-mysql php-opcache php-xmlrpc php-xml php-fpm php-zip php-gd2 -y

Example mysqli, activate the php module :

        sudo phpenmod mysqli
        sudo /etc/init.d/apache2 restart


Just type this in a terminal :

        php -m

You'll must see now the list of all modules installed with php by default. 
If you want to add another mod to php, just type this :

        apt install php-name_of_the_module

Php current module list :

* [doc.ubuntu.fr](https://doc.ubuntu-fr.org/php)
* [packages.ubuntu.com/bionic/amd64/php7.2-common/](https://packages.ubuntu.com/bionic/amd64/php7.2-common/filelist)

### Minimum configuration for php
TODO

### Install Mysql (Mariadb-server in fact)

Type this in a terminal :

        sudo apt install mariadb-server
        sudo service apache2 restart

Set root password and secure mysql server


        sudo mysql_secure_installation


You will be asked for :

* enter current password for root : default is blank / press Enter,
* set root password : type Y / press Enter.
* set new password and press Enter (Important: this root password for mysql !!!),
* re-enter the new password / press Enter,
* remove anonymous users : type Y / press Enter.
* disallow root login remotely : type Y / press Enter.
* remove test database : type Y / press Enter.
* reload privilege tables now : type Y / press Enter. 

When finish, you will see the message " All done! Thanks for using MariaDB ! ".

After that, just type this (5 differents command with "enter" between) :


        sudo mysql --user=root
        DROP USER 'root'@'localhost';
        CREATE USER 'root'@'localhost' IDENTIFIED BY 'password';
        GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
        QUIT;

You will see "Bye !" ...


#### Minimum configuration for Mariadb-server
TODO


## Install adminer.php light alternative to phpmyadmin

Go here [adminer.org](https://www.adminer.org/) and download the last version of adminer.php. 
Open the file with an editor. Make necessaries configuration directly in the file. 
When you need to have access to your database via GUI just do that :

        cd adminer_path/adminer.php 

and type this in a terminal :

        php -S localhost:8000/adminer.php

Then open this url : "localhost:8000/adminer.php" in a web browser.
enter your credentials and manage your db !