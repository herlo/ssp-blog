---
title: 'Thunderbird 2.0 – Fedora Core 6'
author: herlo
layout: post
date: 2007-05-19T05:32:43+00:00
url: /2007/05/18/thunderbird-20-fedora-core-6/
categories:
  - Install
  - Mail
  - Releases
  - Tech
  - Tools

---
So, I recently installed Thunderbird 2.0 on my Fedora Core 6 box. Here is what I did to get it working:

`# yum --enablerepo=development list thunderbird`
  
`. . . snip . . .`
  
`Available Packages`
  
`thunderbird.i386                         2.0.0.0-1.fc7          development`

`# yum -y --enablerepo=development update thunderbird`
  
`. . . snip . . .`
  
`Updated: thunderbird.i386 0:2.0.0.0-1.fc7`
  
`Complete!`

The great thing is Thunderbird 2.0 comes with some really cool features which I have completely enjoyed:

  * Save searches as folders
  * Type as you go search in the message body
  * GMail and .mac accounts in two clicks
  * Custom message tags

This is also fun to write as a comparison to the <a href="http://ubuntu-tutorials.com/2007/05/18/manually-install-thunderbird-2-ubuntu-704/" target="_blank">Thunderbird installation on Ubuntu</a>.  I thought you'd like to hear the experience from another side.

Cheers,

Herlo