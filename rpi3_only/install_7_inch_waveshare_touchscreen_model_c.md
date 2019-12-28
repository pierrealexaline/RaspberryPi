# Configure the wavesharescreen for a raspberry pi 3 model b or A+

## Raspbian buster OS

Open the file config.txt in the boot partition of the sdcard with your favorite editor,
if you have Raspbian buster installed, then after "[all]" modify the file to have :

        [all]
        #dtoverlay=vc4-fkms-v3d
        gpu_mem=256
        max_usb_current=1
        hdmi_group=2
        hdmi_mode=87
        hdmi_cvt 1024 600 60 6 0 0 0 


## Raspbian Jessy and Stretch (not tested on Wheezy)

for other Raspbian just comment all the things about hdmi, sdtv, fkms ...,
and add this line at the end of config.txt :

        gpu_mem=256
        max_usb_current=1
        hdmi_group=2
        hdmi_mode=87
        hdmi_cvt 1024 600 60 6 0 0 0

Then go to a terminal and type :

      sudo apt update && sudo apt-upgrade -y
      sudo raspi-config
 
### Make some change in raspi-config

In raspi-config , go to **advanced options**. 
* select "**resolution**" set to `DMT 88 1024x600 60Hz 15:9`, 
* reboot :

        sudo reboot

if you have any problem come back to raspi-config,     
select "**GL driver**" and set to `Legacy Original non-GL desktop driver`,
then reboot :


        sudo reboot

