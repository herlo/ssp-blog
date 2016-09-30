---
title: 'sfdisk – My new Saving Grace'
author: herlo
layout: post
date: 2007-03-16T16:55:27+00:00
url: /2007/03/16/sfdisk-my-new-saving-grace/
categories:
  - Recovery
  - Tech
  - Tools

---
How many of you have ever lost your data on a hard drive? I know I have, more than once. Usually, I give up on recovering the drive but this time I really couldn't.

I was installing a machine as I normally do for class, I have a removable usb drive (80GB) that I keep the installation media spooled. For some reason, this time when the installation had completed, the disk appeared to be completely wiped. I thought I was screwed. The data I had was company data which has to be saved for several months. It was important that I recover this data.

Luckily for me, the data wasn't gone, just the partition table. I hunted around the interweb for a while and struggled to find anything useful to help me recover the lost partition. After about a day and a half searching, I was about to give up, when I found <a href="http://www.linuxplanet.com/linuxplanet/tutorials/3174/7/" target="_blank">this guide</a>. The guide is a bit cryptic but nonetheless gets the job done.

This is my saving grace. I've got this tutorial bookmarked in several places now and intend on making a tutorial here on how to accomplish this as well, mainly just so I always have it available.

Now, I could have completely avoided the situation if I had backed up my partition table. And because of what had happened, I am going to show you how to back up your partition tables quickly and easily using **sfdisk**.

**sfdisk**, or scriptable **fdisk** is useful for creating partitions on the fly, or in our case, quickly backing up partition tables.

First, take a look at this partition table. Note that I have 7 partitions here:

`# fdisk -l`
  
`Disk /dev/sdc: 66 MB, 66240512 bytes`
  
`3 heads, 43 sectors/track, 1002 cylinders`
  
`Units = cylinders of 129 * 512 = 66048 bytes`

`Device Boot      Start         End      Blocks   Id  System`
  
`/dev/sdc1               1         152        9782+  83  Linux`
  
`/dev/sdc2             153         259        6901+  83  Linux`
  
`/dev/sdc3             260         305        2967   82  Linux swap / Solaris`
  
`/dev/sdc4             306        1002       44956+   5  Extended`
  
`/dev/sdc5             306         563       16640+  fd  Linux raid autodetect`
  
`/dev/sdc6             564         776       13738   fd  Linux raid autodetect`
  
`/dev/sdc7             777        1002       14576+  83  Linux`

/dev/sdc1 is mounted at /mnt and has a couple files loaded:

`# mount`
  
`..snip..`
  
`/dev/sdc1 on /mnt type ext3 (rw)`

`# ls -l /mnt`
  
`total 8353`
  
`-rw-rw-r-- 1 root root   65182 Mar 16 10:42 iah-sna.pdf`
  
`drwx------ 2 root root   12288 Mar 16 10:35 lost+found`
  
`-rw------- 1 root root 8437760 Mar 16 10:42 zlm-administrator-guide.pdf`

To back up the partition table run the following command:

`# sfdisk -d /dev/sdc > /tmp/sdc-backup.txt`

What does that produce:

``How many of you have ever lost your data on a hard drive? I know I have, more than once. Usually, I give up on recovering the drive but this time I really couldn't.

I was installing a machine as I normally do for class, I have a removable usb drive (80GB) that I keep the installation media spooled. For some reason, this time when the installation had completed, the disk appeared to be completely wiped. I thought I was screwed. The data I had was company data which has to be saved for several months. It was important that I recover this data.

Luckily for me, the data wasn't gone, just the partition table. I hunted around the interweb for a while and struggled to find anything useful to help me recover the lost partition. After about a day and a half searching, I was about to give up, when I found <a href="http://www.linuxplanet.com/linuxplanet/tutorials/3174/7/" target="_blank">this guide</a>. The guide is a bit cryptic but nonetheless gets the job done.

This is my saving grace. I've got this tutorial bookmarked in several places now and intend on making a tutorial here on how to accomplish this as well, mainly just so I always have it available.

Now, I could have completely avoided the situation if I had backed up my partition table. And because of what had happened, I am going to show you how to back up your partition tables quickly and easily using **sfdisk**.

**sfdisk**, or scriptable **fdisk** is useful for creating partitions on the fly, or in our case, quickly backing up partition tables.

First, take a look at this partition table. Note that I have 7 partitions here:

`# fdisk -l`
  
`Disk /dev/sdc: 66 MB, 66240512 bytes`
  
`3 heads, 43 sectors/track, 1002 cylinders`
  
`Units = cylinders of 129 * 512 = 66048 bytes`

`Device Boot      Start         End      Blocks   Id  System`
  
`/dev/sdc1               1         152        9782+  83  Linux`
  
`/dev/sdc2             153         259        6901+  83  Linux`
  
`/dev/sdc3             260         305        2967   82  Linux swap / Solaris`
  
`/dev/sdc4             306        1002       44956+   5  Extended`
  
`/dev/sdc5             306         563       16640+  fd  Linux raid autodetect`
  
`/dev/sdc6             564         776       13738   fd  Linux raid autodetect`
  
`/dev/sdc7             777        1002       14576+  83  Linux`

/dev/sdc1 is mounted at /mnt and has a couple files loaded:

`# mount`
  
`..snip..`
  
`/dev/sdc1 on /mnt type ext3 (rw)`

`# ls -l /mnt`
  
`total 8353`
  
`-rw-rw-r-- 1 root root   65182 Mar 16 10:42 iah-sna.pdf`
  
`drwx------ 2 root root   12288 Mar 16 10:35 lost+found`
  
`-rw------- 1 root root 8437760 Mar 16 10:42 zlm-administrator-guide.pdf`

To back up the partition table run the following command:

`# sfdisk -d /dev/sdc > /tmp/sdc-backup.txt`

What does that produce:

`` `cat /tmp/sdc-backup.txt`
  
`partition table of /dev/sdc`
  
`unit: sectors`

`/dev/sdc1 : start=       43, size=    19565, Id=83`
  
`/dev/sdc2 : start=    19608, size=    13803, Id=83`
  
`/dev/sdc3 : start=    33411, size=     5934, Id=82`
  
`/dev/sdc4 : start=    39345, size=    89913, Id= 5`
  
`/dev/sdc5 : start=    39346, size=    33281, Id=fd`
  
`/dev/sdc6 : start=    72628, size=    27476, Id=fd`
  
`/dev/sdc7 : start=   100105, size=    29153, Id=83`

Looks pretty much like what **fdisk _-l_** show, but in a slightly different format. **sfdisk** will use this file later on to recover.

Let's destroy the partition table. The **dd** command overwrites the first 512 bytes of the disk with zeros.

`# dd if=/dev/zero of=/dev/sdc bs=512 count=1`

`# fdisk -l /dev/sdc`
  
`Disk /dev/sdc: 66 MB, 66240512 bytes`
  
`3 heads, 43 sectors/track, 1002 cylinders`
  
`Units = cylinders of 129 * 512 = 66048 bytes`

`Disk /dev/sdc doesn't contain a valid partition table`

Oops, gone is the partition table. That's not good. Luckily a backup has been made, and should be able to restore it quite easily:

`# sfdisk /dev/sdc < /``tmp/sdc-backup.txt`
  
`Checking that no-one is using this disk right now ...`
  
`OK`

`Disk /dev/sdc: 1002 cylinders, 3 heads, 43 sectors/track`

`sfdisk: ERROR: sector 0 does not have an msdos signature`
  
 `/dev/sdc: unrecognized partition table type`
  
`Old situation:`
  
`No partitions found`
  
`New situation:`
  
`Units = sectors of 512 bytes, counting from 0`

   `Device Boot    Start       End   #sectors  Id  System`
  
`/dev/sdc1            43     19607      19565  83  Linux`
  
`/dev/sdc2         19608     33410      13803  83  Linux`
  
`/dev/sdc3         33411     39344       5934  82  Linux swap / Solaris`
  
`/dev/sdc4         39345    129257      89913   5  Extended`
  
`/dev/sdc5         39346     72626      33281  fd  Linux raid autodetect`
  
`/dev/sdc6         72628    100103      27476  fd  Linux raid autodetect`
  
`/dev/sdc7        100105    129257      29153  83  Linux`
  
`Warning: no primary partition is marked bootable (active)`
  
`This does not matter for LILO, but the DOS MBR will not boot this disk.`
  
`Successfully wrote the new partition table`

`Re-reading the partition table ...`

`If you created or changed a DOS partition, /dev/foo7, say, then use dd(1)`
  
`to zero the first 512 bytes:  dd if=/dev/zero of=/dev/foo7 bs=512 count=1`
  
`(See fdisk(8).)`

Remount _/dev/sdc1_ to see if the partition data is still there:

`# mount -t ext3 /dev/sdc1 /mnt`
  
`# ls -l /mnt`
  
`total 8353`
  
`-rw-rw-r-- 1 root root   65182 Mar 16 10:42 iah-sna.pdf`
  
`drwx------ 2 root root   12288 Mar 16 10:35 lost+found`
  
`-rw------- 1 root root 8437760 Mar 16 10:42 zlm-administrator-guide.pdf`

There it is! Wow, data was never lost, just hidden for a while.

This can be helpful in other ways too. Using **sfdisk** to build scripted partitions is never easier now. Just build a file from one pre-partitioned disk, modify and use it everywhere else.

Cheers,

Herlo