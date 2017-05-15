---
layout: post
title: Raspberry pi3 installation
---

## Insert the microSD card

```bash
sudo fdisk -l
sudo fdisk /dev/mmcblk0
# then d (all), n, p --> yes, t, b (FAT32), w
sudo mkfs.vfat /dev/mmcblk0p1
```

> [http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/](http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/)

## Copy the Ubuntu server image to the card

```bash
xzcat ~/Downloads/ubuntu-16.04-preinstalled-server-armhf+raspi3.img.xz | sudo dd of=/dev/mmcblk0 bs=4M
sync
```

> [https://ubuntu-pi-flavour-maker.org/download/](https://ubuntu-pi-flavour-maker.org/download/)

Insert the card into the Raspberry and boot it with an ethernet connection available.

## Upgrade package

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

> [https://raspberrypi.stackexchange.com/a/62384](https://raspberrypi.stackexchange.com/a/62384)

Reboot the Raspberry and all must be ok.
