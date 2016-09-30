---
title: 'RAID 6 – Fedora Core 6'
author: herlo
layout: post
date: 2007-05-23T03:08:45+00:00
url: /2007/05/22/raid-6-fedora-core-6/
categories:
  - RAID
  - Tech
  - Tools

---
You've probably heard of RAID 0, RAID 1, and even RAID 5. But RAID 6?

What is Raid 6 you ask? Well, first we need to take a look at RAID 5 and understand how it works. If you understand RAID 5, then RAID 6 is an easy transition.

RAID 5 is what is referred to as a striped set with distributed [parity][1]. Essentially, the data is spread across the disk, and one bit is flipped each time a piece of data is written. This helps the RAID 5 set compute the missing data if one of the drives fails.

RAID 6 extends this concept one further by providing an additional drive for distributing the parity. Essentially, there is one more disk that can fail before data is lost. Comparing this with RAID 5, you get more redundancy. Comparing this with RAID 10 might be something you'd consider as well, but RAID 6 is better if for nothing more than the cost and efficiency.

_So_ how do you configure linux with Software RAID 6? With Fedora Core 6 and Red Hat Enterprise Linux 5, RAID 6 is easily configured. Here's how:

_Four_ disk drives are recommended (3 are required) to set up the raid, _five_ if you want a hot spare. This initial sacrifice of two (or three) drives will come in handy later on when something fails. This demonstration will use 4 512MB usb drives, sdb, sdc, sdd and sde.

First we need to partition the drives and assign them the correct partition type. As a general rule, partitioning the entire space on the disk is appropriate:

`# fdisk /dev/sdd`

Create a new partition using the entire disk:

`Command (m for help): n<br />
Command action<br />
e   extended<br />
p   primary partition (1-4)<br />
p<br />
Partition number (1-4): 1<br />
First cylinder (1-1019, default 1):<br />
Using default value 1<br />
Last cylinder or +size or +sizeM or +sizeK (1-1019, default 1019):<br />
Using default value 1019`

Change the type of the partition from the default (83 Linux):

`Command (m for help): t<br />
Selected partition 1<br />
Hex code (type L to list codes): l`

`. . . snip . . .`

`17  Hidden HPFS/NTF   64  Novell Netware    b7  BSDI fs         fd  Linux raid auto`

`Hex code (type L to list codes): fd<br />
Changed system type of partition 1 to fd (Linux raid autodetect)`

Now the device is created, lets have a look at it and write it out to the partition table:

`Command (m for help): p`

`Disk /dev/sdd: 501 MB, 501088256 bytes<br />
16 heads, 60 sectors/track, 1019 cylinders<br />
Units = cylinders of 960 * 512 = 491520 bytes`

`Device      Boot   Start              End           Blocks     Id    System<br />
/dev/sdd1                         1         1019          489090     fd    Linux raid autodetect`

`Command (m for help): w<br />
The partition table has been altered!`

Make sure to do this for each of your devices. Once that the partitions are created, we need to load the module that will support RAID 6.

`# modprobe raid6<br />
# lsmod | grep raid<br />
raid456               123985  0<br />
xor                    18249  1 raid456`

Now create the software RAID 6 device:

`# mdadm --create /dev/md0 --level=6 --raid-devices=4 /dev/sd{b,c,d,e}1<br />
mdadm: array /dev/md0 started.`

Yes, the array is started, but it does take some time to build. Try the **watch** command to show the array build in real time (almost).

`#  watch cat /proc/mdstat`

`Every 2.0s: cat /proc/mdstat                                                                                                            Tue May 22 20:12:47 2007`

`Personalities : [raid6] [raid5] [raid4]<br />
md0 : active raid6 sde1[3] sdd1[2] sdc1[1] sdb1[0]<br />
978048 blocks level 6, 64k chunk, algorithm 2 [4/4] [UUUU]<br />
[====>................]  resync = 21.3% (104760/489024) finish=23.8min speed=266K/sec`

`Personalities : [raid6] [raid5] [raid4]<br />
md0 : active raid6 sde1[3] sdd1[2] sdc1[1] sdb1[0]<br />
978048 blocks level 6, 64k chunk, algorithm 2 [4/4] [UUUU]<br />
[===================>.]  resync = 95.6% (468472/489024) finish=1.2min speed=267K/sec`

`Personalities : [raid6] [raid5] [raid4]<br />
md0 : active raid6 sde1[3] sdd1[2] sdc1[1] sdb1[0]<br />
978048 blocks level 6, 64k chunk, algorithm 2 [4/4] [UUUU]`

Make a filesystem on the new RAID 6:

`# mkfs -t ext3 -b 4096 /dev/md0<br />
. . . snip . . .`

Mount the new filesytem:

`# mkdir /storage;  mount /dev/md0 /storage`
  
`# mount`
  
`. . . snip . . .`
  
`/dev/md0 on /storage type ext3 (rw)`

Enjoy the RAID 6. Later on, I'll write another tutorial on failing and recovering this RAID 6 and other software raid devices.

RAID 6 will grow more and more as its adopted and understood, get your Software RAID 6 configured soon.

Cheers,

Herlo

 [1]: http://en.wikipedia.org/wiki/Parity_bit "Parity bit"