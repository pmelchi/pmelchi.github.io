---
layout: post
title: Running docker and instances out of the box 
date: 2020-05-04 08:00:00:00 +0600
description: What happens when you run docker and images out of the box (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [docker, architecture]
---

I felt in love with the idea of docker and containers at once but I've found that it looks more like micro-management than a self-contained risk

What do I mean with that?

# Persistent storage
Out of the box everything is **ephemeral**, everything that you run with a straighforward run will command will vanish because you didn't specify at least a [docker volume]
{% highlight shell %}
$ docker run --name some-nginx -d some-content-nginx
{% endhighlight %}
Now that might be used to your advantage when you are running temporal jobs that might need or to store something directly in the filesystem, and let's be honest here unless you are a running some kind of persistent storage system you probably won't need it right away

# Swarm and persistence
[Docker swarm] sounds like a pretty interesting concept where you might want to deploy a [docker stack] and everything will be a microservice 

## Using NFS
You can attach an NFS to your [docker volume] and use it directly from your container although here's the thing, you'll face the regular NFS issues *e.g. security, permissions* plus your container is running with god knows what user, so it mounts the volume using *root* and it tries to access the folder with the same permission than is in your container.
For example in [mariadb] ask you have to make sure that your volume (NFS or not) has to belong to the mysql user and if use are using NFS, that means mapping has to be done

### Plus inherent issues from MYSQL:
https://dev.mysql.com/doc/refman/8.0/en/disk-issues.html


## Attaching physical storage
Let's say that some nodes in your swarm have better storage that others and you prefer to run your *file intensive process* on these nodes, well you'll have to run that service our of your swarm as an independent container with an independent network [overlay]

[docker volume]: https://docs.docker.com/storage/volumes/
[docker swarm]: https://docs.docker.com/engine/swarm/
[docker stack]: https://docs.docker.com/engine/swarm/stack-deploy/
[overlay]: https://docs.docker.com/network/overlay/
[mariadb]: https://hub.docker.com/_/mariadb