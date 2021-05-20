---
layout: post
title: Install HA proxy using raspberry pi
date: 2020-12-09 08:00:00:00 +0600
description: Installing HA proxy in a raspberry pi with certs
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [raspberry, raspberryos, haproxy]
---

# Mounting your new filesystem

This is a configuration for an already formated USB disk with EXT4
The prefered method to mount a disk us using ** UUID ** or ** LABELS ** since device names can change between boots

## 1) Find your device
I have a USB disk then I can run *lsubs* to get some basic information of the device but in order to mount the device I need to find out where has the linux kernel put my new device

There're 2 commands I find useful for this purpose

{% highlight shell %} dmesg {% endhighlight %}

![dmesg log]({{site.baseurl}}/assets/img/posts/2020-12-09-find_mount_1.png)

If it's a busy environment this will be dificult but you can always *grep* 

Another way is with {% highlight shell %} lsblk {% endhighlight %}
![lsblk output]({{site.baseurl}}/assets/img/posts/2020-12-09-find_mount_2.jpg)

Note. sdb is your device and sdb1 is your partition

Now that you have identified your device you are ready to mount it



## Mounting your device




# Installing haproxy
Straight forward installation 

{% highlight shell %}
sudo apt install haproxy
{% endhighlight %}

[ubuntu new harddrive]: https://help.ubuntu.com/community/InstallingANewHardDrive
[using UUID]: https://help.ubuntu.com/community/UsingUUID