---
title: 'POW: Codec Buddy'
author: herlo
layout: post
date: 2007-11-07T16:26:23+00:00
url: /2007/11/07/pow-codec-buddy/
categories:
  - Fedora
  - Guru
  - Install
  - POW
  - Tech
  - Tools
tags:
  - audio
  - codec buddy
  - f8
  - mp3
  - mpeg4
  - video

---
This week's Program of the Week is a bit ahead of its release. The package is Codec Buddy, and is currently slated for release in Fedora 8 tomorrow.

Codec Buddy, with a little help from the Fedora and Fluendo development teams has grown into something that **could** be great. I see Codec Buddy really helping those who want to use and play non-free media sources from within Fedora. If you are currently running rawhide, you probably already know about this, but very soon, many other people will start to understand how Codec Buddy works as well.

One of the goals of the Fedora Project is to be free of any proprietary software. Though I don't see that many people using Fedora without at least a few proprietary components, media codecs, drivers, etc. Maybe one day&#8230;we can always hope.

To that end, I am a big media buff. I regularly watch TV shows and movies that use proprietary codecs. As an example, most people don't realize that using the reverse engineered DVD encoding provided by <a href="http://en.wikipedia.org/wiki/Jon_Johansen" target="_blank">DVD Jon</a> could be considered illegal. Fedora doesn't want to be encumbered by these risks, and truthfully, I don't blame them one bit. Considering that my backlog of mp3s and DVD rips will require an additional bit of software not normally included with Fedora, I think this is a great software solution. Give the user what they want without compromising the integrity of the project.

Codec Buddy is provided to help the average Joe understand the world of media formats. Its job was originally to provide a short description of why Fedora doesn't include this in its distribution. Then point to where one might find more information about these formats. Codec Buddy has been altered a little, but attempts to accomplish the same thing using the Fluendo website.

<a href="http://www.fluendo.com/press/releases/PR-2007-01.html" target="_blank">Fluendo</a> is the company that employs many of the individuals that work on the <a href="http://gstreamer.freedesktop.org/" target="_blank">gstreamer</a> project. Its quite a noble project, providing media codecs (installable formats) for many of the audio and video we like to use every day. Its great to have open source companies like Fluendo helping open source grow.

Codec Buddy works by launching a small application when someone tries to access a media codec not currently on the system. For instance, I've attempted to play a show I've downloaded.

<p align="left">
  Launch Totem
</p>

<p align="left">
  <a href="{{<siteurl>}}uploads/2007/10/codec-buddy-1.png" title="Opening Totem"><img src="{{<siteurl>}}uploads/2007/10/codec-buddy-1.thumbnail.png" alt="Opening Totem" /></a>
</p>

Open the file

<p align="left">
  <a href="{{<siteurl>}}uploads/2007/10/codec-buddy-3.png" title="Opening a media file"><img src="{{<siteurl>}}uploads/2007/10/codec-buddy-3.thumbnail.png" alt="Opening a media file" /></a>
</p>

Start the video

[![Start the video][1]][2]

As the video attempts to play, a prompt appears, indicating the media isn't supported. Codec buddy then provides a few options to enable playback for this particular media format.

[![Choose your codec wisely, young padawan][3]][4]

The available items are MP3 Audio Decoder, MPEG Playback Bundle and MPEG4 Part 2 Video Decoder. By default only the MP3 Audio Decoder, which is also the only codec that will be installed without payment, is checked. The other two codecs are available for a small fee, which helps Fluendo to provide these codecs.

Clicking the &#8220;Get Selected&#8221; button will immediately start the download of the MP3 Audio Decoder (if it was selected).

[![Downloading the MP3 Codec][5]][6]

A license agreement then appears, make sure to read this and if you agree, click **Accept**.

[![Agreement][7]][8]

Once the agreement is complete, its time to purchase the remaining codecs. Choose **Start Web Browser** and in a few moments, the Fluendo website should appear. This should allow you to purchase the remaining codecs needed for the video I want to watch.

[![Open Web Browser][9]][10]

The Fluendo website has a good list of available codecs beyond the choices available in Codec Buddy.

[![Fluendo website][11]][12]

The purchase will seem similar to many others on the web, add things to the cart, and pay.

Fluendo is a good start. I'm sure there will be many people interested in purchasing these codecs here. However, I believe however, that the biggest problem is that most people can get these codecs for free on Windows, Mac and even other Linux distributions. So far, the thing I feel is missing here is the explanation for **why** charge for these codecs and **who** benefits.

Fluendo is a great resource and provides some kick-ass codecs. If there is no explanation as to why we need to pay for something that one can get for free. Potential customers who don't understand the reasoning behind it might go elsewhere, or worse even, choose another distro or operating system.

I love fedora for the freedom it gives me to choose my path. I love fedora for its focus on making sure things are free and open, both monetarily and in liberty. I love fedora for trying things like Codec Buddy, I want it to succeed. I hope that with a few suggestions, both fedora and Fluendo can make Codec Buddy the informational tool that it was originally intended.

Cheers,

Herlo

 [1]: {{<siteurl>}}uploads/2007/10/codec-buddy-2.thumbnail.png
 [2]: {{<siteurl>}}uploads/2007/10/codec-buddy-2.png "Start the video"
 [3]: {{<siteurl>}}uploads/2007/10/codec-buddy-6.thumbnail.png
 [4]: {{<siteurl>}}uploads/2007/10/codec-buddy-6.png "Choose your codec wisely, young padawan"
 [5]: {{<siteurl>}}uploads/2007/10/codec-buddy-7.thumbnail.png
 [6]: {{<siteurl>}}uploads/2007/10/codec-buddy-7.png "Downloading the MP3 Codec"
 [7]: {{<siteurl>}}uploads/2007/10/codec-buddy-8.thumbnail.png
 [8]: {{<siteurl>}}uploads/2007/10/codec-buddy-8.png "Agreement"
 [9]: {{<siteurl>}}uploads/2007/10/codec-buddy-9.thumbnail.png
 [10]: {{<siteurl>}}uploads/2007/10/codec-buddy-9.png "Open Web Browser"
 [11]: {{<siteurl>}}uploads/2007/10/codec-buddy-10.thumbnail.png
 [12]: {{<siteurl>}}uploads/2007/10/codec-buddy-10.png "Fluendo website"