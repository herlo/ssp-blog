---
title: Upgraded! Fedora 8 (Werewolf) is installed!
author: herlo
layout: post
date: 2007-11-05T04:00:43+00:00
url: /2007/11/04/upgraded-fedora-8-werewolf-is-installed/
categories:
  - Fedora
  - Install
  - News
  - Tech
tags:
  - f8
  - rawhide
  - upgrade
  - werewolf
  - yum update

---
And so the saga continues!

<pre>Transaction Summary
=============================================================================
Install     98 Package(s)
Update    1092 Package(s)
Remove       2 Package(s)

Total download size: 1.3 G
Is this ok [y/N]: y</pre>

Resulted in:

<pre>$ cat /etc/*release
Fedora release 8 (Werewolf)
Fedora release 8 (Werewolf)
Fedora release 8 (Werewolf)</pre>

I did have a few problems, mostly things that were from non-fedora repositories. Once I cleared those up, all went well. Fedora 8 is beautiful.

A couple things to note. My ATI drivers seemed to stay in place and as horrible as ever for dual displays. I'm going to be trying xrandr as soon as I can find the open ATI drivers. Another is that I love to use vlc, but its in the livna repository and currently requires python 2.4, but Werewolf uses python 2.5. I guess I'll have to get the src.rpm and rebuild it with python 2.5 as the requirement. I also noted that my mouse pad is currently not working, I'll have to find out why the synaptics drivers stopped working.

**Update**: I've decided it might be useful to at least include a couple cool pictures of the new theme, so here you go.

[![fedora8-background.png][1]][2] [![fedora8-gimp.png][3]][4] [![fedora8-rsyslogviewer.png][5]][6]

Cheers,

Clint

 [1]: {{<siteurl>}}uploads/2007/11/fedora8-background.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/11/fedora8-background.png "fedora8-background.png"
 [3]: {{<siteurl>}}uploads/2007/11/fedora8-gimp.thumbnail.png
 [4]: {{<siteurl>}}uploads/2007/11/fedora8-gimp.png "fedora8-gimp.png"
 [5]: {{<siteurl>}}uploads/2007/11/fedora8-rsyslogviewer.thumbnail.png
 [6]: {{<siteurl>}}uploads/2007/11/fedora8-rsyslogviewer.png "fedora8-rsyslogviewer.png"