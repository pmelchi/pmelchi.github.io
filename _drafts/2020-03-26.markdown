---
layout: post
title: Setting up your disk in USB 
date: 2020-03-26 08:00:00:00 +0600
description: Mounting and using your USB disk # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Linux, singleboard, armbian]
---

We want to create a rsync client with an 

In order to see where your USB device is located, we can use dmesg (on a not so busy system), you can easily spot your device with the sda :sda1 (let's remember that sda is you device and sda1 is your partition)

Sources: https://linuxhint.com/list-usb-devices-linux/

Note. Document post are post where I cover very obvious things you can google, but it saves my time next time I need to use it