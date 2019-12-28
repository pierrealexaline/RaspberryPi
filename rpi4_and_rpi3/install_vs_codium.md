# How to install VS codium on a raspberry pi model 3 or 4 with Raspbian Buster OS

Add the GPG key of the repository :

        wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg | sudo apt-key add -

Add the repository:

        echo 'deb https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/repos/debs/ vscodium main' | sudo tee --append /etc/apt/sources.list.d/vscodium.list

Update and  install vscodium:

        sudo apt update && sudo apt install codium


Verify installation by typing :

        codium -v

### Sources :
[Official wiki of vscodium repository on github](https://vscodium.com/)


