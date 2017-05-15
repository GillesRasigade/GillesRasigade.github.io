---
layout: post
title: Raspberry pi3 installation
---

## Raspberry pi3

### Insert the microSDCard

```bash
sudo fdisk -l
sudo fdisk /dev/mmcblk0
$> d (all), n, p --> yes, t, b (FAT32), w
sudo mkfs.vfat /dev/mmcblk0p1
```

### Copy the Ubuntu server image to the card
