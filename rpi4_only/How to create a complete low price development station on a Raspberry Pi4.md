# How to create a complete low price development station with Symfony, Composer, node, PHP, Mariadb, PHPmyadmin, React , Docker and VScodium on an RPI4

Since 2 days theres a solution to install Symfony 5 on a raspberry pi 4. Thanks to Tugdual Saunier from symfony. And we can now integrate this to our little big Rpi4 sbc.
This tutorial explain how to do that... and more how to **create a complete development station with a Raspberry pi**. What we need for that ? only ten fingers and 1 hour free, 2 liter of Blue Montains coffee,... Seriously, just a little understanding on linux debian world.

**What is the interest will you tell me? It is multiple:**
* Take into account the problem of global warming in development activities (the RPI4 consumes less than a current or older laptop whatever its configuration).
* Offer the possibility of working or training for people living in areas where electricity is not easily accessible (the rpi coupled to a small screen can easily operate on battery, so thanks to alternative energies like solar. For the network, just pair it with a Smartphone
* Provide the opportunity for people to train in development jobs at a lower cost. An RPI 4 model B with a mini screen running on USB 3.0 and some recycled accessories cost around 150 euros.
* Possibility to develop application interfacing the GPIO of the RPI4 from root
* finally, for fun!

**What we gonna get after :**

* Ubuntu server and Lubuntu, or Xubuntu or kubuntu(*)
* Curl
* Apache2
* Mariadb
* Php
* Phpmyadmin(**)
* Composer
* Symfony
* NodeJs
* Npm (not tested Nvm)
* Yarn
* React
* Docker
* Python
* Git
* Vscode(**)
* Nano

ssh, ssl capability, ...etc... You can add FTP, Chromium + headless browsers,  and many more.

* (*)Gui is facultative but in the case you don't want to have one, the Ide must be changed to nano or Vim, or ne ...
* (**)gui only

## First we must install a proper vesrion of ubuntu server or ubuntu desktop

The very first versions of ubuntu for Raspberry 4 was very buggy and laggy with 4gb RAM not recognized 
by the system and USB 3.0 not detected. Since last update, this seems to have changed, Ubuntu is fonctionnal. 
You can choose from 2 version of Ubuntu :
* ubuntu 18.04.4
* ubuntu 19.1
And 2 architectures :
* 32bit
* 64bit

(nota : not tested on raspbian or Kali but this should be the same)

### Download an ubuntu-server version and architecture (approximative duration < 5mn)

* [Ubuntu 18.04.4 LTS -> 32 bits (support until April 2023)](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04.4&architecture=armhf+raspi3)
* [Ubuntu 18.04.4 LTS -> 64 bits (support until April 2023)](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04.4&architecture=arm64+raspi3)
* [Ubuntu 19.10 LTS -> 32 bits (support until July 2020)](https://ubuntu.com/download/raspberry-pi/thank-you?version=19.10.1&architecture=armhf+raspi3)
* [Ubuntu 19.10 LTS -> 64 bits (support until July 2020)](https://ubuntu.com/download/raspberry-pi/thank-you?version=19.10.1&architecture=arm64+raspi3)

Install the img on a 16gb or 32gb Sdcard (class10 or new Sdcard) with balena etcher or others solutions (
[Download balena etcher here : ](https://www.balena.io/etcher/) 

if you want to active ssh at first boot just create an empty file (without extension) named ssh.

Insert the sdcard on the RPI4 and launch the system. Enter the default login and password (ubuntu:ubuntu), and change the password on first boot.

Now you have two options : 

* if you want to make the raspberry a PC with GUI you must **download a desktop solution**  (see just bellow)
* if you just want to have a server and interact with it with SSH, FTP, ...you're done !

### Install a desktop environment (approximative duration < 5mn)

* `sudo apt-get install xubuntu-desktop`
* `sudo apt-get install lubuntu-desktop`
* `sudo apt-get install kubuntu-desktop`

I have tested with Xubuntu, it's work like a charm.

## Install the classicals : Apache2, MariaDb and PHP7.2 (approximative duration < 10 mn) 

For more detailed instructions on how to manage php.ini and sql configuration files look at the web, there's a lot of tutorials on these.

**Prerequisite**

* `sudo apt install build-essential`
* `sudo apt install curl gcc g++ make`

### Install Apache2

* `sudo apt install apache2`

### Install PHP 7.2 and modules

* `sudo apt install php php-mbstring php-gd`
* `sudo phpenmod mysqli`
* `sudo phpenmod sqlite`
* `sudo service apache2 restart`

(you can activate other SGDB like PostgreSQL if you want)

### Install MariaDb

* `sudo apt install mariadb-server php-mysql`
* `sudo mysql_secure_installation`

Create a new root user for distant access :

```
sudo mysql --user=root --password
> create user admin@localhost identified by 'your_password';
> grant all privileges on *.* to admin@localhost;
> FLUSH PRIVILEGES;
> exit;
```

**optional : change the permissions for your /var/www/html/**

* `sudo chown -R pi:www-data /var/www/html/`
* `sudo chmod -R 770 /var/www/html/`

### Install phpmyadmin

* `sudo apt install phpmyadmin`

Create a new user for phpmyadmin

#### Resolve the bugs (2019-2020) :

todo :)° same as the standart non ARM versions

## Install composer (approximative duration < 2 mn)

Just for the example (it's better to reffer to the composer site beacuse the hash file is updated continually)
here're the link for original version :
* [Get composer](https://getcomposer.org/download/)
* [install it globaly (recommended)](https://getcomposer.org/doc/00-intro.md#globally)

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
```

## Install Nodejs, npm, yarn (approximative duration < 2 mn)

You must install the LTS version for ARM8 if you use a RPI4 and ARM7 for RPI3

#### nodeJs (approximative duration < 2 mn)

* `curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`
* `sudo apt install -y nodejs`

#### Npm (approximative duration < 2 mn)

* `sudo npm install npm -g`

#### yarn (approximative duration < 2 mn)

* `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`
* `echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
* `sudo apt-get update && sudo apt-get install yarn`


## Install Symfony 5 and Symfony 5 cli (approximative duration < 2 mn)

Normally git is pre installed, if not :

* `sudo apt install git`

after that, we have to install symfony cli normaly ...

* `wget https://get.symfony.com/cli/installer -O - | bash`

...and to get it installed globaly running this :

* mv /home/ubuntu/.symfony/bin/symfony /usr/local/bin/symfony

ok now just download the cli for ARM (thx to Tugdual Saunier):

* [symfony cli for ARM8 64bits](https://gist.github.com/tucksaun/9a6490616fc2cce623363985510d9dea#file-symfony_linux_arm64)
* [symfony cli for ARM6 or ARM7 32bits](https://gist.github.com/tucksaun/9a6490616fc2cce623363985510d9dea#file-symfony_linux_arm)

... remove the non-arm cli ...

* `sudo rm /user/local/bin/symfony`

... and replace + rename the arm8 version 64bits (for example) ...

* `sudo mv /home/ubuntu/Downloads/symfony_linux_arm64 /user/local/bin/symfony`

... make it executable

* `sudo chmod -x /user/local/bin/symfony`

... some configuration if needed :

* `sudo apt install libnss3-tools`
* `symfony server:ca install`
* `git config --global user.mail "my.email@myprovider.ext`

... now you're ready to use symfony 5 with CLI on a Raspberry pi 4 modele B

## Install Docker and docker compose (approximative duration < 2 mn)

### Docker ...  (approximative duration < 6 mn)

* `curl -sSL https://get.docker.com | sh`
* `sudo usermod -aG docker pi`
* `sudo docker run hello-world`

### ...and dependencies ####

* `sudo apt-get install libffi-dev libssl-dev`
* `sudo apt-get install -y python python-pip`
* `sudo apt-get remove python-configparser`

### ...and docker compose ####

* `sudo pip install docker-compose`

## Install ReactJs (just for my Friend Sami ! :)°

Nothing needed ! yes ! React is a library who's coming with npm. just do that :
* npx create-react-app my-app
* cd my-app
* npm start or npm start

If your browser open and you can see React logo turned on localhost:3000, this mean all is ok !!!
your rpi4 is React compliant :)° 

## Install Codium (open source Vscode without Microsoft trackers)

### VsCodium
* download codium from here https://vscodium.com/
* wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | sudo apt-key add - 
* echo 'deb https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/repos/debs/ vscodium main' | sudo tee --append /etc/apt/sources.list.d/vscodium.list 
* sudo apt update && sudo apt install codium 

if you don't like VScodium, you can install VScode (it's possible i've done in the past but laggy), Atom (it's possible too) or Gedit (more speed but very bad look)
Alternatives for non GUI : nano (preinstalled with ubuntu), vim, ne ...
All is done !!! you'ready to dev the new google with your RPI4 now!

## Sources

* https://github.com/nodesource/distributions
* https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
* https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl
* (...)
