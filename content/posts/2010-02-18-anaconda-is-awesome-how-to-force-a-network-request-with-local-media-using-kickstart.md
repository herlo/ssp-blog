---
title: Anaconda is Awesome! How to force a network request with local media using kickstart
author: herlo
layout: post
date: 2010-02-18T23:56:14+00:00
url: /2010/02/18/anaconda-is-awesome-how-to-force-a-network-request-with-local-media-using-kickstart/
categories:
  - Fedora
  - Guru
  - Install
  - Tech
  - Yum
tags:
  - anaconda
  - asknetwork
  - centos
  - dhcp
  - kickstart
  - network
  - repo
  - Yum

---
I sure love it when I solve my own problems, but the internets are a great help to enabling me.

Today, I found myself needing to enable the network (using dhcp) from the anaconda command line (the part that says **boot:** when you load a CentOS/RHEL/Fedora install disk).

I needed this because I was providing a bit of local media to our external employees for them to use to install, but I had 3 yum repositories I wanted them to be able to use for a few additional rpms I provided.

So, I popped into one of my common support channels and asked the question:

<pre>16:11 &lt; herlo&gt; looking for an option that I can put on the anaconda boot: prompt that will force a
               dhcp request even though the install is from a local disk.  I have repos that are not
               being accessed because the network is not being enabled.
16:11 &lt; herlo&gt; things I have tried
16:11 &lt; herlo&gt; ip=dhcp
16:12 &lt; herlo&gt; boot: linux noipv6 ks=hd:sdb1:media/kickstart.cfg ip=dhcp
16:20 &lt; herlo&gt; okay, so for those who might care
16:20 &lt; herlo&gt; if you do
16:20 &lt; herlo&gt; boot: linux asknetwork ip=dhcp noipv6 ks=hd:sdb1:media/kickstart.cfg
16:20 &lt; herlo&gt; anaconda will force a network dhcp request :)
16:20  * herlo is happy again
</pre>

As you may have noticed above, I resolved this issue without any assistance from the channel, and it only took me 10 minutes to do so.  I found my answer by trial and error from a great page on the fedora wiki: <https://fedoraproject.org/wiki/Anaconda/Options>

Probably the only thing I wish was documented on that page was when each of the options started being supported in anaconda.  Otherwise, thank you to the folks that wrote and maintain that page.

Cheers,

Herlo