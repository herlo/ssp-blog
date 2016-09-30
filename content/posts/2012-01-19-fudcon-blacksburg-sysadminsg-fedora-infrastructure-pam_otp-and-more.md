---
title: 'FUDCon Blacksburg: sysadminSG, Fedora Infrastructure, pam_otp and more!'
author: herlo
layout: post
date: 2012-01-19T19:47:01+00:00
url: /2012/01/19/fudcon-blacksburg-sysadminsg-fedora-infrastructure-pam_otp-and-more/
categories:
  - Fedora
  - FUDCon
  - News
  - Tech
  - Tools
tags:
  - 2012
  - Fedora
  - fudcon
  - infrastructure
  - January
  - pam_otp
  - puppet
  - SysadminSG

---
Well, [FUDCon Blacksburg][1] has come and gone. I believe it was the most productive I've been at a FUDCon EVER! I was able to get quite a bit accomplished and much more than I had planned!

What was it that I did, you ask? Well let me tell you all of the tasks I was able to complete.

### System Administration Study Group

Over the past year, I've been working on a way to do a regular free study group for those who want to improve their system administration skills, get certified, or just brush up on something they didn't quite understand.

Enter [sysadminSG][2], a self-guided tour of many of the standard tasks any system administrator should know. The main goal was to create an instance of a Fedora 14 machine for studiers to use.

Some of the tasks on the study sheets indicate certain issues that would need to be resolved which can't be resolved without a 'master' instance. I was able to recruit a couple of excellent individuals to help get this further than I thought it would. [Jon Stanley][3] and [Ivan Makfinsky][4] helped put together many of the pieces which will help studiers get more done. Specifically, an ldap server for centralized authentication and iscsi target luns for use with LUKS encryption, LVM and disk partitioning.

### Fedora Infrastructure

I attended the Fedora Infrastructure session, where we covered two major things of concern. One was removing the puppet staging branch and moving everything into 'Production'. This is a mental shift for many, but makes sense because in truth, everything maintained from an infrastructure perspective is production.

Additionally, a longer term plan of being able to spin up 'staging' environments for any new things that will go into production looks to be the direction we'll be going. Many of the applications we have in Fedora require some work to get us to this point, mostly so they can be more atomic pieces. I think a proof of concept environment will provide us with an good idea of how much work will be involved.

### pam_otp

After the Fedora Infrastructure hackfest, there was a two-factor authentication hackfest. We discussed using [Yubikeys][5] and a unique PIN together for authentication within Fedora. The initial goal was determined to setup sudo authentication for sysadmin-main group with two-factor authentication.

[Nathaniel McCallum][6] found the pam_otp library and was able to get it to compile. He passed it on to me to test and document it, which I was able to get working after a drunk night by the fire. I was then able to document the usage of it and have a test rpm that we'll be using.

All in all, it was a very productive weekend and more work will be getting done over the next few weeks as well. It's all very exciting and fun, a really good reason for attending FUDCon!

Cheers,

Herlo

 [1]: https://fedoraproject.org/wiki/FUDCon:Blacksburg_2012
 [2]: https://fedoraproject.org/wiki/System_Administration_Study_Guide
 [3]: http://blog.jds2001.org/random_thoughts/
 [4]: http://www.sparsebrain.com/
 [5]: http://yubico.com/yubikey
 [6]: http://nathaniel.themccallums.org/blog/