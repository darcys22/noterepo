## Setup
install raspberry pi lite (headless) onto the SD card using the rpi imager
https://www.raspberrypi.org/software/

## Setup wireless and SSH
The imager will make a "boot" disk and you can put the following files directly onto it to instantly set up wifi and SSH

wpa_supplicant.conf
```
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
  ssid="YOURSSID"
  scan_ssid=1
  psk="YOURPASSWORD"
  key_mgmt=WPA-PSK
}
```

then just make an empty file named 'ssh' on the boot folder which will enable ssh

## Default login details

User: pi
Pass: raspberry
