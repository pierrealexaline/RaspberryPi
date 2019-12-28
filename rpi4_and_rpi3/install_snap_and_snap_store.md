# How to install snap and snap-store on the raspberry pi
## First install snap 

Type this in a terminal :

        sudo apt update && sudo apt upgrade -y
        sudo apt install snapd
        sudo reboot

Test the installation :

        snap install hello-world 
        hello-world 

## Install snap-store

Type this in a terminal :

        sudo snap install snap-store
        sudo reboot

Well done !