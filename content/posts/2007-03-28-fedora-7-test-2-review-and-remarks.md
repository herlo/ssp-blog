---
title: Fedora 7 Test 2 Review and Remarks
author: herlo
layout: post
date: 2007-03-29T04:41:01+00:00
url: /2007/03/28/fedora-7-test-2-review-and-remarks/
categories:
  - Install
  - News
  - Releases
  - Tech

---
**So pretty, so very pretty!**

At least the install is quite pretty. The new look and feel of Fedora 7 is definitely nice. I did, however notice a couple things that I didn't like. It wasn't immediately obvious how to pass commands on the Anaconda boot line.  After a little looking around, I discovered that hitting the _tab_ key will allow you to edit the boot line.

**One device standard to rule them all**

It's been a long time coming and now Fedora 7 is running the 2.6.20 kernel with _libata_ activated, all of the hard drives on my systems will now be referred to as a consistent **/dev/sd**. No more **/dev/hd**! Isn't that great! This will definitely come in handy when writing kickstart files and mounting drives.

**Fastest 'user switching' in town!
  
** 

Although it broke a little for me, it was easy to switch from user _clints_ to another user quite easily. It only took about 3 seconds and I had to enter the password for my other users. In addition, there are some glitches in the switching back and forth.

**Let's see what they give us tomorrow**

Tomorrow is the release of Fedora 7 Test 3. I expect big improvements over Test 2. Go ahead and get the new release. It should be announced anytime now. Download the Test 3 release tomorrow (hopefully) at <a href="http://torrent.fedoraproject.org/" target="_blank">http://torrent.fedoraproject.org/</a>.

Cheers,

Herlo