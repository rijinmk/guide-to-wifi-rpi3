## To connect to Wifi [Using terminal]

This guide is to connect ONLY to WPA/WPA2 wifi networks. 
This guide will show you how to connect to the Wifi on a Raspberry Pi 3. 
This is for people who already has an OS installed on their Raspberry Pi and don't have a mouse to navigate through and click on the wifi icon OR anyone who wants to learn to connect using the terminals. 

### STEP 1 - SETTING IT UP

* Insert your SD card with the OS in it.
* Power up your Raspberry Pi 3 using a Micro USB charger. 
* Connect your keyboard
* Connect your screen to see whats happening
* Open terminals by pressing CTRL + ALT + T

### STEP 2 - TERMINAL COMMANDS

* Navigate to the etc folder 
```bash
cd /etc/
```
* In that there will be a folder named *wpa_supplicant*, Get into that folder.
```bash
cd wpa_supplicant
```
* Here you have to edit the file named *wpa_supplicant.conf*
* We are going to use terminals nano text editor to do that.
* We have to be a Super User to make changes to this file, hence we have to use *sudo* 
```bash
sudo nano wpa_supplicant.conf
```
* If you have connected your Raspberry Pi 3 to Wifi before you will see:
```bash 
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
        ssid="wifi-1-ssid"
        psk="wifi-1-password"
        key_mgmt=wifi-password-security-type
}

network={
        ssid="wifi-2-ssid"
        psk="wifi-2-password"
        key_mgmt=wifi-password-security-type
}
```
* If not, you wont see the *network={...}* 
* What we have to understand is that *network={...}* is EACH network that we connected to in the past. 
* Now, We have to add our own *network={...}*, We can do that like this, *ADD THIS TO THE END OF THE FILE*: 
```bash 
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=GB

network={
        ssid="wifi-1-ssid"
        psk="wifi-1-password"
        key_mgmt=wifi-password-security-type
}

network={
        ssid="wifi-2-ssid"
        psk="wifi-2-password"
        key_mgmt=wifi-password-security-type
}

#Add it here.. 
network={
        ssid="new-wifi-2-ssid"
        psk="new-wifi-2-password"
        key_mgmt=new-wifi-password-security-type
}
```
* "new-wifi-2-ssid" will be your Wifi name which you want to connect to. 
* "new-wifi-2-password" will be your Wifi password of the wifi you want to connect to. 
* *wifi-password-security-type* will be the security type: WPA/WPA2
* Now we have to reconfigure, We can do that by
```bash
sudo wpa_cli reconfigure
```
* This should connect you to the Wifi network, now you can use SSH to use your Raspberry Pi 3.

