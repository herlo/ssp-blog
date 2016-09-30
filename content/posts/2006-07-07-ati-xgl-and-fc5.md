---
title: ATI, Xgl and FC5
author: herlo
layout: post
date: 2006-07-07T17:16:54+00:00
url: /2006/07/07/ati-xgl-and-fc5/
categories:
  - Tech
  - Tools

---
I am giddy!!

I am soooo giddy!

Its a great day here at the Herlo Household. I have been able to successfully get Xgl working on FC5 where Ubuntu failed me. Mind you, it wasn't actually Xgl, it was the ATI drivers that failed, but in essence, that prevented me from getting Xgl working, but hey, its my post.

Life is good at the Herlo Household, yes, very good indeed&#8230;

I used a couple easy-to-follow but no-troubleshooting-provided blogs to get this going.

I was able to get my ATI FireGL 5200 working from this post:

<a title="ATI Drivers on FC5" target="_blank" href="http://www.fedorafaq.org/index.php#radeon">http://www.fedorafaq.org/#radeon</a>

And running fglrxinfo, I was able to see that my ATI drivers were indeed working

[clints@herlo-lap courseware]$ fglrxinfo
  
Xlib: extension &#8220;XFree86-DRI&#8221; missing on display &#8220;:0.0&#8221;.
  
display: :0.0 screen: 0
  
OpenGL vendor string: ATI Technologies Inc.
  
OpenGL renderer string: ATI MOBILITY FireGL V5200 Pentium 4 (SSE2) (FireGL) (GNU_ICD)
  
OpenGL version string: 1.2 (2.0.5879 (8.26.18))

Afterward, I was able to successfully (with a few tries) get Xgl running with gdm using this post:

<a target="_blank" title="XGL via GDM on FC5" href="http://forums.fedoraforum.org/showthread.php?t=111771">http://forums.fedoraforum.org/showthread.php?t=111771</a>

I was struggling for a little while getting gdm to come up. In fact, I had to spend time loading into Runlevel 3 and running startx to make gnome even come up. At one point, I ran gdm setup and changed gdm to load Standard rather than xgl. But that didn't fix my problem. After a bit more research, I found this comment near the bottom of the above post.

<font size="-2">Optional: Some people have reported that adding the line 'GdmXserverTimeout=60' to '/etc/gdm/custom.conf' under the heading '[daemon]' will allow Xgl to start where it would not otherwise&#8230;.</font>

This line saved my bacon, no really, it did! I restarted gdm after adding the detail, waited about 25 seconds and boom!, gdm came up. I logged in, and voila, Xgl was working, awesome, yes, so awesome!

Here are some screenshots for your viewing pleasure&#8230;

[<img id="image54" alt="xgl.2.png" src="{{<siteurl>}}uploads/2006/07/xgl.2.thumbnail.png" />][1]{.imagelink}[<img id="image55" alt="xgl.3.png" src="{{<siteurl>}}uploads/2006/07/xgl.3.thumbnail.png" />][2]{.imagelink}[<img id="image56" alt="xgl.4.png" src="{{<siteurl>}}uploads/2006/07/xgl.4.thumbnail.png" />][3]{.imagelink}[<img id="image57" alt="xgl5-2.png" src="{{<siteurl>}}uploads/2006/07/xgl5-2.thumbnail.png" />][4]{.imagelink}

Cheers,

Herlo

**Update:** After showing this to a few coworkers at <a target="_blank" title="Guru Labs" href="http://www.gurulabs.com">Guru Labs</a> today, I was able to help get at least one more person setup on Xgl. Cool beans!

 [1]: {{<siteurl>}}uploads/2006/07/xgl.2.png "xgl.2.png"
 [2]: {{<siteurl>}}uploads/2006/07/xgl.3.png "xgl.3.png"
 [3]: {{<siteurl>}}uploads/2006/07/xgl.4.png "xgl.4.png"
 [4]: {{<siteurl>}}uploads/2006/07/xgl5-2.png "xgl5-2.png"