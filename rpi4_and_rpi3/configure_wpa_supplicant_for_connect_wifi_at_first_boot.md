# Configure wpa_supplicant for connecting the raspberry on wifi at the first boot

* Open **etc/wpa_supplicant/wpa_supplicant.conf** (in sudo mode) with your favorite editor,
* then just add :

        network={
            ssid="MY-SSID"
            psk="MY-PASSWORD"
            key_mgmt=MYCRYPTMODE_LIKE_WPA-PSK
        }

* save the file at the same place, reboot the raspberry pi. It should be connected to the wifi ssid you've given to it above !
