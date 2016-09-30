---
title: 'Thoughts on the Fedora Upgrade – Part 1'
author: herlo
layout: post
date: 2007-11-06T18:43:20+00:00
url: /2007/11/06/thoughts-on-the-fedora-upgrade-part-1/
categories:
  - Fedora
  - Install
  - Releases
  - Tech
tags:
  - f8
  - packages
  - rawhide
  - rpm
  - upgrade
  - werewolf
  - Yum

---
So its been a whole two days since I upgraded to Werewolf. I love it! Most everything works out of the box (OOTB), wireless, bluetooth, even suspend/resume seem to be possible for the first time!

But one of the oddities I encountered while upgrading was the names of the packages. Mind you, this is just my twisted mind being interested in some of the funny odd or strange package names I found while the **yum upgrade** was taking place.**
  
** 

So here's the list anyway, with a short description of each. Enjoy:

  * gwenhywfar – A multi-platform helper library for networking and security applications and libraries.
  * meanwhile – <a href="http://tinyurl.com/2lqk8s" target="_blank">Lotus Sametime</a> session functionality.<a href="http://tinyurl.com/2lqk8s" target="_blank"></a>
  * neon – An HTTP and WebDAV client library.
  * coolkey – Linux Driver support for the CoolKey and CAC products.
  * rarian – Designed as a replacement for scrollkeeper; A documentation meta-data library.
  * openjade – An implementation of the <a href="http://www.jclark.com/dsssl/" target="_blank">ISO/IEC 10179:1996 standard</a> DSSSL.
  * sox – (Sound eXchange) is a sound file format converter.
  * cadaver – A command-line WebDAV client.
  * booty – Small python library for use with bootloader configuration.
  * orca – A flexible, extensible, and powerful assistive technology.
  * zenity – Lets you display Gtk+ dialog boxes from the command line and through shell scripts.
  * _eog_ – Eye of GNOME (EOG) is an image viewer.
  * _gok_ – Enables users to control their computer without relying on a standard keyboard or mouse, leveraging GNOME's accessibility framework
  * _devilspie_ – A window-matching utility.*

This information was gathered using the command '**rpm -qi** <packagename>'.  This provided enough information to help understand at least the basics of each of these packages and whether to consider using them in the future.

The packages in _italics_ above are packages that I consider interesting, and I plan to attempt to blog about each of them in turn as part of my <a href="{{<siteurl>}}category/pow/" target="_blank">POW</a> series.

The _devilspie_ package has a * which means that I've used this program before.  I quite enjoyed using the Devil's Pie, and plan to take a look at it again in Fedora 8 as the previous package had some real limitations and lacked needed flexibility.

Please watch for the upcoming articles on these utilities.  Also, if there are packages that you found interesting during your upgrade, please comment and let me know what they are so I can learn and possibly use them as well.

Cheers,

Herlo