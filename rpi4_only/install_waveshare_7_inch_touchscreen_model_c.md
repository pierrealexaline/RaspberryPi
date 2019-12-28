# How to connect and configure a 7 inch touchscreen (model C) from waveshare to a rasberry pi 4 model B
## Presentation
Since the last version of Raspbian (Buster) and the last version of the raspberry pi (rpi4b) the tutorial of the screen has not being updated correctly by Waveshare.

### The 7 inch hdmi screen (model C) from waveshare 
The 7 screen inch model C from Waveshare is originaly a basic LCD 1024x600x60Htz Hdmi touchscreen caracterized by a  very low power consumption (5v - 30mA to 300 mA with backlight on). It can run on an USB port. This screen is compatible with most OS and architectures (it can run on 32Bit, Arm, 64bit, or Windows 10, Linux Debian, and a lot of SBC like the Bananapi, Raspberry pi, Odroid ...).

### The raspberry pi model 4 model B 
The Raspberry Pi 4 model B has been launched at the end of 2019. Some problems occurs and need to be fixed. For example, Ubuntu is not totaly compatible at this date. It can't manage the new 4 Gb range of ram of the rpi4b. 
One of these problem was : how to connect and use the 7 inch touchscreen (model C) from waveshare with this new rpi ?
After a few hours of investigation this can be done !

### Prerequisites
* A rpi with **raspbian buster** pre-installed,
* a PC with a terminal on the same network and a **ssh client** installed,
* an official adaptator 5.1V+ -  3A  **!very Important!**.

## Prepare SD card before first boot
After burned the Raspbian Buster OS, open the sdcard on a pc,
open the file **config.txt** at the root on the boot partition
with a text editor.

### Change the config.txt file on boot partition
Comment this lines (*), just add a "#" before each line :

      #dtoverlay=vc4-fkms-v3d
      #max_framebuffers=2

And add this lines just under [rpi4] :

      max_usb_current=1
      hdmi_force_hotplug=1
      config_hdmi_boost=7
      hdmi_group=2
      hdmi_mode=88
      hdmi_drive=1
      hdmi_cvt 1024 600 60 6 0 0 0
      
Save the file at the same place.

(*) Recommandation from waveshare and Raspberry foundation. The fkms overlay is not supported by this type of screen. We can use standard kms overlay and work without 3d material acceleration. This work perfectly. 
 
### Add a 'ssh' file to boot partition
On the boot partition add a file named 'ssh' (without extention) for activate ssh at first boot.

## Connect via SSH on first boot from your PC to the rpi4b
Reboot the pi4 without the screen but with connected to your network, open a PC (connected on the same network) open a ssh client (like Putty) and connect it to the raspberry pi (with default user/password : pi/raspberry) 

Debian - example on how to connect your pi in ssh : ssh 192.168.0.87 -p22
replace the ip and port with your pi ip and ssh port.
First, on the PC, type in the terminal :


      sudo apt update && sudo apt-upgrade -y
      sudo raspi-config
 
### Make some change in raspi-config
In raspi-config , go to **advanced options**. 
* select "**resolution**" set to `DMT 88 1024x600 60Hz 15:9`,
* select "**Pi 4 Video Output**" set to `V1 Enable 4Kp60 HDMI`,
* select "**GL driver**" and set to `Legacy Original non-GL desktop driver`,

### last thing ... connect to USB3 port
Connect the waveshare screen to the raspberry pi 4 . **The screen mini USB must be connected on a USB3 port** because USB2.0 seems limited in Volts or A and can't give enough to the screen) .

### Reboot ...
Reboot the pi4... **You're done !!!**. You can now use VLC in 4k mode with your HDMI screen, or use touch screen for launch raspbian software ...etc

## Sources ...

* [Waveshare 7 inch screen (model C)](https://www.waveshare.com/wiki/7inch_HDMI_LCD).
* [Raspberry Pi 4 Model B - official presentation page](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
* [lcdwiki.com - Standard 7inch_HDMI_Display-C](http://www.lcdwiki.com/7inch_HDMI_Display-C#Step_2.2C_modify_the_.E2.80.9Cconfig.txt.E2.80.9D).
* [Github - detailled LCD-show drivers for Waveshare 7 inch screen (model C)](https://github.com/waveshare/LCD-show).
* [Android LineageOs- sourceforge - Waveshare 7 inch screen (model C) drivers](https://sourceforge.net/projects/pinn/files/os_next/lineage/waveshare/).