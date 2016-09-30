---
title: Changing the IP range for docker0
author: herlo
layout: post
date: 2014-05-07T22:02:45+00:00
url: /2014/05/07/changing-the-ip-range-for-docker0/
categories:
  - docker
  - Fedora
  - Networking
tags:
  - docker
  - Fedora
  - ip
  - network

---
Lately, I've been tinkering a lot with docker. Mostly, I've been doing it for work at [The Linux Foundation][1]. But I do have a desire to have docker instances on my local box for distros which I do not run.

While doing some testing for work on my personal laptop, I noticed that the network which docker uses for it's bridge, aptly named _docker0_, was in the same network as one of our VPNs.

<pre># ip a s docker0
7: docker0: &lt;BROADCAST,MULTICAST,UP,LOWER_UP&gt; mtu 1500 ...
 link/ether fe:54:00:18:1a:fd brd ff:ff:ff:ff:ff:ff
 inet 172.17.41.1/16 brd 10.100.72.255 scope global docker0
 ..snip..

# ip a s tun0
139: tun0: &lt;POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP&gt; mtu 1412 ...
    link/none 
    inet 172.17.123.32/24 brd 172.17.224.255 scope global tun0
       valid_lft forever preferred_lft forever</pre>

As you can tell, the _docker0_ network bridge covers all of the _tun0_ network. Any time I would attempt to ssh into one of the systems inside the VPN, it would time out. I was left wondering why for a few moments.

Luckily, it's very easy to fix this problem. All that is needed is a defined bridge for _docker0_ and to restart the docker service. Here's what to do:

First, stop docker:

<pre># service docker stop
Redirecting to /bin/systemctl stop  docker.service</pre>

Next, create the network bridge file. You can choose any IP range you like. On Fedora 19, it looks like this:

<pre># cat /etc/sysconfig/network-scripts/ifcfg-docker0 
DEVICE="docker0"
TYPE="Bridge"
ONBOOT="yes"
NM_CONTROLLED="no"
BOOTPROTO="static"
IPADDR=10.100.72.254
NETMASK=255.255.255.0</pre>

Restart your network services.  **NOTE:** _service network restart_ may be needed.

<pre># service NetworkManager restart
Redirecting to /bin/systemctl restart  NetworkManager.service</pre>

The _docker0_ bridge should now be in a range outside the VPN.

<pre># ip a s docker0
7: docker0: &lt;BROADCAST,MULTICAST,UP,LOWER_UP&gt; mtu 1500 ...
    link/ether fe:54:00:18:1a:fd brd ff:ff:ff:ff:ff:ff
    inet 10.100.72.254/24 brd 10.100.72.255 scope global docker0</pre>

Starting new containers with docker should get IP addesses in the above range:

<pre># service docker start
Redirecting to /bin/systemctl start  docker.service

# docker run -i -t herlo/fedora:20 /bin/bash
bash-4.2# ip a s eth0
141: eth0: &lt;BROADCAST,UP,LOWER_UP&gt; mtu 1412 ...
    link/ether fa:5f:e3:8d:61:f2 brd ff:ff:ff:ff:ff:ff
    inet 10.100.72.2/24 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::f85f:e3ff:fe8d:61f2/64 scope link 
       valid_lft forever preferred_lft forever</pre>

**SUCCESS!**

Cheers,

herlo

 [1]: https://linuxfoundation.org