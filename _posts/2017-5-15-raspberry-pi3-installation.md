---
layout: post
title: Ubuntu Server 16.04 installation on a Raspberry Pi 3
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

## Upgrade package [^3]

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

--------------------------------------------------

[^1]: [http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/](http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/)

[^2]: [https://ubuntu-pi-flavour-maker.org/download/](https://ubuntu-pi-flavour-maker.org/download/)

[^3]: [https://raspberrypi.stackexchange.com/a/62384](https://raspberrypi.stackexchange.com/a/62384)