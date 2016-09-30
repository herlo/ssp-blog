---
title: Werewolf (Fedora 8) Upgrade in 3 Easy Steps Using yum
author: herlo
layout: post
date: 2007-11-10T07:35:03+00:00
url: /2007/11/10/werewolf-fedora-8-upgrade-in-3-easy-steps/
categories:
  - Fedora
  - Guru
  - Install
  - Releases
  - Tech
  - Tools
  - Yum
tags:
  - Fedora
  - update
  - upgrade
  - werewolf
  - Yum

---
Recently, there was a request in one of my comments on [this post][1]. The request was for an easy way to upgrade from Fedora 7 to Fedora 8. So I took this on as a bit of a challenge. I feel pretty comfortable with **yum** and I thought it would be a good and easy task.

A bit of warning here, make sure your current Moonshine ( Fedora 7 ) release is update by running **yum update**. Also, it is recommended that backups be made of files being modified. **If you don't backup the file, it may be impossible to fix in the future. YOU HAVE BEEN WARNED**

Let's upgrade Moonshine ( Fedora 7 ) to Werewolf ( Fedora 8 ) in three easy steps:

First things first, lets print out some version info:

<pre>$ cat /etc/*release
Fedora release 7 (Moonshine)
Fedora release 7 (Moonshine)</pre>

<pre>$ uname -r
2.6.23.1-21.fc7</pre>

Its easy to tell that this machine is indeed using Moonshine ( Fedora 7 ), so let's upgrade!

### Step 1 – Modify the yum repo files

Located in _/etc/yum.repos.d_ directory are where the yum repository files are stored. We need to modify one line so that **yum** will know where to look:

<pre>$ su -
# vim /etc/yum.repos.d/fedora.repo</pre>

Find the first line that starts:

<pre>mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-$releasever&arch=$basearch</pre>

and change it:

<pre>mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-8&arch=$basearch</pre>

What changed? Well, the _$releasever_ value is the current value for our version of fedora, in this case 7. By changing it to 8, it'll load the correct repositories for Werewolf (F8) instead of Moonshine (F7). Save the file, and now we're ready to move onto the next step.

### Step 1 (Alternate)

Since posting this, I've learned that another option is available. To update the repositories, its possible to install an rpm to accomplish the same as above and it won't require **Step 3**.

Choose your mirror from <http://mirrors.fedoraproject.org>. I picked University of Oregon's site because it was close to me.

<pre># rpm -Uvh \
ftp://ftp.osuosl.org/pub/fedora/linux/releases/8/Everything/i386/os/Packages/fedora-release-*.rpm</pre>

Your ftp/http line here may be different, that is fine. This command installs the updated repositories for Werewolf ( Fedora 8 )

### Step 2 – Upgrade

In this step, we just need to run (as root):

<pre># yum update
fedora               100% |===============| 2.1 kB   00:00
primary.sqlite.bz2   100% |===============| 4.9 MB   00:03
Setting up Update Process
Resolving Dependencies
.. snip ..</pre>

A few prompts will appear, after the repository data is loaded, a list of several hundred megs (possibly a gigabyte or more) of packages will be ready to install. This is the moment of truth.

<pre>Transaction Summary
============================
Install     88 Package(s)
Update     836 Package(s)
Remove       1 Package(s)

Total download size: 1.0 G
Is this ok [y/N]:</pre>

Start the download of over 800 packages (in my case) and install and update your system. If you feel a bit of trepidation, I concur. Its still exciting though, isn't it?

<pre>Is this ok [y/N]: <strong>y</strong></pre>

Now aren't you excited! In about 30-45 minutes, you'll have a newly upgraded _Werewolf_ ( Fedora 8 ).

<pre>Downloading Packages:
orca-2.20.0.1-1. 100% |=========================| 1.5 MB    00:01
.. snip ..</pre>

### Step 3 – Cleanup and Reboot

Welcome to your new Werewolf. Treat it wisely. First things first though, we need to clean up our editing from step 1:

<pre># vim /etc/yum.repos.d/fedora.repo</pre>

Find the first line that starts:

<pre>mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-8&arch=$basearch</pre>

and change it:

<pre>mirrorlist=http://mirrors.fedoraproject.org/mirrorlist?repo=fedora-$releasever&arch=$basearch</pre>

Save the file, or if you prefer, copy the backup you made over the modified repo file.

In addition, there are some items that aren't in Fedora 8 the same way they were in Fedora 7. For these, read <a href="http://fedoraproject.org/wiki/YumUpgradeFaq#head-56b13936246769f517ac488a0098d193c7fc3600" target="_blank">this guide</a>. I didn't have these problems myself, ymmv.

To get the newly updated kernel and all the new goodness of Werewolf, a reboot **is** necessary. Enjoy your new Lycanthrope on the flip side.

Cheers,

Herlo

 [1]: {{<siteurl>}}2007/11/04/upgraded-fedora-8-werewolf-is-installed/