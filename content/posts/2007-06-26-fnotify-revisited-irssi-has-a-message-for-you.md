---
title: 'fnotify Revisited – irssi has a message for you'
author: herlo
layout: post
date: 2007-06-27T02:37:47+00:00
url: /2007/06/26/fnotify-revisited-irssi-has-a-message-for-you/
sociableoff:
  - 'false'
categories:
  - irssi
  - News
  - Releases
  - Tech
  - Tools
tags:
  - fnotify
  - irssi
  - scripting

---
I've debated this for some time. How long should it be to be notified of an instant message (IM), or private message (PM), or someone saying your name in internet relay chat (IRC)? I've still not answered this question, but I've got at least a tool that will help you when <a href="http://irssi.org" target="_blank">irssi</a> receives a message directly to you.

This tool was first described to me <a href="http://thorstenl.blogspot.com/2007/01/thls-irssi-notification-script.html" target="_blank">here</a>. And I blogged about it <a title="Fedora People Rule" href="{{<siteurl>}}2007/03/20/fedora-people-rule/" target="_blank">in this previous post</a>. The general idea is to set up an irssi script that will write out data to a file. That file, in turn was read by the **tail** command over **ssh** and a notification window would appear anytime a new message was sent directly to you.

That capability hasn't changed. Instead, I'm trying to improve how that is done. In the old way, a persistent **ssh** connection was needed to tail the file on the remote machine running **irssi**. This caused headaches and problems; some were easy to deal with, others much harder. I think for the most part, I've addressed these issues.

What does the new script do you ask? Well, the perl part from the original hasn't changed, the other script have changed, however. Its been divided up into two scripts in fact. The original script **irssi-script.sh** now obtains the flat file written by the **irssi** _perl_ plugin using a cron job that runs every minute. The new file **fnotify.sh** will run every 10 seconds and check to see if the flat file has been downloaded. Once it detects a new file, it will display the contents of that file as messages using the notify-send tool.

All of the scripts are available as a tarball from <a title="fnotify svn repository" href="http://www.herlo.org/fnotify" target="_blank">http://www.herlo.org/misc/fnotify</a>[.tar.bz2][1]. Please feel free to check it out as its set up for anonymous checkout.

I've provided a README and an INSTALL file which should help you get the script set up for you. Please send an email to clints At UToS . OrG or comment here on the blog with any questions and I'll happily try to help.

Back to my original question. How long should it take? Will you let me know?  Currently, this script can take as long as 1 minute 10 seconds to send notification of a message.  Is this too long?

Thank you,

Herlo

 [1]: http://herlo.org/misc/fnotify.tar.bz2