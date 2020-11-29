---
layout: post
title: Smartmon with UAS
date: 2020-05-26 08:00:00:00 +0600
description: Smartmon is not working because of UAS configuration, fixed via quirks
img: posts/2020-11-29-uas.png # Add image post (optional)
fig-caption: usb with UAS # Add figcaption (optional)
tags: [docker, nextcloud]
---

There's a known *issue* in linux where USB disk won't run smartmon with UAS because of the driver
This is how to disable th

##How do I know if I'm using UAS driver

if you use *lsusb -t* the output of this command will give you the information
You can see below the second line contains *Driver=uas*

{% highlight shell %}
#lsusb -t
/:  Bus 03.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 5000M
    |__ Port 3: Dev 2, If 0, Class=Mass Storage, Driver=uas, 5000M
{% endhighlight %}

##Find the idVendor and idProduct fields for your device

Since we want to disable it via quirks, you need to find your *idVendor and IdProduct*

Again *lsusb* without option does the job for me

I know that drive is the only Seagate on my system, so I don't have problems locating it.
The *idVendor and idProduct* come after the work ID (3rd line)

{% highlight shell %}
#lsusb
Bus 002 Device 002: ID 8087:8000 Intel Corp.
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 002: ID 0bc2:3322 Seagate RSS LLC SRD0NF2 [Expansion Desktop Drive]
Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 002: ID 8087:07dc Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
{% endhighlight %}

##Update initramfs options and reboot
Add the quirk option to your configuration 
We'll be telling the kernel to not bind UAS for this drive 

>usb-storage.quirks, u = IGNORE_UAS (don't bind to the uas driver);

{% highlight shell %}
echo "options usb-storage quirks=0bc2:3322:u" >> /etc/modprobe.d/usb-storage-quirks.conf
update-initramfs -u
reboot
{% endhighlight %}


[smartmon with UAS]: https://www.smartmontools.org/wiki/SAT-with-UAS-Linux
[OMV disable UAS]: https://forum.openmediavault.org/index.php?thread/26601-how-to-get-smart-on-external-drives/