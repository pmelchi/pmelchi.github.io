---
layout: post
title: Add ddclient to ubuntu - google domains 
date: 2020-11-21 08:00:00:00 +0600
description: Add ddclient configured with google domains
img: posts/2020-11-21-rack.jpg # Add image post (optional)
fig-caption: Photo by Taylor Vick on Unsplash
tags: [linux, ubuntu, dynamicdns]
---

# HOWTO: Configure ddclient for google domains in ubuntu
This is a sample configuration to create a new dynamic subdomain using google domains


## Google domains: Create your new subdomain

You need to set a new Dynamic DNS synthetic record by signing in you google domain

1. Select the name of your domain.
2. Click DNS.
3. Go to Synthetic Records.
4. Select "Dynamic DNS" from the list of synthetic record types.
5. Enter a  name of the subdomain 
6. Click View Credentials to view the user name and password created for this record.

## Server side: Install DD client

The first step is to install ddclient in ubuntu, which you can achive by executing 

{% highlight shell %}
sudo apt-get install ddclient
{% endhighlight %}

This will take you to a series of steps to help you with the configuration, use the Google domain reference configuration.

- Note1. I usually confused about the server, it's domains.google.com
- Note2. Interface configuration will help you get the IP. So if you put your "eth0" you'll get your local IP. You might need to configure it to "use web", "use web" will use an external service to get your Internet IP.


## I need to change the configuration
if you missed something or typed something wrong, you can edit your configuration with

{% highlight shell %}
sudo nano /etc/ddclient.conf
{% endhighlight %}

## I need to test my configuration

You can run the following command to test your configuration 
{% highlight shell %}
sudo ddclient -daemon=0 -debug -verbose -noquiet
{% endhighlight %}
 
Where 
 - **daemon** Run the request right now
 - **debug** Print debugging information
 - **verbose** Print verbose information
 - **noquiet** Print messages for unnecesary updates

Here's the ddlclient official [usage information](https://sourceforge.net/p/ddclient/wiki/usage/)


## Notes of possible errors


[Google domain reference configuration]: https://support.google.com/domains/answer/6147083?hl=en