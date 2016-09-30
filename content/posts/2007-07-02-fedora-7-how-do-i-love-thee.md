---
title: Fedora 7, How do I love thee?
author: herlo
layout: post
date: 2007-07-03T05:16:28+00:00
url: /2007/07/02/fedora-7-how-do-i-love-thee/
categories:
  - Fedora
  - News
  - Passion
  - Tech
  - Tools

---
Oh joy, I **finally** decided to take the plunge and upgrade to Fedora 7 on my laptop. I was really nervous because my previous experience upgrading from Fedora Core 5 to FC6 was harrowing at best. Lots of errors and other junk happened back then.

But this&#8230;. this –was flawless. So simple, so easy. My grandma could install it its that simple. I was so impressed! So blown away at the improved upgradeability that has been made in Anaconda using **yum**.

I upgraded using the Fedora 7 DVD. I literally chose upgrade, followed the prompts and a short while later, I was told the installation was complete and to reboot. Being the geek that I am, I poked around while the upgrade was taking place. Nothing looked strange, no errors, nothing. Just a perfect upgrade.

My fears were unfounded. In my previous upgrade, I ran into problems with LVM. No issues here whatsoever. It was just awesome!

I rebooted my machine and waited for the kernel to boot. Here is where I found the first quirk, it tried to boot FC6 and failed. Obviously they need to clean up just a little more, but this was easily remedied by choosing the Fedora 7 boot option from GRuB. And yes, I removed the option from the grub.conf (menu.lst)

Literally 45 seconds later and I was at the login screen. Wow!! That was fast! My boot time in FC6 was over 2 minutes. Fedora 7 cut more than half the time off!

Have you seen the login screen? If not, its very pretty. Here's a screenshot:

[![Fedora Login Screen][1]][2]

Its just so beautiful! I love the fact that you can interact with the login window (gdm) with your mouse and choose your user. Linux on the desktop is well on its way up and love being a part of the revolution!

What about the other features. Oh, right! Let's get to them.

After logging in, I was psyched to see that my network card, the Intel ipw3945, worked out of the box. I have never been able to regularly use NetworkManager and nm-applet, but Fedora 7 fixed that too. Boy do I love the simplicity of it all. My networking is now so easy to set up.

Another tool that has been included is the new Pidgin. Previously named GAIM but because of legal pressures from AOL, was forced to change their name. Seems odd I'd be talking about this, but I just thought the logo was cool.

I also like the fact that I can build my own LiveCD without much effort. Try out **revisor** today, you'll have your very own LiveCD you can give away, tweaked the way you want.

There are many more features of Fedora 7 available, including _Fast User Switching, <a href="http://lwn.net/Articles/223185/" target="_blank">Dynamic Kernel Ticks</a>_, new and improved _NetworkManager_ and Multi-Display hotplugging with the new _Xorg Server_ 1.3.

Have a look around at the new Fedora 7 today and enjoy all that it has to offer&#8230;

Cheers,

Herlo

 [1]: {{<siteurl>}}uploads/2007/07/021_login_screen.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/07/021_login_screen.png "Fedora Login Screen"