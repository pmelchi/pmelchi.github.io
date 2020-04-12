---
layout: post
title: Basic docker/compose installation on rock64
date: 2020-04-12 08:00:00:00 +0600
description: How to install docker and docker compose on a rock64, including packages that need to be installed first  # Add post description (optional)
img: 20-04-12-docker.png # Add image post (optional)
fig-caption: Docker/ rock 64 # Add figcaption (optional)
tags: [Linux, singleboard, armbian, docker]
---

It's a pretty straighforward process the only thing different is that compose needs to be installed via pip

# Install docker

Installing docker, it's easy with softy, it's actually easier than the official docker method where in version 19.03 suggested to use the "convinience script" (which in general it also seems to be detecting and using the package)

Softy is a menu based installed, you can get directly there by executing
```
sudo softy
```

Or you can always check the whole set of options by using:
```
sudo armbian-config
```
Then go to: Software > Softy 

![Softy]({{site.baseurl}}/assets/img/posts/2020-04-12-softy.jpg)


Once that's done, we can jump to installing docker-compose

# Docker compose

This is the list I came up with, (just jumping into installing docker-compose doesn't work), the

## Summary of commands
```
foo@bar:~$ sudo apt install python3 python3-pip libffi-dev python3-setuptools python3-dev

foo@bar:~$ sudo pip3 install wheel docker-compose
```

Maybe you can try going directly with docker-compose and skip wheel since it should be a requirement