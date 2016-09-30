---
title: 'rtorrent – The Options'
author: herlo
layout: post
date: 2007-06-09T15:08:20+00:00
url: /2007/06/09/rtorrent-the-options/
categories:
  - Tech
  - Tools

---
A little over a week and a half ago, I wrote an <a href="{{<siteurl>}}2007/05/27/rtorrent-an-introduction/" title="rtorrent - An Introduction" target="_blank">introduction to <strong>rtorrent</strong></a> that covered the basic functionality of **rtorrent**. This tutorial should have made it easier for those of you out there to use my favorite torrent client.

Because I love **rtorrent** so much, I thought I'd share a simple way to configure this awesome tool. I'll also take the time to share a few of the command line options I use from time to time and why I value them as well.

Take a minute to look through the **rtorrent** man page. Along with some of the interactive keystrokes and functions pointed out in the <a href="{{<siteurl>}}2007/05/27/rtorrent-an-introduction/" title="rtorrent - An Introduction" target="_blank">previous post</a>, you'll find that there are many options that can actually be passed directly on the command line. Many times its much easier to use a configuration file; in this case, its called _.rtorrent.rc_ and it should be found in your home directory.

In this tutorial, I'll cover the options one by one that are regularly used. Then, I'll cover some simply cool advanced configurations that will help you manage your torrent downloads.

* * *As you might recall, I run 

**rtorrent** within screen. This affords me the ability to access it at will and pretty much run it 24/7. Because of this, I have specific upload and download speed requirements. This is where **rtorrent** really shines!All of the options covered below must be set after the **_-o_** option. The next options I am going to cover are the ones that control the speed of both the upload and the download. These should be pretty self-explanatory:**_upload_rate=50_** – Set the maximum upload rate at 50Kb/s. All active torrents will be cumulatively constrained to this limit.
  
_**download**_**__rate=250_** – Set the maximum upload rate at 250Kb/s. All active torrents will be cumulatively constrained to this limit.What does this mean for you? Well, if you have 10 torrents uploading to other peers and 5 torrents downloading, the maximum for upload will be 50Kb/s overall and 250Kb/s overall for those downloads. Executing these two options on the command line is easy:`$ rtorrent  -o upload_rate=50,download_rate=250`**rtorrent** begins and at the bottom, you should see something similar to this:</p> 

`[Throttle  50/250 KB] [Rate  49.9/ 31.4 KB] [Port: 19814]`

Now, this is nice, throttling downloads and uploads overall, but there's more.

How about setting the directory where all of the downloads will be stored? What about setting port ranges to use? And what about verifying the hash is valid of a partially downloaded file? These are all great things to have, so lets set them in our next **rtorrent** call:

`$ rtorrent  -o directory=/data/torrents/current,upload_rate=50,download_rate=250,check_hash=yes,port_range=19340-19400`

Now isn't that great!? Try saving a couple of files with this and see what you get.

Cheers,

Herlo