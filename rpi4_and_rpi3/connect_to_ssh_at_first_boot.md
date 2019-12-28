# How to launch ssh server at first boot

* create a file named ***ssh*** without extension,
* save this file at the root of the boot partition on the raspberry pi sdcard,
* get the ip of the raspberrypi (example : 192.168.0.96 port: 22),
* reboot the raspberry pi,
* connect to the pi via your PC and ssh (use your favorite ssh client example: ssh pi@192.168.0.96 -p 22),

That's all !
Important : Don't forget to change your root password (use raspi-config), however everyone can access to your pi using **pi** root user and **raspberry** root password via ssh !

