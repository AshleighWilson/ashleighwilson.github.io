---
layout: post
title:  "OctoPi Installation on a Raspberry Pi 4B"
categories: [ computing ]
tags: [ raspberry pi, system administration, 3d printing, linux ]
mathjax: false
---

This article provides details on installing OctoPi on a Raspberry Pi 4. It also describes the necessary steps for setting the device up as a Munin node so that it's resources can be monitored.

## Installation of OctoPi
The first step is to install OctoPi, a Raspbian Linux distribution with OctoPrint already installed. The latest OctoPi image can be downloaded from [https://octoprint.org/download/](https://octoprint.org/download/){:target="_blank"}. Using the [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/){:target="_blank"}, or other tool, burn the image file an SD card suitable for the Raspberry Pi.

As this installation will be a head-less setup, we now need to automatically join the correct wireless network on boot. To accomplish this, we need to edit the octopi-wpa-supplicant.txt file to provide the wireless network SSID and pre-shared keys.

Edit /boot/octopi-wpa-supplicant.txt by uncommenting the following lines and updating the SSID and PSK fields with the correct values for your network.

{% highlight zsh %}
network={
  ssid="put SSID here"
  psk="put password here"
}
{% endhighlight %}

## Connecting to the Raspberry Pi

Insert the SD card into the Raspberry Pi and then power up the device. The SSH daemon should automatically start on boot, as the /boot folder already contains a file named `ssh`. So, allow a few minutes before attempting to SSH into the Raspberry Pi using the hostname `OctoPi.local`, username `pi` and password `raspberry`:

{% highlight zsh %}
$ ssh pi@octopi.local
{% endhighlight %}

Once succesfully logged in, it is important to change the default password for security.

{% highlight zsh %}
$ sudo raspi-config
{% endhighlight %}

## Configuring OctoPi

It is now time to configure OctoPrint from your web browser. Head over to [http://octopi.local](http://octopi.local) and follow the configuration wizard. When you have finished with the configuration wizard, it is worth updating OctoPrint from `Settings` within OctoPrint.

## Installation of Munin Node

I have Munin installed on my systems so that I can monitor and trend system resources. This provides useful data to analyse any issues that may arise. To setup OctoPi as a Munin node, you first need to install `munin-node` and then run the configuration utility select relevant plugins for the system.

{% highlight zsh %}
$ sudo apt install munin-node
$ munin-node-configure --suggest --shell
{% endhighlight %}

Next, the configurations need to be updated for the Munin master and the new node.

Add the following text to `/etc/munin/munin-node.conf` on OctoPi:

{%- highlight munin -%}
allow ^192\.168\.0\.100$
{%- endhighlight -%}

Add the following to the Munin master's `/etc/munin/munin.conf`. Don't forget to add the correct IP address.

{%- highlight munin -%}
[octopi.local]
  address 192.168.0.30
  use_node_name yes
{%- endhighlight -%}
