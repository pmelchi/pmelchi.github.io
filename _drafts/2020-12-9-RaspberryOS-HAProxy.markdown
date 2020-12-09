---
layout: post
title: Install HA proxy using raspberry pi
date: 2020-12-09 08:00:00:00 +0600
description: Installing HA proxy in a raspberry pi with certs
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [raspberry, raspberryos, haproxy]
---

# Installing it
Straight forward installation 

{% highlight shell %}
sudo apt install haproxy
{% endhighlight %}

[docker volume]: https://docs.docker.com/storage/volumes/
[docker swarm]: https://docs.docker.com/engine/swarm/
[docker stack]: https://docs.docker.com/engine/swarm/stack-deploy/
[overlay]: https://docs.docker.com/network/overlay/
[mariadb]: https://hub.docker.com/_/mariadb