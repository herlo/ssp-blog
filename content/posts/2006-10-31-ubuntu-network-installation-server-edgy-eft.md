---
title: 'Ubuntu Network Installation Server – Edgy Eft'
author: herlo
layout: post
date: 2006-10-31T08:00:00+00:00
url: /2006/10/31/ubuntu-network-installation-server-edgy-eft/
categories:
  - Install
  - Tech

---
I've been working on installing the new Ubuntu 6.10 (Edgy Eft) via a network installation method known as Netboot. This method can be tricky to get setup, however after a bit of persistence, the steps are actually pretty easy to repeat. In addition, much of what I put here should be able to boot many operating systems via Netboot. My plan was to prepare network based installs for the <a target="_blank" href="http://www.ubuntu-utah.org">Ubuntu-Utah</a> installfest that happened this last weekend. Unfortunately, I travel a bunch for a living and didn't have an additional machine to work with until the night before. Also, I tried it with VMWare and was utterly unsuccessful in getting it to work at first. One thing to keep in mind is that I am currently installing Ubuntu using Fedora Core 5 as the install server. I plan on including instructions on how to setup the install server from Ubuntu itself as well.

**THE GOAL**

This weeks goal is actually planned to be a part of a larger goal. Installing Network Intallation of Ubuntu 6.10 is, in fact, only the initial phase of my plan for network based booting. I plan on future implementations to include extra functionality into the netboot feature provided by both Debian and Ubuntu Installers. In addition, I'd like the installation to run much smoother, more like the Red Hat installation method using 'linux askmethod' and choosing a source from which to install.

To speak only of this week's goal, I planned on successfully booting an installation of Ubuntu 6.10 using only the network and spooled media on a installation server. Thus providing a central way of installing multiple machines from one source.

**THE REASONING**

My reasoning for doing this is two-fold. One, I'd like to learn more about the installation process on the Debian/Ubuntu side of things. It's much more mystical of a process to me than the Red Hat/SuSE/Fedora way of doing things. And two, network installation can quickly install machines, and is usually quite a bit faster, especially in a laboratory/teaching environment.

**THE PROCESS**

Before starting the process, I want to mention that I did not want to install Ubunto to accomplish this task, rather I used what I had, in this case Fedora Core 5. I do believe, however, that the instructions I provide here will, most deservedly so, prove to work on Ubuntu/Debian and other *nix variants that support the components I set up.

Essentially, there are three parts to getting this working. First, there is the network setup, including dhcp, tftpd, and providing the install media via pxelinux (a derivative of syslinux). Each of these components required some tinkering, so I'll try to identify the problems I encountered below in my &#8220;THE GOTCHAS&#8221; section.

Next came understanding the boot process of a managed network card. This proved to be difficult to actually get an IP address, download via TFTP, and get the pxe boot image.

And finally, troubleshooting both the server and client components together proved to be the most challenging. This essentially provided the other two with constant tweaking with a little bit of hope and a prayer.

First service; dhcpd, the Dynamic Host Configuration Protocol Daemon. I spent a good bit of time researching each of the options below, and even at that, I've yet to define all of the options, or even if they are all needed. It is possible that dhcpd is not installed by default, if it is not installed:

\# yum install dhcp-server

Once installed, dhcpd will need to be configured. Here is my dhcpd.conf (each line is explained inline):

\# start of dhcpd.conf

<pre># <span style="font-style: italic">a required line from the Fedora compiled version of dhcpd</span></pre>

<pre>ddns-update-style none; <span style="font-style: italic" /></pre>

<pre># filename provides the location of the pxelinux.0 boot pxe kernel image</pre>

<pre>filename="/tftpboot/ubuntu-cd/install/netboot/pxelinux.0";</pre>

<pre># define the given subnet to supply dhcp addresses</pre>

<pre>subnet 172.16.217.0 netmask 255.255.255.0 {</pre>

<pre># define the given range of ip addresses</pre>

<pre>range 172.16.217.43 172.16.217.249;</pre>

<pre># define the next tftp boot server.  This line is vital to getting the pxelinux file.</pre>

<pre># If this line is not there the pxelinux.0 file will not be found!!</pre>

<pre>next-server 172.16.217.1; <span style="font-style: italic" /></pre>

<pre>}</pre>

DHCP is an integral part of a network based installation, without it, the client cannot get an IP Address, which will prevent the rest of the steps from happening as they all depend on the network being accessible.

Next, tftpd, the Trivial FTP Daemon. Most *nix operating sytems do not install tftpd by default because it is an inherent security risk. tftpd provides a minimal ftp experience and is required to get the PXE boot image. Because there are several tftpd servers, their configurations may change slightly. I chose to use tftpd through xinetd:

\# yum install tftp-server

Once installed, tftpd must be configured to run with the xinetd service. tftpd can be run without xinetd, but I've never configured it that way. Since I am installing on a Fedora box, here is that configuration:

<pre># <em>define the service being used from within the xinetd service</em>.</pre>

<pre>service tftp
{</pre>

<pre># <span style="font-style: italic">Is the service available, uses backward logic, thus no means the service "is" available and running.</span></pre>

<pre>disable            = no</pre>

<pre><span style="font-style: italic" /># <span style="font-style: italic">standard datagram packets, default, no need to change this</span>.</pre>

<pre>socket_type        = dgram</pre>

<pre># <span style="font-style: italic">most ftp services run over udp AFAIK.</span></pre>

<pre>protocol           = udp</pre>

<pre># <span style="font-style: italic">not sure of this setting, it's again another default.</span></pre>

<pre>wait               = yes</pre>

<pre># <span style="font-style: italic">this may not be the best user to run as,</span></pre>

<pre><span style="font-style: italic"># but if you aren't running this service all the time, maybe the risk is lessened.</span></pre>

<pre>user               = root</pre>

<pre># <span style="font-style: italic">the actual file the service uses.</span></pre>

<pre>server             = /usr/sbin/in.tftpd</pre>

<pre># <span style="font-style: italic">options to pass to tftpd, -v is verbose, and /tftpboot is the root of the server.  </span></pre>

<pre>#<span style="font-style: italic">Use any settings you like here, but I wouldn't recommend the -s option unless you know what you are doing.</span></pre>

<pre>server_args        = -v /tftpboot</pre>

<pre># <span style="font-style: italic">number of simultaneous connections per source, usually the default is a good number</span></pre>

<pre><span style="font-style: italic" /></pre>

<pre>per_source         = 11</pre>

<pre># <span style="font-style: italic">this is the default as well.</span></pre>

<pre>flags              = IPv4 <span style="font-style: italic" /></pre>

<pre>}</pre>

After configuring the tftp server, it needs to be started. Because it is part of the available xinetd services, it is started differently than most System V services. In this case, turning the service on involves restarting xinetd, rather than tftpd (but tftpd does need to be &#8220;not disabled&#8221;, as above):

\# /etc/init.d/xinetd restart

And&#8230;. the last configuration detail, spooling the media. My original intent, and one I finally went back to after some trial and error was to mount the .iso image onto the filesystem. This provides the look as if the CD were connected at the mount point, yet no external media is used. This is where the real speed up comes. Without the .iso image, running a CD across the network would in fact prove to be a bunch slower and wouldn't actually be worth it.

\# mkdir /tftpboot/ubuntu-cd
  
\# mount -o loop /path/to/ubuntu-6.10-alternate-i386.iso /tftpboot/ubuntu-cd/

<span style="font-style: italic">Mounting with the '-o loop' option provides an easy way to mount an .iso image over a loopback device.</span>

An alternate way to do this would be to copy the source of the .iso image to the hard drive. This takes up another 700MB on disk:

\# mount -o loop /path/to/ubuntu-6.10-alternate-i386.iso /mnt
  
\# cp -a /mnt/* /tftpboot/ubuntu-cd/

At this point, the only thing left to do is start up the dhcpd server:

\# /etc/init.d/dhcpd restart

Either way, that's the last step and things should be ready for installation.

**THE RESULTS**

Booting the server with PXE is pretty easy. You might have to edit your BIOS to enable the boot capability, but many network cards now support PXE boot. After getting PXE boot working, the results below should appear.

I think the results speak for themselves. I've included several screenshots from my VMWare server, but I've also been able to successfully get this working with real hardware.

[<img id="image71" alt="If you get even one thing wrong" src="{{<siteurl>}}uploads/2006/10/netinstall-pxe-fail.thumbnail.png" />][1]{.imagelink}Make sure to get it all correct or this will happen to you. If it does, it can be repaired, yet that involves time and patience.

[<img id="image72" alt="And When It All Works" src="{{<siteurl>}}uploads/2006/10/netboot-success.thumbnail.png" />][2]{.imagelink} Now that is much better, this is what an install should look like. It sure seems like a basic install, but as you can see, it loaded the network first. BTW, yes, this image is edited to provide you with the best display of what really happens upon success.

**THE GOTCHAS**

In the initial phases of this setup, I ran into several problems. Here are a few of the things to watch:

When setting up dhcpd, it may be required to indicate which network interface provides the actual addresses to the specified subnets. This usually causes problems starting dhcpd. I added the following to my /etcy/sysconfig/dhcpd file:

<pre>DHCPDARGS=eth0</pre>

Another gotcha that made it difficult to see was providing the -s option as an argument to the /etc/xinetd.d/tftp. This option provides for a secure tftp server, but in my case, it prevented me from actually downloading the correct file from the pxelinux.cfg directory. If you are interested in using the -s option, please refer to the syslinux/pxelinux site referenced below.

**THE RESOURCES**

Provided below are all of the URLs visited and used as reference guides to get this working:

  * <a target="_blank" href="http://www.mywheel.net/blog/index.php/ubuntu-network-install/">http://www.mywheel.net/blog/index.php/ubuntu-network-install/</a> – A blog post about a simple netboot installation. I adapted much of these components into my own installation server.
  * <a target="_blank" href="https://help.ubuntu.com/community/Installation/QuickNetboot">https://help.ubuntu.com/community/Installation/QuickNetboot</a> – Ubuntu always has good resources, this link is no exception. It's not perfect and mislead me a bit in a couple spots, but it was helpful overall.
  * <a target="_blank" href="https://help.ubuntu.com/community/Installation/QuickNetboot">http://syslinux.zytor.com/pxe.php</a> – The original syslinux/pxelinux site. It provides detailed information on the pxelinux booting process.

I've also provided all of the config files I created/used in the links below, enjoy.

  * <a target="_blank" href="{{<siteurl>}}files/my-dhcpd.conf">/etc/dhcpd.conf</a>
  * <a target="_blank" href="{{<siteurl>}}files/my-tftp-config">/etc/xinetd.d/tftp </a>

**THE NEXT STEP**

Right, so the next step is to move beyond a PXE boot, and setup machines that do not have a managed network card. That is next week's challenge.

Until next week then&#8230;

Cheers,

Clint

 [1]: {{<siteurl>}}uploads/2006/10/netinstall-pxe-fail.png "If you get even one thing wrong"
 [2]: {{<siteurl>}}uploads/2006/10/netboot-success.png "And When It All Works"