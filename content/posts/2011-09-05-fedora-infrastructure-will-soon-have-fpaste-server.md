---
title: Fedora Infrastructure will soon have fpaste-server
author: herlo
layout: post
date: 2011-09-06T01:52:20+00:00
url: /2011/09/05/fedora-infrastructure-will-soon-have-fpaste-server/
categories:
  - Fedora
  - fpaste-server
  - Geek
  - Guru
  - Tech
  - Tools
tags:
  - Fedora
  - fedorahosted
  - fpaste
  - fpaste-server
  - python
  - rpm
  - trac
  - Yum

---
Today, I deployed the latest [fpaste-server][1] package on a [development box][2] within Fedora Infrastructure.

## Test fpaste-server

I'd like to get some folks to hit it and do some testing. If you have time, I would love it if you could take a moment, read below and help.

### On the development server

To help, just point your browser to <http://paste01.dev.fedoraproject.org/> and add some pastes. In fact, it should be pretty sturdy. If you do happen to find a bug, please [file it][3] on our [fedorahosted.org Trac instance][4].

### Roll your own

Another way to help is to install your own instance of [fpaste-server][5]. I've posted some [simple installation instructions][6] for anyone who is interested.

We are always looking for helpers to make fpaste-server better. Please contact me (herlo AT fedoraproject doT Org) if you are interested in helping improve or maintain this simple and fun project.

Cheers,

herlo

 [1]: http://koji.fedoraproject.org/koji/packageinfo?packageID=11844
 [2]: http://paste01.dev.fedoraproject.org/
 [3]: https://fedorahosted.org/fpaste-server/newticket
 [4]: https://fedorahosted.org/fpaste-server
 [5]: https://fedorahosted.org/fpaste-server/
 [6]: https://fedorahosted.org/fpaste-server/browser/INSTALL.rst