---
title: 'LVM – From Failure to Recovery'
author: herlo
layout: post
date: 2006-09-15T17:42:03+00:00
url: /2006/09/15/lvm-from-failure-to-recovery/
categories:
  - Tech
  - Tools

---
Recently, our LVM died, yes, our 2.2TB (Terabytes, that's right!) LVM died. How did it die you ask? Simple, with a little lack of luck, a little bit of idiocy and a little trial and error. This is the story of how not to fail disks and the recovery that was required.

<span style="font-weight: bold">The Story</span>

So one seemingly happy night last week, my roommate Chris and I were each in our own office, watching television as might be normal. I was also copying the 9 seasons of the x-files I had just obtained over to our file server, named &#8220;rhubarb&#8221;. Everything is stored on LVM (with 2 underlying raid5 configs, one software – 750G, one hardware – 1.45TB) which resides at /dev/LVM/BigDisk, and we affectionately refer to it as &#8220;BigDisk&#8221; or &#8220;rhubarb&#8221;.

During this watching and copying that was going on, out of the blue, the show I was watching from BigDisk stopped showing. Being later in the evening (around 11pm I believe), and because I wanted to watch the rest of the episode of Ed, I tried to restart it. No Luck!

After trying several other methods which did not include my movement from the room I was in, I decided that it'd be okay to run downstairs to have a look. So I threw on some clothes and headed downstairs hoping for some sort of quick fix to get my episode of Ed to restart.

On my way down the stairs, Chris, hollered at me and asked if I'd done anything to rhubarb. I said I hadn't and then proceeded downstairs. This, my friends, is where the hilarity ensues, and I highly recommend against what I did that night.

<span style="font-weight: bold">The Error</span>

It appeared everything was in working order, but it obviously wasn't. Hard drives appeared to be spinning but some weren't. After some digging and realizing we couldn't access the LVM (formatted in jfs, btw). We decided it was time to do a reboot and see what was going on with the LVM. Normally, I don't reboot, so a good 20 minutes went by before any sort of thoughts went that way.

The reboot revealed a power supply had failed. At the time, we had 3 different power supplies providing power to all of the different drives in the system. We weren't sure which ones had failed, so we started eliminating them, one-by-one. Problem was, we didn't really have any reliable power supplies with which to test, and this was my biggest mistake. Yes, I take full credit for what happened next, it was a very idiotic move, so don't you do it. Mind you, these are IDE drives all setup on a software raid 5, over 4 disks. We found a couple other power supplies and hooked them up.

Nothing erroneous happened, no problems, the drives were recognized on boot and it seemed okay. So it was up and running, for about 2 minutes. We restored the LVM ran jfs_fsck, and because my roommate is a Windows Admin, and it's the only way he'd done it before, the machine &#8220;needed&#8221; to be rebooted.

Nothing came up!!

I decided it would be okay to use an extender and one of the power cables from the power supply sitting right next to rhubarb. But of course, if you haven't figured it out by now, it was running!!!

I proceeded to try to power some of the drives with this power supply using the molex connector.

SHOCK!!
  
(blue light actually was visible from the molex connector to the drive)

I am pretty sure it was dead then, but dummy me, decided to continue. Because there was more than one molex connector, I decided to continue connecting the other molex up to another drive.

SHOCK!!
  
(oh boy, am I stupid, why can't I quit when I am ahead. It'd only be the morning before I could go buy a new power supply to fix the problem)

After that, nothing would come up, yes rhubarb would boot, but no BigDisk, boo hoo&#8230; No Ed!

In the aftermath of this disaster, my roommate was at least consoling. He said he probably would've done the same thing, but I still think there was no excuse. Luckily for me, that's not the end of the story.

<!--more-->

<span style="font-weight: bold">The Attempted Repair</span>

We went to the store the next day, bought an Antec TruPower 480watt power supply to replace the two we had been using. Chris modified it to allow us to use the second 12v rail as well, giving us the ability to power all of the drives off one power supply.

Once that was up, I went to work that night trying to partially recover the LVM. Remember, the two drives from my failed software RAID were still missing.

In doing so, I ran across one very good article done by Linux Journal a while back. I even have the magazine containing the article.

http://www.linuxjournal.com/article/8874 – Recovery of RAID and LVM2 Volumes

I also found this article, which details another failure of RAID and LVM, so I read through it as well.

http://codeworks.gnomedia.com/archives/2005/general/lvm_recovery/ – LVM Recovery Tale

From the LJ article above, I spent a good amount of time running dd and extracting the information for the LVM structure. I also looked in /etc/lvm/backup/ and found another definition file.

\# dd if=/dev/sda1 bs=512 count=255 skip=1 of=/tmp/lvm.out

Here are the resulting files. I've modified them some since running dd.

Initially, I decided I would try to recreate the LVM, only without /dev/md0 in the middle.

\# vgcfgrestore -f /tmp/lvm.out LVM # <a title="Here's the LVM definition file I used" target="_blank" href="{{<siteurl>}}files/lvm.out">Here's the LVM definition file I used</a>.
  
\# vgscan
  
Reading all physical volumes. This may take a while&#8230;

That didn't work, moving /dev/md0 out of the way had problems with cylinder (or extent) boundaries. No luck. Normally, you are to get an output of all of the volume groups, but no dice. Back to the drawing board.

Next, I decided that it could be feasible to recover everything prior to the location of /dev/md0 in the volume group, so I changed the LVM definition file again. Ran vgcfgrestore and vgscan as well. Because it was about half the size of the original LVM, I decided to call it LVH and the logical volume HalfDisk.

\# vgcfgrestore -f /tmp/lvm2.out LVH # <a title="Here's the LVM definition file I used" target="_blank" href="{{<siteurl>}}files/lvm2.out">Using a different LVM definition file</a>.
  
\# vgscan
  
Reading all physical volumes. This may take a while&#8230;
  
Found volume group &#8220;LVH&#8221; using metadata type lvm2
  
\# vgchange LVH -a y
  
\# lvscan
  
ACTIVE '/dev/LVH/HalfDisk' [798.51 GB] inherit

Well, I got a little further, so I attempted to mount it, maybe it would work.

\# mount /dev/LVH/HalfDisk /mnt/HalfDisk
  
mount: wrong fs type, bad option, bad superblock on /dev/LVM/BigDisk,
  
missing codepage or other error
  
In some cases useful info is found in syslog – try
  
dmesg | tail or so

Running jfs\_fsck complained that the superblock was unrecoverable. A little closer, but still no success. I spent some time messing around with jfs\_debugfs and jfs_tune to try to tweak the data, but none of it was really successful, though I learned some cool stuff about how to manipulate bits. Finally, around 11:30 that night, I gave up and went to bed.

A couple of days went by, mainly we were waiting for one of the failed drives to return from RMA.

<span style="font-weight: bold">The Real Recovery</span>

Finally, the drive came in, Chris tried to setup a broken RAID 5 set in the same location (/dev/md0), but couldn't get it working. He settled for a RAID 0 set of three drives, totaling very closely to the original drives. It turns out, it didn't matter what the RAID was as long as it was close.

I went to work that evening. First I had to figure out how to get the new RAID array setup as if it were the old one. I tried several things, then it dawned on me, just assign the old physical volume identifier to the new one. So that's what I did.

\# pvcreate -u 6JSvVN-qLzV-YMRE-qAKk-tHv5-e32R-KA9yDk /dev/md1
  
Physical volume &#8220;/dev/md1&#8221; successfully created

Then, as before I ran vgcfgrestore this time. This time, of course, I ran it with the original LVM definitions in place, only modifying the RAID from /dev/md0 to /dev/md1.

\# vgcfgrestore -f /etc/lvm/backup/LVM LVM # <a title="{{<siteurl>}}files/lvm2.out" target="_blank" href="{{<siteurl>}}files/LVM2">Using the original LVM definition file</a>, except the software RAID is slightly different.
  
\# vgscan
  
Reading all physical volumes. This may take a while&#8230;
  
Found volume group &#8220;LVM&#8221; using metadata type lvm2
  
\# vgchange LVM -a y
  
\# lvscan
  
ACTIVE '/dev/LVM/BigDisk' [2.2 TB] inherit

After recovering the LVM (it looked successful), I tried to mount it. That didn't work.

\# mount /dev/LVM/BigDisk /mnt/BigDisk/
  
mount: wrong fs type, bad option, bad superblock on /dev/LVM/BigDisk,
  
missing codepage or other error
  
In some cases useful info is found in syslog – try
  
dmesg | tail or so

So I ran fsck on the jfs filesystem.

\# jfs_fsck /dev/LVM/BigDisk

File system object FF466998 is linked as: /Torrents/herlo1/Ed Season 3/ed – s03e22 – The Decision.mpg
  
cannot repair the data format error(s) in this file.
  
cannot repair FF466998. Will release.
  
File system object FF466999 is linked as: /Torrents/herlo1/Ed Season 3/ed.s03e22.the.decision-ftv.mpg
  
cannot repair the data format error(s) in this file.
  
cannot repair FF466999. Will release.
  
File system object DF467008 is linked as: /Torrents/herlo1/ED – Complete Season 4
  
Fileset object DF475168: No paths found.
  
File system object FF479235 is linked as: /Torrents/herlo1/Good Eats – Season 1/Good Eats – S01E03 – The Egg Files [digitaldistractions].avi
  
cannot repair the data format error(s) in this file.
  
cannot repair FF479235. Will release.
  
File system object FF479240 is linked as: /Torrents/herlo1/Good Eats – Season 1/Good Eats – S01E08 – Gravy Confidential [digitaldistractions].avi
  
cannot repair the data format error(s) in this file.
  
cannot repair FF479240. Will release.
  
File system object FF483329 is linked as: Andromeda.1&#215;01.Under.The.Night.[WS.DVDRip.XviD.AC3-TyR].avi
  
cannot repair the data format error(s) in this file.
  
cannot repair FF483329. Will release.
  
File system object FF483330 is linked as: Andromeda.1&#215;02.An.Affirming.Flame.[WS.DVDRip.XviD.AC3-TyR].avi
  
cannot repair the data format error(s) in this file.
  
cannot repair FF483330. Will release.
  
File system object FF487427 is linked as: /Torrents/herlo1/24.Season.1.DVDRip.XViD-FoV/24.1&#215;03.2.00.am\_3.00.am.ac3.dvdrip\_ws_xvid-fov.avi
  
cannot repair the data format error(s) in this file.
  
cannot repair FF487427. Will release.
  
**Phase 5 – Check Connectivity
  
**Phase 6 – Perform Approved Corrections
  
97 directories reconnected to /lost+found/.
  
383 files reconnected to /lost+found/.
  
**Phase 7 – Rebuild File/Directory Allocation Maps
  
**Phase 8 – Rebuild Disk Allocation Maps
  
2292355072 kilobytes total disk space.
  
48527 kilobytes in 13287 directories.
  
1136550438 kilobytes in 144517 user files.
  
0 kilobytes in extended attributes
  
71301657 kilobytes reserved for system use.
  
1084551504 kilobytes are available for use.
  
Filesystem is dirty.

So I ran it again.

\# jfs_fsck /dev/LVM/BigDisk
  
jfs_fsck version 1.1.7, 22-Jul-2004
  
processing started: 9/14/2006 0.50.37
  
Using default parameter: -p
  
The current device is: /dev/LVM/BigDisk
  
Block size in bytes: 4096
  
Filesystem size in blocks: 573088768
  
**Phase 0 – Replay Journal Log
  
**Phase 1 – Check Blocks, Files/Directories, and Directory Entries
  
**Phase 2 – Count links
  
**Phase 3 – Duplicate Block Rescan and Directory Connectedness
  
**Phase 4 – Report Problems
  
File system object DF2 is linked as: /
  
Errors detected in Directory Index Table. Will Fix.
  
File system object DF4100 is linked as: /Movies
  
Errors detected in Directory Index Table. Will Fix.
  
.. snip ..
  
File system object DF4117 is linked as: /lost+found/D004099.RCN/Season 3
  
File system object DF483328 is linked as: /lost+found/D483328.RCN
  
Errors detected in Directory Index Table. Will Fix.
  
**Phase 5 – Check Connectivity
  
**Phase 6 – Perform Approved Corrections
  
**Phase 7 – Rebuild File/Directory Allocation Maps
  
**Phase 8 – Rebuild Disk Allocation Maps
  
2292355072 kilobytes total disk space.
  
48427 kilobytes in 13287 directories.
  
1205764266 kilobytes in 144517 user files.
  
0 kilobytes in extended attributes
  
482169 kilobytes reserved for system use.
  
1086157064 kilobytes are available for use.
  
Filesystem is clean.

WooHoo!! A clean filesystem!

I attempted a mount to see what was left of my drive.

\# mount /dev/LVM/BigDisk /mnt/BigDisk/

Success!!

\# ls -l /mnt/BigDisk/
  
total 40
  
drwxrwxrwx 16 otis 100 1 Jan 20 2006 Audio
  
drwx–– 99 root root 1 Sep 14 00:49 lost+found
  
drwxrwxrwx 3 otis 100 1 Aug 2 23:02 Movies
  
drwxrwxrwx 5 root 100 1 Sep 4 22:12 Torrents
  
\# ls -l /mnt/BigDisk/Torrents/
  
total 904
  
drwxrwxrwx 2 nobody nobody 16 Nov 9 2005 CentOS-4.1-i386-binDVD1
  
lrwxrwxrwx 1 root root 6 May 6 00:19 herlo -> herlo1
  
drwxrwxrwx 10 nobody nobody 1 Sep 6 23:03 herlo1
  
drwxrwxrwx 2 nobody nobody 1 Jul 26 20:17 jfinkx

\# ls -l /mnt/BigDisk/Torrents/herlo1/
  
total 6440896
  
drwxr-xr-x 2 nobody nobody 1 Sep 3 23:36 24.Season.1.DVDRip.XViD-FoV
  
-rwxrwxrwx 1 nobody nobody 365928448 Aug 21 06:40 30 Days – Immigration.avi
  
drwxrwxrwx 2 nobody nobody 1 Sep 4 22:26 ED – Complete Season 4
  
drwxrwxrwx 2 nobody nobody 4096 Aug 20 03:26 Ed Season 3
  
drwxrwxrwx 2 nobody nobody 16 Jul 9 07:22 fc6-test1-dvd-i386
  
drwxrwxrwx 2 nobody nobody 1 Aug 21 03:43 Good Eats – Season 1
  
drwxrwxrwx 2 nobody nobody 1 Aug 13 01:58 Lost Season 2
  
. . snip . .
  
-rwxrwxrwx 1 nobody nobody 453132288 Aug 18 23:22 ubuntu-6.06.1-server-i386.iso
  
-rwxrwxrwx 1 nobody nobody 727588864 Jul 9 08:05 ubuntu-6.06-alternate-amd64.iso
  
-rwxrwxrwx 1 nobody nobody 725923840 Jun 25 02:38 ubuntu-6.06-alternate-i386.iso
  
-rwxrwxrwx 1 nobody nobody 732846080 Jun 9 21:58 ubuntu-6.06-desktop-amd64.iso
  
-rwxrwxrwx 1 nobody nobody 731744256 Jul 9 07:34 ubuntu-6.06-desktop-i386.iso
  
-rwxrwxrwx 1 nobody nobody 449359872 Jul 9 07:26 ubuntu-6.06-server-amd64.iso
  
-rwxrwxrwx 1 nobody nobody 452603904 Jul 9 07:11 ubuntu-6.06-server-i386.iso

What appears to be recovered is everything after the software RAID that failed. Nothing before. This means we lost several hundred gigs of data. Here's the disk information:

\# df -h
  
Filesystem Size Used Avail Use% Mounted on
  
/dev/hdc2 35G 6.8G 27G 21% /
  
/dev/hdc1 99M 15M 80M 16% /boot
  
/dev/shm 506M 0 506M 0% /dev/shm
  
/dev/mapper/LVM-BigDisk
  
2.2T 1.2T 1.1T 53% /mnt/BigDisk

We recovered about half of what we had on the drive. Before it crashed it was pretty full. Well, back to downloading more stuff&#8230;.and getting back what we lost.

**BUT WAIT!!**

Before I went to bed, I was reading what I had copied from output and had noticed that many things were being recovered into the 'lost+found' directory. One of the things I had on this drive was many (almost all) of my pictures. I'd planned on backing them up, (and some I had) but hadn't done the work yet (bad Clint, bad boy!!) so I was excited to see that many of my images had been recovered!!

\# cd lost+found/; ls -lR * | grep -i jpg | grep -i IMG
  
-rwxrwxrwx 1 root users 35115 Nov 15 2005 IMG_0450.JPG
  
-rwxrwxrwx 1 root users 34584 Nov 15 2005 IMG_0451.JPG
  
-rwxrwxrwx 1 root users 64155 Nov 15 2005 IMG_0452.JPG
  
-rwxrwxrwx 1 root users 62216 Nov 15 2005 IMG_0453.JPG
  
-rwxrwxrwx 1 root users 68744 Nov 15 2005 IMG_0454.JPG

<span style="font-weight: bold">Moral of the story&#8230;</span>

Don't do what I did, get a backup system. This article is a fairly happy article, I have heard many a horror story about data loss and crashing hard drives. I got lucky, in fact, this week, I am making sure to implementing backup, so we don't have a repeat of this scenario.