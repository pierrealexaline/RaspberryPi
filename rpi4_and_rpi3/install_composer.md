# Install composer on a Raspberry pi model 3 or 4

Installation via cUrl, type this in a terminal :

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

Check version :

    composer --version

### Sources :
* [Composer official site](https://getcomposer.org/)
* [Installing composer and laravel on rpi unoficial tutorial medium.com/](https://medium.com/@roniemeque/using-raspberry-pi-for-laravel-developing-30dabcdeba43)
* [Composer tutorial from digitalocean.com](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-debian-9)