---
title: 'Distro Comparison: openSUSE 10.3 first impressions'
author: herlo
layout: post
date: 2007-12-14T19:06:07+00:00
url: /2007/12/14/distro-comparison-opensuse-103-first-impressions/
categories:
  - Bash
  - Fedora
  - GNOME
  - Guru
  - Install
  - Networking
  - Suse
  - Tech
tags:
  - 
  - distro
  - features
  - Fedora
  - Suse
  - tehsuck
  - yast
  - zypper

---
I don't know if I can last an entire week with openSUSE 10.3. I can't believe I even thought it possible. I am jonesing for Fedora right now, even though any other distro would probably do&#8230;

What's wrong with SUSE you ask? Just about EVERYTHING! I'm not comfortable at all in this rancid environment. It sucks the life right out of you. I hope some SUSE people come running to save me from this turmoil I feel as I currently hate using this distro. Here's my first impressions: (beware, the list is rather long)

**GOOD**

The items below are positives and the openSUSE team deserves credit for all of their hard work in these areas.

  * Wireless works _(+1)_ 
      * My Intel wireless card from my T60p is recognized and associates with my access points
  * The nautilus-open-terminal package is enabled by default _(+2)_ 
      * This is the **right-click** on desktop –> Terminal option, (something severely lacking in fedora and not easily installed in a kickstart)
      * Having this feature, its very simple to get started with the terminal which is definitely needed for the power user in me
  * Install allowed me to choose not to use their grub _(0_) [while this is nice, if I had installed their grub, it would have wiped out my fedora grub components]
  * **zypper** is much improved over the previous rug (10.1) tool _(+1)_ 
      * still needs work though
      * easy to add repos compared with fedora 
          * packagekit can solve much of the incontinuity in fedora
          * though its nice to have a simple gui to add repos, knowing which repos is still a bit of an exercise in futility.

Positive Score: +4

**BAD**

Whle there is some good in openSUSE, its apparent to me that there is much to be improved.  As noted below, many more things are in need of improvement, to put it nicely.

  * The install takes much longer than necessary _(-3)_ 
      * Still uses ugly YAST text user interface 
          * YAST didn't recognize my video driver, but could have just used the VESA driver for the gui install
      * Asks too many questions about details that could easily be simpler
      * Did not work well with other OSes (GRUB) 
          * YAST installer wanted to overwrite my fedora GRUB configuration, shouldn't Linux play well with each other in this sense?
  * One-click install is more like 10-click _(-1)_ 
      * From opensuse.org, you can do what is called a &#8220;one-click install&#8221;, and about 8-10 clicks later its installed. If its one-click, its should be one (maybe two) clicks total.
  * The initial GNOME config of openSUSE is too Windows-like _(-1)_ 
      * If I wanted my Linux desktop to look like Windows, I'd use KDE (or even run Windows)
      * It has only one bar, and at the bottom, not enough room for status apps
      * I had to add workspaces as only one was provided by default, that seems limiting
  * bluez-gnome doesn't have hidd or any sort of recognition for my bluetooth mouse (or anyone's bluetooth mouse, for that matter) _(-2)_ 
      * dbus fails to recognize bluetooth mouse
      * There's even a bug on it blaming others, yet it works in Fedora – <a href="https://bugzilla.novell.com/show_bug.cgi?id=330461" target="_blank">https://bugzilla.novell.com/show_bug.cgi?id=330461</a>
  * The bash prompt is ugly – _(0)_ 
      * This one is a personal preference, but its hard to tell when I am the root user and when I am not. As such, I will modify my .bashrc and fix the PS1 value
  * The wireless driver for my T60p is not the new iwl3945, but the ipw3945 proprietary from intel – _(-1)_ 
      * The open driver has been out for quite some time 
        
  * Proprietary codecs were not easy to find, nor install _(0)_ 
      * Fedora doesn't make this simple either really.  Yet, when I found them in Fedora they worked first try, gstreamer failed miserably several times in openSUSE
      * an attempt at a codec buddy like tool was made, but doesn't work&#8230;
  * **zypper** does not inform you of the dependencies needed to install even though it reports how much it will download _(-1)_ 
      * I want to know what packages I'll be installing before I install them

Negative Score: -9

Total score for day 1:  **-5** OOPS – that's not good!

To be honest, I think I'm being very generous in some of the points I'm giving.  OpenSUSE makes it very difficult for my lifestyle so far.  I'm not sure what they can do with 10.3 to make it better, but I'd like to hear comments and suggestions on ways to help.

I'm sure hoping that day two will be better.  I'm already starting my list and will be testing such things as; video, development, lvm, raid, kvm/xen virtualization and much, much more.  As I continue to suffer through this bluetoothless mouse world openSUSE has created for me.

Cheers until tomorrow,

Herlo