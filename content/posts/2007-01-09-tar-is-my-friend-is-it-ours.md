---
title: GNU tar is my friend, is it yours?
author: herlo
layout: post
date: 2007-01-09T16:34:30+00:00
url: /2007/01/09/tar-is-my-friend-is-it-ours/
categories:
  - Tech
  - Tools

---
Today, while evaluating some content at work, I came across a very neat trick I didn't know about. tar can archive or extract <a target="_blank" href="http://www.gzip.org/">gzip</a>ped, <a target="_blank" href="http://www.bzip.org/">bzip</a>ped or compressed content without using their respective switches.

First, we must have a couple correct archives:

`tar -czf projects-withz.tar.gz /share/projects/<br />
tar -cjf projects-withj.tar.bz2 /share/projects/`

`$ ls -l projects-withz.tar.*<br />
-rw-rw-r-- 1 clints clints 184819851 Jan  8 13:32 projects-withz.tar.bz2<br />
-rw-rw-r-- 1 clints clints 186552744 Jan  8 13:22 projects-withj.tar.gz`

`$ file projects*tar*<br />
projects-withz.tar.bz2: bzip2 compressed data, block size = 900k<br />
projects-withz.tar.gz:  gzip compressed data, from Unix, last modified: Mon Jan  8 13:21:52 2007`

What's interesting about this is that the `-j` and `-z` are not needed. This has actually been around for some time. The release notes where I found this stated that this feature was available in December of 2004. So here's what you can do now:

`tar -tf projects.tar.gz /share/projects/<br />
tar -tf projects.tar.bz2 /share/projects/`

See what you get. It's a nice feature that I didn't know existed, so maybe you didn't either.

Cheers,

Herlo