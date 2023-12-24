---
layout: post
title: "TCPDump cheatsheet"
date: 2024-01-02 10:00:00 +0300
description: These are few commands that sometimes I use when doing tasks with . 
img: 2020-04-12-docker.png # Fix
fig-caption: Docker/ rock 64 # CLI with TCPdump
tags: [Linux, Unix, CLI, cheatsheet]
---

# Starting 

## Identify network interfaces available
{% highlight shell %}
sudo tcpdump -D
{% endhighlight %}

Useful if 'ifconfig' is not available.

# Capture

## Capture a limite number of packages and show it
{% highlight shell %}
sudo tcpdump -i eth0 -v -c5
{% endhighlight %}

 - -i eth0: Capture data specifically from the eth0 interface.
 - -v: Display detailed packet data.
 - -c5: Capture 5 packets of data.

 ## Capture packages to a file in an specific port

{% highlight shell %}
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
{% endhighlight %}

This command will run in the background until '9' packages are captured.
{% highlight shell %}
[1]+  Done                    sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap
{% endhighlight %}

File 'capture.pcap' will be generated

- -i eth0: Capture data from the eth0 interface.
- -nn: Do not attempt to resolve IP addresses or ports to names.This is best practice from a security perspective, as the lookup data may not be valid. It also prevents malicious actors from being alerted to an investigation.
- -c9: Capture 9 packets of data and then exit.
- port 80: Filter only port 80 traffic. This is the default HTTP port.
- -w capture.pcap: Save the captured data to the named file.
- &: This is an instruction to the Bash shell to run the command in the background.


# Analyse

## Display content of pcap file

{% highlight shell %}
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
{% endhighlight %}


- -nn: Disable port and protocol name lookup.
- -r: Read capture data from the named file.
- -v: Display detailed packet data.

## Display content of pcap file in HEX

{% highlight shell %}
sudo tcpdump -nn -r capture.pcap -X
{% endhighlight %}

- -nn: Disable port and protocol name lookup.
- -r: Read capture data from the named file.
- -X: Display the hexadecimal and ASCII output format packet data. 
