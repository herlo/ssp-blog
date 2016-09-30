---
title: 'POW: Yum installation by groups'
author: herlo
layout: post
date: 2007-10-31T20:28:14+00:00
url: /2007/10/31/yum-installation-by-groups/
categories:
  - Fedora
  - Guru
  - Install
  - POW
  - Tech
  - Tools
  - Yum
tags:
  - Fedora
  - groupinfo
  - groupinstall
  - grouplist
  - POW
  - Yum

---
The second in the Program of the Week (POW) is here.

Yum, the Yellowdog Updater Modifer, has a very interesting feature. One which you might find useful if you want to install an entire set of packages for say a new &#8220;Windows File Server&#8221;.

Yum provides this feature right out of the box these days, and its quite a nice feature. SUSE 10.1 has rug which is a very similar feature, called bundles. I would guess that Ubuntu either already has this feature, or will in the near future.

So how does installation by groups work? Pretty simple really, first we must learn a few new options in yum:

First is &#8220;grouplist&#8221;. Grouplist will tell you which groups of packages you have installed and which ones haven't been installed.

> <pre>$ yum grouplist</pre>
> 
> <pre>Setting up Group Process

Installed Groups:
  Office/Productivity
  Engineering and Scientific
  .. snip ..

Available Groups:
  .. snip ..

  Windows File Server
  .. snip ..

  Development Tools
Done</pre>

In my case, you can see that I've not yet installed &#8220;Windows File Server&#8221;. Interestingly enough, I'm not sure what's in that group of packages, so its time to check:

> <pre>$ yum groupinfo "Windows File Server"
Setting up Group Process</pre>
> 
> <pre>Group: Windows File Server
 Description: This package group allows you to share files
 between Linux and MS Windows(tm) systems.

 Mandatory Packages:
   samba
   samba-client
 Default Packages:
   system-config-samba</pre>

Wow, quite a few packages, there's also some good information here. We now know that there are 10 optional packages and 1 conditional package that can be installed. To get the details on any of these packages, yum can tell us:

> <pre>$ yum info samba
  .. snip ..

Available Packages
Name   : samba
Arch   : i386
Version: 3.0.26a
Release: 0.fc7
Size   : 3.1 M
Repo   : updates
Summary: The Samba Suite of programs
Description:Samba is the suite of programs by which a lot of
PC-related machines share files, printers, and other
information (such as lists of available files and printers).
The Windows NT, OS/2, and Linux operating systems support
this natively, and add-on packages can enable the same thing
for DOS, Windows, VMS, UNIX of all kinds, MVS,
and more..</pre>

Yum informs us that the &#8220;samba&#8221; package is useful for setting up file sharing between Windows and Linux. Other packages from the list above will also be installed so we'll get to play with some of those as well. If desired, 'yum info' can be run for each of the packages found in the grouplist. However, for us, lets move on and install the group of packages:

> <pre>$ su -# yum groupinstall "Windows File Server"
.. snip ..

============================================================
Package               Arch    Version        Repo      Size
============================================================
Installing:
system-config-samba   noarch  1.2.52-1.fc7   updates  287 k
Installing for dependencies:
samba                 i386    3.0.26a-0.fc7  updates  3.1 M
Transaction Summary
============================================================
Install      2 Package(s)
Update       0 Package(s)
Remove       0 Package(s)

Total download size: 3.4 M
Is this ok [y/N]:</pre>

At this point, we need to choose whether we're going to install the 2 packages that will enable samba for us. Hitting enter will answer no, so we need to type a 'y' and hit enter. The packages are then downloaded, and installed:

> <pre>Is this ok [y/N]: y
Downloading Packages:
(1/2): system-config-samb 100% |=============| 287 kB  00:00
(2/2): samba-3.0.26a-0.fc 100% |=============| 3.1 MB  00:02
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
Installing: samba                 ################## [1/2]
Installing: system-config-samba   ################## [2/2]
Installed: system-config-samba.noarch 0:1.2.52-1.fc7
Dependency Installed: samba.i386 0:3.0.26a-0.fc7
Complete!</pre>

As you can see, its pretty nice to be able to install a group of packages together, letting yum do the work to figure out the details. In another article in the near future, I'll cover how we create these relationships and build a back end yum server from the ground up.

Cheers,

Herlo