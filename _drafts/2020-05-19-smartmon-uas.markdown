---
layout: post
title: Smartmon with UAS
date: 2020-05-26 08:00:00:00 +0600
description: I've found a lot of options and post on how to do it but this is my version # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [docker, nextcloud]
---

##Is it working with UAS?
~~
#lsusb -t
/:  Bus 03.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 5000M
    |__ Port 3: Dev 2, If 0, Class=Mass Storage, Driver=uas, 5000M
~~

##find the idVendor and idProduct fields for your device
~~
#lsusb
Bus 002 Device 002: ID 8087:8000 Intel Corp.
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 002: ID 0bc2:3322 Seagate RSS LLC SRD0NF2 [Expansion Desktop Drive]
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 002: ID 8087:07dc Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
~

##Update initramfs and reboot
~~
echo "options usb-storage quirks=0bc2:3322:u" >> /etc/modprobe.d/usb-storage-quirks.conf
update-initramfs -u
reboot
~

[smartmon UAS]: https://www.smartmontools.org/wiki/SAT-with-UAS-Linux
[OMV disable UAS]: https://forum.openmediavault.org/index.php?thread/26601-how-to-get-smart-on-external-drives/