---
title: Cool rsync Action
author: herlo
layout: post
date: 2006-12-20T17:48:07+00:00
url: /2006/12/20/cool-rsync-action/
categories:
  - Tech
  - Tools

---
Lately, I've been uploading very large iso files up to SoftwareFor.org for an up coming release of <a target="_blank" href="http://www.softwarefor.org/">Software for Starving Students</a>. Because of this, I've been reminded of a really cool feature of **rsync**.

**rsync** can, if you ask it to, update an individual file block by block. I am not completely familiar with the details, but I believe it has something to do with comparing small sections of a file. Hashing the small sections, and deciding whether that block actually needs to be transfered up to the remote location. Here's my example:

On my box, I have one file SSS\_WIN\_2007.01.iso, it's approximately 500MB. Initially, I transfered a slightly larger file (about 520MB) up to softwarefor.org via ssh. This process took about 3 hours on my qworst dsl connection. To me this is too long for anybody to really wait, but luckily for us, it only has to happen once.

After making some serious modifications to the interface of the iso, I needed to put the iso up again, but didn't want to wait another three hours. In comes **rsync** to save the day. Because I had an older SSS\_WIN\_2007.01.iso up on softwarefor.org, and a newer one on my local box, I was able to upload only the changes (plus some negligible comparison overhead) by running the following command:

<pre># rsync -avz --progress -e ssh SSS_WIN_2007.01.iso herlo@softwarefor.org:/path/to/old/.iso/</pre>

The resulf of running this command was a transfer time of approximately 30 minutes, where ssh would surely be over 2 hours again. I am glad I can save myself that much time. Here's the output from the transfer itself.

<pre>herlo@softwarefor.org's password:
building file list ...
1 file to consider
SSS_WIN_2007.01.iso
521142272 100%  264.48kB/s    0:32:04 (xfer#1, to-check=0/1)

sent 105324111 bytes  received 142731 bytes  54294.38 bytes/sec
total size is 521142272  speedup is 4.9</pre>

Neat ain't it?

Cheers,

Clint