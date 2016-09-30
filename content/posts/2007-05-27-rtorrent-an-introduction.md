---
title: 'rtorrent – An introduction'
author: herlo
layout: post
date: 2007-05-27T20:09:08+00:00
url: /2007/05/27/rtorrent-an-introduction/
categories:
  - Tech
  - Tools

---
Recently, I've been asked a few times how to use <a href="http://libtorrent.rakshasa.no/" target="_blank">rtorrent</a> so I thought it time to introduce it to others who might be interested in configuring my favorite bittorrent client.

First off, this is a Fedora tutorial, but much of what you'll see in this tutorial is applicable to just about any Linux distro.

**rtorrent** is a ncurses based (meaning text user interface) client for bittorrent downloading. I've used bittorrent for a few years now and run a couple trackers of my own as well.

Getting **rtorrent** is quite simple:

`# yum install rtorrent`

This provides you the **rtorrent** binary, some documentation and an sample _.rtorrent.rc_ file which we'll use later on to make it easier to configure **rtorrent** to start it's torrents automatically. So far the file list is about 7, but that's what makes **rtorrent** great.

`# rpm -ql rtorrent<br />
/usr/bin/rtorrent<br />
/usr/share/doc/rtorrent-0.6.4<br />
/usr/share/doc/rtorrent-0.6.4/AUTHORS<br />
/usr/share/doc/rtorrent-0.6.4/COPYING<br />
/usr/share/doc/rtorrent-0.6.4/INSTALL<br />
/usr/share/doc/rtorrent-0.6.4/README<br />
/usr/share/doc/rtorrent-0.6.4/TODO<br />
/usr/share/doc/rtorrent-0.6.4/rtorrent.rc.example<br />
/usr/share/man/man1/rtorrent.1.gz`

Now that **rtorrent** is installed, there's some knowledge your going to need to get it started. Once you've played with **rtorrent** for a while, you'll feel right at home with all of the keystrokes you are about to learn.

Simply start **rtorrent**:

`$ rtorrent`

A screen appears something like this:

<a href="{{<siteurl>}}uploads/2007/05/rtorrent.png" target="_nothere" title="rtorrent - main"><img src="{{<siteurl>}}uploads/2007/05/rtorrent.thumbnail.png" alt="rtorrent - main" /></a>

I tend to use <a href="http://ubuntu-tutorials.com/2007/05/04/command-line-multitasking-with-screen/" target="_blank"><strong>screen</strong></a> with **rtorrent** so you may be interested in this as well. **screen** provides the extra functionality of closing the window and reconnecting to **rtorrent** at will.

The keystrokes you need to learn will come in two parts. One set for starting the download and one for maintaining the downloads and uploads. Lets start with the former.

1, 2, 3, 4, 5, 6, 7 – Each of these keys represent a different _view_ inside **rtorrent**. The _view_s are main, sort by name, started, stopped, complete, incomplete and hashing respectively.

Enter – Will allow you to load a particular torrent into **rtorrent**. Once you do this, you'll get the following prompt:

`load>`

Enter the filename of the torrent you'd like to download. URLs are accepted as well

`load> /home/clints/SSS_WIN_2007.01.torrent`
  
`load> http://mirrors.xmission.com/softwarefor.org/iso/SSS_WIN_2007.01.torrent`

Once you have the torrent loaded, you'll need to start it up. This requires the up and down arrow keys. Because this part is a little bit tricky, you'll need to play around with it to get a feel for it. Try just hitting the down arrow, you should see something like this:

[![Selecting a torrent][1]][2]

Once you've selected it, the three vertical * (asterisks) will appear next to your selection. Starting and stopping the torrent can easily be done:

_Ctrl-s_ – Start the torrent
  
_Ctrl-d_ – Stop the torrent

Once the torrent file is running, it should connect to the appropriate tracker and start the download to the directory where **rtorrent** was invoked. Now that the torrent is started, its easy to manage using the following keystrokes. Mind you, these are global controls:

a, s, d – Increase the _upload_ speed by 1, 5, 50 Kb/s respectively.
  
z, x, c – Decrease the _upload_ speed by 1,5,50 Kb/s respectively.
  
A, S, D – Increase the _download_ speed by 1,5,50 Kb/s respectively.
  
Z, X, C – Decrease the _download_ by 1,5,50 Kb/s respectively.

In all honesty, this is as simple as it gets, but there's more you can do. In one of my next posts, I'll cover the .rtorrent.rc file and some other advanced features of **rtorrent**. Until then, enjoy the coolest tool for downloading your torrents.

Cheers,

Herlo.

 [1]: {{<siteurl>}}uploads/2007/05/rtorrent-select.png
 [2]: {{<siteurl>}}uploads/2007/05/rtorrent-select.png "Selecting a torrent"