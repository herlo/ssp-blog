---
title: 'SCTP – a new replacement for TCP (or UDP)'
author: herlo
layout: post
date: 2007-10-09T03:12:24+00:00
url: /2007/10/08/sctp-a-new-replacement-for-tcp-or-udp/
categories:
  - Networking
  - Tech
  - Tools

---
Recently, I've been quite overwhelmed with keeping up with my latest ambition, the <a href="http://utosf.org" target="_blank">Utah Open Source Foundation</a>, which has made it a bit difficult to keep up on my blog here. I'll be doing some updates to this blog soon and you should start seeing regular updates from me here in the very near future.

In the meantime, I've got a post that may knock your sock off! If you've not yet heard about it, there's a new transport protocol on the way, and its called Stream Control Transmission Protocol (SCTP). Its an amazing new way of looking at the network, providing multi-stream transmissions through one port.

Have you ever thought it would be nice to take three network connections, one ethernet, one fiber and one wireless and bond them?  What about using those three connections to stream video?  Or to manage data on one and have a control connection on another?  TCP/UDP can't really do this for you without some external elements, but SCTP might just be the thing you're looking for, and its already here.  Currently in testing, SCTP looks to be a great replacement (augmentation) to the already popular TCP and UDP prototols.

Linux Journal is doing a 3 part series on this protocol which started in last months article: <a href="http://interactive.linuxjournal.com/article/9748" title="SCTP - An Introduction - Linux Journal" target="_blank">Introduction to Stream Control Transmission Protocol</a>.  This article is a quick look into how this protocol works.  The follow-up, in this month's issue (not yet available for non-subscribers) talks about how the protocol is implemented in the Linux kernel and even gives some good code references.

I suggest you take a look at SCTP if you've not yet heard of it.  I am very excited to see where this protocol could take us in the future.