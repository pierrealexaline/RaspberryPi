# Install nodeJs, npm and yarn to Raspberry pi model > 2

## Install nodeJs & npm
According to nodeJs documentation. Type this in a terminal :

        sudo su curl -sL https://deb.nodesource.com/setup_12.x | bash -
        sudo apt-get install -y nodejs

Test if both nodejs and npm installed :

        node -v
        npm -v

## Install Yarn

Enable the Yarn repository by importing the repository's GPG key using curl :

        curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -

Enable the Yarn APT repository :

        echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.l

Update the package index and install Yarn :

        sudo apt update && sudo apt upgrade -y
        sudo apt install yarn

Verify installation :

        yarn --version

## Sources :
* [nodeJs official documentation on installing nodeJS to debian ARM](https://github.com/nodesource/distributions/blob/master/README.md)
* [instructables.com/id/Install-Nodejs-and-Npm-on-Raspberry-Pi/](https://www.instructables.com/id/Install-Nodejs-and-Npm-on-Raspberry-Pi/)
* [Arm supported now - yarnpkg/yarn/issues/2634](https://github.com/yarnpkg/yarn/issues/2634)
* [linuxize.com/post/how-to-install-yarn-on-debian-9/](https://linuxize.com/post/how-to-install-yarn-on-debian-9/)

