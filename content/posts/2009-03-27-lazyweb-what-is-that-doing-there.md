---
title: 'LazyWeb: What is that . doing there?'
author: herlo
layout: post
date: 2009-03-28T04:34:51+00:00
url: /2009/03/27/lazyweb-what-is-that-doing-there/
sociableoff:
  - 'false'
categories:
  - Conferences
  - Fedora
  - Filesystems
  - Guru
  - Releases
  - Tech
tags:
  - Fedora
  - Filesystems
  - linux
  - permissions
  - rawhide

---
So tonight I was sitting there tonight getting ready to setup cobbler for another installation source, and I noticed something very odd.

`# ls -l /root<br />
total 88<br />
-rw-------. 1 root root  1176 2008-11-23 17:22 anaconda-ks.cfg<br />
drwxr-xr-x. 2 root root  4096 2008-12-14 18:37 bin`

See the . ? Where you ask?  Look closer!

drwxr-xr-x. <– look, there it is!!  At first, I thought it was just one file, but then I noticed it other places, then I looked further, and it seems to be everywhere.

What is up with that? Where does this come from?  What is it for?  LazyWeb, can you help me?

Cheers,

Herlo