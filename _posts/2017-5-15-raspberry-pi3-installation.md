---
layout: post
title: Ubuntu Server 16.04 installation on a Raspberry Pi&nbsp;3
category: raspberry
date: 2017-05-15
---

Overall process to install [Ubuntu Server 16.04](http://releases.ubuntu.com/16.04/) on a [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/).

## Insert the microSD card [^1]

```bash
sudo fdisk -l
sudo fdisk /dev/mmcblk0
# then d (all), n, p --> yes, t, b (FAT32), w
sudo mkfs.vfat /dev/mmcblk0p1
```

## Copy the Ubuntu server image to the card [^2]

```bash
xzcat ~/Downloads/ubuntu-16.04-preinstalled-server-armhf+raspi3.img.xz | sudo dd of=/dev/mmcblk0 bs=4M
sync
```

Insert the card into the Raspberry and boot it with an ethernet connection available.

## Upgrade packages [^3]

```bash
ssh ubuntu@192.168.x.x
# password update
sudo apt-get update
sudo apt-get upgrade # wait...
```

Mount the SDCard into  a PC and update the root file config.txt from:

```bash
...
device_tree_address=0x100
device_tree_end=0x8000
...
```

to

```bash
...
device_tree_address=0x02008000
...
```
Reboot the Raspberry and all must be ok.

## Configure the automatic wifi connection

Install `wpasupplicant` to the system.

```bash
sudo apt install wpasupplicant
```

Edit the file located `/etc/wpa_supplicant/wpa_supplicant.conf` to add the following lines:

```bash
# allow frontend (e.g., wpa_cli) to be used by all	users in 'wheel' group
ctrl_interface=/sbin/wpa_supplicant

# home network; allow all valid ciphers
network={
  ssid="[SSID]"
  scan_ssid=1
  key_mgmt=WPA-PSK
  psk="[PSK]"
}
```

Update the network interfaces to use this configuration

Decrease the boot connection delay to several seconds [^4] (useful for testing):

```bash
sudo vi /etc/systemd/system/network-online.targets.wants/networking.service
# TimeoutStartSec=20sec
sudo systemctl daemon-reload
sudo /etc/init.d/networking restart
ifconfig
# Check that the wireless interface has an attached IP
```

--------------------------------------------------

[^1]: [http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/](http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/)

[^2]: [https://ubuntu-pi-flavour-maker.org/download/](https://ubuntu-pi-flavour-maker.org/download/)

[^3]: [https://raspberrypi.stackexchange.com/a/62384](https://raspberrypi.stackexchange.com/a/62384)

[^4]: [https://ubuntuforums.org/showthread.php?t=2323253&p=13488422#post13488422](https://ubuntuforums.org/showthread.php?t=2323253&p=13488422#post13488422)