---
title: An alternate way to rotate photos
author: herlo
layout: post
date: 2006-11-29T03:45:41+00:00
url: /2006/11/28/an-alternate-way-to-rotate-photos/
categories:
  - Tech
  - Tools

---
So <a target="_blank" href="http://www.tuxgirl.com">TuxGirl</a> and I got into a bit of a discussion the other day about rotating images. In her <a target="_blank" href="http://www.tuxgirl.com/archive.php?id=29">post</a>, she found a cool tool called Exifautotran, which is a cool way to rotate images easily, and I am sure it has a few other cool features. I'll admit, I've never used it myself, because ImageMagick does everything for me, and so I commented on her blog and told her so&#8230;.

<span style="font-weight: bold">Me: </span>Did you also know that ImageMagick can rotate your images? I believe it's the 'convert' tool as I've rotated many images with it. In fact, at one time I wrote a very nice script that would detect the rotation, then rotate accordingly. Clint

<span style="font-weight: bold">TuxGirl</span>: Clint: that was what I was planning on using to do the rotation, but I wanted something that would automatically detect whether the image needed to be rotated. I didn't see that option available in ImageMagick, although it's possible that I just missed it.

In fact, it would be easily missed if I hadn't taken the time a few months back to figure it out. It's as simple as Exifautotran, but as we all should know ImageMagick has many features we've grown to love. Here is the simple command I ran to rotate a photo from my digital camera.

<pre>$ convert -auto-orient IMG_1860.JPG IMG_1860a.JPG</pre>

Pretty easy if you ask me. I do have to admit that it's simple enough to run Exifautotran to perform this function on a bunch of images in one directory and automatically rotate them. That's definitely cool, and now you have two choices for your rotating needs.

Isn't Open Source great!

Cheers,

Clint