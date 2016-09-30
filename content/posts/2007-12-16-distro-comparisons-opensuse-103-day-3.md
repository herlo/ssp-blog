---
title: 'Distro Comparison: openSUSE 10.3 – Day 3'
author: herlo
layout: post
date: 2007-12-17T03:47:18+00:00
url: /2007/12/16/distro-comparisons-opensuse-103-day-3/
categories:
  - Guru
  - Suse
  - Tech
  - Tools
tags:
  - distros
  - printing
  - Suse
  - tehsuck
  - yast

---
Wow, I'm excited by the response, and while I still believe that openSUSE is **not** the distro for me, it definitely has grown on me. I believe on my <a href="{{<siteurl>}}2007/12/14/distro-comparison-opensuse-103-first-impressions/" target="_blank">last review</a>, I might have been a bit hasty in stating that just about everything was useless. And while I do have a few more complaints about this distribution, getting settled in might have been all it takes to shake of the pure hatred I recently expressed.

Much of my response has been in fact aimed at my personal opinions of certain features, and while a few of the failures I noted were indeed things that bugged me, they were personal preference and thus, I will be revising my scoring system a little. In fact, **how** I will award points will not so much be based upon personal preference unless its completely unbearable to me. And to that end, I'll make a new PREFERENCES section, which will not receive scores, but will have things I personally like or dislike.

In addition, I so appreciate all of the comments I've received, many were very helpful in pointing out errors in my representation of openSUSE. Others were part of the reason I decided to change the scoring a bit. And even others I'd like to take the time to reply:

First, to my friend Heartsbane, thanks for the **smartass** reply. I should've known it was coming!

Sontek pointed out that there were bugs in the iwlwifi driver when 10.3 was released. While I agree with not releasing something before its ready, I find it interesting that 2 months after its release openSUSE doesn't have iwlwifi drivers available in their updates. Why is this? Did I miss them somewhere? My problems with the ipw3945 are more to the fact that it never seems to work with the WPA PSK setup I have at home/work. The iwlwifi driver has less issues with this specific problem.

apokryphos had several comments, and I will address a few of them.

  1. The _1-click-install_ feature is to help reduce much of the repo setup and installation that used to be a long drawn out process has been reduced to 1 click. While I agree that this is a major improvement, it is such a misnomer to call it a _1-click-install_ when it clearly isn't. I only suggest we rename the process as someone coming from another world to Linux who find openSUSE may be disappointed when a 1-click-install indeed requires more like 7 clicks.
  2. zypper shows what will be installed was another response I received contrary to what I saw. He asked me for an example, and in return I would suggest that indeed it does tell you what will be installed, but **only after** you agree to install the extra dependencies. Please provide me a command/option that shows me the dependencies prior to my agreement to install the package(s).
  3. The root prompt was another failure on my end, however. Mostly, I have it ingrained in my head to look for the &#8220;root&#8221; part in the prompt. The entire prompt indeed turns red as suggested, this is something I just have to get used to, or change to my preference I guess. I do still think the prompt is ugly, but its growing on me. Others mentioned this as well, thanks for pointing out this to me.

Another, which I received from Ani and lejocelyn (as well as apokryphos), was in regard to my complaint about the Windows-like look and feel. First off, its not a cop-out and secondly, it does look like Windows. Where is the multiple-workspaces? Isn't that a big plus, I had to add them and enable the panel object. What about this &#8220;control center&#8221;, feels a lot like Windows &#8220;control panel&#8221; to me. There is much more I think, and it also might be somewhat because I'm a GNOME user. But like I said, if I wanted it to look like Windows, I would just run Windows.

Ani also pointed out that some of my complaints about the lack of horizontal bars were because of the wasted space, especially with the new widescreen displays coming out. In retrospect, I agree that its useful to only have one bar on widescreen displays or because it takes up so much space. The &#8220;one glance&#8221; aspect I get from my status bars sure helps me, however, so I'll define this as just a preference.

benji.weber@gmail.com pointed out his installation time was much shorter than mine. I'm not sure how he got this, but I installed from DVD offline so maybe its a bit related. He also mentioned that there are many more users testing KDE over GNOME. I suppose this might be the case for openSUSE, but overall, I think that number is pretty evenly split between the two major desktops.

Thank you all for your wonderful comments, I really appreciate the contrasting views and look forward to the next round of comments.

As I didn't use openSUSE as much yesterday and today, so I have a little less to report:

**GOOD**

  * YaST is growing on me, but I'm still adjusting to living in this world. Its still not my favorite tool _(0)_
  * Suspend works like a charm. Although this also works in Fedora. _(+1)_

Positive Score: **+1**

**BAD**

  * The YaST printer tool does not deliver reliable results when setting up printers. YaST discovered my printer, but failed to deliver the correct IP address _(-1)_
  * My bluetooth mouse is still not working, even after following several good tutorials I found online. As per this tutorial from Andrew Jorgensen, I already have the bluez-gnome and bluez-utils from the GNOME Community repository installed. Not sure why, but it looks this one will have to wait for an update, whenever that occurs. _(0)_
  * Enabling the fingerprint reader only asks me for files. I thought that was odd, clicking on the help indicates that providing files from another installation that uses the fingerprint reader will set it up. I didn't see a way to set this up from scratch with openSUSE in YaST, however. _(-1)_

Negative Score: **-2**

Total Score for the last two days: **-1** (not bad for day two, you never know, I might actually give a positive score by the end&#8230;)

Overall score: **-6**

**PREFERENCES**

  * I still prefer the **system-config-*** tools from Fedora over YaST. I don't like its interface and it still seems to be unfriendly. I do think that its much improved over the original YaST I used back in SUSE 10.0